Piping
======

Mit Piping (Pipelining) können in PowerShell Befehlsketten gebaut
werden. Wenn man eine Pipe (= \|) in PowerShell verwendet wird das
Ergebnis eines Befehls nicht direkt an den Benutzer weitergegeben
sondern an den nächsten Befehl in der Befehlskette.

.. code:: powershell

   Get-Process | ForEach-Object { Write-Host $_.Name } # Gibt alle laufenden Prozesse aus
   # oder
   Get-Process | Get-Member # Gibt alle Methoden und Properties einenes Prozesses aus
   # oder
   (Get-Process | Get-Random).Name # Gibt den Namen eines zufälligen Prozesses aus

