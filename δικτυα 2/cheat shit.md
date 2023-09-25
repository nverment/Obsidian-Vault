cheat sheet for exercises

- how to find **network id**? 
	- take IP as is, see the /x and set the x last bits to 0 - where x last bits are the **host bits**
- **bridges** provide greater scalability for ethernet rather than hubs
- to find amount of **hosts** supported, we do **2^(ID bits) -2** (because we can’t use the “all 0’s” and “all 1’s” addresses) 
- to split a network into **n networks/subnets** we try to find an x where **2^x** ≥ n, then we “borrow” n bits for said networks by setting the last n bits of the mask to 0 (instead of 1).
- 127.0.0.1 is **home network**
- **ARP** requests are sent to FF-FF-FF-FF-FF-FF
- switches *do not make more broadcast domains*
- **bridges and switches** are layer 2 (data link) devices
- **route aggregation** reduces the size of the routing table
- **ARP** address to physical address 
- **layer 3 addresses** are IPs in “numbers” form


things i’m not sure about 

- in **hubs**, there is 1 collision domain and i n **switches** the collision domains are equal to the ports











![[Pasted image 20230918182731.png]]

