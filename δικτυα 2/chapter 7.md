
**elements of a wireless network**
- **wireless hosts**
	- e.g. laptop, phone
	- run apps
- **base station**
	- connected to wired network
	- [[relay]] - send packets between wired network and wireless hosts in its area
- **wireless link**
	- connects mobile(s) to base station, backbone link
- infrastructure mode
	- base station connects mobiles into wired network, mobile changes base station providing connection into wired network
- ad hoc mode
	- no base stations, transmit only to nodes within link coverage

![[relay]]

**wireless network taxonomy**
![[Pasted image 20230917141701.png]]

**wireless link characteristics**
differences from wired link

- **decreased signal strength** radio signal attenuates as it propagates through matter (path loss)
	explanation: when a radio signal is sent, it can encounter obstacles, which it interacts with. occasionally we have “path loss”, meaning the signal strength decreases
- **interference from other sources** standardized frequencies are shared by other devices 
- **multipath propagation** radio signal reflects off objects, resulting in slight delay
- **SNR** signal to noise ratio

![[SNR versus BER tradeoffs]]

-----
**LAN architecture**
wireless host, communicates with base station
- **basic service set BSS** (aka “cell” in infrastcurcture mode) contains
	- wireless hosts
	- access point: base station
	- ad hoc mode: hosts only

![[Pasted image 20230917152050.png]]

-----
**802.11b: 2.4GHz - 2.485GHz spectrum** divided into 11 channels at different frequencies
- AP admin chooses frequency (AP = ACCES POINT)
- if channel is the same as the one chosen by neighboring AP, **interference**

host must **associate with an AP** - scans, selects, may perform authentication (will run DHCP to get IP address in AP’s subnet)

- **passive scanning** 
	- beacon frames sent
	- association request
	- association response
- **active scanning** 
	- probe request
	- probe response
	- association request
	- association response

** no collision detection without CSMA

**IEE 802.11 MAC protcol CSMA/CA**
![[Pasted image 20230917153408.png]]

**compontnts of cellular network architecture**
- **cell**
	- covers geographical region
	- **base station** analogous to 802.11 AP
	- **mobile users** attach through BS
	- **air-interface** physical and link layer protocol between mobile and BS

**mobility**
![[Pasted image 20230918122159.png]]

vocabulary
![[Pasted image 20230918122255.png]]
![[Pasted image 20230918122317.png]]

**how to contact mobile**
- **let routing handle it** advertise permanent address of mobile nodes via routing table, indicating where “target” located (VERY HARD - DOES NOT SCALE)
- **let end systems handle it** 
	- [[indirect routing]] communication from correspondent goes through home agent, then forwarded to remote
	- [[direct routing]] correspondent gets *foreign address* of mobile, sends directly

**registration**
if mobile agent is at a certain home network
- foreign agent contacts home agent “this mobile is resident in my network”
- mobile contacts foreign agent on entering visited network

![[indirect routing]]

![[direct routing]]

**mobile IP**
“packet within a packet”

![[Pasted image 20230918125956.png]]

**agent advertisement** foreign/home agents advertise service by broadcasting ICMP messages (typefield = 9)

![[Pasted image 20230918130015.png]]

