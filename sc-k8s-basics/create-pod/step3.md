## Pod über yaml Datei starten
Die Konfiguration für einen Pod werden zur Reproduzierbarkeit in einer Datei gespeichert. z.B.:   
```
cat << EOF > pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: mysecondpod
  namespace: default
spec:
  containers:
  - name: nginx
    image: nginx
EOF
```{{execute}}   
    
Die yaml Datei wird benutzt um den Pod zu starten:   
`kubectl apply -f pod.yaml`{{execute}}   
Der erste Unterschied ist, dass hier ein **apply** mit der Datei ausgeführt wird. Das es sich um einen Pod handelt ist in der Datei definiert. Über das **apply** lassen sich also beliebige Resourcen starten oder ändern. Eine Konfigurationsdatei kann beliebig viele Resourcen definieren.   

Wie auch im letzten Beispiel kann man jetzt die gleichen Aktionen ausführen:   
      
`kubectl get pods`{{execute}}  
    
`kubectl describe pod mysecondpod`{{execute}}   
     
`kubectl describe pod mysecondpod | grep State`{{execute}}      

 `kubectl describe pod mysecondpod | grep IP`{{execute}}    

   
`kubectl get pod mysecondpod -o=yaml`{{execute}}   

