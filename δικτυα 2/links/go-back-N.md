a network protocol used to achieve reliable data transmission
- sender can have up to N unacked packets in pipeline
- receiver only sends **cumulative** ACK (no ACK if gap)
- sender has timer for oldest unacked packet (when timer expires RETRANSMIT ALL unacked packets)
