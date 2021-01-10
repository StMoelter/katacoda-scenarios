## Dokumentation Service
`kubectl explain service`{{execute}}

## Service yaml erstellen
<pre class="file" data-filename="service.yaml" data-target="replace">
apiVersion: v1
kind: Service
metadata:
  name: myservice
spec:
  selector:
    app: app-pod-label
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
</pre>   

## Service starten
`kubectl apply -f service.yaml`{{execute}}

## Status
`kubectl get services`{{execute}}   
## Auf Service zugreifen
`k describe services myservice | grep IP`
