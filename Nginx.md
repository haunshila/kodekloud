## linux nginx reverse proxy
* check linux OS version
```
cat /etc/*release
cat /etc/*version

```
Connect to backup server and switched to root 
```
# Ater ssh into server
sudo -i
```
### Install Apache
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
### Install nginx
```
yum install epel-release
yum install nginx
```
* Go to nginx config by typing
```
 vi /etc/nginx/nginx.conf
```
* Edit the config as follows. For reverse proxy add the proxy_pass in location tab like this config image.
 ![NGINX configuration](https://github.com/haunshila/kodekloud/blob/master/nginx_config_reverse_proxy.png)
 
 Save it and restart nginx

### Test the configuration

* Go backe to jump host and copy index.html file 
```
scp /home/index.html backup_server_user@backup_server_ip:/tmp
```
* Now switch to backup server and copy it to httpd document root
```
cp /tmp/index.html /var/www/html
```
* Restart Apache server
```
systemctl restart httpd
```
* Finally move to jump_host and check
```
# curl http://<BACKUP_SERVER_IP>:<NGINX-PORT>
curl http://172.16.238.16:8093
```
Ref:
* https://www.linuxpathfinder.com/How-to-Install-Apache-using-yum-in-Linux
* https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7
* https://phoenixnap.com/kb/nginx-reverse-proxy
