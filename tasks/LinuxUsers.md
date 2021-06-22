### Create non interactive shell user
```
adduser USERNAME -s /sbin/nologin
```

Ref:
* https://www.tecmint.com/add-users-in-linux/

### Create linux user with expiry
```
$ sudo useradd -e YYYY-MM-DD username

```

### Get a List of All Users using the /etc/passwd File #
Local user information is stored in the /etc/passwd file. Each line in this file represents login information for one user. 
To open the file you can either use cat or less :
```
less /etc/passwd
```
