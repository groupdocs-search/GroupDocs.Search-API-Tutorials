---
date: '2026-07-07'
description: Learn how to disable stop words java and add documents to index using
  GroupDocs.Search for Java, boosting search accuracy and performance.
images:
- /java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/og-image.png
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: Disable stop words java and add documents to index with GroupDocs.Search
  for Java. Follow this step‑by‑step guide to improve query accuracy and performance.
og_title: Disable Stop Words Java – Add Docs to Index with GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: Disable Stop Words Java – Add Docs to Index with GroupDocs
type: docs
url: /java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Disable Stop Words Java – Add Docs to Index with GroupDocs

In this tutorial you’ll discover how to **disable stop words java** while adding your files to a searchable index with GroupDocs.Search for Java. By turning off the built‑in stop‑word filter, every token—including common words like “on”, “by”, or “the”—becomes searchable, which dramatically improves result relevance for specialized domains such as legal contracts, e‑commerce catalogs, or technical manuals.

## Quick Answers
- **What does “add documents to index” mean?** It means loading your source files into a searchable index so they can be queried efficiently.  
- **Why would I disable stop words?** To include common words (e.g., “on”, “the”) in searches when those terms are meaningful for your domain.  
- **Which library version is required?** GroupDocs.Search for Java 25.4 or later.  
- **Do I need a license?** A free trial works for evaluation; a permanent license is required for production.  
- **Can I use this in a Maven project?** Yes – just add the repository and dependency shown below.

## What are stop words in search and why might you want to disable them?

Stop words are high‑frequency terms that many search engines automatically filter out to speed up query processing. Disabling them ensures that **every word**—including those traditionally ignored—contributes to the search index, which is essential when those words carry domain‑specific meaning. For example, in a legal contract the word “by” can distinguish parties, and in a product catalog “on” may be part of a model name.

## How does adding documents to index work in GroupDocs.Search?

When you add documents, GroupDocs.Search reads each file, tokenizes the content, and stores the tokens in an optimized inverted index. This structure enables sub‑second retrieval even for collections containing **hundreds of thousands of files**. The library also supports incremental updates, so you can keep the index fresh without rebuilding from scratch.

## Prerequisites

- **Required Libraries**: GroupDocs.Search for Java 25.4 (or newer).  
- **Development Environment**: IntelliJ IDEA, Eclipse, or any Java IDE you prefer.  
- **Basic Knowledge**: Familiarity with Java syntax and the concept of indexing.

## Setting Up GroupDocs.Search for Java

### Maven Installation

If you're using Maven, include the following in your `pom.xml`:

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

### Direct Download

Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### License Acquisition Steps
- **Free Trial** – start testing right away.  
- **Temporary License** – obtain a time‑limited key for full functionality.  
- **Purchase** – secure a permanent license for production use.

## Basic Initialization and Setup

IndexSettings is a configuration class that defines how the index is built, searched, and which features are enabled.

Create an instance of `IndexSettings` to control how the index behaves:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## How to disable stop words in search (Java)?

IndexSettings is the configuration object that controls the behavior of the search index. By default it enables a built‑in stop‑word filter. To turn this filter off, call the method `setUseStopWords(false)` on the `IndexSettings` instance. This single call disables stop‑word removal, ensuring that every token—including common words such as “on” or “the”—is indexed and can be queried.

## How to add documents to index

Adding documents to the index is performed by creating an `Index` object with the desired `IndexSettings` and then invoking its `add` method for each file or folder. The library reads each document, tokenizes its content, and stores the resulting terms in the inverted index, making them searchable instantly. You can point the index to a specific output directory and specify the source folder containing the files to be indexed.

### Defining the Output Directory

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### Specifying the Document Directory

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## Performing a Search Query

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Because `disable stop words java` is active, a query containing the term `"on"` will be evaluated, returning matches that would otherwise be ignored by the default filter.

## Practical Applications

1. **Enterprise Document Search** – Preserve critical terminology that would be stripped by default stop‑word lists.  
2. **E‑commerce Platforms** – Boost product discoverability by indexing every word in descriptions, model numbers, and specifications.  
3. **Legal Research Tools** – Capture every legal term, even those commonly treated as stop words, to avoid missing crucial clauses.

## Performance Considerations

- **Optimization Tips**: Regularly update and prune your index to keep search speed high. GroupDocs.Search can handle **up to 1 million documents** while maintaining sub‑second query times.  
- **Resource Usage**: Monitor JVM heap size; large indexes may require a maximum heap (`-Xmx`) of 4 GB or more.  
- **Java Memory Management**: Use off‑heap storage options for very large corpora to keep the on‑heap footprint under 2 GB.

## Common Issues and Solutions

| Symptom | Likely Cause | Fix |
|---|---|---|
| No results for common words | `setUseStopWords(true)` (default) | Call `setUseStopWords(false)` as shown above. |
| Out‑of‑memory errors during indexing | Indexing too many large files at once | Index files in batches; increase `-Xmx` JVM option. |
| Search returns stale data | Index not refreshed after adding new files | Call `index.update()` or re‑add the changed documents. |

## Frequently Asked Questions

**Q: What are stop words?**  
A: Stop words are common terms (e.g., “the”, “is”, “on”) that many search engines ignore to speed up queries. Disabling them lets you treat every token as searchable.

**Q: Why disable stop words in search indexes?**  
A: When exact phrase matching is required—such as in legal or technical documents—every word carries meaning, so you need to include stop words.

**Q: How does GroupDocs.Search handle large datasets?**  
A: The library uses optimized data structures and incremental indexing to keep memory usage low, even with **millions of documents**.

**Q: Can I integrate GroupDocs.Search with other Java applications?**  
A: Yes, the API is designed for easy embedding into any Java‑based system, from web services to desktop apps.

**Q: What should I do if my search results are not accurate?**  
A: Verify that the index includes all required files (`add documents to index`), ensure stop‑word filtering is disabled when needed, and consider rebuilding the index after major changes.

## Additional Resources

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

By following this guide, you now know how to **add documents to index** and **disable stop words java** to deliver more accurate search results in your Java applications.

---

**Last Updated:** 2026-07-07  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

---

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## Related Tutorials

- [Language Processing Java – Create Synonym Dictionary with GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)