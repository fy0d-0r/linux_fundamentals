## Uncomplicated Firewall

### Status and Enabling
```
ufw status
ufw enable
```


### Default Policy
```
ufw default allow outgoing
ufw default deny incoming
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
ufw allow ssh
ufw allow 20 //the same as ssh
```

