## Kubernetes starten
In diesem Kurs wird ein Kubernetes Cluster genutzt. Dieses wir gestartet mit:   
`launch.sh`{{execute}}   

## Einen Pod starten
Als Beispiel Pod wird ein Pod mit einem einzelnen nginx Container verwendet.   
`kubectl run mypod --image=nginx`{{execute}}  


## Befehl in Pod ausführen 
 Wie auch bei Docker kann ein zusätzlichen Befehl in einem Pod ausgeführt werden:   
 `kubectl exec -it mypod -- sh`{{execute}}  
 Wobei **-it** das Terminal verbindet und so Eingaben und Ausgaben erlaubt. Das **--** trennt den kubectl Befehl von dem Befehl dir im Pod ausgeführt werden soll.   
 Sollten sich mehrere Container in einem Pod befinden, so muss mit dem **--container** Parameter der gewünschte Containers gewählt werden.

 ## Befehl als anderer User ausführen
Das Kommando in dem Pod wird als **appuser** ausgeführt:   
 `kubectl run mypod --image=stmoelter/alpine-sleep-user`{{execute}}   
    
 das Image wurde mit folgendem Dockerfile erstellt:     
 ```
 FROM alpine:3.13.0
RUN addgroup -S appgroup -g 1000 && adduser -S appuser -G appgroup -u 1000
USER 1000
WORKDIR /home/appuser

CMD ["sleep", "infinity"]
```    
Lässt man sich jetzt den voreingestellten User ausgeben:   
`kubectl exec mypod -- whoami`{{execute}}   
So wird *appuser* ausgegeben. Es wurde auf **-it** verzichtet, dadurch wird nur die Ausgabe des Befehls (*whoami*) auf der Konsole ausgegeben und keine interaktive Shell gestartet.   

Aus Sicherheitsgründen sollte ein Container im Pod nicht als root laufen und einen User definieren.   
Mit Docker kann man als user **root** Befehle ausführen, mit kubectl gaht das nicht so einfach. Dafür wird ein Plugin benötigt, welches in einer seperaten Lektion besprochen wird.   
Folgendes Plugin löst das Problem:   
[kubectl-exec-as](https://github.com/jordanwilson230/kubectl-plugins/tree/krew#kubectl-exec-as)

 ## Weitere Infos   
`kubectl help exec`{{execute}}
zigt nochmal die Optionen und Syntax für den **exec** Befehl.
