---
date: '2026-01-24'
description: Lernen Sie, wie Sie die Basis‑Ports von GroupDocs für skalierbare Suchnetzwerke
  mit GroupDocs.Search Java konfigurieren, die Abrufgeschwindigkeit optimieren und
  Multi‑Node‑Systeme einrichten.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Basisport von GroupDocs im Java Search Network konfigurieren
type: docs
url: /de/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

ports für GroupDocs im Java Search Network

In modernen, daten von denNode‑Konfiguration – sodass Sie ein skalierbares Suchnetzwerk mit GroupDocs.Search für Java sicher starten können.

## Quick Answers
- **Was ist der Hauptzweck?** Einzigartige Ports und Verzeichnisse für jeden Suchknoten festzulegen, um Konflikte zu vermeiden.
- **Benötige ich eine Lizenz?** Ja, für den Produktionseinsatz ist eine Test‑ oder Voll‑Lizenz erforderlich.
- **Welche Java‑Version wird unterstützt?** Java 8 oder höher.
- **Kann ich das auf Cloud‑Servern ausführen?** Absolut – stellen Sie nur sicher, dass die Ports in Ihren Sicherheitsgruppen geöffnet sind.
- **Wie viele Knoten kann ich hinzufügen?** Es gibt keine feste Obergrenze; fügen Sie so viele hinzu, wie Ihre Hardware und Ihr Netzwerk zulassen.

## What‑noten verwendet (und für nachfolgende Knoten inkrementiert). Dieser einfache Schritt eliminiert die gefürchteten „Port bereits in Verwendung“-Fehler und legt die Grundlage für einen sauberen, horizontal skalierbaren Such‑Cluster.

## Why use GroupDocs.Search for a scalable network?
- **Hohe Leistung** – optimierte Indexierungs‑ und Suchalgorithmen.
- **Flexible Architektur** – Sie können Indexer, Sucher, Shards und Extraktoren- **IDE** wie IntelliJ IDEA oder Eclipse.
- (‑Ports, localhost vs. Remote‑Hosts).

## Setting Up GroupDocs.Search for Java

### Installation Instructions

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

**Direct Download:**

Alternativ laden Sie die neueste Version von [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) herunter.

### License Acquisition

- **Kostenlose Testversion** – sofort mit dem Testen beginnen.
- **Temporäre Lizenz** – erhalten Sie eine erweiterte Testversion unter [Temporary License](https://purchase.groupdocs.com/temporary-license).
- **Vollkauf** – erforderlich für Produktionseinsätze.

### Basic Initialization and Setup

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Implementation Guide

### How to configure base port groupdocs

#### Setting Up Base Paths

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Warum**: Eine konsistente Verzeichnisstruktur ermöglicht es jedem Knoten, seine Index‑, Shard‑ oder Extraktor‑Dateien eindeutig zu finden.

#### Configuring Base Port

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Warum**: Der Start mit einer hohen Portnummer (z. B. 49100) verringert die Wahrscheinlichkeit von Kollisionen mit gängigen Diensten. Erhöhen Sie den Port für jeden zusätzlichen Knoten.

#### Define Host Address

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Warum**: Die Verwendung von `localhost` ist ideal für die Entwicklung; ersetzen Sie sie für die Produktion durch die IP‑Adresse oder den DNS‑Namen Ihres Servers.

#### Create Network Configuration

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Warum**: Diese Optionen balancieren Geschwindigkeit und Speichereffizienz und bieten Ihnen einen schlanken, aber leistungsstarken Suchindex.

#### Add Nodes

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Warum**: Das Aufteilen von Aufgaben auf Knoten (Indexierung vs. Suche, Sharding vs. Extraktion) verbessert Parallelität und Fehlertoleranz.

#### Finalize Configuration

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Common Issues & Solutions

- **Portkonflikte** – Erhöhen Sie stets `basePort` für jeden neuen Knoten. Überprüfen Sie dies mit `netstat` oder dem Port‑Monitor Ihres Betriebssystems.
- **Fehlende Verzeichnisse** – Stellen Sie sicher, dass jeder referenzierte Ordner (`Indexer0`, `Searcher0` usw.) existiert und der Java‑Prozess Lese‑/Schreibrechte hat.
- **Netzwerkerreichbarkeit** – Beim Wechsel zu einer Multi‑Machine‑Umgebung ersetzen Sie `127.0.0.1` durch die tatsächliche Host‑IP und öffnen Sie die gewählten Ports in den Firewalls.

## Practical Applications

| Szenario                     | Nutzen der Konfiguration des Basisports für GroupDocs |
|------------------------------|------------------------------------------------------|
| Enterprise Document Management | Nahtloses Skalieren über Abteilungen hinweg ohne Ausfallzeiten |
| Large CMS Platforms          | Schnellere Inhaltsabfrage, da der Index verteilt ist |
| Legal Case Management        | Parallele Extraktion von PDFs reduziert die Suchlatenz |

## Performance Considerations

- **CPU/Memory überwachen** – Verwenden Sie Javas JMX oder ein Profiling‑Tool, um die Thread‑Auslastung zu beobachten.
- **Kompression anpassen** – `Compression.High` spart Festplattenspeicher, kann jedoch CPU‑Overhead erzeugen; testen Sie sowohl `High` als auch `Normal`.
- **Regelmäßig aktualisieren** – Neue GroupDocs.Search‑Versionen enthalten häufig Performance‑Patches.

## Conclusion

Sie haben nun gelernt, wie Sie **den Basisport für GroupDocs konfigurieren** und ein Multi‑Node‑Suchnetzwerk mit GroupDocs.Search für Java einrichten. Experimentieren Sie mit zusätzlichen Knoten, passen Sie Index‑Einstellungen an und integrieren Sie das Netzwerk in Ihre bestehenden Anwendungen für eine wirklich skalierbare Suchlösung.

## Frequently Asked Questions

**F: Was ist der Zweck der Deaktivierung von Stoppwörtern beim Indexieren?**  
A: Die Deaktivierung von Stoppwörtern kann die Suchgenauigkeit verbessern, indem häufige Begriffe erhalten bleiben, die in spezialisierten Bereichen entscheidend sein können.

**F: Wie gehe ich mit Portkonflikten um, wenn ich mehrere Knoten hinzufüge?**  
A: Beginnen Sie mit einem hohen `basePort` (z. B. 49100) und erhöhen Sie ihn sodass jeder Knoten einen eindeutigen TCP‑Endpunkt hat.

**F: Kann ich dieses Setup für cloud‑basierte Anwendungen verwenden?**  
A` bietet `Fast‑Szenarien abzielen.

**F: Gibt es eine Begrenzung für die Anzahl der Knoten, die ich hinzufügen kann?**  
A: Technisch gibt es keine; die Grenze wird durch Ihre Hardware‑Ressourcen und die Netzwerkbandbreite bestimmt.

---

**Last Updated:** 2026-01-24  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs