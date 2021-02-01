Mit Labels werden den Pods einfache Schlüssel Wertepaare zugeordnet. Mit diesen lassen sich die Pods danach selektieren. 
Die Labels sind ein Hauptinstrument bei Kubernetes um die Pods und andere Resourcen zu organisieren. Labels können nicht nur auf Pods gesetzt werden. Die Benutzung auf anderen Resourcen ist analog zu Pods. In diesem Szenario werden nur Pods betrachtet.  

## Pods mit Labels erzeugen
Es werden 4 Pods mit verschiedenen Labels erzeugt:
<pre class="file" data-filename="labeled-pods.yaml" data-target="replace">
apiVersion: apps/v1
kind: pod
metadata:
  name: labeledpod_1_1
  labels:
    app: server
    tier: frontend
spec: {container: [{name: nginx_1, image: nginx}]}
---
apiVersion: apps/v1
kind: pod
metadata:
  name: labeledpod_2_1
  labels:
    app: server
    tier: backend
spec: {container: [{name: nginx_2, image: nginx}]}
---
apiVersion: apps/v1
kind: pod
metadata:
  name: labeledpod_1_2
  labels:
    app: sleep
    tier: frontend
spec: {container: [{name: sleep_1, image: stmoelter/alpine-sleep-user}]}
---
apiVersion: apps/v1
kind: pod
metadata:
  name: labeledpod_2_2
  labels:
    app: sleep
    tier: backend
    extra: whatever
spec: {container: [{name: sleep_2, image: stmoelter/alpine-sleep-user}]}
</pre>   
Diese Pods werden nun auch mit dem **apply** Kommando gestartet:   
`kubectl apply -f labeled-pods.yaml`{{execute}}  
und natüröich wieder getstet, ob diese auch gestartet sind:   
`kubectl get pods`{{execute}}   
   
## Pods selektieren
Es gibt verschiedene möglichkeiten Pods zu selektieren. Die kann in einer **.yaml** Datei geschehen, um z.B. Pods wür ein Deployment zu selektieren. Hier wird nur die Selektion auf der KOmmandozeile im **get pods** Kommando betrachtet. Die **.yaml** hat kennt die gleichen Selektoren.   
Auf der Kommandozeile besitzt **kubectl** die Option **-l**, um nach Labels zu selektieren.   

### Testen auf Gleicheit oder Ungleichheit
Dies ist ein einfacher Selektor, es wird geschaut, ob einem Schlüssel ein definierter Wert zugeordnet ist oder nicht:   
`kubectl get pods -l tier=frontend`{{execute}}   
Dies liefert alle Pods mit dem *frontend* *tier* zurück.   
Alternativ:   
`kubectl get pods -l tier!=frontend`{{execute}}  
gibt die pods zurück, die nicht im *frontend tier* sind.   

#### Kombination
Die verschiedenen Labels können kombiniert werden, dadurch trennt man sie mit einem Komma.   
Alle Pods die im Backend schlafen:   
`kubectl get pods -l tier=frontend, app=sleep`{{execute}}



