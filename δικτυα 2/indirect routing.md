communication from correspondent goes through home agent, then forwarded to remote

- mobile uses *two* addresses
	- **permanent address** used by correspondent (hence mobile location is transparent to correspondent)
	- **care-of-address** used by home agent to forward datagrams to mobile
- foreign agent functions may be done to mobile itself
- **triangle routing** correspondent - home network - mobile (inefficient when correspondent are in the same network)

**if mobile user moves to another network** 
- registers with new foreign agent
- foreign agent registers with home agent
- home agent update care-of-address for mobile
- packets still forwarded to mobile, with *new care-of-address*

![[Pasted image 20230918122821.png]]