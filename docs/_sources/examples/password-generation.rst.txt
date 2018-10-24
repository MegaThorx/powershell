Passwort generieren
===================

Generiere ein Passwort mit 5 Buchstaben, 2 Zahlen und einem
Sonderzeichen.

Lösung
~~~~~~

.. code:: powershell

   <#
       > (65..90) - ASCII Code für A-Z
       > (97..122) - ASCII Code für a-z
       mit ((65..90) + (97..122)) werden beide Arrays in einen neuen Array kombiniert.

       > Get-Random -Count 5
       Gibt 5 Einträge aus dem Array zurück

       > ForEach-Object {[char]$_}
       Mit [char]65 wird die Zahl in Text umgewandelt
   #>
   $letters = ((65..90) + (97..122) | Get-Random -Count 5 | ForEach-Object {[char]$_})
   $numbers = ((48..57) | Get-Random -Count 2 | ForEach-Object {[char]$_})
   $special = ((33, 35, 36, 37, 38, 64) | Get-Random -Count 1 | ForEach-Object {[char]$_})

   <#
       > Sort-Object {Get-Random}
       Sortiert die Einträge der Arrays zufällig.

       > -join
       Kombiniert alle Einträge von den Arrays in eine Zeichenkette
   #>
   $passwort = -join ($letters + $numbers + $special | Sort-Object {Get-Random});

