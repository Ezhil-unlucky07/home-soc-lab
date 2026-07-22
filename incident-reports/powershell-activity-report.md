Incident Information

    Field	Details
    Incident ID   :	IR-2026-003
    Incident Name :	Suspicious PowerShell Execution
    Severity	      : High
    Category	      : Execution
    Detection Source :	Microsoft Defender / Sysmon / SIEM
    Status	      : Closed
    
Executive Summary

    The SIEM detected suspicious PowerShell execution on a Windows workstation. Analysis showed encoded PowerShell commands executed from the command line. The activity matched known attacker tradecraft commonly used for  post-exploitation.
    
Affected Assets

    Hostname:ADMIN
    Username:ADMIN
    IP Address:172.16.139.129
    Operating System:
    
Timeline

    Time  	Event
    14:10	PowerShell executed
    14:11	SIEM alert generated
    14:15	Process tree analyzed
    14:20	Endpoint isolated
    14:40	Investigation completed
    
    
Indicators of Compromise

    Process : powershell.exe

    Command : powershell.exe -ExecutionPolicy Bypass -EncodedCommand <Base64>

    Parent Process : cmd.exe

Investigation

  Findings
  
    Encoded PowerShell command detected.
    Execution Policy bypass used.
    PowerShell launched from Command Prompt.
    No persistence mechanisms identified.


MITRE ATT&CK

    Technique	                         ID
    
    PowerShell                       	T1059.001
    Command and Scripting Interpreter	T1059
    
    
Containment

    Terminated PowerShell process
    Isolated endpoint
    Collected forensic artifacts
    Performed antivirus and EDR scan
    
Recommendations

    Enable PowerShell Script Block Logging
    Enable PowerShell Module Logging
    Restrict PowerShell usage through Group Policy
    Monitor encoded PowerShell commands
    Deploy Microsoft Defender ASR rules
    
Final Status : Resolved
