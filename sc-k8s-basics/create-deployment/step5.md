Es wurde in diesem Szenario die Konfiguration des Deployments geändert und zugewiesen, so dass das Deployment mit den neuen Konfigurationen durchgestartet wird. In der Regel ändert man da **image**, um die neueste Softwareversion bereit zu stellen.

## Deployment Versoin 2.0
Hier wird jetzt die Version 2.0 ausgerollt:   
<pre class="file" data-filename="deployment.yaml" data-target="replace">
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myfirstdeployment
  labels:
    app: app-deployment-label
spec:
  replicas: 3
  selector:
    matchLabels:
      app: app-pod-label
  template:
    metadata:
      labels:
        app: app-pod-label
    spec:
      containers:
      - name: nginx
        image: stmoelter/create-deployment-demo-nginx:2.0
        volumeMounts:
        - name: authvolume
          mountPath: "/etc/nginx/auth/"
          readOnly: true
      volumes:
      - name: authvolume
        secret:
          secretName: mysecret
</pre>   
   
Wichtig ist hier also **image: stmoelter/create-deployment-demo-nginx:2.0**   

Das wird gestartet mit:  
`kubectl apply -f deployment.yaml`  

Das sollte nun ausgerollt sein:
`k get pods`{{execute}}   

Nun soll die Version 2 der Webseite ausgeliefert werden:   
`curl $(kubectl get pod myfirstpod -o jsonpath="{.status.podIP}")`{{execute}}   

## Ändern von Selektoren
Wenn Pod-Selektoren geändert werden, dann funktioniert das erstmal nicht:   
   
  
