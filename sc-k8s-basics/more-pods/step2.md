## Pod yaml erstellen
<pre class="file" data-filename="pod.yaml" data-target="replace">
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: nginx
    image: nginx
</pre>   