# Uncomplicated Firewall (UFW)
## Basics

### Enabling
```
sudo systemctl enable ufw.service
sudo systemctl start ufw.service
sudo ufw enable
```

### Status
```
sudo ufw status
sudo ufw status numbered
sudo ufw status verbose
sudo ufw show raw
sudo ufw app list
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

### For Specific Protocol
```
sudo ufw allow proto udp from any to any
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

### Allow Local Network Connections
```
sudo ufw allow 192.168.0.0/24 
```

### Using App List
```
sudo ufw app list
sudo ufw allow Transmission
```

### Rate limitation
```
sudo ufw limit ssh
sudo ufw limit 80
```

### Deleting Rules

```
sudo ufw status numbered
sudo ufw delete rule_number
```

### Resetting UFW Rules
```
sudo ufw reset
```

## Logging
```
sudo ufw logging on
sudo ufw loggine off
```
```
sudo less /var/log/ufw*
```











