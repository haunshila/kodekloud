* Login in app server
* create .sh file in mentioned foler
```
touch <folder>/<.sh file name>
```
* add below commands to archieve and copy the zip file
```
#!/bin/bash
zip -r /backup/xfusioncorp_media.zip /var/www/html/media
scp /backup/xfusioncorp_media.zip clint@stbkp01:/backup/
```
* Create ssh files to copy files in backup server without prompt of password

1. create a keygen files in app server
```
ssh-keygen
```
2. copy public rsa file in authorized_keys of backup server using below commands
```
cat .ssh/id_rsa.pub | ssh clint@stbkp01 'cat >> .ssh/authorized_keys'
```
3. test above steps are configured properly, in app-server

```
ssh-copy-id clint@stbkp01

```
