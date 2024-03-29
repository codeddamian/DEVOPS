# Deploy Nginx and Phpfpm on Kubernetes
> The Nautilus Application Development team is planning to deploy one of the php-based application on Kubernetes cluster. As per discussion with DevOps team they have decided to use nginx and phpfpm. Additionally, they shared some custom configuration requirements. Below you can find more details. Please complete the task as per requirements mentioned below:

+ Create a service to expose this app, the service type must be NodePort, nodePort should be 30012.
+ Create a config map nginx-config for nginx.conf as we want to add some custom settings for nginx.conf.
+ Change default port 80 to 8099 in nginx.conf.
+ Change default document root /usr/share/nginx to /var/www/html in nginx.conf.
+  Update directory index to index index.html index.htm index.php in nginx.conf.
+ Create a pod named nginx-phpfpm .
+ Create a shared volume shared-files that will be used by both containers (nginx and phpfpm) also it should be a emptyDir volume.

+ Map the ConfigMap we declared above as a volume for nginx container. Name the volume as nginx-config-volume, mount path should be   /etc/nginx/nginx.conf and subPath should be nginx.conf

+ Nginx container should be named as nginx-container and it should use nginx:latest image. PhpFPM container should be named as php-fpm-container and it should use php:7.3-fpm image.

+ The shared volume shared-files should be mounted at /var/www/html location in both containers. Copy /opt/index.php from jump host to the nginx document root inside nginx container, once done you can access the app using App button on the top bar.

+ Before clicking on finish button always make sure to check if all pods are in running state.

+ You can use any labels as per your choice.

+ The kubectl utility on jump_host has been configured to work with the kubernetes cluster.


```apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-config
data:
  nginx.conf: |
    events {} 
    http {
      server {
        listen 8099;
        index index.html index.htm index.php;
        root  /var/www/html;
        location ~ \.php$ {
          include fastcgi_params;
          fastcgi_param REQUEST_METHOD $request_method;
          fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          fastcgi_pass 127.0.0.1:9000;
        }
      }
    }
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-phpfpm
  labels:
    app: nginx-phpfpm
spec:
  volumes:
    - name: shared-files
      emptyDir: {}
    - name: nginx-config-volume
      configMap:
        name: nginx-config
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-files
          mountPath: /var/www/html
        - name: nginx-config-volume
          mountPath: /etc/nginx/nginx.conf
          subPath: nginx.conf
    - name: php-fpm-container
      image: php:7.3-fpm
      volumeMounts:
        - name: shared-files
          mountPath: /var/www/html
---                                                                                                           
apiVersion: v1                                                                                                
kind: Service                                                                                                 
metadata:                                                                                                     
  name: nginx-phpfpm                                                                                        
spec:                                                                                                         
   type: NodePort                                                                                             
   selector:                                                                                                  
     app: nginx-phpfpm                                                                                        
   ports:                                                                                                     
     - port: 8099                                                                                               
       targetPort: 8099                                                                                         
       nodePort: 30012    
``` 

```
##### COMMANDS
    kubectl get configmap
    kubectl get pods
    kubectl apply -f updated with service exposeNginx and Phpfpm on Kubernetes
    kubectl cp /opt/index.php nginx-phpfpm:/var/www/html/ --container=nginx-container
    kubectl exec -it nginx-phpfpm -- /bin/bash [^1]
```
[https://www.nbtechsupport.co.in/2022/07/deploy-nginx-and-phpfpm-on-kubernetes.html)
[https://www.nginx.com/resources/wiki/start/topics/examples/full/)


