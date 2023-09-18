#δίκτυα #σεπτέμβριος #εξ8

[[chapter3exs]]

**transport services + protocols**
provide logical communication between app processes running on different hosts

run in end systems
- send side, breaks msgs into segments, passes to [[network layer]]
- rcv side, reassembles segments into messages, passes to [[app layer]]

**network layer** logical communication between hosts
**transport layer** logical communication between processes

**multiplexing + demultiplexing**
- **multiplexing at sender** handle data from multiple sockets, add transport header (later used for demultiplexing)
- **demultiplexing at reciever** use header info to deliver recieved segments to correct socket

![[Pasted image 20230904192332.png]]
host uses ip address and port numbers to direct segment into socket

when creating socket, we set a host-local port 
	DatagramSocket mySocket1 = new DatagramSocket(12345);
	
![[UDP]]

**TCP socket identified by**
- source ip address
- source port # 
- dest ip address
- dest port #

- server host may support many simultaneous TCP sockets
- web servers: different socket for each client 
	*non-persistent HTTP has different socket for each request*

for reliable transfer
- reliability at application layer
- application-specific error recovery

**checksum** detects errors (e.g. flipped bits) in transmitted segment

***sender***
- segment contents = sequence of 16bit ints
- checksum is [[addition]] (1's complement sum) of segment 
- checksum value -> field put by sender

**receiver** compute checksum, check if equal

**RDT** reliable data transfer
**FSM** finite state machines

**rdt 1.0** reliable transfer over reliable channel

![[Pasted image 20230904193452.png]]

**rdt 2.0** channel with bit errors 
*how to recover from errors?* 
- **acknowledgments (ACKS)** receiver tells sender packet received ok
- **negative acknowledgments (NACKS)** receiver tells sender packet had errors


**pipelining**
sender allows multiple, "in-flight", yet-to-be-acknowledged packets 
- go-back-N![[go-back-N]]
- selective repeat![[selective repeat]]
![[TCP]]


![[Pasted image 20230904195252.png]]

**sequence numbers** byte stream "number" of first byte in segment's data
**acknowledgments** seq # of next byte expected from other side, *cumulative ACK*

**TCP timeout value** longer than RTT, but RTT varies (value to set for the timeouts)
	**sampleRTT** measured time from segment transmission until ACK receipt, ignore retransmissions

**estimatedRTT = (1-a)\*estimatedRTT + a\*sampleRTT**
- weighted moving average 
- typically a=0.125

**timeout interval** estimated RTT plus "safety margin"

**devRTT = (1-b)\*devRTT + b\*|sampleRTT - estimatedRTT|**

**timeoutInterval = estimatedRTT + 4\*devRTT**

[[retransmissions]] triggered by
- timeout events
- [[duplicate ACKS ]]

**TCP sender events** 
- **data received from app** 
	- create segment with seg#
	- seq# is byte-stream number of first byte in segment
	- start timer = *oldest unacked segment*
- **timeout**
	- retransmit segment that caused timeout
	- restart timer
- **ack rcvd**
	- if ack acknowledges previously unacked packet, update and start timer if there are still unacked segments

![[Pasted image 20230904202657.png]]

**TCP fast retransmit** if sender receives 3 ACKS for some data ("triple duplicate ACKS"), *resend unacked segment with smallest seq#, and don't wait for timeout* (meaning, the first one that hasn't been ACKed)

![[Pasted image 20230904203819.png]]

**connection management**
*handshake* before exchanging data = agree to establish connection, agree on connection parameters

tcp 3-way handshake 
- client LISTEN > SYNSENT > ESTAB
- server LISTEN > SYNRCVD > ESTAB

![[Pasted image 20230904204603.png]]

**closing a connection**
- send TCP segment with FIN bit =1 
- respond to FIN with ACK (on rcv FIN, ACK can be combined with its own FIN)

**congestion control**
*congestion* too many sources sending too much data too fast for network to handle ([[congestion control]])

**where**
R = output link capacity
λ = data

**scenario 1**
![[Pasted image 20230904205856.png]]

**scenario 2**
*idealization - perfect knowledge*
- sender only sends when router buffers available
- sender only resends if packet is known to be lost

![[Pasted image 20230904210232.png]]

*realistic*
- sender times out prematurely, sending two copies both of which are delivered 
- happens if router's buffers are full, packets lost or dropped

![[Pasted image 20230904210551.png]]


**end to end congestion control**
- no explicit feedback from network
- congestion inferred from end to end system observed loss, delay
- used by TCP 

**network-assisted congestion control**
- routers provide feedback to end systems
- congestion indicated with a single bit

**TCP congestion control**
approach : sender increases transmission rate, probing for usable bandwidth until loss occurs

![[Pasted image 20230904211040.png]]
additive increase : increase by 1 max sgt size till loss

**for exercises, with TCP Reno:**
- slow start is the curve
- congestion avoidance is the straight line

- if the window size is cut in half, that means we have a *triple duplicate ACK*
- if the window size drops to 0, that means we have a *timeout*

**LastByteSent - LastByteAcked <= cwnd**
**rate ~= cwnd/RTT** bytes/sec

![[Pasted image 20230904211416.png]]

**reacting to loss**
loss is indicated by timeout 
- cwnd set to 1 MSS
- window then grows exponentially (slow start) to **threshold (ssthresh)**, then grows linearly
- **congestion window = ssthresh + 3 MSS**

**loss indicated by 3 duplicate ACKs : TCP RENO**
- dupACKs indicate network capable of delivering *some* segments
- cwnd is cut in half, then window grows linearly
TCP Tahoe always sets cwnd to 1 (timeout for 3 dupACKs)

![[TCP sequence number ]]

**avg. TCP throughput = 3/4 (W/RTT)**
where w window size

**fairness** for k TCP sessions that share bottleneck of bandwidth R, each should have avg. rate R/K

[[FTP]]