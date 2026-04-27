# phishing_typosquatting-8817
# 🛡️ Incident Report: Phishing via Typosquatting Domain – Case 8817

**Case ID:** 8817
**Date:** June 10, 2025
**Exercise Source:** LetsDefend – SOC Simulation
**Severity:** Medium – Phishing (Typosquatting)

---

## 🔎 Executive Summary

A phishing alert was triggered by an email sent from a domain impersonating Microsoft through typosquatting. The message, directed at user `c.allen@thetrydaily.thm`, contained a link to a spoofed login page hosted on the fraudulent domain `m1crosoftsupport.co`. Unlike previous cases, the firewall **did not block** the connection — the user successfully reached the malicious site, which prompted **incident escalation** for further investigation and containment.

---

## 🧪 Technical Analysis

| Field | Value |
|---|---|
| **Sender** | `no-reply@m1crosoftsupport.co` |
| **Recipient** | `c.allen@thetrydaily.thm` |
| **User Internal IP** | `10.20.2.25` |
| **Malicious Link** | `https://m1crosoftsupport.co/login` |
| **Resolved Destination IP** | `45.148.10.131` |

### Threat Intelligence Findings

- **VirusTotal:** 13 antivirus engines flagged the IP as malicious.
- **AbuseIPDB:** IP `45.148.10.131` has multiple abuse reports on record.
- **Domain Analysis:** Domain employs typosquatting — replacing the letter `o` with the digit `1` (`m1crosoftsupport.co`) to mimic a legitimate Microsoft support domain.
- **Firewall:** Connection was **permitted** — no perimeter blocking occurred.
- **SIEM (Splunk):** User click event was logged, confirming successful access to the malicious URL.

---

## 🧾 Indicators of Compromise (IOCs)

| Type | Value | Notes |
|---|---|---|
| Email | `no-reply@m1crosoftsupport.co` | Sent from typosquatted domain |
| URL | `https://m1crosoftsupport.co/login` | Fake Microsoft login page |
| IP | `45.148.10.131` | Malicious IP flagged in VirusTotal and AbuseIPDB |
| User | `c.allen@thetrydaily.thm` | Affected user account |
| Internal IP | `10.20.2.25` | Workstation IP of affected user |

---

## 🗺️ MITRE ATT&CK Mapping

| Technique ID | Name | Description |
|---|---|---|
| T1566.002 | Phishing: Spearphishing Link | Malicious link delivered via email |
| T1204.001 | User Execution: Malicious Link | User clicked and accessed the phishing link |
| T1583.001 | Acquire Infrastructure: Domains | Attacker registered a typosquatted domain to deceive the victim |

---

## 🚨 Final Verdict

| | |
|---|---|
| **Classification** | ✅ Confirmed Malicious |
| **Impact** | ⚠️ High — user successfully reached the malicious site |
| **Escalation Required** | 📈 Yes — escalated to Tier 2 for forensic analysis |

---

## 🛡️ Response Actions Taken

- Incident escalated to the Tier 2 response team for deeper forensic investigation.
- Malicious domain `m1crosoftsupport.co` and IP `45.148.10.131` blocked at firewall and proxy level.
- Forensic analysis requested on `c.allen`'s workstation to check for credential harvesting or further compromise.
- Targeted security awareness communication issued to the affected user and broader team.

---

## 📘 Lessons Learned

- Typosquatted domains can bypass basic email filtering rules, as the domain itself may not yet be in known blocklists at the time of delivery.
- This case highlights a **gap in perimeter controls** — the firewall permitted access to an actively malicious host, underscoring the need for DNS filtering and reputation-based URL inspection.
- Proactive SIEM alerting on suspicious `.co` TLDs and lookalike domains should be considered as an additional detection layer.
- Early log analysis in Splunk was critical in confirming user interaction and accelerating the escalation decision.

---

## 📎 Evidence

### 📌 SIEM Alert (Splunk)

**Initial alert triggered in Splunk**
![caso2](https://github.com/user-attachments/assets/72e7a447-e7d2-479d-ad9d-27b5cec4546d)

**User click logged — firewall allowed the connection**
![caso2-1](https://github.com/user-attachments/assets/1936d795-a90b-4847-8332-b02529e8dca3)

### 📌 VirusTotal Analysis

**13 engines detected the destination IP as malicious**
![virustotal](https://github.com/user-attachments/assets/30b0a22f-7fc3-4d6e-a3ea-129c3547bec7)

### 📌 Reporte en AbuseIPDB

- La IP ha sido reportada muchas veces
![abuse](https://github.com/user-attachments/assets/207c227b-d5e8-4291-9a62-51a9a5ec7cff)



