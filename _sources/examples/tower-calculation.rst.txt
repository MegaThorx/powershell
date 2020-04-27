Zapfenrechnen
=============

Berechne den Zapfen für eine Zahl welche der Benutzer eingeben kann.

Lösung
~~~~~~

.. code:: powershell

   [float]$zahl = Read-Host -Prompt "Welche Zahl soll berechnet werden?"
   $position = 0
   $maximum = 9

   do{
       $position += 1 # Zähler um 1 erhöhen
       $old = $zahl # Vorherige Zahl zwischenspeichern für die Ausgabe
       $zahl = $zahl * $position # Neue Zahl berechnen
       write-host "$old * $position = " $zahl # Ausgabe der Position
   }
   until ($position -eq $maximum)

   # Zähler zurückstellen
   $position = 0

   do{
       $position += 1 # Zähler um 1 erhöhen
       $old = $zahl # Vorherige Zahl zwischenspeichern für die Ausgabe
       $zahl = $zahl / $position # Neue Zahl berechnen
       write-host "$old / $position = " $zahl # Ausgabe der Position
   }
   until ($position -eq $maximum)

