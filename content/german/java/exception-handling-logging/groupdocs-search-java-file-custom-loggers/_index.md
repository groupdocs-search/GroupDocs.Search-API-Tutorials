---
date: '2025-12-24'
description: Erfahren Sie, wie Sie die Logdateigröße begrenzen und den Konsolen‑Logger
  in Java mit GroupDocs.Search für Java verwenden. Dieser Leitfaden behandelt Logging‑Konfigurationen,
  Tipps zur Fehlerbehebung und Leistungsoptimierung.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Logdateigröße mit GroupDocs.Search Java-Loggern begrenzen
type: docs
url: /de/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Begrenzen der Logdateigröße mit GroupDocs.Search Java Loggern

Effizientes Logging ist entscheidend beim Verwalten großer Dokumentensammlungen, insbesondere wenn Sie die **Logdateigröße begrenzen** müssen, um den Speicherverbrauch im Griff zu behalten. **GroupDocs.Search for Java** bietet robuste Lösungen zur Handhabung von Logs durch seine leistungsstarken Suchfunktionen. Dieses Tutorial führt Sie in die Implementierung von Datei‑ und benutzerdefinierten Loggern mit GroupDocs.Search ein und verbessert die Fähigkeit Ihrer Anwendung, Ereignisse zu verfolgen und Probleme zu debuggen.

## Quick Answers
- **Was bedeutet „Logdateigröße begrenzen“?** Sie begrenzt die maximale Größe einer Logdatei und verhindert ein unkontrolliertes Wachstum auf der Festplatte.  
- **Welcher Logger ermöglicht das Begrenzen der Logdateigröße?** Der integrierte `FileLogger` akzeptiert einen Max‑Size‑Parameter.  
- **Wie verwende ich den Console Logger in Java?** Instanziieren Sie `ConsoleLogger` und setzen Sie ihn in `IndexSettings`.  
- **Benötige ich eine Lizenz für GroupDocs.Search?** Eine Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Was ist der erste Schritt?** Fügen Sie die GroupDocs.Search‑Abhängigkeit zu Ihrem Maven‑Projekt hinzu.

## Was bedeutet das Begrenzen der Logdateigröße?
Das Begrenzen der Logdateigröße bedeutet, den Logger so zu konfigurieren, dass die Datei, sobald sie einen vordefinierten Schwellenwert (z. B. 4 MB) erreicht, nicht weiter wächst oder rotiert. Dadurch bleibt der Speicherbedarf Ihrer Anwendung vorhersehbar und Leistungsverschlechterungen werden vermieden.

## Warum Datei‑ und benutzerdefinierte Logger mit GroupDocs.Search verwenden?
- **Auditierbarkeit:** Einen dauerhaften Nachweis von Indexierungs‑ und Suchvorgängen behalten.  
- **Debugging:** Probleme schnell lokalisieren, indem Sie prägnante Logs prüfen.  
- **Flexibilität:** Zwischen persistenten Datei‑Logs und sofortiger Konsolenausgabe wählen (`use console logger java`).  

## Prerequisites
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 oder neuer, IDE (IntelliJ IDEA, Eclipse usw.).  
- Grundkenntnisse in Java und Maven.  

## Einstellung von GroupDocs.Search für Java

Fügen Sie die Bibliothek Ihrem Projekt mit einer der untenstehenden Methoden hinzu.

**Maven Setup:**

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

**Direkter Download:**  
Laden Sie das neueste JAR von der offiziellen Seite herunter: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lizenzbeschaffung
Erhalten Sie eine Testversion oder erwerben Sie eine Lizenz über die [Lizenzierungsseite](https://purchase.groupdocs.com/temporary-license/).

## Wie man die Logdateigröße mit dem File Logger begrenzt
Im Folgenden finden Sie eine Schritt‑für‑Schritt‑Anleitung, die zeigt, wie Sie `FileLogger` so konfigurieren, dass die Logdatei niemals die von Ihnen angegebene Größe überschreitet.

### 1️⃣ Import Necessary Packages
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Set Up Index Settings with File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Create or Load the Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Add Documents to the Index
```java
index.add(documentsFolder);
```

### 5️⃣ Perform a Search Query
```java
SearchResult result = index.search(query);
```

**Wichtiger Hinweis:** Das zweite Argument des `FileLogger`‑Konstruktors (`4.0`) definiert die maximale Logdateigröße in Megabyte und erfüllt damit direkt die Anforderung, die **Logdateigröße zu begrenzen**.

## Wie man den Console Logger in Java verwendet
Wenn Sie sofortiges Feedback im Terminal bevorzugen, ersetzen Sie den File Logger durch einen Console Logger.

### 1️⃣ Import the Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Set Up Index Settings with Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Create or Load the Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Add Documents and Perform a Search
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tipp:** Der Console Logger ist während der Entwicklung ideal, da er jeden Log‑Eintrag sofort ausgibt und Ihnen hilft zu überprüfen, dass Indexierung und Suche wie erwartet funktionieren.

## Practical Applications
1. **Dokumentenmanagement‑Systeme:** Audit‑Spuren für jedes indizierte Dokument führen.  
2. **Enterprise‑Suchmaschinen:** Abfrage‑Performance und Fehlerraten in Echtzeit überwachen.  
3. **Legal‑ und Compliance‑Software:** Suchbegriffe für regulatorische Berichte aufzeichnen.

## Leistungsüberlegungen
- **Loggröße:** Durch Begrenzen der Logdateigröße vermeiden Sie übermäßige Plattennutzung, die Ihre Anwendung verlangsamen könnte.  
- **Asynchrones Logging:** Wenn Sie einen höheren Durchsatz benötigen, sollten Sie den Logger in eine asynchrone Warteschlange einbinden (außerhalb des Umfangs dieses Leitfadens).  
- **Speichermanagement:** Geben Sie große `Index`‑Objekte frei, sobald sie nicht mehr benötigt werden, um den JVM‑Footprint gering zu halten.

## Häufige Probleme & Lösungen
- **Log‑Pfad nicht zugänglich:** Stellen Sie sicher, dass das Verzeichnis existiert und die Anwendung Schreibrechte hat.  
- **Logger wird nicht ausgelöst:** Stellen Sie sicher, dass Sie `settings.setLogger(...)` *vor* dem Erzeugen des `Index`‑Objekts aufrufen.  
- **Konsolenausgabe fehlt:** Vergewissern Sie sich, dass Sie die Anwendung in einem Terminal ausführen, das `System.out` anzeigt.

## Frequently Asked Questions

**F: Was steuert der zweite Parameter von `FileLogger`?**  
A: Er legt die maximale Größe der Logdatei in Megabyte fest, wodurch Sie die Logdateigröße begrenzen können.

**F: Kann ich Datei‑ und Console‑Logger kombinieren?**  
A: Ja, indem Sie einen benutzerdefinierten Logger erstellen, der Nachrichten an beide Ziele weiterleitet.

**F: Wie füge ich nach der ersten Erstellung Dokumente zum Index hinzu?**  
A: Rufen Sie jederzeit `index.add(pathToNewDocs)` auf; der Logger zeichnet den Vorgang auf.

**F: Ist `ConsoleLogger` thread‑sicher?**  
A: Er schreibt direkt zu `System.out`, das von der JVM synchronisiert wird, wodurch er für die meisten Anwendungsfälle sicher ist.

**F: Wird das Begrenzen der Logdateigröße die Menge der gespeicherten Informationen beeinflussen?**  
A: Sobald das Größenlimit erreicht ist, können neue Einträge verworfen oder die Datei rotiert werden, je nach Implementierung des Loggers.

## Resources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Zuletzt aktualisiert:** 2025-12-24  
**Getestet mit:** GroupDocs.Search for Java 25.4  
**Autor:** GroupDocs  

---