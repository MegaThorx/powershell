String Manipulation
===================

Kombinieren von Strings
-----------------------

Natürlich lassen sich mehrere Strings auch zu einem gesamten String
vereinigen. Dies wird auch Konkatenation genannt. Ob es sich dabei um
einen String oder ein Stringliteral handelt, spielt keine Rolle. Die
Konkatenation lässt sich mithilfe des ``+``-Operators durchführen:

.. code:: powershell

   $text1 = "Hallo"
   $text2 = "World"
   $text_neu = $text1 + " " + $text2

.ToUpper()
----------

Wandelt einen String in Großbuchstaben um.

.. code:: powershell

   $text = "Hallo"
   $text.ToUpper() # aus Hallo wird HALLO
   # oder
   ("Hallo").ToUpper() # aus Hallo wird HALLO

.ToLower()
----------

Wandelt einen String in Kleinbuchstaben um.

.. code:: powershell

   $text = "Hallo"
   $text.ToLower() # aus Hallo wird hallo

.Contains(Text)
---------------

Prüft ob ein String einen bestimmte Zeichenkette enthält.

.. code:: powershell

   $text = "Hallo"
   $text.Contains("a") # Gibt Wahr zurück
   $text.Contains("c") # Gibt Falsch zurück

.StartsWith(Text)
-----------------

Prüft ob ein String mit bestimmte Zeichenkette beginnt.

.. code:: powershell

   $text = "Hallo"
   $text.StartsWith("Ha") # Gibt Wahr zurück
   $text.StartsWith("al") # Gibt Falsch zurück

.EndsWith(Text)
---------------

Prüft ob ein String mit bestimmte Zeichenkette endet.

.. code:: powershell

   $text = "Hallo"
   $text.StartsWith("lo") # Gibt Wahr zurück
   $text.StartsWith("ll") # Gibt Falsch zurück

.Replace(AlterText, NeuerText)
------------------------------

Ersetzt eine bestimmte Zeichenkette in einem String mit einer anderen
String.

.. code:: powershell

   $text = "Hallo"
   $text.Replace("Hallo", "World") # Hallo wird mit World ersetzt

   ####

   $text = "Test"
   $text.Replace("es", "se") # Der neue Wert ist `Tset`

.SubString(StartIndex, Länge)
-----------------------------

Mit SubString kann man einen Teil eines Strings anhand der Position
entfernen

.. code:: powershell

   $text = "Hallo"
   $text.SubString(2) # Entfernt die ersten zwei Zeichen 'llo'
   $text.SubString(0, 2) # Gibt zwei Zeichen ab dem ersten Zeichen aus 'Ha'

.TrimStart(ZeichenZumEntfernen)
-------------------------------

Ersetzt eine bestimmte Zeichenkette am Anfang des Textes.

.. code:: powershell

   $text = "    Hallo"
   $text.TrimStart(" ") # Entfernt alle Leerzeichen am Anfang des Stringes

.TrimEnd(ZeichenZumEntfernen)
-----------------------------

Ersetzt eine bestimmte Zeichenkette am Ende des Textes.

.. code:: powershell

   $text = "Hallo------"
   $text.TrimStart("-") # Entfernt alle - am Ende des Stringes

