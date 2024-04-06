# Socat

Basic Syntax:
```
socat [options] <source> <destination>
```

## Chat Communication (Bidirectional Data Transfer)
On listener side:
```
socat -d -d TCP-LISTEN:1337 -
```
On client side:
```
socat -d -d TCP-CONNECT:127.0.0.1:1337 -
```

## File Transfer
File Transfer
On listener side:
```
socat -d -d TCP-LISTEN:1337 OPEN:filetransfer.txt,create //create a new file if not found
<or>
socat -d -d TCP-LISTEN:1337 OPEN:filetransfer.txt,trunc //overwrite the file if found
<or>
socat -d -d TCP-LISTEN:1337 OPEN:filetransfer.txt,excl //do not overwrite the file if found
<or>
socat -d -d TCP-LISTEN:1337 OPEN:filetransfer.txt,append //append to the existing file 
```
On client side:
```
socat -d -d TCP-CONNECT:127.0.0.1:1337 FILE:/PATH/TO/FILE
```
or
```
socat -d -d FILE:/PATH/TO/FILE TCP-CONNECT:127.0.0.1:1337 #This will make more sense
```
## Service Exposing

On listener side:
```
socat TCP-LISTEN:80 TCP:127.0.0.1:8080
```
or
```
socat TCP-LISTEN:80,fork,reuseaddr TCP:127.0.0.1:8080
```
"fork" for allowing multiple connections
- by forking(duplicating) new chile processes with different(unique/their own) pid incluing the socket bound to the same address and port to establish new connections while the main parent process still remain listening for tcp connections.

"reuseaddr" for faster restart of server
- by allowing socket in time_wait stage to rebind the same address and port (while by default is not allowed by operating system)
- or by allowing newly forked socket to rebind the same address and port when one the sockets in this address enters a time_wait stage

or
```
socat TCP-LISTEN:80,fork,reuseaddr,bind=127.0.0.1 TCP:127.0.0.1:8080 
```
"bind=127.0.0.1" for limiting the connections to the loopback interface while "bind=192.168.100.28" might be for wlan0 or eth0.


## TCP Port Forwarding
```
socat TCP-LISTEN:8080,fork TCP:remote_server:80
```

client -> node:80 -> server:8080
connections are forwarded from node to server
In node:
```
socat TCP4-LISTEN:80,fork,reuseaddr,bind=192.168.100.254 TCP4:server:8080
```
or
```
socat -T5 TCP4-LISTEN:80,fork,reuseaddr,bind=192.168.100.254 TCP4:server:8080
```
"-T5" for terminating the connection after inactive for 5s.

## Creating SSL Certificate

Generate a Private Key
```
openssl genrsa -out server.key 2048
```
Create a Certificate Signing Request (CSR)
```
openssl req -new -key server.key -out server.csr
```
Generate a Self-Signed Certificate (Optional)
```
openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```
Sign the Certificate (Optional): If you want to obtain a certificate signed by a certificate authority (CA), you need to submit the CSR (server.csr) to a CA for signing. The CA will then provide you with a signed certificate that you can use.

Implementing this in one line
```
openssl req -newkey rsa:2048 -nodes -keyout cert.key -x509 -days 1000 -out cert.crt
```

## UDP Forwarding
```
socat UDP-LISTEN:5000,fork UDP:remote_host:5000
```

## Encrypted Communication using OpenSSL
```
socat - OPENSSL-LISTEN:443,cert=server.pem,verify=0 TCP4:localhost:80
```
