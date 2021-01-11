## Secret Dokumentation
`kubectl explain secret`{{execute}}

## Secret yaml erstellen
<pre class="file" data-filename="secret.yaml" data-target="replace">
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  .htpasswd: vdXNlcjE6JGFwcjEkaG5MYWpObXIkLjFUcU5pL0dObWpmLzhEbkx4ZGxHMAo=
</pre>   

## Starten
`kubectl apply -f secret.yaml`{{execute}}

## Beschreiben
`kubectl get services`{{execute}}   
   
`kubectl describe service myservice`{{execute}}   
   