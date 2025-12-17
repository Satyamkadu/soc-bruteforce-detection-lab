# Incident Report: SSH Brute Force Attack (Lab Simulation)

## Incident Metadata
- **Incident ID:** SOC-LAB-001
- **Date Detected:** 15 Dec 2025
- **Reported By:** Satyam Kadu
- **Environment:** Self-hosted Kali-Ubuntu Lab
- **Incident Type:** Brute Force Attack (SSH)
- **Severity:** Medium
- **Status:** Closed (Lab Simulation)

## Executive Summary
On 15 Dec 2025, a simulated SSH brute-force attack was detected against an Ubuntu system within a controlled lab environment. Multiple failed authentication attempts targeting the SSH service were observed originating from a single source host. Log analysis revealed abnormal authentication failure patterns consistent with brute-force activity. During the attack, a valid credential was successfully identified, resulting in an unauthorized login attempt. Automated security controls limited further access and prevented repeated authentication attempts. The incident was classified as medium severity due to confirmed brute-force behavior with limited impact.

## Environment Details
- **Victim System:** Ubuntu 24.04 (SSH server)
- **Attacker System:** Kali Linux 2025.04
- **Network Configuration:** Bridged Adapter (Internal lab network)
- **Targeted Service:** OpenSSH (Port 22)
- **Log Sources:** /var/log/auth.log

## Detection & Analysis

### Initial Detection
The incident was initially identified through review of authentication logs showing repeated SSH login failures over a short time period. The volume and frequency of failed authentication attempts indicated abnormal SSH activity requiring further analysis.

### Log Analysis
- Authentication events were analyzed from `/var/log/auth.log`.
- Multiple failed SSH login attempts were recorded over a short period.
- All authentication attempts originated from a single source IP address.
- The same user account was repeatedly targeted during the attack.
- Login failures occurred in rapid succession, consistent with automated activity.
- A successful authentication was observed following multiple failed attempts.

### Attack Characteristics
- High-frequency SSH authentication attempts.
- Repeated password guessing behavior.
- Consistent source IP throughout the attack window. 
- Behavior consistent with brute-force automation.

## Impact Assessment
- An unauthorized SSH login occurred during the attack window.
- The incident impacted a single Ubuntu system within the lab environment.
- No persistence mechanisms or privilege escalation were observed.
- No data modification, exfiltration, or integrity impact was identified.
- No service disruption or availability issues were detected.

## Severity Justification
- Repeated unauthorized authentication attempts confirmed active brute-force behavior.
- Login attempts occurred in rapid succession, indicating automated password guessing.
- The attack scope was limited to a single system and user account.
- While initial access occurred, further access and escalation were restricted, limiting overall impact.

## Containment Actions
- Automated controls temporarily blocked the attacking source IP after multiple failed SSH authentication attempts.
- SSH access from the identified source was restricted, preventing further login attempts during the attack window.
- The incident was contained without impacting other systems or services.

## Mitigation & Preventive Measures
- fail2ban was configured to monitor SSH authentication logs and automatically ban source IPs after three failed login attempts.
- Temporary IP bans were enforced for a duration of ten minutes to disrupt brute-force activity.
- SSH authentication monitoring was strengthened to improve visibility into repeated login failures.
- Additional hardening measures were identified to further reduce the SSH attack surface.

## Lessons Learned
- Repeated SSH authentication failures provide early indicators of brute-force activity.
- Automated security controls significantly reduce the impact of credential-based attacks.
- Centralized log review enables timely detection and response to suspicious behavior.
- Credential-based services such as SSH remain common targets for automated attacks.

## Recommendations
- Enforce stronger authentication mechanisms for SSH access.
- Regularly review authentication logs to identify abnormal login patterns.
- Implement alerting for repeated authentication failures to improve response time.
- Apply additional SSH hardening measures to further reduce the attack surface.
- Periodically test detection and response processes using controlled lab simulations.
