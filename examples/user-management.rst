Userverwaltung
==============

In diesem Tutorial erstellen wir eine Userverwaltung.

Erstelle eine neue Datei mit dem folgenden Inhalt und speichere diese als **.csv** ab.

.. code::

    Abteilung;Nachname;Vorname
    Einkauf;Schreiber;Florian
    Einkauf;Bayer;Maik
    Einkauf;Schweitzer;Michelle
    Einkauf;Schweitzer;Marco
    Verkauf;Seiler;Barbara
    Verkauf;Amsel;Anne
    Verkauf;Moeller;Stefanie
    Verkauf;Moeller;Sven
    Verkauf;Moeller;Stefan

Aufgabe 1
~~~~~~~~~

Lade die CSV mit dem Befehl ``Import-Csv`` und gib die Länge der Liste aus.
Zusätzlich gebe jeden Nachname aus (keine duplikate).

Lösung
------

.. code:: powershell
    # -Delimiter ";" - um den trenner zwischen den Daten in einer Zeile festzulegen
    # -Encoding Default - damit die Datei als Windows 1251 geöffnet wird (Zeichenkodierung)
    $users = Import-Csv -Delimiter ";" -Encoding Default  $file

    # $users.length gibt die Länge des Arrays zurück
    Write-Host "Es gibt " $users.length " User"

    # Mit $users.Nachname wird ein neuer Array erzeugt in welchem nur die Nachname sind
    # Dabei exisiteren aber noch die Duplikate
    $lastnames = $users.Nachname

    # Mit diesem Befehl kann ich nun die eindeutigen Nachnamen ermitteln
    $lastnames = $lastnames | Get-Unique

    Write-Host $lastnames


Aufgabe 2
~~~~~~~~~

Generiere die Benutzernamen für alle Benutzer.

Dabei gibt es die folgenden Reglen:
- keine Duplikate
- erstes Zeichen von Vorname + Nachname
- falls dies nicht möglich ist zwei Zeichen usw..
- falls dies nicht geht soll eine Zahl zwischen dem ganzen Vor- und Nachname eingefügt werden.


Lösung
------

.. code:: powershell
    # -Delimiter ";" - um den trenner zwischen den Daten in einer Zeile festzulegen
    # -Encoding Default - damit die Datei als Windows 1251 geöffnet wird (Zeichenkodierung)
    $users = Import-Csv -Delimiter ";" -Encoding Default  $file

    # Fügt das Feld Username zu den Objekten im Array hinzu
    $users | Add-Member Username ""

    
    foreach ($user in $users) {
        $firstname_count = 0 # wird mit 0 initialisiert da es bei der Schleife direkt erhöht wird
        $zahl = 0

        # Im ersten Schritt werden alle Zeichen in Kleinbuchstaben umgewandelt und dann alle Zeichen welche im Benutzernamen nicht zulässig sind entfernt
        # hierfür wird .Replace() verwendet
        $firstname = $user.Firstname.ToLower().Replace("ä", "ae").Replace("ö", "oe").Replace("ü", "ue").Replace("ß", "ss")
        $lastname = $user.Lastname.ToLower().Replace("ä", "ae").Replace("ö", "oe").Replace("ü", "ue").Replace("ß", "ss")


        do {
            # Erhöht die Anzahl der Zeichen vom Vornamen
            $firstname_count++
            
            # Prüft ob die Anzahl der Zeichen vom Vornamen größer ist als die Länge des Vornamens
            # falls ja dann wird probiert eine Zahl zwischen Vorname und Nachname einzufügen
            if ($firstname_count -gt $firstname.length) {
                $zahl++
                $username = $firstname + $zahl + $lastname
            } else {
                # $firstname.Substring(0, X) gibt die Zeichen bis X
                # Wenn X gleich 1 ist gibt es das erste Zeichen zurück
                # Wenn X gleich 2 ist gibt es die ersten zwei Zeichen zurück
                $username = $firstname.Substring(0, $firstname_count) + $lastname
            }
            # $users.Username erstellt wieder einen Array mit allen Benutzernamen
            # mit -contains wird geprüft ob der Name in diesem Array existiert
            # dadurch wird die Schleife solange wiederholt bis ein Benutzername frei ist
        } while ($users.Username -contains $username)

        # Setzt den Benutzernamen beim Objekt
        $user.Username = $username
    }

    # Gibt alle User aus
    Write-Host $users
