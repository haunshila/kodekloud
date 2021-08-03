### Application Security @Firewall
##### Step 1: Login to backup server
```
ssh clint@stbkp01
```
#### Step 2: Add these two Rules
```
sudo iptables -A INPUT -p tcp --dport 8099 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 8085 -m conntrack --ctstate NEW -j REJECT
sudo iptables-save > /etc/sysconfig/iptables
```
#### Now, check if the rules are added or not
```
cat /etc/sysconfig/iptables
```

Restart ipatables
```
systemctl start iptables
# OR
systemclt restart iptables
```

### Application Security: block all incoport request on port 8400 and accept all request on 8000
* First check iptables service is running
```
systemctl status iptables
```
* Start and enable as a service 
```
systemctl start iptables
systemctl enable iptables
```
* block all request from port 6400 and accept all from port 8000 
```
iptables -I INPUT -p tcp --destination-port 6400 -j DROP

iptables -I INPUT -p tcp --destination-port 8000  -j ACCEPT

service iptables save
```
* check the applied rules
```
iptables -L
```
