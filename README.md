# Tutorials für Kitodo
Dieses Repository beinhaltet Schritt-für-Schritt-Anleitungen für exemplarische Arbeitsschritte mit der Software Kitodo, einer Softwaresuite zur Digitalisierung von Kulturgut.

[![Kitodo Logo](images/kitodo_300x110.png)](https://www.kitodo.org)

## Tutorials

Die Workflowkomponente von Kitodo (Kitodo.Production) wird derzeit in einem [DFG-Projekt](https://www.kitodo.org/software/entwicklung/dfg-projekt/) umfangreich weiterentwickelt, weshalb sich die Tutorials für die Versionen 2 (stabil) und 3 (in Entwicklung) wesentlich unterscheiden:

* **[Tutorial für Kitodo 2.x](kitodo2/README.md)**
  * entstand anlässlich des [Workshops "Kitodo for newbies"](https://www.kitodo.org/news/2018/03/07/workshop-kitodo-for-newbies/) am 11./12.6.2018 an der TU Berlin
* **[Tutorial für Kitodo 3.x](kitodo3/README.md)**
  * entstand anlässlich eines [weiteren Workshops](http://www.kitodo.org/news/2018/07/23/online-tutorial/) am 10./11.9.2018 an der TU Berlin

Im Folgenden finden Sie zum Einstieg allgemeine Informationen zu Kitodo, die für beide Tutorials gleichermaßen gelten.

## Kurzeinführung in Kitodo

### Struktur

Die Software-Suite Kitodo unterstützt alle Schritte des Digitalisierungsprozesses von der Produktion über die Präsentation bis zur Archivierung digitaler Objekte. Sie umfasst mehrere Module, die gemeinsam oder unabhängig voneinander eingesetzt werden können. Dank offener Schnittstellen und der Einhaltung internationaler Standards sind sie untereinander und mit anderen Systemen interoperabel.

![Kitodo Logo](images/kitodo_uebersicht.png)

### Kitodo.Presentation

[Kitodo.Presentation](https://www.kitodo.org/software/kitodopresentation/) ist das Präsentationsmodul der Kitodo-Suite. Es kann unter anderem digitalisierte Drucke, Zeitschriften, Zeitungen, Handschriften, Noten und Musikalien, Einblattmedien und Dokumenten-Nachlässe darstellen. 

Kitodo.Presentation ist als [Erweiterung](http://typo3.org/extensions/repository/view/dlf/) des freien Content Management Systems [TYPO3](http://typo3.org/) realisiert und fügt sich nahtlos in redaktionell betreute Webseiten ein. TYPO3-Funktionen wie Benutzer-Authentifizierung, Session-Handling, Sprachlokalisierung, Caching, etc. stehen uneingeschränkt auch innerhalb der Funktionsmodule von Kitodo.Presentation zur Verfügung. Das gesamte System ist voll mandantenfähig, d.h. innerhalb einer einzigen TYPO3-Installation können beliebig viele Instanzen von Kitodo.Presentation betrieben werden, die jeweils über eigene Konfiguration, Such-Index, Datenbestand, Zugriffsrechte, optische Gestaltung, etc. verfügen.

### Kitodo.Production

[Kitodo.Production](https://www.kitodo.org/software/kitodoproduction/) ist das Workflowmanagementmodul der Kitodo-Suite. Es unterstützt den Digitalisierungsprozess von verschiedenen Materialarten wie Drucken, Periodika, Handschriften, Noten und Musikalien, Einblattmedien und Dokumentennachlässen.

Kitodo.Production ist als Webapplikation in Java programmiert und kann plattform- und ortsunabhängig über einen herkömmlichen Webbrowser bedient werden. Sie beinhaltet alle Funktionen zur Begleitung des Digitalisierungsprozesses bis zur Veröffentlichung des fertigen Digitalisats.

## Anpassungs- und Erweiterungsmöglichkeiten

### Individuelle Konfiguration

* Weitreichende Konfiguration über XML-Dateien möglich, z.B. in [Regelsatz-Datei](https://github.com/kitodo/kitodo-production/wiki/Regelsatz-XML-Datei)
* [Unterstützung von Zeitungsdigitalisierung](https://github.com/kitodo/kitodo-production/wiki/Neuen-Vorgang-anlegen-I-Zeitungen) u.a. über [Batchexport](https://github.com/kitodo/kitodo-production/wiki/Batchexport-Zeitungen)
* [Anbindung von OCR-Services](https://github.com/kitodo/kitodo-production/wiki/OCR) möglich
* siehe auch [FAQ](https://github.com/kitodo/kitodo-production/wiki/FAQs) sowie die [Dokumentation der Anwenderbibliotheken im Wiki](https://github.com/kitodo/kitodo-production/wiki/Dokumentationen-der-Anwenderbibliotheken)

### Erweiterungen

* [DFG-Projekt zur Weiterentwicklung von Kitodo.Production](https://www.kitodo.org/software/entwicklung/dfg-projekt/) (Kitodo 3.x)
  * Modularisierung der Software (u.a. Überarbeitung Systemkern, neue Workflowkomponente, Qualifzierung der Schnittstellen, Elasticsearch für die Suche, neues Rechte- und Rollensystem, Datenimport- und export für Nicht-Pica-Kataloge, Unterstützung mehrfach hierarchischer Beziehungen)
  * Medientypologische Flexibilisierung (METS/TEI für Handschriften, EAD für Archivalien und LIDO für grafische Medien und mediale Objekte)
  * Neues Bedienkonzept (Redesign auf Basis von Nutzerstudien insbesondere für Arbeitsschritte im Metadaten- und Strukturdateneditor)
* Individuelle Erweiterungen durch Dienstleister möglich (vgl. Dokumentation der erledigten Projekte von [effective WEBWORK](https://github.com/kitodo/kitodo-production/wiki/effective-webwork-Dokumentation) und [Zeutschel](https://github.com/kitodo/kitodo-production/wiki/Zeutschel-Dokumentation))
* [Medienserver mit Rechtemanagement](https://github.com/tuub/kitodo-mediaserver) (in Entwicklung an der TU Berlin)
* [Unterstützung der IIIF Presentation API in Kitodo.Presentation](https://wiki.dnb.de/download/attachments/132748423/2018-04-11_KIMWS18_Meyer-IIIF%2BDFG-Viewer.pptx?version=1&modificationDate=1523606567000&api=v2) (in Entwicklung an der UB Leipzig)
* Modul [Kitodo.Publication](https://www.kitodo.org/software/kitodopublication/) für Dokumentenserver
* Exportmechanismen zur Überführung von Daten in die [Langzeitarchivierung](https://www.kitodo.org/software/langzeitarchivierung/)

## Fragen zum Tutorial

Falls bei der Bearbeitung der Tutorials Fragen auftreten, richten Sie diese gerne an die [Community-Mailingliste](https://maillist.slub-dresden.de/cgi-bin/mailman/listinfo/kitodo-community).

## Feedback erwünscht!

Verbesserungsvorschläge und Korrekturen über GitHub [Issues](https://github.com/kitodo/kitodo-tutorials/issues) oder [Pull Requests](https://github.com/kitodo/kitodo-tutorials/pulls) und natürlich gerne auch [persönlich](https://felixlohmeier.de/).

## Lizenz

Dieses Werk ist lizenziert unter einer [Creative Commons Namensnennung 4.0 International Lizenz](https://creativecommons.org/licenses/by/4.0/).

[![Creative Commons Lizenzvertrag](images/cc_by_88x31.png)](https://creativecommons.org/licenses/by/4.0/)
