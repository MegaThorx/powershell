Ein-/Ausgabe von Daten (Read-Host)
==================================

Mit dem Cmdlet ``Read-Host`` wird eine Eingabezeile aus der Konsole
gelesen. Man kann mit ihm einen Benutzer zur Eingabe auffordern.

Erstelle ein Programm in welchem man sein Alter eingibt und diese dann
wieder mittels ``Write-Host`` ausgegeben wird.

Lösung
~~~~~~

.. code:: powershell

   $age = Read-Host "Please enter your age"
   Write-Host "Your age is" $age

