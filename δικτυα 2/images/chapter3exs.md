**P45**. Recall the macroscopic description of TCP throughput. In the period of time from when the connection’s rate varies from W/(2 · RTT) to W/RTT, only one packet is lost (at the very end of the period). 

a. Show that the loss rate (fraction of packets lost) is equal to

![[Pasted image 20230905184141.png]]

b. Use the result above to show that if a connection has loss rate L, then its average rate is approximately given by

![[Pasted image 20230905184235.png]]

**Solution**
a. The loss rate, L , is the ratio of the number of packets lost over the number of packets sent. In a cycle, 1 packet is lost. The number of packets sent in a cycle is
![[Pasted image 20230905184421.png]]
b.
![[Pasted image 20230905184443.png]]



**P40.** Consider Figure 3.58. Assuming TCP Reno is the protocol experiencing the behavior shown above, answer the following questions. In all cases, you should provide a short discussion justifying your answer.
a. Identify the intervals of time when TCP slow start is operating. 
b. Identify the intervals of time when TCP congestion avoidance is operating. 
c. After the 16th transmission round, is segment loss detected by a triple duplicate ACK or by a timeout? 
d. After the 22nd transmission round, is segment loss detected by a triple duplicate ACK or by a timeout? 
e. What is the initial value of ssthresh at the first transmission round? 
f. What is the value of ssthresh at the 18th transmission round? 
g. What is the value of ssthresh at the 24th transmission round? 
h. During what transmission round is the 70th segment sent? 
i. Assuming a packet loss is detected after the 26th round by the receipt of a triple duplicate ACK, what will be the values of the congestion window size and of ssthresh?
![[Pasted image 20230905185307.png]]


**a)** TCP slowstart is operating in the intervals (1,6) and (23,26)

**b)** TCP congestion advoidance is operating in the intervals (6,16) and (17,22) 

**c)** After the 16th transmission round, packet loss is recognized by a triple duplicate ACK. If there was a timeout, the congestion window size would have dropped to 1. 

**d)** After the 22nd transmission round, segment loss is detected due to timeout, and hence the congestion window size is set to 1. 

**e)** The threshold is initially 32, since it is at this window size that slowtart stops and congestion avoidance begins. 

**f)** The threshold is set to half the value of the congestion window when packet loss is detected. When loss is detected during transmission round 16, the congestion windows size is 42. Hence the threshold is 21 during the 18th transmission round. 

**g)** The threshold is set to half the value of the congestion window when packet loss is detected. When loss is detected during transmission round 16, the congestion windows size is 42. Hence the threshold is 21 during the 18th transmission round. 

**h)** During the 1st transmission round, packet 1 is sent; packet 2-3 are sent in the 2nd transmission round; packets 4-7 are sent in the 3rd transmission round; packets 8- 15 are sent in the 4th transmission round; packets15-31 are sent in the 5th transmission round; packets 32-63 are sent in the 6th transmission round; packets 64 – 96 are sent in the 7th transmission round. Thus packet 70 is sent in the 7th transmission round. 

**i)** The congestion window and threshold will be set to half the current value of the congestion window (8) when the loss occurred. Thus the new values of the threshold and window will be 4.