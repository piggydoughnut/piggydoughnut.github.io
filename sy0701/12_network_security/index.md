# Network security

## OSI

- 7 layers

## Infrastructure considerations

- attack surface
- device placement
- security zones
- connectivity considerations
- failure modes
- network taps

## Network Design concepts

### Physical isolation

### Logical segmentation - using software or settings to divide a computer network into smaller, more manageable segments based on logical.

- Vlan tags - When a switch or other network device handles a packet associated with a VLAN, it inserts a VLAN tag into the Ethernet frame header. This tag allows network devices to identify which VLAN the packet belongs to.

### High availability

### Implementing secure protocols

### Reputation services

### Software defined networking

### Software defined WAN (Wide Area Network)

### Secure Access Service Edge (SASE)

### Network Segmentation - physical grouping of devices

- a broadcast domain is a group of devices that can receive and send broadcast messages.

- Screened subnets - often called DMZs (Demilitarized Zones), network zones that contain systems that are exposed to less trusted areas.
- Intrantes
- Extranets

### Zero trust

- Control Plane - the rules that define how the network is configured and managed.
  - Adaptive Identity
  - Threat Scope Reduction - limiting the scope of what the subject can access, relies on least privilege as well as identity based network segmentation.
  - Policy driven access control - policy engines rely on policies to make decisions, that are then enforced by the Policy Administrator and Policy Enforcement Point.
  - The Policy Administrator
- Data Plane
  - Implicit Trust Zones - allow use and movement once a subject is authenticated by a Zero Trust Policy Engine.
  - Subjects and systems - which are the devices and users seeking access to the network.
  - Policy Enforcement Point - the point where the policy is enforced.

### Network Access Control

- 802.1x - IEEE standard for network access control, standard for authentication and authorization. Uses centralized authentication using EAP 802.1X

### Post Security and Port Level Protection

**Port security** - a feature that limits the number of devices (MAC addresses) that can be connected to a port. Prevents MAC address spoofing, content addressable memory (CAM) table overflows, plugging in additional devices to extend the network.

**Dynamically lock the port** - setting a maximum number of MAC addresses that can be connected to a port.
**Statically lock the port** - to allow only specific MAC addresses.

**Loop prevention** - focuses on preventing loops in a network, disabling ports that are part of a loop.

**Broadcast storm prevention** - prevents broadcast packets from being amplified as they traverse a network, relies on loop protection on ports, enabling STP (Spanning Tree Protocol) on switches to prevent loops, rate limiting broadcast traffic.

**Bridge Protocol Data Unit (BPDU) Guard** protects STP by preventing ports that should not send BDPU messages from sending them.

**DHCP - Dynamic Host Configuration Protocol snooping** - focuses on preventing rogue DHCP servers from handing out IP addresses to devices on the network. Snooping drops a message from any unknown DHCP server.

## Virtual Private Networks and Remote Access
