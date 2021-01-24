Gerade bei der Fehlerfindung möchte man die Ausgabe des Pods auf einem Port auf seiner lokalen Maschine nachvollziehen können. Dazu kann man via kubectl ein 'Port Forwarding' einrichten.

## Einen Pod starten
Als Beispiel Pod wird ein Pod mit einem einzelnen nginx Container verwendet.  
Wenn der Pod *mypod* aus dem vorherigem Beispiel noch nicht läuft:   
`kubctl get pods`{{execute}}   
Sollte dieser mit:     
`kubectl run mypod --image=nginx`{{execute}}    
gestartet werden.

## Tunneln
 In diesem Beispiel wird ein Port-Forwarding vom Port 80 im Pod auf Port 8081 der lokalen Maschine, die den kubectl Befehl ausführt.   
`kubectl port-forward mypod 8081:80 &`{{execute}}   
Test:    
`curl http://localhost:8081`{{execute}}      
Beenden der Port Weiterleitung:   
`killall kubectl`{{execute}}   
   
## Weitere Infos
Wie auch bei den anderen Kommandos kann eine Dokmunentation des Kommandos mit:   
`kubectl help port-forward`{{execute}}   


