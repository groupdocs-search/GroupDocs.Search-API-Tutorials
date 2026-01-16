---
date: '2026-01-16'
description: เรียนรู้วิธีกำหนดค่าเครือข่ายการค้นหา GroupDocs ใน Java และเพิ่มคำพ้องความหมายลงในดัชนีเพื่อเพิ่มประสิทธิภาพการค้นหา.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: กำหนดค่า GroupDocs.Search Network ใน Java – เพิ่มประสิทธิภาพการค้นหา
type: docs
url: /th/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Configure GroupDocs.Search Network in Java – Boost Search

ในแอปพลิเคชันที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน **configure groupdocs search network** เป็นขั้นตอนสำคัญในการให้ผลลัพธ์ที่เร็วและแม่นยำในคอลเลกชันเอกสารขนาดใหญ่ ไม่ว่าคุณจะสร้างพอร์ทัลการค้นหาแบบองค์กรทั้งหมดหรือขยายโซลูชันที่มีอยู่แล้ว การตั้งค่า GroupDocs.Search network อย่างเหมาะสมจะช่วยให้คุณสเกลแนวนอน เพิ่มการสนับสนุนคำพ้องความหมาย และรักษาความหน่วงเวลาให้ต่ำ ในบทเรียนนี้คุณจะได้เรียนรู้วิธีตั้งค่า ปรับใช้ และปรับจูน GroupDocs.Search network ด้วย Java พร้อมเคล็ดลับการเพิ่มคำพ้องความหมายลงในดัชนีและการจัดการวงจรชีวิตของโหนด

## Quick Answers
- **What is the primary benefit of configuring a GroupDocs.Search network?** It enables distributed indexing and querying, improving performance and scalability.  
- **Do I need a license to run the examples?** A free trial works for development; a commercial license is required for production.  
- **Can synonyms be added without rebuilding the index?** Yes—use the synonym dictionary at runtime to **add synonyms to index**.  
- **How many nodes can I deploy?** You can deploy as many nodes as your infrastructure allows; each node runs on its own port.  

## What is configuring a GroupDocs.Search network?
Configuring a GroupDocs.Search network means defining the folder structure, ports, and node settings that let multiple JVM instances collaborate on indexing and searching. This setup creates a master‑node that coordinates workers (shards) and ensures queries are executed across the entire dataset.

## Why configure a GroupDocs.Search network?
- **Scalability** – Distribute indexing load across several machines.  
- **Reliability** – Nodes can be added or removed without downtime.  
- **Search relevance** – Add synonyms to index for richer results.  
- **Performance** – Parallel query execution reduces response time.

## Prerequisites
- Java Development Kit (JDK) 8 or newer  
- Maven for building the project  
- Basic familiarity with Java syntax  
- Access to the GroupDocs.Search for Java library (downloaded via Maven or the official release page)

## Setting Up GroupDocs.Search for Java

Add the repository and dependency to your Maven **pom.xml**:

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

Alternatively, download the latest version directly from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Free Trial** – Explore core features without cost.  
- **Temporary License** – Unlock full capabilities for short‑term testing.  
- **Commercial License** – Required for production deployments.

### Basic Initialization and Setup
Create a simple Java class to verify the library loads correctly:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Step‑by‑Step Guide to Configure GroupDocs.Search Network

### 1. Configuring the Search Network
Define the base document folder and the starting port for node communication.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Where dictionaries (e.g., synonym files) reside.  
- **basePort** – The first port; subsequent nodes increment from this value.

### 2. Deploying Search Network Nodes
Spin up multiple worker nodes that share the same configuration.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Each node runs on its own port (basePort + index) and holds a shard of the overall index.

### 3. Subscribing to Node Events
Monitor health, indexing progress, and error conditions by attaching an event listener to the master node.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Event callbacks let you react to node start/stop, indexing completion, and unexpected failures.

### 4. Adding Synonyms to a Node’s Indexer  
Enhance relevance by **add synonyms to index** at runtime.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Array of terms that should be treated as equivalents.  
- **clearBeforeAdding** – Set to `true` if you want to replace existing entries.

### 5. Adding Directories for Indexing
Tell the master node which folders contain the documents you want searchable.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

The method scans the directory recursively and distributes files across shards.

### 6. Performing Text Search in the Network
Execute a query across all nodes, optionally forcing exact‑match behavior.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Switch `exactMatchOnly` to `true` when you need strict term matching without stemming.

### 7. Closing Network Nodes
Release resources gracefully once processing is complete.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Proper shutdown prevents memory leaks and keeps the JVM healthy.

## Practical Applications
| Scenario | How the network helps |
|----------|-----------------------|
| **Enterprise Search** | Distribute indexing across data‑center servers for petabyte‑scale corpora. |
| **Document Management** | Add synonyms to index so users find documents even with varied terminology. |
| **E‑commerce Catalog** | Deploy region‑specific nodes to serve localized product searches quickly. |
| **Content Management** | Keep content searchable while editors add new files to specific directories. |

## Common Issues & Solutions
- **Port Conflicts** – Ensure each node’s port (basePort + index) is free; adjust `basePort` if needed.  
- **Synonym Not Applied** – Verify you called `indexer.setDictionary(dictionary)` after adding terms.  
- **Node Not Responding** – Subscribe to events; look for `NodeFailed` callbacks to diagnose network problems.  
- **Memory Leak on Close** – Always invoke `node.close()` for every deployed node.

## Frequently Asked Questions

**Q: How does deploying multiple nodes improve search performance?**  
A: Each node indexes a shard of the data, allowing parallel processing and reducing query latency as the workload is shared.

**Q: Can I add synonyms without re‑indexing existing documents?**  
A: Yes, you can **add synonyms to index** at runtime via the synonym dictionary; the changes take effect immediately for new queries.

**Q: Is subscribing to node events mandatory?**  
A: While not required for basic operation, event subscription gives you visibility into node health and helps you react to failures promptly.

**Q: What are best practices for managing node resources?**  
A: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes during off‑peak hours to keep resource consumption optimal.

**Q: Does GroupDocs.Search support non‑text formats like PDFs or images?**  
A: Absolutely. The library extracts text from PDFs, Office files, and even performs OCR on images, making them searchable out‑of‑the‑box.

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs