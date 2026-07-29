# Introduction to SIEM

**Type:** 📘 Concept Documentation

## What is a SIEM?

A Security Information and Event Management (SIEM) system is a centralized platform that collects, stores, correlates, and analyzes logs from multiple devices and applications. It helps Security Operations Center (SOC) analysts detect, investigate, and respond to security incidents.

---

## Why is a SIEM important?

Without a SIEM, analysts would need to manually review logs from hundreds or thousands of devices.

A SIEM centralizes this data, making it possible to:

- Detect suspicious activity
- Correlate events from multiple sources
- Generate security alerts
- Investigate incidents
- Support compliance and auditing

---

## Common Log Sources

A SIEM can ingest logs from many different sources, including:

- Windows Event Logs
- Linux Syslog
- Firewalls
- IDS/IPS
- Endpoint Detection & Response (EDR)
- Antivirus
- DNS Servers
- Web Servers
- Proxy Servers
- Cloud Services
- Active Directory
- Network Devices

---

## Core SIEM Functions

### Log Collection

Collects logs from multiple systems into a centralized platform.

### Log Normalization

Converts logs from different formats into a standardized structure for easier analysis.

### Event Correlation

Combines related events from different systems to identify suspicious activity that would otherwise appear unrelated.

### Alerting

Generates alerts when predefined detection rules or correlation rules are triggered.

### Investigation

Allows analysts to search logs, examine timelines, and investigate incidents.

### Reporting

Produces dashboards and reports for monitoring, auditing, and compliance.

---

## Common SIEM Solutions

- Splunk Enterprise Security
- Microsoft Sentinel
- Elastic Security (ELK Stack)
- IBM QRadar
- Google Security Operations (Chronicle)

---

## Typical SOC Workflow

1. Logs are collected from multiple sources.
2. The SIEM ingests and normalizes the data.
3. Detection rules and correlation searches analyze incoming events.
4. A suspicious event triggers an alert.
5. The SOC analyst investigates the alert.
6. Evidence is correlated with other telemetry.
7. The analyst determines whether the alert is a True Positive or False Positive.
8. If malicious, the incident is escalated or contained.

---

## Example

A user logs into a workstation.

↓

Minutes later, the same account authenticates to a domain controller from another country.

↓

The firewall records an unusual outbound connection.

↓

The EDR detects PowerShell execution.

↓

The SIEM correlates all of these events into a single high-severity alert for analyst investigation.

---

## Related MITRE ATT&CK

A SIEM is used to detect activity across many ATT&CK tactics, including:

- TA0001 – Initial Access
- TA0002 – Execution
- TA0003 – Persistence
- TA0005 – Defense Evasion
- TA0006 – Credential Access
- TA0007 – Discovery
- TA0008 – Lateral Movement
- TA0011 – Command and Control
- TA0040 – Impact

---

## Key Takeaways

- SIEM centralizes security logs from multiple systems.
- Correlation rules provide context by linking related events.
- SIEMs enable faster detection and investigation of security incidents.
- Effective log analysis depends on high-quality data ingestion and normalization.
- SIEM is one of the primary tools used by SOC analysts during incident investigations.
