# Lab: Basic Device Configuration

## Objective
Configure basic device settings for a router, switch, and PC.

## Topology
- Router (R1): Gig2/0 connected to Switch Gig0/0 port with IP 192.168.1.1/24
- Switch (SW1): VLAN1 with management IP 192.168.1.2 /24.
- PC (PC1): ether 0  Connected to Switch Gig0/1.

## Configurations
### Router (R1)
```
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#hostname R1
R1(config)#no ip domain-lookup
R1(config)#line console 0
R1(config-line)#logging synchronous
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#line vty 0 4
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#service password-encryption
R1(config)#banner motd # Authorized Access only! #
R1(config)#int g2/0
R1(config-if)#ip add 192.168.1.1 255.255.255.0
R1(config-if)#no sh
R1(config-if)#
*Feb  9 20:14:34.259: %LINK-3-UPDOWN: Interface GigabitEthernet2/0, changed state to up
*Feb  9 20:14:35.259: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet2/0, changed state to up
R1(config-if)#ex

```
## Configurations ##
### SWITCH (SW1)
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW1
SW1(config)#no ip domain-lookup
SW1(config)#line console 0
SW1(config-line)#logging synchronous
SW1(config-line)#password cisco
SW1(config-line)#login
SW1(config-line)#line vty 0 4
SW1(config-line)#password cisco
SW1(config-line)#login
SW1(config-line)#exit
SW1(config)#service password-encryption
SW1(config)#banner motd # Authorised Users Allowed Only!!! #
SW1(config)#interface vlan 1
SW1(config-if)#ip a
*Feb  9 20:19:16.001: %LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to down
SW1(config-if)#ip add 192.168.1.2 255.255.255.0
SW1(config-if)#no sh
SW1(config-if)#exit
*Feb  9 20:19:39.297: %LINK-3-UPDOWN: Interface Vlan1, changed state to up
*Feb  9 20:19:40.297: %LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up
SW1(config-if)#exit

## Configuration ##
### VPC
``
PC1> 
PC1> ip 192.168.1.3 255.255.255.0 
Checking for duplicate address...
PC1 : 192.168.1.3 255.255.255.0

## Verification
###### Ping Results :
  > From PC to Router: Success
`` 
PC1> ping 192.168.1.1

84 bytes from 192.168.1.1 icmp_seq=1 ttl=255 time=39.277 ms
84 bytes from 192.168.1.1 icmp_seq=2 ttl=255 time=7.509 ms
84 bytes from 192.168.1.1 icmp_seq=3 ttl=255 time=6.557 ms
84 bytes from 192.168.1.1 icmp_seq=4 ttl=255 time=7.010 ms
84 bytes from 192.168.1.1 icmp_seq=5 ttl=255 time=6.392 ms

> From PC to Switch: Success
PC1> ping 192.168.1.2

84 bytes from 192.168.1.2 icmp_seq=1 ttl=255 time=2.870 ms
84 bytes from 192.168.1.2 icmp_seq=2 ttl=255 time=1.801 ms
84 bytes from 192.168.1.2 icmp_seq=3 ttl=255 time=1.520 ms
84 bytes from 192.168.1.2 icmp_seq=4 ttl=255 time=1.565 ms
84 bytes from 192.168.1.2 icmp_seq=5 ttl=255 time=1.768 ms
