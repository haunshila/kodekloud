### Install and configure HAProxy Load Balancer
* Login into load balancer system and switch to root
```
$ ssh user@lbr
$ sudo -i
```
* Install HAProxy using yum
```
$ yum -y install haproxy
```
* To configure HAProxy, open /etc/haproxy/haproxy.cfg, And create a backup of the configuration file in case of rollback
```
cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.bkp
vi /etc/haproxy/haproxy.cf
```
#### HAProxy 101
![HAProxy LBR](https://github.com/haunshila/kodekloud/blob/master/haproxy-load-balancer.png)
#### Edit the frontend and backend section of cfg file
- Update the frontend port and map appropriate backend
```
frontend http_front
   bind *:80
   stats uri /haproxy?stats
   acl url_blog path_beg /blog
   use_backend blog_back if url_blog
   default_backend http_back
```
- Update the backend host name, IP and ports under backend section
```
backend http_back
   balance roundrobin
   server server_name1 private_ip1:80 check
   server server_name2 private_ip2:80 check
```
- Save the cfg settings and then verify, enable, start and check status
```
haproxy -f /etc/haproxy/haproxy.cfg
systemctl enable haproxy && service haproxy start && service haproxy status
```
