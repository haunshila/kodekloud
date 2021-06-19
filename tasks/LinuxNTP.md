## Linux NTP Setup

* Install NTP (logged in as root)
```
$ sudo -i
$ sudo yum install ntp
```

* we need is the address for public ntp servers closest to us or at a desired location. 
To get the list of all the ntp server, goto the following url,
http://www.pool.ntp.org/zone/@

& select the ntp server of your choosing. We will now make the server entries in ntp configuration 
file i.e. ‘/etc/ntp.conf’. For this tutorial, we will be using the ntp servers from North Ameraica/United states,

```
$ sudo vim /etc/ntp.conf


server 0.us.pool.ntp.org

server 1.us.pool.ntp.org

server 2.us.pool.ntp.org

server 3.us.pool.ntp.org

```
* Also enable logging to troubleshoot any issues with ntp, to do this make the entry for following line in the same file,
```
logfile /var/log/ntp.log
```
Save the file & exit. Restart the ntp service to implement the changes made,
```
$ sudo systemctl restart ntpd
```

Now to make sure that our ntp server is synchronized with the public ntp server, run the following command from the terminal,
```
$ ntpq –p
```

