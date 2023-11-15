# Networking

- an FQDN, Fully Qualified Domain Name (www.hackthebox.eu) only specifies the address of the "building" and
- an URL (https://www.hackthebox.eu/example?floor=2&office=dev&employee=17) also specifies the "floor," "office," "mailbox" and the corresponding "employee" for whom the package is intended.

## Network types

**Wide Area Network (WAN)**

- The Internet
- a large number of LANs joined together
- Company Internal WAN - Intranet, Airgap Network, etc.
- To identify if the network is a WAN is to use a WAN specific routing protocal such as BGP and if the IP Schema in use is not within RFC 1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16).

**Local Area Network (LAN) and Wireless Local Area Network (WLAN)**

- LAN - Internal Networks (e.g Home or Office)
- WLAN - Internal Networks accessible over WiFi
- Will typically assign IP addresses designated for local use (RFC 1918, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16)
- In some cases, like some colleges or hotels, you may be assigned a routable (internet) IP Address from joining their LAN, but that is much less common.
- There's nothing different between a LAN or WLAN, other than WLAN's introduce the ability to transmit data without cables. It is mainly a security designation.

**Virtual Private Networks (VPN)**

- Connects multiple network sites to one LAN
- The goal is to make the user feel as if they were plugged into a different network.

Site-To-Site VPN

- both client and server are Network Devices, typically routers or firewalls, and share entire network ranges. Most commonly used to join company networks together over the internet, allowing multiple locations to communicated over the Internet as if they were local.

Remote Access VPN

- Client's computer creates a virtual interface that behaves as if it is on a client's network
- When analyzing these VPNs, an important piece to consider is the routing table that is created when joining the VPN. If the VPN only creates routes for specific networks (ex: 10.10.10.0/24), this is called a Split-Tunnel VPN, meaning the Internet connection is not going out of the VPN. For a company, split-tunnel VPN's are typically not ideal because if the machine is infected with malware, network-based detection methods will most likely not work as that traffic goes out the Internet.

SSL VPN

- This is a VPN that is done within our web browser and is becoming increasingly common as web browsers are becoming capable of doing anything.
- Typically these will stream applications or entire desktop sessions to your web browser. A great example of this would be the HackTheBox Pwnbox.

**Global Area Network (GAN)**

- Global network, internet
- GANs use the glass fibers infrastructure of wide-area networks and interconnect them by international undersea cables or satellite transmission.

**Metropolitan Area Network (MAN)**

- Regional network (multiple LANs)
- MAN is a broadband telecommunications network that connects several LANs in geographical proximity. As a rule, these are individual branches of a company connected to a MAN via leased lines.
- The transmission speed between two remote nodes is comparable to communication within a LAN.
- Internationally operating network operators provide the infrastructure for MANs. Cities wired as Metropolitan Area Networks can be integrated supra-regionally in Wide Area Networks (WAN) and internationally in Global Area Networks (GAN).

**Wireless Personal Area Network (WPAN)**

- Modern end devices such as smartphones, tablets, laptops, or desktop computers can be connected ad hoc to form a network to enable data exchange. This can be done by cable in the form of a Personal Area Network (PAN).
- based on Bluetooth or Wireless USB technologies
- A wireless personal area network that is established via Bluetooth is called Piconet
- PANs and WPANs usually extend only a few meters and are therefore not suitable for connecting devices in separate rooms or even buildings.
- In the context of the Internet of Things (IoT), WPANs are used to communicate control and monitor applications with low data rates. Protocols such as Insteon, Z-Wave, and ZigBee were explicitly designed for smart homes and home automation.
