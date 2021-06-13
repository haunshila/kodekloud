## Install And Configure PostgreSQL

* Login to database server

```
ssh peter@stdb01
```
* Login as root
```
sudo su
```
* Install postgresql
```
yum install postgresql-server postgresql-contrib
postgresql-setup initdb
systemctl enable postgresql && sudo systemctl start postgresql
systemctl status postgresql
```
* To configure DB and User: Enter into postgresql database

```
sudo -u postgres psql postgres
```
* Create user, database, and grant permission

```
CREATE USER kodekloud_aim WITH PASSWORD 'dCV3szSGNA';
CREATE DATABASE kodekloud_db8;
GRANT ALL PRIVILEGES ON DATABASE "kodekloud_db8" to kodekloud_aim;
\q
```
* Allow local client to connect using md5 method
  * Set the config for local
  ```
  sudo vi /var/lib/pgsql/data/pg_hba.conf
  ```
  * Go to bottom of the config and edit, make sure that indentation as listed as for sample in pg_hba.conf file
  ```
  local all all md5
  host all all 127.0.0.1/32 md5 
  ```
  * Next open another config
  ```
  sudo vi /var/lib/pgsql/data/postgresql.conf
  ```
  * Uncomment below line
  ```
  listen_address=localhost
  ```
  * Re-start postgre
  ```
  sudo systemctl restart postgresql
  sudo systemctl status postgresql.service
  ```
* Finally Check
```
psql -U kodekloud_aim -d kodekloud_db8 -h 127.0.0.1 -W

psql -U kodekloud_tim -d kodekloud_db8 -h localhost -W
```


