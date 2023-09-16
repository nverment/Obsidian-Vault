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

