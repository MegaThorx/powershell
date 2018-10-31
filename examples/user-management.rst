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
    $users = Import-Csv -Delimiter ";" -Encoding Default "users.csv"

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
    $users = Import-Csv -Delimiter ";" -Encoding Default "users.csv"

    # Fügt das Feld Username zu den Objekten im Array hinzu
    $users | Add-Member Username ""

    
    foreach ($user in $users) {
        $firstname_count = 0 # wird mit 0 initialisiert da es bei der Schleife direkt erhöht wird
        $zahl = 0

        # Im ersten Schritt werden alle Zeichen in Kleinbuchstaben umgewandelt und dann alle Zeichen welche im Benutzernamen nicht zulässig sind entfernt
        # hierfür wird .Replace() verwendet
        $firstname = $user.Vorname.ToLower().Replace("ä", "ae").Replace("ö", "oe").Replace("ü", "ue").Replace("ß", "ss")
        $lastname = $user.Nachname.ToLower().Replace("ä", "ae").Replace("ö", "oe").Replace("ü", "ue").Replace("ß", "ss")


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

Aufgabe 3
~~~~~~~~~

Generiere nun zusätzlich für jeden Benutzer ein Passwort und speichere es anschließend in eine CSV zurück.

Lösung
------

.. code:: powershell

    # -Delimiter ";" - um den trenner zwischen den Daten in einer Zeile festzulegen
    # -Encoding Default - damit die Datei als Windows 1251 geöffnet wird (Zeichenkodierung)
    $users = Import-Csv -Delimiter ";" -Encoding Default "users.csv"

    # Fügt das Feld Username zu den Objekten im Array hinzu
    $users | Add-Member Username ""
    $users | Add-Member Password ""

    
    foreach ($user in $users) {
        $firstname_count = 0 # wird mit 0 initialisiert da es bei der Schleife direkt erhöht wird
        $zahl = 0

        # Im ersten Schritt werden alle Zeichen in Kleinbuchstaben umgewandelt und dann alle Zeichen welche im Benutzernamen nicht zulässig sind entfernt
        # hierfür wird .Replace() verwendet
        $firstname = $user.Vorname.ToLower().Replace("ä", "ae").Replace("ö", "oe").Replace("ü", "ue").Replace("ß", "ss")
        $lastname = $user.Nachname.ToLower().Replace("ä", "ae").Replace("ö", "oe").Replace("ü", "ue").Replace("ß", "ss")


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

        # Dieser Teil ist vom Beispiel "Passwort generieren"
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
        $user.password = -join ($letters + $numbers + $special | Sort-Object {Get-Random});
    }

    # -Delimiter ";" - um den trenner zwischen den Daten in einer Zeile festzulegen
    # -Encoding Default - damit die Datei als Windows 1251 geöffnet wird (Zeichenkodierung)
    $users | Export-Csv -Path "users_with_password.csv" -NoTypeInformation -Delimiter ";" -Encoding Default

Aufgabe 4
~~~~~~~~~

User im ActiveDirectory erstellen mit OUs für jede Abteilung.
Für dieses Beispiel wird die CSV welche beim Aufgabe 3 erstellt wurde weiterverwendet.

.. code::

    "Abteilung";"Nachname";"Vorname";"Username";"Password"
    "Einkauf";"Schreiber";"Florian";"fschreiber";"hB75&cfL"
    "Einkauf";"Bayer";"Maik";"mbayer";"&w6ZUM5L"
    "Einkauf";"Schweitzer";"Michelle";"mschweitzer";"&M7ep9PR"
    "Einkauf";"Schweitzer";"Marco";"maschweitzer";"0M3%qpNb"
    "Verkauf";"Seiler";"Barbara";"bseiler";"0BXeQ7!k"
    "Verkauf";"Amsel";"Anne";"aamsel";"3WXhQ!M2"
    "Verkauf";"Moeller";"Stefanie";"smoeller";"qF7P6!ED"
    "Verkauf";"Moeller";"Sven";"svmoeller";"W13Cv!Pq"
    "Verkauf";"Moeller";"Stefan";"stmoeller";"aN%36vwh"

Lösung
------

.. code:: powershell

    # -Delimiter ";" - um den trenner zwischen den Daten in einer Zeile festzulegen
    # -Encoding Default - damit die Datei als Windows 1251 geöffnet wird (Zeichenkodierung)
    $allusers = Import-Csv -Delimiter ";" -Encoding Default "users_with_password.csv"

    # Ermittelt alle eindeutigen Abteilungen
    $abteilungen = $allusers.Abteilung | Get-Unique

    foreach ($abteilung in $abteilungen) {
        # Domäne ist TEST.AT und die User sollen in TEST\Users abgelegt werden
        # der Pfad zur richtigen OU wird rückwärts angegeben
        $path = "OU=Users,OU=TEST,DC=test,DC=at"

        $filter = 'Name -eq "' + $abteilung + '"'

        # Versucht das OU Objekt für die Abteilung zu bekommen
        # falls dies fehlschlägt ist in $org kein Wert
        $org = Get-ADOrganizationalUnit -Filter $filter -SearchBase $path

        # Wenn die OU noch nicht vorhanen ist wird diese mit dem Befehl erstellt
        if (-Not $org) {
            New-ADOrganizationalUnit -Name $abteilung -Path $path -ProtectedFromAccidentalDeletion $False
        }
        
        # Fügt die neue OU zum Pfad hinzu
        $path = "OU=" + $abteilung + "," + $path

        # Ermittelt alle User mit der gegeben Abteilung
        $users = $allusers | Where-Object {$_.Abteilung -eq $abteilung}

        foreach ($user in $users) {
            # Mit ConverTo-SecureString wird das Passwort gehashed, da bei New-AdUser kein klartext Passwort zulässig ist.
            $password = $user.Password | ConvertTo-SecureString -AsPlainText -Force
            
            # Erstellt den AdUser
            # -Name - Username
            # -AccountPassword - das gehashte Passwort
            # -ChangePasswordAtLogon - das der User beim Login das Passwort ändern muss
            # -GivenName - Vorname
            # -Surname - Nachname
            # -Path - Pfad im AD
            # -Enable - Ob der Account aktiviert werden soll
            New-AdUser -Name $user.Username -AccountPassword $password -ChangePasswordAtLogon $True -GivenName $user.Vorname -Surname $user.Nachname -Path $path -Enabled $True
        }
    }