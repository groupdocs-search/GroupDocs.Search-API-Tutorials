---
date: '2026-11-02'
description: Learn how to add folder to index with GroupDocs.Search in Java, configure
  high compression, and run fast full‑text queries.
images:
- /java/indexing/master-text-indexing-java-groupdocs-search-guide/og-image.png
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Learn how to add folder to index with GroupDocs.Search in Java, configure
  compression, and execute fast full‑text searches. Ideal for large document sets.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: How to add folder to index with GroupDocs.Search in Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: How to add folder to index with GroupDocs.Search in Java
type: docs
url: /java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# How to add folder to index with GroupDocs.Search in Java

If you need **java full text search** that can scale to millions of documents, you’re in the right place. In this tutorial you’ll learn how to **add folder to index** using GroupDocs.Search, configure high‑compression storage, and run lightning‑fast queries. By the end you’ll have a production‑ready solution you can drop into any Java project.

## Quick answers
- **What is the primary library?** GroupDocs.Search for Java  
- **How to add a folder to index?** Use `index.add(folderPath)`  
- **Can I configure text compression?** Yes, via `TextStorageSettings(Compression.High)`  
- **Which Java version is required?** JDK 8 or higher  
- **Where to get a trial license?** From the GroupDocs website or the repository page  

## What is java full text search and why it matters?

Java full text search converts raw documents into an inverted index, enabling sub‑second retrieval of any term across thousands of files. This capability is essential for legal repositories, research libraries, and enterprise knowledge bases where users expect instant results. It also improves productivity in modern applications.

## Why use groupdocs.search for java full text search?

GroupDocs.Search delivers high‑throughput indexing and query execution while offering built‑in high compression. It supports **50+ input and output formats**—including PDF, DOCX, EML, and HTML—and can process multi‑hundred‑page documents without loading the entire file into memory, keeping the memory footprint under 200 MB for typical workloads.

## Prerequisites

- **GroupDocs.Search for Java** (version 25.4 or later) – the core library that powers indexing and searching.  
- **JDK 8+** installed and configured – the minimum runtime required for the SDK.  
- **Maven** for dependency management – simplifies adding the library to your project.  
- An IDE such as **IntelliJ IDEA** or **Eclipse** – for writing and debugging Java code.

## Setting up GroupDocs.Search for java

### Maven setup
Add the repository and dependency to your `pom.xml` file:

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

### Direct download
Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### License acquisition
- **Free trial** – explore all features without commitment.  
- **Temporary license** – extended testing period.  
- **Purchase** – unlock full production capabilities.

### Basic initialization and setup
`Index` is the core class used to create, open, and manage a search index.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Index text with custom compression

### Step 1: define the index folder
Choose a directory where the index files will reside:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Step 2: configure index settings
`TextStorageSettings` configures how text is stored in the index, including compression level. `Compression` is an enum that specifies the desired compression algorithm.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Step 3: create the index with custom settings
Instantiate the index using the configuration defined above:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## How to add a folder to index

`Index` is the main class representing the searchable index.

Load the existing index (or create a new one) and then call the `add` method on the `Index` object. The `add` operation scans the supplied directory, extracts text from each supported file, and stores it in the compressed index, ready for instant search.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## How to search indexed documents

`SearchResult` represents a single match with document path and relevance.

Define a search query string that represents the term or phrase you want to locate, then invoke the `search` method on the `Index` instance. The method returns a collection of `SearchResult` objects, each containing the document path, relevance score, and snippet highlighting the match.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Practical applications

Real‑world scenarios where **java full text search** shines:

1. **Legal document management** – instant retrieval of case files.  
2. **Academic research libraries** – fast lookup of papers and theses.  
3. **Enterprise knowledge bases** – quick access to manuals and FAQs.  
4. **Content management systems** – efficient content discovery for large sites.  
5. **Customer service archives** – rapid search of past tickets and chats.  

## Performance considerations

- **Compression vs. speed**: High compression saves up to 70 % disk space but adds a modest indexing overhead; run benchmark tests for your data volume.  
- **Memory management**: Allocate at least 2 GB of heap for indexes larger than 10 GB to avoid `OutOfMemoryError`.  
- **Index updates**: Incrementally add new documents with `index.add()` and periodically call `index.optimize()` to keep the index compact.  
- **Query optimization**: Use the advanced query syntax (wildcards, proximity, fuzzy search) to narrow results and reduce response time.

## Common pitfalls & pro tips

- **Pitfall:** Forgetting to call `index.optimize()` after bulk additions.  
  **Pro tip:** Run `index.optimize()` nightly to keep the index compact.  

- **Pitfall:** Using the default (low) compression on massive datasets.  
  **Pro tip:** Switch to `Compression.High` for production environments to cut storage costs.  

- **Pitfall:** Not handling `IOException` when adding files from a network share.  
  **Pro tip:** Wrap `index.add()` in a try‑catch block and log any failures for later review.  

## Frequently asked questions

**Q: What is GroupDocs.Search?**  
A: It is a robust Java library that provides advanced full‑text search capabilities, including indexing, compression, and complex query support.

**Q: How do I handle large datasets with GroupDocs.Search?**  
A: Enable high compression (`Compression.High`) and periodically commit changes to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for indexes over 20 GB).

**Q: Can I integrate GroupDocs.Search with existing enterprise systems?**  
A: Yes, the library can be embedded in any Java‑based backend, REST services, or micro‑services architecture.

**Q: What if my index becomes outdated?**  
A: Use the `index.add()` method to append new files and `index.delete()` to remove obsolete ones, then re‑run `index.optimize()` if needed.

**Q: Where can I get help or support?**  
A: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10) for troubleshooting and best‑practice tips.

## Additional resources

- Detailed usage guide: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Full API reference: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Stay up‑to‑date with new features: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Last Updated:** 2026-11-02  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs  

---

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Related Tutorials

- [Groupdocs Search Java Create Index Guide](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Mastering Groupdocs Search Java Index Management Guide](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java Full Text Search Library – Optimize Index with GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)