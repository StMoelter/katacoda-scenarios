# Erstellung eines Deployments inklusive Service
Ziel ist es mehrere **nginx** Instanzen zu starten und über einen Service auf einer IP Adresse im Cluster zu veröffentlichen.   
Dabei gibt es eine öffentliche Seite und Seite, die mit einem Passwort (httpauth) geschützt ist.   
Dieses Szenario baut auf dem Szanrio 'Erstellen eines Pods in Kubernetes' auf.  