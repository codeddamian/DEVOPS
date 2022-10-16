# Setup-Puppet-Certificate.
> The Nautilus DevOps team has set up a puppet master and an agent node in Stratos Datacenter. 
 Puppet master is running on jump host itself (also note that Puppet master node is also running as Puppet CA server) and 
 Puppet agent is running on App Server 2. Since it is a fresh set up, the team wants to sign certificates for puppet master as well as puppet agent
 nodes so that they can proceed with the next steps of set up. You can find more details about the task below:



+ Puppet server and agent nodes are already have required packages, but you may need to start puppetserver (on master) and puppet service on both nodes.
- Assign and sign certificates for both master and agent node.

**Root Priviledges are required on both nodes**

```
On the Puppet master node go to the `etc` directory and afterwards the `hosts` subdirectory - `vi /etc/hosts`
Step2: Add `puppet` as an alias to the end of each hostname of the master server to resolve and save - `wq`
Step3: `systemctl status puppetserver` - to check the status
Step4: `puppetserver ca list --all`
Step5: Cat /etc/hosts and copy the hostnames 
Step6: Sign into the worker node and - `ssh x@y ` and past th emaster node hostname into the worker node. 
Step7: `systemctl status puppet` - to check the status
step8: `systemctl Restart puppet` - to start
Step9:  `puppetserver ca list --all`
Step10: `puppetserver ca sign --all` to sign the certidficate
Step11: To test `puppet -agent t
```









##### Why we Setup a Puppet Certificate 
>+ Puppet can use its built-in certificate authority (CA) and public key infrastructure (PKI) tools or use an existing external CA for all of its secure socket layer (SSL) communications.
>+ Puppet uses certificates to verify the the identity of nodes. These certificates are issued by the certificate authority (CA) service of a Puppet primary server. When a node checks into the Puppet v for the first time, it requests a certificate. The Puppet primary server examines this request, and if it seems safe, creates a certificate for the node. When the agent node picks up this certificate, it knows it can trust the Puppet primary server, and it can now identify itself later when requesting a catalog.
 >+ After installing the Puppet Server, before starting it for the first time, use the puppetserver ca setup command to create a default intermediate CA. For more complex use cases, see the Intermediate and External CA documentation.
(https://puppet.com/docs/puppet/7/ssl_certificates.html)
