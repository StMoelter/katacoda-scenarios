Der Pod aus dem letzten Beispiel sollte noch laufen:  
`kubctl get pods`{{execute}}   
Ist die Liste leer den Pod starten mit:         
`kubectl run mypod --image=nginx`{{execute}}   

## Datei aus Pod kopieren
Zum kopieren benutzt man das **cp** Kommando. Dazu muss in dem Pod das Programm **tar** installiert sein.   
Hier wird die index.html aus dem nginx-Pod auf den lokalen Rechner kopiert:  
`kubectl mypod:/usr/share/nginx/html/index.html index.html`{{execute}}    

Ein Blick in die Datei, ob das auch funtioniert hat:   
`cat index.html`{{execute}}    

## Datei in den Pod kopieren:
Um zu seheh, ob die Datei auch in den Pod kopiert wurde, wird die lokale index.html geändert.   
### Datei anpassen
```
cat << EOF > index.html
<!DOCTYPE html>
<html><head><title>
Kopierte Datei
</title></head><body>
<h1>Kopierte Datei</h1>
</body>
EOF
```{{execute}}   

### Datei kopieren
Hier wird die lokale Datei in den Pod kopiert.   
`kubectl index.html mypod:/usr/share/nginx/html/index.html`{{execute}}   

Test, ob die Datei kopiert wurde:   
`curl $(kubectl get pod mypod -o jsonpath="{.status.podIP}")`{{execute}}    
Hier sollte jetzt die geänderte HTML Datei ausgeliefert werden.


