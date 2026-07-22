# Incident Report: SSH Brute Force Attack

## Incident Information

 Field           Details                         
 
 Incident ID     IR-2026-001                     
 Incident Title  SSH Brute Force Attack Detected 
 Date            06 July 2026                    
 Detection Time  14:32 UTC                       
 Analyst         SOC Analyst                     
 Severity        Medium                          
 Status          Closed                          



# 1. Executive Summary

On 06 July 2026 at 14:32 UTC, the Security Operations Center (SOC) detected a brute-force attack targeting the SSH service on a Linux server. A single external IP address repeatedly attempted to authenticate using multiple usernames within a short period. The attack was identified through authentication logs and SIEM alerts. Investigation confirmed that no login attempts were successful and there was no evidence of unauthorized access or compromise. The malicious IP address was blocked, and the incident was closed after verification.



# 2. Affected Asset

 Asset             Value               
  
 Hostname          Ubuntu-Server       
 IP Address        172.16.139.131        
 Operating System  Ubuntu 22.04 LTS    
 Service           SSH (TCP Port 22)   
 Asset Owner       Infrastructure Team 



# 3. Detection Details

**Detection Source**

* SIEM Alert
* Linux Authentication Logs (`/var/log/auth.log`)

**Alert Name**
SSH Brute Force Attack Detected

**Detection Description**

The SIEM generated an alert after detecting more than 100 failed SSH authentication attempts from a single external IP address within two minutes. The activity exceeded the organization's alert threshold for SSH login failures.



# 4. Timeline

 Time (UTC)  Event                                  
 20:06       First failed SSH login attempt detected 
 20:07       Multiple failed login attempts observed 
 20:08      SIEM generated brute-force alert        
 20:09      Investigation initiated by SOC analyst  
 20:11      Source IP address blocked by firewall 
 20:18      Authentication logs reviewed            
 20:28      No evidence of successful login found   
 20:33      Incident closed                         



# 5. Indicators of Compromise (IOCs)

**Source IP Address**

* 172.16.139.1

**Destination IP**

* 172.16.139.131

**Destination Port**

* TCP/22

**Targeted Usernames**

* admin

**Log Source**

* /var/log/auth.log



# 6. Evidence

### Authentication Log Sample


2026-07-06T05:20:06.616946+00:00 ubuntuserver sshd-session[5138]: Failed password for admin from 172.16.139.1 port 40294 ssh2
2026-07-06T05:20:06.736915+00:00 ubuntuserver sshd-session[5134]: Failed password for admin from 172.16.139.1 port 40300 ssh2
2026-07-06T05:20:06.952346+00:00 ubuntuserver sshd-session[5136]: Failed password for admin from 172.16.139.1 port 40298 ssh2
2026-07-06T05:20:07.225648+00:00 ubuntuserver sshd-session[5135]: Failed password for admin from 172.16.139.1 port 40296 ssh2



### Investigation Summary

* Total failed login attempts: 156
* Successful logins: 0
* Unique attacker IPs: 1
* Targeted accounts: 4
* Privilege escalation observed: No
* Malware detected: No
* Persistence established: No



# 7. Root Cause Analysis

The incident resulted from an automated SSH brute-force attack originating from an external IP address. The attacker attempted to gain unauthorized access by repeatedly guessing passwords for common user accounts. Password authentication was enabled on the server, making it a target for automated credential-guessing attacks. Existing monitoring controls successfully detected the attack before any unauthorized access occurred.


# 8. MITRE ATT&CK Mapping

 Tactic             Technique                   Technique ID 
 
 Credential Access  Brute Force                 T1110        
 Initial Access     Valid Accounts (Attempted)  T1078        



# 9. Response Actions

The SOC analyst reviewed authentication logs and validated the SIEM alert. The attacker IP address was immediately blocked at the firewall. Additional log analysis confirmed that no authentication attempts were successful and that no suspicious activity occurred after the attack. The server's integrity was verified, and continuous monitoring was maintained to detect any further malicious activity.



# 10. Recommendations

* Disable password-based SSH authentication and enforce SSH key authentication.
* Disable direct root login over SSH.
* Implement Fail2Ban to automatically block repeated failed login attempts.
* Restrict SSH access to trusted IP addresses using firewall rules.
* Enable Multi-Factor Authentication (MFA) for administrative accounts where supported.
* Monitor authentication logs continuously for suspicious login activity.
* Conduct regular reviews of SSH configuration and access controls.



# 11. Conclusion

The SSH brute-force attack was successfully detected and contained before any unauthorized access occurred. Analysis confirmed that all login attempts failed and the targeted Linux server remained uncompromised. The implemented security monitoring controls effectively identified the attack, allowing prompt response and mitigation. Recommendations have been provided to strengthen SSH security and reduce the likelihood of similar attacks in the future.
