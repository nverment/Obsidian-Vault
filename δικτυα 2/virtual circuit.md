virtual circuit network provides a network-layer **connection** service.

like a "telephone circuit"
- call setup, tear down for each call before data can flow
- each packet with VC identifier (**only** relates to where packet goes)
- router maintains "state" for each connection

VC has
1. path from source to destination
2. VC numbers, one for each link along the path
3. entries in forwarding tables in routers along path

** the VC number can be changed on each link