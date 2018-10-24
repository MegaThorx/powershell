Try-Catch
=========

Mit Try-Catch kann man Fehler in Powershell behandeln. Falls ein Befehl
welcher im ``try``-Block steht einen Programmabbruch verursacht springt
das Programm zum ``catch``-Block und dort kann der Entwickler den Fehler
behandeln.

.. code:: powershell

   try {
       [int]$zahl = Read-Host "Zahl" # Powershell wirft einen Fehler falls man keine Zahl eingibt
       Write-Host "Die Zahl" $zahl # Dieser Code wird nicht ausgeführt falls es einen Fehler gibt
   } catch {
       Write-Host "Keine Zahl" # Gibt einen Fehler aus.
   }

Übung
-----

Schreibe ein Programm welches eine eingegeben Zahl durch 2 dividiert und
einen Fehler ausgibt falls der Benutzer keine Zahl eingibt.

.. code:: powershell

   try {
       [int]$zahl = Read-Host "Zahl"
       Write-Host $zahl / 2
   } catch {
       Write-Host "Keine Zahl"
   }

