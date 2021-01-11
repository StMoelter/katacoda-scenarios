## ConfigMap Dokumentation
`kubectl explain configmap`{{execute}}

## Service yaml erstellen
<pre class="file" data-filename="secret.yaml" data-target="replace">
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
stringData:
  auth: user1:$apr1$hnLajNmr$.1TqNi/GNmjf/8DnLxdlG0
</pre>   