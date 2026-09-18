# Defensive Security Intro

- TryHackMe: [Defensive Security Intro](https://tryhackme.com/room/defensivesecurityintro)
- Difficulty: Easy
- Estimated time: 25 minutes
- Topics: `defensive security`, `SOC`, `threat intelligence`, `DFIR`, `malware analysis`, `SIEM`

> This walkthrough is for the authorized TryHackMe room only. Do not investigate or access systems without permission.

## Objective

This room introduces defensive security and the teams, processes, and tools used to prevent, detect, investigate, and respond to cyber attacks.

## Introduction to defensive security

Defensive security has two main goals:

1. Prevent intrusions from happening.
2. Detect and respond to intrusions when they occur.

Common defensive activities include security awareness training, asset management, patching, firewall and IPS configuration, logging, and monitoring.

The team that focuses on defensive security is the **Blue Team**.

## Areas of defensive security

### Security Operations Center (SOC)

A Security Operations Center is a team of cybersecurity professionals that monitors systems and networks for suspicious or malicious activity. A SOC may investigate:

- Vulnerabilities and missing patches
- Policy violations
- Unauthorized account activity
- Network intrusions
- Alerts from security monitoring tools

The correct name for a team monitoring a network and its systems for malicious events is **Security Operations Center**, commonly shortened to **SOC**.

### Threat intelligence

Threat intelligence is the process of collecting, processing, and analyzing information about current or potential adversaries. It helps an organization understand:

- Who may target it
- What the attacker may want
- Which tactics, techniques, and procedures may be used
- How to improve detection and response

Threat intelligence sources can include internal logs, security reports, public research, forums, and information about known threat actors.

### Digital Forensics and Incident Response

DFIR stands for **Digital Forensics and Incident Response**.

#### Digital forensics

Digital forensics examines evidence from systems involved in an incident. Relevant evidence sources include:

- File systems and disk images
- System memory
- Host logs
- Network logs

The goal is to understand what happened, identify relevant artifacts, and support the investigation.

#### Incident response

Incident response provides a structured method for handling a security incident. The four major phases are:

1. **Preparation**: Build and train the response team and prepare the required tools and procedures.
2. **Detection and analysis**: Identify an incident and determine its scope and severity.
3. **Containment, eradication, and recovery**: Stop the spread, remove the cause, and restore affected systems.
4. **Post-incident activity**: Document the incident and apply lessons learned.

### Malware analysis

Malware is malicious software. Examples include viruses, Trojan horses, and ransomware.

- **Static analysis** examines malware without executing it.
- **Dynamic analysis** executes malware in a controlled environment and observes its behavior.

The malware that encrypts files and demands payment to restore access is **ransomware**.

## Practical SIEM example

The room provides a simulated Security Information and Event Management system. A SIEM collects security events from different sources and presents them to analysts in a central dashboard.

Not every alert is malicious. An analyst must investigate the context and determine whether an alert is a real incident or a false positive.

Examples of events that may require investigation include:

- Multiple failed logins
- Connections from unfamiliar IP addresses
- Access to sensitive resources
- Activity outside a user’s normal behavior

### Investigation workflow

1. Open the SIEM simulation with the **View Site** button in the room.
2. Read the instructions shown inside the simulation.
3. Review the listed events and follow the suspicious activity through the available views.
4. Correlate the events to identify the incident.
5. Locate the flag displayed by the simulation.

The room’s SIEM flag is intentionally not included in plain text:

```text
THM{REDACTED}
```

## Answers

| Question | Answer |
| --- | --- |
| Which team focuses on defensive security? | Blue Team |
| What team monitors a network and its systems for malicious events? | Security Operations Center (SOC) |
| What does DFIR stand for? | Digital Forensics and Incident Response |
| Which malware requires payment to regain access to files? | Ransomware |
| What flag was obtained from the SIEM simulation? | `THM{REDACTED}` |

## Conclusion

Defensive security combines preventive controls, continuous monitoring, investigation, and incident response. This room introduces the main blue-team areas and shows how a SOC analyst can use SIEM alerts to investigate suspicious activity.
