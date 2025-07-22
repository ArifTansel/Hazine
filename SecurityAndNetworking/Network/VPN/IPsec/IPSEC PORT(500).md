
#### VPN

![[Pasted image 20250716110448.png]]

A virtual private network (VPN) is an Internet security service that allows users to access the Internet as though they were connected to a private network.
Some of the most common reasons people use VPNs:
-  protect against snooping on public WiFi
- connect to a business’s internal network for the purpose of remote work 
- circumvent Internet censorship


#### IPSEC
It is often used to set up VPNs, and it works by encrypting IP packets, along with authenticating the source where the packets come from.

 The Internet Protocol is the main routing protocol used on the Internet; it designates where data will go using IP addresses. IPsec is secure because it adds encryption* and authentication to this process.
 
 VPN connections take place over public networks, but the data exchanged over the VPN is still private because it is encrypted.

Many VPNs use the IPsec protocol suite to establish and run these encrypted connections. However, not all VPNs use IPsec. Another protocol for VPNs is SSL/TLS, which operates at a different layer in the OSI model than IPsec.

## How does IPsec work?

IPsec connections include the following steps:

- **Key Exchange**
- **Packet headers and trailers:** . IPsec adds several headers to data packets containing authentication and encryption information. IPsec also adds trailers, which go after each packet's payload instead of before.
- **Authentication** : This ensures that packets are from a trusted source and not an attacker. 
- **Encryption** :  IPsec encrypts the payloads within each packet and each packet's IP header
- **Transmission** : IPsec uses UDP because this allows IPsec packets to get through firewalls. 
- **Decryption** : At the other end of the communication, the packets are decrypted


## What protocols are used in IPsec?

**Authentication Header (AH):**
**Encapsulating Security Protocol (ESP): **

#### MODES : 

- Transport Mode : In transport mode, the payload of each packet is encrypted, but the original IP header is not.
	- **Only the payload (TCP/UDP + application data) is encrypted**.
```css
[IP header][ESP header][Encrypted payload][ESP trailer][ESP auth (optional)]
```

- Tunnel Mode : IPsec tunnel mode is used between `two dedicated routers`, with each router acting as one end of a virtual "tunnel" through a public network.  In IPsec tunnel mode, the original IP header containing the final destination of the packet is encrypted.  To tell intermediary routers where to forward the packets, IPsec adds a new IP header
	- Used for **gateway-to-gateway** or **gateway-to-host** VPNs.
	- The **entire original IP packet (header + payload) is encrypted**.
	- A **new IP header** is added outside to route the packet.
```css
[New IP header][ESP header][Encrypted (Original IP header + payload)][ESP trailer][ESP auth (optional)]
```



## How does IPsec impact MSS and MTU?

MSS(Maximum Segment Size) and MTU(Maximum Tranmission Unit) are two measurements of packet size. 
Packets can only reach a certain size (measured in bytes) before computers, routers, and switches cannot handle them. 
MSS measures the size of each packet's payload, while MTU measures the entire packet, including headers. Packets that exceed a network's MTU may be fragmented, meaning broken up into smaller packets and then reassembled.
Packets that exceed the MSS are simply dropped.