---
layout: default
title: Administration
nav_order: 3
---

Diese Seite beschreibt Funktionen, die von einem Administrator von eScriptorium eingerichtet werden: Standardmerkmale, die pro Instanz konfiguriert werden, sowie eine Erweiterung, die die Instanz der UB Mannheim über das Standard-Release hinaus bietet.

## 1. Transkriptionsschriftarten einrichten

Die Schriftart, mit der die Transkriptionszeilen im Bearbeitungsfenster angezeigt werden, ist in eScriptorium ein Standardmerkmal, das auf Dokument-, Projekt- oder Benutzerebene gewählt wird (siehe [neues Interface, Abschnitt 1.12](./Nutzungsanleitung_neues_Interface_eScriptorium.md#112-schriftart-für-die-transkription-wählen)). Welche Schriftarten dabei zur Auswahl stehen, richtet der Administrator der Instanz ein.

### 1.1. Übersicht der Schriftarten

Im Django-Admin (unter „Core“) ist das Modell **„Fonts“** aufgeführt. Es enthält alle der Instanz hinterlegten Schriftarten:

<img src="./images/current/admin-fonts.png" style="width:80%; height:auto;">

### 1.2. Eine neue Schriftart hinterlegen

Eine neue Schriftart wird über „Fonts“ → „Add“ angelegt:

<img src="./images/current/admin-font-add.png" style="width:80%; height:auto;">

- **Name:** Der in den Auswahllisten der Benutzer angezeigte Name (z.&nbsp;B. „Noto Sans“).
- **File:** Die Schriftdatei im Format `ttf`, `otf`, `woff` oder `woff2`.
- **Preview:** Zeigt nach dem Speichern die gewählte Schrift in einer Beispielzeile an.
- **Metrik (metrics):** Steuert, wie die Schrift selbst auf der Zeile sitzt und überall dort wirkt, wo Transkriptionen angezeigt werden. *Size* ist ein Skalierungsfaktor (1.0 belässt die Schrift unverändert), *Ascent* den Abstand über der Grundlinie (erhöhen, wenn hohe Zeichen abgeschnitten werden), *Descent* den Abstand unter der Grundlinie (erhöhen, wenn tiefe Zeichen abgeschnitten werden) und *Line height* den Zeilenabstand in em (leer lässt den Standard).
- **Eingabefeld der Zeilenansicht (line editor input):** Steuert die Gestaltung des Eingabefelds in der Zeilenansicht (Höhe, Innenabstände oben/unten, Außenabstände oben/unten und vertikale Ausrichtung), jeweils in em; leere Werte lassen die jeweiligen Standardwerte gelten.

Nach dem Speichern steht die Schriftart allen Benutzern in den Auswahllisten zur Verfügung.

### 1.3. Standard-Schriftarten der Instanz

Die Instanz der UB Mannheim stellt die Transkriptionsschriftarten **Gentium Plus**, **Noto Sans**, **Noto Sans Hebrew**, **OpenDyslexic** und **Abyssinica** (Schrift für äthiopische Schriften) vor. Die Schriftdateien können über die oben beschriebene Funktion im Django-Admin nachinstalliert oder aktualisiert werden; eine vorhandene Schriftart (erkannt am Namen) wird nicht doppelt angelegt, sondern übersprungen.

## 2. Benutzer einladen

Neue Benutzer werden über Einladungen per E-Mail registriert: Der Empfänger erhält eine E-Mail mit einem Link, über den er sein Konto anlegt (Login, E-Mail-Adresse, Vor- und Nachname, Passwort). Die Einladeseite ist für alle Benutzer sichtbar, die die Berechtigung „Benutzer einladen“ (*can_invite*) haben – dazu zählen in der Regel Administrator:innen; sie kann über das Benutzermenü oben rechts unter „Einladen“ geöffnet werden.

### 2.1. Einzelne Einladung

Im Modus „Einzeln“ geben Sie die Angaben zum Empfänger ein: E-Mail-Adresse, optional Vor- und Nachname sowie optional das **Team** (Gruppe), in das der Benutzer nach der Registrierung aufgenommen werden soll, und ein optionales **Ablaufdatum** für das Konto. Mit „Absenden“ wird die Einladungsmail verschickt.

### 2.2. Massenversand

Im Modus „Massenversand“ können mehrere Einladungen auf einmal versendet werden: Entweder wird eine CSV-Datei mit einer E-Mail-Adresse pro Zeile hochgeladen oder die Adressen werden direkt eingegeben (eine pro Zeile, optional in der Form „Vorname Nachname <adresse>"). Auch hier können optional Team und Ablaufdatum festgelegt werden; ungültige Adressen werden übersprungen.

Versendete Einladungen (mit Empfänger, Team und Status) können über das Benutzermenü unter „Profileinstellungen“ → „Einladungen“ eingesehen werden.

## 3. API-Token und REST-API

eScriptorium stellt eine REST-API (DRF) bereit, mit der sich Projekte, Dokumente, Transkriptionen, Bilder, Annotationen, Modelle, Schriftarten und mehr per HTTP verwalten lassen. Jeder Benutzer besitzt einen persönlichen **API-Token**:
- Den Token finden Sie unter „Profileinstellungen“ → „API-Schlüssel“; die Buttons daneben kopieren ihn in die Zwischenablage bzw. erzeugen einen neuen Token (der alte wird dabei ungültig).
- Autorisiert wird mit dem Header `Authorization: Token <token>`; die Seite zeigt ein `curl`-Beispiel.

Die API ist selbst dokumentiert (OpenAPI): Unter `/api/schema/` liegt das Schema, `/api/swagger/` die interaktive Swagger-UI und `/api/redoc/` eine ReDoc-Darstellung.

## 4. Web-Statistik (Matomo)

Die Instanz der UB Mannheim bietet – als Erweiterung gegenüber dem Standard-Release, die derzeit als Pull Request für die Standardversion vorgeschlagen ist – eine optionale Web-Statistik auf Basis von [Matomo](https://matomo.org/). Die Auswertung wird auf Instanzebene konfiguriert und betrifft die gesamte Oberfläche (also auch Seiten ohne Login); die Einbindung respektiert dabei die ortsbezogene Datenschutzkonfiguration.

- Die Statistik wird durch die Variablen `MATOMO_URL` (URL der Matomo-Instanz, z.&nbsp;B. `https://ub-monitor.bib.uni-mannheim.de/matomo/`) und `MATOMO_SITE_ID` (die Kennung des betroffenen Matomo-Projekts) aktiviert.
- Sind beide Werte gesetzt, fügt eScriptorium das Matomo-Skript in jede Seite ein; bleiben sie leer, wird keine Statistik geladen.
- So lässt sich die Nutzung der Instanz (Seitenaufrufe, Klicks) anonymisiert auswerten, ohne dass eine Analyse-Drittanbieterdatenbank kontaktiert wird.
