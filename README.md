# SOC Investigation with Splunk

## Overview

This project demonstrates a hands-on Security Operations Center (SOC) investigation using system security event logs and Splunk.

The objective was to ingest Windows event logs into Splunk, analyze authentication-related events, identify failed login activity, investigate suspicious authentication patterns, and generate investigation reports based on Windows Event IDs.

## Objectives

* Ingest Windows security logs into Splunk
* Understand and analyze Windows Security Event IDs
* Investigate failed authentication attempts
* Identify frequently targeted accounts and source systems
* Analyze login activity over time
* Correlate failed and successful authentication events
* Build Splunk searches for security monitoring
* Document investigation findings in a SOC-style report

## Technologies Used

* Splunk
* Windows Security Event Logs
* SPL (Search Processing Language)
* Windows Event IDs
* SOC Investigation Techniques

## Investigation Workflow

```text
Windows System
      │
      ▼
Windows Security Logs
      │
      ▼
Log Collection / Import
      │
      ▼
Splunk
      │
      ├── Event ID Analysis
      │
      ├── Failed Login Analysis
      │
      ├── Authentication Timeline
      │
      └── Suspicious Activity Investigation
      │
      ▼
Investigation Findings
      │
      ▼
SOC Report
```

## Windows Event IDs Investigated

| Event ID | Description                 |
| -------- | --------------------------- |
| 4624     | Successful logon            |
| 4625     | Failed logon                |
| 4634     | Logoff                      |
| 4647     | User-initiated logoff       |
| 4672     | Special privileges assigned |
| 4720     | User account created        |
| 4740     | User account locked out     |

## Failed Login Investigation

Windows Event ID **4625** was analyzed to identify authentication failures and determine whether repeated failures originated from the same source.

The investigation examined:

* Username
* Source IP address
* Workstation
* Logon type
* Failure reason
* Number of failed attempts
* Timestamp
* Authentication patterns

### Example SPL

```spl
index=windows EventCode=4625
| stats count by Account_Name, Source_Network_Address, Workstation_Name
| sort - count
```

## Investigation Questions

The analysis focused on questions such as:

1. Which accounts experienced the highest number of failed login attempts?
2. Which source addresses generated the most failures?
3. Were multiple accounts targeted from the same source?
4. Did failed authentication attempts occur in bursts?
5. Were successful logins observed after repeated failures?
6. Were there signs consistent with password spraying or brute-force activity?
7. Were privileged accounts involved?

## Findings

The investigation results are documented in the `reports/` directory.

Screenshots of Splunk searches, visualizations, and dashboards are available in the `screenshots/` directory.

> Note: Any identifying information in the logs should be sanitized before publication. The repository is intended for cybersecurity learning and SOC investigation demonstration purposes.

## Skills Demonstrated

* SIEM log analysis
* Splunk
* SPL
* Windows Event Log Analysis
* Authentication Monitoring
* Failed Login Investigation
* Security Event ID Analysis
* Basic Threat Detection
* SOC Investigation
* Security Documentation
