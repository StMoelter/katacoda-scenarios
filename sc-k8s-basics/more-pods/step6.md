Kubernetes kennt 3 verschiedene Tests für einen Container:
- startupProbe
- readinessProbe
- livenessProbe   
Die Proben gibt es nur für 'normale' Container, also nicht für Init-Container.

## startupProbe
Die **startupProbe** ist dazu gedacht zu warten, bis der Comtainer gestartet ist. Die **readinessProbe** und **livenessProbe** werden erst ausgeführt, wenn die **startupProbe** erfolgreich war. Führt die **startupProbe** nicht zum Erfolg, so wird Container durchgestartet.   
Dieser Test wird für langsam startende Container beutzt, damit die anderen Tests während des Startups nicht fälschlicherweise fehlschlagen.   
    
       
## readinessProbe
Die **readinessProbe** testet, ob der Container bereit ist und so der Pod Netzwerkverkehr vom Service erhalten soll.   
Der hier definierte Test wird permanent ausgeführt und wenn dieser Erfolgreich sind, so wird der Netzwerkverkehr an den Pod aktiviert. Schlägt der Test bei einem Container fehl, so wird der Pod von Service nicht mehr angesprochen.    
   
## livenessProbe
Wenn die **livenessProbe** fehlschlägt, so wird der Container innerhalb des Pods gelöscht und neu gestartet.   
  


