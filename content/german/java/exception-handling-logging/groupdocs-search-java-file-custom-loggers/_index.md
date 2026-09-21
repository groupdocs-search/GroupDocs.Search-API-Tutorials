---
date: '2026-09-21'
description: Erfahren Sie, wie Sie einen Logger erstellen, die max log size festlegen
  und den console logger in GroupDocs.Search für Java verwenden.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Erfahren Sie, wie Sie einen Logger erstellen, die max log size festlegen
  und den console logger in GroupDocs.Search für Java verwenden. Befolgen Sie Schritt‑für‑Schritt‑Anleitungen
  und Tipps zu bewährten Methoden.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Wie man einen Logger erstellt und die max log size in GroupDocs.Search begrenzt
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Wie man einen Logger erstellt und die max log size in GroupDocs.Search für
  Java begrenzt
type: docs
url: /de/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Wie man Logger erstellt und die Logdateigröße in GroupDocs.Search für Java begrenzt

In diesem Tutorial erfahren Sie **wie man Logger erstellt** Implementierungen für GroupDocs.Search, konfigurieren eine maximale Logdateigröße und wechseln zwischen dateibasiertem und Konsolen‑Logging. Eine ordnungsgemäße Protokollverwaltung verhindert, dass Festplatten bei großen Indexierungsaufgaben voll werden, verbessert die Fehlersuche und gibt Ihnen sofortiges Feedback während der Entwicklung. Wir beginnen mit der Maven‑Einrichtung, gehen die Logger‑Konfiguration durch und schließen mit einer einfachen Suchabfrage ab, die den Logger in Aktion zeigt.

## Schnelle Antworten
- **Was bedeutet „Logdateigröße begrenzen“?** Sie begrenzt die maximale Größe einer Logdatei und verhindert unkontrolliertes Wachstum auf der Festplatte.  
- **Welcher Logger ermöglicht das Begrenzen der Logdateigröße?** Der integrierte `FileLogger` akzeptiert einen Max‑Größen‑Parameter.  
- **Wie verwende ich den Console‑Logger in Java?** Instanziieren Sie `ConsoleLogger` und setzen ihn in `IndexSettings`.  
- **Benötige ich eine Lizenz für GroupDocs.Search?** Eine Testversion funktioniert für die Evaluierung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Was ist der erste Schritt?** Fügen Sie die GroupDocs.Search‑Abhängigkeit zu Ihrem Maven‑Projekt hinzu.  

## Was bedeutet Logdateigröße begrenzen?
Die Einstellung **Logdateigröße begrenzen** weist den Logger an, keine neuen Einträge mehr zu schreiben, sobald die Datei einen definierten Schwellenwert erreicht (z. B. 4 MB). Wird das Limit erreicht, verwirft der Logger entweder weitere Meldungen oder wechselt zu einer neuen Datei, sodass die Festplattennutzung vorhersehbar bleibt.

## Warum Datei‑ und benutzerdefinierte Logger mit GroupDocs.Search verwenden?
Datei‑ und benutzerdefinierte Logger bieten Auditierbarkeit, Debug‑Einblicke und Flexibilität. In Produktionsumgebungen liefern Dateilog‑Einträge ein permanentes Protokoll jeder Index‑ und Suchoperation, während Konsolen‑Logs sofortiges Feedback während der Entwicklung geben. Diese Logs helfen Teams, die Leistung zu überwachen, Fehler nachzuvollziehen und Compliance‑Anforderungen durch ein detailliertes Aktivitätsprotokoll zu erfüllen.

## Voraussetzungen
- GroupDocs.Search für Java ≥ 25.4.  
- JDK 8 oder neuer, mit einer IDE wie IntelliJ IDEA oder Eclipse.  
- Grundlegende Kenntnisse in Maven und Java‑Programmierung.  

## Einrichtung von GroupDocs.Search für Java

Fügen Sie die Bibliothek Ihrem Projekt mit einer der untenstehenden Methoden hinzu.

**Maven‑Einrichtung:**  

```text
```xml
<repositories>
    <repository>
        <id>repository.groupdocs.com</id>
        <name>GroupDocs Repository</name>
        <url>https://releases.groupdocs.com/search/java/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-search</artifactId>
        <version>25.4</version>
    </dependency>
</dependencies>
```
```

**Direkter Download:**  
Laden Sie das neueste JAR von der offiziellen Seite herunter: [GroupDocs.Search für Java Releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
Erhalten Sie eine Testversion oder kaufen Sie eine Lizenz über die [Lizenzierungsseite](https://purchase.groupdocs.com/temporary-license/).

## Wie man einen benutzerdefinierten Logger für GroupDocs.Search erstellt
Das Erstellen eines benutzerdefinierten Loggers ist unkompliziert, weil GroupDocs.Search auf dem `ILogger`‑Interface basiert. Durch Implementierung dieses Interfaces – oder durch Erweiterung des bereitgestellten `FileLogger` bzw. `ConsoleLogger` – können Sie zusätzliches Verhalten wie Remote‑Weiterleitung oder Log‑Rotation einbinden. Sie können zudem Initialisierungslogik hinzufügen, z. B. das Öffnen von Netzwerkverbindungen, und sicherstellen, dass Ressourcen im `shutdown`‑Methodenaufruf des Loggers geschlossen werden. Dieser Ansatz ermöglicht die Integration mit Monitoring‑Plattformen wie ELK oder Splunk.

### Definition Anker
`ILogger` ist der Kern‑Logging‑Vertrag in GroupDocs.Search; jede Klasse, die deren `log(Level, String)`‑Methode implementiert, kann ein Logger sein.

### Beispielansatz (kein Code‑Block)
1. Erstellen Sie eine Klasse, die `ILogger` implementiert.  
2. Überschreiben Sie die `log`‑Methode, um Nachrichten an Ihr gewünschtes Ziel (Datei, Datenbank, HTTP‑Endpunkt) zu schreiben.  
3. Rufen Sie in der Index‑Konfiguration `settings.setLogger(new YourCustomLogger())` auf.  

## Wie man die Logdateigröße mit dem File Logger begrenzt
Der `FileLogger` schreibt Log‑Einträge in eine Datei auf dem Datenträger und akzeptiert ein Max‑Größen‑Argument. Durch Angabe des Größenlimits stoppt der Logger automatisch das Hinzufügen neuer Einträge oder erstellt eine neue Datei, sobald der Schwellenwert erreicht ist, und verhindert so unkontrolliertes Wachstum der Festplatte. Dieses Verhalten stellt sicher, dass das Logging die Indexierungs‑Performance nicht beeinträchtigt und gleichzeitig ein kompakter Ereignis‑Verlauf erhalten bleibt.

### Definition Anker
`FileLogger` ist ein integrierter Logger, der Nachrichten in einer Textdatei speichert und eine konfigurierbare maximale Dateigröße unterstützt.

### Schritt‑für‑Schritt‑Anleitung
1️⃣ **Notwendige Pakete importieren**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Indexeinstellungen mit File Logger einrichten**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Index erstellen oder laden**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Dokumente zum Index hinzufügen**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Suchabfrage ausführen**  
```text
```java
SearchResult result = index.search(query);
```
```

**Wichtiger Hinweis:** Das zweite Argument des `FileLogger`‑Konstruktors (`4.0`) definiert die **maximale Loggröße** in Megabyte und erfüllt damit die Anforderung **Logdateigröße begrenzen**.

## Wie man den Console Logger in Java verwendet
Wenn Sie sofortige Sichtbarkeit von Log‑Ereignissen benötigen, schreibt der `ConsoleLogger` jede Nachricht nach `System.out`. Dieser Logger ist leichtgewichtig und thread‑sicher, wodurch er sich für Entwicklungs‑ und Debug‑Sitzungen eignet. Er liefert sofortiges Feedback zum Indexierungs‑Fortschritt, zu Suchabfragen und zu Fehlermeldungen, ohne Dateizugriffe, was iterative Tests beschleunigen kann.

### Definition Anker
`ConsoleLogger` ist ein leichtgewichtiger Logger, der Log‑Einträge in den Standard‑Konsolen‑Stream ausgibt und sich ideal für Debug‑Sitzungen eignet.

### Konfigurationsschritte
1️⃣ **Console Logger importieren**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Indexeinstellungen mit Console Logger einrichten**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Index erstellen oder laden**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Dokumente hinzufügen und Suche ausführen**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Tipp:** Der Console Logger ist während der Entwicklung ideal, da er jeden Logeintrag sofort ausgibt und Ihnen hilft zu überprüfen, dass Indexierung und Suche wie erwartet funktionieren.

## Praktische Anwendungen
1. **Dokumenten‑Management‑Systeme:** Audit‑Trails für jedes indexierte Dokument führen und Compliance‑Anforderungen erfüllen.  
2. **Enterprise‑Suchmaschinen:** Echtzeit‑Überwachung von Abfrage‑Performance und Fehlerraten für schnelle SLA‑Kontrollen.  
3. **Rechts‑ und Compliance‑Software:** Suchbegriffe und Zeitstempel für regulatorische Berichte aufzeichnen und für den vorgeschriebenen Aufbewahrungszeitraum speichern.

## Leistungsüberlegungen
- **Loggröße:** Durch **maximale Loggröße setzen** vermeiden Sie übermäßige Festplattennutzung, die sonst den Garbage‑Collector der JVM verlangsamen könnte.  
- **Asynchrones Logging:** Für Szenarien mit hohem Durchsatz können Sie Ihren Logger in eine asynchrone Warteschlange einbinden, um I/O vom Index‑Thread zu entkoppeln (Implementierung liegt außerhalb dieses Leitfadens).  
- **Speicherverwaltung:** Große `Index`‑Objekte mit `index.close()` freigeben, sobald sie nicht mehr benötigt werden, um den JVM‑Speicherverbrauch gering zu halten.

## Häufige Probleme & Lösungen
- **Log‑Pfad nicht zugänglich:** Stellen Sie sicher, dass das Verzeichnis existiert und die Anwendung Schreibrechte für das Benutzerkonto hat, das die JVM ausführt.  
- **Logger wird nicht ausgelöst:** Vergewissern Sie sich, dass Sie `settings.setLogger(...)` *vor* dem Erstellen des `Index`‑Objekts aufrufen; sonst wird der Standard‑Logger verwendet.  
- **Konsolenausgabe fehlt:** Prüfen Sie, ob die Anwendung in einem Terminal läuft, das `System.out` anzeigt, und ob kein Logging‑Framework (z. B. SLF4J) die Ausgabe abfängt.

## Häufig gestellte Fragen

**Q: Was steuert der zweite Parameter von `FileLogger`?**  
A: Er legt die maximale Größe der Logdatei in Megabyte fest, sodass Sie die **maximale Loggröße** setzen und unkontrolliertes Wachstum verhindern können.

**Q: Kann ich Datei‑ und Console‑Logger kombinieren?**  
A: Ja. Erstellen Sie einen benutzerdefinierten Logger, der jeden `log`‑Aufruf sowohl an einen `FileLogger` als auch an einen `ConsoleLogger` weiterleitet, und registrieren Sie diesen zusammengesetzten Logger bei `IndexSettings`.

**Q: Wie füge ich nach der Erst­erstellung Dokumente zum Index hinzu?**  
A: Rufen Sie jederzeit `index.add(pathToNewDocs)` auf; der konfigurierte Logger zeichnet die Hinzufügung automatisch auf.

**Q: Ist `ConsoleLogger` thread‑sicher?**  
A: Er schreibt direkt nach `System.out`, das von der JVM intern synchronisiert wird, sodass er für typische multithreaded‑Szenarien sicher ist.

**Q: Beeinflusst das Begrenzen der Logdateigröße die Menge gespeicherter Informationen?**  
A: Sobald das Größenlimit erreicht ist, werden neue Einträge entweder verworfen oder der Logger wechselt zu einer neuen Datei, abhängig von der gewählten Implementierung.

## Ressourcen
- [Dokumentation](https://docs.groupdocs.com/search/java/)
- [API‑Referenz](https://reference.groupdocs.com/search/java/)

**Zuletzt aktualisiert:** 2026-09-21  
**Getestet mit:** GroupDocs.Search für Java 25.4  
**Autor:** GroupDocs  

## Verwandte Tutorials

- [Wie man Logging implementiert – Ausnahmebehandlung und Logging‑Tutorials für GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Asynchrones Logging in Java mit GroupDocs.Search implementieren – Leitfaden für benutzerdefinierten Logger](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Suchindex in Java erstellen – GroupDocs.Search Tutorials](/search/java/indexing/)