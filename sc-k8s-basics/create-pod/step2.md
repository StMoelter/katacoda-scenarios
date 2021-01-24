## Übersicht über Pods
Eine Liste aller pods (im aktuellen Namespace) kann man sich anzeigen lassen mit:   
`kubectl get pods`{{execute}}   
Anstatt des Wortes 'pods' können natürlich andere API-Resourcen abgefragt werden, in diesem Szenario betrachten wir nur Pods.

## Einen Pod starten
Ein Pod kann mit dem **run** Kommando des kubectl Clients gestartet werden:   
`kubectl run myfirstpod --image=nginx`{{execute}}   
dabein diesem Beispiel wird das offizielle nginx Image der letzten Version vom Docker-Hub geladen und gestartet.  

Die Übersicht über die Pods wird jetzt einen laufenden Pod anzeigen:      
`kubectl get pods`{{execute}}   
## Pod beschreiben lassen
Details über den Pod wird mit:   
`kubectl describe pod myfirstpod`{{execute}}   
ausgeben.  
Interessant ist hier der Status, ob der Pod läuft:   
`kubectl describe pod myfirstpod | grep State`{{execute}}   
die Ausgabe sollte **running** sein.   
Falls das nicht der Fall ist, findet sich ganz unten in der kompletten Ausgabe unter Events weitere Details, die bei der Fehlerfindung behilflich sind.   
    
Wenn der Pod aktiv ausgeführt wird, dann hat er eine IP-Adresse zugewiesen bekommen, welche man auch beim **describe pod** findet:   
 `kubectl describe pod myfirstpod | grep IP`{{execute}}    
 Die IP Adresse kann man kopieren und darauf mal ein **ping**, **curl** oder **lynx** ausprobieren.  

 ## Logging
 Die Log-Ausgabe kann sieht man mit:   
 `kubectl logs myfirstpod`{{execute}}   
 eine permanente Ausgabe, wie man sie von `tail -f` gewöhnt ist erhält man auch hier mit dem **-f** Parameter. 

## yaml Ausgabe der Konfiguration
Die Ausgabe der Pod Konfiguration kann auch als yaml Datei Ausgeben werden:  
`kubectl get pod myfirstpod -o=yaml`{{execute}}   
Das ist ganz praktisch, wenn die Konfiguration eines schnell auf der Konsole erzeugten Pod (Resource) in einer Datei persistieren werden soll, z.B. um diese ins Repo zu überführen.  

## json Ausgabe
Die Ausgabe kann auch als json erfolgen:   
`kubectl get pod myfirstpod app=db-proxy -o json`{{execute}}  
Alternativ kann man sich auch nur einen Teil der Json-Ausgabe anzeigen lassen:   
`kubectl get pod -l app=db-proxy -o jsonpath="{.items[0].metadata.name}"`   

## Pod löschen
Wenn der Pod nicht mehr benötigt wird, so kann er mit:   
`kubectl delete pod myfirstpod`{{execute}}   
gelöscht werden.   
`kubectl get pods`{{execute}}   
Ist jetzt wieder leer.

## Anmerkung
Resourcen auf der Konsole über kubectl wie beschrieben zu starten, ist die denkbar schlechteste Methode und sollte nur in Ausnahmen benutzt werden.   
Das Problem ist, dass die Aktion nur schwer nachvollzogen werden kann, es entstehen also 'Snowflake Cluster'.   
Alle Kubernetes Resourcen gehören ins git Repository und sollen replizierbar zu erstellen sein.      


