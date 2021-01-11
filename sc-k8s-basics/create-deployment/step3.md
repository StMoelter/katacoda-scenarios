## ConfigMap Dokumentation
`kubectl explain configmap`{{execute}}

## Service yaml erstellen
<pre class="file" data-filename="secret.yaml" data-target="replace">
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  .htpasswd: dXNlcjE6JGFwcjEkaG5MYWpObXIkLjFUcU5pL0dObWpmLzhEbkx4ZGxHMAo=
</pre>   