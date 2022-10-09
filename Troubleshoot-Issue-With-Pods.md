### One of the junior DevOps team members was working on to deploy a stack on Kubernetes cluster. 
### Somehow the pod is not coming up and its failing with some errors. We need to fix this as soon as possible. Please look into it.



##### There is a pod named webserver and the container under it is named as nginx-container. It is using image nginx:latest

#####  There is a sidecar container as well named sidecar-container which is using ubuntu:latest image.

##### Look into the issue and fix it, make sure pod is in running state and you are able to access the app.

#####  Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.


_Solution

Kubectl get pods 

Then:
The second option is to extract the pod definition in YAML format to a file using the command 
###### kubectl get pod <pod name> -o yaml > my-new-pod.yaml
  vi my-new-pod.yaml
and Edit the pod 
  
Then delete the existing pod 
#####   kubectl delete pod pod-name
Then create a new pod with the edited file
#### kubectl create -f my-new-pod.yaml

