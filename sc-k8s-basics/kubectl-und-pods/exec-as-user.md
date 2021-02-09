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
`kubectl exec mypod -- whoami`{{execute}}   
So wird *appuser* ausgegeben. Es wurde auf **-it** verzichtet, dadurch wird nur die Ausgabe des Befehls (*whoami*) auf der Konsole ausgegeben und keine interaktive Shell gestartet.  