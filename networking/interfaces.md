# `iproute2` Basics

### Output IP and Data Link Configurations 

`ip address show`
or
`ip addr`
or
`ip a`

`ip link show`
or
`ip link`
or
`ip l`

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
```

## Setting Default/Static Route

On iproute2
```
ip route add default via 192.168.1.1 dev wlan0
ip route del default via 192.168.1.1 dev wlan0

ip route add 172.16.0.0/16 via 192.168.1.1 dev wlan0
ip route del 172.16.0.0/16
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

## Checking if a interface is up or down

```
ip link
ip link show
ip link eth0
```

## Setting a new custom(virtual) interface(tun,tap)


# Bridging

```
sudo apt install bridge-utils
sudo brctl addbr br0
sudo brctl addif br0 ens33
```
sudo nano /etc/network/interfaces 
```
auto lo
iface lo inet loopback

auto br0
iface br0 inet static
  bridge_ports    ens33
  address  192.168.7.124
  netmask  255.255.255.0
  gateway  192.168.7.1
```








