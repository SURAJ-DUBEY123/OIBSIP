**Basic Network Scanning with Nmap**



**OASIS INFOBYTE SIP - Cyber Security Task 1**



**Objective**



The objective of this task is to perform a basic network

scan using Nmap, identify open ports and services, and

document their potential security considerations.



**Tool Used**



\- Nmap 7.99.1

\- Windows PowerShell



**Target**



The scan was performed against:



127.0.0.1



This represents the local machine and was selected to

ensure that the security assessment was performed on an

authorized system.



**Nmap Installation**



Nmap was installed on the Windows system before performing

the scans.



The installed version was verified using:



```powershell

nmap --version



**Scans Performed**



1. Basic Scan: nmap 127.0.0.1

&#x20;   

This scan identifies open TCP ports on the target.



2\. Service Version Detection: nmap -sV 127.0.0.1



This scan identifies the services and versions running on open ports.



3\. Operating System Detection: nmap -O 127.0.0.1



This scan identifies the operating system as Microsoft Windows 11 23H2.



**Results**



Port 135/tcp -- Microsoft RPC -- Adds windows networking attack surface



Port445/tcp -- Microsoft-DS/SMB -- Should be restricted on untrusted networks



Port 8254/tcp -- PremiereOpinion related process -- Bound to localhost



Port 8888/tcp -- PremiereOpinion service -- Listens on all IPv4 interfaces



A detailed analysis is available in nmap\_scan\_results.txt



**Security Obervations**



The scan identified four open ports. Open ports indicate

that services are listening, but an open port by itself

does not prove that the service is vulnerable.



Port 8254 was found to be associated with pmropn.exe and

was bound only to 127.0.0.1.



Port 8888 was associated with the PremierOpinion

pmservice.exe service and was listening on 0.0.0.0.

Firewall checks did not establish whether the service is

remotely accessible.



Ports 135 and 445 are associated with Windows networking

functionality and should be appropriately protected.



**Screenshots**



The screenshots folder contains screenshots of:

1.Basic Nmap scan

2.Service version scan

3.Operating system detection



**Ethical Considerations**



This project was performed against 127.0.0.1, the local

machine, for educational and authorized security testing.



**Conclusion**



Nmap successfully identified the open ports and provided

information about the services running on the local system.

Further investigation using Windows PowerShell helped map

the less clearly identified ports to their associated

processes.

