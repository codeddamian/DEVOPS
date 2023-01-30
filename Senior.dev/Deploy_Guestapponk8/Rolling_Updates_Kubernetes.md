### We have an application running on Kubernetes cluster using nginx web server. The Nautilus application development team has pushed some of the latest
 changes and those changes need be deployed. The Nautilus DevOps team has created an image nginx:1.19 with the latest changes.

### Perform a rolling update for this application and incorporate nginx:1.19 image. The deployment name is nginx-deployment

+ Make sure all pods are up and running after the update.

+ Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.


```
Solution:

In jump_host check the deployment, 
+ kubectl get deployment nginx-deployment -o yaml    <-Then check the image container name. Here it is nginx-container

Next, set the updated image according to question. Here it is nginx:1.19 image

+ kubectl set image deployment/nginx-deployment nginx-container=nginx:1.19

# Run the watch command to see live rolling update with zero downtime

watch kubectl get pods

Finally check the status

kubectl rollout status deployment nginx-deployment

Then check the image

kubectl get deployment nginx-deployment -o yaml

```


 

 





