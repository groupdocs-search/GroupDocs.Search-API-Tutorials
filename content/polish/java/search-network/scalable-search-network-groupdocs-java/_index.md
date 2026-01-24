---
date: '2026-01-24'
description: Dowiedz się, jak skonfigurować bazowy port GroupDocs dla skalowalnych
  sieci wyszukiwania przy użyciu GroupDocs.Search Java, zoptymalizować prędkość wyszukiwania
  i skonfigurować systemy wielowęzłowe.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Skonfiguruj podstawowy port groupdocs w sieci Java Search
type: docs
url: /pl/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Configure base port groupdocs in Java Search Network

W nowoczesnych, intensywnie wykorzystujących dane aplikacjach, **konfigurowanie podstawowego portu groupdocs** jest podstawowym krokiem do budowania szybkiej, niezawodnej infrastruktury wyszukiwania. Niezależnie od tego, czy obsługujesz tysiące plików PDF, czy skalujesz się portów i ścieżek zapewnia Cię przez każdy szczegół — od wymagań wDo I need a license?** Yes, a trial or full license is Java version is supported?** Java 8 or higher.
- **Can I run this on cloud servers?** Absolutely—just ensure the ports are open in your security groups.
- **How many nodes can I add?** There’s no hard limit; add as many as your hardware and network allow.

## What is “configure base port groupdocs”?
When you **configure base port groupdocs**, you assign a starting TCP port that each node will use (and increment for subsequent nodes). This simple step eliminates the dreaded “port already in use” errors and lays the groundwork for a clean, horizontally‑scalable search cluster **Flexible architecture** – you can mix indexers, searchers, shards, and extractors across nodes.
- **Easy integration** – works with any Java application, on‑premise or cloud.
- **Robust licensing** – trial options let you test before committing.

## Prerequisites
- **Java Development Kit (JDK)** 8 or newer.
- **IDE** such as IntelliJ IDEA or Eclipse.
- **GroupDocs.Search for Java** library (version 25.4 or later) installed via Maven or manual download.
- Basic networking knowledge (TCP ports, localhost vs. remote hosts).

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

Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition

- **Free Trial** – start testing immediately.
- **Temporary License** – get an extended trial at [Temporary License](https://purchase.groupdocs.com/temporary-license).
- **Full Purchase** – required for production deployments.

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

- **Why**: A consistent directory structure lets every node locate its index, shard, or extractor files without ambiguity.

#### Configuring Base Port

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: Starting at a high port number (e.g., 49100) reduces the chance of colliding with common services. Increment the port for each additional node.

#### Define Host Address

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: Using `localhost` is ideal for development; replace with your server’s IP or DNS name for production.

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

- **Why**: These options balance speed and storage efficiency, giving you a lean yet powerful search index.

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

- **Why**: Splitting responsibilities across nodes (indexing vs. searching, sharding vs. extracting) improves parallelism and fault tolerance.

#### Finalize Configuration

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Common Issues & Solutions

- **Port Conflicts** – Always increment `basePort` for each new node. Verify with `netstat` or your OS’s port monitor.
- **Missing Directories** – Ensure every folder referenced (`Indexer0`, `Searcher0`, etc.) exists and the Java process has read/write permissions.
- **Network Reachability** – When moving to a multi‑machine setup, replace `127.0.0.1` with the actual host IP and open the chosen ports in firewalls.

## Practical Applications

| Scenario | Benefit of Configuring Base Port GroupDocs |
|----------|--------------------------------------------|
| Enterprise Document Management | Seamless scaling across departments without downtime |
| Large CMS Platforms | Faster content retrieval as the index is distributed |
| Legal Case Management | Parallel extraction of PDFs reduces search latency |

## Performance Considerations

- **Monitor CPU/Memory** – Use Java’s JMX or a profiling tool to watch thread usage.
- **Adjust Compression** – `Compression.High` saves disk space but may add CPU overhead; test both `High` and `Normal`.
- **Update Regularly** – New GroupDocs.Search releases often include performance patches.

## Conclusion

You’ve now learned how to **configure base port groupdocs** and set up a multi‑node search network using GroupDocs.Search for Java. Experiment with additional nodes, tweak index settings, and integrate the network into your existing applications for a truly scalable search solution.

## Frequently Asked Questions

**Q: What is the purpose of disabling stop words in indexing?**  
A: Disabling stop words can improve search accuracy by retaining common terms that might be crucial in specialized domains.

**Q: How do I handle port conflicts when adding multiple nodes?**  
A: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent node, ensuring every node has a unique TCP endpoint.

**Q: Can I use**  
A: Yes—just make sure the chosen ports IP.

**Q: What is the difference between NormalIndex and other index types?**  
A: `NormalIndex` offers a balanced trade‑off between speed and memory usage, while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.

**Q: Is there a limit to the number of nodes I can add?**  
A: Technically no; the limit is dictated by your hardware resources and network bandwidth.

---

**Last Updated:** 2026-01-24  
**Tested With:** GroupDocs.Search Java 25.4  
**