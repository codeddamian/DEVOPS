#### Puppet Database Setup 
Question: 
> The Nautilus DevOps team had a meeting with development team last week to discuss about some new requirements for an application deployment. 
> Team is working on to setup a mariadb database server on Nautilus DB Server in Stratos Datacenter. They want to setup the same using Puppet. 
> Below you can find more details about the requirements:

>Create a puppet programming file ecommerce.pp under /etc/puppetlabs/code/environments/production/manifests directory on puppet master node
> i.e on Jump Server. Define a class mysql_database in puppet programming code and perform below mentioned tasks:
1. Install package mariadb-server (whichever version is available by default in yum repo) on puppet agent node i.e on DB Server also start its service.
2. Create a database kodekloud_db10 , a database userkodekloud_aim and set passwordksH85UJjhb for this new user also remember host should be localhost.
Finally grant some usual permissions like select, update (or full) ect to this newly created user on newly created database.

> Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.


Solution 

```
---
Puppet file 

class mysql_database {
    package {'mariadb-server':
      ensure => installed 
    }
 service {'mariadb':
      ensure  => ruuning,
      enable  =>  true
      }
 mysql::db { 'kodekloud_db10':
   user       =>  'kodekloud_aim',
   password   =>  'ksH85UJjhb',
   host       =>  'localhost',
   grant      =>  ['ALL'];
 }
   
}

node 'stdb01.stratos.xfusioncorp.com' {
   include mysql_database
}   
  
---

```

After entering the puppet file, you need to valider it with the command, *Puppet paser validate filename* 
Go to the stdserver and check the puppet agent - puppet agent -tv 
After which you check for the status of the mariadb. and loggin to the database with command 
db command: mysql -u dbname -p datab
