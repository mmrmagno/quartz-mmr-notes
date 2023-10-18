
# Hauptsitz (Baar) 
## R1 
```
interface GigabitEthernet0/0
 ip nat inside
exit

interface GigabitEthernet0/0.10
 ip nat inside
 ip access-group VLAN10 in
exit

interface GigabitEthernet0/0.20
 ip nat inside
 ip access-group VLAN20 in
exit

interface GigabitEthernet0/0.30
 ip nat inside
 ip access-group VLAN30 in
exit

interface GigabitEthernet0/0.99
 ip nat inside
 ip access-group VLAN99 in
exit

interface GigabitEthernet0/1
 ip nat outside
exit

ip nat inside source list 100 interface GigabitEthernet0/1 overload

ip nat inside source static tcp 192.168.20.1 80 20.0.0.2 80 
ip nat inside source static udp 192.168.20.2 1645 20.0.0.2 1645

access-list 100 permit ip 192.168.0.0 0.0.255.255 any

ip access-list extended VLAN10
deny ip 192.168.10.0 0.0.0.255 192.168.99.0 0.0.0.255
permit tcp 192.168.10.0 0.0.0.255 host 192.168.20.1 eq 80
permit udp 192.168.10.0 0.0.0.255 host 192.168.20.2 eq 1645
deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
permit ip 192.168.10.0 0.0.0.255 any

ip access-list extended VLAN20 
deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
deny ip 192.168.20.0 0.0.0.255 192.168.30.0 0.0.0.255
deny ip 192.168.20.0 0.0.0.255 192.168.99.0 0.0.0.255
permit ip 192.168.20.0 0.0.0.255 any

ip access-list extended VLAN30
deny ip 192.168.30.0 0.0.0.255 192.168.99.0 0.0.0.255
permit tcp 192.168.30.0 0.0.0.255 host 192.168.20.1 eq 80
permit udp 192.168.30.0 0.0.0.255 host 192.168.20.2 eq 1645
deny ip 192.168.30.0 0.0.0.255 192.168.20.0 0.0.0.255
permit ip 192.168.30.0 0.0.0.255 any

ip access-list extended VLAN99
permit ip any any

snmp-server community funlight2023 RO
```

Username: admin Password: Admin12345 Radius-Secret: iajfioajsijwiqejifewiojiewjrioj3248798dj823eu83jf

![[Pasted image 20231018165807.png]]

## S1

```
interface FastEthernet0/1
 switchport trunk native vlan 99
 switchport mode trunk
exit

interface FastEthernet0/2
 switchport trunk native vlan 99
 switchport mode trunk
exit

interface FastEthernet0/4
 switchport trunk native vlan 99
 switchport mode trunk
exit

snmp-server community funlight2023 RO
```

## S2

```
interface FastEthernet0/1
 no switchport access vlan 10
 switchport trunk native vlan 99
 switchport mode trunk
exit

snmp-server community funlight2023 RO
```

## S3 

```
interface FastEthernet0/2
 no switchport access vlan 10
 switchport trunk native vlan 99
 switchport mode trunk
exit

snmp-server community funlight2023 RO
```

## Standort Emmensee 

```
interface GigabitEthernet0/0
 ip nat outside
exit

interface GigabitEthernet0/1
 ip nat inside
exit 

interface GigabitEthernet0/1.40
 ip nat inside
exit

ip nat inside source list 100 interface GigabitEthernet0/0 overload
access-list 100 permit ip 192.168.40.0 0.0.255.255 any
```

# Standort Vevey 

```
interface GigabitEthernet0/0
 ip nat outside
exit

interface GigabitEthernet0/1
 ip nat inside
exit 

interface GigabitEthernet0/1.50
 ip nat inside
exit

ip nat inside source list 100 interface GigabitEthernet0/0 overload
```