- **point-to-point** one sender, one receiver
- **reliable, in-order byte stream** no msg boundaries
- **pipelined** TCP congestion and flow control set window size
- **full duplex data** bidirectional dataflow, [[MSS]] 
- **connection-oriented** handshaking inits sender, receiver state before data exchange
- **flow controlled** sender will not overwhelm receiver


**TCP flow control**
- **flow control** receiver controls sender, so sender won't overflow receiver's buffer by transmitting too much too fast
- **rwnd value** included in TCP header, it's "free buffer space" - data to receiver's rwnd value is limited, guaranteeing the receive buffer will not overflow
