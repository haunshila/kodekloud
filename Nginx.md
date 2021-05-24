#### linux nginx reverse proxy
* check linux OS version
```
cat /etc/*release
cat /etc/*version

```

##### Install Apache
Use the following steps to install Apache:

Run the following command:
```
 yum install httpd
```
Update the port in /etc/httpd/conf/httpd.conf
```
vi  /etc/httpd/conf/httpd.conf

Listen 6000

```
Use the systemd systemctl tool to start the Apache service:
```
 systemctl start httpd
```
Enable the service to start automatically on boot:
```
 systemctl enable httpd.service
```

Open up port 80 for web traffic:

 firewall-cmd --add-service=http --permanent
Reload the firewall:

 firewall-cmd --reload
Confirm successful installation by entering your server’s IP address in a browser to view the default Apache test page.

Ref:
https://www.linuxpathfinder.com/How-to-Install-Apache-using-yum-in-Linux
https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7
https://phoenixnap.com/kb/nginx-reverse-proxy
