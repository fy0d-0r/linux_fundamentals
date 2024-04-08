## Uncomplicated Firewall

### Status and Enabling
```
sudo ufw status
sudo ufw enable
```


### Default Policy
```
sudo ufw default allow outgoing
sudo ufw default deny incoming
```
### Rules at Layer 4 Level

```
sudo ufw allow port/protocol
sudo ufw deny port/protocol
```

```
sudo ufw allow 22/tcp
```

```
sudo ufw allow ssh
sudo ufw allow 20 //the same as ssh

sudo ufw allow http
sudo ufw allow 80
```
### For a Range of Ports 

```
sudo ufw allow/deny starting_port:ending_port/protocol
```
```
sudo ufw deny 300:310/UDP
```

### Denying or Allowing IP Address Connections

```
sudo ufw allow/deny from ipaddress
```
```
sudo ufw allow from 192.168.100.28
```

```
sudo ufw allow from ipaddress to any port portnumber
```
```
sudo ufw allow from 192.168.1.3 to any port 44
sudo ufw deny from 192.168.1.3 to any port 44
```

```
sudo ufw allow from 192.168.1.3 to 192.168.1.1 port 44
sudo ufw deny from 192.168.1.3 to 192.168.1.1 port 44
```
allow/deny an IP address to connect to port 44 of your server.















