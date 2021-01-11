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
        image: stmoelter/create-deployment-demo-nginx
        volumeMounts:
        - name: authvolume
        mountPath: "/etc/nginx/.htpasswd"
        readOnly: true
      volumes:
      - name: authvolume
        secret:
          secretName: mysecret
          items:
         - key: auth
</pre>