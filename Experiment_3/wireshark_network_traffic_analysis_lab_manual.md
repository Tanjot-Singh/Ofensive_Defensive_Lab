# Experiment: Basic Network Traffic Analysis with Wireshark

## Aim

To capture and examine network packets using Wireshark and identify suspicious activity or cleartext credentials in a simulated network.

## Requirements

- Kali Linux
- Metasploitable 2
- Wireshark
- VirtualBox or VMware
- Isolated Host-only/Internal Network
- Metasploitable IP: `192.168.56.100`

> **Safety:** Perform this experiment only on the isolated lab network using your own virtual machines and test credentials.

---

## 1. Theory

**Wireshark** is a network protocol analyzer used to capture and inspect network packets.

It can help identify network protocols, source and destination IP addresses, TCP connections, unencrypted application traffic, cleartext authentication information, and suspicious network activity.

Basic process:

```text
Start packet capture
        ↓
Generate network traffic
        ↓
Apply Wireshark filters
        ↓
Inspect packets
        ↓
Follow TCP streams
        ↓
Identify cleartext/suspicious data
        ↓
Document observations
```

---

## 2. Verify Network Connectivity

On Kali:

```bash
ip addr
```

Identify the interface connected to the `192.168.56.0/24` lab network.

Test connectivity:

```bash
ping 192.168.56.100
```

Expected output:

```text
64 bytes from 192.168.56.100: icmp_seq=1 ttl=64 time=...
```

---

## 3. Start Wireshark

Start Wireshark:

```bash
sudo wireshark
```

Select the network interface connected to the lab network and start the packet capture.

---

## 4. Generate Network Traffic

From Kali:

```bash
ping 192.168.56.100
```

In Wireshark, observe:

```text
ICMP Echo Request
ICMP Echo Reply
```

Stop the ping with `Ctrl + C`.

---

## 5. Generate HTTP Traffic

If the Metasploitable web server is running:

```bash
curl http://192.168.56.100
```

In Wireshark, apply:

```text
http
```

You may observe requests such as:

```text
GET / HTTP/1.1
Host: 192.168.56.100
```

This demonstrates that HTTP traffic is not protected by TLS encryption.

---

## 6. Filter Traffic from the Target

Use:

```text
ip.addr == 192.168.56.100
```

Other useful filters:

```text
icmp
```

```text
tcp
```

```text
http
```

```text
ftp
```

---

## 7. Analyze TCP Communication

Select a TCP packet and expand:

```text
Transmission Control Protocol
```

Observe the TCP three-way handshake:

```text
SYN
 ↓
SYN/ACK
 ↓
ACK
```

---

## 8. Follow a TCP Stream

Right-click a TCP packet and select:

```text
Follow → TCP Stream
```

Wireshark reconstructs the data exchanged over that TCP connection, making application-layer communication easier to inspect.

---

## 9. Examine Cleartext FTP Traffic

Connect to the lab FTP service:

```bash
ftp 192.168.56.100
```

Use only test/lab credentials.

In Wireshark:

```text
ftp
```

FTP does not encrypt its traditional control connection, so authentication information and FTP commands may be visible in a packet capture.

You can also use:

```text
Follow → TCP Stream
```

to inspect the exchange.

---

## 10. Examine Telnet Traffic

If Telnet is enabled:

```bash
telnet 192.168.56.100
```

Use only lab/test credentials.

In Wireshark, filter:

```text
telnet
```

Telnet does not encrypt its communication, so session data may be visible in the capture.

---

## 11. Identify Suspicious Activity

Examples of activity worth investigating include:

- Unexpected connections to unfamiliar ports
- Repeated connection attempts
- Cleartext authentication
- Use of unencrypted protocols
- Unexpected source or destination IP addresses
- Unusual amounts of network traffic

Repeated connection attempts to many ports can, for example, be evidence consistent with port-scanning activity.

---

## 12. Observation Table

| Activity | Wireshark Filter | Observation |
|---|---|---|
| ICMP ping | `icmp` | Echo Request and Echo Reply packets |
| TCP traffic | `tcp` | TCP segments and connections |
| HTTP traffic | `http` | HTTP requests/responses visible |
| FTP traffic | `ftp` | FTP commands/authentication may be visible |
| Telnet traffic | `telnet` | Unencrypted session data may be visible |
| Target traffic | `ip.addr == 192.168.56.100` | Traffic involving Metasploitable |

---

## 13. Result

Network traffic between Kali Linux and the Metasploitable virtual machine was successfully captured and analyzed using Wireshark. Different protocols were identified, TCP communication was examined, and the security risks of cleartext protocols such as FTP and Telnet were demonstrated in the isolated lab environment.

---

## 14. Precautions

1. Perform packet capture only on the authorized lab network.
2. Use only your own virtual machines and test credentials.
3. Do not capture credentials or traffic belonging to other users.
4. Keep the Metasploitable VM isolated from the public Internet.
5. Do not use captured credentials outside the authorized laboratory environment.

---

## Viva Questions

### Q1. What is Wireshark?

Wireshark is a network protocol analyzer used to capture and inspect network packets.

### Q2. What is packet capture?

Packet capture is the process of recording network packets traveling through a network interface for analysis.

### Q3. What is a Wireshark display filter?

A display filter limits the packets shown in Wireshark according to specified conditions.

### Q4. What does `ip.addr == 192.168.56.100` do?

It displays packets where `192.168.56.100` is either the source or destination IP address.

### Q5. What is the TCP three-way handshake?

It establishes a TCP connection using:

```text
SYN → SYN/ACK → ACK
```

### Q6. Why are FTP and Telnet considered insecure?

Traditional FTP and Telnet do not encrypt their communication, so sensitive information transmitted through them can potentially be read from captured packets.

### Q7. What is the difference between HTTP and HTTPS?

HTTP does not provide TLS encryption for application data, while HTTPS uses TLS to encrypt communication between the client and server.
