# Unit Files

Unit files have three sections
```
[Unit]
[Service]
[Install]
```

## Service Types
Service Type options configure how the unit is treated when it starts up.
```
Type=exec
Type=notify
Type=simple
Type=forking
Type=oneshot
Type=dbus
Type=idle
```
Type option indicates startup behaviour.





