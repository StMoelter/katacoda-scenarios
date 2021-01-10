## Kubernetes starten
Das Kubernetes Cluster muss als erstes gestartet werden:   
`launch.sh`{{execute}}   

## Deployment yaml erstellen
Als erstes wird das Deployment erstellt:   
<pre class="file" data-filename="app.js" data-target="replace">
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
        image: stmoelter/create-deployment-demo-nginx
</pre>