In a network that uses MPLS, each packet is assigned to a class called a forwarding equivalence class (FEC).
The network paths that packets can take are called label-switched paths (LSP). A packet's class (FEC) determines which path (LSP) the packet will be assigned to. Packets with the same FEC follow the same LSP.

**But whether a VPN or some other security service is used, MPLS is not secure by default.**

- **Long setup time**: Setting up complicated dedicated paths across one or more large networks takes time. LSPs have to be manually configured by the MPLS vendor or by the organization using MPLS. This makes it difficult for organizations to scale up their networks quickly.

- **Complexity**: MPLS is usually a managed service offered by Internet service providers (ISPs). Since ISPs have different coverage areas, this makes MPLS a region-specific service, and it has to be negotiated with multiple different providers for WANs that span a country or the globe.

- **Lack of encryption**: MPLS is not encrypted; any attacker that intercepts packets on MPLS paths can read them in plaintext. Encryption has to be set up separately.

- **Cloud challenges:** Organizations that rely on cloud services may not be able to set up direct network connections to their cloud servers, as they do not have access to the specific servers where their data and applications live.