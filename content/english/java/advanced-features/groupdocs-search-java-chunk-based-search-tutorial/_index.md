---
title: "Add documents to index with chunk-based search in Java"
description: "Learn how to add documents to index and enable chunk-based search in Java using GroupDocs.Search, boosting performance for large document sets."
date: "2025-12-19"
weight: 1
url: "/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/"
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
type: docs
---

# Add documents to index with chunk-based search in Java

In today's data‑driven world, being able to **add documents to index** quickly and then perform chunk‑based searches is essential for any application that handles large collections of files. Whether you're dealing with legal contracts, customer support archives, or massive research libraries, this tutorial shows you exactly how to set up GroupDocs.Search for Java so you can index documents efficiently and retrieve relevant information in bite‑sized chunks.

## What You'll Learn
- How to create a search index in a specified folder.  
- Steps to **add documents to index** from multiple locations.  
- Configuring search options to enable chunk‑based searching.  
- Performing initial and subsequent chunk‑based searches.  
- Real‑world scenarios where chunk‑based document search shines.

## Quick Answers
- **What is the first step?** Create a search index folder.  
- **How do I include many files?** Use `index.add()` for each document folder.  
- **Which option enables chunk search?** `options.setChunkSearch(true)`.  
- **Can I continue searching after the first chunk?** Yes, call `index.searchNext()` with the token.  
- **Do I need a license?** A free trial or temporary license works for development; a full license is required for production.

## Prerequisites
To follow this guide, ensure you have:

- **Required Libraries**: GroupDocs.Search for Java 25.4 or later.  
- **Environment Setup**: A compatible Java Development Kit (JDK) installed.  
- **Knowledge Prerequisites**: Basic Java programming and Maven familiarity.

## Setting Up GroupDocs.Search for Java
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

### License Acquisition
To try out GroupDocs.Search:

- **Free Trial** – test core features without commitment.  
- **Temporary License** – extended access for development.  
- **Purchase** – full license for production use.

### Basic Initialization and Setup
Create an index in the folder where you want the searchable data to live:

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

## How to add documents to index
Now that the index exists, the next logical step is to **add documents to index** from the locations where your files are stored.

### 1. Creating an Index
**Overview**: Set up a directory for the search index.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Adding Documents to Index
**Overview**: Pull in files from several source folders.

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

### 3. Configuring Search Options for Chunk Search
Enable chunk‑based searching by tweaking the options object.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Performing Initial Chunk‑Based Search
Run the first query using the chunk‑enabled options.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuing Chunk‑Based Search
Iterate through the remaining chunks until the search is complete.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Why use chunk‑based search?
Chunk‑based searching breaks massive document collections into manageable pieces, reducing memory pressure and speeding up response times. It’s especially beneficial when:

1. **Legal teams** need to locate specific clauses across thousands of contracts.  
2. **Customer support portals** must surface relevant knowledge‑base articles instantly.  
3. **Researchers** sift through extensive datasets without loading entire files into memory.

## Performance Considerations
- **Memory Management** – Allocate sufficient heap space (`-Xmx`) for large indexes.  
- **Resource Monitoring** – Keep an eye on CPU usage during indexing and search operations.  
- **Index Maintenance** – Periodically rebuild or clean the index to discard stale data.

## Common Pitfalls & Troubleshooting
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## Frequently Asked Questions

**Q: What is chunk‑based searching?**  
A: Chunk‑based searching divides the dataset into smaller pieces, allowing efficient queries over large volumes of data without loading entire documents into memory.

**Q: How do I update my index with new files?**  
A: Simply call `index.add()` with the path to the new documents; the index will incorporate them automatically.

**Q: Can GroupDocs.Search handle different file formats?**  
A: Yes, it supports PDFs, DOCX, XLSX, PPTX, and many other common formats.

**Q: What are typical performance bottlenecks?**  
A: Memory constraints and unoptimized indexes are the most common; allocate sufficient heap and regularly optimize the index.

**Q: Where can I find more detailed documentation?**  
A: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) for in‑depth guides and API references.

## Resources
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2025-12-19  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---