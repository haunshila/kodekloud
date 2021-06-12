### Linxu Nginx SSL

#### Install nginx
```
yum install epel-release
yum install ngin
```

#### Edit nginx.conf

* Uncomment the TLS section of server block
* set the server_name to IP of Application server
* note down the crt, key and root PATH
* 
#### Copy Certificate, Key and Index.html
* copy provided cert and key in respective PATH
* create index.html in root PATH
* restart nginx
* Go to jump server and verify the connects by using below command
```
curl -Ik https://<APP-SERVER-IP>
```
