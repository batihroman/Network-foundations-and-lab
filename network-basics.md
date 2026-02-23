Networking Fundamentals.

1. OSI Layers and Functions.
-  Layer 7 (Application): The layer users interact with, including protocols such as HTTP/HTTPS, DNS, and FTP.
• Layer 6 (Presentation): Responsible for data formatting, and encryption/decryption (e.g., SSL/TLS).
• Layer 5 (Session): Starts, maintains, and stops the communication sessions between applications.
• Layer 4 (Transport): Does the transport of data. Uses TCP (connection-oriented) and UDP (connectionless) protocols.
• Layer 3 (Network): The "routing" layer. It uses IP addresses to determine the next hop for data and handles packet break down.
• Layer 2 (Data Link): The "switching" layer. It uses Media Access Control (MAC) addresses for communication between devices.
• Layer 1 (Physical): The physical layer involves cables, connectors, and wireless frequencies.

2. TCP and UDP.
- TCP is connection-oriented, reliable, controls the flow of the files, and is used in web traffic, Emails, file transfers.
- UDP is connectionless, unreliable, doesn't control the flow, and is used for Voice over IP, streaming and DNS queries.

3. The TCP 3-Way Handshake
Before data transfer, TCP establishes a connection with three steps:
- SYN: Client sends a Synchronize packet with a random Initial Sequence Number.
- SYN-ACK: Server acknowledges and sends its own sequence number.
- ACK: Client acknowledges the server’s sequence. Both sides enter the ESTABLISHED state.

4. Domaine Name System (DNS)
- DNS translates human-readable Fully Qualified Domain Names (FQDNs) into IP addresses.
- System starts at the root (.) and goes through Top-Levl Domains (.com, .org, or country codes .uk) to specific domains.
- Non-authoritative servers cache DNS results for a duration defined by the Time to Live (TTL) value to improve performance and reduce network traffic.
- Security Extensions:
    ◦ DNSSEC: Uses digital signatures to authenticate responses.
    ◦ DNS over TLS (DoH): Uses TCP port 853 to encrypt DNS traffic.
    ◦ DNS over HTTPS (DoH): Encapsulates DNS queries within HTTPS packets on TCP port 443.

5. Dynamic Host Configuration Protocol (DHCP)
- Discover: Client broadcasts to find a server.
- Offer: Server suggests an IP address.
- Request: Client asks to use the offered address.
- Acknowledgement: Server confirms the lease.
- DHCP Relay/Helper: Because DHCP relies on broadcasts (which do not cross routers), a "DHCP Relay" or "Helper" must be configured on a router to forward requests to a central server on a different subnet.

6. Ports.
- FTP, port number TCP 20/21 for File Transfer (20 for data, 21 for control).
- SSH/SFTP, PN TCP 22, for Secure Shell/Secure File Transfer.
- DNS, PN UDP/TCP 53, for Domain Name System.
- DHCP, PN UDP 67/68.
- HTTP, PN TCP 80. (Unencrypted).
- HTTPS, PN TCP 443, secure web traffic (SSL/TLS).

7. IPv4 and Subnetting.
- IP Address: A unique identifier for every device on a network.
- Subnet Mask: A value used locally by a device to distinguish between local and remote traffic.
- Default Gateway: The IP address of a local router that allows communication outside the local subnet.
- Loopback Address: Range 127.0.0.1 through 127.255.255.255, used to test the local IP stack.
- Subnet Calculation: The number of subnets is calculated as 2n (where n is the number of borrowed subnet bits).
- Class A subnet: octet range 0-127, subnet mask: 255.0.0.0 (/8), for large networks.
- Class B subnet: octet range 128-191, subnet mask: 255.255.0.0 (/16), for medium networks.
- Class C subnet: octet range 192-223, subnet mask: 255.255.255.0 (/24), for small networks.

8. Private Addressing (RFC 1918)
Private addresses are used within internal networks and are not routable on the public internet. They must be translated to public IPs via Network Address Translation (NAT).
- 10.0.0.0/8: Over 16 million addresses.
- 172.16.0.0/12: Over 1 million addresses.
- 192.168.0.0/16: Over 65,000 addresses.
