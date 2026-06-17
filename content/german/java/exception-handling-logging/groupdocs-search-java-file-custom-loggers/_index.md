---
date: '2026-02-24'
description: Erfahren Sie, wie Sie einen benutzerdefinierten Logger erstellen, die
  maximale Protokollgröße festlegen und einen Konsolen‑ oder Dateilogger in GroupDocs.Search
  für Java konfigurieren.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Wie man einen benutzerdefinierten Logger erstellt und die Logdateigröße mit
  GroupDocs.Search Java begrenzt
type: docs
url: /de/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Begrenzen der Logdateigröße mit GroupDocs.Search Java Loggern

In diesem Leitfaden **erstellen Sie benutzerdefinierte Logger**‑Implementierungen und lernen, wie Sie **die Logdateigröße begrenzen** können, während Sie GroupDocs.Search für Java verwenden. Die Kontrolle des Log‑Wachstums ist für groß angelegte Dokumenten‑Indexierung entscheidend, und die integrierten Logger ermöglichen es Ihnen, **die maximale Loggröße festzulegen**, **Logdateien zu rotieren** oder zu einem **Console‑Logger zu wechseln** für sofortiges Feedback. Lassen Sie uns die komplette Einrichtung durchgehen – von der Maven‑Konfiguration bis zum Ausführen einer Suchabfrage – und sehen, wie Sie **Dokumente zum Index hinzufügen** können, während der Logger aktiv ist.

## Schnellantworten
- **Was bedeutet „Logdateigröße begrenzen“?** Sie begrenzt die maximale Größe einer Logdatei und verhindert unkontrolliertes Wachstum auf der Festplatte.  
- **Welcher Logger lässt sich zur Begrenzung der Logdateigröße verwenden?** Der integrierte `FileLogger` akzeptiert einen Max‑Size‑Parameter.  
- **Wie verwende ich den Console‑Logger in Java?** Instanziieren Sie `ConsoleLogger` und setzen Sie ihn in `IndexSettings`.  
- **Benötige ich eine Lizenz für GroupDocs.Search?** Eine Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Was ist der erste Schritt?** Fügen Sie die GroupDocs.Search‑Abhängigkeit zu Ihrem Maven‑Projekt hinzu.  

## Was bedeutet Logdateigröße begrenzen?
Die Begrenzung der Logdateigröße bedeutet, den Logger so zu konfigurieren, dass er, sobald die Datei einen vordefinierten Schwellenwert (z. B. 4 MB) erreicht, nicht weiter wächst oder rotiert. Das hält den Speicherbedarf Ihrer Anwendung vorhersehbar und verhindert Leistungseinbußen.

## Warum Datei‑ und benutzerdefinierte Logger mit GroupDocs.Search verwenden?
- **Auditierbarkeit:** Permanent Aufzeichnungen von Indexierungs‑ und Suchvorgängen führen.  
- **Debugging:** Probleme schnell lokalisieren, indem Sie kompakte Logs prüfen.  
- **Flexibilität:** Zwischen persistenten Datei‑Logs und sofortiger Konsolenausgabe (`use console logger`) wählen.  

## Voraussetzungen
- **GroupDocs.Search für Java** ≥ 25.4.  
- JDK 8 oder neuer, IDE (IntelliJ IDEA, Eclipse usw.).  
- Grundkenntnisse in Java und Maven.  

## GroupDocs.Search für Java einrichten

Fügen Sie die Bibliothek Ihrem Projekt mit einer der untenstehenden Methoden hinzu.

**Maven‑Setup:**

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
Erhalten Sie eine Testlizenz oder kaufen Sie eine Lizenz über die [Lizenzierungsseite](https://purchase.groupdocs.com/temporary-license/).

## Wie man einen benutzerdefinierten Logger für GroupDocs.Search erstellt
GroupDocs.Search ermöglicht das Einbinden beliebiger Implementierungen des `ILogger`‑Interfaces. Durch das Erweitern von `FileLogger` oder `ConsoleLogger` können Sie zusätzliches Verhalten hinzufügen – etwa das Rotieren der Logdatei oder das Weiterleiten von Nachrichten an einen Remote‑Monitoring‑Dienst. Diese Flexibilität ist der Grund, warum viele Teams **benutzerdefinierte Logger** erstellen, die ihren betrieblichen Anforderungen entsprechen.

## Wie man die Logdateigröße mit dem File Logger begrenzt
Im Folgenden finden Sie eine Schritt‑für‑Schritt‑Anleitung, wie Sie den **File Logger** so konfigurieren, dass die Logdatei niemals die von Ihnen angegebene Größe überschreitet.

### 1️⃣ Notwendige Pakete importieren
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Index‑Einstellungen mit File Logger festlegen
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Index erstellen oder laden
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Dokumente zum Index hinzufügen
```java
index.add(documentsFolder);
```

### 5️⃣ Suchabfrage ausführen
```java
SearchResult result = index.search(query);
```

**Wichtiger Hinweis:** Das zweite Argument des `FileLogger`‑Konstruktors (`4.0`) definiert die **maximale Loggröße** in Megabyte und erfüllt damit die Anforderung **Logdateigröße begrenzen**.

## Wie man den Console Logger in Java verwendet
Wenn Sie sofortiges Feedback im Terminal bevorzugen, ersetzen Sie den File Logger durch einen Console Logger.

### 1️⃣ Console Logger importieren
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Index‑Einstellungen mit Console Logger festlegen
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Index erstellen oder laden
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Dokumente hinzufügen und Suche ausführen
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tipp:** Der Console Logger ist während der Entwicklung ideal, weil er jeden Log‑Eintrag sofort ausgibt und Ihnen hilft zu überprüfen, ob Indexierung und Suche wie erwartet funktionieren.

## Praktische Anwendungsfälle
1. **Dokumenten‑Management‑Systeme:** Audit‑Trails für jedes indizierte Dokument führen.  
2. **Enterprise‑Suchmaschinen:** Abfrage‑Performance und Fehlerraten in Echtzeit überwachen.  
3. **Legal‑ & Compliance‑Software:** Suchbegriffe für regulatorische Berichte protokollieren.

## Leistungsüberlegungen
- **Loggröße:** Durch **maximale Loggröße setzen** vermeiden Sie übermäßigen Festplattenverbrauch, der Ihre Anwendung verlangsamen könnte.  
- **Asynchrones Logging:** Für höhere Durchsatzraten können Sie den Logger in eine asynchrone Warteschlange einbinden (nicht Teil dieses Leitfadens).  
- **Speichermanagement:** Große `Index`‑Objekte freigeben, sobald sie nicht mehr benötigt werden, um den JVM‑Footprint gering zu halten.

## Häufige Probleme & Lösungen
- **Log‑Pfad nicht zugänglich:** Stellen Sie sicher, dass das Verzeichnis existiert und die Anwendung Schreibrechte hat.  
- **Logger wird nicht ausgelöst:** Rufen Sie `settings.setLogger(...)` *vor* der Erstellung des `Index`‑Objekts auf.  
- **Keine Konsolenausgabe:** Vergewissern Sie sich, dass Sie die Anwendung in einem Terminal ausführen, das `System.out` anzeigt.

## Häufig gestellte Fragen

**F: Was steuert der zweite Parameter von `FileLogger`?**  
A: Er legt die maximale Größe der Logdatei in Megabyte fest und ermöglicht das **setzen der maximalen Loggröße**.

**F: Kann ich Datei‑ und Console‑Logger kombinieren?**  
A: Ja, indem Sie einen benutzerdefinierten Logger erstellen, der Nachrichten an beide Ziele weiterleitet.

**F: Wie füge ich nach der Erst­erstellung Dokumente zum Index hinzu?**  
A: Rufen Sie jederzeit `index.add(pathToNewDocs)` auf; der Logger protokolliert den Vorgang.

**F: Ist `ConsoleLogger` thread‑sicher?**  
A: Er schreibt direkt nach `System.out`, das von der JVM synchronisiert wird, sodass er für die meisten Anwendungsfälle sicher ist.

**F: Beeinflusst das Begrenzen der Logdateigröße die Menge der gespeicherten Informationen?**  
A: Sobald das Größenlimit erreicht ist, können neue Einträge verworfen oder die Datei **rotiert** werden, abhängig von der Logger‑Implementierung.

## Ressourcen
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Zuletzt aktualisiert:** 2026-02-24  
**Getestet mit:** GroupDocs.Search für Java 25.4  
**Autor:** GroupDocs  

---