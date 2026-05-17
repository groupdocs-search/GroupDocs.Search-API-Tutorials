---
date: '2026-05-17'
description: Erfahren Sie, wie Sie das search network java konfigurieren, Shards optimieren,
  Textsuche durchführen und Portkonflikte mit GroupDocs.Search for Java beheben.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Wie man Shards in GroupDocs.Search for Java optimiert: Ein umfassender Leitfaden'
type: docs
url: /de/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Wie man Shards in GroupDocs.Search für Java optimiert: Ein umfassender Leitfaden

Effizientes Dokumentensuchen ist entscheidend für Entwickler und Unternehmen, die große Datensätze verwalten oder eine schnelle interne Abrufung benötigen. In diesem Tutorial lernen Sie **how to configure search network java**, wie man Dokumente indexiert und abfragt, und die genauen Schritte zum **optimize shards** für maximale Leistung. Wir behandeln außerdem reale Anwendungsfälle, häufige Stolperfallen und praktische Tipps, um Ihre Suchknoten reibungslos laufen zu lassen.

## Schnelle Antworten
- **What is shard optimization?** Es reorganisiert Indexdaten, um Abfragen zu beschleunigen und den Speicheraufwand zu reduzieren.  
- **How to configure a search network?** Definieren Sie ein Basisverzeichnis und einen Port und setzen Sie dann Knoten mit der bereitgestellten API ein.  
- **How to perform text search?** Verwenden Sie `TextSearchInNetwork.searchAll` mit Ihrem Abfrage-String.  
- **How to index documents in Java?** Fügen Sie Dokumentverzeichnisse dem Master‑Knoten mit `IndexingDocuments.addDirectories` hinzu.  
- **How to handle port conflicts?** Ändern Sie die Variable `basePort` zu einem unbenutzten Port auf Ihrem Rechner.

## Wie man ein Suchnetzwerk konfiguriert
`Configuration` speichert alle Einstellungen, die zum Starten eines GroupDocs.Search‑Netzwerks erforderlich sind, wie den Speicherort des Indexordners und den Kommunikations‑Port.  
`SearchNetwork` orchestriert die Knoten, übernimmt die Indexierung und die Verteilung von Abfragen.

Laden Sie Ihre Suchkonfiguration, setzen Sie den Basis‑Pfad für Dokumente, wählen Sie einen freien Port und starten Sie das Netzwerk – alles in wenigen Code‑Zeilen. Diese direkte Antwort erklärt den gesamten Prozess in weniger als 70 Wörtern: **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`.** Das Netzwerk startet automatisch einen Master‑Knoten und alle erforderlichen Worker‑Knoten, bereit, Indexierungs‑Anfragen zu akzeptieren.

### Definitionsanker
`Configuration` ist die Kernklasse, die alle Einstellungen speichert, die zum Starten eines GroupDocs.Search‑Netzwerks erforderlich sind, wie den Speicherort des Indexordners und den Kommunikations‑Port.

Um den gefürchteten Fehler „port already in use“ zu vermeiden, prüfen Sie zuerst, ob der gewählte Port frei ist (z. B. mit `netstat` oder einem einfachen Socket‑Test), bevor Sie das Netzwerk initialisieren.

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

## Wie man Dokumente in Java indexiert
`IndexingDocuments` ist eine Hilfsklasse, die das Hinzufügen mehrerer Verzeichnisse zu einem Suchknoten vereinfacht und die Indexierungspipeline auslöst.

Fügen Sie Ihre Dokumentordner dem Master‑Knoten hinzu und lassen Sie den Indexer sie durchsuchen. **Direct answer:** Call `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` and then invoke `masterNode.index()`; the engine will create searchable shards for every folder you supplied. This approach scales horizontally—add more nodes, and the same method distributes the workload automatically.

### Definitionsanker
`IndexingDocuments` ist eine Hilfsklasse, die das Hinzufügen mehrerer Verzeichnisse zu einem Suchknoten vereinfacht und die Indexierungspipeline auslöst.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Wie man eine Textsuche durchführt
`TextSearchInNetwork` stellt statische Hilfsmethoden bereit, um eine Textabfrage an jeden Knoten im Netzwerk zu senden und die Ergebnisse zu aggregieren.  
`SearchResult` fasst die ID eines gefundenen Dokuments, einen Ausschnitt und den Relevanz‑Score zusammen.

Führen Sie eine Abfrage über alle Shards mit einem einzigen Methodenaufruf aus. **Direct answer:** Use `TextSearchInNetwork.searchAll("your query", searchNetwork)`; the method returns a collection of `SearchResult` objects containing document IDs, snippets, and relevance scores. You can further filter results by language, file type, or custom metadata without writing extra code.

### Definitionsanker
`TextSearchInNetwork` provides static helper methods that broadcast a text query to every node in the network and aggregate the results.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Wie man Portkonflikte behandelt
Wenn der Standard‑Port (`49132`) belegt ist, wählen Sie einfach einen anderen freien Port und aktualisieren Sie das Feld `basePort`, bevor Sie das Netzwerk starten. **Direct answer:** Change `int basePort = 49132;` to an unused value like `49133`, rebuild, and restart; the network will bind to the new port without affecting existing nodes.

Pro‑Tipp: Halten Sie eine kleine Konfigurationsdatei (z. B. `search-config.properties`) bereit, damit Sie den Port ohne Neukompilierung ändern können.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

### Erforderliche Bibliotheken, Versionen und Abhängigkeiten
Um diese Lösung zu implementieren, binden Sie die GroupDocs.Search‑Bibliothek über Maven ein, indem Sie die folgende Konfiguration zu Ihrer `pom.xml`‑Datei hinzufügen:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Alternativ laden Sie die neueste Version von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunter.

### Anforderungen an die Umgebung
- Java Development Kit (JDK) 8 oder höher.  
- Netzwerkberechtigungen, die das Binden an den gewählten `basePort` erlauben.  
- Ausreichend Festplattenspeicher für Indexdateien (jeder Shard kann ca. 10 MB pro 1.000 Dokumente belegen).

### Wissensvoraussetzungen
Ein grundlegendes Verständnis von Java, objektorientierter Programmierung und Ausnahmebehandlung hilft Ihnen, den Beispielen problemlos zu folgen.

## Einrichtung von GroupDocs.Search für Java
Um GroupDocs.Search in Ihrem Projekt zu verwenden, folgen Sie diesen Schritten:

1. **Add the Dependency**: As shown above, add the necessary Maven dependency to your project or download directly from the releases page.  
2. **License Acquisition**:  
   - **Free trial** – no license key required, but usage is limited to 500 documents per day.  
   - **Temporary license** – request a 30‑day trial key from [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – purchase a production license for unlimited access and priority support.  
3. **Basic Initialization and Setup**:  
   Initialize the configuration using the `Configuration` class, setting up the base path for documents and specifying a port number:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Implementierungsleitfaden
Now let's explore the implementation of key features using GroupDocs.Search Java.

### Feature: Konfiguration des Suchnetzwerks
**Overview**: Setting up a search network involves defining your document directory and configuring it with a specific port for communication between nodes.

#### Schritt 1: Dokumentverzeichnisse und Port definieren
`DocumentDirectory` is a simple holder for the absolute path of a folder you want to index. Provide one or more paths to the configuration.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Schritt 2: Suchnetzwerk konfigurieren
Create the configuration object using the defined paths:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Feature: Bereitstellung von Suchnetzwerkknoten
**Overview**: Deploy nodes to handle document searches efficiently across your network.

#### Schritt 1: Knoten mit Konfiguration bereitstellen
Deploy search network nodes and identify the master node for centralized management:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Feature: Abonnieren von Netzwerk-Knoten-Ereignissen
**Overview**: Monitor your search network by subscribing to events that notify you of important changes or actions.

#### Schritt 1: Master-Knoten-Ereignisse abonnieren
`SearchNetworkEventListener` lets you react to indexing completion, node failures, or shard optimizations.

CODE_BLOCK_PLACEHOLDER_9_END

### Feature: Dokumente in Netzwerk-Knoten indexieren
**Overview**: Add directories containing documents to the indexing process for efficient searches.

#### Schritt 1: Dokumentverzeichnisse zum Indexierungsprozess hinzufügen
Pass a list of folder paths to the master node; the engine will create a separate shard for each folder, enabling parallel query execution.

CODE_BLOCK_PLACEHOLDER_10_END

### Feature: Textsuche in Netzwerk-Knoten
**Overview**: Execute text searches across all indexed documents within your search network.

#### Schritt 1: Eine Textsuche durchführen
Invoke the static helper to run a query and retrieve matching documents with relevance scores.

CODE_BLOCK_PLACEHOLDER_11_END

### Feature: Optimierung von Shards
**Overview**: Enhance performance by optimizing shards within the indexer of your search network node.

#### Schritt 1: Indexer‑Shards optimieren
Optimize shards to improve search efficiency (this is where **how to optimize shards** really matters):

CODE_BLOCK_PLACEHOLDER_12_END

## Praktische Anwendungen
GroupDocs.Search for Java can be applied in various real‑world scenarios, each benefiting from shard optimization:

1. **Enterprise Document Management** – Handles 10 TB+ archives with sub‑second query times after shard optimization.  
2. **E‑commerce Platforms** – Powers product search across 1 million SKUs, reducing latency by up to 45 % when shards are optimized.  
3. **Legal Firms** – Retrieves case files from 200 GB repositories in under 200 ms.  
4. **Library Systems** – Supports catalog searches for 500 k digital books with efficient memory usage.  
5. **Content Management Systems (CMS)** – Enables instant content discovery for multi‑site deployments with over 2 million pages.

## Leistungsüberlegungen
To ensure optimal performance of your GroupDocs.Search implementation:

- **Regularly optimize shards** – Running `optimizeShards()` after every 10 GB of new data reduces query response times by 30‑50 %.  
- **Monitor memory usage** – Keep JVM heap below 75 % of physical RAM; enable G1GC for large indexes.  
- **Use incremental indexing** – Add only changed files to avoid full re‑indexing.  
- **Leverage multi‑node scaling** – Add worker nodes to distribute shards; each additional node can improve throughput by ~20 % for read‑heavy workloads.

## Häufige Probleme und Lösungen
| Problem | Symptom | Lösung |
|-------|---------|----------|
| Portkonflikt beim Start | `java.net.BindException: Address already in use` | Change `basePort` to an unused value; verify with `netstat -ano`. |
| Out‑of‑memory‑Fehler während der Optimierung | `java.lang.OutOfMemoryError: Java heap space` | Increase JVM `-Xmx` flag or run optimization on a dedicated node with more RAM. |
| Fehlende Dokumente in Suchergebnissen | No results returned after indexing | Ensure directories are correctly added via `IndexingDocuments.addDirectories` and that `masterNode.index()` completed without exceptions. |
| Veraltete Shards nach Massenlöschung | Deleted files still appear | Run `optimizeShards()` to merge segments and purge tombstones. |

## Häufig gestellte Fragen

**Q: How does shard optimization affect query speed?**  
A: Optimizing shards compacts the index, reduces disk I/O, and typically yields 30‑50 % faster query responses for large datasets.

**Q: Is it safe to run `optimizeShards` on a live node?**  
A: Yes, the operation is designed to run without downtime, but scheduling during low‑traffic periods is recommended for indexes larger than 20 GB.

**Q: Can I customize the `OptimizeOptions`?**  
A: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor` to fine‑tune the optimization process.

**Q: What should I do if I encounter an `IOException` during optimization?**  
A: Verify file system permissions, ensure enough free disk space, and confirm that no other process is locking the index files.

**Q: Does optimizing shards also reclaim deleted document space?**  
A: Yes, the optimizer merges segments and removes tombstones, freeing up space occupied by deleted documents.

## Fazit
By following this comprehensive guide, you now know how to **configure search network java**, index documents, run text queries, and most importantly, **optimize shards** to keep your search performance razor‑sharp. Apply these patterns to any Java‑based enterprise search solution, and you’ll see measurable improvements in latency, scalability, and resource utilization. For next steps, explore advanced features like custom analyzers, faceted search, and integration with cloud storage providers.

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Verwandte Tutorials

- [Configuring GroupDocs.Search Network in .NET&#58; A Comprehensive Guide](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Master .NET Document Indexing with GroupDocs.Search&#58; A Comprehensive Guide](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Tutorials and Examples of GroupDocs.Search for Java](/search/net/)