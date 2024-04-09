# Bridge Interface Management

Creating the required interfaces

```
sudo ip link add name br0 type bridge
sudo ip link add name vth1 type veth peer name vth_1
sudo ip link add name vth2 type veth peer name vth_2
```
```
ip -br -c link show type bridge
ip -br -c link show
```

Creating Namespaces for two end points

```
sudo ip netns add ns1
sudo ip netns add ns2
ip netns ls
```









In Summary
```
sudo ip link add name br0 type bridge
sudo ip link add name vth1 type veth peer name vth_1 
sudo ip link add name vth2 type veth peer name vth_2
sudo ip -br -c link show type bridge
sudo ip -br -c link show

sudo ip netns add ns1
sudo ip netns add ns2

sudo ip link set dev vth_1 netns ns1
sudo ip link set dev vth_2 netns ns2
ip -n ns1 -br -c link show
ip -n ns2 -br -c link show

sudo ip -n ns1 addr add 192.168.10.1/24 dev vth_1 <or>
sudo ip netns exec ns1 ip addr add 192.168.10.1/24 dev vth_1
sudo ip -n ns1 link set dev vth_1 up <or>
sudo ip netns exec ns1 ip link set dev vth_1 up
sudo ip -n ns1 -br -c addr show 

sudo ip -n ns2 addr add 192.168.10.2/24 dev vth_2
sudo ip -n ns2 link set dev vth_2 up
sudo ip -n ns2 -br -c addr show

sudo ip link set dev vth1 master br0
sudo ip link set dev vth2 master br0

sudo ip link set dev vth1 up
sudo ip link set dev vth2 up
sudo ip link set dev br0 up

ip netns exec ns1 ping 192.168.10.2 
ip netns exec ns2 ping 192.168.10.1
```
