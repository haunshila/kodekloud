###  Linux Access Control Lists

* Login on App server as per the task
```
ssh user@appserver
# switch to root
sudo su -
```

* Check existing premissions
```
getfacl /etc/hostname  

# output will be like this
getfacl: Removing leading '/' from absolute path names                                                           

# file: etc/hostname                                                                                            

# owner: root                                                                                                   

# group: root                                                                                                   

user::rw-                                                                                                       

group::r--                                                                                                      

other::r--                      
```
* Check users are already created
```
# id <username>
id john

# Output:
uid=1003(john) gid=1003(john) groups=1003(john)
```
* Set ACLs
```
  The setfacl utility sets ACLs (Access Control Lists) of files and directories. On the command line, a sequence of commands is followed by a sequence of files     (which in turn can be followed by another sequence of commands, and so on).

  The options -m and -x expect an ACL on the command line. Multiple ACL entries are separated by commas (","). The options -M and -X read an ACL from a file or     from standard input. The ACL entry format is described in the ACL Entries section, below.

   The --set and --set-file options set the ACL of a file or a directory. The previous ACL is replaced. ACL entries for this operation must include permissions.

  The -m (--modify) and -M (--modify-file) options modify the ACL of a file or directory. ACL entries for this operation must include permissions.

  The -x (--remove) and -X (--remove-file) options remove ACL entries. It is not an error to remove an entry which does not exist. Only ACL entries without the     perms field are accepted as parameters, unless the POSIXLY_CORRECT environment variable is defined.

  The perms field is a combination of characters that indicate the permissions: read ("r"), write ("w"), execute ("x"), or "execute only if the file is a           directory or already has execute permission for some user" (capital "X"). Alternatively, the perms field is an octal digit ("0"-"7").
 ```
 ```
 # john with no access, eric with read only access
 setfacl -m u:john:-,eric:r /etc/hostname
 ```
Ref:-
* https://www.redhat.com/sysadmin/linux-access-control-lists
* https://www.tecmint.com/secure-files-using-acls-in-linux/
