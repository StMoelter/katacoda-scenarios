## Kubernetes starten
In diesem Kurs benutzen wir ein Kubernetes Cluster. Dieses muss allerdings als erstes gestartet werden. Dazu einfach das Script:   
`launch.sh`{{execute}}   
ausführen.   

## kubectl
Um mit dem K8s API Server zu kommunizieren und Status Abfragen zu tätigen, sowie Befehle zu erteilen benutzt man den kubectl Client.   
Der Client hat eingebaute Dokumentationen.
## API Resourcen
Eine Liste aller API Resourcen lässte sich mit dem Befehl:   
`kubectl api-resources`{{execute}}   
anzeigen.   
Hier interessiert uns die Resource 'pods' oder kurz 'po' genannt.   
## Pod Resource Dokumentation
Eine Übersicht über die Definition der Pod Resource kann man sich mit:   
`kubectl explain pod`{{execute}}   
ausgeben lassen.   
Dabei ist kubectl recht tolerant als Resourcen-Name funktioniert 'pod', 'pods' oder 'po'.
