<pre class="file" data-filename="deployment.yaml" data-target="replace">
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
          mountPath: "/etc/nginx/auth/"
          readOnly: true
      volumes:
      - name: authvolume
        secret:
          secretName: mysecret
</pre>