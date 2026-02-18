# Action Model – Ransomware Detection & Response Workflow

## Objective
Create an automated system that detects ransomware-like activity on servers or domains, alerts administrators, contains threats, ensures secure backups, and generates incident reports.

## Step 1: File Integrity Monitoring 
**Purpose:** Detect abnormal file modifications that could indicate ransomware activity.  

**Actions:**
1. Install Wazuh agent on the server: https://documentation.wazuh.com/current/installation-guide/
2. Configure monitoring for critical directories:
   - `/var/www/`
   - `/etc/`
   - `/home/`
3. Generate baseline file hashes for comparison.

**Output:** Normal system file baseline established.

---

## Step 2: Detect Suspicious File Activity
**Purpose:** Identify ransomware-like behavior early.

**Detection Rules:**
- More than 500 file modifications within 2 minutes
- File extensions change to `.locked`, `.encrypted`, etc.
- Unknown processes modifying multiple files

**Output:** Alerts triggered on abnormal behavior.

---

## Step 3: Monitor Network Traffic
**Purpose:** Detect command-and-control communication.  

**Actions:**
1. Deploy Suricata IDS: https://suricata.io/
2. Monitor outbound connections for:
   - Tor exit nodes
   - Unknown foreign IPs
   - DNS tunneling patterns
3. Flag abnormal traffic spikes.

**Output:** Network-level ransomware indicators detected.

---

## Step 4: Automated Alerting
**Purpose:** Notify security admins immediately.

**Actions:**
- Slack webhook setup: https://api.slack.com/messaging/webhooks
- Include in alert:
  - Hostname
  - Time detected
  - Process name
  - Number of affected files
  - Recommended containment action

**Output:** Real-time notifications delivered.

---

## Step 5: Automated Containment
**Purpose:** Prevent ransomware from spreading.

**Actions:**
- Quarantine affected server (block outbound traffic)
- Disable compromised user accounts
- Stop suspicious processes
- Temporarily lock shared file systems

**Output:** Threat contained within seconds.

---

## Step 6: Backup Verification & Recovery
**Purpose:** Ensure recovery without paying ransom.

**Actions:**
- Enable immutable backups (AWS S3 Object Lock): https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html
- Daily verification of backup integrity
- Maintain offline backup copies weekly

**Output:** Secure recovery plan in place.

---

## Step 7: Incident Report Generation
**Purpose:** Document attacks and response actions.

**Output Requirements:**
- File format: PDF
- Filename pattern: `ransomware_incident_report_YYYY-MM-DD.pdf`
- Delay: Wait 5 seconds for charts to fully load
- Save location: `/reports/security/incidents/`
- Upload destination: Google Drive folder `ActionModel → Security Reports → Incidents`
- Annotation: Highlight any spike above threshold (e.g., >500 file changes/min)

**Output:** Clear documented incident report.

---

## Step 8: Review & Continuous Improvement
**Daily Checks:**
- Alerts triggering correctly
- Containment actions working
- Backups verified

**Weekly Review:**
- Analyze false positives
- Update detection thresholds
- Safe ransomware simulation drills

**Monthly Audit:**
- Improve detection rules
- Update incident response procedures

**Output:** System remains effective over time.
