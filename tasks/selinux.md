### Selinux Installation
* Install Selinux packages
```
yum install policycoreutils policycoreutils-python selinux-policy selinux-policy-targeted libselinux-utils setroubleshoot-server setools setools-console mcstrans
```
* check selinux config and update if requiered
```
cat /etc/selinux/config
# for task if it is asked to disable SELINUX update /etc/selinux/config as below
SELINUX=disabled
```
Ref:-
1. https://www.digitalocean.com/community/tutorials/an-introduction-to-selinux-on-centos-7-part-1-basic-concepts
2. https://www.linode.com/docs/guides/a-beginners-guide-to-selinux-on-centos-7/
