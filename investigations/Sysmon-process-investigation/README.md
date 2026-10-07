# 🔎 Sysmon Process Investigation

## Overview

This investigation examines Windows process creation activity using **Sysmon Event ID 1** to determine whether observed process execution was legitimate or potentially suspicious.

The investigation focuses on process relationships, execution context, command-line activity, and endpoint telemetry to assess the behaviour observed on the system.

## Investigation Objective

The objective of this investigation was to:

- Analyse Sysmon process creation events
- Identify parent-child process relationships
- Examine PowerShell execution
- Review command-line and process context
- Determine whether the observed activity was suspicious
- Identify any potential indicators of compromise (IOCs)
- Document the investigation and final assessment

## Environment

| Component | Details |
|---|---|
| Operating System | Windows 10 Home |
| Monitoring Tool | Sysmon v15.21 |
| Primary Event | Sysmon Event ID 1 — Process Create |
| Log Source | Microsoft-Windows-Sysmon/Operational |
| Analysis Tools | Windows Event Viewer, PowerShell |

## Investigation Workflow

1. Identify relevant Sysmon process creation events
2. Examine the process and execution context
3. Analyse parent-child process relationships
4. Review command-line information
5. Check for suspicious behaviour or indicators of compromise
6. Determine whether the activity is legitimate or suspicious
7. Document the findings and conclusion

---

# 1. Initial Observation

A Sysmon Event ID 1 process creation event was identified for investigation.

The event provided endpoint telemetry including:

- Process image
- Process ID
- Process GUID
- Parent process information
- Command line
- User context
- Integrity level
- Timestamp

The investigation focused on understanding how the observed process was launched and whether its execution context was consistent with normal activity.

---

# 2. Process Relationship Analysis

The investigated process chain was:

```text
explorer.exe
    ↓
powershell.exe
    ↓
conhost.exe
