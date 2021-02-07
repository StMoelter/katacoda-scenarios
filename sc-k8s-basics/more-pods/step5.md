Ein Pod kann über einen oder mehrere Init-Container verfügen.  
Ein Init-Container wird benutzt um Arbeiten zu erledigen, bevor der (oder die) eigentliche(n) Container gestartet werden.   
Bricht der Init-Container mit einem Fehler ab, wird er nach einiger Zeit wieder ausgeführt. Läuft er ohne Fehler durch wieder der Container (oder der nächste Init-Container) gestartet.   
Die Init-Container werden in der Praxis genutzt um z.B. Datenbankmigration vor dem Start einer neuen Applikation durchzuführen oder arbeiten (z.B. Bereinigen) eines Filesystem durchzuführen, dass gemountet werden soll. Ein Init-Container kann auch auf Kubernetes Ressourcen, wie z.B. ein Service oder Secret warten, welches vom Container benutzt wird, bis der Container gestartet wird.  
   
Hier wird ein Pod mit einem Init-Container betrachtet.   

## Beispiel


<pre class="file" data-filename="init.yaml" data-target="replace">
apiVersion: v1
kind: Pod
metadata:
  name: init
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: workdir
      mountPath: /usr/share/nginx/html
  initContainers:
  - name: install
    image: busybox
    command:
    - echo
    - '<html><head><title>Init</title></head><body><h1>Init</h1></body></html>' 
    - ">"
    - "/init-dir/index.html"
    volumeMounts:
    - name: workdir
      mountPath: "/init-dir"
  volumes:
  - name: workdir
    emptyDir: {}
</pre>    
    

Container starten:   
`k apply -f init.yaml`{{execute}}   
   
Testen ob der Container läuft:   
`k get pod init`{{execute}}    
    
Ausgabe der index.html:   
`curl $(kubectl get pod myfirstpod -o jsonpath="{.status.podIP})`{{execute}}

## resources und Init Container
Als **request** und **init** Parameter werden die jeweiliger Maximalwerte vun **cpu**, bzw. **memory** benutzt.   
In die Berechnung der Maximalwerte gehen die einzelnen Werte jedes Init-Container, sowie die Summe über alle Container ein.  



