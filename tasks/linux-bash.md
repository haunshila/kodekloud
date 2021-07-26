### Linux Bash Script


#### Create bash script
* go to the secific folder where you want to put the script and create using below command to perform tasks
```
vi name_of_the_script.sh
```
* Put below line at top of the script which make it this file as bash script
```
#!/bin/bash
```
* To zip and copy it to remote server, put below lines in .sh file
```
zip -r <zip-name>.zip PATH-OF-THE-FOLDER-WHICH-YOU-WANT-TO-ZIP
scp full-path-of-above-zip user@server:SERVER-FULL-PATH
i.e.
scp /backup/some.zip clint@stbkp01:/backup/
```

* Then create a keygen and copy the key to backup server so that bash script will not require any password
you need to put ssh public file of app-server to remote server/backup server

```
#in app server
# make sure .ssh folder is present in app server
ssh-keygen
# above command create .pub and secret file
ssh-copy-id -i PATH-OF-PUB-FILE clint@stbkp01
```
Finally go to scripts folder and run the bash scripts by this command
```
sh  script-name.sh
```
