## Kubernetes starten
In diesem Kurs wird ein Kubernetes Cluster genutzt. Dieses wir gestartet mit:   
`launch.sh`{{execute}}   

## Einen Pod starten
Als Beispiel Pod wird ein Pod mit einem einzelnen nginx Container verwendet.   
`kubectl run mypod --image=nginx`{{execute}}   
    
Es kann einen Moment dauer, bis der Pod gestartet ist, deshalb sichergehen mit:   
`kubectl get pod mypod`{{execute}}       
   
   
## Befehl in Pod ausführen 
 Wie auch bei Docker kann ein zusätzlichen Befehl in einem Pod ausgeführt werden:   
 `kubectl exec -it mypod -- sh`{{execute}}  
 Wobei **-it** das Terminal verbindet und so Eingaben und Ausgaben erlaubt. Das **--** trennt den kubectl Befehl von dem Befehl dir im Pod ausgeführt werden soll.   
 Sollten sich mehrere Container in einem Pod befinden, so muss mit dem **--container** Parameter der gewünschte Containers gewählt werden.   
 Verzichtet man auf **it** so wird der Befehl ausgeführt und die Ausgabe in der Konsole angezeigt:   
 `kubectl exec userpod -- whoami`{{execute}}   
oder den Inhalt einer Datei ausgeben:   
 `kubectl exec mypod -- cat /usr/share/nginx/html/index.html`{{execute}}   

 ## Befehl als anderer User ausführen
 Aus Sicherheitsgründen sollte ein Container im Pod nicht als root ausgeführt werden.      
Mit Docker kann man als beliebeiger User Befehle ausführen, mit kubectl geht das nicht so einfach. Dafür wird ein Plugin benötigt, welches in einer seperaten Lektion besprochen wird.   
Folgendes Plugin löst das Problem:   
[kubectl-exec-as](https://github.com/jordanwilson230/kubectl-plugins/tree/krew#kubectl-exec-as)

-> TBD das hier in plugin Sektion verschieben
Das Kommando in dem Pod wird als **appuser** ausgeführt:   
 `kubectl run userpod --image=stmoelter/alpine-sleep-user`{{execute}}  
 und einmal sichergehen, dass der Pod läuft:   
 `kubectl get pod userpod`{{execute}} 
    
 das Image wurde mit folgendem Dockerfile erstellt:     
 ```
 FROM alpine:3.13.0
RUN addgroup -S appgroup -g 1000 && adduser -S appuser -G appgroup -u 1000
USER 1000
WORKDIR /home/appuser

CMD ["sleep", "infinity"]
```    
Lässt man sich jetzt den voreingestellten User ausgeben:   
`kubectl exec userpod -- whoami`{{execute}}   
So wird *appuser* ausgegeben. Es wurde auf **-it** verzichtet, dadurch wird nur die Ausgabe des Befehls (*whoami*) auf der Konsole ausgegeben und keine interaktive Shell gestartet.   



 ## Weitere Infos   
`kubectl help exec`{{execute}}
zigt nochmal die Optionen und Syntax für den **exec** Befehl.
