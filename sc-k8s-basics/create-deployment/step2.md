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
Das starten des Services erfolgt analog zu den anderen Resourcen:   
`kubectl apply -f service.yaml`{{execute}}

## Status
Einen Überblick über die Services zeigt:   
`kubectl get services`{{execute}}   
Die detailierte Ansicht des Services findet sich mit:
`kubectl describe service myservice`{{execute}}   
## Auf Service zugreifen
Die IP Adresse findet sich im der Beschreibung des Service:   
`kubectl describe services myservice | grep IP`{{execute}}   
über diese Adresse kann auf die Pods zugegriffen werden.

## DNS
-> TBD katacoda DNS funktioniert nicht wie beschrieben.
