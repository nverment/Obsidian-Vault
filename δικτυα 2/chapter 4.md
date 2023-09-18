**network layer**
application, transport

![[network layer]] 

**forwarding** move packets from router's input to appropriate router output
*"going through an interchange"*

**routing** determine route taken by packets from source to destination ([[routing algorithm]])
*"planning the trip"*

![[routing algorithm]] 

![[forwarding table]]

in some architectures, "virtual segway" 
- network: between two hosts (computers)
- transport: between two processes (apps)

![[datagram]]

![[virtual circuit]]

like TCP/UDP, but
- service: host to host
- no choice: network provides one or the other
- implementation: in network core

**datagram networks**
no call setup at network layer, no state about end to end connections

*use destination host address for forwarding - so if we wanna send to host 3, thru 1,2,3 we put in:*
![[Pasted image 20230905191833.png]]
*we use RANGE instead of list of individual IP addresses*

![[Pasted image 20230905192153.png]]

**longest prefix matching**
when looking for forwarding table entry for given address, use [[longest prefix]] that matches destination address.

**internet (datagram)** simple inside network, complexity at edge
**ATM (VC)** complexity inside network

**router architecture**
- forwarding datagrams (in > out - hardware)
- run routing algorithms (calc in to out route - software) (*forwarding tables*)

![[Pasted image 20230905193255.png]]

**decentralized switching**
- given datagram destination, look up output port using forwarding table in input port memory
- queuing if datagrams arrive faster than fwd rate into [switch fabric]

![[switch fabric]]

**memory**
- packet copied to system's memory, stays in memory till sent
- speed limited by 2 bus crossings

**bus** (up to 32Gbps)
- datagram from input port memory to output port memory via shared bus 
- bus contention = switching speed limited by bandwidth

**interconnection network-crowbar** overcome bus limitations (up to 60Gbps)

**output ports**
*buffering* required when datagrams arrive from fabric faster than transmission rate
*scheduling discipline* chooses among queued for transmission

![[Pasted image 20230905201128.png]]

**queuing delay (and loss) due to output port buffer overflow (not INPUT)**
 
average buffering equal to “typical” RTT times link capacity / sqrt(N)
![[Pasted image 20230916141105.png]]
N parallel flows

**network layer**
host, router network layer functions:

ICMP protocol
- error reporting
- router signaling

IP protocol
- address conventions
- datagram format
- packet handling conventions

![[Pasted image 20230916141332.png]]

**IP fragmentation**
- MTU = max transfer size - largest possible link level frame
- large IP datagrams divided (“fragmented”) within net
	- one datagram into multiple, reassembly at dest. using IP header bits
	- *overhead MULTIPLIES*

**offset = num. important bytes / 8**
where **important bytes = total bytes - overhead**
# subnets

**IP address** subnet part = high order bits, host part = low order bits

subnet = device interfaces with the same subnet part of IP address (first part) - can physically reach each other without *router*

![[CIDR]]

![[how do we get IP address ]]

---
DHCP overview
- host broadcast (DHCP discover)
- server responds with (DHCP offer)
- host requests IP address (DHCP request)
- server sends (DHCP ack)
---
ICANN Internet Corporation for Assigned Names and Numbers
- allocates addresses
- manages DNS 
- assigns domain names, resolves disputes - it’s how ISP’S get a block of addresses

[[telnet]]

**local - home network**
datagram with source or destination in local network have 10.0.0/24 address for source, destination - but all datagrams leaving local network have the same SINGLE SOURCE **NAT IP address**

**NAT network address translation**
local network uses just **one IP** as far as outside world is concerned
- one address for all devices
- change local addresses w/o notifying outside world
- local devices not explicitly addresses

NAT router must
- replace source IP, port with **NAT IP, port for outgoing**
- remember translated pairs
- replace NAT source IP, port with **source IP, port for incoming**

** NAT has a 60.000 connections limit with a single LAN address

**port forwarding** configure NAT to forward incoming connection requests at given port to server (one specific device)

-----
ICMP messages (not for exam just for later use)
![[Pasted image 20230916152220.png]]

--------
**traceroute and ICMP**
- source sends series of UDP segments to dest.
- when nth set of datagrams arrives to nth router, datagrams discarded
- router sends source ICMP messages including name of router + IP 
- when ICMP messages arrive, source records RTTs

traceroute is a tool to figure out the path a packet takes, and how long it takes it to reach the destination

traceroute command
- first set TTL=1, second TTL=2, … when n’th set arrices to n’th router 
- router discards datagrams, sends ICMP messages
- ICMP messages make name of router and IP address
---------
stopping criteria 
- UDP segment arrives at destination
- destination host returns “port unreachable” ICMP message
- source stops
-----
**IPV6**
32- bit addresses “ran out”

![[Pasted image 20230916154817.png]]

**datagram format** 
- fixed length to 40 byte header
- no fragmentation allowed

flow = “σύνδεση”

not all routers can be upgraded at the same time, so 
**tunneling** IPV6 datagram carried as **payload (data)** in IPV4 datagram among IPV4 routers
