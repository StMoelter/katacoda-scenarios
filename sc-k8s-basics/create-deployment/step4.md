## Secret in Deployment einbinden
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
        image: stmoelter/create-deployment-demo-nginx:1.0
        volumeMounts:
        - name: authvolume
          mountPath: "/etc/nginx/auth/"
          readOnly: true
      volumes:
      - name: authvolume
        secret:
          secretName: mysecret
</pre>

## Starten
`kubectl apply -f deployment.yaml`