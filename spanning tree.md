- construct spanning tree
- nodes forward - make copies only along tree
![[Pasted image 20230916172229.png]]

**creation**
1. center node
2. each node sends **join message** to center node - forwarded till it arrives at node already belonging to spanning tree
 ![[Pasted image 20230916172346.png]]

**goal** is to find a tree or trees connecting routers having local mcast group members
- **tree** not all paths used
- **shared tree** same tree used by all group members
- **source-based** different tree form each sender to receivers

