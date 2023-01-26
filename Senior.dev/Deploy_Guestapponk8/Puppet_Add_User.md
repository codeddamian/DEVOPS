 # Puppet Add Users 
> A new teammate has joined the Nautilus application development team, the application development team has asked the DevOps team
  to create a new user account for the new teammate on application server 1 in Stratos Datacenter. The task needs to be performed using Puppet only.
  You can find more details below about the task.

+ Create a Puppet programming file official.pp under /etc/puppetlabs/code/environments/production/manifests directory on master node i.e Jump Server,
  and using Puppet user resource add a user on all app servers as mentioned below:
 
+ Create a user ammar and set its UID to 1144 on Puppet agent nodes 1 i.e App Servers 1.

+ Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues.
  In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.

+ :- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, 
  also please make sure to run puppet agent test to apply/test the changes manually first.
  
``` 
class user_creator {

user { 'ammar':

ensure   => present,

uid => 1144,

 }

}

node 'stapp01.stratos.xfusioncorp.com', 'stapp02.stratos.xfusioncorp.com', 'stapp03.stratos.xfusioncorp.com' {

include user_creator

}

Step 2 Puppet parser validate filemname.pp 
step 3 ssh to the server where the file will be used  ssh tony@stapp01
step 4 puppet agent -tv 
step 5 Validate by - cat /etc/passwd | grep username 


```
