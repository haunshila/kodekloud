### Configure Local Yum repos

* pacage location is provided by the portal like /packages/downloaded_rpms/
*  Switch to the system and login as a user with root or sudo privileges.
```
sudo su -
```
* To check existing repo list, before and after configuration
```
yum repolist
```
* create local repo config file under '/etc/yum.repos.d/' directory
```
cd /etc/yum.repos.d/
vi localyum.repo
```
* put below content in localyum.repo,  set Repository ID as asked in question

[localyum]

name=localyum

baseurl=file:///packages/downloaded_rpms/

enabled=1

gpgcheck=0
```

* Run a command to install a package with the yum package manager
```
sudo yum install wget

```

Ref:
* https://phoenixnap.com/kb/create-local-yum-repository-centos

