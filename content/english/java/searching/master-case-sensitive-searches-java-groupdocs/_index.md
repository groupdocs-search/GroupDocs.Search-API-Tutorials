---
title: "Add documents to index: case‑sensitive Java search with GroupDocs"
description: "Learn how to add documents to index and enable case sensitive search in Java with GroupDocs.Search, boosting accuracy of your application."
date: "2026-02-06"
weight: 1
url: "/java/searching/master-case-sensitive-searches-java-groupdocs/"
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
type: docs
---

# Add documents to index: Mastering Case‑Sensitive Searches in Java with GroupDocs

Retrieving the right piece of information from a massive collection of documents is a core requirement for modern applications. In this guide, you’ll learn **how to add documents to index** and perform **case‑sensitive searches** using GroupDocs.Search for Java. Whether you’re building a legal‑document repository, an e‑commerce catalog, or a content‑management system, precise search results keep users happy and your data trustworthy.

## Quick Answers
- **What is the primary step to start searching?** Add documents to an index with `index.add(...)`.
- **How to enable case sensitive search?** Set `options.setUseCaseSensitiveSearch(true)`.
- **Can I search across multiple directories?** Yes – call `index.add()` for each folder you want to include.
- **Which method lets me search with objects?** Use `SearchQuery.createWordQuery(...)`.
- **Do I need a license for testing?** A temporary license is available for trial purposes.

## What does “add documents to index” mean?
Adding documents to an index means feeding your source files (PDFs, Word docs, plain text, etc.) into GroupDocs.Search so it can build a searchable data structure. Once indexed, the engine can execute fast queries, including case‑sensitive ones.

## Why enable case‑sensitive search in Java?
- **Exact term matching** – differentiate “Apple” (the company) from “apple” (the fruit).  
- **Regulatory compliance** – some industries require exact phrase matching.  
- **Improved relevance** – users often expect case‑specific results in technical or legal contexts.

## Prerequisites
- JDK (Java 17 or later recommended)  
- Maven for dependency management  
- An IDE such as IntelliJ IDEA or Eclipse  
- Basic familiarity with Java programming  

## Setting Up GroupDocs.Search for Java
First, add the GroupDocs repository and dependency to your `pom.xml`:

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

Alternatively, you can download the latest version directly from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensing
To get started with a trial, visit GroupDocs to acquire a temporary license. This will allow you to test all features without any limitations.

## How to add documents to index – Text Query Search

### Step 1: Create an Index and add your documents
Create a folder where the index files will be stored, then add the source directory that contains the documents you want to search.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Pro tip:** You can call `index.add()` multiple times to **search across multiple directories** in a single index.

### Step 2: Enable case‑sensitive search
Configure the search options to respect letter casing.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Step 3: Execute a case‑sensitive text query
Run a query that differentiates “Advantages” from “advantages”.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

The loop prints the full path of each document that contains the exact case‑matched term.

## How to add documents to index – Object Query Search

Object queries give you more flexibility, especially when you need to combine multiple criteria.

### Step 1: Initialize a second index (optional)
If you prefer to keep object‑based searches separate, create another index folder.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Step 2: Re‑use the case‑sensitive option
The same `SearchOptions` instance works for object queries.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Step 3: Build and run an object query
Create a word query object and pass it to the search engine.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Using `createWordQuery` lets you later combine it with phrase, wildcard, or Boolean queries for more complex scenarios.

## Practical Applications
- **Legal Document Management:** Retrieve case‑specific statutes where capitalization matters.  
- **E‑commerce Platforms:** Distinguish product SKUs like “PRO‑X” vs. “pro‑x”.  
- **Content Management Systems (CMS):** Ensure authors find exact headings or tags.

## Performance Considerations
- **Keep the index up‑to‑date** – re‑index when new files are added or existing ones change.  
- **Monitor memory usage** – large corpora benefit from incremental indexing and proper JVM heap sizing.  
- **Leverage Java’s garbage collector** – release `Index` objects when they’re no longer needed.

## Common Issues and Solutions
| Issue | Solution |
|-------|----------|
| `useCaseSensitiveSearch` appears ignored | Verify you are using the latest GroupDocs.Search version and that the index was rebuilt after changing the option. |
| No results returned for a known term | Ensure the term’s case matches exactly and that the document was successfully added to the index. |
| Searching many folders slows down | Add each folder individually with `index.add()` and consider splitting the index into shards for very large datasets. |

## Frequently Asked Questions

**Q:** How do I handle large datasets with GroupDocs.Search?  
**A:** Utilize index partitioning, tune JVM memory settings, and periodically compact the index to keep performance optimal.

**Q:** Can I search across multiple directories simultaneously?  
**A:** Yes – call `index.add()` for each directory you want to include, then run a single query against the combined index.

**Q:** What are common pitfalls when setting up case‑sensitive searches?  
**A:** Forgetting to rebuild the index after enabling `useCaseSensitiveSearch`, or using the wrong case in the query string.

**Q:** How can I troubleshoot search errors?  
**A:** Check the log files generated by GroupDocs.Search for stack traces, and confirm that all Maven dependencies are correctly resolved.

**Q:** Is GroupDocs.Search suitable for real‑time applications?  
**A:** With proper indexing strategies (incremental updates and in‑memory caching), it can deliver near‑real‑time search results.

## Resources
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API Reference:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub Repository:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Support Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Temporary License:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-02-06  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs  

---