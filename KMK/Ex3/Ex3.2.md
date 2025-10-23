```shell
# Admin network/pc should be w/ a static ip

# ROUTER
enable
conf t
host Plovdiv
int fa0/0
no ip add
no shut
exit
int fa0/0.10
encapsulation dot1Q 10
ip add 192.168.10.1 255.255.255.0
no shut
exit
int fa0/0.20
encapsulation dot1Q 20
ip add 192.168.20.1 255.255.255.0
no shut
exit
do show ip int br
ip dhcp pool pool_10
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.10.1
domain-name test.com
exit
ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp pool pool_20
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 192.168.20.1
domain-name test.com
exit
ip dhcp excluded-address 192.168.20.1 192.168.20.10
do wr
do show running-config

# SWITCH
enable
conf t
host S_Plovdiv
vlan 10
name Hr
exit
vlan 20
name Sales
exit
int fa0/1
switchport mode access
switchport access vlan 10
no shut
exit
int fa0/2
switchport mode access
switchport access vlan 10
no shut
exit
int fa0/3
switchport mode access
switchport access vlan 20
no shut
exit
int fa0/4
switchport mode access
switchport access vlan 20
no shut
exit
int gigabitEthernet 0/1
switchport mode trunk
no shut
do wr
exit
do show vlan


# Ex3.2
# ROUTER

enable
conf t
int fa0/1
no ip add
no shut
exit
int fa0/1.30
encapsulation dot1Q 30
ip add 192.168.30.1 255.255.255.0
no shut
exit
ip dhcp pool pool_30
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
dns-server 192.168.30.1
domain-name test.com
exit
ip dhcp excluded-address 192.168.30.1 192.168.30.20
int fa0/1.40
encapsulation dot1Q 40
ip add 192.168.40.1 255.255.255.0
no shut
exit

do wr
do show running-config

# SWITCH
enable
conf t
host S_Plovdiv_2
vlan 30 
name Acc
exit
vlan 40
name Admin
exit
int fa0/1
switchport mode access
switchport access vlan 30
no shut
exit
int fa0/2
switchport mode access
switchport access vlan 30
no shut
exit
int fa0/3
switchport mode access
switchport access vlan 40
no shut
exit
int gigabitEthernet 0/1
switchport mode trunk
no shut
do wr
exit

```
