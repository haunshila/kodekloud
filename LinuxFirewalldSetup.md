* To check the status of nginx and httpd
```
systemctl status nginx && systemctl status httpd
```

* To check the port number for nginx and httpd
```
grep -i Listen /etc/httpd/conf/ht* /etc/nginx/nginx.conf
```

* install firewall & start and check status
```
yum install firewalld -y
systemctl start firewalld && systemctl enable firewalld && systemctl status firewalld
```


* adding firewall rules to allow and block, update NGINX_PORT and APACHE_PORT in below commands
```
firewall-cmd --zone=public --add-port=NGINX_PORT/tcp --permanent
firewall-cmd --permanent --zone=public --add-service={http,https}
firewall-cmd --permanent --zone=public --add-rich-rule 'rule family="ipv4" source address="<LBR IP>" port protocol=tcp port=APACHE_PORT accept'
firewall-cmd --permanent --zone=public --change-interface=wan

firewall-cmd --reload
firewall-cmd --get-active-zones
systemctl restart firewalld && systemctl status firewalld
firewall-cmd --zone=public --list-ports && firewall-cmd --zone=public --list-all && firewall-cmd --list-all
```

Also, modified the nginx config file
```
server {
#nginx port
listen 8091;
#nginx port
listen [::]:8091;
# This severname should be IP of app server
server_name 172.16.238.10;
root /usr/share/nginx/html;
}

systemctl restart nginx
systemctl status httpd
```
