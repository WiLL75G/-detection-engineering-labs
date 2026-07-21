# Detection Engineering Labs

Four labs, four detection surfaces, one attack caught twice. The same SSH brute force is detected host-side and network-side by two independent sensors, and one PowerShell payload is recovered in plaintext from telemetry that was never meant to give it up.

## At a Glance

| Field | Detail |
| --- | --- |
| Work Type | Detection engineering and SOC analysis |
| Labs | 4, all complete |
| Detection Surfaces | Host logs, network traffic, endpoint telemetry, IR workflow |
| Platforms | Wazuh 4.14.6, ServiceNow, Suricata 7.0.3, Windows/Sysmon |
| MITRE Techniques | T1110, T1046, T1059.001 |
| Attack Detected Twice | SSH brute force, host and network |
| Evidence Standard | Every finding backed by a lab screenshot |

## What This Is

A self-contained detection engineering portfolio. Each lab runs a real attack in a home lab, detects it, investigates it, and documents the whole thing as a Tier 1 style incident report mapped to MITRE ATT&CK.

Nothing here is simulated on paper. A Kali attacker runs the attacks, real sensors catch them, and the investigation works from actual log lines and telemetry. The focus is evidence over claims: if a finding is stated, a screenshot from the lab backs it.

## Labs

| Lab | Focus | Platform | MITRE | Status |
| --- | --- | --- | --- | --- |
| [Wazuh SSH Brute Force](01-wazuh-ssh-bruteforce/) | Detecting a brute force through to confirmed compromise | Wazuh 4.14.6 | T1110 | Complete |
| [ServiceNow ITSM Incident Lifecycle](02-servicenow-itsm/) | Working a security incident New to Closed with SLA tracking | ServiceNow | T1110 | Complete |
| [Suricata IDS Custom Rules](03-suricata-ids/) | Writing network detection rules for scan and brute force | Suricata 7.0.3 | T1046, T1110 | Complete |
| [PowerShell Investigation](04-powershell-investigation/) | Recovering obfuscated PowerShell from endpoint telemetry | Windows, Sysmon | T1059.001 | Complete |

## What Each Lab Demonstrates

**01 Wazuh SSH Brute Force.** A Kali attacker runs Hydra against SSH on an Ubuntu host monitored by Wazuh. The detection chain is traced from individual failed logins, through frequency correlation, to a level 12 alert confirming the failure-then-success compromise, then traced back to the attacker source IP and mapped to T1110.

The value here is the escalation logic, not the alert. A brute force that only fails is noise. A brute force that fails and then succeeds is an incident, and the difference between the two is a single log line. This lab proves that line can be found.

**02 ServiceNow ITSM Incident Lifecycle.** The Wazuh detection is operationalized as a managed incident in a live ServiceNow instance. It is created, prioritized on the Impact-by-Urgency matrix, routed, worked with documented triage and containment notes, resolved, and permanently closed, with automatic SLA tracking and an honestly documented SLA breach.

The breach is the point, not a blemish. Most portfolios show the clean path. This one shows what a real record looks like when a clock runs out, because an auditor and a shift lead both trust the record that admits the miss over the one that never has them.

**03 Suricata IDS Custom Rules.** Suricata is deployed as a network sensor on the Ubuntu host, and two custom detection rules are written from scratch: a port scan detector and an SSH brute force detector. Both fire on live attacks from Kali.

The brute force rule detects the same attack Wazuh caught host-side in lab 01. That overlap is deliberate. One attack, two independent sensors, two layers, is defense in depth demonstrated rather than asserted, and it is the reason these two labs are stronger together than either is alone.

**04 PowerShell Investigation.** Suspicious PowerShell simulating real attacker behavior is executed on the Windows host and reconstructed from Sysmon and PowerShell Script Block Logging. The investigation recovers the deobfuscated plaintext of a base64-encoded command, identifies a download cradle, and traces a discovery sequence.

This is the lab that separates "PowerShell ran" from "here is exactly what it did." The first is an alert. The second is an investigation. Script Block Logging is what makes the second possible, and recovering the plaintext is the proof it was read correctly.

## Coverage

| Surface | Sensor | Lab | What It Catches |
| --- | --- | --- | --- |
| Host logs | Wazuh | 01 | Failed and successful authentications, escalation to compromise |
| IR workflow | ServiceNow | 02 | Incident lifecycle, prioritization, SLA tracking |
| Network traffic | Suricata | 03 | Port scans and brute force on the wire |
| Endpoint telemetry | Sysmon, PS logging | 04 | Process execution and deobfuscated PowerShell |

The detection surface spans host, network, endpoint, and workflow. The same SSH brute force is detected at two different layers to show defense in depth is a design property here, not a slogan.

## The SOC Angle

Two of these labs describe the two halves of a working SOC seat, and the seam between them is where most analysts get evaluated.

Lab 01 is detection: seeing the attack. Lab 02 is response: running the incident the detection created. An analyst who can only do the first hands off half a job. The reason these two labs are chained, one attack feeding one incident record, is that the handoff from alert to managed incident is exactly the transition a Tier 1 analyst is hired to own.

Lab 03 and lab 04 push the same instinct outward: catch the attack on more than one surface, and reconstruct what it actually did rather than stopping at that it happened.

## What This Demonstrates

Tracing a brute force from individual failed logins to a confirmed compromise on a single log line.

Operationalizing a raw detection into a managed incident with an honest SLA record.

Writing network detection rules from scratch and firing them on live traffic.

Catching one attack on two independent sensors to demonstrate defense in depth rather than claim it.

Recovering the plaintext of an obfuscated PowerShell payload from endpoint telemetry.

Treating detection and response as two halves of the same job, not two separate skills.

Keeping every claim honest to what the lab actually showed.

## Home Lab

A self-contained environment: a macOS host, an Ubuntu Server victim, a Windows 11 endpoint, and a Kali Linux attacker, with detection and response tooling deployed across it. Each lab folder holds its own README and a screenshots directory with the supporting evidence.

## Repository Structure

```
detection-engineering-labs/
├── README.md
├── 01-wazuh-ssh-bruteforce/
├── 02-servicenow-itsm/
├── 03-suricata-ids/
└── 04-powershell-investigation/
```

## About

Built and documented by William Gokah, learning in public across detection engineering and SOC analysis. Detection and response are treated as two halves of the same job: seeing the attack, and running the response. Claims are kept honest to what was actually demonstrated in the lab.

---

[![LinkedIn](https://img.shields.io/badge/LinkedIn-WilliamInCyber-blue?style=flat&logo=linkedin)](https://linkedin.com/in/WilliamInCyber)
[![X](https://img.shields.io/badge/X-@WilliamInCyber-black?style=flat&logo=x)](https://x.com/WilliamInCyber)
