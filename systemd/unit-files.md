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


notify and simple is default and common type
notify and simple types cause systemd to consider the service to be started up as soon as you start it.
notify is the same except it's not configured to be running until the process tells systemd that it's ready.
forking	- the process is configured to be started when other processes are spawned from a parent process and then the parent process stops to where the children are the only processes that are running.



### `Type=simple`

### `Type=exec`

### `Type=notify`

### `Type=oneshot`

### `Type=forking`

### `Type=dbus`

### `Type=idle`



