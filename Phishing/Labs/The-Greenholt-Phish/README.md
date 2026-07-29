# Greenholt Phish 

**Type:** 🧪 Investigation Write-up

## Overview

This lab focused on investigating a phishing email using multiple OSINT and malware analysis tools. The objective was to validate the legitimacy of the email, identify indicators of compromise (IOCs), analyze the malicious attachment, and determine whether the message represented a genuine phishing attempt.

**Skills Practiced**

- Email header analysis
- Message source inspection
- Attachment analysis
- File hashing
- VirusTotal investigation
- IP reputation analysis
- WHOIS lookup
- SPF validation
- DMARC validation
- IOC identification

---

# Scenario

A suspicious email claiming to contain payment information was received by an organization's webmaster. The email included a CAB attachment disguised as a PDF document and referenced an interbank transfer.

The objective was to determine whether the email was malicious and collect intelligence that could be used during incident response.

---

# Tools Used

- Mozilla Thunderbird
- Linux Terminal
- sha256sum
- VirusTotal
- MXToolbox
- WHOIS Lookup

---

# Investigation

## 1. Initial Email Analysis

The email impersonated a financial notification regarding a successful transfer.

Important observations:

- Subject referenced a payment transfer
- Sender used a business-like identity
- Attachment claimed to be a PDF
- Urgent language encouraged the recipient to open the attachment

Collected information:

| Indicator          | Value                      |
|--------------------|----------------------------|
| Transfer Reference | **09674321**               |
| Display Name       | Mr. James Jackson          |
| Sender Address     | info@mutawamarine.com      |
| Reply-To Address   | info.mutawamarine@mail.com |

> **Finding**
>
> The Reply-To address differs from the sender address, a common phishing technique used to redirect victim responses to an attacker-controlled mailbox.

---

### Screenshot

```
images/email.png
```

---

# 2. Email Header Analysis

The email source was inspected to identify the real origin of the message.

Important findings:

| Indicator      | Value          |
|----------------|----------------|          
| Originating IP | 192.119.71.157 |

The message source also revealed the Return-Path domain used later for SPF and DMARC validation.

---

### Screenshot

```
images/source_analysis.png
```

---

# 3. IP Intelligence

A WHOIS lookup was performed on the originating IP.

Results:

- IP Owner: **HostPapa**
- Country: United States
- Hosting Provider

The sender originated from hosted infrastructure instead of a legitimate banking mail server.

This significantly reduced the credibility of the email.

---

# 4. SPF and DMARC Validation

The Return-Path domain was analyzed to determine whether email authentication had been configured.

## SPF Record

v=spf1 include:spf.protection.outlook.com -all

The SPF record exists and restricts authorized mail servers.

## DMARC Record

v=DMARC1; p=quarantine; fo=1

The DMARC policy instructs receiving servers to quarantine emails that fail authentication checks.

Although these security controls were correctly configured, attackers can still abuse compromised accounts or spoof visible sender information.

---

### Screenshot

```
images/ip_domain_intel.png
```

---

# 5. Attachment Analysis

The email contained the following attachment:

```
SWT_#09674321____PDF__.CAB
```

Although presented as a PDF, the attachment was actually a compressed archive.

The SHA-256 hash was generated using:

```bash
sha256sum SWT_#09674321____PDF__.CAB
```

Hash:

```
2e91c533615a9bb8929ac4bb76707b2444597ce063d84a4b33525e25074fff3f
```

VirusTotal analysis identified:

- File Size: **400.26 KB**
- Actual File Type: **RAR archive**
- Multiple antivirus detections
- Classified as malicious
- Associated with Loki malware

The mismatch between the displayed filename and the actual archive format is a classic phishing technique intended to trick users into executing malicious payloads.

---

### Screenshot

```
images/hash_analysis.png
```

---

# Indicators of Compromise (IOCs)

## Email Indicators

| Type         | Value                                |
|--------------|--------------------------------------|
| Sender       | info@mutawamarine.com                |
| Reply-To     | info.mutawamarine@mail.com           |
| Display Name | Mr. James Jackson                    |
| Subject      | Transfer Reference Number (09674321) |

---

## Network Indicators

| Type             | Value          |            
|------------------|----------------|
| Originating IP   | 192.119.71.157 |
| Hosting Provider | HostPapa       |

---

## File Indicators

| Type       | Value                                                            |
|------------|------------------------------------------------------------------|
| Attachment | SWT_#09674321____PDF__.CAB                                       |
| Real Type  | RAR                                                              |
| SHA256     | 2e91c533615a9bb8929ac4bb76707b2444597ce063d84a4b33525e25074fff3f |

---

# Detection Opportunities

A SOC analyst could detect this phishing attempt through multiple indicators:

- Reply-To address mismatch
- Compressed attachment masquerading as a PDF
- External sender impersonating financial communications
- Malicious file hash detected by VirusTotal
- Hosted infrastructure rather than a legitimate banking mail server
- Suspicious attachment extension (.CAB)

---

# Mitigation Recommendations

- Block the malicious file hash through endpoint protection.
- Block the sender and Reply-To addresses.
- Block or monitor the originating IP if observed within organizational telemetry.
- Configure email filtering to quarantine compressed executable attachments.
- Enforce SPF, DKIM, and DMARC validation.
- Train users to verify unexpected payment notifications and attachments.
- Submit identified IOCs to SIEM and EDR platforms for continuous monitoring.

---

# Key Takeaways

This investigation demonstrated a standard phishing workflow used by SOC analysts:

1. Inspect the email contents.
2. Analyze message headers.
3. Identify the originating infrastructure.
4. Validate SPF and DMARC records.
5. Hash suspicious attachments.
6. Investigate reputation using VirusTotal.
7. Extract actionable indicators of compromise.
8. Recommend detection and mitigation strategies.

The collected evidence confirmed that the email was a phishing attempt delivering a malicious attachment disguised as a financial document.
