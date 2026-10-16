# Splunk SOC Home Lab

A hands-on Security Operations Center (SOC) home lab built to learn SIEM administration, Windows log collection, Search Processing Language (SPL), security monitoring, threat detection, alert triage, and incident investigation using Splunk Enterprise.

The project simulates a small enterprise environment where an analyst collects endpoint telemetry, investigates suspicious activity, writes detection searches, and documents findings using a controlled virtual lab.


## Table of Contents

* [1. Project Overview](#1-project-overview)
* [2. Project Objectives](#2-project-objectives)
* [3. Lab Architecture](#3-lab-architecture)
* [4. Host Environment](#4-host-environment)
* [5. Prerequisites and Downloads](#5-prerequisites-and-downloads)
* [6. Project Scope and Implementation Phases](#6-project-scope-and-implementation-phases)
* [7. Detection and Investigation Scenarios](#7-detection-and-investigation-scenarios)
* [8. Learning Resources](#8-learning-resources)
* [9. Repository Structure](#9-repository-structure)
* [10. Project Deliverables](#10-project-deliverables)
* [11. Success Criteria](#11-success-criteria)
* [12. Security and Safety](#12-security-and-safety)

## 1. Project Overview

This project builds a small, isolated SOC environment using VirtualBox and three virtual machines.

The environment will generate endpoint activity, collect security logs, forward those logs to Splunk, and use SPL searches to identify and investigate suspicious behavior.

The project follows a practical SOC workflow:

1. Generate activity on an endpoint.
2. Collect and forward relevant security telemetry.
3. Search and analyze events in Splunk.
4. Identify suspicious patterns and create detections.
5. Investigate alerts using event timelines and supporting evidence.
6. Document findings, conclusions, and remediation recommendations.

The objective is to demonstrate practical blue-team skills rather than simply install a SIEM.

## 2. Project Objectives

* Deploy and configure a Splunk-based SIEM.
* Build an isolated virtual enterprise environment.
* Enable Windows security auditing and collect endpoint logs.
* Understand Windows Event Viewer, Security logs, and Sysmon telemetry.
* Learn SPL for filtering, aggregation, correlation, and investigation.
* Develop practical detections for authentication and process activity.
* Investigate suspicious behavior using event timelines and supporting evidence.
* Map relevant detections to the MITRE ATT&CK framework.
* Create analyst-style incident reports and reusable detection documentation.
* Maintain a version-controlled portfolio on GitHub.

### Skills demonstrated

`Splunk Enterprise` · `SPL` · `Windows Event Logs` · `Sysmon` · `SIEM` · `Detection Engineering` · `Alert Triage` · `Incident Investigation` · `MITRE ATT&CK` · `VirtualBox` · `Git/GitHub`

## 3. Lab Architecture

The lab uses a dedicated VirtualBox Internal Network named `SOC-LAB`. The three virtual machines communicate over this isolated network.

| Component   | Operating system | Planned IP      | Purpose                                         |
| ----------- | ---------------- | --------------- | ----------------------------------------------- |
| Attacker VM | Kali Linux       | `192.168.50.10` | Generate controlled security test activity      |
| Endpoint VM | Windows 11       | `192.168.50.20` | Generate Windows security and system telemetry  |
| SIEM VM     | Ubuntu Desktop   | `192.168.50.30` | Host Splunk and perform security investigations |

Subnet: `192.168.50.0/24`

These are the intended lab addresses and the addresses previously configured. Connectivity and final configuration should be verified during setup.

### Architecture diagram

```text
                 SOC-LAB
          VirtualBox Internal Network
                       |
        +--------------+--------------+
        |              |              |
        v              v              v
   Kali Linux      Windows 11      Ubuntu Desktop
   Attacker        Endpoint        Splunk SIEM
   .50.10          .50.20          .50.30
                       |
                       | Windows security logs
                       | Sysmon telemetry (planned)
                       v
                 Splunk ingestion
                       |
                       v
              SPL detections and searches
                       |
                       v
             Alert triage and investigation
                       |
                       v
              Incident report and evidence
```

**Planned telemetry flow:** Splunk Universal Forwarder will be installed on the Windows endpoint to forward selected Windows Security and Sysmon events to Splunk Enterprise. The configuration will be validated after installation.

## 4. Host Environment

| Resource                | Configuration                                       |
| ----------------------- | --------------------------------------------------- |
| Virtualization platform | Oracle VirtualBox                                   |
| Virtual machines        | Kali Linux, Windows 11, Ubuntu Desktop              |
| SIEM                    | Splunk Enterprise                                   |
| Network mode            | VirtualBox Internal Network                         |

Virtual machine memory, CPU allocation, and disk sizing will be tuned to the host's available resources. Running all three VMs simultaneously may require reducing their resource allocations.

## 5. Prerequisites and Downloads

Use official sources wherever possible. Check current licensing, platform compatibility, and system requirements before downloading or installing software.

### 5.1 Virtualization and operating systems

| Prerequisite      | Purpose                            | Official resource                                     |
| ----------------- | ---------------------------------- | ----------------------------------------------------- |
| Oracle VirtualBox | Create and manage virtual machines | https://www.virtualbox.org/wiki/Downloads             |
| Kali Linux        | Controlled source of test activity | https://www.kali.org/get-kali/                        |
| Windows 11 ISO    | Endpoint for security telemetry    | https://www.microsoft.com/software-download/windows11 |
| Ubuntu Desktop    | Planned Splunk host                | https://ubuntu.com/download/desktop                   |

### 5.2 SIEM and log collection

| Component                  | Purpose                                         | Official resource                                                   |
| -------------------------- | ----------------------------------------------- | ------------------------------------------------------------------- |
| Splunk Enterprise          | Search, analyze, and correlate security data    | https://www.splunk.com/en_us/download/splunk-enterprise.html        |
| Splunk Universal Forwarder | Forward Windows events to Splunk                | https://www.splunk.com/en_us/download/universal-forwarder.html      |
| Splunk documentation       | Installation, administration, and configuration | https://docs.splunk.com/Documentation                               |
| Splunk Search Reference    | SPL commands, syntax, and examples              | https://docs.splunk.com/Documentation/Splunk/latest/SearchReference |
| Sysmon                     | Detailed Windows process and system telemetry   | https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon     |
| Windows Event Viewer       | Inspect and validate endpoint events            | https://learn.microsoft.com/en-us/shows/inside/event-viewer         |

**Important:** Confirm the Splunk Enterprise licensing and trial terms that apply to your installation. Choose compatible Splunk and forwarder versions. Do not assume a paid enterprise license is necessary for every learning activity.

### 5.3 Development and documentation tools

| Tool               | Purpose                                          | Resource                       |
| ------------------ | ------------------------------------------------ | ------------------------------ |
| Git                | Version control                                  | https://git-scm.com/downloads  |
| GitHub             | Host project documentation and detection content | https://github.com/            |
| Visual Studio Code | Edit Markdown, configuration, and SPL files      | https://code.visualstudio.com/ |

## 6. Project Scope and Implementation Phases

### Phase 1 — Lab setup and networking

**Objective:** Establish a stable, isolated environment.

* Install and configure VirtualBox.
* Create Kali Linux, Windows 11, and Ubuntu virtual machines.
* Configure the `SOC-LAB` Internal Network.
* Assign the planned static IP addresses.
* Test connectivity and document troubleshooting.
* Capture screenshots of VM and network configurations.

**Deliverables:** Lab architecture, IP address table, network validation results, setup documentation.

### Phase 2 — Splunk installation and initial configuration

**Objective:** Deploy the SIEM and confirm that it is operational.

* Install Splunk Enterprise on Ubuntu.
* Configure the Splunk web interface and administrative access.
* Learn indexes, sources, source types, hosts, and events.
* Create or validate the index used for Windows security data.
* Run initial searches and verify timestamps and event fields.
* Document installation and troubleshooting steps.

**Deliverables:** Installation guide, configuration notes, initial search screenshots.

### Phase 3 — Windows logging and telemetry collection

**Objective:** Make endpoint activity visible in Splunk.

* Configure Windows audit policies for relevant security events.
* Inspect logs using Windows Event Viewer.
* Install Sysmon with a documented, suitable configuration.
* Install and configure Splunk Universal Forwarder on the Windows endpoint.
* Forward relevant Windows Security and Sysmon events.
* Validate event ingestion, timestamps, host names, and field extraction.

**Deliverables:** Collection configuration, event source documentation, ingestion validation searches.

### Phase 4 — SPL fundamentals

**Objective:** Build confidence with Splunk searches before developing detections.

Learn and practice:

* `search` and field-based filtering
* `table`, `fields`, and `rename`
* `stats`, `chart`, and `timechart`
* `sort`, `dedup`, and `top`
* `eval`, `where`, and conditional logic
* `rex` and field extraction
* Time-range filtering and event timelines
* Basic correlation and aggregation

**Deliverables:** A collection of tested SPL examples with explanations and sample results.

### Phase 5 — Detection engineering

**Objective:** Create useful detections from endpoint telemetry.

Develop and validate searches for:

* Repeated failed logon attempts
* Successful logons following repeated failures
* New local account creation
* Addition of users to privileged groups
* Suspicious process execution
* PowerShell execution requiring further investigation
* Unexpected process parent-child relationships
* Security logging or defensive control changes, where suitable telemetry is available

Each detection should document its purpose, required data, SPL, expected results, false-positive considerations, and investigation steps.

**Deliverables:** Reusable SPL searches, detection notes, ATT&CK mappings, and validation evidence.

### Phase 6 — Controlled adversary simulation

**Objective:** Generate safe, observable activity to test the detections.

* Perform controlled authentication tests against the Windows endpoint.
* Create test accounts or group changes where appropriate.
* Generate benign process and PowerShell activity.
* Use the Kali VM only for authorized lab activity.
* Record timestamps and expected telemetry.
* Verify whether each action produced the expected logs and detection results.

**Deliverables:** Test plan, activity timeline, event evidence, detection validation results.

### Phase 7 — Alert triage and incident investigation

**Objective:** Practice the analytical workflow of a SOC analyst.

For each test case:

1. Identify the alert or suspicious search result.
2. Establish the time window and affected host.
3. Review the underlying events.
4. Correlate related accounts, processes, and timestamps.
5. Determine whether the activity is expected, suspicious, or inconclusive.
6. Document evidence, confidence, impact, and recommended response.
7. Record the detection's limitations and possible improvements.

**Deliverables:** Incident investigation reports, event timelines, evidence screenshots, and remediation recommendations.

## 7. Detection and Investigation Scenarios

The following scenarios are proposed project objectives, not claims that detections have already been implemented or validated.

| Scenario                            | Example Windows telemetry                                             | Investigation goal                                              |
| ----------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------- |
| Repeated failed logons              | Security Event ID `4625`                                              | Identify repeated authentication failures and affected accounts |
| Successful logon                    | Security Event ID `4624`                                              | Establish successful authentication context                     |
| Account created                     | Security Event ID `4720`                                              | Identify the new account and creation time                      |
| Privileged group membership changed | Security Event IDs `4728`, `4732`, or `4756`, depending on group type | Investigate potential privilege escalation                      |
| Process execution                   | Sysmon Event ID `1`                                                   | Review process name, command line, parent process, and user     |
| Network connection                  | Sysmon Event ID `3`, if enabled                                       | Correlate process activity with network connections             |
| PowerShell activity                 | Available PowerShell operational logs and process telemetry           | Examine execution context and suspicious commands               |

Event IDs and their availability depend on audit policy, log source, and Sysmon configuration. Not every event will be present by default.

### Detection documentation template

Each detection should include:

* **Detection name**
* **Objective and hypothesis**
* **Data source and required fields**
* **SPL query**
* **How to run and validate it**
* **Expected results**
* **False positives and limitations**
* **MITRE ATT&CK technique, where applicable**
* **Analyst triage steps**
* **Evidence and test results**

## 8. Learning Resources

Use the following sequence to avoid trying to learn every tool at once.

### 8.1 Start with Splunk

1. **Splunk Education** — official training and learning paths:
   https://www.splunk.com/en_us/training.html

2. **Search Tutorial** — learn the search interface and SPL basics:
   https://docs.splunk.com/Documentation/Splunk/latest/SearchTutorial/WelcometotheSearchTutorial

3. **Search Reference** — look up commands and syntax as you build queries:
   https://docs.splunk.com/Documentation/Splunk/latest/SearchReference

4. **Splunk Enterprise documentation** — installation and administration:
   https://docs.splunk.com/Documentation/Splunk/latest

**Recommended learning order:** Search fundamentals → filtering → aggregation with `stats` → time-based analysis → field extraction → detection searches.

### 8.2 Learn Windows logging and Sysmon

* Windows Security Auditing:
  https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/basic-audit-logon-events

* Microsoft Sysmon documentation:
  https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

* Microsoft Windows event documentation:
  https://learn.microsoft.com/en-us/windows/win32/eventlog/event-logging

Focus on understanding what an event records, when it is generated, and which fields are useful during an investigation.

### 8.3 Learn threat detection and MITRE ATT&CK

* **MITRE ATT&CK knowledge base:** https://attack.mitre.org/
* **MITRE ATT&CK Enterprise matrix:** https://attack.mitre.org/matrices/enterprise/
* **Sigma detection rules:** https://github.com/SigmaHQ/sigma

Use ATT&CK to describe adversary behaviors and Sigma as a source of detection ideas. Treat community rules as learning material that must be adapted to your telemetry and validated before use.

### 8.4 Practice security investigation

* **Splunk Security Content:** https://research.splunk.com/
* **Splunk Community:** https://community.splunk.com/
* **Blue Team Labs Online:** https://blueteamlabs.online/
* **CyberDefenders:** https://cyberdefenders.org/

These resources complement the home lab with investigation exercises, examples, and detection ideas. External platforms may require accounts or have different access terms.

### 8.5 Learn Git and GitHub

* Git documentation: https://git-scm.com/doc
* GitHub documentation: https://docs.github.com/
* GitHub Markdown guide: https://docs.github.com/en/get-started/writing-on-github

Use Git to track changes to your SPL files, investigation reports, configuration examples, and project documentation.

## 9. Repository Structure

A suggested repository layout:

```
splunk-soc-home-lab/
├── README.md
├── .gitignore
│
├── Phase-1-Lab-Setup/
│   ├── README.md
│   └── screenshots/
│
├── Phase-2-Splunk-Installation/
│   ├── README.md
│   ├── installation-notes/
│   ├── configuration/
│   ├── splunk-searches/
│   └── screenshots/
│
├── Phase-3-Windows-Log-Collection/
│   ├── README.md
│   ├── windows-audit-policy/
│   ├── sysmon/
│   ├── universal-forwarder/
│   ├── sample-events/
│   └── screenshots/
│
├── Phase-4-SPL-Fundamentals/
│   ├── README.md
│   ├── filtering/
│   ├── aggregation/
│   ├── time-analysis/
│   ├── field-extraction/
│   └── queries.spl
│
├── Phase-5-Detection-Engineering/
│   ├── README.md
│   ├── authentication/
│   ├── account-management/
│   ├── process-execution/
│   ├── powershell/
│   ├── detection-template.md
│   └── test-results/
│
├── Phase-6-Adversary-Simulation/
│   ├── README.md
│   ├── test-plans/
│   ├── activity-timelines/
│   ├── sample-events/
│   └── detection-validation/
│
└── Phase-7-Incident-Investigation/
    ├── README.md
    ├── investigation-template.md
    ├── cases/
    ├── evidence/
    └── final-reports/
```

## 10. Project Deliverables

The completed portfolio should contain:

* [ ] Lab architecture and network documentation
* [ ] Splunk installation and configuration guide
* [ ] Windows event collection and validation guide
* [ ] SPL learning examples
* [ ] A set of tested security detection searches
* [ ] Detection documentation and relevant ATT&CK mappings
* [ ] Controlled test scenarios and results
* [ ] Incident investigation reports
* [ ] Screenshots demonstrating key implementation steps
* [ ] Troubleshooting notes and lessons learned
* [ ] A final summary of skills demonstrated and project limitations

## 11. Success Criteria

The project is considered functionally complete when:

* Splunk is installed and accessible.
* Windows endpoint telemetry arrives in Splunk reliably.
* The analyst can search, filter, and aggregate relevant events using SPL.
* Controlled test activity produces identifiable event evidence.
* Multiple detections have been tested against available data.
* At least one investigation report traces activity from initial event to analyst conclusion.
* Documentation explains how to reproduce the key steps.
* The GitHub repository contains no credentials, tokens, or other sensitive information.

## 12. Security and Safety

* Keep the lab on the VirtualBox Internal Network unless temporary connectivity is explicitly required.
* Avoid Bridged networking for the attacker VM.
* If temporary internet access is required, use a separate NAT adapter and remove or disable it when no longer needed.
* Generate test activity only on systems you own or are authorized to test.
* Do not expose the Splunk management interface directly to the public internet.
* Use strong administrative credentials and do not commit passwords, API tokens, private keys, or license secrets.
* Sanitize usernames, IP addresses, host details, and other potentially sensitive data in published evidence.
* Document any deliberate changes to Windows security settings and restore them when testing is complete.

---

## Final Project Goal

Build a reproducible, documented Splunk SOC home lab that demonstrates the practical workflow of a junior SOC analyst: **collect telemetry, search events, detect suspicious activity, investigate evidence, and document a defensible conclusion.**

The focus is on understanding and explaining the work performed, not merely obtaining screenshots of a working tool.
