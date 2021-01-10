## Kubernetes starten
Das Kubernetes Cluster muss als erstes gestartet werden:   
`launch.sh`{{execute}}   

## Dokumentation Deployment
`kubectl explain deployment`{{execute}}

## Deployment yaml erstellen
Als Erstes wird das Deployment erstellt:   
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
</pre>  

## Deployment starten
Das Deployment wird aktiviert mit:   
`kubectl apply -f deployment.yaml`{{execute}}  

## Übersicht
Eine Übersicht über die Deployments erhält man mit:   
`kubectl get deployments`{{execute}}   
Details des Deployments zeigt:   
`kubectl describe deployment myfirstdeployment`{{execute}}   
Es wurden 3 Pods gestartet, die in der Pod Übersicht angezeigt werden:   
`kubectl get pods`{{execute}}  
Man kann jetzt auf den Server zugreifen mit:   
`lynx $(kubectl get pods -o=json | jq -r [.items[].status.podIP][0])`{{execute}}   
## Skalieren auf der Kommandozeile
Die Anzahl der laufenden Pods lässt sich mit:   
`k scale deployment myfirstdeployment --replicas=5`{{execute}}   
ändern.




