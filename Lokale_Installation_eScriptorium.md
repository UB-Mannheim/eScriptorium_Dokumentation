# Anleitung zur lokalen Installation von eScriptorium unter Linux oder Windows (WSL/Virtual Box)

Die folgende Installationsanleitung basiert auf einer Installation unter Windows über **WSL** (Windows Subsystem for Linux) mit den Distributionen **Ubuntu 20.04.3** und **Debian 11** oder der Installation einer **Virtual Box** mit Linux 20.04.3. Wenn Sie weitere Informationen oder Hilfe bei der Installation dieser Anwendungen brauchen, wenden Sie sich gerne an Larissa Will (larissa.will@uni-mannheim.de).  
Nachdem die Virtual Box bzw. die Ubuntu-Umgebung auf dem PC installiert und gestartet wurde, öffnen Sie mittels eines Rechtsklicks auf den Desktop das **Terminal**. Wenn Sie WSL nutzen, dann öffnen Sie einfach die installierte Distribution.

1. Zunächst installieren Sie alle Programme, die Sie für die Nutzung bzw. Installation von eScriptorium benötigen. 
Dazu gehören Git, NPM, Postgresql-Installationen, der Redis-Server, Werkzeuge von Drittanbietern sowie Python und die virtuelle Umgebung:  
```
$ sudo apt install git postgresql postgresql-contrib libpq-dev redis-server netcat-traditional jpegoptim pngcrush libvips build-essential python3 python3-dev python3-venv npm
```

**Hinweis:** Nach dem ersten Sudo-Befehl (Sudo wird benutzt, um Prozesse mit den Rechten eines anderen Benutzers (z. B. des Superusers root) zu starten, fordert Sie die Linux-Distribution immer dazu auf, Ihr Passwort einzugeben. Es fragt Sie dann, ob Sie den entsprechenden Speicherplatz für die Installation freigeben möchten.  
Im Terminal erscheint dann die Auswahlmöglichkeit: [Y/n]. Durch Betätitgung der Enter-Taste wird automatisch die großgeschriebene Auswahl bestätigt, alternativ kann der entsprechende Buchstabe eingegeben und mit Enter bestätigt werden. Dies kann während der Installationen öfter auftreten.

OPTIONAL: Sollte der Installationsprozess nicht erfolgreich sein, geben Sie zunächst folgende Befehle ein und anschließend erneut den Installationsbefehl:  
```
$ sudo apt-get update  
$ sudo apt-get upgrade  
```

OPTIONAL: Falls Fehlermeldungen bei Postgresql auftauchen:
**Postgresql:**
```
$ sudo apt update   
$ sudo apt update --fix-missing   
$ sudo apt install postgresql  
```
 
2. Nun starten Sie Postgresql und Redis-Server, indem Sie folgendes in das Terminal eingeben:  
```
$ sudo service postgresql start  
$ sudo service redis-server start  
```
OPTIONAL: Der derzeitige Status von Postgresql kann jederzeit mit folgendem Befehl abgefragt werden:

`$ service postgresql status`  

3. Anschließend wechseln Sie zu Ihrem Postgres-User. Mit diesem Befehl wird automatisch Ihr Benutzername von Linux als eScriptorium-Benutzername gesetzt:  

`$ sudo -u postgres createuser --superuser $USER`  

Wenn Sie Ihren Namen anders als Ihren Linux-Nutzernamen wählen möchten, geben Sie ein:  

`$ sudo -u postgres createuser --superuser <Nutzername>`  

4. Anschließend legen Sie eine Datenbank für eScriptorium an:  

`$ createdb escriptorium`  

5. Nun können Sie das Repository von Gitlab klonen.  

`$ git clone https://gitlab.com/scripta/escriptorium.git`  

6. Nun wechseln Sie in das Verzeichnis escriptorium:  

`$ cd escriptorium`  

7. Jetzt erstellen und aktivieren Sie eine virtuelle Umgebung:  
```
$ python3 -m venv env  
$ source env/bin/activate  
$ pip install -U pip setuptools    
```
(Damit aktualisieren Sie die heruntergeladenen Versionen, dies kann später viele Fehler verhindern)  
```
$ pip install wheel psycopg2-binary==2.8.6  
$ pip install -r app/requirements.txt  
```
Falls hierbei eine Fehlermeldung angezeigt wird, öffnen Sie bitte die Einstellungen und ändern folgende Angaben:  

`$ vi app/requirements.txt`  

- Ändern Sie bei **psycopg** die Versionsangabe zu `psycopg2-binary==2.8.6` (Bei neueren Versionen würde folgende Fehlermeldung erscheinen: „Database section isn’t set to UTC“)  
- bei **scikit-image**, **scipy** sowie bei **scikit-learn** löschen Sie die Versionsangaben  
- **Hinweis:** Innerhalb des VI-Editors aktivieren Sie mit der Taste `i` Sie den „Insert-Mode“ mit der Taste, danach können Sie wie gewohnt schreiben. Um den Eingabemodus wieder zu verlassen, drücken Sie die Escape-Taste. Wenn Ihre Eingabe beendet ist, verlassen Sie die Settings mittels `:x`, insofern Sie die Änderungen speichern möchten. Möchten Sie eine Änderung nicht speichern, geben Sie `:q` ein.  

Anschließend müssen Sie den vorherigen Befehl noch einmal ausführen.  

Nun geben Sie folgenden Befehl ein:  

`$ pip install -r app/requirements-dev.txt`  

8. Nun müssen Sie noch Py Examples kopieren:  

`$ cp app/escriptorium/local_settings.py.example app/escriptorium/local_settings.py`  

9. OPTIONAL: Über folgenden Befehl gelangen Sie in die Einstellungen. Hier können Veränderungen vorgenommen werden. Für den Anfang müssen Sie jedoch nichts ändern und können diesen Schritt demnach überspringen.  

`$ edit app/escriptorium/local_settings.py`  

10. Nun geben Sie ein:  

`$ export DJANGO_SETTINGS_MODULE=escriptorium.local_settings`  

11. Anschließend wechseln Sie in das Arbeitsverzeichnis:  

`$ cd app`  

12. Um die bisherige Installation zu überprüfen, führen Sie folgenden Befehl aus:  

`$ python manage.py check`  

13. Führen Sie einen einfachen Celery Worker in einem neuen Terminal aus:  

`$ celery -A escriptorium worker -l INFO &`  

Bestätigen Sie mit Enter. Mittels dieses Befehls läuft Celery direkt im Hintergrund und Sie können fortfahren.  

14. Anschließend verlassen Sie das Arbeitsverzeichnis und wechseln in das Verzeichnis „Front“ und installieren NPM:  
```
$ cd ..  
$ cd front  
$ npm install  
```

OPTIONAL: Falls Fehlermeldungen erscheinen, dass es Schwachstellen (Vulnerabilities) gibt, vor allem im roten Bereich, dann sollten Sie den folgenden Befehl ausführen:  

`$ npm audit fix` 
 
und dann erneut:  

`$ npm install`  

15. Um eScriptorium produktiv zu nutzen (EntwicklerInnen wählen besser andere Optionen) geben Sie nun ein:  

`$ cd front` (falls Sie nicht bereits in diesem Ordner sind)  

`$ npm run production`  

16. Jetzt erstellen Sie eine SQL-Tabelle:  
```
$ cd ..  
$ cd app  
$ python manage.py migrate  
```

17.	Optional: Kreieren Sie einen Nutzer:  

`$ python manage.py createsuperuser`  

18.	Anschließend starten Sie den Server:  

`$ python manage.py runserver`  

19.	Nun können Sie eScriptorium nutzen, geben Sie dafür einfach in Ihren Browser folgenden Link ein: http://localhost:8000/  
(Hinweis: Sollten Sie eScriptorium in einer virtuellen Maschine installiert haben, nutzen Sie den Browser darin.)  

20.	Weitere Nutzung: Sobald Sie Ihren PC bzw. die virtuelle Maschine neugestartet haben, müssen Sie eScriptorium erneut aktivieren über das Terminal.   
```
$ cd escriptorium  
$ source env/bin/activate  
$ cd app  
$ sudo service postgresql start  
$ sudo service redis-server start  
$ celery -A escriptorium worker -l INFO &  
$ python manage.py runserver  
```
Browser: http://localhost:8000  


**Achtung:** eScriptorium erstellt automatisch einen Nutzer mit dem Namen „admin“ und dem Passwort „admin“. Dies sollten Sie wissen, da auf diese Weise Unbefugte in Ihr System eindringen können, vor allem wenn Sie Ihre eScriptorium-Installation später auch als Webdienst verfügbar machen.  

Die Anleitung basiert auf der Gitlab-Dokumentation von Robin Tissot. Jedoch wurden hier einige Veränderungen vorgenommen, um die Installation möglichst einfach zu gestalten und einige Fehler zu beheben.  
Link: https://gitlab.com/scripta/escriptorium/-/wikis/full-install  
