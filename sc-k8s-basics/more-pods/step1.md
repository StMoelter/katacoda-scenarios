Hier wird betrachtet, wie ENV-Variablen in einem Pod (bzw. dem Container im Pod) gesetzt werden.   
Die Variablen können entweder direkt gesetzt oder durch Secrets befüllt werden.   
Das Befüllen über Secrets wird später erst behandelt.

## Kubernetes starten
Zu Beginn der Lektion muss Kuberbetes gestartet werden:   
`launch.sh`{{execute}}

## YAML Datei mit ENV erstellen
<pre class="file" data-filename="envpod.yaml" data-target="replace">
apiVersion: v1
kind: Pod
metadata:
  name: envpod
spec:
  containers:
    - name: nginx
      image: nginx
      env:
        - name: RUNS_ON_K8S
          value: 'true'
</pre>   
   
Hier ist die Sektion **env** unter **spec** interessant und dass dort Arrays von Key, Value Paaren die Variablen definieren.   

## Pod starten
Hier wird der Pod mit dem **apply** Befehl gestartet:   
`kubectl apply -f envpod.yaml`{{execute}}   
und sichergestellt, dass er auch läuft:   
`kubectl get pod envpod`{{execute}}   
   
## ENV ausgeben lassen
Über den **printenv** Befehl von Linux wird hier die **RUNS_ON_K8S** Umgebungsvariable ausgegeben:     
`kubectl exec envpod -- printenv RUNS_ON_K8S`{{execute}}   

## Pod abräumen
Dieser Pod wird nicht mehr benötigt und kann gelöscht werden:   
`kubectl delete pod envpod`{{execute}}