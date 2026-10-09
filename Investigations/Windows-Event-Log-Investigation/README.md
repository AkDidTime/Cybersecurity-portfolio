# 🔎 Windows Event Log Investigation

## Overview

This investigation analyses Windows Security Event Logs to understand authentication activity on a Windows 10 endpoint. The objective was to identify successful and failed logon events, examine their context, and determine whether the available evidence indicated potentially suspicious authentication behaviour.

The investigation used PowerShell to retrieve and filter Windows Security events, with particular focus on **Event ID 4624 (successful logon)** and **Event ID 4625 (failed logon)**.

## Investigation Objectives

* Analyse Windows authentication events.
* Identify and interpret Windows logon types.
* Examine account, process, and source-address information.
* Investigate failed logon activity and potential authentication anomalies.
* Assess whether the observed events indicated suspicious behaviour.
* Document findings and acknowledge the limitations of the available evidence.

## Environment

| Component          | Details                                      |
| ------------------ | -------------------------------------------- |
| Operating System   | Windows 10 Home                              |
| Log Source         | Windows Security Event Log                   |
| Analysis Tool      | Windows PowerShell                           |
| Primary Event IDs  | 4624 — Successful logon; 4625 — Failed logon |
| Investigation Type | Endpoint authentication log analysis         |

## Investigation Workflow

1. Retrieve successful and failed logon events.
2. Extract relevant authentication fields.
3. Analyse logon types and associated processes.
4. Review source network addresses where available.
5. Search for failed logon events and potential remote logons.
6. Assess the findings against the available evidence.
7. Document the conclusion and recommended actions.

---

## 1. Initial Log Collection

The Windows Security log was queried to retrieve recent successful and failed logon events.

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4624, 4625
} -MaxEvents 20 |
Select-Object TimeCreated, Id, Message
```

### Purpose

* Retrieve Event ID 4624, indicating a successful logon.
* Retrieve Event ID 4625, indicating a failed logon.
* Review event timestamps and message details.
* Establish which authentication events were available for further analysis.

The initial query returned multiple successful logon events. Their presence alone did not indicate suspicious activity, so the investigation examined the associated logon types and execution context.

## 2. Successful Logon Analysis — Event ID 4624

Event ID 4624 was examined to understand the context of successful authentication events.

Relevant fields included:

* Logon Type
* Account Name and Account Domain
* Process Name
* Source Network Address
* Logon Process
* Authentication Package
* Event Timestamp

The following PowerShell command was used to extract selected fields from recent successful logon events.

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4624
} -MaxEvents 20 |
ForEach-Object {
    $xml = [xml]$_.ToXml()

    [PSCustomObject]@{
        TimeCreated = $_.TimeCreated
        LogonType = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'LogonType'}).'#text'
        Account = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'TargetUserName'}).'#text'
        Process = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'ProcessName'}).'#text'
        SourceIP = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'IpAddress'}).'#text'
    }
} | Format-Table -AutoSize
```

### Logon Type Analysis

| Logon Type | Meaning           | Investigation relevance                                                                                       |
| ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------- |
| 3          | Network logon     | May warrant investigation when unexpected, especially alongside unusual source addresses or account activity. |
| 5          | Service logon     | Commonly associated with Windows services.                                                                    |
| 7          | Unlock            | Indicates a workstation unlock event.                                                                         |
| 10         | RemoteInteractive | Commonly associated with Remote Desktop logons.                                                               |
| 11         | CachedInteractive | Interactive logon using cached domain credentials.                                                            |

These logon types provide context but do not independently establish whether an event is malicious.

### Finding: Service Logon

One examined event contained the following characteristics:

* **Event ID:** 4624
* **Logon Type:** 5
* **Account:** SYSTEM
* **Process:** `C:\Windows\System32\services.exe`
* **Source Network Address:** Not populated

The SYSTEM account and `services.exe` process were consistent with normal Windows service activity. The event did not provide evidence of an external source address.

This event was assessed as consistent with expected operating system behaviour.

### Finding: Cached Interactive Logon

Another examined event contained:

* **Event ID:** 4624
* **Logon Type:** 11
* **Process:** `C:\Windows\System32\svchost.exe`
* **Source Network Address:** `127.0.0.1`

Logon Type 11 indicates a cached interactive logon. The loopback address `127.0.0.1` refers to the local computer rather than an external host.

The available fields were consistent with local authentication activity. However, the event alone was not sufficient to establish the exact user action that initiated it.

### Additional Logon Context

The extracted events also included Logon Type 7, associated with workstation unlock activity.

A separate query examined the 200 most recent successful logon events for Logon Types 3 and 10. No matching events were returned by that query.

This finding is limited to the sample examined and does not establish that network or Remote Desktop logons never occurred.

## 3. Failed Logon Analysis — Event ID 4625

Event ID 4625 was queried to identify failed authentication attempts and examine their context.

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4625
} -MaxEvents 20 |
ForEach-Object {
    $xml = [xml]$_.ToXml()

    [PSCustomObject]@{
        TimeCreated = $_.TimeCreated
        Account = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'TargetUserName'}).'#text'
        LogonType = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'LogonType'}).'#text'
        Status = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'Status'}).'#text'
        SubStatus = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'SubStatus'}).'#text'
        SourceIP = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'IpAddress'}).'#text'
        Process = ($xml.Event.EventData.Data |
            Where-Object {$_.Name -eq 'ProcessName'}).'#text'
    }
} | Format-Table -AutoSize
```

### Finding

The query returned no matching events, and PowerShell reported that no events matched the selection criteria.

No Event ID 4625 records were available in the Security log at the time of the query.

This means the investigation could not analyse failed logon patterns, source addresses, or failure status codes. It does not prove that failed authentication attempts never occurred; relevant events may be absent from the available log or outside the retained period.

## 4. Log Coverage and Investigation Scope

The Security log was checked to establish the approximate time range available for analysis.

```powershell
Get-WinEvent -LogName Security -Oldest -MaxEvents 1 |
Select-Object TimeCreated

Get-WinEvent -LogName Security -MaxEvents 1 |
Select-Object TimeCreated
```

The oldest returned event was dated **8 September 2026**, and the newest was dated **8 October 2026**.

This indicates that the available log covered approximately one month at the time of collection. Findings in this investigation are limited to the retained events and the samples queried.

## 5. Findings Summary

| Area                              | Result                                                                                                                 |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Successful logons                 | Multiple Event ID 4624 records were examined.                                                                          |
| Service authentication            | A Type 5 logon involving SYSTEM and `services.exe` was consistent with normal Windows service activity.                |
| Cached interactive authentication | A Type 11 event with `svchost.exe` and loopback address `127.0.0.1` was consistent with local authentication activity. |
| Workstation unlock                | Type 7 events were observed.                                                                                           |
| Failed logons                     | No Event ID 4625 records were returned by the query.                                                                   |
| Network and Remote Desktop logons | No Type 3 or Type 10 events were found in the sample of 200 successful logons examined.                                |
| Indicators of compromise          | No clear indicators of compromise were identified in the events examined.                                              |

## 6. Conclusion

The investigation examined Windows Security authentication events using PowerShell, focusing on successful logons, logon types, process context, source addresses, and failed authentication attempts.

The successful logon events reviewed were consistent with ordinary Windows service, cached interactive, and workstation unlock activity. No failed logon events were returned by the query, and no Type 3 or Type 10 events were identified in the sample of 200 successful logons examined.

**No clear indicators of compromise were identified in the available evidence.** However, this assessment is limited to the events and samples examined. The absence of failed logon records does not establish that no failed attempts occurred, and the investigation does not prove that the endpoint was free from compromise.

The investigation demonstrated how authentication logs can be queried and interpreted to establish context, assess potential anomalies, and document evidence-based findings.

## 7. Recommended Next Steps

* Continue monitoring Event IDs 4624 and 4625 for unusual authentication patterns.
* Investigate repeated failed logons, unexpected account activity, and suspicious source addresses if such events appear.
* Correlate authentication events with process telemetry and other available endpoint logs.
* Preserve relevant event records and screenshots during future investigations.
* Extend the investigation with a controlled lab scenario that generates clearly labelled test authentication events, if additional detection evidence is required.

## 8. Skills Demonstrated

* Windows Security Event Log analysis
* PowerShell log retrieval and filtering
* XML event-data extraction
* Authentication and logon-type analysis
* Process and source-address interpretation
* Investigation scoping and evidence assessment
* Indicator of compromise review
* Technical documentation
