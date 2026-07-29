<<<<<<< HEAD
# 🛡️ SOC Learning Path

Documentation, methodologies, and technical write-ups from my path into SOC / blue-team work — incident response, threat hunting, SIEM, and phishing analysis, written up the way I'd document them on the job.

> 🚧 **Status: In Progress.** This repo is actively growing as I complete new labs and concepts. Check back for updates, or ⭐ it to follow along.

---

## About this repo

Everything here comes from hands-on labs and self-study, written as if I were handing findings to a SOC team lead: scenario, investigation steps, evidence, IOCs, MITRE ATT&CK mapping, and lessons learned. The goal is to build a portfolio that shows not just that I know the concepts, but that I can investigate, document, and communicate them clearly.

---

## 📂 Contents

### 🧩 Frameworks
Core concepts every SOC analyst should know cold.

| Write-up | Description |
|---|---|
| [Cyber Kill Chain](Frameworks/Cyber-Kill-Chain) | Lockheed Martin's 7-stage attack lifecycle model |
| [MITRE ATT&CK](Frameworks/MITRE-ATTACK) | Tactics, techniques, and sub-techniques used to map adversary behavior |
| [Pyramid of Pain](Frameworks/Pyramid-Of-Pain) | Why behavioral detections outlast IOC-based ones |
| [Summit — Sample 3](Frameworks/Lab/Summit) | Investigation write-up: registry-based Defense Evasion + custom Sigma rule |

### 🚨 Incident Response
| Write-up | Description |
|---|---|
| [Introduction to EDR](Incident-Response/EDR) | EDR telemetry, dashboards, and how it differs from traditional AV |

### 🎣 Phishing
| Write-up | Description |
|---|---|
| [Phishing Analysis Tools](Phishing/Tools) | Cisco Talos, VirusTotal, ANY.RUN, and PhishTool in a typical investigation workflow |
| [The Greenholt Phish](Phishing/Labs/The-Greenholt-Phish) | Header analysis, SPF/DMARC validation, and malicious CAB attachment triage |
| [Snapped Phish_ing Line](Phishing/Labs/Snapped-Phish_ing-Line) | Full campaign teardown: exposed phishing kit, credential harvesting, PHP exfiltration logic |

### 📊 SIEM
| Write-up | Description |
|---|---|
| [Introduction to SIEM](SIEM/Concepts) | Core SIEM concepts: log collection, normalization, correlation, alerting |
| [Splunk](SIEM/Splunk/Introduction) | SPL basics, architecture, and typical analyst workflow |
| [Elastic Stack (ELK)](SIEM/Elastic/Introduction) | Elasticsearch, Logstash, Kibana, and Beats |

### 🕵️ Threat Hunting
| Write-up | Description |
|---|---|
| [Warzone 1](Threat-Hunting/Network-Traffic/Warzone-1) | IDS alert triage using Brim (Zeek) and Wireshark to confirm C2 activity |

---

## 🧠 Skills demonstrated

`Log Analysis` `SIEM (Splunk, Elastic)` `EDR` `Phishing Triage` `Malware Triage` `Packet Analysis (Wireshark, Brim/Zeek)` `MITRE ATT&CK Mapping` `Sigma Rule Development` `IOC Extraction` `Threat Intelligence (VirusTotal, Cisco Talos)` `Incident Documentation`

---

## 🗺️ Roadmap

- [ ] More threat hunting labs (network + endpoint)
- [ ] Detection engineering write-ups (Sigma → SIEM rule conversion)
- [ ] Cloud security fundamentals
- [ ] Digital forensics basics

---

## 📫 Contact

Feel free to connect or reach out — always open to feedback on these write-ups.

**LinkedIn:** [Kendall A. Chacon Vargas](https://www.linkedin.com/in/kndch/)
**GitHub:** [Kendall-Sec](https://github.com/Kendall-Sec)
