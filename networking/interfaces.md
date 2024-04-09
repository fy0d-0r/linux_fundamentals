# `iproute2` Basics

### Output IP and Data Link Configurations 
```
ip address show
ip addr show lo
ip addr
ip a
```

```
ip link show
ip link show lo
ip link
ip l
```

### Setting MTU
```
ip link set lo mtu 70000
```

### Brief and Colored Output
```
ip -br -c link show
ip -br -c l

ip -br -c address show
ip -br -c addr
ip -br -c a
```

### In Oneline
```
ip --oneline a
ip -o a | column -t 
ip -o -4 a | awk '{print $4}'
ip -o -4 a | awk '{print $4}' | cut -d/ -f1
```

### Output in JSON Format
```
ip -j a
ip -j -p a //with prettify
```

## Renaming a network interface

```
ip link set <current_interface_name> down
ip link set <current_interface_name> name <new_interface_name>
ip link set <current_interface_name> up
```


## Setting IP address and Subnet

```
ifconfig wlan0 192.168.1.2 netmask 255.255.255.0
```

```
ip addr add 192.168.100.32/24 dev wlan0
```

## Chaning IP address

```
sudo ip addr del <old_ip_address>/<subnet_mask> dev <interface_name>
sudo ip addr add <new_ip_address>/<subnet_mask> dev <interface_name>
```

### Show Routing Table 
```
ip route
ip -c r | column -t
ip route get 8.8.8.8
```

## Setting Default/Static Route

On iproute2
```
ip route add default via 192.168.1.1 dev wlan0
ip route del default via 192.168.1.1 dev wlan0

ip route add 172.16.0.0/16 via 192.168.1.1 dev wlan0
ip route del 172.16.0.0/16
```

```
ip route change default via 10.0.0.1 dev eth0
ip route change 172.16.0.0/16 via 10.0.0.1 dev eth0
```

On route
```
route add default gw 192.168.1.1 eth0
route del default gw 192.168.1.1 eth0
```

## Setting the interface up and down

```
sudo ip link set <interface_name> up
sudo ip link set <interface_name> down
```

### Adding Interface 

```
ip link add test0 type dummy
```

### Detail and Satistic Output
```
ip -d addr show eth0
ip -d link show eth0
```
```
ip -s addr show eth0
ip -s addr show eth0
```

### ip tunnel

```
ip tunnel show
ip tunnel add tn0 mode gre local 192.168.1.1 remote 203.0.113.10
ip tunnel del tn0
```

### ip neighbour 
The same as `arp` utility
```
ip n
```
### Manage TCP Metrics
```
ip tcpmetrics show
```

### Watch for Netlink Messages 
```
ip monitor
ip -4 monitor neigh
```

### Multicast Address
```
ip maddress show lo
ip mroute show
```

### Manage Neighbour Cache
```
ip ntable 
```

## Setting a new custom(virtual) interface(tun,tap)


# Bridging

```
sudo apt install bridge-utils
```

### Adding Bridge Interface
Creating a Bridge Intreface
```
ip link add name br0 type bridge
```

Creating Virtual Interface Pairs
```
ip link add name vth1 type veth peer vth_1
ip link add name vth2 type veth peer vth_2
```

```
ip netns ls
```





