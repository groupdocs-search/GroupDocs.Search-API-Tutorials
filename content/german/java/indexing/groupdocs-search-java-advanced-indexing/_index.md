---
date: '2026-08-15'
description: Erfahren Sie, wie Sie die search latency mit den advanced indexing-Funktionen
  von GroupDocs.Search for Java verbessern können, einschließlich cancellation, async
  operations, multithreading und metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Verbessern Sie die search latency mit GroupDocs.Search for Java durch
  die Verwendung von cancellation, asynchronous indexing, multithreading und metadata
  customization. Steigern Sie die Leistung und reduzieren Sie den Ressourcenverbrauch.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Verbessern Sie die search latency mit advanced indexing in GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Verbessern Sie die search latency mit advanced indexing in GroupDocs
type: docs
url: /de/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Verbessern Sie die Suchlatenz mit fortschrittlicher Indizierung in GroupDocs

In der heutigen schnelllebigen digitalen Umgebung ist **Suchlatenz verbessern** entscheidend, um den Benutzern sofortige Ergebnisse zu liefern. Egal, ob Sie eine benutzerdefinierte Suchmaschine bauen oder ein bestehendes Dokumenten‑Management‑System erweitern, die richtige Indexierungsstrategie kann die Latenz dramatisch senken, den Ressourcenverbrauch reduzieren und **Suchlatenz verbessern** überall. In diesem Tutorial führen wir Sie durch die leistungsstärksten Funktionen von GroupDocs.Search für Java – Abbruch, asynchrone Indexierung, Multithreading und Metadaten‑Anpassung – sodass Sie **Dokumente zum Index hinzufügen** schneller und effizienter können.

**Was Sie lernen werden**

- Wie man einen Indexierungsvorgang nach einer festgelegten Zeit abbricht  
- Durchführen asynchroner Indexierungsoperationen und Handhabung von Statusänderungen  
- Konfiguration von Multithreading für schnellere Indexierung  
- Anpassen der Metadaten‑Indexierungsoptionen, um **Suchmetadaten anzupassen**  

Stellen wir sicher, dass Sie alles haben, was Sie benötigen, bevor wir in den Code eintauchen.

## Schnelle Antworten
- **Was bewirkt der Abbruch?** Er stoppt die Indexierung nach einem festgelegten Timeout und gibt CPU und Speicher für andere Aufgaben frei.  
- **Kann ich Dokumente asynchron indexieren?** Ja – aktivieren Sie es mit `options.setAsync(true)`.  
- **Wie viele Threads kann ich verwenden?** Jede positive ganze Zahl; 2‑4 Threads sind für die meisten Server üblich.  
- **Ist die Metadaten‑Indexierung optional?** Absolut – Sie können sie pro Feld aktivieren oder feinjustieren.  
- **Benötige ich eine Lizenz für diese Funktionen?** Eine Testversion reicht für Tests; für die Produktion ist eine Voll‑Lizenz erforderlich.

## Voraussetzungen

- **GroupDocs.Search library** – Version 25.4 oder neuer.  
- **Java Development Environment** – JDK 8 oder höher wird empfohlen.  
- Grundlegende Kenntnisse in Java und dem Konzept der Indexierung.

### Einrichtung von GroupDocs.Search für Java

#### Maven-Installation

Fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml`‑Datei hinzu:

`pom.xml`‑Konfiguration teilt Maven mit, welche GroupDocs.Search‑Artefakte heruntergeladen und in Ihr Projekt eingebunden werden sollen.

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

#### Direkter Download

Laden Sie alternativ das neueste JAR von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunter.

**License acquisition** – Beginnen Sie mit einer kostenlosen Testversion oder beantragen Sie eine temporäre Lizenz, um das vollständige Funktionsset freizuschalten.

### Grundlegende Initialisierung und Einrichtung

Die Klasse `SearchIndex` ist der Einstiegspunkt, der einen durchsuchbaren Index darstellt, der auf Festplatte oder im Speicher gespeichert wird.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Was bedeutet „Suchleistung optimieren“ in diesem Kontext?

Die Optimierung der Suchleistung bedeutet, den Indexierungsprozess so zu konfigurieren, dass er die richtige Menge an CPU, Speicher und Zeit verbraucht, während er gleichzeitig die relevantesten Ergebnisse sofort liefert. Durch die Steuerung von Abbruch, asynchroner Ausführung, Thread‑Management und Metadaten‑Handling beeinflussen Sie direkt, wie schnell die Engine **Dokumente zum Index hinzufügen** und auf Abfragen reagieren kann.

## Warum fortschrittliche Indexierungsfunktionen verwenden?

Asynchrone und multithreaded Indexierung halten Ihre Anwendung reaktionsfähig, während der Abbruch runaway‑Prozesse verhindert. Feinabgestimmte Metadaten‑Optionen ermöglichen es, die wichtigsten Informationen hervorzuheben, was **Suchlatenz verbessern** für Endbenutzer direkt bewirkt. Zusätzlich reduzieren diese Funktionen CPU‑Spitzen, senken den Speicher‑Druck und ermöglichen ein reibungsloses Skalieren bei großen Dokumentenmengen.

## Wie kann man die Suchlatenz mit fortschrittlicher Indexierung verbessern?

Laden Sie Ihre `SearchIndex`‑Instanz, konfigurieren Sie `IndexingOptions` mit Abbruch, Async‑ und Thread‑Einstellungen und rufen Sie `index.add(document)` auf – diese Kombination reduziert die gesamte Indexierungszeit um bis zu 60 % bei typischen Workloads und stellt sicher, dass langlaufende Jobs andere Vorgänge nicht blockieren. Sie können zudem die Metadaten‑Indexierungsgrenzen anpassen und den Fortschritt über Status‑Changed‑Events überwachen, um sicherzustellen, dass die Pipeline innerhalb der Leistungsbudgets bleibt.

## Implementierungsleitfaden

### Abbruch‑Eigenschaft

**Übersicht** – Indexierung nach einer festgelegten Dauer abbrechen, um eine Überbeanspruchung von Ressourcen zu vermeiden.

#### Schritt 1: Umgebung einrichten

Erstellen Sie eine `SearchIndex`‑Instanz, die auf Ihren Index‑Ordner zeigt.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Schritt 2: Indexierungsoptionen mit Abbruch erstellen

`IndexingOptions` ermöglicht es Ihnen, das Verhalten der Indexierungs‑Engine festzulegen.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Wichtige Punkte**

- `setCancellation()` aktiviert die Funktion.  
- `cancelAfter(int milliseconds)` definiert das Timeout (in diesem Beispiel 3 Sekunden).

### Asynchrone Eigenschaft

**Übersicht** – Indexierung in einem Hintergrund‑Thread ausführen und auf Statusänderungen hören.

#### Schritt 1: Umgebung einrichten

Instanziieren Sie den Index und bereiten Sie die Dokumentensammlung vor.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Schritt 2: Ereignis für Statusänderungen abonnieren

Das `StatusChanged`‑Event benachrichtigt Sie, wenn der Indexierungs‑Job zwischen Zuständen wechselt.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Schritt 3: Asynchrone Optionen konfigurieren

Aktivieren Sie den Async‑Modus, sodass der Aufruf sofort zurückkehrt und die Verarbeitung im Hintergrund weiterläuft.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Thread‑Eigenschaft

**Übersicht** – Indexierung beschleunigen, indem mehrere CPU‑Kerne genutzt werden.

#### Schritt 1: Umgebung einrichten

Bereiten Sie den Index vor und stellen Sie sicher, dass die JVM über ausreichend Heap‑Speicher verfügt.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Schritt 2: Multithreading konfigurieren

Legen Sie die Anzahl der Worker‑Threads fest; jeder Thread verarbeitet einen Teil der Dokumente.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metadaten‑Indexierungsoptionen‑Eigenschaft

**Übersicht** – Feinabstimmung, welche Dokumenten‑Metadaten indexiert werden und wie sie gespeichert werden.

#### Schritt 1: Umgebung einrichten

Laden Sie ein Dokument, das Metadaten‑Felder wie Autor, Titel und benutzerdefinierte Tags enthält.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Schritt 2: Metadaten‑Optionen konfigurieren

`MetadataIndexingOptions` ermöglicht das Aktivieren oder Deaktivieren einzelner Metadaten‑Felder und das Festlegen von Größen‑Grenzwerten.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Praktische Anwendungen

1. **Document management systems** – Verwenden Sie asynchrone Indexierung, um die UI reaktionsfähig zu halten, während große Stapel im Hintergrund verarbeitet werden.  
2. **Content search engines** – Setzen Sie den Abbruch ein, um zu verhindern, dass langlaufende Jobs während Spitzenlasten Server‑Ressourcen beanspruchen.  
3. **Large‑scale ingestion pipelines** – Nutzen Sie Multithreading, um **Dokumente zum Index hinzufügen** in großem Maßstab zu ermöglichen und die Verarbeitungszeit drastisch zu verkürzen.  

## Leistungsüberlegungen

- **Thread management** – CPU‑Auslastung überwachen; zu viele Threads können Overhead durch Kontextwechsel verursachen.  
- **Memory footprint** – Metadaten‑Grenzwerte (z. B. `setMaxBytesToIndexField`) halten den Speicherverbrauch vorhersehbar.  
- **Garbage collection** – Verwenden Sie geeignete JVM‑Flags (`-Xmx`, `-XX:+UseG1GC`) beim Indexieren riesiger Korpora.  

## Häufige Probleme und Lösungen

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Indexierung endet nie | Abbruch zu niedrig eingestellt | Erhöhen Sie den Wert von `cancelAfter` oder entfernen Sie den Abbruch für lange Jobs |
| Keine Statusupdates im Async‑Modus | Ereignis‑Handler nicht korrekt angebunden | Stellen Sie sicher, dass `index.getEvents().StatusChanged.add(...)` vor `index.add` aufgerufen wird |
| Out‑of‑Memory‑Fehler | Zu viele Threads oder hohe Metadaten‑Grenzwerte | Reduzieren Sie `options.setThreads` und senken Sie die Metadaten‑Feld‑Grenzwerte |
| Fehlende Metadaten in den Ergebnissen | Metadaten‑Indexierung deaktiviert | Überprüfen Sie, dass `options.getMetadataIndexingOptions()` konfiguriert ist und nicht auf das Ignorieren von Feldern gesetzt ist |

## Häufig gestellte Fragen

**Q: Wie erhalte ich eine temporäre Lizenz für GroupDocs.Search?**  
A: Besuchen Sie die [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) und folgen Sie den Anweisungen auf dem Bildschirm.

**Q: Kann ich einen Indexierungsvorgang mitten im Prozess abbrechen?**  
A: Ja – verwenden Sie die Abbruch‑Eigenschaft mit `cancelAfter()` oder rufen Sie programmgesteuert `Cancellation.cancel()` auf.

**Q: Welche Anwendungsfälle gibt es für asynchrone Indexierung?**  
A: Echtzeit‑Dokumentenabruf, Hintergrund‑Batch‑Verarbeitung und UI‑responsive Anwendungen profitieren von asynchroner Indexierung.

**Q: Ist es sicher, die Thread‑Anzahl auf einem geteilten Server zu erhöhen?**  
A: Erhöhen Sie schrittweise und überwachen Sie die CPU‑Last; in stark geteilten Umgebungen sollte die Thread‑Anzahl moderat bleiben (2‑4).

**Q: Wie wirkt sich die Metadaten‑Indexierung auf die Suchrelevanz aus?**  
A: Richtig indexierte Metadaten (Autor, Erstellungsdatum, Tags) können in Abfragen höher gewichtet werden, wodurch die Ergebnisgenauigkeit steigt.

## Fazit

Durch die Nutzung dieser fortschrittlichen Funktionen von GroupDocs.Search für Java werden Sie **Suchlatenz verbessern** in einer Vielzahl von Szenarien – von schneller Dokumentenaufnahme bis hin zu feinkörniger Metadaten‑Steuerung. Experimentieren Sie mit verschiedenen Konfigurationen, überwachen Sie den Ressourcenverbrauch und passen Sie die Einstellungen an Ihre spezifische Arbeitslast an, um die besten Ergebnisse zu erzielen.

---

**Zuletzt aktualisiert:** 2026-08-15  
**Getestet mit:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [How to Add Multiple Aliases and Add Documents to Index in GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)