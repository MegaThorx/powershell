Variablen und Datentypen
========================

Variablen sollten für die meisten aus der Mathematik bereits bekannt sein. In der Programmierung lässt sich eine Variable als Platzhalter für einen bestimmten Inhalt sehen.

So lässt sich sagen: Eine Variable ordnet einem **Wert** einen **Namen** zu.

Literale
--------

Literale sind feste Werte, die direkt - so wie sie sind - im Code stehen.

.. code:: powershell

    Write-Host 4
    Write-Host "Hi"

Sowohl ``4`` als auch ``"Hi"`` sind hier Literale.

Variablennamen
--------------

Damit der Powershell Interpreter (das Programm, das den Powershell Code ausführt) Variablen auch als solche identifizieren kann, muss man sich an bestimmte Regeln halten.

Ein Variable beginnt mit einem ``$`` Zeichen.

Der Name darf...
* ...nur aus alphanumerischen Zeichen (= Buchstaben und Zahlen) bestehen (Sonderzeichen und Umlaute sind jedoch nicht erlaubt)
* ...nicht mit einer Zahl anfangen (muss also mit einem Buchstaben anfangen)

Dabei ist zu beachten das die Groß-/Kleinschreibung von Powershell bei Variablennamen vernachlässigt wird.

Des Weiteren ist es sinnvoll sich an bestimmte Namenskonventionen zu halten, damit der Code auch von anderen Entwicklern möglichst schnell verstanden werden kann. Der wichtigste Punkt ist, dass du deinen Variablen eindeutige und selbsterklärende Namen geben solltest. Weiterhin solltest du überlegen, ob sich später vielleicht Personen aus dem internationalen Raum anschließen und dann typischerweise mit einer englischen Namensgebung und Kommentaren arbeiten.

Datentypen
----------

Variablen in Powershell sind grundsätzlich *dynamisch typisiert*. Das bedeutet, dass eine Variable jeden beliebigen Typ annehmen und diesen wechseln kann, wenn diese nicht mit einem Typ initalisiert wurden.
Das macht Powershell gerade auch für Anfänger besonders attraktiv, da es dadurch besonders einfach wird.

Beim Schreiben von Powershell Code muss lediglich die Syntax der Defintion von Literalen bekannt sein.

Beispiel
--------

.. code:: powershell

    $zahl = 1
    Write-Host $zahl

    $zahl = "Test"
    Write-Host $zahl

Das Beispielprogramm gibt erst die Zahl ``1`` aus und anschließend den Text ``Test``

.. code:: powershell

    [int]$zahl = 1
    Write-Host $zahl

    $zahl = "Test"
    Write-Host $zahl

Das Beispielprogramm gibt erst die Zahl ``1`` aus und wird beim zuweisen des Textes scheitern, da die Variable ``$zahl`` typisiert ist.`

Zahlen
~~~~~~

Je nach Art der Zahl gibt es zwei Datentypen für Zahlen in Powershell. Für Ganzzahlen (Zahlen ohne Dezimalstellen) sollte man `int` verwenden. Für Zahlen mit Dezimalen gibt es dann die Datentypen ``single``, ``double`` und ``decimal``, welche sich bei der maximalen Größe der Zahl unterscheiden.

Dezimalzahlen (also Zahlen mit Komma) müssen statt eines Dezimalkommas jedoch einen Dezimalpunkt verwenden.

int
^^^

-  Wertebereich: 2147483647 bis -2147483648
-  Größe: 4 Bytes

single
^^^^^^

-  Wertebereich: 3.402823E+38 bis -3.402823E+38
-  Größe: 4 Bytes
-  Anzahl an Dezimalen: 7

double
^^^^^^

-  Wertebereich: 1.79769313486232E+308 bis -1.79769313486232E+308
-  Größe: 8 Bytes
-  Anzahl an Dezimalen: 15-16

decimal
^^^^^^^

-  Wertebereich: 79228162514264337593543950335 bis -79228162514264337593543950335
-  Größe: 16 Bytes
-  Anzahl an Dezimalen: 28-29


Beispiele
^^^^^^^^^

Zahlen können ganz einfach wie folgt definiert werden:

.. code:: powershell

    [int]$meine_zahl = 42 # ganze Zahl
    Write-Host $meine_zahl
    [decimal]$meine_zahl_decimal = 13.37 # Dezimalzahl mit Dezimalpunkt

An diesem Beispiel lässt sich sehen, wie eine Variable als Platzhalter eingesetzt werden kann.

Strings / Zeichenketten
~~~~~~~~~~~~~~~~~~~~~~~

Zeichenketten, also beliebige Aneinanderreihungen von Zeichen, in der Programmierung auch **Strings** genannt, müssen zwischen Anführungszeichen gestellt werden.

.. code:: powershell

    $meine_zeichenkette = "Hallo Welt!"

Array
~~~~~

Ein Array speichert mehrere Werte, ähnlich einer 2 spaltigen Tabelle.

.. code:: powershell

    $array = ("Wert 1", "Wert 2", "Wert 3") # Erstellen eines Arrays

    Write-Host $array[2] # Gibt "Wert 3" aus

+-------+--------+
| Index | Wert   |
+=======+========+
| 0     | Wert 1 |
+-------+--------+
| 1     | Wert 2 |
+-------+--------+
| 2     | Wert 3 |
+-------+--------+

Dabei ist zu beachten das die Nummerierung der Einträge **bei 0 beginnt!**

Man kann auch einen Wert zu einem bestehenden Array mittels der ``+=`` Operation hinzufügen.

.. code:: powershell

    $array = ("Wert 1", "Wert 2", "Wert 3") # Array mit 3 Werten definieren

    $array += "Wert 4" # Eintrage hinzufügen

Wenn man jetzt schnell die Zahlen 1 bis 10 als einen Array erstellen möchte gibt es ``..`` Operator.

.. code:: powershell

    $array = (1..10) # Array mit Zahlen von 1 bis 10 erstellen

Übung
-----

Teil 1
~~~~~~
Aufgabe dieser Übung ist das Definieren von 4 Variablen (die Namen der
Variablen können frei gewählt werden, wenn nicht anders angegeben)

1. Eine Variable soll mit der **ganzen Zahl** ``-5`` initialisiert
   werden
2. Variable mit dem **Fließkommawert** ``42.1337``
3. Variable mit dem **String** ``Mein Name ist Fritz``
4. Variable 4 soll Variable 2 zugewiesen werden und den Namen
   ``letzte_variable`` tragen

Im Anschluss sollen alle 4 Variablen in der angeführten Reihenfolge ausgegeben werden.

Lösung
^^^^^^

.. code:: powershell

   # Variablen definieren
   $variable1 = -5
   $variable2 = 42.1337
   $variable3 = "Mein Name ist Fritz" # auf Anführungszeichen achten!
   $letzte_variable = $variable2

   # Variablen ausgeben
   Write-Host $variable1 $variable2 $variable3 $letzte_variable

Teil 2
~~~~~~

Welche der folgenden Variablen sind **keine** gültigen
   Variablennamen?

-  ``$variable1``
-  ``$1variable``
-  ``$fritz``
-  ``fritz``
-  ``$__``
-  ``$--``

Lösung
^^^^^^

-  ``$1variable``, weil eine Zahl am Anfang ist
-  ``fritz``, weil die Variable mit ``$`` beginnen muss
-  ``$--`` nicht erlaubtes Zeichen

Teil 3
~~~~~~

Erstelle einen Array mit den Zahlen 1 bis 100.

Lösung
^^^^^^

.. code:: powershell

   $array = (1..100)