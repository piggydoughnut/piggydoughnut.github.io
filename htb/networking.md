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

## Networking topologies

Physical or logical connection of devices in a network. Include network components such as switches, bridges and routers.

### Connections

Wired connections: Coaxial cabling, glass fiber cabling, twisted pair cabling
Wireless connections: Wi-Fi, Cellular, Satelite

### Nodes - Network Interface Controller (NICs)

Network nodes are the transmission medium's connection points to transmitters and receivers of electrical, optical, or radio signals in the medium.

Repeaters
Hubs
Bridges
Switches
Router/Modem
Gateways
Firewalls

### Classifications

We can imagine a topology as a virtual form or structure of a network. This form does not necessarily correspond to the actual physical arrangement of the devices in the network. Therefore these topologies can be either physical or logical. For example, the computers on a LAN may be arranged in a circle in a bedroom, but it is very unlikely to have an actual ring topology.

#### Point-to-Point

Connection between two hosts - physical link. Point-to-poin are the beasic model of traditional telephony and must not be confused with Peer-to-Peer architecture.

![point to point](./networking/topo_p2p.png "Point to Point")

#### Bus

All hosts are connected via a tramission medium in the bus topology. Every host has access to the transmission medium and the signals that are transmitted over it. Transmission medium can be a e.g. coaxial cable.

Since the medium is shared with all the others, only one host can send, and all the others can only receive and evaluate the data and see whether it is intended for itself.

![bus](./networking/topo_bus.png "Bus")

#### Star

Each host is connected to the central network component via a separate link. This is usually a router, hub or a switch. These handle forwarding function for the data packets.

![star](./networking/topo_star.png "Star")

#### Ring

The physical ring topology is such that each host or node is connected to the ring with two cables:

- one for the incoming signals
- one for the outgoing signals

The ring topology does not require and active network component. The control and access to the transmission medium are regulated by a protocol to which all stations adhere.

The informations is transmitted in a predetermined transmission direction. Typically, the transmissin medium is accessed sequentially from station to station using a retrieval system from the central station or a token.

A token is a bit pattern that continually passes through a ring network in one direction, which works according to the claim token process.

![ring](./networking/topo_ring.png "Ring")

#### Mesh

Many nodes decided about the connections on a physical level and the routing on a logical level in meshed networks. No fixed topology.

![Mesh](./networking/topo_mesh.png "Mesh")

**Fully meshed**

Each host is connected to every other host in the network in a fully meshed structure. Hosts are meshed with each other. Used in WAN or MAn to ensure high reliability and bandwitdth.

Routers can be networked together in case of one failure others can continue working.

Each node has the same routing functions and knows the neighbouring nodes it can communicate with proximity to the network gateway and traffic loads.

**Partially meshed**

The edpoints are connected by only one connection. Specific nodes are connected to exactly one other node, and some other nodes are connected to two or more other nodes with point-to-point connection.

![FullPartMesh](./networking/fullVSpart.png "FullPartMesh")

#### Tree

Used in larger company buildings, extended start topology.

There are both logical and physical tree structures. Modular modern networks, based on structured cabling with a hub hierarchy, also have a tree structure.

Tree topologies are also used for broadband networks and city networks (MAN).

![Tree](./networking/topo_tree.png "Tree")

#### Hybrid

Combine two or more topologies that the resulting network does not present any standard topologies.

E.g. tree network can represent a hybrid topology in which star networks are connected via interconnected bus networks.

A tree network linked to another tree network is still topologically a tree network.

A hybrid topology is always created when two different basic network topologies are interconnected.

![Hybrid](./networking/topo_hybrid.png "Hybrid")

#### Daisy Chain

Multiple hosts are connected by placing a cable from one node to another. This creates a chain of connections, multiple hardware components are connected in a series.

Often used for automation technology - CAN.

Daisy chaining is based on a physical arrangements of nodes, in contrast to token procedures, which are structural but can be made independent of the physical layout. The signal is sent to and from a component via its previous nodes to the computer system.

![Daisy](./networking/topo_daisy-chain.png "Daisy")
