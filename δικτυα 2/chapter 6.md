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

