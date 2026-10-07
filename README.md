# Hi, my name is Ayan Ahmed 👋

### Aspiring SOC Analyst | Cybersecurity | IT Support

I'm an aspiring **SOC Analyst** building a career in cybersecurity, with a background in IT Support and a **T Level in Digital Production, Design and Development**, awarded by Pearson.

As part of my T Level, I completed **two years of industry placement in IT Support**, gaining practical experience in a professional IT environment. My experience included endpoint management, patch remediation, remote administration, troubleshooting, PowerShell, technical documentation, and user support.

I'm now building on this foundation through hands-on cybersecurity labs, security investigations, and technical projects focused on **Security Operations, security monitoring, detection, log analysis, incident response, and threat hunting**.

---

## 🎓 Education

### T Level — Digital Production, Design and Development

**Pearson**

* Completed a 2-year T Level programme
* Completed 2 years of industry placement as part of the qualification
* Developed practical technical, problem-solving, and professional skills
* Gained real-world experience working within a professional IT environment

---

## 💼 Industry Experience

### IT Support — 2-Year Industry Placement

During my industry placement, I gained hands-on experience supporting users, managing endpoints, troubleshooting technical issues, and working within a professional IT environment.

A key area of my experience was **endpoint patch management and remediation**.

### Patch Management & Remediation

* Used **ConnectWise Manage** to monitor endpoints and identify machines with failed patch deployments
* Used **ConnectWise Automate** to locate and remotely access affected machines
* Investigated failed patch deployments and troubleshot endpoint issues
* Used **PowerShell** to manually download and apply Microsoft updates using their KB IDs
* Recorded patches that repeatedly failed across multiple machines
* Documented recurring patch failures, including patch names and KB IDs
* Investigated patterns in recurring endpoint issues to support troubleshooting and remediation

This experience developed my practical skills in:

**Endpoint Management · Troubleshooting · Remote Administration · PowerShell · Patch Management · Technical Documentation · Problem Solving**

These skills have provided a strong technical foundation that I'm now applying to cybersecurity and Security Operations.

---

## 🔐 Cybersecurity Focus

I'm currently developing practical skills across:

* Security Operations (SOC)
* SIEM & Log Analysis
* Security Monitoring
* Threat Detection
* Incident Response
* Threat Hunting
* Windows Security
* Linux Security
* Network Security
* Security Automation
* MITRE ATT&CK
* Digital Forensics Fundamentals

My goal is to develop the ability to investigate security events from **initial detection through evidence collection, analysis, scoping, documentation, and recommended remediation**.

---

## 🛠️ Tools & Technologies

### Professional / Industry Experience

* **ConnectWise Manage**
* **ConnectWise Automate**
* **PowerShell**
* **Windows**
* Endpoint Management
* Remote Administration

### Cybersecurity Labs & Development

(not completed yet)
* **Wazuh**
* **Splunk**
* **Sysmon**
* **Wireshark**
* **Linux**
* **Git & GitHub**
  
* **Python**

I'm continuing to expand this toolkit through hands-on labs, investigations, and security-focused projects.

---

# 📂 Cybersecurity Portfolio

This portfolio is organised around practical investigations and security projects rather than purely theoretical coursework.

## 🔎 Completed Investigations

### Sysmon Process Investigation

Performed a hands-on endpoint investigation using **Sysmon** and Windows Event Viewer to analyse process creation telemetry.

The investigation focused on:

* Analysing **Sysmon Event ID 1 — Process Create**
* Examining process command lines
* Identifying parent and child processes
* Reconstructing process relationships
* Investigating PowerShell and `conhost.exe` activity
* Reviewing process hashes and integrity levels
* Assessing whether observed activity appeared suspicious or legitimate
* Documenting investigation findings

### Process Tree

```text
explorer.exe
    |
    └── powershell.exe
            |
            └── conhost.exe
```

### Key Finding

Based on the available telemetry, the observed PowerShell activity was assessed as **consistent with legitimate interactive user activity**.

The process tree showed `explorer.exe` launching PowerShell, which in turn spawned `conhost.exe`. No suspicious command line, unusual parent process, or other indicators of compromise were identified during the investigation.

The investigation demonstrated how **process relationships and endpoint telemetry can be used to establish context around security events and distinguish potentially suspicious activity from legitimate behaviour**.

### Tools Used

* Sysmon
* Windows Event Viewer
* PowerShell
* Windows Event Logs

> A detailed investigation report will be added to the portfolio as the project structure develops.

---

# 🚧 Projects In Progress

## SOC Home Lab

Building a small security monitoring environment to develop practical SOC skills.

The lab is focused on:

* Endpoint monitoring
* Log collection
* SIEM configuration
* Security alert analysis
* Detection engineering
* Incident investigation
* Security monitoring workflows

---

## Windows Event Log Investigation

Developing investigations around Windows security telemetry to understand normal and potentially suspicious system activity.

Areas of investigation include:

* Authentication activity
* Failed and successful logins
* Suspicious processes
* Account activity
* Security events
* Indicators of potential compromise
* Event timelines
* Investigation findings

---

## Brute Force Detection

Building a detection and investigation workflow for repeated authentication failures.

The project focuses on:

* Identifying suspicious login patterns
* Analysing Windows authentication logs
* Investigating source IP addresses
* Identifying affected accounts
* Establishing attack timelines
* Analysing authentication frequency and patterns
* Determining scope and potential impact
* Mapping activity to **MITRE ATT&CK**
* Documenting investigation findings
* Developing detection logic

---

## Phishing Investigation

Developing an investigation workflow for analysing suspicious emails and identifying potential indicators of compromise.

Areas of investigation include:

* Email headers
* Sender information
* URLs and domains
* Attachments
* Indicators of compromise
* User interaction
* Potential endpoint activity
* Scope and impact
* Recommended containment
* Recommended remediation

The objective is to develop a structured approach to investigating phishing activity from the initial alert through to containment and remediation recommendations.

---

## Threat Hunting Lab

Developing structured threat-hunting exercises using endpoint and network telemetry.

The focus is on:

* Developing hunting hypotheses
* Searching security logs
* Identifying suspicious behaviour
* Investigating indicators
* Correlating events
* Establishing timelines
* Mapping findings to **MITRE ATT&CK**
* Documenting conclusions
* Developing repeatable hunting workflows

---

# 🧪 Security Investigation Methodology

For my cybersecurity investigations, I'm developing a consistent analytical methodology:

```text
Alert
  ↓
Collect Evidence
  ↓
Analyse Logs & Telemetry
  ↓
Establish Context
  ↓
Identify Indicators
  ↓
Determine Scope & Impact
  ↓
Map to MITRE ATT&CK
  ↓
Assess Findings
  ↓
Document Investigation
  ↓
Recommend Remediation
```

The aim is not simply to identify suspicious activity, but to understand **what happened, how it happened, what was affected, and what evidence supports the conclusion**.

Where appropriate, investigations will distinguish between:

* **Observed facts**
* **Analytical assessment**
* **Indicators of compromise**
* **Potential impact**
* **Recommended actions**

This approach helps avoid jumping to conclusions and encourages evidence-based security analysis.

---

# 📊 What I'm Learning

I'm actively developing my knowledge and practical skills in:

### Security Operations

* SIEM
* Security monitoring
* Alert triage
* Log analysis
* Incident investigation
* Incident response
* Detection engineering

### Endpoint Security

* Windows Event Logs
* Sysmon
* Process analysis
* PowerShell security
* Endpoint telemetry
* Process trees
* Authentication activity

### Threat Detection & Hunting

* Detection logic
* Threat hunting
* Indicators of compromise
* Attack timelines
* MITRE ATT&CK
* Suspicious behaviour analysis

### Network & Security Fundamentals

* Network traffic analysis
* Network security
* Linux security
* Digital forensics fundamentals

### Automation & Scripting

* PowerShell
* Python
* Security automation
* Data analysis

---

# 📈 Current Development

I'm continuing to build practical experience through:

* Hands-on SOC labs
* Windows security investigations
* SIEM exercises
* Detection engineering
* Threat-hunting scenarios
* Incident-response exercises
* Network analysis
* Security documentation
* MITRE ATT&CK mapping
* Security automation

As projects are completed, they will be added to this repository with supporting evidence, investigation methodology, findings, and conclusions.

---


# 📌 Portfolio Roadmap

As I continue developing my skills, this repository will grow to include:

* 🔎 Security investigations
* 🖥️ SOC lab environments
* 🚨 Detection use cases
* 📊 SIEM queries
* 🕵️ Threat-hunting exercises
* 🧪 Incident-response scenarios
* 📝 Investigation reports
* 🛡️ MITRE ATT&CK mappings
* ⚙️ Security automation projects
* 📚 Technical notes and learning documentation

---

## 🚀 Portfolio Objective

I'm building this portfolio to demonstrate my development toward a career in **Security Operations** through practical, evidence-based cybersecurity work.

My focus is on developing the mindset of a SOC Analyst:

> **Investigate first. Analyse the evidence. Establish context. Scope the activity. Document the findings. Recommend appropriate action.**

---
