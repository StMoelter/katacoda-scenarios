Der Bereich **resources** gibt an wieviel CPU und Speicher ein Container benutzen darf, bzw initial reserviert wird.    
Hier werden die Unterpunkte **requests** und **limits** betrachtet.   
Mehr Details finden sich im Link am Ende.   
    
## limits
Die **limits** setzen den maximalen Verbrauch an CPU, bzw. Speicher fest.  
CPU und Speicher werden auf diese Werte geregelt. Das kann auch schonmal zu einem Out Of Memory Error führen, wodurch der Container durchgestartet wird. Details finden in der Dokumentation, die am Ende der Seite verlinkt ist. 
## requests
Unter **requests** wird definiert wieviel Ressourcen (CPU und Speicher) initial reserviert werden. Dies ist für den Scheduler wichtig. Der Scheduler sucht einen geeigneten Node für den Pod, dieser Node muss genug freie Ressourcen wie unter **requests** definiert besitzen.  
Gibt es mehrere Container in einem Pod, so wird hier die Summe über alle COntainer benutzt.    
Benutzt ein Container mehr Speicher als unter **requests** angegeben, so kann der ganze Pod von dem Node entfernt werden, wenn der Node zu wenig Ressourcen hat. In diesem Falle wird der Pod auf einem anderen Node ausgelagert und wieder gestartet, in so fern es einen Node gibt, der die Anforderungen von **request** erfüllt.   
Ist **requests** nicht gesetzt so wird diese mit **limits** gleich gesetzt. Die Werte für **limits** sind i.d.R. viel höher.    
     
Für Entwicklungssysteme oder zum Testen der K8s Konfiguration macht es Sinn kleine Requests zu wählen. Dadurch können viele Entwicklungsumgebungen auf weniger Nodes laufen. Auf Produktionssystemen kann es Sinn machen die Requests hochzusetzen, damit der Node auch unter Last genug Resourcen besitzt.   
   
## CPU 
Der Parameter CPU wird in Einheiten von einer CPU angebenen. Also eine '1' beudeutet, dass eine CPU, bzw. Hyperthread benutzt werden kann. Da COntainer evtl. weniger Leistung brauchen gibt man die EInheiten auch im milli CPU mit der Einheit _m_ an. Eine ganze CPU wird als:   
**1000m*** oder **1**  
angeben.

## Memory
Der Speicher wird in Bytes angegeben. Wobei es die Abkürzungen:   
_E, P, T, G, M, K_ gibt, bezogen auf eine Basis von 1000 Bytes und   
_Ei, Pi, Ti, Gi, Mi, Ki_ bezogen auf eine Basis von 1024 Bytes.   
Eigentlich von Interesse sind i.d.R.:
- M:  1.000.000 Bytes
- Mi: 1.048.576 Bytes (1024^2)
- G:  1.000.000.000 Bytes
- Gi  1.073.741.3824 Bytes (1024^3)

## Beispiele
### CPU geht über das Limit
    
<pre class="file" data-filename="cpu.yaml" data-target="replace">   
apiVersion: v1
kind: Pod
metadata:
  name: cpu
spec:
  containers:
  - name: cpu
    image: stmoelter/alpine-sleep-user
    command:
    - stress-ng
    - --cpu
    - "2"
    resources:
      limits:
        cpu: 250m
      requests:
        cpu: 100m
</pre>   
   
`kubectl apply -f cpu.yaml`{{execute}}   
Sicherstellen, dass der Pod gestartet wurde:      
`kubectl get pod cpu`{{execute}}  

Aktueller CPU Verbrauch:   
`kubectl top pod cpu`{{execute}}   
     
`k exec -it cpu -- top`{{execute}}       

Details des Pods:   
`kubectl describe pod cpu`{{execute}}   

### CPU Request ist höher als vorhandene Ressourcen auf den Nodes
    
<pre class="file" data-filename="cpu.yaml" data-target="replace">   
apiVersion: v1
kind: Pod
metadata:
  name: cpu
spec:
  containers:
  - name: cpu
    image: stmoelter/alpine-sleep-user
    command:
        - stress-ng
        - --cpu
        - "5"
    resources:
      limits:
        cpu: 100
      requests:
        cpu: 100
</pre>   
   
`kubectl delete pod cpu`{{execute}}   

`kubectl apply -f cpu.yaml`{{execute}}   
Status des Pods ansehen:      
`kubectl get pod cpu`{{execute}}    

Details des Pods:   
`kubectl describe pod cpu`{{execute}}  

Ressourcen freigeben:   
`kubectl delete pod cpu`{{execute}}   


## Weitere Dokumentation
[https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)