

## Install and configure iptables
Use the following steps to install and configure iptables:

Install the iptables-services package (if it is not already installed) by running the following command:
```
$ yum install iptables-services
```
Enable the service to start at boot time by running the following commands:
```
$ systemctl enable iptables && systemctl enable ip6tables
```
Next, add iptables rules. You can do this in either of the following ways:

From the command-line interface (CLI), by running commands similar to iptables -I INPUT ...
```
iptables -R INPUT -p tcp --destination-port 8084 -s 172.16.238.14 -j ACCEPT
iptables -A INPUT -p tcp --destination-port 8084 -j DROP

service iptables save
```
By creating or editing your /etc/sysconfig/iptables file to look similar to the following basic example, which leaves ports 22 and 80 open:
```
$ cat /etc/sysconfig/iptables
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [214:43782]
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-port-unreachable
COMMIT
```
```
$cat /etc/sysconfig/ip6tables

*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [214:43782]
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -j REJECT --reject-with icmp6-adm-prohibited
COMMIT
```
(Optional) If you are saving your rules in the /etc/sysconfig/ip{,6}tables files, you must also run the following commands:
```
$ systemctl restart iptables && systemctl restart ip6tables
```
Next, check that the iptables service is active by running the following commands:
```
$ systemctl status iptables && systemctl status ip6tables
```
Check your iptables rules by running the following commands:
```
$ iptables -L
$ ip6tables -L
```
Verify that your server is listening on the ports that you opened (22 and 80 in the above example) by running the following command:
```
$ netstat -plant
```
Query the systemd journal for a log of the changes that you made to the iptables service by running the following commands:
```
$ journalctl -f -u iptables.service
$ journalctl -f -u ip6tables.service
```
Reboot the server. The iptables rules should be saved and automatically reloaded.
