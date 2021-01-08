## Übersicht über Pods
Eine Liste aller pods (im aktuellen Namespace) kann man sich anzeigen lassen mit:   
`kubectl get pods`{{execute}}   
Anstatt des Wortes 'pods' kann man natürlich andere API-Resourcen nehmen, aber hier bleiben wir erstmal bei den Pods.

## Einen Pod starten
Ein Pod kann über einen Befehl mit dem kubectl Client gestartet werden:   
`kubectl run myfirstpod --image=nginx`{{execute}}   
dabei wird das offizielle nginx Image in der letzten Version vom Docker-Hub geladen und gestartet.  

Die Übersicht über die Pods sollte jetzt einen laufenden Pod anzeigen:      
`kubectl get pods`{{execute}}   
## Pod beschreiben lassen
Details über den Pod kann man sich mit:   
`kubectl describe pod myfirstpod`{{execute}}   
ausgeben lassen.  
Interessant ist hier erstmal der Status, ob der Pod läuft:   
`kubectl describe pod myfirstpod | grep State`{{execute}}   
die Ausgabe sollte **running** sein.   
Falls das nicht der Fall ist, einfach mal ganz unten in der kompletten Ausgabe unter Events schauen, da findet sich zumeist der Grund.   
    
Wenn der Pod aktiv ausgeführt wird, dann hat er eine IP-Adresse zugewiesen bekommen, welche man auch beim **describe pod** findet:   
 `kubectl describe pod myfirstpod | grep IP`{{execute}}    
 Die IP Adresse kann man kopieren und darauf mal ein **ping**, **curl** oder **lynx** ausprobieren.  

 ## Befehl in Pod ausführen 

## yaml Ausgabe der Konfiguration
Die Ausgabe der Pod Konfiguration kann man sich auch als yaml Datei Ausgeben lassen:  
`kubectl get pod myfirstpod -o=yaml`{{execute}}   
das ist ganz praktisch, wenn man die Konfiguration eines schnell auf der Konsole erzeugten Pod (Resource) in einer Datei persistieren möchte, z.B. um diese ins Repo zu überführen.    

## Pod löschen
Wenn der Pod nicht mehr benötigt wird, so kann er mit:   
`kubectl delete pod myfirstpod`{{execute}}   
gelöscht werden.   
`kubectl get pods`{{execute}}   
Sollte jetzt wieder leer sein.

## Anmerkung
Resourcen auf der Konsole über kubectl wie beschrieben zu starten, ist die denkbar schlechteste Methode und sollte nur in Ausnahmen benutzt werden.   
Das Problem ist, dass das nicht nachvollzogen werden kann, man bekommt also ein 'Snowflake Cluster'.   
Alle Kubernetes Resourcen gehören ins git Repository und sollen replizierbar zu erstellen sein.      


