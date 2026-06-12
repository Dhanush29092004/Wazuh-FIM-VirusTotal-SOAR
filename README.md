# Automated Malware Detection and Response using Wazuh, n8n, VirusTotal & Telegram

![License](https://img.shields.io/badge/License-MIT-green.svg)
![Platform](https://img.shields.io/badge/Platform-Ubuntu-orange)
![SIEM](https://img.shields.io/badge/SIEM-Wazuh-blue)
![SOAR](https://img.shields.io/badge/SOAR-n8n-red)

## Project Overview

This project implements an automated malware detection and response workflow by integrating Wazuh SIEM, n8n SOAR, VirusTotal Threat Intelligence, and Telegram notifications.

The solution continuously monitors critical directories using Wazuh File Integrity Monitoring (FIM). When a file is created, modified, or deleted, Wazuh generates an alert and forwards the event to an n8n workflow via a webhook.

The workflow extracts the file's SHA256 hash, queries VirusTotal for threat intelligence, analyzes the reputation score, and sends a real-time alert to Telegram.

The workflow was validated using the EICAR Anti-Malware Test File, resulting in a 62/76 malware detection rate from VirusTotal.

---

## Key Features

- Real-time File Integrity Monitoring (FIM)
- Automated SHA256 and MD5 hash extraction
- VirusTotal Threat Intelligence Integration
- Real-time Telegram Notifications
- Malware Detection Validation using EICAR
- Security Orchestration and Automation (SOAR)
- Automated Incident Detection Workflow

---

## Technologies Used

| Technology | Purpose |
|------------|----------|
| Wazuh | SIEM & File Integrity Monitoring |
| n8n | Security Orchestration & Automation |
| VirusTotal API | Threat Intelligence Lookup |
| Telegram Bot API | Incident Notifications |
| Ubuntu Linux | Monitoring Environment |
| Webhooks | Event Communication |

---

## Architecture

```text
File Creation / Modification
            │
            ▼
┌─────────────────────┐
│   Wazuh FIM Agent   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Wazuh Manager    │
└──────────┬──────────┘
           │ Webhook
           ▼
┌─────────────────────┐
│      n8n SOAR       │
│  Parse SHA256 Hash  │
└──────────┬──────────┘
           │
    ┌──────┴──────┐
    │             │
    ▼             ▼
┌─────────┐   ┌─────────┐
│VirusTotal│  │Telegram │
│Analysis  │  │ Alerts  │
└─────────┘   └─────────┘
```

---

## Workflow Architecture

### Step 1: File Monitoring

Wazuh File Integrity Monitoring continuously monitors sensitive directories for file changes.

### Step 2: Event Detection

When a file event occurs, Wazuh generates an alert containing:

- File path
- Username
- SHA256 hash
- MD5 hash
- Event type

### Step 3: Webhook Trigger

The alert is sent to an n8n webhook.

### Step 4: Threat Intelligence Lookup

n8n extracts the SHA256 hash and queries the VirusTotal API.

### Step 5: Security Analysis

VirusTotal returns:

- Malicious detections
- Suspicious detections
- Harmless detections
- Undetected engines

### Step 6: Alert Generation

n8n formats the information and sends a Telegram notification.

---

## Screenshots

### Wazuh FIM Detection

Wazuh detects file creation events in real time.

[Wazuh FIM Alert]<img width="913" height="501" alt="Screenshot 2026-06-11 235808" src="https://github.com/user-attachments/assets/b6bd08f8-2c98-4999-89af-22598fe3a25a" />


---

### n8n SOAR Workflow

Automated workflow responsible for extracting hashes, querying VirusTotal, and sending Telegram alerts.

[n8n Workflow]<img width="908" height="221" alt="Screenshot 2026-06-11 235852" src="https://github.com/user-attachments/assets/bd57fbb7-dd91-4dbf-89b2-9b11f036ba1d" />


---

### VirusTotal Analysis

Threat intelligence analysis performed using the SHA256 hash extracted from the monitored file.

[VirusTotal Result]<img width="822" height="308" alt="Screenshot 2026-06-11 235925" src="https://github.com/user-attachments/assets/9c1cb085-8055-466a-9672-55808915cc01" />


---

### Telegram Incident Notification

Real-time notification generated after malware reputation analysis.

[Telegram Alert]<img width="612" height="470" alt="Screenshot 2026-06-12 000004" src="https://github.com/user-attachments/assets/88550228-fec3-4c2f-9b39-c35ca701a06d" />


---

## Test Scenario

### Test File

EICAR Anti-Malware Test File

### Test Procedure

1. Create EICAR file on monitored system.
2. Wazuh FIM detects file creation.
3. Webhook triggers n8n workflow.
4. SHA256 hash extracted.
5. VirusTotal lookup performed.
6. Telegram alert generated.

### Result

| Metric | Value |
|----------|---------|
| Malicious | 62 |
| Suspicious | 0 |
| Harmless | 0 |
| Undetected | 0 |

### Verdict

🔴 MALICIOUS FILE DETECTED

---

## Sample Telegram Alert

```text
🚨 WAZUH FIM ALERT 🚨

Hostname: Ubuntu-Agent
Filename: /root/eicar.txt
Event Type: added

Malicious: 62
Suspicious: 0
Harmless: 0
Undetected: 0

Verdict:
🔴 MALICIOUS FILE DETECTED
```

---

## Skills Demonstrated

- Security Information and Event Management (SIEM)
- Security Orchestration, Automation and Response (SOAR)
- Threat Intelligence Integration
- API Integration
- Incident Detection and Response
- Linux Administration
- Cybersecurity Automation
- File Integrity Monitoring
- Malware Analysis
- Security Monitoring

---

## Future Enhancements

- Automatic malware quarantine
- Slack integration
- Email notifications
- AbuseIPDB integration
- IOC enrichment
- Automatic ticket generation
- Multi-source threat intelligence
- Dashboard reporting

---


## Author

**Chimakurthi Dhanush**

Cybersecurity Enthusiast | SIEM | SOAR | Threat Detection | Security Automation

GitHub: https://github.com/Dhanush29092004

LinkedIn: https://www.linkedin.com/in/dhanush-chimakurty-601066255/

---

## License

This project is licensed under the MIT License.
