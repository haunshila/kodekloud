## Configure protected directories in Apache

Change username, server and directory name according 
to task when you retry it
* Step 1: login to server mention in Task
```
ssh banner@stapp03
sudo -i
```
* Step 2: Add a user and set password & restart httpd
```
htpasswd -c /etc/httpd/.htpasswd james
systemctl restart httpd
```
* Step 3: Edit configuration
```
vi /etc/httpd/conf/httpd.conf 
```

###### Scroll down to the <Directory> section for 
###### "/var/www/html" and change  
```
AllowOverride to All
```
* Step 4: Create mentioned Directory
```
mkdir /var/www/html/sysops 
```
* Step 5: Go to sysops directory and create .htaccess file
```
vi .htaccess
```

Give this configuration
```
 AuthType Basic
 AuthName "Password Required"
 Require valid-user
 AuthUserFile /etc/httpd/.htpasswd
 ```
* Step 6: Copy file
Now go to jump server and copy index file
```
scp /tmp/index.html banner@stapp03:/tmp
```

Again copy from tmp folder to mentioned directory
```
cp /tmp/index.html /var/www/html/sysops
```
* Step 7: Test
```
curl -u james http://127.0.0.1:8080/sysops/index.html
```


- Ref : 
1. https://www.nbtechsupport.co.in/2021/01/configure-protected-directories-in.html 
2. https://youtu.be/jcp68jEgiVE

