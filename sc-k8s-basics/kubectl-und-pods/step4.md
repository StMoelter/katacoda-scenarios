kubectl hat einen eingebauten **top** Befehl mit dem sich der aktuelle CPU und Speicherverbrauch eines Pods und einer Node ausgeben lassen. Hier wird nur der Pod betrachtet.

## Pod unter Stress setzen
Mit dem Befehl stress-ng lässt sich CPU Last und Speicherverbrauch anstoßen.   
`kubectl run stress --image stmoelter/alpine-sleep-user --command -- stress-ng --cpu 1 --vm 1 --vm-bytes 200M`{{execute}}    
Ob der Pod läuft wird wieder mit:   
`k get pod stress`{{execute}}   
ermittelt.   

## Top ausführen
Der Befehl:   
`k top pod stress`{{execute}}   
gibt nun den aktuellen Resourcenverbrauch des Pods aus

## Details
Wie üblich gibt es eine Dokumentation unter:   
`k help top`{{execute}}
