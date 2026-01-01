---
date: '2025-12-19'
description: Erfahren Sie, wie Sie Dokumente zum Index hinzufügen und die Chunk‑basierte
  Suche in Java mit GroupDocs.Search aktivieren, um die Leistung bei großen Dokumentensammlungen
  zu steigern.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Dokumente zum Index hinzufügen mit chunkbasierter Suche in Java
type: docs
url: /de/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Dokumente zum Index hinzufügen mit Chunk-basierter Suche in Java

In der heutigen datengetriebenen Welt ist es entscheidend, **add documents to index** schnell durchführen zu können und anschließend Chunk‑basierte Suchen auszuführen. Das ist für jede Anwendung wichtig, die große Dateisammlungen verarbeitet. Egal, ob Sie mit Rechtsverträgen, Kunden‑Support‑Archiven oder riesigen Forschungsbibliotheken arbeiten – dieses Tutorial zeigt Ihnen genau, wie Sie GroupDocs.Search für Java einrichten, um Dokumente effizient zu indexieren und relevante Informationen in handlichen Chunks abzurufen.

## Was Sie lernen werden
- Wie man einen Such‑Index in einem angegebenen Ordner erstellt.  
- Schritte zum **add documents to index** aus mehreren Quellen.  
- Konfiguration von Suchoptionen, um Chunk‑basierte Suche zu aktivieren.  
- Durchführung einer ersten und nachfolgenden Chunk‑basierter Suche.  
- Praxisbeispiele, bei denen Chunk‑basierte Dokumentensuche glänzt.

## Schnellantworten
- **Was ist der erste Schritt?** Einen Such‑Index‑Ordner erstellen.  
- **Wie füge ich viele Dateien hinzu?** `index.add()` für jeden Dokumenten‑Ordner verwenden.  
- **Welche Option aktiviert die Chunk‑Suche?** `options.setChunkSearch(true)`.  
- **Kann ich nach dem ersten Chunk weiter suchen?** Ja, rufen Sie `index.searchNext()` mit dem Token auf.  
- **Benötige ich eine Lizenz?** Eine kostenlose Test‑ oder temporäre Lizenz reicht für die Entwicklung; für die Produktion ist eine Voll‑Lizenz erforderlich.

## Voraussetzungen
Um diesem Leitfaden zu folgen, stellen Sie sicher, dass Sie:

- **Erforderliche Bibliotheken**: GroupDocs.Search für Java 25.4 oder neuer.  
- **Umgebungs‑Setup**: Ein kompatibles Java Development Kit (JDK) installiert.  
- **Kenntnis‑Voraussetzungen**: Grundlegende Java‑Programmierung und Maven‑Kenntnisse.

## GroupDocs.Search für Java einrichten
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

- **Free Trial** – Kernfunktionen ohne Verpflichtung testen.  
- **Temporary License** – Erweiterter Zugriff für die Entwicklung.  
- **Purchase** – Voll‑Lizenz für den Produktionseinsatz.

### Grundlegende Initialisierung und Setup
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
Jetzt, wo der Index existiert, ist der nächste logische Schritt, **add documents to index** aus den Speicherorten Ihrer Dateien hinzuzufügen.

### 1. Erstellen eines Index
**Übersicht**: Ein Verzeichnis für den Such‑Index einrichten.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Dokumente zum Index hinzufügen
**Übersicht**: Dateien aus mehreren Quellordnern einbinden.

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

### 3. Suchoptionen für Chunk‑Suche konfigurieren
Aktivieren Sie die Chunk‑basierte Suche, indem Sie das Options‑Objekt anpassen.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Erste Chunk‑basierte Suche durchführen
Führen Sie die erste Abfrage mit den aktivierten Chunk‑Optionen aus.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Chunk‑basierte Suche fortsetzen
Iterieren Sie über die verbleibenden Chunks, bis die Suche abgeschlossen ist.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Warum Chunk‑basierte Suche verwenden?
Chunk‑basierte Suche zerlegt massive Dokumentensammlungen in handhabbare Stücke, reduziert den Speicherverbrauch und beschleunigt die Antwortzeiten. Besonders vorteilhaft ist sie, wenn:

1. **Legal Teams** spezifische Klauseln in Tausenden von Verträgen finden müssen.  
2. **Customer Support Portale** sofort relevante Knowledge‑Base‑Artikel bereitstellen sollen.  
3. **Researchers** umfangreiche Datensätze durchsuchen, ohne ganze Dateien in den Speicher zu laden.

## Leistungsüberlegungen
- **Speicherverwaltung** – Weisen Sie ausreichend Heap‑Speicher (`-Xmx`) für große Indizes zu.  
- **Ressourcen‑Monitoring** – Behalten Sie die CPU‑Auslastung während Index‑ und Suchvorgängen im Auge.  
- **Index‑Wartung** – Rebuilden oder bereinigen Sie den Index regelmäßig, um veraltete Daten zu entfernen.

## Häufige Stolperfallen & Fehlersuche
| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| `OutOfMemoryError` während des Indexierens | Heap‑Größe zu klein | JVM‑Heap erhöhen (`-Xmx2g` oder höher) |
| Keine Ergebnisse | Chunk‑Token nicht verarbeitet | Sicherstellen, dass die `while`‑Schleife bis `getNextChunkSearchToken()` `null` läuft |
| Langsame Suchleistung | Index nicht optimiert | `index.optimize()` nach Bulk‑Additionen ausführen |

## Häufig gestellte Fragen

**F: Was ist Chunk‑basierte Suche?**  
A: Chunk‑basierte Suche teilt den Datensatz in kleinere Stücke, wodurch effiziente Abfragen über große Datenmengen möglich sind, ohne gesamte Dokumente in den Speicher zu laden.

**F: Wie aktualisiere ich meinen Index mit neuen Dateien?**  
A: Rufen Sie einfach `index.add()` mit dem Pfad zu den neuen Dokumenten auf; der Index integriert sie automatisch.

**F: Kann GroupDocs.Search verschiedene Dateiformate verarbeiten?**  
A: Ja, es unterstützt PDFs, DOCX, XLSX, PPTX und viele andere gängige Formate.

**F: Was sind typische Leistungsengpässe?**  
A: Speicherbeschränkungen und nicht optimierte Indizes sind die häufigsten; ausreichend Heap zuweisen und den Index regelmäßig optimieren.

**F: Wo finde ich ausführlichere Dokumentation?**  
A: Besuchen Sie die offizielle [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) für detaillierte Anleitungen und API‑Referenzen.

## Ressourcen
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Zuletzt aktualisiert:** 2025-12-19  
**Getestet mit:** GroupDocs.Search 25.4 für Java  
**Autor:** GroupDocs  

---