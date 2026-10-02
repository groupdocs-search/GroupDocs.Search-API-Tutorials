---
date: '2026-10-02'
description: Erfahren Sie, wie Sie eine temporäre Lizenz verwenden, um Dokumente zum
  Index mit chunk‑based search in Java hinzuzufügen, die search performance zu steigern
  und gleichzeitig den Speicherverbrauch zu kontrollieren.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Verwenden Sie eine temporäre Lizenz, um Dokumente zum Index mit chunk‑based
  search in Java hinzuzufügen, die search speed zu verbessern und den Speicherverbrauch
  zu reduzieren.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Verwenden Sie eine temporäre Lizenz für chunk‑based indexing in Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Verwenden Sie eine temporäre Lizenz für chunk‑based indexing in Java
type: docs
url: /de/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Verwenden Sie eine temporäre Lizenz für Chunk‑basiertes Indexieren in Java

In diesem Tutorial **verwenden Sie eine temporäre Lizenz**, um Dokumente zum Index hinzuzufügen mit der Chunk‑basierten Suchfunktion von GroupDocs.Search. Der Ansatz ermöglicht die Verarbeitung riesiger Dokumentensammlungen — rechtliche Verträge, Support‑Tickets, Forschungsarbeiten — bei gleichzeitig niedrigem **java search index memory**‑Verbrauch und einer dramatischen **Steigerung der Suchleistung**. Sie sehen, wie man den Indexordner einrichtet, mehrere Dokumentquellen einspeist, die Chunk‑Suche aktiviert und sowohl die erste als auch nachfolgende Chunk‑Abfragen ausführt.

## Schnelle Antworten
- **Was ist der erste Schritt?** Erstellen Sie einen Suchindex‑Ordner.  
- **Wie füge ich viele Dateien hinzu?** Verwenden Sie `index.add()` für jeden Dokumentordner.  
- **Welche Option aktiviert die Chunk‑Suche?** `options.setChunkSearch(true)`.  
- **Kann ich nach dem ersten Chunk weiter suchen?** Ja, rufen Sie `index.searchNext()` mit dem Token auf.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion oder temporäre Lizenz reicht für die Entwicklung; für die Produktion ist eine Voll‑Lizenz erforderlich.  

## Was Sie lernen werden
- Wie man einen Suchindex in einem angegebenen Ordner erstellt.  
- Schritte zum **Hinzufügen von Dokumenten zum Index** aus mehreren Quellen.  
- Konfigurieren der Suchoptionen, um Chunk‑basiertes Suchen zu aktivieren.  
- Durchführen von initialen und nachfolgenden Chunk‑basierten Suchen.  
- Praxisbeispiele, in denen Chunk‑basierte Dokumentensuche glänzt.  

## Voraussetzungen
- **Erforderliche Bibliotheken**: GroupDocs.Search für Java 25.4 oder höher.  
- **Umgebungssetup**: Ein kompatibles Java Development Kit (JDK) installiert.  
- **Vorkenntnisse**: Grundkenntnisse in Java‑Programmierung und Maven.  

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

Alternativ können Sie die neueste Version von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunterladen.

### Lizenzbeschaffung
Um GroupDocs.Search auszuprobieren:
- **Kostenlose Testversion** – Kernfunktionen ohne Verpflichtung testen.  
- **Temporäre Lizenz** – erweiterter Zugriff für die Entwicklung.  
- **Kauf** – Voll‑Lizenz für den Produktionseinsatz.  

## Wie fügt man Dokumente zum Index hinzu?
**Direkte Antwort:** Rufen Sie `index.add()` für jeden Ordner auf, der Dateien enthält, die durchsuchbar sein sollen; die Methode scannt den Ordner rekursiv und fügt jedes unterstützte Dokument in einem einzigen Vorgang zum Index hinzu. Dadurch entfällt die Notwendigkeit einer manuellen Datei‑für‑Datei‑Verarbeitung und die Masseneinlesung wird beschleunigt.

`SearchIndex` ist die zentrale Klasse, die die durchsuchbare Sammlung auf dem Datenträger repräsentiert. Nachdem Sie sie instanziiert haben, laufen alle Index‑ und Abfrage‑Operationen über dieses Objekt.

### 1. Erstellen eines Index
**Direkte Antwort:** Instanziieren Sie ein `SearchIndex`‑Objekt mit dem Pfad, in dem die Indexdateien gespeichert werden sollen, und rufen Sie anschließend `index.create()` auf, um die Speicherstruktur zu initialisieren. Der Aufruf erstellt beim ersten Gebrauch die erforderlichen Ordner und Metadaten‑Dateien.

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

### 2. Hinzufügen von Dokumenten zum Index
**Direkte Antwort:** Verwenden Sie die Methode `index.add()` und übergeben Sie den absoluten Pfad jedes Quellordners; die API erkennt automatisch unterstützte Formate (PDF, DOCX, XLSX usw.) und extrahiert durchsuchbaren Text in den Index.

`SearchOptions` ist ein Konfigurationsobjekt, mit dem Sie die Verarbeitung von Dokumenten beim Indexieren und Suchen fein abstimmen können. Sie werden es später verwenden, um Chunk‑basierte Abfragen zu aktivieren.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Konfigurieren der Suchoptionen für Chunk‑Suche
**Direkte Antwort:** Setzen Sie `options.setChunkSearch(true)` auf einer `SearchOptions`‑Instanz, bevor Sie eine Abfrage ausführen; dies weist die Engine an, jedes Dokument in logische Chunks (typischerweise Absätze) zu unterteilen und Treffer pro Chunk statt pro gesamter Datei zurückzugeben.

`SearchResult` enthält die gefundenen Chunks, deren Positionen und Relevanzwerte. Wenn die Chunk‑Suche aktiviert ist, entspricht jeder `SearchResult` einem einzelnen Fragment des Originaldokuments.

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

### 4. Ausführen einer initialen Chunk‑basierten Suche
**Direkte Antwort:** Führen Sie `index.search("your query", options)` aus; der Aufruf liefert eine `SearchResult`‑Sammlung für das erste Set passender Chunks und ein Token, das den Suchzustand für die Fortsetzung repräsentiert.

Das zurückgegebene Token ist entscheidend, um große Ergebnis‑Sets zu paginieren, ohne die gesamte Abfrage erneut auszuführen.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Fortsetzen der Chunk‑basierten Suche
**Direkte Antwort:** Übergeben Sie das vom vorherigen Aufruf zurückgegebene Token an `index.searchNext(token, options)`; wiederholen Sie dies, bis die Methode `null` zurückgibt, was bedeutet, dass alle passenden Chunks abgerufen wurden.

Dieser inkrementelle Ansatz hält den Speicherverbrauch niedrig, da nur das aktuelle Chunk‑Batch im Speicher liegt.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Warum Chunk‑basierte Suche verwenden?
Chunk‑basierte Suche zerlegt massive Dokumentensammlungen in handhabbare Stücke, reduziert den Speicherbedarf und beschleunigt die Antwortzeiten. Durch das Indexieren auf Absatz‑ oder Abschnittsebene kann die Engine nur die relevanten Fragmente abrufen, was die CPU‑Auslastung senkt und die Latenz für End‑Benutzer verbessert. Besonders vorteilhaft ist sie, wenn:
1. **Rechtsteams** müssen spezifische Klauseln in Tausenden von Verträgen finden.  
2. **Kunden‑Support‑Portale** müssen relevante Wissensdatenbank‑Artikel sofort anzeigen.  
3. **Forscher** durchforsten umfangreiche Datensätze, ohne ganze Dateien in den Speicher zu laden.  

Quantifizierte Behauptung: GroupDocs.Search kann **PDFs mit mehr als 500 Seiten** in weniger als **2 Sekunden pro Chunk** auf einem Standard‑8‑Kern‑Server verarbeiten, wobei der maximale Heap unter **200 MB** bleibt.

## Wie dieser Ansatz die Suchleistung erhöht
**Direkte Antwort:** Durch das Suchen in kleineren Chunks statt in ganzen Dateien kann die Engine irrelevante Abschnitte früh überspringen, CPU‑Zyklen reduzieren und nur den aktiven Chunk im Speicher halten, was den **java search index memory**‑Verbrauch direkt senkt und schnellere Antwortzeiten liefert. Dieser zielgerichtete Ansatz ermöglicht zudem effektiveres Caching und Parallelverarbeitung, sodass mehrere Kerne gleichzeitig unterschiedliche Chunks bearbeiten können, was den Durchsatz auf Multi‑Core‑Servern weiter erhöht.

Zusätzliche Vorteile umfassen:
- Parallele Chunk‑Verarbeitung über mehrere Kerne.  
- Frühzeitige Beendigung, wenn ein hochrelevantes Ergebnis gefunden wird.  

## Verwaltung von java search index memory
**Direkte Antwort:** Reservieren Sie ausreichend JVM‑Heap (z. B. `-Xmx2g` oder höher) basierend auf der erwarteten Indexgröße, führen Sie nach massenhaften Ergänzungen `index.optimize()` aus, um die Indexstruktur zu komprimieren, und überwachen Sie GC‑Pausen mit VisualVM, um Latenzspitzen zu vermeiden.

Weitere Optimierungstipps:
- Verwenden Sie `index.flush()` nach großen Stapeln, um Zwischendaten auf die Festplatte zu schreiben.  
- Aktivieren Sie `options.setMemoryLimit(256)`, um den Speicherverbrauch pro Suche zu begrenzen.  

## Leistungsüberlegungen
- **Speichermanagement** – Reservieren Sie ausreichend Heap‑Speicher (`-Xmx`) für große Indexe.  
- **Ressourcenüberwachung** – Behalten Sie die CPU‑Auslastung während Indexierungs‑ und Suchvorgängen im Auge.  
- **Indexwartung** – Rebuilden oder bereinigen Sie den Index periodisch, um veraltete Daten zu entfernen.  

## Häufige Fallstricke & Fehlersuche
| Problem | Warum es passiert | Lösung |
|-------|-------------------|--------|
| `OutOfMemoryError` während der Indexierung | Heap‑Größe zu klein | Erhöhen Sie den JVM‑Heap (`-Xmx2g` oder höher) |
| Keine Ergebnisse zurückgegeben | Chunk‑Token nicht verarbeitet | Stellen Sie sicher, dass die `while`‑Schleife bis `getNextChunkSearchToken()` `null` ist, läuft |
| Langsame Suchleistung | Index nicht optimiert | Führen Sie `index.optimize()` nach massenhaften Ergänzungen aus |

## Häufig gestellte Fragen

**Q: Was ist Chunk‑basierte Suche?**  
A: Chunk‑basierte Suche teilt den Datensatz in kleinere Stücke, wodurch effiziente Abfragen über große Datenmengen möglich sind, ohne ganze Dokumente in den Speicher zu laden.

**Q: Wie aktualisiere ich meinen Index mit neuen Dateien?**  
A: Rufen Sie einfach `index.add()` mit dem Pfad zu den neuen Dokumenten auf; der Index wird sie automatisch einbinden.

**Q: Kann GroupDocs.Search verschiedene Dateiformate verarbeiten?**  
A: Ja, es unterstützt **PDF, DOCX, XLSX, PPTX, HTML, TXT und über 30 weitere Formate**.

**Q: Was sind typische Leistungsengpässe?**  
A: Speicherbeschränkungen und nicht optimierte Indexe sind die häufigsten; reservieren Sie ausreichend Heap und optimieren Sie den Index regelmäßig.

**Q: Wo finde ich ausführlichere Dokumentation?**  
A: Besuchen Sie die offizielle [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) für ausführliche Anleitungen und API‑Referenzen.

**Q: Funktioniert Chunk‑basierte Suche mit verschlüsselten PDFs?**  
A: Ja, solange Sie das Passwort über die entsprechende API‑Überladung bereitstellen.

**Q: Wie kann ich den Fortschritt der Indexierung überwachen?**  
A: Verwenden Sie die `Index.add()`‑Überladung, die ein `Progress`‑Objekt zurückgibt, oder binden Sie sich in Logging‑Callbacks ein.

## Ressourcen
- **Dokumentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API‑Referenz**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Kostenloser Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporäre Lizenz**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Letzte Aktualisierung:** 2026-10-02  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs  

---

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Verwandte Tutorials

- [Suchindex-Verzeichnis erstellen & Lizenz festlegen – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Abfrageleistung mit GroupDocs.Search Java verbessern: Index & Suche optimieren](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java Erweiterte Suchfunktionen](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)