# actionmodel-ransomware-detection
Defensive workflow to detect and respond to ransomware like attacks on servers and domains, using action model principles
# Action Model Ransomware Detection Workflow

## Project Overview
This repository contains a defensive cybersecurity workflow designed to detect and respond to ransomware-like activity on servers, domains, or applications. The workflow continuously monitors critical files and network activity, triggers alerts, automates containment actions, and ensures recovery through immutable backups. It also generates incident reports for analysis and improvement.

The purpose is **defensive only**: preventing ransomware-style attacks and protecting infrastructure.

## Objectives
- Detect abnormal file modifications and suspicious encryption behavior
- Identify unusual network activity and command-and-control communication
- Alert administrators in real-time via Slack or email
- Automatically contain affected systems to prevent spread
- Ensure recovery using secure backups
- Generate incident reports for forensic review
- Continuously review and improve detection rules

## Workflow Components
1. **File Integrity Monitoring (FIM)** – Monitors critical directories for unusual changes.
2. **Behavioral Detection** – Detects rapid file modifications, suspicious file extensions, and unknown processes.
3. **Network Monitoring** – Observes outbound connections for anomalies.
4. **Alerting** – Sends real-time notifications through Slack or email.
5. **Containment** – Quarantines affected systems and stops harmful processes.
6. **Backup & Recovery** – Uses immutable backups for safe restoration.
7. **Reporting** – Generates PDF incident reports and dashboard summaries.
8. **Review & Improvement** – Continuous evaluation to reduce false positives and improve detection.

## Usage Instructions
- See [workflow.md](workflow.md) for full step-by-step instructions.
- Use diagrams in `diagrams/` for architecture understanding (optional).
- Reference `resources/config_sample.json` for example configuration files.
- Ensure credentials and environment setup are completed as described in `docs/instructions.md` (optional).

## Requirements
- Wazuh Monitoring Platform: [https://wazuh.com/](https://wazuh.com/)
- Suricata IDS: [https://suricata.io/](https://suricata.io/)
- Slack Webhook URL: [https://api.slack.com/messaging/webhooks](https://api.slack.com/messaging/webhooks)
- Immutable backups (AWS S3 Object Lock): [https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html)
- Baseline file hashes for monitored directories
- Access to the server or domain you want to protect

## Workflow diagram
     +-------------------+
     |                   |
     |   Server / Domain |
     |                   |
     +---------+---------+
               |
               v
     +-------------------+
     |                   |
     | Wazuh Agent       |  <-- File Integrity Monitoring (FIM)
     |                   |
     +---------+---------+
               |
               v
     +-------------------+
     |                   |
     | Detection Engine  |  <-- Behavioral Detection
     | (File & Process)  |
     +---------+---------+
               |
    +----------+-----------+
    |                      |
    v                      v



## Contributing
This project focuses on **defensive security only**. Contributions should aim to improve monitoring, detection, alerting, containment, or recovery procedures.

## License
MIT License
