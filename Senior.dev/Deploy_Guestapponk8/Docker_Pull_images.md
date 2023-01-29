# Nautilus project developers are planning to start testing on a new project. As per their meeting with the DevOps team, 
  they want to test containerized environment application features. As per details shared with DevOps team, we need to accomplish the following task
  
  a. Pull busybox:musl image on App Server 1 in Stratos DC and re-tag (create new tag) this image as busybox:media.

```
SSH to the Server > ssh name@servername
step 2: check docker images -> docker images 
step 3 pull docker image -> docker pull busybox:musl 
step 4 retag docker image as busybox:media -> docker image tag busybox:musl  busybox:blog
step 5 verify docker image retage -> docker images 
```
