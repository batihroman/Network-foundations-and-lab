Report 02.03.2026.
Target IP: 10.64.125.83.
Objective of the project: to perform a network enumeration against a target host in a controlled lab environment and identify exposed servises, versions, and potential attac services. 
I used a Try Hack Me AttackBox with installed Nmap to scan an existing network.

Methodology:
1. Verified host availability.
2. Performed TCP port scan using Nmap.
3. Identified service versions using -sV.
4. Executed default scripts using -sC.
5. Saved results in normal, XML, and grepable formats using -oA.

<Command used: nmap 10.64.125.83. Goal: to see open ports, their names and services.>
Open ports: 
- 22/tcp with a service "ssh"
- 53/tcp with a service "domain"
- 80/tcp with a service "http"
- 81/tcp with a service "hosts2-ns"
- 111/tcp with a service "rpcbind"
- 389/tcp with a service "ldap"Used -n to disable DNS
• Used -sC for default scripts
• Used -sV for version detection
• Saved output with -oA
- 3389/tcp with a service "ms-wbt-server"
- 5901/tcp with a service "vnc-1"
- 6001/tcp with a service "x11:1".

Filtered ports:
- 7777/tcp with a service "cbt"
- 7778/tcp with a service "interwise".

<Command used: nmap -n -sC -sV -oA initial "ip address" scan.>
What I can see from it:
- 9 Open ports.
- 2 Filtered ports.
- 989 Closed ports.
- Port 22 is open running OpenSSH 8.2p1 on Ubuntu. SSH allows remote authentication. If weak credentials exist, this service could allow remote access to the system.
- Port 53 is open running dnsmasq 2.90. This indicates the host may function as a DNS server. Misconfigurations could allow DNS information disclosure.
- Port 80 is running WebSockify Python 3.8.10. WebSockify is commonly used to proxy VNC over HTTP. This suggests a remote desktop interface may be exposed through a web based client.
- Port 81 is running Apache 2.4.41. The default Ubuntu Apache page is displayed. No custom web application is visible at the root path.
- Port 111 is running rpcbind. This service supports RPC based services such as NFS. Further enumeration is required to determine if file shares are exposed.
- Port 389 is running OpenLDAP. LDAP services frequently store authentication data and directory information. Anonymous bind or misconfiguration may allow information disclosure.
- Port 3389 is running xrdp. This indicates remote desktop access is enabled. Weak credentials could allow full graphical access to the system.
- Port 5901 is running VNC protocol 3.8. VNC may allow remote graphical access. If authentication is weak or disabled, this may provide direct system control.
- Port 6001 is running X11. Exposed X11 services can allow remote graphical interaction and potential session hijacking if access control is weak.

Command ran: nmap -p 389 --script ldap-rootdse 10.64.125.83.
What it showed: The LDAP RootDSE query revealed the naming context dc=eu-west-1,dc=compute,dc=internal. This discloses internal domain structure information. The server supports LDAPv3 and multiple authentication mechanisms including NTLM. Anonymous bind appears partially allowed, resulting in information disclosure.

Command ran: ldapsearch -x -h 10.64.125.83
What it showed: An anonymous LDAP search attempt returned error 32 No such object, indicating directory enumeration is restricted. No full directory disclosure observed.

Command ran: rpcinfo -p 10.64.125.83
What it showed: No exposed NFS service detected.

Command ran: nmap -p 3389 --script rdp-enum-encryption 10.64.125.83
What it showed: RDP encryption enumeration shows high level encryption enabled with support for CredSSP, SSL, and 128 bit encryption. Network Level Authentication appears active. While encryption is properly configured, the service remains exposed to credential attacks.

Command ran: nmap -p 5901 --script vnc-info 10.64.125.83
What it showed: The VNC service on port 5901 was probed using the vnc-info script. The script failed to retrieve server information. This suggests authentication is likely required or the server does not disclose banner details. No unauthenticated access was confirmed

Command ran: nmap -p 6001 --script x11-access 10.64.125.83
What it showed: The X11 service on port 6001 was tested using the x11-access script. The script did not confirm unauthenticated access. While the service is exposed, no direct access was identified during initial testing.

Overview:
The host appears to expose services typically restricted to internal networks. In a production environment, services such as LDAP, RPC, VNC, and X11 should not be publicly accessible.

Potential attack paths:
- Credential attacks against SSH, RDP, VNC
- LDAP enumeration
- Web directory discovery on Apache
- RPC and NFS enumeration
