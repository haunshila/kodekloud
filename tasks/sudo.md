# Configure sudo

* Installing sudo if it is not already installed
```
# RHEL/CentOS
yum install sudo -y
```

* Adding the sudo user if its not there
Get a List of All Users using the /etc/passwd File 
Local user information is stored in the /etc/passwd file. 
Each line in this file represents login information for one user. 
To open the file you can either use cat or less :
```
cat /etc/passwd
```
A sudo user is a normal user account on a Linux or Unix machine.

```
RHEL/CentOS and Debian
adduser mynewusername
```

* Enable Passwordless Sudo For User rose in Linux

  * Edit sudoers file: sudo nano /etc/sudoers
  * Find a line which contains includedir /etc/sudoers.d
  * Below that line add: username ALL=(ALL) NOPASSWD: ALL , where username is your passwordless sudo username; Save your changes.
  ```
  rose ALL=(ALL) NOPASSWD:ALL
  ```
