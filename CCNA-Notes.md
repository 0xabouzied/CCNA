# CCNA

#### made by Abouzied

## S1, 2: Basic Router Configuration.

```jsx
CCNA & MCSA

logical address = ip address
physical addresss = physical ports

Router 2911
switch 2960

--------------
Modes:
- User EXEC mode. "enable" enters privileged EXEC mode.
- "conf t" enters global configuration mode.

Router configuration:
	1. Change the name with: hostname new_name.
	2. Set an enable password with: enable password new_password.
	Or use: enable secret new_passwd (to encrypt the password).
	
	3. To set a console password, enter: "line console 0"
		=> "password new_passwd"
		=> "login"
	4. To save the configuration (in privileged mode), use #WR or #copy run start. Use #show Run to view the previous settings.

------
# port = gateway = interface = ip address
  The first IP address is named the gateway, for example, 192.168.1.1.

	1- interface g0/0
	2- ip address 192.168.1.1 255.255.255.0
	3- no shutdown
```

## S4: DHCP server.

```jsx
CCNA 4:-

# Any device (host) needs:
	- an IP address.
	- a subnet mask.
	- Options: DNS and a default gateway.

# you can add those:
	- static: manual.	
(or)    - Dynamic: DHCP server (Dynamic host Configuration Protocol). 
	  DHCP: give every host these 4 things.

# How does a device communicate with DHCP? (DORA messages):
	Client: 'Discover'
	DHCP: 'Offer'
	Client: 'Request'
	DHCP: 'Acknowledge'

# making DHCP server:-
	- Give the server an IP address.
	- Set the default gateway.
	- Turn on the DHCP service.
	- put the Default gateway.
	- Set the DNS server to "8.8.8.8".
	- Set the starting IP address.

$ Servers must use static IP addresses.

# to make DHCP in router:-
	# ip dhcp excluded-address 192.168.1.1 192.168.1.50
	# ip dhcp pool L
	# network 192.168.1.0 255.255.255.0
	# default-router 192.168.1.1
	# dns-server 8.8.8.8
	# show ip dhcp pool

# APIPA (Automatic Private IP Addressing):
 	- Works when DHCP fails.
	- Range (private IP): 169.254.x.x
	- Works locally only.
	- This address is configured on the host itself.
```

## S5: Static & Default Routing.

```jsx
CCNA 5:-

# Routing:
	- Static Routing.
	- Default Route.
	- Dynamic Route: RIP , OSPF.

# "show ip route": (to show the router table)
	C: directly connected.
	L: local IP address for the gateway.
	S: static route.
	S*: default route.

$ A router connects different networks.

$ If you connect two routers, assign addresses from the same network (192.168.2.x) to the two ports (exit interfaces).

$ Static routing: If you connect two routers, add the IP address of the other router's port in this command (Ip route 192.168.3.0 255.255.255.0 g0/1).

$ Default route: IP route 0.0.0.0 0.0.0.0 <exit interface> (g0/0).
```

## S6: FLSM Subniting.

```jsx
CCNA 6:
IP addressing:

1.unicast: one => one.

2.Broadcast: one device => all devices.

3.multicast: one device => many devices.

# IPv4 structure:
	- consists of 4 octet (octet = byte) 
          (byte = 8 bits).
	
	- DDN (Dotted Decimal notation): this is the name of the system that we use to make ip v4.

# IPv4 classes:
	- class A: 1 -> 126
	- class B: 128 -> 192
	- class C: 192 -> 223
	- class D: 224 -> 239
	- class E: 240 -> 255
	$ 127.0.0.1 : Reserved (loop back test).

# Subnet masks:
	- Class A: 255.0.0.0 (or prefix length /8).
	- Class B: 255.255.0.0 (or prefix length /16).
	- Class C: 255.255.255.0 (or prefix length /24).
	- Class D: routing.
	- Class E: research.

# Subnetting:
	- FLSM (Fixed-Length Subnet Masking):
		- The same subnet mask is used for every network.
		- Each network has the same number of hosts.
		
	- VLSM (Variable-Length Subnet Masking).

------------------

CIA:-
	- Confidentiality.
	- Integrity.
	- Availability.

DAD:
	- Disclosure: unauthorized access.
	- Alteration: unauthorized modification.
	- Destruction: loss of data or systems.
```

## S6: Solving.

```jsx
128 64 32 16 8 4 2 1

128: 10000000

192: 11000000

224: 11100000

240: 11110000

248: 11111000

252: 11111100

254: 11111110

255: 11111111

-----------------------------------
FLSM:

192.168.1.0 (4 networks):

 4 = 2^2  , 192.168.1.1100 0000 /26
 
 H = 2^6 - 2 = 62  , Hop count= 2^6 = 64

 1st net: 192.168.1.0 /26

 2nd net: 192.168.1.64 /26

 3rd net: 192.168.1.128 /26

 4th net: 192.168.1.192 /26

-------------------

192.168.10.0 (2 networks):

2=2^1 , 192.168.10.1000 0000  

255.255.255.128  = /25

h = 2^7 - 2 = 126, total address count = 128

1st net: 192.168.10.0 (net)
	 192.168.10.1:126
	 192.168.10.127 (broadcast)

2nd net: 192.168.10.128 (net)
	 192.168.10.129:254
	 192.168.10.255 (broadcast)
```

## S7: VLSM subnetting.

```jsx
CCNA 7

VLSM:
	- Every network has its own subnet mask.
	- The number of hosts varies.

How to do it:
	- Start with the largest number of hosts.

-------------------------------
192.168.1.0

1st: 
	100 hosts 
	H = 2^7-2 = 126
	255.255.255.1000 0000
	255.255.255.128 /25
	ntw -> 192.168.1.0
	fip -> 192.168.1.1
	lip -> 192.168.1.126
	broadcast -> 192.168.1.127

2nd:
	50 hosts
	H = 2^6-2 = 62
	255.255.255.1100 0000 
	255.255.255.192 /26
	ntw -> 192.168.1.128
	fip -> 192.168.1.129
	lip -> 192.168.1.190
	broadcast -> 192.168.1.191

3rd:
	30 hosts
	H = 2^5-2 =30
	255.255.255.1110 0000
	255.255.255.224 /27
	ntw -> 192.168.1.192
	fip -> 192.168.1.193
	lip -> 192.168.1.222
	broadcast -> 192.168.1.223

4th:
	5 hosts
	H = 2^3-2 = 6
	255.255.255.1111 1000
	255.255.255.248 /29
	ntw -> 192.168.1.224
	fip -> 192.168.1.225
	lip -> 192.168.1.230
	broadcast -> 192.168.1.232

Youssef abouzied 7_1
-------------------------------
192.168.10.0

1st:
	120 hosts
	H = 2^7-2 = 126
	255.255.255.1000 0000
	255.255.255.128 /25
	
	ntw -> 192.168.1.0
	fip -> 192.168.1.1
	lip -> 192.168.1.126
	broadcast -> 192.168.1.127

2nd:
	25 hosts
	H = 2^5-2 = 30
	255.255.255.1110 0000
	255.255.255.224 /27
	
	ntw -> 192.168.1.128
	fip -> 192.168.1.129
	lip -> 192.168.1.158
	broadcast -> 192.168.1.159

3rd:
	2 hosts
	H = 2^2-2 = 2
	255.255.255.1111 1100
	255.255.255.252 /30

	ntw -> 192.168.1.160
	fip -> 192.168.1.161
	lip -> 192.168.1.162
	broadcast -> 192.168.1.163

Youssef abouzied 7_2
------------------------------------------
205.5.5.0 /24

8 = 2^3
255.255.255.1110 0000
255.255.255.224 /27
h = 2^5-2 = 30, total address count = 32

1st:
	net -> 205.5.5.0
	fip -> 205.5.5.1
	lip -> 205.5.5.30
	broadcast -> 205.5.5.31

2nd:
	net -> 205.5.5.32
	fip -> 205.5.5.33
	lip -> 205.5.5.62
	broadcast -> 205.5.5.63

3rd:
	net -> 205.5.5.64
	fip -> 205.5.5.65
	lip -> 205.5.5.94
	broadcast -> 205.5.5.95

4th:
	net -> 205.5.5.96
	fip -> 205.5.5.97
	lip -> 205.5.5.126
	broadcast -> 205.5.5.127

5th:
	net -> 205.5.5.128
	fip -> 205.5.5.129
	lip -> 205.5.5.158
	broadcast -> 205.5.5.159

Youssef abouzied 7_4
```

## S8: RIP protocol & Router Components.

```jsx
CCNA 8:-

# CIDR (Classless Inter-Domain Routing):
	 This is the prefix format for a subnet mask. For example, 255.255.254.0 is /23.

# What is the difference between classless and classful addressing?
	- Classful addressing uses default subnet masks (Class A /8, Class B /16, Class C /28).
	 
	- Classless addressing uses CIDR prefixes such as /25 and /26. We can create subnets using FLSM or VLSM.

# Router components:
	- CPU.
	- Power Supply.
	- Memories:  ROM  , RAM  , NVRAM  , Flash.
	- Interfaces (ports).

$ Memories:
	- ROM: contains BIOS/startup code that performs POST (a self-test to make sure all components are present).

	- RAM: volatile memory (running configuration file).
	
	- NVRAM: non-volatile memory (startup configuration file).

$ When you save the configuration, you copy it from RAM to NVRAM with this command (copy run start).
	
	- Flash memory: stores IOS (the operating system). Use show flash to see the files; IOS images often end in ".bin".

---------------------------------

```

```jsx
Routing:

1. Static:
	- Static (S).
	- Default (S*).
	- Directly connected (C) (next hop, exit interface).

2. Dynamic:
	- Distance vector (RIP v1, IGRP: not used).
	- Link state (OSPF).
	- Hybrid (EIGRP, RIP v2).

$ direct connected: when using 1 router and 2 devices.

=> RIP (Routing Information Protocol (R)):

$ The default in RIP is v1.
$ It is an open standard.

$ For example, consider three routers:
R1:
	# router rip
	# version 2
	# network 192.168.1.0

	# network 192.168.2.0
R2:
	# router rip
	# version 2
	# network 192.168.2.0
	# network 192.168.3.0
	# network 192.168.4.0

R3:
	# router rip
	# version 2
	# network 192.168.4.0
	# network 192.168.5.0

# show Ip route

=> RIP:
	- v1.
	- v2.

	- v3: for ipv6

1. A router with a hop count greater than 15 is unreachable (v1 and v2).
2. distance vector.
3. classful.
4. Sends routing-table updates by broadcast. 
5. metric = hop count = cost -> best path.
```

## S11: Access Control List (ACL).

```jsx
# ACL (Access Control List): We configure it on a router to act like a firewall.

# Firewall -> packet filtering.

# The firewall is placed between the LAN and WAN:
	LAN (Trusted) -- Firewall -- WAN (un-trusted).
	
	firewall -- DMZ (the website is placed in this area so normal users can access the LAN).
	

# Security levels: LAN: 100, DMZ: 50, WAN: 0.

# ACL:
	1 -> Action: -deny   - permit.
	2 -> location.
	3 -> Direction.

# Types of ACLs:
	-> Standard: number (1-99) or named.
	-> Extended: number (100-199) or named.

	- Standard: depends on the source.
	- Extended: depends on both the source and destination.

# To make an access list (standard -> number):
$ Apply it to the interface nearest to the destination.

Configurations:-
$ Apply them on the router nearest to the destination because this is a standard ACL.
  
	# access-list 1 deny 192.168.1.2 (action)
	# access-list 1 permit 192.168.1.0 0.0.0.255(wildcard mask)
	# interface G0/1 (location: the nearest from destination)
	# Ip access-group 1 out(direction)
	
# show Ip access-list
```

## S12: OSPF Protocol.

```jsx
#Routing :

 1.Static 
	- static (S).
	- default (s*).
	- direct connected (c). (next hope , exit interface).

 2.Dynamic 
	- distance vector (Rip v1 , IGRP: not used).
	- link state (OSPF).
	- Hybrid (EIGRP , RIP v2).

```

```jsx
#AD (Administrative Distance):
	- RIP: 120.
	- OSPF: 110.
	- EIGRP: 90.
 $ The lowest value is preferred. If one router learns routes through two protocols, it uses the route with the lower AD.

# Metric = cost.

- RIP has a maximum hop count of 15, so it is suitable for small networks.
- So OSPF was developed. 

```

```jsx
# OSPF (Open Shortest Path First):
	1. It is an open standard.
	2. Unlimited hop count.
	3. Requires more processing power and RAM.
	4. AD = 110.
	5. Metric = cost = 10^8/BW (the cost helps select the path).
	6. Sends a hello message every 10 seconds.

$ If the other router does not respond to four hello messages, the router declares the neighbor down after the dead interval.
  
$ Area 0 is called the backbone area or transit area.

# OSPF configuration:
	# Router ospf 1
	# Network 192.68.1.0 0.0.0.255 area 0.
	# Network 192.168.2.0 0.0.0.255 area 0.

$ You must connect all other areas to area 0. Use a router to connect them..

$ ABR (Area Border Router): used to connect two areas.
$ Routers inside other areas are called internal routers, while routers inside area 0 are called backbone routers.
$ An area has a maximum of 50 routers.

# For a multi-area configuration:
	On the ABR, configure the interface connected to area 0 in area 0, and configure the other interfaces in their respective areas.
```

## S13: OSPF.

```jsx
# Cables:
	- Serial: 		1,544 Mbps
	- Ethernet: 		10 Mbps
	- Fast Ethernet: 	100 Mbps
	- Gigabit Ethernet: 	1000 Mbps
	- 10 Gigabit Ethernet:	10,000 Mbps
```

```jsx
OSPF authentication types:
	- Null: T0
	- Simple password: T1
	- MD5: T2

Configuration:
	# int g0/0
	# ip ospf authentication
	# ip ospf authenticaion-key 123

# multicast :-
	OSPF: 224.0.0.5
	RIP: 224.0.0.9
	EIGRP: 224.0.0.10

# LSDB: Link State Database (contains many LSAs).
  LSA: Link State Advertisement (information about a link).
  LSR: Link State Request.
  LSU: Link State Update.
  LSAck: acknowledges messages.

# If a router does not have information about another router:
	Router 1: LSR
	Router 2: LSU
	Router 1: LSAck
```

```jsx
OSPF phases:

	1. Neighbor discovery:
		- Same area.
		- Same authentication.
		- Same timer (same hello interval).
		- Same subnet.
	
	2. Database exchange:
		- Routers exchange LSAs with each other to build the LSDB.

	3. Draw the tree.

	4. Make the routing table based on the lowest metric.

------------

OSPF topology:
	1. Neighbor Table:
		# show ip ospf neighbor.
	
	2. OSPF database:
		# show ip ospf database.
	
	3. OSPF Table:
		# show ip route ospf.

$ OSPF make Load Balancing if there are 2 ways (maxmum:4) 
  have the same metric (equal load balancing).
```

```jsx
OSPF passive interface:
 Use passive interfaces on ports that are not connected to routers. Otherwise, the router sends hello messages to end devices.

configuration: 
	# router ospf 1
	# net....
	# passive-inter g0/0
	# show ip ospf interface g0/0
```

## S14: NAT (public & private IPs).

```jsx
# Routing: 
	- connect different networks.
	- find the best path to the destination.

#Routing protocols and routed protocols:

 1. Routing protocols:
	- Find the best path.
	- Examples: OSPF, RIP, etc.

 2. Routed protocols:
	- IP.

# RIP v1 sends updates by broadcast (255.255.255.255).

# Routers:
	- Prefer the lowest AD.
	- Prefer the lowest metric (cost), because the lowest metric indicates the best path.

# AS (Autonomous System):
	- It is a fixed number for every company; it helps organize devices.

# Some configuration commands:

 #erase startup-config (this command deletes the configuration file).
 #show flash.
 # delete flash   => file name
```

```jsx
Private and public IP addresses:

	# Private IP:
		These are the IP addresses we use in the configuration.

	# Public IP:
		We need these to communicate with another
	  	network.

$ NAT is used on a router to convert a private IP address to a public IP address.

# NAT:
	1. Static NAT.
	2. Dynamic.
	3. PAT (Port Address Translation).

# Static NAT:
	- Every private IP is mapped to a public IP.
	
	- config:
			#int g0/1 
			#ip nat inside
			#ex
			#int g0/0
			#ip nat outside
			#ex
		
			#ip nat inside source static 10.0.0.2
			 50.0.0.1 (mapping).
			#=======  10.0.0.3 50.0.0.2
			# show ip nat translations
	

# Dynamic NAT:
	- Many-to-many.
	- Maps many private IP addresses (devices) to many public IP addresses.

```

## S15: NAT (Dynamic & PAT).

```jsx
NAT:-
	1. Static.
	2. Dynamic.
	3. PAT.

2. Dynamic:
	- Many-to-many.
	- Uses a pool.

 configuration:
	# ip nat pool nti 50.0.0.5 50.0.0.30 netmask 	 	 255.0.0.0
	# ip nat inside source list 1 pool nti
	# access-list 1 permit 10.0.0.0 0.0.0.255
	
	

3. PAT (Port Address Translation):
	- Uses one public IP address for all private IP addresses.
	- Many-to-one.
	- The router uses ports (logical ports) to distinguish between private IP addresses in the NAT table.
	- The router uses ports starting from 49152.

 configuration:
	# int g0/0
	# ip nat inside
	# ip g0/1
	# ip nat outside

	# ip nat inside source list 1 interface g0/0 
	  overload
	# access-list 1 permit 10.0.0.0 0.0.0.255
```

## S16: Port Security & IPv6.

```jsx
Port security:
	Prevents someone from unplugging a computer and connecting their laptop to the switch port.

switch mode:
	Access: used when a switch port connects to PCs only.

Switch configuration:
	# interface g0/1  (or) interface range f0/1-4 .
	# switchport mode access.
	# switchport port-security.
	# switchport port-security mac-address sticky.
	# show port-security.

	# switchport port-security violation <violation type>.

There are three violation modes:
	1. shutdown (default):
		 the port is put into error-disabled mode.
		 If you change the PC, the port remains disabled even after reconnecting the original cable.
		#shutdown => #no shutdown. (to open port).
	
	2. restrict:
		when you reconnect the PC, the switch sends a notification.
	
	3. protect:
		Similar to restrict, but without a notification.
```

```jsx
IPv4:
	- Consists of 4 octets and 32 bits.
	- DDN.
	- Uses decimal notation.
	- 2^32 IP addresses.

IPv6:
	- Consists of 8 groups separated by colons.
	- Each group is 16 bits, for a total of 128 bits.
	- Uses the hexadecimal system.
	- 2^128 IP addresses.
	
- configuration: 
	#ipv6 unicast-routing
	# int g0/0
	# ipv6 add 2001::1/64
	# no shutdown

- Static route:
	#ipv6 route 2002::/64 2000::2(or)g0/1

Leading-zero compression:
	2001:0000:0000:01cd:0000:0000:0000:102a /64

    =>  2001:0:0:1cd:0:0:0:102a/64
    =>  2001:0:0:1cd::102a/64
```

## S18: IPv6 & Redundancy (FHRP) & STP.

```jsx
DHCP:
	When a device sends DORA messages:
		-SRC IP: 0.0.0.0
		-DEST IP : 255.255.255.255
		-SRC MAC: -----
		-DEST MAC: FF:FF:FF:FF:FF:FF

IPv6:
	1. Global unicast address (public IPv4).

	2. Link-local address (APIPA in IPv4):
		169.254.0.0/16

	3. Unique-local address (private IP).
	
	4. Loopback address:
		::1
	
	5. Multicast:
		(RIPv2) FF02::9 (224.0.0.9 in IPv4).
		(EIGRP) FF02::A (224.0.0.10 in IPv4).
		(OSPF) FF02::5||6 (224.0.0.5||6).

```

```jsx
FHRP (First Hop Redundancy Protocol):
	- Types:
		1. HSRP.     2.VRRP.      3.GLBP.

1. HSRP (Hot Standby Router Protocol):
	- From Cisco.

	- This protocol provides redundancy by allowing another router to act as a backup. 
	
	- We use 2 routers: one is active and the other is passive (standby).
	
	# Put the two routers and the devices on the same network (192.168.1.x).
	  Then set the default gateway to the IP of the active router.

	- The active router sends a hello message every 3 seconds. After 3 missed messages, the standby router becomes active after a total of 10 seconds (hold time).

	- If the active router fails, the standby router becomes active.
 
	- If the former active router works again, it will become active if I enter the last two configuration commands.

  - Active Router Configuration:
		# interface G0/0.
		# Standby 5 Ip 192.168.1.100 (virtual IP).
		# Standby 5 priority 200 (default 100).
		# Standby 5 preempt.
	
  - Standby Router Configuration:
		# standby 5 Ip 192.168.1.100
	
		# show Standby
	
	- This type uses a virtual IP (1.100) and a chosen group number (5).
	  Set the active router's priority above 100. The last command allows the former active router to become active again.

2. VRRP (Virtual Routing Redundancy Protocol):
	- Open standard.
	- Hello interval: 1 second.
	- Hold time: 3 seconds.

3. GLBP (Gateway Load Balancing Protocol):
	- From Cisco.
	- Supports a maximum of 4 routers.
	- Provides load balancing.

---------------------------------

	              		(FHRP)

 HSRP			           VRRP		        	    GLBP

.cisco.			      .open Standard.		    .cisco
.hello=3 sec.	    .hello=1 sec.		      .4 gateways
.hold=10 sec.	    .hold=3 sec.

```

```jsx
Number of cables = number_of_switches - 1 (no redundancy).

When you add redundancy (3 switches -> 3 cables):
	- Loops.
	- Broadcast storms.
	- MAC address table instability.

	# To solve these problems, use the STP (Spanning Tree Protocol).
	# STP blocks one cable to avoid these problems.
	# STP works by default.

	- Number of blocked points = (number of cables - number of switches) + 1.
	
	
- STP Algorithm:
	-> One Root bridge per network:
		The root switch has the lowest priority.
		If priorities are the same, the switch with the lowest MAC address is selected.

	-> One root port per non-root bridge:
		The root port is the port with the best path to the root bridge.

	-> One designated Port per segment.
		These are the active ports on the root bridge.

	-> Blocked Port:
		Choose the switch with the lowest priority.
		If priorities are equal, choose the one with the lowest MAC address.

- Election:
	1. Elect the root bridge.
	2. Elect the root port.
	3. Elect the Designated ports.
	4. Block the remaining ports.

- config:
	# show Spanning-tree.

```

## S20: Syslog, NTP, Neighbor Discovery Protocols, and PortFast.

```jsx
Syslog:
	- Every configuration change has a log.
	
	- port: 514 UDP.
	
	- Works at the application layer.
	
	- It records every change or action on routers and switches.
	
	- Storing log messages:
		1.Console.	2.Buffer(RAM).
	
	   1. To stop messages from appearing on the console:
		# no logging console
	
	   2. To store logs in the buffer:
		# logging buffered.
		
	   3.Syslog server:
		- In a real network, you need to install Kiwi on a server to use it as a syslog server.
		- Enable syslog on the server.
		- Then enter this command on the routers:
		   #logging <server Ip>
	
	- Logs appear only on the console, not in remote sessions such as Telnet or SSH.
	
	- Log message severity levels:
		0 => Emergency.
		1 => Alert.
		2 => Critical.
		3 => error.
		4 => Warning.
		5 => Notifications.
		6 => Information.
		7 => Debug.
	
	- To add sequence numbers to logs:	
		#Service sequence numbers.
	
	- To filter logs by severity:
		#logging trap <the highest severity (<5)>.

NTP:
	- A server for the date and time.
	
	- Use it with Syslog to add a date and time to every log.
	
	- Router configuration:
		#service time stamp log date time msec.
```

```jsx
Neighbor discovery protocols:

CDP (Cisco Discovery Protocol):

	- Discovers basic information about neighboring routers and switches.

	- Works only on Cisco devices.

	- Sends a message every 60 seconds, 3 times.
	
	- Basic information:
		- host name.
		- IP.
		- MAC.
		- Interfaces.
		- Capabilities list (connect with router/switch).

	- conf:
		# show CDP
		# show CDP neighbors

	- It works by default. To disable it:
		# no CDP run

LLDP (Link Layer Discovery Protocol):
	- Open source.
	- Not enabled by default.
	- Sends a message every 30 seconds, 4 times.
	- conf:	
		# show lldp
		# run lldp
```

```jsx
PortFast:
	- After a switch is connected to devices, the ports are in the blocking state for 30 seconds (15 seconds listening + 15 seconds learning). 
	
	- To avoid the 30-second delay, use PortFast.
	
	- configuration:
		# interface range f0/1-4
		# switchport mode access
		# spanning-tree portfast

Network characteristics:
	1. Availability.
	2. Cost.
	3. Security.
	4. Speed.
	5. performance.
	6. Reliability.
	7. Scalability (for example, having 30 places for 20 PCs).

#int f0/1
#spanning-tree bpduguard enaple
```

## S21: Ether channel Protocols & DHCP Attacks.

```jsx
Ether channel Protocols:-

	- make load balancing.
	- Group multiple interfaces to one logical interface.
	- it makes four ways as a one way to make load
	  balance.

	- port Aggregation = channel group = port channel
	  = Ether channel.

Protocols:
	1. LACP:
		- IEEE 802.3.ad
		- open standard.
		- support 16 link.

	2. PAGP:
		- Cisco.
		- support 8 links.
		- we have to switches desirable & auto.
		- 1st router 		2st router
		    Active		  Active
		    Passive		  Passive

		- Trunk: means the cables can connect all
		  VLANS.
		- in security i have to make both routers 
		  trunks.
		  

Config:
	# interface range f0/1-4
	# switchport mode trunk
	# channel-group 1 mode desirable
	# show EtherChannel 
```

```jsx
DHCP Attacks:

	1.DHCP snooping:
		- to protect network from hacker, because 
		  hacker can make his lab like a DHCP and 
		  make man in the middle attack.
	
		-conf:
			# ip dhcp snooping
			# ip dhcp snooping vlan 1
			# interface f0/5
			# ip dhcp snoofing trust
	

	2.DHCP Starvation:

```

## S23: VLANs.

```jsx
VLAN (virtual LANs):

	- every VLAN is a local network but other VLANs are use router.

	- There are a default VLAN 1 for all interfaces.

	- VLAN IDs between 0:4096 but we can't use 0 & 4096.

	- Every switch has two types of ports:
		1.Access port: connect to devices , UnTagged.
		2.Trunk port: connect between two switches or switch 
								  to router , Tagged.

- VLAN Tagging: switch adds tag on the frame before sending 
		it , this tag has some info like VLAN ID.
		
		1. IEEE 802.1Q
		2. ISP (not used).
```

```jsx
Inter-vlan-Routing:
	- each vlan needs physical interface as a default gateway in the router.

	-Types:
		1. legacy: 
			-to make a physical port for every VLAN.
			- Configuration:
				$in switch
				#vlan 10
				#name HR
				#exit
	
				#interface fa0/1 (or) interface 
				 Range f0/1-3 
				#switchport mode access
				#switchport access vlan 10
				
				$in router
				#just give IPs for every physical port.

		2. ROAS: one physical port to work as a multiple 
			 logical interface.
			 - Conf: (in router)
				#int g0/0
				#no shutdown
				#int g0/0.10
				#encapsulation  dot1Q 10
				#ip address 192.168.1.100 255.255.255.0

				#int f0/5  (to make trunk)
				#switch port mode trunk
		
		
		3. MLS:
			-SVI (Switched virtual interface):
			- we use multilayer switch (3500).
			-conf:
				$ work as ROAS after that.
				#ip routing (to work as a router)
				# int vlan 10
				#ip address ....
```

## S24: VTP protcol.

```jsx
Inter-Vlan-Routing:
	1-Traditional inter-vlan Routing:
		- every vlan has a physical port from routing.
	
	2- ROAS:
		- we use one physical interface put we make it alot of 
		  virtual interfaces (ports) on it.

	3- Multi layer switch:
		- it works as a router & a switch.
		- 
```

```jsx
VTP (Vlan Trunking protocol):
	- we use it to create vlans on switches automatically.
	- cisco devices only.
	- It's like Active directory and Domain controller.
	- it gives vlans for other switches.
	
	- conf switch:
		#vtp domain HOSPITAL
		#vtp mode server (or) vtp mode client
		#vtp password ccna123
		#vtp version 2
```

## S25: Interview questions.

```jsx
CCNA 25

Client ---> server   (centralized Admin)

Device --> switch --> device	(un centralized Admin).

---------------------

Network component:
	1. Hardware:
		- End devices.  -media

	2. Software:

---------------------
Intranet: in LAN

Extranet: in DMZ

Internet: in WAN

------------------
Network characteristics:
	1. Availability.
	2. Cost.
	3. Security.
	4. Speed.
	5. performance.
	6. Reliability.
	7. Scalability (for example, having 30 places for 20 PCs).

--------------------
CIA:-
	- Confidentiality.
	- Integrity.
	- Availability.

---------------------
Aim of a network:
	- sharing of resources.
	- modern technologies.

---------------------
Router modes:
	- user mode.
	- privileged.
	- Global configuration.

--------------------
Assign ip address:
	- static.
	- dynamic.

--------------------
one --> one (unicast).

one --> all (Broadcast).

one --> many (multicast).

--------------------------
7 layer:
	- app
	
	- presentation
	
	- session

	- transportation

----------------------
Benefits of using layer:
	-

----------------------
PDU (Protocol Data Unit):

---------------------
Logical address = IP --> in network layer
physical address = mac --> data link layer

---------------------
pc ---- sw ---- Router --- Router --- sw --- server

- from pc to server ip is stable but mac changes.

IP : end --> end  (stable in way). 
MAC: hop --> hop  (change in way).

-----------------------------------
Function of physical layer:
	1. Bit transmission:
		-send , receives
	2. connectors.
	3. transmission mode:
		-simplex.   -half duplex.   -full duplex.

-------------------------------
Data link layer:
	1. Hop - to - Hop  (Delivery).

	2. packet -> to frame (encapsulation and but make on frame).

	2. Error detection.

----------------------------	
Network layer:
	1. Addressing.	
	
	2. Encapsulation. 
	
	3. Routing.
	
	4. De-encapsulation.

----------------------------
IP properties:
	1. connection less.
	
	2. Best effort.

---------------------
IPv4 , IPv6

------------------
Transport layer.
	- segmentation.
	- TCP: 
		1.connection-oriented.  2.Reliability.  3.order d..
		4.ACK.
	
	- UDP:
		1.connectionless.  2.Best effort. 

----------------------
Port numbers: 65535

----------------------
Socket = IP + Port

---------------------
3-way handshake 

Syn ->
Syn ack <-
Ack ->

4-Way handshake 
Session termination

fin ->
Ack <-
fin <-
Ack ->
```
