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
