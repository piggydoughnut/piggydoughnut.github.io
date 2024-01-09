# Network Mapping

```
nmap --help

<SNIP>
SCAN TECHNIQUES:
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
  -sU: UDP Scan
  -sN/sF/sX: TCP Null, FIN, and Xmas scans
  --scanflags <flags>: Customize TCP scan flags
  -sI <zombie host[:probeport]>: Idle scan
  -sY/sZ: SCTP INIT/COOKIE-ECHO scans
  -sO: IP protocol scan
  -b <FTP relay host>: FTP bounce scan
<SNIP>
```

`TCP-SYN` is the default setting, scans serveral thousand ports per second. The `TCP-SYN` scan sends one packet with the SYN flag and, therefore, never completes the three-way handshake, which results in not establishing a full TCP connection to the scanned port.

If our target sends an `SYN-ACK` flagged packet back to the scanned port, Nmap detects that the port is open.

If the packet receives an `RST` flag, it is an indicator that the port is closed.

If Nmap does not receive a packet back, it will display it as filtered. Depending on the firewall configuration, certain packets may be dropped or ignored by the firewall.

## Host Discovery

- get an overview of which systems are online that we can work with
- **ICMP echo requests** - the most effecting nmap option to find out if our taget is alive or not

`nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5`

### Scan IP List

- Nmap also gives us the option of working with lists and reading the hosts from this list instead of manually defining or typing them in.

`nmap -sn -oA tnet -iL hosts.lst`

Some hosts may ignore the default **ICMP echo requests** becaude of their firewall configurations. Since `nmap` does not receive a response it marks those hosts as inactive.

### Scan multiple IPs

`nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20`

scan a range

`nmap -sn -oA tnet 10.129.2.18-20`

### Scan single IP

`nmap 10.129.2.18 -sn -oA {host} `

If we disable port scan (-sn), Nmap automatically ping scan with ICMP Echo Requests (-PE). Once such a request is sent, we usually expect an ICMP reply if the pinging host is alive.

The more interesting fact is that our previous scans did not do that because before Nmap could send an ICMP echo request, it would send an ARP ping resulting in an ARP reply.
