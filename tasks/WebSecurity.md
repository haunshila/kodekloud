## How to Hide Apache Version Number and Other Sensitive Info

```
$ sudo vi /etc/httpd/conf/httpd.conf 
```

* And add/modify/append the lines below:
```
ServerTokens Prod
ServerSignature Off 
```

* restart the apache server
```
sudo systemctl restart httpd
```
## How do I disable directory browsing?
* open file with vi /etc/httpd/conf/httpd.conf 
* Update specific directory with below content.. remove indexes as Options
```
<Directory /var/www/>
        Options FollowSymLinks
        AllowOverride None
        Require all granted
</Directory>
```
