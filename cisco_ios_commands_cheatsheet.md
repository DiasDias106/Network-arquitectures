# Cisco IOS Commands Cheat Sheet

Commands used throughout the Packet Tracer labs in this repository.

## Basic device configuration

```
enable
configure terminal
hostname R_CORE                     ! set the device name
no ip domain-lookup                 ! stop IOS from trying to resolve mistyped commands via DNS
service password-encryption         ! encrypt plain-text passwords in the config (type 7)
enable secret <password>            ! privileged EXEC password (MD5 hashed)
username ADMIN password <password>  ! local user for console/VTY login
```

### Console and remote (VTY) access with a local user

```
line console 0
 login local
 logging synchronous                ! keep log messages from breaking the command you are typing
exit
line vty 0 15
 login local
exit
```

### Message of the day banner

```
banner motd &
==========================================
Device: Core Router | CISCO2911
Company: XYZNet
!RESTRICTED ACCESS!
==========================================
&
```

## Router interfaces

```
interface g0/1
 ip address 172.16.3.254 255.255.252.0
 description g0/1_DEP1_net
 no shutdown
exit
interface g0/2
 ip address 172.16.5.254 255.255.254.0
 description g0/2_DEP2_net
 no shutdown
exit
```

## Switch management interface (SVI)

```
hostname SW_DEP1
interface vlan 1
 ip address 172.16.3.253 255.255.252.0
 description vlan1_mgmt_SW_DEP1
 no shutdown
exit
ip default-gateway 172.16.3.254
```

## VLANs

### Create VLANs and assign access ports (switch)

```
vlan 10
 name NET10
vlan 20
 name NET20
vlan 30
 name NET30
vlan 40
 name NET40
exit
interface range f0/1-6
 switchport access vlan 10
interface range f0/7-12
 switchport access vlan 20
interface range f0/13-18
 switchport access vlan 30
interface range f0/19-24
 switchport access vlan 40
exit
interface range g0/1-2
 switchport mode trunk
exit
```

### Inter-VLAN routing: router-on-a-stick (router)

```
interface g0/0
 no shutdown
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.254 255.255.255.0
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.254 255.255.255.0
! ...repeat for the remaining VLANs
```

### Inter-VLAN routing: multilayer switch with routed ports

```
interface range f0/1-4
 no switchport
interface f0/1
 ip address 192.168.5.254 255.255.254.0
```

## DHCP server on the router (one pool per VLAN)

```
ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp pool NET10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.254
exit
! ...repeat for NET20, NET30, NET40
```

## EtherChannel

### PAgP (`desirable`)

```
interface range f0/21-22
 shutdown
 channel-group 1 mode desirable
 no shutdown
interface port-channel 1
 switchport mode trunk
```

### LACP (`active`)

```
interface range g0/1-2
 shutdown
 channel-group 2 mode active
 no shutdown
interface port-channel 2
 switchport mode trunk
```

## Spanning Tree

```
spanning-tree vlan 1 root primary
```
