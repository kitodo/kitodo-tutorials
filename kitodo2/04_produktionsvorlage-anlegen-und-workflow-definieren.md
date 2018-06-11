[kitodo-tutorials](../README.md) » [kitodo2](README.md) » 04_produktionsvorlage-anlegen-und-workflow-definieren.md

# Produktionsvorlage anlegen und Workflow definieren

In der Regel wird für jedes zu digitalisierende Objekt ein eigener Vorgang erstellt. Um nicht für jeden dieser Vorgänge die Arbeitsschritte neu festlegen zu müssen, können Produktionsvorlagen erstellt werden, die dann als Muster dienen.

Die Unterscheidung zwischen Produktionsvorlagen und Vorgängen in Kitodo.Production sorgt oft für Verwirrung, weil die Eingabemasken nahezu identisch sind und sich lediglich durch die Checkbox `ist eine Vorlage` unterscheiden.

Für diesen Schritt werden Administrationsrechte benötigt. Sie können für die Konfiguration den in Schritt [3. Benutzerkonfiguration](03_benutzerkonfiguration.md) angelegten Account verwenden:

- Login: `workshop20180611admin`
- Passwort: `test`

## Aufgabe: Produktionsvorlage anlegen

Im Workshop verwenden wir den Regelsatz [gdz.xml](config/gdz.xml). Wenn Sie nicht den Demo-Server, sondern eine lokale Installation verwenden, dann muss diese Datei zuvor in den Ordner `rulesets` kopiert werden und im Menü Administration / `Regelsätze` angelegt werden.

Die Produktionsvorlage kann wie folgt angelegt werden:

- Menüpunkt Administration / `Produktionsvorlagen` aufrufen, dort Link `Eine neue Produktionsvorlage anlegen` klicken und folgende Angaben vornehmen:
  - Vorgangstitel: `Workshop20180611`
  - Projekt: `Workshop20180611`
  - Regelsatz: `GDZ`
  - Laufzettel: `default`
  - Ist eine Vorlage: (ja)

## Aufgabe: Workflow definieren

Nach dem Speichern erscheint die Detailansicht der gerade angelegten Produktionsvorlage. Diese ist in der Liste unter dem Menüpunkt Workflow / `Produktionsvorlagen` auch über den Button Aktionen / `Vorgang bearbeiten`  erreichbar.

Im Abschnitt `Abfolge der Aufgaben` können wir nun unseren Workflow, d.h. die bei jedem Vorgang in bestimmter Reihenfolge zu erledigenden Arbeitsschritte, definieren. Kitodo.Production nennt diese Arbeitsschritte `Aufgaben`.

* Klicken Sie auf den Link `Aufgabe hinzufügen`  und legen Sie nacheinander die folgenden Aufgaben an:
  * Scannen
    * Titel: `Scannen`
    * Reihenfolge: `1`
    * Images lesen: (ja)
    * Images schreiben: (ja)
    * Status: `Offen`
    * Benutzergruppen: `Administration` und `Scanning`
  * Erschließung
    - Titel: `Erschließung`
    - Reihenfolge: `2`
    - Metadaten: (ja)
    - Bei Annahme Modul starten: (ja)
    - Modul: `zedOSGo action:AddStructData`
    - Status: `Gesperrt`
    - Benutzergruppen: `Administration` und `Metadata`
  * Export
    - Titel: `Export`
    - Reihenfolge: `3`
    - Export DMS: (ja)
    - Status: `Gesperrt`
    - Benutzergruppen: `Administration` und `Projektmanagement`



## Hinweise

* Wenn eine Gruppe von Personen Vorgänge anlegen soll, die nicht gleichzeitig Projektmanagement-Rechte (z.B. für Statistiken) besitzen darf, dann kann auch dafür eine eigene Aufgabe definiert werden.
* Die obige Konfiguration bei Erschließung / Modul nutzt eine Funktion des ZED Server, um Strukturdaten automatisch zu ergänzen. Diese ist im Standardumfang von Kitodo.Production 2.1 nicht enthalten.
* Je nach Qualitätsanforderungen sind weitere dezidierte Aufgaben wie Qualitätskontrolle oder Nachbearbeitung vorzusehen.
* Mit der Funktion `Automatische Aufgabe` lassen sich externe Scripte auf Kommandozeilenebene starten, beispielsweise eine OCR-Anbindung. Über Variablen lassen sich Informationen aus Kitodo.Production übermitteln, z.B. der Pfad zu den Bilddateien oder der Schrifttyp (Fraktur/Antiqua).

## Literatur

* Anwenderdokumentation Produktionsvorlage: [Produktionsvorlage](https://github.com/kitodo/kitodo-production/wiki/Produktionsvorlage) und [Bearbeitung Produktionsvorlage](https://github.com/kitodo/kitodo-production/wiki/Bearbeitung-Produktionsvorlage)
* Anwenderdokumentation Workflow: [Aufgaben](https://github.com/kitodo/kitodo-production/wiki/Aufgaben), [Bearbeitung Aufgabe](https://github.com/kitodo/kitodo-production/wiki/Bearbeitung-Aufgabe) und [Scriptschritte](https://github.com/kitodo/kitodo-production/wiki/Scriptschritte)




------

<p align="center">Vorige Seite: <a href="03_benutzerkonfiguration.md">3. Benutzerkonfiguration</a> | Nächste Seite: <a href="05_vorgaenge-anlegen.md">5. Vorgänge anlegen</a></p>