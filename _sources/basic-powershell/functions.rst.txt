Funktionen
==========

Oft ist man in der Situation, dass ein bestimmer Codeteil an bestimmten
Stellen immer wieder benötigt wird (z.B. eine komplexere Berechnung).
Diesen Code jedes Mal komplett zu kopieren würde nicht nur viele
unnötige Codezeilen erzeugen, sondern auch die Wartbarkeit erheblich
verringern, da im Falle eines Bugs in diesem Codeteil alle Stellen
gefunden und repariert werden müssen, obwohl es sowieso überall der
gleiche Code ist. Wie sich jetzt leicht vermuten lässt, lösen Funktionen
dieses Problem.

Parameter
---------

In vielen Fällen ist der Code in einer Funktion von zusätzlichen
Eingaben abhängig. Damit nicht für jeden nur erdenklichen Fall dieser
abhängigen Werte eine eigene Funktion geschrieben werden muss, wurden
die sogenannten (Funktions-)parameter eingeführt.

Rückgabewert
------------

Da in den meisten Fällen nicht nur eine bestimmte Prozedur ausgeführt
wird, muss eine Funktion nicht nur Eingaben (über Parameter), sondern
auch Ausgaben erzeugen können. Dazu gibt es die sogenannten
**Rückgabewerte**.

Syntax
------

.. code:: powershell

   function meine_funktion([string]$parameter1, [string]$parameter2) {
       # beide Parameter (Eingaben) kombiniert und in Variable "ergebnis" speichern
       $ergebnis = $parameter1 + $parameter2

       # hier kann nahezu jeder beliebige Code stehen
     
       # Rückgaben werden mit dem "return" Schlüsselwort angegeben
       return $ergebnis
   }
   $rueckgabe = meine_funktion "Hello" "World"
   Write-Host $rueckgabe

   ## oder

   function meine_funktion_zahl([int]$parameter1, [int]$parameter2) {
       # beide Parameter (Eingaben) addiert und in Variable "ergebnis" speichern
       $ergebnis = $parameter1 + $parameter2

       # hier kann nahezu jeder beliebige Code stehen
     
       # Rückgaben werden mit dem "return" Schlüsselwort angegeben
       return $ergebnis
   }

   $rueckgabe = meine_funktion_zahl 2 3
   Write-Host $rueckgabe

Funktionen werden mit dem Schlüsselwort function eingeleitet, direkt
gefolgt vom Namen der Funktion. Danach folgen in runden Klammern die
Namen der Parameter. Die Parameter verhalten sich innerhalb der Funktion
genauso wie lokale Variablen. Schließlich wird mit dem Schlüsselwort
return die lokale Variable ergebnis zurückgegeben.

Der Aufruf der Funktion sollte dir von der Funktion print bekannt
vorkommen, die uns schon die ganze Zeit begleitet hat. Hier wird ganz
intuitiv der Name der Funktion, gefolgt von runden Klammern, zwischen
denen sich die Eingaben/Parameter der Funktion befinden, geschrieben.
Dabei können natürlich sowohl Variablen als auch direkt Werte (Literale)
übergeben werden.
