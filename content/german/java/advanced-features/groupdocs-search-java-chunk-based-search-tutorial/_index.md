---
date: '2026-02-21'
description: Erfahren Sie, wie Sie Dokumente zum Index hinzufügen und die Suchleistung
  mit Chunk‑basierter Suche in Java mithilfe von GroupDocs.Search steigern, indem
  Sie den Speicher des Java‑Suchindexes für große Dokumentensätze optimieren.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Dokumente zum Index hinzufügen mit Chunk-basierter Suche in Java
type: docs
url: /de/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Dokumente zum Index hinzufügen mit Chunk-basierter Suche in Java

In modernen Anwendungen, die **Dokumente zum Index hinzufügen** schnell benötigen und dann schnelle, chunk‑basierte Abfragen ausführen wollen, benötigen Sie eine Lösung, die skaliert, ohne den Speicher zu sprengen. Dieses Tutorial führt Sie durch die Einrichtung von GroupDocs.Search für Java, das Hinzufügen mehrerer Dokumentenordner und die Konfiguration der Engine, um **die Suchleistung zu erhöhen**, während die **java search index memory** Nutzung unter Kontrolle bleibt. Egal, ob Sie rechtliche Verträge, Support‑Tickets oder Forschungsarbeiten indexieren, die nachfolgenden Schritte bieten Ihnen eine produktionsreife Implementierung.

## Schnelle Antworten
- **Was ist der erste Schritt?** Erstellen Sie einen Suchindex‑Ordner.  
- **Wie kann ich viele Dateien einbinden?** Verwenden Sie `index.add()` für jeden Dokumentenordner.  
- **Welche Option aktiviert die Chunk‑Suche?** `options.setChunkSearch(true)`.  
- **Kann ich nach dem ersten Chunk weiter suchen?** Ja, rufen Sie `index.searchNext()` mit dem Token auf.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion oder eine temporäre Lizenz reicht für die Entwicklung; für die Produktion ist eine Voll‑Lizenz erforderlich.  

## Was Sie lernen werden
- Wie man einen Suchindex in einem angegebenen Ordner erstellt.  
- Schritte, um **Dokumente zum Index hinzufügen** aus mehreren Quellen.  
- Konfiguration der Suchoptionen, um Chunk‑basierte Suche zu aktivieren.  
- Durchführung initialer und nachfolgender Chunk‑basierter Suchen.  
- Praxisbeispiele, bei denen Chunk‑basierte Dokumentensuche glänzt.  

## Voraussetzungen
- **Required Libraries**: GroupDocs.Search for Java 25.4 or later.  
- **Environment Setup**: A compatible Java Development Kit (JDK) installed.  
- **Knowledge Prerequisites**: Basic Java programming and Maven familiarity.

## Einrichtung von GroupDocs.Search für Java
Um zu beginnen, integrieren Sie GroupDocs.Search in Ihr Projekt mittels Maven:

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

Alternativ laden Sie die neueste Version von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunter.

### Lizenzbeschaffung
Um GroupDocs.Search auszuprobieren:

- **Free Trial** – testen Sie Kernfunktionen ohne Verpflichtung.  
- **Temporary License** – erweiterter Zugriff für die Entwicklung.  
- **Purchase** – Voll‑Lizenz für den Produktionseinsatz.

### Grundlegende Initialisierung und Einrichtung
Erstellen Sie einen Index in dem Ordner, in dem die durchsuchbaren Daten gespeichert werden sollen:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Wie man Dokumente zum Index hinzufügt
Jetzt, wo der Index existiert, ist der nächste logische Schritt, **Dokumente zum Index hinzufügen** aus den Speicherorten, an denen Ihre Dateien liegen.

### 1. Erstellen eines Index
**Übersicht**: Richten Sie ein Verzeichnis für den Suchindex ein.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Dokumente zum Index hinzufügen
**Übersicht**: Laden Sie Dateien aus mehreren Quellordnern.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Konfiguration der Suchoptionen für Chunk‑Suche
Aktivieren Sie die Chunk‑basierte Suche, indem Sie das Options‑Objekt anpassen.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Ausführen einer initialen Chunk‑basierten Suche
Führen Sie die erste Abfrage mit den aktivierten Chunk‑Optionen aus.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Fortsetzen der Chunk‑basierten Suche
Iterieren Sie über die verbleibenden Chunks, bis die Suche abgeschlossen ist.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Warum Chunk‑basierte Suche verwenden?
Chunk‑basierte Suche zerlegt massive Dokumentensammlungen in handhabbare Stücke, reduziert den Speicherbedarf und beschleunigt die Antwortzeiten. Besonders vorteilhaft ist sie, wenn:

1. **Legal teams** need to locate specific clauses across thousands of contracts.  
2. **Customer support portals** must surface relevant knowledge‑base articles instantly.  
3. **Researchers** sift through extensive datasets without loading entire files into memory.

## Wie dieser Ansatz **die Suchleistung erhöht**
Durch das Durchsuchen kleinerer Chunks statt ganzer Dateien kann die Engine:

- Irrelevante Abschnitte frühzeitig überspringen und CPU‑Zyklen sparen.  
- Nur den aktiven Chunk im Speicher halten, wodurch der **java search index memory** Verbrauch direkt sinkt.  
- Chunk‑Verarbeitung auf Mehrkernmaschinen parallelisieren für schnellere Ergebnisse.

## Verwaltung von **java search index memory**
Obwohl Chunk‑basierte Suche bereits den Speicherbedarf reduziert, können Sie die JVM weiter optimieren:

- Genügend Heap zuweisen (`-Xmx2g` oder höher) abhängig von der Indexgröße.  
- `index.optimize()` nach Masseneinfügungen ausführen, um die Indexstruktur zu komprimieren.  
- GC‑Pausen mit Tools wie VisualVM überwachen, um Latenzspitzen zu vermeiden.

## Leistungsüberlegungen
- **Memory Management** – Genügend Heap‑Speicher (`-Xmx`) für große Indexe bereitstellen.  
- **Resource Monitoring** – CPU‑Auslastung während Indexierung und Suche im Auge behalten.  
- **Index Maintenance** – Index regelmäßig neu aufbauen oder bereinigen, um veraltete Daten zu entfernen.

## Häufige Fallstricke & Fehlersuche
| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## Häufig gestellte Fragen

**Q: Was ist Chunk‑basierte Suche?**  
A: Chunk‑basierte Suche teilt den Datensatz in kleinere Stücke, wodurch effiziente Abfragen über große Datenmengen möglich sind, ohne ganze Dokumente in den Speicher zu laden.

**Q: Wie aktualisiere ich meinen Index mit neuen Dateien?**  
A: Rufen Sie einfach `index.add()` mit dem Pfad zu den neuen Dokumenten auf; der Index integriert sie automatisch.

**Q: Kann GroupDocs.Search verschiedene Dateiformate verarbeiten?**  
A: Ja, es unterstützt PDFs, DOCX, XLSX, PPTX und viele andere gängige Formate.

**Q: Was sind typische Leistungsengpässe?**  
A: Speicherbeschränkungen und nicht optimierte Indexe sind die häufigsten; weisen Sie ausreichend Heap zu und optimieren Sie den Index regelmäßig.

**Q: Wo finde ich ausführlichere Dokumentation?**  
A: Besuchen Sie die offizielle [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) für detaillierte Anleitungen und API‑Referenzen.

**Q: Funktioniert Chunk‑basierte Suche mit verschlüsselten PDFs?**  
A: Ja, solange Sie das Passwort über die entsprechende API‑Überladung bereitstellen.

**Q: Wie kann ich den Fortschritt der Indexierung überwachen?**  
A: Verwenden Sie die `Index.add()`‑Überladung, die ein `Progress`‑Objekt zurückgibt, oder binden Sie Logging‑Callbacks ein.

## Ressourcen
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Zuletzt aktualisiert:** 2026-02-21  
**Getestet mit:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs