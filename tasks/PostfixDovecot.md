### Install Postfix

* install Postifix using command:
```
sudo su -
yum install -y postfix

```
* Configuring Postfix, /etc/postfix/main.cf file:

```
vi /etc/postfix/main.cf
```
  Find and edit the following lines:
  ```
  ## Uncomment and set your mail server FQDN ##
  myhostname = stratos.xfusioncorp.com

  ##Uncomment and Set domain name ##
  mydomain = xfusioncorp.com

  ## Uncomment ##
  myorigin = $mydomain

  ## Uncomment and Set ipv4 ##
  inet_interfaces = all

  ## Change to all ##
  inet_protocols = all

  ## Comment ##
  #mydestination = $myhostname, localhost.$mydomain, localhost,
  
  ##Uncomment ##
  mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

  ## Uncomment and add IP range ##
  mynetworks = 192.168.1.0/24, 127.0.0.0/8

  ## Uncomment##
  home_mailbox = Maildir/
  ```
Save and exit the file.

Start/restart Postfix service now:
```
systemctl enable postfix
systemctl restart postfix
```
* Testing Postfix mail server
First, create a  user called “john“.

useradd john
Set the password for the user:

passwd YchZHRcLkL
Access the server via Telnet and enter the commands manually shown in red colored text.

telnet localhost smtp

Now navigate to the user “john“ mail directory and check whether the new mail has been received.
```
ls /home/john/Maildir/new/
```
Sample output:
```
112323722056.DFAadfF.stratos.xfusioncorp.com

```
Success! A new mail is received to the user “john“.

To read the mail, enter the following command:

```
cat /home/sk/Maildir/new/112323722056.DFAadfF.stratos.xfusioncorp.com
```
If there will be fields with "X-Original-To" and "Delivered-To" associated with appropriate value
Done. Postfix is working!!

### Install Dovecot




Ref:
https://www.unixmen.com/setup-a-local-mail-server-in-centos-7/
