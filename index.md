# Nutzung von eScriptorium

## 1. Schritt für Schritt
### 1.1. Einloggen in eScriptorium
Sie loggen sich bei eScriptorium mit einem individuellen Konto ein, das aus einem Login, einem Passwort und einer E-Mail-Adresse besteht. Ein Konto wird vom Benutzer nach Erhalt einer Einladung oder vom Administrator der Website erstellt:   
![grafik](https://user-images.githubusercontent.com/91966243/161035980-383e1833-4a9b-458c-b9ff-c378c9e087b3.png)


Sobald Sie eingeloggt sind, sehen Sie das Dashboard, welches Ihnen alle Dokumente, die Sie selbst erstellt haben und die mit ihnen geteilt wurden, anzeigt. Beim ersten Login ist das Dashboard leer.  
![grafik](https://user-images.githubusercontent.com/91966243/161036239-ee2d7b36-1ec1-400b-97a2-23abc7fa96a3.png)

### 1.2. Ein neues Dokument anlegen
#### 1.2.1. Terminologie
- Ein **„Dokument“** ist eine Kollektion von Bildern, die eine Einheit bilden.
- Ein **„Teil-Dokument“** ist ein Bild bzw. eine Seite, die Teil eines Dokumentes ist.

#### 1.2.2.Instruktionen
Um ein Dokument zu erstellen, klicken Sie auf den Button „Create new“, dadurch öffnet sich eine neue Seite sowie ein Eingabeformular:  
![grafik](https://user-images.githubusercontent.com/91966243/161036295-5a7bdfa4-46f1-4389-a04f-0bff0562cca0.png)

Das Feld „Name“ muss ausgefüllt werden. Alle anderen Felder sind optional und können später ergänzt werden.  
Nach der Eingabe der Informationen, klicken Sie auf „Create“, um das Dokument zu erstellen. Anschließend wird die Meldung „Document created successfully!“ angezeigt. Die eingegebenen Daten können später immer noch angepasst werden: der „Create“-Button wird durch einen „Update“-Button ersetzt.  
![grafik](https://user-images.githubusercontent.com/91966243/161036379-1fa3671e-c8df-4798-935c-b7926e4a7aa3.png)

Um vom Dashboard wieder auf das Eingabeformular zu kommen, müssen Sie auf das „Edit“-Icon klicken, welches sich neben dem Dokument befindet.

### 1.3. Bilder hochladen
#### 1.3.1. Zugriff auf das Interface
Unter der Schnittstelle „Bilder“ werden alle Anwendungen hinsichtlich der automatischen Bildverarbeitung sowie der Importe und Exporte verwaltet.  
Um auf diese Schnittstelle zuzugreifen, klicken Sie innerhalb eines Dokumentes einfach auf den Tab „Images“. 
![grafik](https://user-images.githubusercontent.com/91966243/161036469-eec9a3de-7311-4e49-a04e-21988456f226.png)

Es gibt mehrere Möglichkeiten Bilder auf die Plattform hochzuladen, die im Folgenden erläutert werden.

#### 1.3.2. Lokale Dateien importieren
Die Bilder können einfach per „Drag and Drop“ hochgeladen werden oder durch Auswählen der Bilder im File Explorer, mittels eines Klicks in die Box.  
![grafik](https://user-images.githubusercontent.com/91966243/161036523-ddb15628-a350-4b84-a951-3ba9002ddb12.png)

**Hinweis**: Bevor die Seite neugeladen werden kann, muss der Import aller Bilder abgeschlossen sein. eScriptorium bietet momentan keine Möglichkeit Bilder automatisch zu sortieren, daher sollte beim Upload darauf geachtet werden, alle Bilder in der richtigen Reihenfolge auszuwählen sowie auf eine entsprechende Benennung zu achten.

#### 1.3.3. Bilder aus einer PDF Datei importieren
Klicken Sie auf den „Import“-Button und dann auf „Images (PDF)“ dadurch können sie eine PDF-Datei hochladen. Aus dieser werden automatisch Bilder extrahiert. Bitte beachten Sie, dass ausschließlich Bilder importiert werden. Sollte das PDF eine Textebene enthalten entsprechend der Transkription, wird diese nicht importiert.  

#### 1.3.4. Verwendung eines IIIF-Manifests
Klicken Sie auf den „Import“-Button, dann auf die Option „Images (IIIF)“und geben anschließend die URL des IIIF-Manifests ein. Alle Bilder werden lokal kopiert, so wie auch deren Metadaten, welche im Tab „Description“ sichtbar sind. Beispiel-Link: https://gallica.bnf.fr/iiif/ark:/12148/btv1b53026595r/manifest.json

### 1.4. Dokumente manuell mit Annotationen versehen
#### 1.4.1. Zugriff auf das Interface
Manuelle Annotationen sind nötig, um Ground-Truth-Daten zu generieren und damit Modelle zu trainieren oder um Ergebnisse dieser Operationen zu korrigieren. Es kann auch als Teil einer Annotation Campaign (gemeinsames Bearbeiten eines Dokumentes innerhalb einer Gruppe) verwendet werden, die nicht auf Kraken-Modelle zurückgreift (eScriptorium ist nur eine Input-Umgebung).
Unter dem Tab „Edit“ können Sie Annotationen manuell erstellen und modifizieren. Diesen Button finden Sie am Seitenanfang sowie auf jedem einzelnen Bild in der Übersicht des Tabs „Images“. Es gibt mehrere Bearbeitungsbereiche in diesem Tab passend zu den möglichen Editierungsoptionen.  
![grafik](https://user-images.githubusercontent.com/91966243/161036566-5f0dbf9e-6d40-496a-88d3-4fed3c41ef4c.png)

- **„Image Source“** erlaubt es Ihnen das Quellbild anzusehen  
- **„Segmentation“** zeigt den Segmentationsbearbeitungsbereich an  
- **„Transcription“** zeigt den Bearbeitungsbereich der Transkription in der diplomatischen Ansicht an  
- **„Text Annotation“** zeigt den Bearbeitungsbereich der Transkription im Textmodus an, um die Lesereihenfolge zu ändern oder um Transkriptionen zu erstellen  
![grafik](https://user-images.githubusercontent.com/91966243/161036601-3f3a1a4d-dcbd-4fb9-87a6-573b0937ae94.png)

#### 1.4.2. Segmente und Bereiche auf dem Bild mit Annotationen versehen
Im Segmentbearbeitungsfenster können Sie mehrere wesentliche Operationen durchführen:  

**Baselines:**  
- Das Zeichnen von „Baselines“, die den Positionen des Textes auf dem Bild entsprechen, kann auf **zwei unterschiedliche Arten erfolgen**:  
  - Freies Zeichnen (nicht empfohlen): linke Maustaste gedrückt halten und gewünschte Zeile ziehen  
  - Punkt-für-Punkt-Darstellung: Linksklick an die entsprechende Stelle, durch einen Rechtsklick können Punkte hinzugefügt werden und durch einen erneuten Linksklick die Zeile beendet werden  
- **Zeilen Verschieben**: Zeilen auswählen und mit STRG + Ziehen an der gewünschten Stelle platzieren  
- **Zeilen auswählen**: SHIFT+Klick auf entsprechende Zeilen  
- **Auswahl aufheben**: Durch das Klicken auf eine leere Stelle, wird die Auswahl aufgehoben.  
- **Zeilenzeichnen abbrechen**: während die Zeile gezeichnet wird, Escape-Taste drücken  
- **Zeilen löschen**: Der rote Papierkorb löscht alle ausgewählten Zeilen; wenn SHIFT gedrückt gehalten wird, können mehrere Zeilen gleichzeitig gelöscht werden  
- **Zeilen verbinden**: Wenn mindestens zwei Zeilen ausgewählt sind, wird eine Option zum Verbinden der Zeilen verfügbar (J-Taste): SHIFT + Auswählen entsprechender Zeilen  SHIFT lösen  STRG + J  
- **Kontrollpunkte auf Zeile hinzufügen**: Zeile auswählen und Doppel-Klick auf die entsprechende Stelle  
- **Verlängern mehrerer Zeilen**: Falls mehrere Zeilen als zu kurz erkannt wurden (meist sinnvoll bei Texten im Blocksatz), können Sie diese einfach auf eine Länge bringen: Gelbe Schere aktivieren  SHIFT + Markieren aller Anfangs- bzw. Endpunkte der Reihe  Schere deaktivieren  SHIFT + erneut alle Punkte markieren   SHIFT lösen  STRG + alle Zeilen auf gewünschte Länge ziehen  
- **Kontrollpunkte auf einer Zeile auswählen oder verändern**: Klicken Sie mit der linken Maustaste auf eine Zeile, um sie auszuwählen, und ziehen Sie dann den ihr am nächsten liegenden Kontrollpunkt. Ein Doppelklick auf die Zeile erzeugt einen neuen Kontrollpunkt an der Mausposition. Sie können die Reihenfolge der Punkte der Zeile umkehren, indem Sie eine Zeile (oder mehrere) auswählen und den Umkehrbutton (Taste I) betätigen.  
- **Verschieben einer oder mehrerer Kontrollpunkte**: einfach Kontrollpunkt auswählen und an gewünschte Stelle ziehen  
- **Lasso-Auswahlwerkzeug**: Mit SHIFT + Ziehen erzeugen Sie ein Lasso-Auswahlwerkzeug, womit Sie Kontrollpunkte auswählen können (sie erscheinen dann schwarz). Hinweis: Wenn bereits Zeilen ausgewählt sind, wählt das Lasso nur Punkte auf diesen Zeilen aus.  
- **Mehrere Kontrollpunkte bzw. Zeilen gleichzeitig verschieben**: Mit der Tastenkombination STRG + Ziehen können Sie alle ausgewählten Kontrollpunkte auf einmal verschieben (oder die ausgewählten Zeilen, wenn keine Kontrollpunkte ausgewählt sind).  
- **Kontrollpunkte löschen**: der gelbe Papierkorb löscht nur ausgewählte Kontrollpunkte; Hinweis: Es sollte eigentlich nur am Anfang und am Ende der Zeilen jeweils ein Punkt sein. Es könnte sein, dass bei einigen Dokumenten ein Problem bei der Transkription auftritt, falls zu viele Punkte vorhanden sind: SHIFT + innerhalb der Anfangs- und Endpunkte der Zeilen alles markieren  gelben Papierkorb anklicken.  
- **Scheren-Tool**: Mit dem Ausschneidemodus (Taste C oder dem gelben Scheren-Button) können Sie Zeilen ausschneiden, in zwei Teile teilen oder einen Teil davon entfernen.  
- **Leserichtung einer Zeile**: Die Leserichtung kann über den Button „Segment“ im Tab „Images“ festgelegt werden.  

**Masken**:  
- **Berechnung von Polygonen/Masken**: Aktivierung der Berechnung von Polygonen, die mit jeder Zeile verbunden sind (Vorgang ist automatisiert und wird asynchron verwaltet, ohne dass der Benutzer nach der ersten Verwendung etwas tun muss)  
- **Erstellung von neuen Masken**: wenn eine Seite bereits Masken hat, erhalten neue Zeilen automatisch auch eine Maske. Bei der Aktualisierung einer Zeile, werden auch automatisch Masken neu berechnet.  
- **Hinweis**: Die Qualität der Masken ist abhängig von der Qualität der Segmentierung und nicht nur der dazugehörigen Zeile. Es sollten alle Zeilen eingezeichnet sein, bevor die Masken kalkuliert werden.  
- **Nur Masken kalkulieren**: Im Tab „Image“ klicken Sie auf „Segment“ und wählen dann die Option „Only Masks“ aus.  

**Textbereiche**:  
In diesem Fenster können Bereiche (oder Zonen) erstellt werden und Segmente/Zeilen mit diesen verbunden werden. Ein Segment, das sich innerhalb eines Bereichs befindet, ist daher nicht automatisch mit diesem verbunden.   
- **Von Zeilenansicht in Segmentierungsansicht wechseln**: „R“-Taste auf der Tastatur drücken  
- **Bereich erstellen**: In der Segmentierungsansicht können Sie durch einen Linksklick einen neuen Bereich anlegen und durch einen erneuten Linksklick den ausgewählten Bereich anlegen/fertigstellen.  
- **Bereiche verändern**: Bereiche können auf die gleiche Weise wie Kontrollpunkte ausgewählt und verändert werden.  
- Zeilen, die innerhalb eines Bereichs gezeichnet werden, werden automatisch an diesen gebunden.  
- **Zeilen mit Bereichen verbinden bzw. davon trennen**: Ausgewählte Zeilen können mit den entsprechenden Schaltflächen mit Bereichen verknüpft (Y-Taste) oder von ihnen getrennt (U-Taste) werden.  
- **Bereiche löschen**: Durch anklicken des Bereichs im Segmentierungsmodus und anschließendem anklicken des roten Papierkorbs, können Bereiche gelöscht werden.  

**Zusätzliche Hinweise:**  
Sie können jederzeit mit Strg + Z (Rückgängig machen) und Strg + Y (Wiederherstellen) Aktionen rückgängig machen bzw. wiederherstellen oder mit den entsprechenden Schaltflächen durch Ihren Änderungsverlauf gehen.
All diese Operationen, die in diesem Bereich genutzt werden können, finden Sie in einem Hilfsfenster, welches sich hinter dem Button „?“ befindet.

#### 1.4.3. Annotieren der Transkription
Nur wenn Segmente und Masken auf dem Bild festgelegt sind, gibt es die Möglichkeit die Funktionalitäten der Buttons „Transcription“ and „Text“ zu nutzen.  
Um eine einer Zeile zugeordnete Transkription hinzuzufügen oder zu ändern, klicken Sie im Bereich "Transcription" auf die entsprechende Zeile. Ein Eingabefenster wird angezeigt. Um eine Transkription aufzunehmen, drücken Sie „Enter“: die Transkriptions-Schnittstelle zeigt automatisch das Eingabefeld für das nächste Segment an.
Während Sie im Fenster "Transcription" tippen, werden die mit Zeilen versehenen Bereiche durch Text ersetzt und der Inhalt des Fensters "Text" ändert sich. Es ist also möglich den Text im Textfenster zu modifizieren, zu kopieren und mehrere Zeilen auf einmal einzufügen.  
![grafik](https://user-images.githubusercontent.com/91966243/161036678-ba7f2b3a-26b1-4597-ba76-204beab7c636.png)

#### 1.4.4. Eine Anmerkung zur Gliederung von Baselines, Polygonen und Transkriptionen
Die „Baseline“ ist ein zentrales Element, um Informationen in der eScriptorium Database zu speichern. Also:  
- Es ist möglich eine Baseline zu modifizieren (bewegen, Punkte hinzufügen) ohne, dass die Transkription beeinflusst wird  
- Das Polygon wird immer von der Baseline aus berechnet, auch während des Trainings  
- Es ist möglich das Polygon händisch zu ändern (nicht empfohlen), ohne dass dies Auswirkungen auf die Transkription hat  
![grafik](https://user-images.githubusercontent.com/91966243/161036730-f3a5e30d-8245-4ff7-adf4-8225aae4cf1f.png)

Während des Trainings der Kraken-Modelle, kann die Berechnung der Polygone zurückgesetzt werden: Für den User ist es daher von Vorteil, nicht in die Polygone einzugreifen und im Gegenteil dafür zu sorgen, dass die Baselines so gezeichnet werden, dass die automatisch erzeugten Polygone korrekt sind. Falls manuell Ground-Truth-Daten eingegeben werden, sollte darauf geachtet werden nur zu transkribieren was innerhalb des Polygons steht.  

#### 1.4.5. Die Reihenfolge der Zeilen ändern
Die Wiedergabereihenfolge der Zeilen erfolgt automatisch. Sie können sich die Ordnungsnummer jeder Zeile im Fenster „Segmentation“ anzeigen lassen, indem sie auf “Toggle ordering display (L)” klicken, oder im Fenster „Text“, wo die Zeilen in der folgenden Reihenfolge angezeigt werden.
Es ist möglich die Reihenfolge im „Text“-Fenster durch das Klicken von “Toggle sorting mode” zu ändern. Durch einfaches „Drag and Drop“ der Zeilen kann die Änderung durchgeführt werden.  

**Hinweis:** Es ist empfehlenswert, die Qualität der Segmentierung sicherzustellen, bevor die Reihenfolge der Zeilen geändert wird, weil das Hinzufügen und Entfernen von Zeilen die Berechnung dieser Reihenfolge systematisch neustartet und dabei manuelle Modifikationen überschreibt.   
![grafik](https://user-images.githubusercontent.com/91966243/161036793-c5c40158-363c-4770-917c-1ba11ca517ea.png)

#### 1.4.6. Semantische Annotationen
Es ist möglich, den Zeilen und Bereichen Etiketten (oder Tags) zuzuordnen, indem man einer vom User auf der Registerkarte „Description“ vordefinierten Ontologie folgt. Es gibt Standard-Tags, aber es ist auch möglich welche über das Eingabefeld hinzuzufügen (Klicken Sie auf „+“ , dann „Update“ und anschließend fügen Sie den neuen Tag zur Liste hinzu) oder zu löschen (entfernen sie Die Haken von den Boxen vor dem Tag und klicken Sie anschließend auf „Update“).  
Wählen Sie im Bereich „Segmentation“ einen Bereich oder eine Zeile aus, klicken Sie auf „Set the type on all selected lines / regions (T)” und wählen Sie das entsprechende Tag aus. Die Farben des Bereichs oder Zeile ändern sich. Es ist möglich ein Tag auf mehrere Bereiche oder Zeilen auf einmal anzuwenden: dafür wählen Sie alle gewünschten Bereiche aus (STRG+ Klick und Ziehen oder STRG gedrückt halten und die gewünschten Zeilen/Bereiche anklicken).
![grafik](https://user-images.githubusercontent.com/91966243/161036820-82db3f93-98ff-4338-85dd-932c1549eade.png)

### 1.5. Annotationen Importieren
#### 1.5.1. Strukturierte Annotationen als XML importieren
Es gibt die Möglichkeit Segmentierungen oder Transkriptionen, die außerhalb von eScriptorium erstellt wurden zu importieren. Dafür klicken Sie unter dem Tab „Images“ auf „Import“ und wählen dann die Option „Transcription (XML)“ aus.
Anschließend öffnet sich ein Formular und Sie können einen Namen für die importierte Version festlegen, und eine Datei für den Import hochladen. Dies kann eine ALTO XML Datei, eine PAGE XML Datei oder eine ZIP-Datei, die ALTO oder PAGE Dateien beinhaltet, sein.
Es ist nicht notwendig vorher auszuwählen, welche Teile des Dokuments vom Import betroffen sind: die Verbindung wird automatisch hergestellt durch die Informationen aus den XML Dateien. 
![grafik](https://user-images.githubusercontent.com/91966243/161036860-281185c8-d93f-4642-8972-eb0646ad9ad7.png)

Bitte beachten Sie, nachdem Segmentierungen importiert wurden, die nicht mit Kraken/eScriptorium erzeugt wurden, ist es wichtig die Polygone (Masken) zurückzusetzen bevor mit diesen Dokumenten Modelle trainiert werden.

#### 1.5.2. Importieren von Annotationen aus einfachem Text
Es ist möglich manuell eine Transkription von einem einfachen Text zu importieren im Fenster „Text“ innerhalb des Tabs „Edit“. Jeder Zeilenumbruch zeigt dann den Übergang zu einem neuen Abschnitt an. Es ist daher darauf zu achten, dass die Lesereihenfolge der Zeilen übereinstimmt.

### 1.6. Dokumente automatisch mit Annotationen versehen
#### 1.6.1. Anleitung
Automatische Dokumentannotationen werden über den Tab „Images“ verwaltet.  
- Wählen Sie die Bilder aus, die Sie mit Annotationen versehen wollen  
- Klicken Sie auf „Segment“ (für die Erkennung von Baselines, Polygonen und/oder Bereichen) oder auf „Transcribe“ (für Transkriptionen)  
- Ein Formular wird angezeigt: es erlaubt Ihnen ein Kraken-Modell hochzuladen oder ein Modell zu nutzen, das schon in eScriptorium existiert und für die Segmentierung, die Annotation zu konfigurieren  

#### 1.6.2. Einrichten der Segmentierung
- **„Segmentation Steps“** erlaubt es Ihnen festzulegen, auf welcher Ebene die Segmentierung durchgeführt werden soll  
- **„Line and Regions“** erzeugt Bereiche (sofern das verwendete Modell dafür trainiert wurde), Baselines und zugehörigen Polygonen  
- **„Line Baselines and Masks“** führt zur Erzeugung von Baselines und den damit verbundenen Polygonen  
- Bei der Option **„Only Line Masks“** ist es nicht erforderlich, ein Modell zu laden; mit dieser Option können Sie die Berechnung der Polygone, die mit den bereits auf den Bildern vorhandenen Baselines verbunden sind, spontan zurücksetzen.  
- **„Regions“** ermöglichen es Baselines und Polygone, die schon auf den Bildern existieren zu erhalten und nur neue Bereiche zu generieren  
- **„Text direction“** indiziert die Leserichtung der Zeilen  
![grafik](https://user-images.githubusercontent.com/91966243/161036930-329c47b7-94fa-48d7-bbdb-526fc9bf0708.png)

#### 1.6.3. Vergleich verschiedener Transkriptionen
- Laden Sie das Bild eines Dokumentes in eScriptorium hoch
- Führen Sie die Texterkennung mit dem gewünschten Modell durch und anschließend mit einem zweiten Modell oder mit manueller Texterkennung  
- Nun wählen Sie die Transkription aus, die angezeigt werden soll  
- anschließend klicken Sie das Zahnrad daneben an und wählen die Transkription mit der Sie die andere Transkription vergleichen möchten und schließen das Fenster wieder  
- Nun schalten Sie die Transkriptionsansicht ein und klicken auf die entsprechende Zeile. Sie sehen nun markierten Text in rot und grün: Grüne Zeichen sind in der aktuellen (bearbeitbaren) Transkription nicht vorhanden, rote Zeichen sind in der verglichenen Transkription nicht vorhanden  
![grafik](https://user-images.githubusercontent.com/91966243/161037014-43d55afd-b9ff-4722-8bb2-21669d4267a7.png)

### 1.7. Modelle trainieren
#### 1.7.1. Ein Training starten  
Das Training von Kraken-Modellen startet man innerhalb des Tabs „Images“. Es wird über den Tab „Models“ verfolgt (inaktiv solange noch kein anderes Modell als das Standardmodell mit dem Dokument verknüpft ist).
Der Zugang zu den Trainingsfunktionen hängt von der Autorisierung ab. Dies kann über die Administrationsschnittstelle verwaltet werden.  
Um ein Modell zu trainieren müssen sich alle Bilder/Annotationen im gleichen Dokument befinden.  
- Wählen Sie die Dokumente aus, die die Ground-Truth-Daten enthalten  
- Klicken Sie auf „Train“ und wählen Sie die Art des Trainingsmodells aus: „Segment“ für ein Segmentationsmodell, „Recognizer“ für ein Transkriptionsmodell  
- Füllen Sie das Formular aus und klicken Sie anschließend auf „Train“  
- Das Training wird gestartet, manchmal müssen Sie einen Augenblick warten bis dies angezeigt wird  
- Wenn das Training beendet ist, erhalten Sie eine Benachrichtigung und können das finale Modell unter dem Tab „Models“ finden. Es ist nun möglich das Modell zu downloaden oder es auf einem Dokument anzuwenden.  

#### 1.7.2. Ein Modell verfeinern oder von Grund auf neu trainieren?
Das Formular für die Trainingskonfiguration ermöglicht Ihnen folgende Auswahl:  
- **ob Sie von Grund auf neu beginnen möchten** (geben Sie hierfür einfach einen Namen für das zu erstellende Modell an)  
- **oder ob Sie ein Modell verfeinern möchten** (es kann über den File Manager hochgeladen werden oder sich schon in der Modellliste des zugehörigen Dokuments befinden)  
**Achtung:** In Version 0.6.9 ist das Bearbeiten der Namen von Modellen nur möglich, wenn man ein ganz neues Modell trainiert. Um zu vermeiden, dass ein bereits existierendes Modell überschrieben wird, sollten Sie das Modell lokal auf ihrem Rechner downloaden und umbenennen in den gewünschten Namen, dann können Sie es über das Formular erneut in eScriptorium hochladen.

### 1.8. Annotationen exportieren
Das Exportieren von Annotationen funktioniert über den Tab „Images“.  
- Wählen Sie die relevanten Bilder aus  
- Klicken Sie auf „Export“, dann füllen Sie das Formular aus:  
  - Spezifizieren Sie die **Version der Transkription**, die Sie exportieren möchten  
  - Spezifizieren Sie das **Export-Format** („Alto“ für XML ALTO, „Pagexml“ für XML PAGE oder „Text“ für einfachen Text)  
  - Setzen Sie einen Haken bei „Include Images“, wenn Sie zusätzlich die **Bilder exportieren** möchten  
  - Klicken Sie auf „Export“ und speichern sie die **generierte ZIP-Datei**  

## 2. Verwalten einer kollaborativen Annotation Campaign  
### 2.1. Erstellen einer Usergruppe (Admin)  
Es ist möglich eine Nutzergruppe im Administrator-Dashboard (Vorausgesetzt Sie haben die erforderlichen Rechte) zu erstellen. Diese Gruppen dienen dazu Arbeitsgruppen zu definieren oder um ausgewählten Usern bestimmte Rechte zu erteilen.
Es wird zudem bald möglich sein für User mit ausreichend Rechten, Teams zu erstellen und andere User dazu einzuladen.

### 2.2. Teilen eines Dokumentes mit einem anderen User oder einer Gruppe
Ein User kann ein Dokument mit mehreren anderen Usern teilen, auch mit denjenigen, die nicht Teil der Gruppe sind, welcher das Dokument angehört. Dies geht über den Tab „Description“:  
- Klicken Sie auf den Button „Share“  
- Geben Sie den Namen des Users ein, mit dem Sie Ihr Dokument teilen möchten oder setzen Sie einen Haken bei seinem Namen in der Liste  
- Um zu bestätigen, klicken Sie auf „Share“  
![grafik](https://user-images.githubusercontent.com/91966243/161037072-2644a074-8d44-404e-ad20-81b4b4de1319.png)

### 2.3. Eine Vorlage mit einem anderen User oder einer Gruppe teilen
Ein Template ist mit einem Dokument verknüpft und nicht mit einem User. Um ein Modell mit anderen Usern zu teilen, gibt es zwei Möglichkeiten:  
- Downloaden Sie das Modell im Tab „Models“ und versenden Sie es mit einem anderen Austauschsystem (z.B. E-Mail)  
- Teilen Sie mit dem User das Dokument, dem die Vorlage zugeordnet ist. Nun kann der andere User das Modell herunterladen und es in das Dokument laden, in dem er es anwenden möchte.  

## 3. Sonstiges
- **Wichtig**: Zeilen, Bereiche und Masken immer bearbeiten bevor Transkription erfolgt ist, da diese sonst an dieser Stelle gelöscht werden können.  
- **Binarisierung**: Dies ist meist nicht nötig, nach dem Hochladen der Bilder können diese i.d.R. direkt segmentiert werden.  
- **Keine Reaktion mehr bei der Bearbeitung des Dokuments**: Seite erneut laden (tauchte bei Firefox bisher öfters auf, ist aber noch unklar wann genau und woran es liegt)  
- **Kein Warten im Fenster auf Segmentierung, Binarisierung und Transkription**: Während dieser Prozesse, die mitunter länger dauern können, kann das Fenster verlassen werden. Der Prozess wird nicht abgebrochen.  
- **Kein Speichern nötig**: Alle Vorgänge, werden automatisch gespeichert. Wird das Bearbeitungsfenster einmal verlassen, kann man Aktionen nicht mehr rückgängig machen.  
