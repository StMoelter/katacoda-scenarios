## Kubernetes starten
In diesem Kurs wird ein Kubernetes Cluster genutzt. Dieses muss allerdings als erstes gestartet werden. Dazu wird einfach das Script:   
`launch.sh`{{execute}}   
ausgeführt.   

## kubectl
Um mit dem K8s API Server zu kommunizieren und Status Abfragen zu tätigen, sowie Befehle zu erteilen benutzt man den kubectl Client.   
Der Client hat eingebaute Dokumentationen, welche über das Kommando **explain** abgerufen wird.
## API Resourcen
Eine Liste aller API Resourcen lässt sich mit dem Befehl:   
`kubectl api-resources`{{execute}}   
anzeigen.   
Hier ist die Resource 'pods' oder kurz 'po' für dieses Szenario von Interesse.    
## Pod Resource Dokumentation
Eine Übersicht über die Definition der Pod Resource kann man sich mit:   
`kubectl explain pod`{{execute}}   
ausgeben lassen.   
Dabei ist kubectl recht tolerant als Resourcen-Name funktioniert 'pod', 'pods' oder 'po'.
