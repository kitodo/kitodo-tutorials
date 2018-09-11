[kitodo-tutorials](../README.md) » [kitodo3](README.md) » 04_produktionsvorlage-anlegen-und-workflow-definieren.md

# Workflow definieren und Produktionsvorlage anlegen

In der Regel wird für jedes zu digitalisierende Objekt ein eigener Vorgang erstellt. Um nicht für jeden dieser Vorgänge die Arbeitsschritte neu festlegen zu müssen, können Produktionsvorlagen erstellt werden, die dann als Muster dienen.

Die grafische Erstellung von Workflows ist eine neue Funktionalität von Kitodo 3.x. Dazu wird der Standard BPMN verwendet und ein bestehender Workflow-Editor Camunda integriert.

http://localhost:8080/kitodo/pages/projects.jsf

- Login: `testAdmin`
- Passwort: `test`

## Aufgabe: Workflow versuchsweise definieren

Die Erstellung von Workflows ist in der aktuellen Entwicklerversion noch etwas unübersichtlich, so dass wir den vorhandenen Beispielworkflow verwenden. Machen Sie sich trotzdem versuchsweise mit dem Editor vertraut.

Menü `Projekte` / Tab `Workflows`

* Button `Neu` / `Neuer Workflow` klicken
* Dateiname vergeben
* Rechts in der Seitenleiste bei `Name` einen Namen für den Workflow vergeben
* Workflow zeichnen und Angaben vornehmen
  - Startpunkt im Diagramm anklicken und das erscheinende rechteckige Symbol (`Append task`) auswählen. Ein neuer Task wurde ergänzt. Vergeben Sie einen Namen und im Reiter `Task` ggf. weitere Parameter.
  - Als Abschluss verwenden Sie den zweiten Kreis (mit mehr Linienbreite, `Create EndEvent`)
  - Workflow mit dem Schalter als `Fertig` markieren und `Speichern`

## Aufgabe: Produktionsvorlage anlegen

Menü `Projekte` / Tab `Produktionsvorlagen`

* Produktionsvorlagentitel: `Workshop20180910`
* Projekt: `Workshop20180910`
* Regelsatz: `SLUBDD`
* Laufzettel: `default`
* Workflow: `Example_Workflow`
* In Auswahlliste anzeigen: (ja)
* Aktiv: (ja)

Die neu erstellte Produktionsvorlage ist in der Liste unter dem Menüpunkt `Projekte`/ Tab `Produktionsvorlagen` erreichbar. Editieren Sie die Produktionsvorlage.

Im Tab `Aufgabenliste` können wir nun unseren Workflow, d.h. die bei jedem Vorgang in bestimmter Reihenfolge zu erledigenden Arbeitsschritte, definieren. Kitodo.Production nennt diese Arbeitsschritte `Aufgaben`.


## Hinweise

* Wenn eine Gruppe von Personen Vorgänge anlegen soll, die nicht gleichzeitig Projektmanagement-Rechte (z.B. für Statistiken) besitzen darf, dann kann auch dafür eine eigene Aufgabe definiert werden.
* Je nach Qualitätsanforderungen sind weitere dezidierte Aufgaben wie Qualitätskontrolle oder Nachbearbeitung vorzusehen.
* Mit der Funktion `Automatische Aufgabe` lassen sich externe Scripte auf Kommandozeilenebene starten, beispielsweise eine OCR-Anbindung. Über Variablen lassen sich Informationen aus Kitodo.Production übermitteln, z.B. der Pfad zu den Bilddateien oder der Schrifttyp (Fraktur/Antiqua).

## Literatur

* Anwenderdokumentation Produktionsvorlage: [Produktionsvorlage](https://github.com/kitodo/kitodo-production/wiki/Produktionsvorlage) und [Bearbeitung Produktionsvorlage](https://github.com/kitodo/kitodo-production/wiki/Bearbeitung-Produktionsvorlage)
* Anwenderdokumentation Workflow: [Aufgaben](https://github.com/kitodo/kitodo-production/wiki/Aufgaben), [Bearbeitung Aufgabe](https://github.com/kitodo/kitodo-production/wiki/Bearbeitung-Aufgabe) und [Scriptschritte](https://github.com/kitodo/kitodo-production/wiki/Scriptschritte)




------

<p align="center">Vorige Seite: <a href="03_benutzerkonfiguration.md">3. Benutzerkonfiguration</a> | Nächste Seite: <a href="05_vorgaenge-anlegen.md">5. Vorgänge anlegen</a></p>
