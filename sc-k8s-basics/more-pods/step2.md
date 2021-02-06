Mit Labels werden den Pods einfache Schlüssel Wertepaare zugeordnet. Mit diesen lassen sich die Pods danach selektieren. 
Die Labels sind ein Hauptinstrument bei Kubernetes um die Pods und andere Resourcen zu organisieren. Labels können nicht nur auf Pods gesetzt werden. Die Benutzung auf anderen Resourcen ist analog zu Pods. In diesem Szenario werden nur Pods betrachtet.  

## Pods mit Labels erzeugen
Es werden 4 Pods mit verschiedenen Labels erzeugt:   
   
<pre class="file" data-filename="labeled-pods.yaml" data-target="replace">
---
apiVersion: v1
kind: Pod
metadata:
  name: labeledpod-1-1
  labels:
    app: server
    tier: frontend
    extra: whatelse
spec: {containers: [{name: nginx-1, image: nginx}]}
---
apiVersion: v1
kind: Pod
metadata:
  name: labeledpod-2-1
  labels:
    app: server
    tier: backend
spec: {containers: [{name: nginx-2, image: nginx}]}
---
apiVersion: v1
kind: Pod
metadata:
  name: labeledpod-1-2
  labels:
    app: sleep
    tier: frontend
spec: {containers: [{name: sleep-1, image: stmoelter/alpine-sleep-user}]}
---
apiVersion: v1
kind: Pod
metadata:
  name: labeledpod-2-2
  labels:
    app: sleep
    tier: backend
    extra: whatever
spec: {containers: [{name: sleep-2, image: stmoelter/alpine-sleep-user}]}
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
`kubectl get pods -l tier=frontend -o jsonpath='{.items[*].metadata.labels}'`{{execute}}   
Dies liefert alle Pods mit dem *frontend* *tier* zurück.   
Alternativ:   
`kubectl get pods -l tier!=frontend`{{execute}}
`kubectl get pods -l tier!=frontend -o jsonpath='{.items[*].metadata.labels}'`{{execute}}  
gibt die pods zurück, die nicht im *frontend tier* sind.   

#### Kombination
Die verschiedenen Labels können kombiniert werden, dadurch trennt man sie mit einem Komma.   
Alle Pods die im Backend schlafen:   
`kubectl get pods -l tier=frontend,app=sleep`{{execute}}
`kubectl get pods -l tier=frontend,app=sleep  -o jsonpath='{.items[*].metadata.labels}'`{{execute}}
   
### Testen ob der Label in einer Liste ist
Beim kombinierten Test werden die Bedingungen mit **und** verknüpft. Möchte man ein **oder** haben, so wird dies ermöglicht in dem getestst wird, ob das Label in einer Liste ist, ähnlich wie der **IN(.., ..)** Operator in SQL.   
`kubectl get pods -l 'tier in (frontend, backend)'`{{execute}}   
oder auch negiert:   
`kubectl get pods -l 'tier notin (frontend)'`{{execute}}    
Eine Kombination ist beliebig möglich:
`kubectl get pods -l 'tier notin (frontend),app=server'`{{execute}}   
   
### Testen ob ein Label gesetzt ist oder nicht (Existenzprüfung)
Auf 2 Pods ist das _extra_ Label gesetzt:   
`kubectl get pods -l 'extra'`{{execute}}   
andere Pods haben das Label nicht gesetzt:   
`kubectl get pods -l '!extra'`{{execute}}   

### Testen ob ein Label gesetzt ist aber einen Wert nicht besitzt
Hier soll der Pod mit einem extra Label selektiert werden, das nicht _whatelse_ ist. Also hier nur der letzte Pod _labeledpod-2-2_ welcher das Label _extra_ mit dem Wert _whatever_ besitzt.      
Dazu schaut man auf Pods, dessen Label nicht _whatelse_ ist:    
`kubectl get pods -l 'extra!=whatelse'`{{execute}}   
bzw.    
`kubectl get pods -l 'extra notin (whatelse)'`{{execute}}   
Es werden nun auch die Pods ausgebenen, die das Label nicht gesetzt haben.   
Die gewünschte Ausgabe erhält man durch eine Kombination mit der Existenzprüfung:   
`kubectl get pods -l 'extra,extra notin (whatelse)'`{{execute}}

## Weitere Infos
[https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

