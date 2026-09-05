---
date: '2026-05-17'
description: Erfahren Sie, wie Sie die GroupDocs Maven-Abhängigkeit hinzufügen, ein
  Java‑Suchnetzwerk einrichten und Verzeichnisse zum Index hinzufügen, um eine schnelle,
  skalierbare Dokumentenabfrage zu ermöglichen.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: So fügen Sie die GroupDocs Maven-Abhängigkeit für das Suchnetzwerk hinzu
type: docs
url: /de/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Wie man die GroupDocs Maven-Abhängigkeit für ein Suchnetzwerk hinzufügt

In diesem umfassenden Leitfaden erfahren Sie **wie Sie die GroupDocs Maven-Abhängigkeit hinzufügen**, konfigurieren ein robustes Java-Suchnetzwerk mit GroupDocs.Search und halten Ihre Shards synchronisiert. Egal, ob Sie juristische Schriftsätze, Finanzberichte oder akademische Arbeiten indizieren, die nachstehenden Schritte helfen Ihnen, durchsuchbare Indizes zu erstellen, die Abfragebelastung über Knoten zu verteilen und die Datenkonsistenz mit minimalem Aufwand zu wahren.

## Schnelle Antworten
- **Was ist die GroupDocs Maven-Abhängigkeit?** Ein Maven-Artefakt, das die GroupDocs.Search-Bibliothek für Java-Projekte bündelt.  
- **Warum ein Suchnetzwerk verwenden?** Es verteilt Indexierungs- und Abfragebelastungen über mehrere Knoten, was Geschwindigkeit und Zuverlässigkeit verbessert.  
- **Wie füge ich Verzeichnisse zum Index hinzu?** Verwenden Sie `IndexingDocuments.addDirectories` auf dem Master-Knoten.  
- **Wie synchronisiere ich Shards?** Rufen Sie `SynchronizeOptions` auf dem `Indexer` jedes Knotens auf.  
- **Benötige ich eine Lizenz?** Ja, für die Produktion ist eine Test- oder kommerzielle Lizenz erforderlich.

## Was ist die GroupDocs Maven-Abhängigkeit?

`GroupDocs Maven dependency` ist ein Maven-Artefakt, das die GroupDocs.Search-Bibliothek für Java-Projekte bündelt.  
Es stellt alle erforderlichen Klassen bereit, um durchsuchbare Indizes zu erstellen, Netzwerk‑Knoten zu verwalten und schnelle Abfragen auszuführen, und Maven löst transitive Abhängigkeiten automatisch auf, sodass Sie mit nur wenigen Zeilen in Ihrer `pom.xml` eine einsatzbereite Suchmaschine erhalten.

## Wie man die GroupDocs Maven-Abhängigkeit hinzufügt

Fügen Sie die Repository‑ und Abhängigkeits‑Einträge zu Ihrer `pom.xml` hinzu und führen Sie anschließend `mvn clean install` aus; Maven lädt das `groupdocs-search`‑JAR und die erforderlichen Bibliotheken herunter und stellt die API in Ihrem Projekt bereit. Nachdem der Build erfolgreich war, können Sie die `com.groupdocs.search`‑Klassen sofort verwenden.

### Maven-Konfiguration

Fügen Sie das Repository und die Abhängigkeit zu Ihrer `pom.xml` hinzu:

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

> **Profi‑Tipp:** Halten Sie die Versionsnummer aktuell, indem Sie die offizielle Release‑Seite prüfen.

Sie können das JAR auch direkt von der offiziellen Seite herunterladen: [GroupDocs.Search für Java Releases](https://releases.groupdocs.com/search/java/).

## Warum ein Suchnetzwerk verwenden?

Ein Suchnetzwerk ermöglicht horizontales Skalieren, indem der Index in Shards aufgeteilt wird, die auf separaten Knoten liegen. GroupDocs.Search kann **mehr als 50 Eingabeformate** verarbeiten und **mehrseitige Dokumente** ohne Laden der gesamten Datei in den Speicher bearbeiten, wodurch subsekundäre Abfrageantworten selbst bei wachsendem Datenvolumen erzielt werden.

## Voraussetzungen

- **JDK** (11 oder neuer) installiert.  
- Eine IDE wie IntelliJ IDEA oder Eclipse.  
- Grundlegende Java‑Kenntnisse, Maven‑Vertrautheit und ein Verständnis von Netzwerk‑Knoten‑Konzepten.  
- Eine gültige GroupDocs.Search‑Lizenz (Testversion oder kommerziell).

## Grundlegende Initialisierung und Einrichtung

Beginnen Sie mit dem Erstellen eines Indexverzeichnisses:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Dieser einfache Schritt bereitet die Umgebung für die nachfolgende Netzwerkkonfiguration vor.

## Implementierungsleitfaden

### Funktion 1: Konfiguration des Suchnetzwerks

#### Übersicht

Die Konfiguration des Suchnetzwerks legt die Dateipfade und Ports fest, die die Knoten zur Kommunikation verwenden.

##### Pfad- und Portkonfiguration

Configuration ist eine Klasse, die Netzwerkpfade, Ports und weitere Einstellungen für den Such‑Cluster enthält.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
Das `configuration`‑Objekt enthält nun alle notwendigen Einstellungen für Ihr Suchnetzwerk.

### Funktion 2: Bereitstellung von Suchnetzwerk‑Knoten

#### Übersicht

Stellen Sie Knoten bereit, um die Arbeitslast über Ihr Netzwerk zu verteilen. Der Master‑Knoten verwaltet Vorgänge und Ereignisse.

##### Bereitstellungscode

`SearchNetworkNode` repräsentiert einen Knoten im Suchnetzwerk, der als Master oder Worker fungieren kann.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Funktion 3: Abonnieren von Ereignissen im Suchnetzwerk‑Knoten

#### Übersicht

Das Abhören von Ereignissen ermöglicht die dynamische Handhabung von Änderungen oder Aktualisierungen in Ihrem Netzwerk.

##### Implementierung der Abonnements

`SearchNetworkNodeEvents` bietet Ereignis‑Hooks für den Knoten‑Lebenszyklus und Indexierungs‑Aktionen.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Funktion 4: Verzeichnisse zum Index hinzufügen

#### Übersicht

Das Hinzufügen von Verzeichnissen ist der zentrale Schritt, der Ihre Dokumente durchsuchbar macht.

##### Dokumentenhinzufügung

`IndexingDocuments.addDirectories` fügt Ordnerpfade dem Index zur Verarbeitung hinzu.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Funktion 5: Synchronisierung von Shards im Suchnetzwerk‑Knoten

#### Übersicht

Die Synchronisierung gewährleistet Datenkonsistenz über alle Shards hinweg.

##### Synchronisierungscode

`SynchronizeOptions` konfiguriert, wie Shards über Knoten hinweg synchronisiert werden.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Funktion 6: Schließen von Suchnetzwerk‑Knoten

#### Übersicht

Das ordnungsgemäße Schließen von Knoten gibt Ressourcen frei und verhindert Speicherlecks.

##### Knoten schließen

`close()` gibt Ressourcen frei und fährt den Suchnetzwerk‑Knoten herunter.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Praktische Anwendungen

1. **Verwaltung juristischer Dokumente** – Schnell Fallakten und Präzedenzfälle abrufen.  
2. **Finanzbuchhaltung** – Auf Rechnungen und Prüfpfade in Sekunden zugreifen.  
3. **Akademische Forschung** – Durchsuchen Sie Tausende von Arbeiten, um relevante Zitate zu finden.

## Leistungsüberlegungen

- **Abfragen optimieren** – Schreiben Sie prägnante Abfragen, um die Antwortzeit zu verkürzen.  
- **Speicherverwaltung** – Überwachen Sie die JVM‑Heap‑Nutzung; erwägen Sie GC‑Optimierung für große Indizes.  
- **Skalierungsstrategie** – Fügen Sie Knoten proportional zum Datenvolumen und zur Abfragebelastung hinzu.

## Häufige Probleme und Lösungen

| Problem | Ursache | Lösung |
|---------|---------|--------|
| Knoten können keine Verbindung herstellen | Portkonflikt | Ändern Sie `basePort` zu einem unbenutzten Wert |
| Index wird nicht aktualisiert | Ereignis‑Abonnement fehlt | Stellen Sie sicher, dass `SearchNetworkNodeEvents.subscribe(masterNode)` aufgerufen wird |
| Hohe Latenz | Unzureichende Shards | Erhöhen Sie die Anzahl der Knoten und balancieren Sie die Dokumentenverteilung |

## Häufig gestellte Fragen

**F: Was ist der Hauptvorteil der Verwendung von GroupDocs.Search?**  
A: Es bietet schnelle, skalierbare Suchfunktionen über große Dokumentensätze hinweg mit minimaler Konfiguration.

**F: Kann ich Knoten‑Konfigurationen in einem Suchnetzwerk anpassen?**  
A: Ja, Sie können benutzerdefinierte Pfade, Ports und weitere Optionen über das `Configuration`‑Objekt festlegen.

**F: Wie füge ich Verzeichnisse zum Index hinzu, nachdem das Netzwerk läuft?**  
A: Rufen Sie `IndexingDocuments.addDirectories(masterNode, "path")` auf, wann immer Sie neue Ordner indizieren müssen.

**F: Wie synchronisiere ich Shards, wenn ein neuer Knoten dem Netzwerk beitritt?**  
A: Verwenden Sie die oben gezeigte `synchronizeShards`‑Methode auf dem neu hinzugefügten Knoten.

**F: Benötige ich eine Lizenz für die Entwicklung?**  
A: Eine kostenlose Testlizenz reicht für Tests aus; für die Produktion ist eine kommerzielle Lizenz erforderlich.

## Fazit

Durch Befolgen dieses Leitfadens wissen Sie jetzt, wie Sie **die GroupDocs Maven-Abhängigkeit hinzufügen**, ein Multi‑Node‑Suchnetzwerk konfigurieren, Verzeichnisse indizieren und Shards synchronisieren. Diese Schritte bilden die Grundlage für eine leistungsstarke Dokumentensuchlösung, die mit den Bedürfnissen Ihrer Organisation mitwachsen kann.

---

**Zuletzt aktualisiert:** 2026-05-17  
**Getestet mit:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

## Verwandte Tutorials

- [Tutorials und Beispiele von GroupDocs.Search für Java](/search/net/)
- [Konfiguration des GroupDocs.Search Netzwerks in .NET: Ein umfassender Leitfaden](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Wie man ein Suchnetzwerk mit GroupDocs.Search in .NET für Dokumenten‑Management‑Systeme implementiert](/search/net/search-network/implement-search-network-groupdocs-dotnet/)