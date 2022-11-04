apiVersion: v1
kind: Pod
metadata:
 name: secret-xfusion
 labels:
   name: myapp
spec:
  volumes:
   - name: secret
     secret:
       secretName: beta
  containers:
   - name: secret-container-xfusion
     image: debian:latest
     command: [ "/bin/bash", "-c", "--" ]
     args: ["while true; do sleep 30; done;"]
     volumeMounts:
      - name: secret
        mountPath: /opt/apps
