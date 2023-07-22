Last week the Nautilus DevOps team met with the application development team and decided to containerize several of their applications. 
The DevOps team wants to do some testing per the following:

* Install docker-ce and docker-compose packages on App Server 2. 
* Start docker service. 

Docker is available in two versions,

 - Docker CE (Community Edition)
 - Enterprise Edition (EE) 


- sudo -i # run as root 
- root@docker-ce ~]#   dnf update -y ; #Install and update dnf befor use of this command 
- [root@docker-ce ~]#  dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo  # Enable Docker CE Repository
- root@docker-ce ~]#  dnf list docker-ce ; dnf list docker-ce --showduplicates | sort -r  #See available packages. 
- root@docker-ce ~]#  sudo dnf install docker-ce-3:18.09.1-3.el7 # to install 
- [root@docker-ce ~]# systemctl start docker
- [root@docker-ce ~]# systemctl enable docker
- [root@docker-ce ~]# docker --version  # check the version instal 
-[root@docker-ce ~]# docker run hello-world  # test that docker is working 

# install docker compose
 - [root@docker-ce ~]# dnf install curl -y
 - [root@docker-ce ~]# curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
-  [root@docker-ce ~]# $ sudo mv docker-compose /usr/local/bin && sudo chmod +x /usr/local/bin/docker-compose  # once the n=binary is Dl we move it to the binary folder /usr/local/bin/

```
credit: 
  https://www.linuxtechi.com/install-docker-ce-centos-8-rhel-8/
  https://linuxconfig.org/how-to-install-docker-in-rhel-8
```
