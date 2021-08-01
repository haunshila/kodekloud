### Linxu Nginx SSL

#### Install nginx
```
yum install -y epel-release
yum install -y nginx
```

#### Edit nginx.conf

* Uncomment the TLS section of server block
* set the server_name to IP of Application server
* note down the crt, key and root PATH
* 
#### Copy Certificate, Key and Index.html
* copy provided cert and key in respective PATH
```
cp /tmp/n.crt <nginx-path>

```
* Create index.html in root PATH, if it is already there, remove it using below command
```
rm index.html
```
* Let's set the owner of the directory and the file in it to the nginx user:

```
chown -R nginx:nginx /var/www/default/


```
* Let's save the file and check the config for errors:

```
nginx -t
```
* Now let's start Nginx and add it to autorun.
```
systemctl enable --now nginx
```
* restart nginx
```
systemctl restart nginx

```
* Go to jump server and verify the connects by using below command
```
curl -Ik https://<APP-SERVER-IP>
```
