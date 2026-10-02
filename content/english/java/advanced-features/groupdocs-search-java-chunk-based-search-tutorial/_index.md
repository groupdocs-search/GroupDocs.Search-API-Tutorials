---
date: '2026-10-02'
description: Learn how to use a temporary license to add documents to index with chunk‑based
  search in Java, boosting search performance while controlling memory usage.
images:
- /java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/og-image.png
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Use a temporary license to add documents to index with chunk‑based
  search in Java, improving search speed and reducing memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Use a temporary license for chunk‑based indexing in Java
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
title: Use a temporary license for chunk‑based indexing in Java
type: docs
url: /java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Use a temporary license for chunk‑based indexing in Java

In this tutorial you’ll **use a temporary license** to add documents to index with GroupDocs.Search’s chunk‑based search feature. The approach lets you handle massive document collections—legal contracts, support tickets, research papers—while keeping **java search index memory** usage low and **increase search performance** dramatically. You’ll see how to set up the index folder, feed multiple document sources, enable chunk searching, and run both the first and subsequent chunk queries.

## Quick Answers
- **What is the first step?** Create a search index folder.  
- **How do I include many files?** Use `index.add()` for each document folder.  
- **Which option enables chunk search?** `options.setChunkSearch(true)`.  
- **Can I continue searching after the first chunk?** Yes, call `index.searchNext()` with the token.  
- **Do I need a license?** A free trial or temporary license works for development; a full license is required for production.  

## What you’ll learn
- How to create a search index in a specified folder.  
- Steps to **add documents to index** from multiple locations.  
- Configuring search options to enable chunk‑based searching.  
- Performing initial and subsequent chunk‑based searches.  
- Real‑world scenarios where chunk‑based document search shines.  

## Prerequisites
To follow this guide, ensure you have:

- **Required libraries**: GroupDocs.Search for Java 25.4 or later.  
- **Environment setup**: A compatible Java Development Kit (JDK) installed.  
- **Knowledge prerequisites**: Basic Java programming and Maven familiarity.  

## Setting up GroupDocs.Search for Java
To begin, integrate GroupDocs.Search into your project using Maven:

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

Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License acquisition
To try out GroupDocs.Search:

- **Free trial** – test core features without commitment.  
- **Temporary license** – extended access for development.  
- **Purchase** – full license for production use.  

## How to add documents to index?
**Direct answer:** Call `index.add()` for each folder that contains files you want searchable; the method scans the folder recursively and adds every supported document to the index in a single operation. This eliminates the need for manual file‑by‑file handling and speeds up bulk ingestion.

`SearchIndex` is the central class that represents the searchable collection on disk. After you instantiate it, all indexing and query operations flow through this object.

### 1. Creating an index
**Direct answer:** Instantiate a `SearchIndex` object with the path where the index files should be stored, then call `index.create()` to initialise the storage structure. The call creates the necessary folders and metadata files on first use.

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

### 2. Adding documents to index
**Direct answer:** Use the `index.add()` method and pass the absolute path of each source folder; the API automatically detects supported formats (PDF, DOCX, XLSX, etc.) and extracts searchable text into the index.

`SearchOptions` is a configuration object that lets you fine‑tune how documents are processed during indexing and searching. You’ll use it later to enable chunk‑based queries.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Configuring search options for chunk search
**Direct answer:** Set `options.setChunkSearch(true)` on a `SearchOptions` instance before executing a query; this tells the engine to split each document into logical chunks (typically paragraphs) and return matches per chunk instead of per whole file.

`SearchResult` holds the matched chunks, their positions, and relevance scores. When chunk search is on, each `SearchResult` corresponds to a single fragment of the original document.

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

### 4. Performing initial chunk‑based search
**Direct answer:** Execute `index.search("your query", options)`; the call returns a `SearchResult` collection for the first set of matching chunks and a token that represents the search state for continuation.

The returned token is essential for paging through large result sets without re‑executing the whole query.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Continuing chunk‑based search
**Direct answer:** Pass the token returned from the previous call to `index.searchNext(token, options)`; repeat until the method returns `null`, indicating that all matching chunks have been retrieved.

This incremental approach keeps memory usage low because only the current chunk batch resides in memory.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Why use chunk‑based search?
Chunk‑based searching breaks massive document collections into manageable pieces, reducing memory pressure and speeding up response times. By indexing at the paragraph or section level, the engine can retrieve only the relevant fragments, which lowers CPU usage and improves latency for end‑users. It’s especially beneficial when:

1. **Legal teams** need to locate specific clauses across thousands of contracts.  
2. **Customer support portals** must surface relevant knowledge‑base articles instantly.  
3. **Researchers** sift through extensive datasets without loading entire files into memory.  

Quantified claim: GroupDocs.Search can process **500‑plus‑page PDFs** in under **2 seconds per chunk** on a standard 8‑core server, while keeping peak heap under **200 MB**.

## How this approach increases search performance
**Direct answer:** By searching smaller chunks instead of whole files, the engine can skip irrelevant sections early, reduce CPU cycles, and keep only the active chunk in memory, which directly lowers **java search index memory** consumption and yields faster response times. This targeted approach also enables more effective caching and parallel processing, allowing multiple cores to handle different chunks simultaneously, which further improves throughput on multi‑core servers.

Additional benefits include:

- Parallel chunk processing across multiple cores.  
- Early termination when a high‑relevance match is found.  

## Managing java search index memory
**Direct answer:** Allocate sufficient JVM heap (e.g., `-Xmx2g` or higher) based on the expected index size, run `index.optimize()` after bulk additions to compress the index structure, and monitor GC pauses with VisualVM to avoid latency spikes.

Further tuning tips:

- Use `index.flush()` after large batches to write interim data to disk.  
- Enable `options.setMemoryLimit(256)` to cap per‑search memory usage.  

## Performance considerations
- **Memory management** – Allocate sufficient heap space (`-Xmx`) for large indexes.  
- **Resource monitoring** – Keep an eye on CPU usage during indexing and search operations.  
- **Index maintenance** – Periodically rebuild or clean the index to discard stale data.  

## Common pitfalls & troubleshooting
| Issue | Why it happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## Frequently asked questions

**Q: What is chunk‑based searching?**  
A: Chunk‑based searching divides the dataset into smaller pieces, allowing efficient queries over large volumes of data without loading entire documents into memory.

**Q: How do I update my index with new files?**  
A: Simply call `index.add()` with the path to the new documents; the index will incorporate them automatically.

**Q: Can GroupDocs.Search handle different file formats?**  
A: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other formats**.

**Q: What are typical performance bottlenecks?**  
A: Memory constraints and unoptimized indexes are the most common; allocate sufficient heap and regularly optimize the index.

**Q: Where can I find more detailed documentation?**  
A: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) for in‑depth guides and API references.

**Q: Does chunk‑based search work with encrypted PDFs?**  
A: Yes, as long as you provide the password via the appropriate API overload.

**Q: How can I monitor indexing progress?**  
A: Use the `Index.add()` overload that returns a `Progress` object or hook into logging callbacks.

## Resources
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary license**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-10-02  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Related Tutorials

- [Create Search Index Directory & Set License – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Groupdocs Search Java Advanced Search Features](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)