### Apache Redirects

* SSH into server and swtched as root
```
sudo su
```
* if asked to update the port of apache (httpd)
```
vi /etc/httpd/conf/httpd.conf

# Find Listen 8080 and update port from 8080 to asked port i.e.
Listen 5000
```

* To configure redirects, need to create file /etc/httpd/conf.d/main.conf with below content
```
# non www to www permanent redirect
<VirtualHost *:5000>
  ServerName undesired.example.com

  Redirect 301 / http://www.example.com:5000/
</VirtualHost>

# temprory redirect www.example.com:5000/blog/ to www.example.com:5000/news/
<VirtualHost *:5000>
  ServerName www.example.com:5000/blog/

  Redirect 302 /blog/ http://www.example.com:5000/news/
</VirtualHost>
```

* Test above configurations
```
curl undesired.example.com
curl www.example.com:5000/blog/
```



