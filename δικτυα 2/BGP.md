border gateway protocol

provides each AS a means to
- **eBGP** obtain subnet reachability info from neighboring ASs
- **iBGP** propagate reachability info to all AS-internal routers
- determine “good” routes to other networks based on reachability information and policy

allows subnet to advertise existence - “i am here”

**basics**
- BGP session = routers exchange messages, advertising paths - **semiu-permanent TCP connections**
- when prefix **advertised**, AS “promises” to forward datagrams toward said prefix, can aggregate prefixes in its advertisement (eBGP)
- router **sends prefix reachability info** to rest of AS (iBGP)
- when router learns of new prefix, it makes new entry for it in **forwarding table**

![[Pasted image 20230916165530.png]]

![[Pasted image 20230916165648.png]]