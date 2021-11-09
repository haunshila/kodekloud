### Docker EXEC Operations

* SSH into server and switch to root user
* check the kkloud container is runnning
```
docker ps
```
* EXEC to container and run a shell into container
```
docker exec -it kkloud /bin/sh
```

  * Install apache2 
  ```
  apt install apache2 -y
  apt install vim -y # In case you want to vi into the port.conf file
  ```
  * cd into apache2 dirctory to update port and host to localhost
   ```
    cd /etc/apache2
    ls -l

    # Update listening port from 80 to 5001 in ports.conf & apache2.conf file
    sed -i ‘s/Listen 80/Listen 5001/g’ ports.conf
    sed -i ‘s/:80/:5001/g’ apache2.conf
    
    # Uncomment/Overwrite the default server configuration to localhost
    sed -i ‘s/#ServerName www.example.com/ServerName localhost/g’ apache2.conf

    # Start apache service
    service apache2 start
    # enable as a service
    service apache2 enable
    # check the status of service
    service apache2 status
  ```
