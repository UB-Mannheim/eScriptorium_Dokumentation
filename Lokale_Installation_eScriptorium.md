# Anleitung zur lokalen Installation von eScriptorium unter Linux bzw. Windows (WSL/Virtual Box)

Die folgende Installationsanleitung basiert auf einer Installation unter Linux
mit den Linux-Distributionen **Ubuntu 20.04.3** oder **Debian 11**.

Unter Windows 10 und 11 stellt das **[Windows Subsystem for Linux](https://docs.microsoft.com/de-de/windows/wsl/install)** (WSL) eine geeignete Linux-Umgebung bereit.
Alternativ kann auch eine Virtualisierungssoftware wie beispielsweise **[Virtual Box](https://www.virtualbox.org/wiki/Downloads)** mit Ubuntu 20.04.3 als Basis genommen werden.

Wenn Sie weitere Informationen oder Hilfe bei der Installation von eScriptorium brauchen, wenden Sie sich gerne an Larissa Will (larissa.will(at)uni-mannheim.de).

Nachdem VirtualBox bzw. die Debian- oder Ubuntu-Umgebung auf dem PC installiert und gestartet wurde,
öffnen Sie mittels eines Rechtsklicks auf den Desktop das **Terminal**.
Wenn Sie WSL nutzen, dann öffnen Sie einfach die installierte Distribution.

Aktualisieren Sie zunächst Ihr Linux mit folgenden Befehlen:
```
sudo apt-get update
sudo apt-get upgrade
```

### 1. Installation relevanter Programme
Zunächst installieren Sie alle Programme, die Sie für die Nutzung bzw. Installation von eScriptorium benötigen.
Dazu gehören Git, NPM, Postgresql-Installationen, der Redis-Server, Werkzeuge von Drittanbietern sowie Python und die virtuelle Umgebung:
```
sudo apt install git postgresql postgresql-contrib libpq-dev redis-server gettext netcat-traditional jpegoptim pngcrush libvips build-essential python3 python3-dev python3-venv npm
```

**Hinweis:** Nach dem ersten sudo-Befehl (sudo wird benutzt, um Prozesse mit den Rechten eines anderen Benutzers (z. B. des Superusers root) zu starten, fordert Sie die Linux-Distribution immer dazu auf, Ihr Passwort einzugeben. Es fragt Sie dann, ob Sie den entsprechenden Speicherplatz für die Installation freigeben möchten.
Im Terminal erscheint dann die Auswahlmöglichkeit: [Y/n]. Durch Betätigung der Enter-Taste wird automatisch die großgeschriebene Auswahl bestätigt, alternativ kann der entsprechende Buchstabe eingegeben und mit Enter bestätigt werden. Dies kann während der Installation öfter auftreten.

OPTIONAL: Falls Fehlermeldungen bei der Postgresql Installation auftauchen:
```
sudo apt update
sudo apt update --fix-missing
sudo apt install postgresql
```

### 2. Start der Server für Postgresql und Redis
```
sudo service postgresql start
sudo service redis-server start
```
OPTIONAL: Der derzeitige Status von Postgresql kann jederzeit mit folgendem Befehl abgefragt werden:
```
sudo service postgresql status
```

### 3. Benutzernamen anlegen
Mit diesem Befehl wird Ihr Linux-Benutzername als eScriptorium-Benutzername gesetzt:
```
(cd /tmp && sudo -u postgres createuser --superuser $(whoami))
```

Wenn Sie einen anderen Namen als Ihren Linux-Nutzernamen wählen möchten, geben Sie ein:
```
sudo -u postgres createuser --superuser <Nutzername>
```
Wobei "Nutzername" dem von Ihnen gewählten Namen entspricht.

### 4. Datenbank für eScriptorium anlegen
```
createdb escriptorium
```

### 5. Repository klonen
Sie klonen nun das Repository von GitLab.
```
git clone https://gitlab.com/scripta/escriptorium.git ~/escriptorium
```

### 6. Verzeichnis wechseln
Nun wechseln Sie in das neu angelegte Verzeichnis *escriptorium*:
```
cd ~/escriptorium
```

### 7. Virtuelle Umgebung
Jetzt erstellen und aktivieren Sie eine virtuelle Umgebung:
```
python3 -m venv env
source env/bin/activate
pip install -U pip setuptools wheel
```
Damit aktualisieren Sie die heruntergeladenen Versionen, dadurch können Fehler später vermieden werden.

Installieren Sie alle notwendigen Python-Pakete:
```
pip install -r app/requirements.txt -r app/requirements-dev.txt
```

### 8. Lokale Einstellungen anlegen
Es gibt eine Beispieldatei für lokale Einstellungen, die hier einfach kopiert wird.
```
cp app/escriptorium/local_settings.py.example app/escriptorium/local_settings.py
```

OPTIONAL: Über folgenden Befehl gelangen Sie in die Einstellungen.
Hier können Veränderungen vorgenommen werden.
Für den Anfang müssen Sie jedoch nichts ändern und können diesen Schritt demnach überspringen.
```
vi app/escriptorium/local_settings.py
```

### 9. NPM installieren
Anschließend wechseln Sie in das Verzeichnis `front` und installieren mit NPM:
```
cd front
# Installiere die Pakete für eScriptorium.
npm install
```

OPTIONAL: Falls Fehlermeldungen erscheinen, dass es Schwachstellen (Vulnerabilities) gibt (vor allem im roten Bereich), dann sollten Sie den folgenden Befehl ausführen:
```
npm audit fix
```
Oft lassen sich so nicht alle Schwachstellen korrigieren.
Für die Installation auf einem Server wäre das ein Sicherheitsrisiko,
aber in einer lokalen Installation ohne Zugang von außen ist es in der Regel unkritisch.

### 10. Produktive Nutzung
Um eScriptorium produktiv zu nutzen (Entwickler:innen wählen besser andere Optionen) führen Sie folgende Befehle aus:
```
npm run production
```

### 11. Installation überprüfen
Führen Sie dafür folgenden Befehl aus:
```
cd ../app
python manage.py check --settings escriptorium.local_settings
```

### 12. SQL-Tabellen
Jetzt erstellen Sie die benötigten SQL-Tabellen in der Datenbank:
```
python manage.py migrate --settings escriptorium.local_settings
```

### 13. Übersetzungen aktualisieren
Unter Umständen müssen noch die Übersetzungen der Benutzeroberfläche (neben den englischen gibt es weitgehend übersetzte deutsche Texte) aktualisiert werden:
```
python manage.py makemessages --all --settings escriptorium.local_settings
python manage.py compilemessages --settings escriptorium.local_settings
```

### 14. OPTIONAL
Nun können Sie noch einen Superuser kreieren
```
python manage.py createsuperuser --settings escriptorium.local_settings
```

### 15. Celery Worker
Starten Sie einen einfachen Celery Worker im Hintergrund aus:
```
DJANGO_SETTINGS_MODULE=escriptorium.local_settings celery -A escriptorium worker -l INFO &
```

### 16. Start des Servers
```
python manage.py runserver --settings escriptorium.local_settings
```

### 17. Nutzung von eScriptorium
Nun können Sie eScriptorium nutzen, geben Sie dafür einfach in Ihren Browser folgenden Link ein: [http://localhost:8000/](http://localhost:8000/)
(Hinweis: Sollten Sie eScriptorium in einer virtuellen Maschine installiert haben, nutzen Sie den Browser darin.)

**Achtung:** eScriptorium erstellt automatisch einen Nutzer mit dem Namen „admin“ und dem Passwort „admin“.
Dies sollten Sie wissen, da auf diese Weise Unbefugte in Ihr System eindringen können,
vor allem wenn Sie Ihre eScriptorium-Installation später auch als Webdienst verfügbar machen.
Ändern Sie das Password oder entfernen Sie diesen Benutzer in diesem Fall.

### 18. Optionale Einstellungen

In der Datei `~/escriptorium/app/local_settings.py` können optional lokale Einstellungen vorgenommen werden.

Mit `DEBUG = False` schaltet man die Anzeige der Debug-Tools (im Webinterface rechts oben) aus.

Die Exportformate OpenITI Markdown und TEI XML lassen sich mit `EXPORT_OPENITI_MARKDOWN_ENABLED = True` bzw. `EXPORT_TEI_XML_ENABLED = True` aktivieren.

Mit `TEXT_ALIGNMENT_ENABLED = True` kann die Textalignierung als zusätzliche Funktionalität aktiviert werden.

`DISABLE_ELASTICSEARCH = False` schaltet die Volltextsuche ein. Dafür sind zusätzliche Einstellungen und die Installation von Elasticsearch erforderlich.

### 19. Erneute Nutzung
Sobald Sie Ihren PC bzw. die virtuelle Maschine neugestartet haben, müssen Sie eScriptorium erneut aktivieren über das Terminal.
```
cd ~/escriptorium
source env/bin/activate
cd app
sudo service postgresql start
sudo service redis-server start
DJANGO_SETTINGS_MODULE=escriptorium.local_settings celery -A escriptorium worker -l INFO &
python manage.py runserver --settings escriptorium.local_settings
```
Browser: [http://localhost:8000/](http://localhost:8000/)

Die Anleitung basiert auf der [GitLab-Dokumentation von Robin Tissot](https://gitlab.com/scripta/escriptorium/-/wikis/full-install).
Jedoch wurden hier einige Veränderungen vorgenommen, um die Installation möglichst einfach zu gestalten und einige Fehler zu beheben.
