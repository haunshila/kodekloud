### Linux Postfix Troubleshooting
```
# install postfix on mentioned server, if it is not installed
yum install postfix -y

# check the status of postfix
systemctl status postfix

# to see the logs of specific service i.e. postfix
journalctl -u postfix

# edit the configuration as per logs
vi /etc/postfix/main.cf
```
