### Linxu Nginx SSL

#### Install nginx
```
yum install epel-release
yum install nginx
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
* create index.html in root PATH, if it is already there, remove it using below command
```
rm index.html
```
* restart nginx
* Go to jump server and verify the connects by using below command
```
curl -Ik https://<APP-SERVER-IP>
```
