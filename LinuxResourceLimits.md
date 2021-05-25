Setting nproc hard/soft limits permanently- We have to edit in below file.
```
vi /etc/security/limits.conf

nfsuser soft nproc 79
nfsuser hard nproc 91
```
* validate after add
```
cat /etc/security/limits.conf | grep nproc | grep -v ^#

or

su - nfsuser
ulimit -u -S
ulimit -u -H
```

Ref:
* https://linuxhint.com/set_max_user_processes_linux/
