# Anleitung zur lokalen Installation von eScriptorium unter Linux bzw. Windows (WSL/Virtual Box)

Die folgende Installationsanleitung basiert auf einer Installation unter Windows über **[Windows Subsystem for Linux](https://docs.microsoft.com/de-de/windows/wsl/install)** (WSL) mit den Distributionen **Ubuntu 20.04.3** und **Debian 11** oder der Installation über **[Virtual Box](https://www.virtualbox.org/wiki/Downloads)** mit Ubuntu 20.04.3. Wenn Sie weitere Informationen oder Hilfe bei der Installation dieser Anwendungen brauchen, wenden Sie sich gerne an Larissa Will (larissa.will(at)uni-mannheim.de).
Nachdem die Virtual Box bzw. die Debian- oder Ubuntu-Umgebung auf dem PC installiert und gestartet wurde,
öffnen Sie mittels eines Rechtsklicks auf den Desktop das **Terminal**.
Wenn Sie WSL nutzen, dann öffnen Sie einfach die installierte Distribution.

Aktualisieren Sie zunächst ihr Linux mit folgenden Befehlen, damit können Sie im Folgenden Fehlermeldungen vorbeugen:
```
sudo apt-get update
sudo apt-get upgrade
```

### 1. Installation relevanter Programme
Zunächst installieren Sie alle Programme, die Sie für die Nutzung bzw. Installation von eScriptorium benötigen.
Dazu gehören Git, NPM, Postgresql-Installationen, der Redis-Server, Werkzeuge von Drittanbietern sowie Python und die virtuelle Umgebung:
```
sudo apt install git postgresql postgresql-contrib libpq-dev redis-server netcat-traditional jpegoptim pngcrush libvips build-essential python3 python3-dev python3-venv npm
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
service postgresql status
```

### 3. Benutzernamen anlegen
Mit diesem Befehl wird Ihr Linux-Benutzername als eScriptorium-Benutzername gesetzt:
```
sudo -u postgres createuser --superuser $USER
```
Eventuell wird dabei eine Fehlermeldung angezeigt, die Sie aber ignorieren können.

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
git clone https://gitlab.com/scripta/escriptorium.git
```

### 6. Verzeichnis wechseln
Nun wechseln Sie in das neu angelegte Verzeichnis *escriptorium*:
```
cd escriptorium
```

### 7. Virtuelle Umgebung
Jetzt erstellen und aktivieren Sie eine virtuelle Umgebung:
```
python3 -m venv env
source env/bin/activate
# setuptools-67.6.1 funktioniert nicht mit oitei~=1.0.0.
pip install -U pip "setuptools<67" wheel
```
Damit aktualisieren Sie die heruntergeladenen Versionen, dadurch können Fehler später vermieden werden.
```
pip install -r app/requirements.txt
```
OPTIONAL: Falls hierbei eine Fehlermeldung angezeigt wird, öffnen Sie bitte die Einstellungen und ändern folgende Angaben:
```
vi app/requirements.txt
```

- Ändern Sie bei **psycopg** die Versionsangabe zu `psycopg2-binary~=2.8.6` (Bei neueren Versionen würde folgende Fehlermeldung erscheinen: „Database section isn’t set to UTC“)
- bei **scikit-image**, **scipy** sowie bei **scikit-learn** löschen Sie die Versionsangaben
- **Hinweis:** Innerhalb des VI-Editors aktivieren Sie mit der Taste `i` Sie den „Insert-Mode“ mit der Taste, danach können Sie wie gewohnt schreiben. Um den Eingabemodus wieder zu verlassen, drücken Sie die Escape-Taste. Wenn Ihre Eingabe beendet ist, verlassen Sie die Settings mittels `:x`, insofern Sie die Änderungen speichern möchten. Möchten Sie eine Änderung nicht speichern, geben Sie `:q` ein.

Anschließend müssen Sie den vorherigen Befehl noch einmal ausführen.

Nun geben Sie folgenden Befehl ein:
```
pip install -r app/requirements-dev.txt
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
# Aktualisiere npm (vorinstallierte Version ist meist veraltet).
sudo npm install -g n
sudo n latest
# Vergiss das alte npm, damit das neue npm verwendet wird.
hash -r
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

### 10. Eingabe
```
export DJANGO_SETTINGS_MODULE=escriptorium.local_settings
```

### 11. Installation überprüfen
Führen Sie dafür folgenden Befehl aus:
```
cd ../app
python manage.py check
```

### 12. SQL-Tabelle
Jetzt erstellen Sie eine SQL-Tabelle im Ordner *app*:
```
python manage.py migrate
```
Bei aktuellen Versionen von eScriptorium wird dabei eine Fehlermeldung angezeigt, die man ignoriert.

### 13. OPTIONAL
Nun können Sie noch einen Superuser kreieren
```
python manage.py createsuperuser
```

### 14. Celery Worker
Öffnen Sie ein neues Terminal und führen Sie einen einfachen Celery Worker aus:
```
celery -A escriptorium worker -l INFO &
```

Bestätigen Sie mit Enter. Mittels dieses Befehls läuft Celery direkt im Hintergrund und Sie können fortfahren.

### 15. Start des Servers
```
python manage.py runserver
```

### 16. Nutzung von eScriptorium
Nun können Sie eScriptorium nutzen, geben Sie dafür einfach in Ihren Browser folgenden Link ein: http://localhost:8000/
(Hinweis: Sollten Sie eScriptorium in einer virtuellen Maschine installiert haben, nutzen Sie den Browser darin.)

### 17. Erneute Nutzung
Sobald Sie Ihren PC bzw. die virtuelle Maschine neugestartet haben, müssen Sie eScriptorium erneut aktivieren über das Terminal.
```
cd escriptorium
source env/bin/activate
cd app
sudo service postgresql start
sudo service redis-server start
celery -A escriptorium worker -l INFO &
python manage.py runserver
```
Browser: http://localhost:8000

**Achtung:** eScriptorium erstellt automatisch einen Nutzer mit dem Namen „admin“ und dem Passwort „admin“. Dies sollten Sie wissen, da auf diese Weise Unbefugte in Ihr System eindringen können, vor allem wenn Sie Ihre eScriptorium-Installation später auch als Webdienst verfügbar machen.

Die Anleitung basiert auf der [GitLab-Dokumentation von Robin Tissot](https://gitlab.com/scripta/escriptorium/-/wikis/full-install).
Jedoch wurden hier einige Veränderungen vorgenommen, um die Installation möglichst einfach zu gestalten und einige Fehler zu beheben.
