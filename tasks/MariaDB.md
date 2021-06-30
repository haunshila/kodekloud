### MariaDB Troubleshooting

* Login to database server as root
```
ssh user@server
sudo su
```

Check mysql installed if not install mysql, and start mysql: 
```
systemctl status mysql
yum install mysql
systemctl start mysql
```

Start mariadb and check status:
```
systemctl start mariadb
systemctl status mariadb
```

* Troubleshoot already if it is already installed mariadb or not working after restargin mariaDB service
```
# check logs
journalctl -u mariadb
```
Once you see that systemctl status and journalctl -xe are not useful, you should always search in var/log/mariadb/mariadb.log , if something is present in that file by saying mysqld have no permission to write in a folder. 
So changing the owner of that folder to mysql user permit to mysqld to write there.
```
sudo chown mysql:mysql /var/run/mariadb
```
