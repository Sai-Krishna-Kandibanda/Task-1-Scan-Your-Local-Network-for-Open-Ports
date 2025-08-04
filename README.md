# Task-1-Scan-Your-Local-Network-for-Open-Ports
Network Port Scanning with Nmap

## Objective
- The objective of this task is to discover open ports on devices within my local network using Nmap. This helps in understanding network exposure and learning how attackers might identify and exploit vulnerable services.
  
## Tools Used
- Nmap - Free and open-source network scanner (for port scanning)   
- Windows Command Prompt
  
## Steps Performed
### 1. Installed Nmap
- Downloaded Nmap from the official site: https://nmap.org -> https://nmap.org/download.html  
- Installed it for my operating system (Windows).
- Verified installation by running: 
  ```
  nmap --version
  ```
### 2. Identified Local IP Range  
- Found My IP using the following command: Windows Command Prompt: `ipconfig`
- Result: `192.168.56.***/24` (IP is masked for privacy)
- Based on this, my local network range is: `192.168.56.***/24`.

### 3. Performed Different Scans  
***Basic Ping Scan (Discover live hosts)***  
- Helps us to find hosts that are up without scanning ports.
- ***Command***:
  ```
  nmap -sn 192.168.56.***/24
  ```
- Output of this scan is saved in a text file using: Basic Ping Scan.txt
    
***Simple Port Scan (Check common ports)***  
- Checks the most common ports on live hosts.
- ***Command***:  
  ```
  nmap 192.168.56.***/24
  ```
- Output of this scan is saved in a text file using: Simple Port Scan.txt

***Stealth SYN Scan (More detailed)***  
- Stealthily discovers all open TCP ports. This performs a stealthy TCP SYN scan on all devices in the subnet.
- ***Command***:
  ```
  nmap -sS 192.168.56.***/24
  ```
- Output of this scan is saved in a text file using: Stealth Scan.txt

***Intense Scan***
- This scan combines several scanning techniques:
  - -sS: SYN scan as in Stealth Scan
  - -T4: Faster scan timing
  - -A: Enables OS detection, version detection, script scanning, and traceroute
  - -v: Verbose output for detailed progress feedback
- This scan delivers detailed information about the devices, open ports, services running, operating systems, and network topology.
- ***Command***:
  ```
  nmap -T4 -A -v 192.168.56.***/24
  ```
- Output of this scan is saved in a text file using: Intense Scan.txt  

### 4. ***Potential Security Risks from Open Ports***
- The scan revealed the following open ports and associated services on the target device:  
  - Port: 135 | Protocol: TCP |	Service: msrpc |	Description: Microsoft Windows Remote Procedure Call
    - Potential Security Risks: This port can be exploited for remote code execution if vulnerable. It is a known target for malware and worms.
  
  - Port: 139 | Protocol: TCP |	Service: netbios-ssn |	Description: Microsoft Windows NetBIOS Session Service
    - Potential Security Risks: Exposes file sharing and may allow unauthorised access if not properly secured. Vulnerable to certain attacks like SMB relay.

  - Port: 445 | Protocol: TCP |	Service: microsoft-ds |	Description: Microsoft Directory Services (SMB)
    - Potential Security Risks: Frequently targeted by ransomware and exploits such as EternalBlue if unpatched. Critical to secure or restrict.

  - Port: 902 | Protocol: TCP |	Service: vmware-auth |	Description: VMware Authentication Daemon using VNC/ SOAP
    - Potential Security Risks: Open VMware ports may expose the host to unauthorised remote management if not properly secured.
   
  - Port: 912 | Protocol: TCP |	Service: vmware-auth | Description: VMware Authentication Daemon (VNC/SOAP)
    - Potential Security Risks: Similar risks to port 902 could provide access to VM management interfaces.
   
  - Port: 3306 | Protocol: TCP |	Service: mysql |	Description: MySQL Database (unauthorised access possible)
    - Potential Security Risks: Unauthorised access risk if not properly secured with strong credentials. Can lead to data breaches.
      
***Summary of Risks***:
- Ports associated with Windows RPC and SMB (135, 139, 445) are common attack vectors for malware and ransomware. Ensuring these services are patched, firewalled, or disabled if unused is crucial.  
- VMware-related ports (902, 912) could permit unauthorised remote control of virtual machines if exposed without proper authentication.  
- The MySQL port (3306) being open and unauthenticated is risky, as attackers can access or manipulate databases, potentially leading to data theft or corruption.  

***Recommended Actions***:
- Close or restrict access to unnecessary ports.
- Apply all security patches and updates.
- Use firewalls to control external access to these services.
- Enforce strong passwords and authentication on all exposed services.

## Concepts Learned
- Port scanning  
- TCP SYN scanning  
- Local network reconnaissance  
- Identifying IP ranges  
- Basic risk analysis based on open ports

## Final Outcome
- By completing this task, I developed basic network reconnaissance skills, gained familiarity with Nmap, and understood how open ports may expose services to attackers. This activity emphasised the importance of regular network audits and port management in cybersecurity.
