Kontrollstrukturen
==================

Bisher haben wir nur Variablen definiert und auf der Konsole ausgegeben.
Damit lässt sich natürlich noch nicht viel machen; vor allem, weil wir
nicht in der Lage sind Fallunterscheidungen zu machen oder bestimmte
Codeteile zu wiederholen.

if-Bedingung
------------

Jeder, der schonmal etwas mit Programmierung zu tun hatte kennt sie: Die
if-Bedingung. Mit der if-Bedingung/-Verzweigung lässt ein bestimmter
Codeteil ausführen, wenn eine Bedingung wahr (oder nicht wahr) ist.

So kann mit if-Bedingungen z.B. geprüft werden, ob eine vorher
definierte Variable einen bestimmten Wert hat und wenn dies der Fall
ist, wird etwas auf der Konsole ausgegeben:

.. code:: powershell

   # Irgendwas definieren
   $irgendwas = 5

   # Jetzt mit der if-Bedingung prüfen, ob irgendwas den Wert 5 hat
   if ($irgendwas -eq 5) {
       Write-Host "Die Variable irgendwas hat den Wert 5"
   }

   # Eine andere Bedingung, die womöglich? nicht wahr ist
   if ($irgendwas -eq 42) then
       Write-Host "Die Variable hat den Wert 42"
   end

   # Natürlich muss man die Variable nicht mit einem Literal vergleichen,
   # sondern kann sie auch mit einer anderen Variablen vergleichen
   $andere_variable = $irgendwas # Wert von '$irgendwas' der Variable '$andere_variable' zuweisen

   if ($andere_variable -eq $irgendwas) {
       Write-Host "irgendwas und andere_variable haben denselben Wert!"
   }

Wie hoffentlich durch das Beispiel klar geworden ist, steht nach dem
``if`` in Klammern ``( )`` die Bedingung und zwischen dem ``{`` und dem
``}`` der Code, der ausgeführt wird, wenn die Bedingung wahr (``true``)
ist.

Bei Vergleichen muss **immer** der ``-eq``-Operator verwendet werden.

Vergleichsoperatoren
--------------------

+-----------------------------------+-----------------------------------+
| Vergleichsoperator                | Beschreibung                      |
+===================================+===================================+
| a ``-eq`` b                       | Prüft a und b auf Gleichheit,     |
|                                   | **true** falls gleich, **false**  |
|                                   | andernfalls                       |
+-----------------------------------+-----------------------------------+
| a ``-ne`` b                       | Prüft a und b auf Ungleichheit    |
+-----------------------------------+-----------------------------------+
| a ``-gt`` b                       | Wahr, wenn a (echt) kleiner als b |
|                                   | ist                               |
+-----------------------------------+-----------------------------------+
| a ``-ge`` b                       | Wahr, wenn a kleiner oder gleich  |
|                                   | b ist                             |
+-----------------------------------+-----------------------------------+
| a ``-lt`` b                       | Wahr, wenn a (echt) größer als b  |
|                                   | ist                               |
+-----------------------------------+-----------------------------------+
| a ``-le`` b                       | Wahr, wenn a größer oder gleich b |
|                                   | ist                               |
+-----------------------------------+-----------------------------------+

Logische Junktoren
------------------

Es reicht meistens nicht nur eine einzelne Sachen abzufragen. Man möchte
oft mehrere einzelne Abfragen miteinander verknüpfen.

+-----------------------------------+-----------------------------------+
| Junktor                           | Beschreibung                      |
+===================================+===================================+
| a ``-and`` b                      | Prüft, ob wohl a **als auch** b   |
|                                   | wahr sind                         |
+-----------------------------------+-----------------------------------+
| a ``-or`` b                       | Prüft a oder b wahr ist           |
+-----------------------------------+-----------------------------------+
| ``-not`` a                        | Negiert a, d.h. ``true`` wird zu  |
|                                   | ``false`` und ``false`` zu        |
|                                   | ``true``                          |
+-----------------------------------+-----------------------------------+

Folgendes Beispiel überprüft, ob sowohl a den Wert 2 als auch b den Wert
3 hat

.. code:: powershell

   # a und b definieren
   $a = 2
   $b = 4
   # erster Ausdruck wird wahr sein, zweiter nicht
   if ($a -eq 2 -and $b -eq 3) { 
       Write-Host "a ist 2 und b ist 3"
   } else {
       Write-Host "Gilt nicht"
   }

if-else
-------

Für if gibt es noch eine kleine Erweiterung: Den else-Block. Dieser
Block wird ausgeführt, wenn die Bedingung zwischen ``if`` und ``then``
**nicht**\ \_ nicht wahr ist. // TODO: Add elseif

.. code:: powershell

   $irgendwas = 1337

   if ($irgendwas == 42) {
       Write-Host "irgendwas riecht nach dem Sinn des Lebens"
   } else {
       Write-Host "Nein, Leetspeak ist besser"
   }

while-Schleife
--------------

Die wohl wichtigste, aber nicht am meisten verwendet Schleife ist die
**while**-Schleife. Sie führt einen Codeteil (= Block) so lange aus wie
eine Bedingung wahr ist.

.. code:: powershell

   # Zähler definieren
   $mein_zaehler = 1

   # Schleife so lange ausführen wie der Zähler kleiner als 5 ist
   while ($mein_zaehler -lt 5) {
       # Zähler ausgeben
       Write-Host $mein_zaehler

       # Zähler erhöhen (= inkrementieren)
       $mein_zaehler = $mein_zaehler + 1
   }

Achte immer darauf, dass eine Bedingung auch eintritt, ansonsten
verharrt das Skript in einer sog. Endlosschleife und kommt (theoretisch)
nie zum Ende.

Mit einer while-Schleife lassen sich alle anderen Schleifentypen
nachbauen, jedoch erlauben andere Schleifentypen in vielen Fällen eine
kürzere und elegantere Lösung.

do-while-Schleife
-----------------

Die do-while Schleife unterscheidet sich von der ``while`` dadurch das
sie immer das erste Mal ausgeführt wird und zum wiederholen die
Bedingung geprüft wird.

.. code:: powershell

   # Zähler definieren
   $mein_zaehler = 1

   # Schleife so lange ausführen wie der Zähler kleiner als 5 ist
   do {
       # Zähler ausgeben
       Write-Host $mein_zaehler

       # Zähler erhöhen (= inkrementieren)
       $mein_zaehler = $mein_zaehler + 1
   } while ($mein_zaehler -lt 5)

for-Schleife
------------

Die for-Schleife ist mit guten Grund die weitverwendetste Schleife.

.. code:: powershell

   # Einen Zähler von 1 bis 4 laufen lassen
   for ($mein_zaehler = 1; $mein_zaehler -le 4; $mein_zaehler++) {
       Write-Host $mein_zaehler
   }

   # alternativ kann auch die Schrittgröße beim Hochzählen angegeben werden
   # (negative Schritte sind ebenfalls möglich)
   Write-Host "" # leere Zeile ausgeben
   for ($mein_zaehler = 1; $mein_zaehler -le 3; $mein_zaehler += 0.5) {
       Write-Host $mein_zaehler
   }

foreach-Schleife
----------------

Mit der foreach-Schleife kann man sehr einfach mit Arrays arbeiten.

.. code:: powershell

   $zahlen = (1..10)

   # Das Programm geht durch alle Zahlen, multipliziert diese und gibt es aus.
   # Es wird immer ein Wert aus dem Array genommen und in die Variable $zahl geschrieben
   foreach ($zahl in $zahlen) {
       Write-Host $zahl * 2
   }

   $processes = Get-Process # Lädt alle laufende Prozesse in eine Variable
   foreach ($process in $processes) {
       # Gibt die Namen der Prozesse aus
       Write-Host $process.Name
   }

   $processes = Get-Process

   $processes | ForEach-Object { Write-Host $_.Name }

ForEach-Object
--------------

Mit dem ``ForEach-Object`` funktioniert gleich wie die ``foreach`` und
wird über Piping verwendet.

.. code:: powershell

   $processes = Get-Process
   $processes | ForEach-Object { Write-Host $_.Name }

break - Schleife abbrechen
--------------------------

Alle Schleifen können wie folgt mit dem Schlüssekwort ``break``
abgebrochen werden.

.. code:: powershell

   for ($i = 0; $i -le 10; $i++) {
       Write-Host $i
       if ($i -eq 5) {
           break
       }
   }

Übung
-----

Teil 1: Verständnisfragen
~~~~~~~~~~~~~~~~~~~~~~~~~

Im ersten Teil der Übung sollen Verständnisfragen beantwortet werden.

1. Was ist der Unterschied zwischen einer if-Bedingung und einer
   Schleife?
2. Was ist der Unterschied zwischen einer for- und while Schleife?
3. Kann man mit einem Schleifentyp allen anderen Typen darstellen? Falls
   ja, mit welcher zum Beispiel?

Lösung
^^^^^^

1. Eine if-Bedingung prüft nur **einmalig** die Bedingung, wohingegen
   eine Schleife eine Bedingung überprüft und dann einen Vorgang z.B.
   bis zum Eintreten der Bedingung wiederholt
2. Eine for-Schleife verwendet immer einen Zähler und zählt bis zum
   Erreichen eines festgelegten Wertes. Eine while-Schleife führt Code
   so lange aus bis eine Bedingung nicht mehr eintritt
3. Ja, z.B. mit der while-Schleife lassen sich alle anderen Schleifen
   darstellen (siehe Teil 2)

Teil 2: Umformen zwischen Schleifentypen
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Wie in *Teil 1* schon angekündigt wurde lassen sich alle Schleifentypen
ineinander mehr oder weniger problemlos überführen (wobei die
for-Schleife einen Sonderfall darstellt)

In dieser Aufgabe soll nun folgende while-Schleife jeweils in eine
do-while Schleife und for-Schleife überführt werden:

.. code:: powershell

   $i = 50
   while ($i -ne -10) {
       $i = $i - 2
       Write-Host $i
   }

.. code:: powershell

   ## do-while
   $i = 50
   do {
       $i = $i - 2
       Write-Host $i
   } while ($i -ne -10)

   # for
   for ($i = 50-2; $i -ne -12; $i -= 2) {
       Write-Host $i
   }

