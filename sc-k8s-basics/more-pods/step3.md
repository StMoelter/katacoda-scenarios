Zusammen mit dem **Image** bei der Containerdefinition innerhalb des Pods kann die **imagePullPolicy** gesetzt werden. Diese kann folgende Werte haben: 
- _Always_
- _IfNotPresent_
- _Never_

## Always
Bei jedem Erzeugen eines Pods wird geprüft, ob das lokale Image noch aktuell ist und bei Bedarf aus der Registry neu geladen. **Always** ist die präferierte Einstellung und sollte immer gewählt werden.   
    
## IfNotPresent   
Dies wird nur angewandt, solange der Tag des Images definiert, aber nicht **latest** ist.   
Das Image wird nur dann aus der Registry geladen, wenn es lokal noch nicht vorliegt. Sollte das Image nach dem initialen Laden in der Registry geändert worden sein, so wird es lokal nicht erneuert.   
Sollte das Image-Tag **latest** oder nicht gesetzt sein, so verhält sich die **imagePullPolicy** wie unter **Always** beschrieben.   

## Never
Das Image wird nicht von einer Registry geladen und wird lokal erwartet.   
   
## Keine Angabe
Wenn die **imagePullPolicy** nicht angegeben wird, so verhält sie sich wie unter **IfNotPresent** beschrieben.

