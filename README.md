# obfsproxy-VPN
How To Make VPN With Obfsproxy 

+ Having access to root

```
sudo apt-get update
``` 

```
sudo apt-get upgrade
```
+ Install PiVPN: with
```
sudo curl -L https://install.pivpn.io | bash
```
+ Follow the on screen instructions. The protocol must be `TCP`, and I chose `5110` as my port 
+ Install obfsproxy: 
```
sudo apt-get install obfsproxy
```
+ Create a service file 
```
sudo nano /etc/systemd/system/obfsproxy.service
``` 
with contents:

```
[Unit] 
Description=VPN-ObfsProxy 
After=network.target 
After=syslog.target

[Service] 
ExecStart=/usr/bin/obfsproxy --log-min-severity=info obfs3 --dest=127.0.0.1:5110 server 0.0.0.0:5112 
Restart=always

[Install] 
WantedBy=multi-user.target
```

```
sudo systemctl enable obfsproxy
``` 
```
sudo systemctl start obfsproxy
```
```
sudo systemctl status obfsproxy
```
+ If you change to script:
```
sudo systemctl daemon-reload
```

+ Check that 5110 and 5112 are listening with `netstat -plnt`

+ Create a user and private key for the VPN with `pivpn -add -o` then enter the desired username and password
