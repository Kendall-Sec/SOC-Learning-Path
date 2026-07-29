# Summit - Sample 3

**Type:** 🧪 Investigation Write-up

## Scenario

A suspicious executable was analyzed in a sandbox environment after exhibiting malicious behavior on a Windows endpoint. The objective was to identify the attacker's actions, determine their security impact, and create a behavioral detection rule capable of identifying similar activity in future incidents.

---

# Objective

- Analyze the malware's behavior.
- Identify malicious registry modifications.
- Map the activity to the MITRE ATT&CK framework.
- Develop a Sigma rule to detect the behavior.

---

# Investigation

## Initial Findings

Sandbox analysis revealed that the malware modified a Windows Defender registry key responsible for Real-Time Protection.

The following registry value was changed:

```
Registry Key:
HKLM\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection

Registry Value:
DisableRealtimeMonitoring = 1
```

![Registry Activity](images/registry.png)

---

## Analysis

The malware attempted to disable Microsoft Defender's Real-Time Protection by modifying the `DisableRealtimeMonitoring` registry value.

Disabling endpoint protection is a common technique used by attackers to evade detection and allow additional malicious payloads to execute without interference.

This behavior is significantly more valuable for detection than relying on static indicators such as filenames or hashes, since the malware could easily be renamed while still performing the same action.

---

# Security Impact

If successful, disabling Real-Time Protection may allow an attacker to:

- Execute additional malware without immediate detection.
- Reduce endpoint visibility.
- Increase persistence within the compromised system.
- Bypass security controls before deploying secondary payloads.

---

# MITRE ATT&CK Mapping

| Category  |                           Value                               |                          
|-----------|---------------------------------------------------------------|
| Tactic    | TA0005 – Defense Evasion                                      |
| Technique | T1562.001 – Impair Defenses: Disable or Modify Security Tools |

The observed registry modification directly aligns with the ATT&CK technique used to impair endpoint security controls.

---

# Detection Engineering

Rather than detecting the malware itself, a behavioral detection rule was created.

The Sigma rule monitors Windows Sysmon events associated with modifications to the Windows Defender Real-Time Protection registry key.

Detection logic:

- Registry Key

```
HKLM\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection
```

- Registry Value

```
DisableRealtimeMonitoring = 1
```

- Sysmon Event ID

```
4663
```

![Sigma Rule Builder](images/sigma-builder.png)

---

## Generated Sigma Rule

The generated Sigma rule detects future attempts to disable Windows Defender by monitoring registry modifications associated with the `DisableRealtimeMonitoring` value.

![Sigma Rule](images/sigma-rule.png)

This behavior-based detection is significantly more resilient than detecting a specific malware hash or filename because it focuses on attacker techniques rather than static indicators.

---

# Containment Recommendation

If this behavior is detected on an endpoint, the recommended response includes:

- Isolate the affected host.
- Perform a full malware scan.
- Verify Windows Defender configuration.
- Restore Real-Time Protection if disabled.
- Investigate additional persistence mechanisms.
- Review lateral movement and privilege escalation activity.

---

# Lessons Learned

- Registry modifications are valuable behavioral indicators during malware investigations.
- Attackers frequently attempt to disable endpoint security products to evade detection.
- Mapping malicious behavior to the MITRE ATT&CK framework improves investigation consistency and communication.
- Sigma provides a vendor-neutral method for detecting attacker behavior across multiple SIEM platforms.
- Behavior-based detections are more durable than detections based solely on Indicators of Compromise (IOCs).

---

# Conclusion

The investigation identified an attempt to disable Microsoft Defender's Real-Time Protection through a registry modification. Instead of relying on static Indicators of Compromise, a Sigma rule was developed to detect this behavior in future attacks. This approach aligns with modern SOC practices by focusing on attacker Tactics, Techniques, and Procedures (TTPs), improving long-term detection capabilities against similar threats.
