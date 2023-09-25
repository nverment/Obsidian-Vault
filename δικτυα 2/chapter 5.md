![[routing algorithm]]

**routing algorithm classification**

- **global** all routers with complete info (costs, topology)
- **decentralized** router knows only physically connected - “collecting info as we go”

- **static** routes change slowly
- **dynamic** routes change quickly (need updates)

**dijkstra’s algorithm** 
- need to check all nodes 
- doesn’t end if costs change dynamically OR if there are any negative costs

https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/
(if explanation needed but i passed domes)
![[Pasted image 20230916161338.png]]


**distance vector algorithm**
(following bellman-ford equation)

only knows neighbors 
	dx(y) = cost of least-cost path from x to y
	dx(y) = min{c(x,v) + dv(y)}
where
	c(x,v) = cost to neighbor v
	dv(y) = cost from neighbor v to destination y

look for shortest path towards target's **neighbors**, and then neighbors → destination
**total min** is the solution

![[Pasted image 20230916162010.png]]

upon link cost change

“good news travels fast”
- node detects local link cost change 
- **update** routing info, recalculate

“bad news travel slow” 
- “count to infinity” needs many steps to update the cost

![[poisoned reverse]]

-----
**hierarchical routing** 

![[AS]]

- intra-AS = routing protocol, **inside** one [[AS]]
- gateway router = “door” at the edge of [[AS]], links to other AS
- inter-AS routing = routing *between* [[AS]]

![[intra-AS routing]]

**hot potato routing** send packet toward the closest of two routers

![[BGP]]

**broadcast routing**
- deliver packets from source to all other nodes 
- source duplication is inefficient

 ![[Pasted image 20230916171825.png]]

- **flooding** when node receives broadcast packet sends copy to all neighbors 
- **controlled flooding** node only broadcasts packet if it *hasn’t broadcast the same packet before*
- **spanning tree** no redundant packets received by any node

![[spanning tree]]

![[multicast group]]

**reverse path forwarding - pruning**
forwarding tree contains **subtrees** with no [[multicast group]] members 
- no need to forward datagrams down structure
- “prune” messages sent upstream by router with no down stream group members

“you don’t need us so we don’t send or receive messages”

**steiner tree** minimum cost tree connecting all routers with attached group members (**NP-complete**, but excellent heuristics exists)

**tunneling** 
can’t make a spanning tree in the internet
- mcast datagram encapsulated inside “normal” (non-multicast-addressed) datagram
- normal IP datagram sent thru “tunnel” via regular IP unicast to receiving mcast router - **like IPV6, IPV4 tunneling**
- receiving router unencapsulates to get mcast datagram

![[multicast datagrams]]
