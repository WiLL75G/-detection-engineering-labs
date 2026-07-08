# Detection Engineering Labs

Hands on detection engineering and SOC analysis labs. Each lab runs a real attack in a self contained home lab, detects it, investigates it, and documents the whole thing as a Tier 1 style incident report mapped to MITRE ATT&CK. The focus is evidence over claims: every finding is backed by a screenshot from the lab.

## Labs

| Lab | Focus | Platform | MITRE | Status |
| --- | --- | --- | --- | --- |
| [01 Wazuh SSH Brute Force](01-wazuh-ssh-bruteforce/) | Detecting a brute force through to confirmed compromise | Wazuh 4.14.6 | T1110 | Complete |
| [02 ServiceNow ITSM Incident Lifecycle](02-servicenow-itsm/) | Working a security incident New to Closed with SLA tracking | ServiceNow | T1110 | Complete |
| 03 Suricata IDS | Writing and tuning network intrusion detection rules | Suricata | planned | Planned |
| 04 PowerShell Investigation | Investigating suspicious PowerShell with process telemetry | Windows, Sysmon | planned | Planned |

## What each lab demonstrates

**01 Wazuh SSH Brute Force.** A Kali attacker runs Hydra against SSH on an Ubuntu host monitored by Wazuh. The detection chain is traced from individual failed logins through frequency correlation to a level 12 alert confirming the failure then success compromise, then traced back to the attacker source IP and mapped to MITRE T1110.

**02 ServiceNow ITSM Incident Lifecycle.** The Wazuh detection is operationalized as a managed incident in a live ServiceNow instance. The incident is created, prioritized using the Impact by Urgency matrix, routed, worked with documented triage and containment notes, resolved, and permanently closed, with automatic SLA tracking and an honestly documented SLA breach.

## Home Lab

A self contained environment: a macOS host, an Ubuntu Server victim, a Windows 11 endpoint, and a Kali Linux attacker, with detection and response tooling deployed across it. Each lab folder holds its own README and a screenshots directory with the supporting evidence.

## About

Built and documented by William Gokah, learning in public across detection engineering and SOC analysis. Detection and response are treated as two halves of the same job: seeing the attack, and running the response. Claims are kept honest to what was actually demonstrated in the lab.
