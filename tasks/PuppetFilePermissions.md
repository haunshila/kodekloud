### Puppet Setup File Permissions	

* switch as root and cd into folder mentioned in task and create puppet file (.pp) on master node (jump_host)
```
    vi news.pp

```
* Put below details in .pp file
```
class file_modifier {

   # Update news.txt under /opt/security

   file { '/opt/security/news.txt':
   
    # its ensure that file is already present
     ensure => 'present',

    # set the content 
     content => 'Welcome to xFusionCorp Industries!',

    # set the file permission
     mode => '0655',

   }

 }

# node/server details where you want to put files, check the question and configure accordingly on master node.
 node 'stapp01.stratos.xfusioncorp.com' {

   include file_modifier

 }
```

* validate puppet file at master node
```
puppet parser validate news.pp
```

* now, logged in app server node, switched to root and run command to run puppet file
```
puppet agent -tv
```
