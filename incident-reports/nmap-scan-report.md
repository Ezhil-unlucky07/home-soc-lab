Incident Information
    Field	        Details
    Incident ID	    : IR-2026-002
    Incident Name	: Network Port Scan Detection
    Severity	        : Medium
    Category	        : Reconnaissance
    Detection Source	: IDS / SIEM
    Status          : Closed
    
    
Executive Summary

    A network reconnaissance activity was detected originating from a single internal host. The attacker used Nmap to enumerate open ports on multiple systems. The scan was identified through IDS alerts and firewall logs.

Affected Assets
    Scanner IP:172.16.139.1
    Target IP:172.16.139.131
    Hostname:pc1
    
Timeline

    Time	Event
    11:00	Port scan initiated
    11:01	IDS generated alert
    11:03	Firewall logs reviewed
    11:08	Source host isolated
    11:15	Investigation completed

Indicators of Compromise

Scanner IP : 172.16.139.1

Target IP : 172.16.139.131

Common Ports :

    22
    80
    135
    139
    445
    3389
    
Investigation 
 
 Findings
 
     Sequential scanning detected.
     TCP SYN packets observed.
     Large number of destination ports accessed within a short timeframe.
     No exploitation attempts observed.

MITRE ATT&CK

    Technique	     ID
    
    Active Scanning	T1595

Containment

    Isolated scanning host
    Blocked scanner IP
    Reviewed firewall rules
    Increased network monitoring
    
Recommendations

    Deploy IDS signatures
    Block unauthorized scanning
    Segment sensitive networks
    Enable continuous monitoring
    

Final Status : Resolved
