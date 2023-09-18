“data link layer”

**terminology**
- hosts and routers are **nodes**
- communication channels that connect nodes are **links**
- layer-2 packet is a **frame**, encapsulates datagram (datagrams “closed” in frame)

![[data-link layer]]

** each node “trip” can use different protocols

**link layer services**:

**framing, link access** 
- encapsulate datagram by adding *header* and *trailer*
- “MAC” addresses used in frame headers to id source, dest (NOT IP addresses)

![[MAC address]]

**reliable delivery between adjacent nodes** 
- wireless links have high error rates
- seldom used on low - bit error rate (chapter 3…)

more…
- flow control
- error detection
- error correction
- half-duplex and full-duplex = whether both ends of link can transmit at the same time

![[Pasted image 20230916183828.png]]

**error detection**
EDC = error detection and correction bits
D = data protected by error checking, may include header fields

![[Pasted image 20230916184447.png]]
“like checksum”

**parity bits**
odd number of bits - 1
even number of bits - 0

**how does it work?** count number of bits, check with parity bit - detect error, NOT correction - can only find errors when there is **odd number of errors**.

**two-dimensinal parity**
parity bits created for columns and rows
![[Pasted image 20230916192837.png]]

**checksum**
addition of all bits - error detection, not correction

**cyclic redundancy check**
to starting bits, add n bits to the **end of packets** so that sum is divided by G (mod=0) where G = number that sender and receiver know
![[Pasted image 20230916193054.png]]
**2^r** shift left by r bits
**XOR R** add the R bits to the end

-----
two types of links 
- **point - to - point** PPP -e.g. ethernet switch and host (direct connection between devices)
- **broadcast** shared wire or medium between multiple devices, e.g. ethernet network, has protocol for sending data (like ARP or DHCP)

![[MAC protocols]]


**CDMA code division multiple access**
- assign unique “code” alter data (encoding) and decode on arrival

**random access protocols**
when node has packet to send, transmit at **full channel** data rate R 
collision - handled by protocols
- ALOHA
- CSMA

----- 
![[slotted ALOHA]]

![[pure - unslotted aloha]]

**CSMA carrier sense multiple access**
- “dpn’t interrupt others”
- nodes “listen” and wait random time then check again

due to propagation delay, collision may still occur - node doesn’t “listen” to other’s transmission

**wired LANs** measure signal “strength”, detect collision

![[Pasted image 20230916222105.png]]

**ARP table** IP/MAC address mappings for some LAN nodes
- A wants to send packet towards B
- A broadcasts ARP query packet, containing B’s IP address
- B receives ARP packet, replies to A with B’s MAC address 
- A caches IP-to-MAC till info is sold - timed out

“plug and play” nodes create ARP tables without intervention from net adminstrator

**routing to another LAN**
send datagram A → B via R, assume A knows B’s IP
- create datagram
- ARP to find MAC address 
- frame (verb) and send to R
- receive frame, remove IP datagram from ethernet frame, sees it’s destined to B
- ARP to get B’s MAC
- create frame containing A-to-B datagram, send

----- 
**ethernet**
dominant wired LAN technology
- uses [[CSMA-CD]]

**frame structure** sender encapsulates IP datagram (or other network layer procotol packet) in ethernet frame
![[Pasted image 20230916222956.png]]

- **preamble** 10101… (7 bytes), lets receiver know packet is on the way
- **dest/source address** (self explanatory)
- **type** indicates protocol, type of data
- **data** (sent data)
- **CRC** for error checking

** connectionless, unreliable service (no handshakes, ACKs, error detection)

**collision detection**
- produces much higher signal voltage than signal, gets detected
- needs max allowed window size
can take as long as 2t 
	t = time of collision (from send)

**CSMA/CD efficiency**
**tprop** = max propagation between 2 nodes in LAN
**ttrans** = time to transmit max size frame
![[Pasted image 20230916223504.png]]

tprop → 0
efficiency → 1

**10BaseT and 100BaseT**
*used for describing data transfer speed*
10/100 = max supposed transmission rate - “fast ethernet”
T = “twisted pair”

nodes connected in “star topology”
![[Pasted image 20230916223834.png]]

-----
**hubs**
physical - layer repeaters 
- m bits coming from **one link to all other links**, at the same rate
- **no CSMA/CD** at the hub, adapters detect collisions
![[Pasted image 20230917133747.png]]

**interconnecting with hubs**
- extends max distance between nodes
- BUT individual segment collision domains become one large collision domain
- can’t interconnect 10BaseT and 100BaseT
![[Pasted image 20230917134216.png]]
-----
**switch**
- [[data-link layer]] device - does NOT separate broadcast domains → cannot make more domains
- stores and forwards ethernet frames **selectively**, based on MAC dest address
- “transparent” - hosts unaware of switches
- plug n play, self learning

![[Pasted image 20230917134420.png]]

**forwarding**
if a switch wants to send a frame
- if dest. switch not on the known table, frame is sent to all interfaces
- data on table updated
- if dest. switch on the known table, frame is instantly sent to correct interface
- *each subnet of LAN segments become separate collision domains*

- routers - routing tables, routing algorithms
- switches - switch tables, **filtering, learning algorithms**
