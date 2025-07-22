A firewall is a security system that monitors and controls network traffic based on a set of security rules
Firewalls usually sit between a trusted network and an untrusted network;


### FireWall Types :

#### Proxy-based firewalls:

These are proxies* that **sit in between clients and servers**. A proxy-based firewall effectively prevents a direct connection between the client and server.

Similarly, a major drawback of a proxy-based firewall is that it can cause latency, particularly during times of heavy traffic.


#### Stateful firewalls:

A stateful firewall **`saves` information regarding open connections** and uses this information to analyze incoming and outgoing traffic, rather than inspecting each packet.

Stateful firewalls can also protect ports* by keeping them all closed unless incoming packets request access to a specific port. This can mitigate an attack known as port scanning. (This can be protect from like nmap scanning)

#### Next-generation firewalls (NGFW):
`Other layer protections` 
Employ a host of added features to address threats on other layers of the OSI model. Features: 

- **Deep packet inspection (DPI)** : This deep inspection can look at things like packet payloads and which application is being accessed by the packets. This allows the firewall to enforce more granular filtering rules.
- **Application awareness** : This can protect against certain types of malware that aim to terminate a running process and then take over its port.
- **Identity awareness** :  This lets a firewall enforce rules based on identity, such as which computer is being used, which user is logged in

#### Web application firewalls (WAF):
![[Pasted image 20250716131151.png]]

A WAF helps protect web applications by filtering and monitoring HTTP traffic between a web application and the Internet

#### Firewall-as-a-service (FWaaS) `cloud firewall`:
FWaaS forms a virtual barrier around cloud platforms, infrastructure, and applications, just as traditional firewalls form a barrier around an organization's internal network.

## What is Magic Firewall? [LATER]

Magic Firewall is a network-level firewall deployed from the Cloudflare network. It is designed to replace hardware-based firewalls for on-premise networks. Hardware-based firewalls only scale up if IT buys more of them; Magic Firewall scales up more easily to handle large amounts of traffic.
