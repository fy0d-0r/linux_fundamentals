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
ufw allow ssh
ufw allow 20 //the same as ssh
```

