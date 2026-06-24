---
title: "Create Search Index GroupDocs with Redaction .NET Faceted Search"
description: "Learn how to create search index groupdocs and add documents to index while implementing faceted search using GroupDocs.Search and GroupDocs.Redaction in .NET."
date: "2026-04-02"
weight: 1
url: "/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/"
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
type: docs
---
# Create Search Index GroupDocs with Redaction .NET Faceted Search

In modern applications, **creating a search index with GroupDocs** is essential for fast, accurate document retrieval. Whether you're handling legal contracts, product catalogs, or large knowledge bases, a well‑built index lets you **add documents to the index** and run powerful faceted searches in seconds. This tutorial walks you through the entire process—from setting up GroupDocs.Redaction to crafting simple and complex faceted queries—so you can deliver a responsive search experience in your .NET projects.

## Quick Answers
- **What is the primary purpose?** To create a search index with GroupDocs and enable faceted search.  
- **Which libraries are required?** GroupDocs.Redaction and GroupDocs.Search for .NET.  
- **How do I add documents to the index?** Use `index.Add(documentsFolder)` after initializing the index.  
- **Can I run complex queries?** Yes, combine object queries with logical operators for advanced filtering.  
- **Is a license needed?** A free trial works for development; a commercial license is required for production.

## What is faceted search and why use it with GroupDocs?
Faceted search lets users refine results by applying multiple filters—like category, date, or author—simultaneously. When combined with **GroupDocs.Redaction**, you gain secure, searchable content that respects redaction rules, making it ideal for compliance‑heavy environments.

## Prerequisites

### Required Libraries, Versions, and Dependencies
- **GroupDocs.Redaction .NET** – latest stable release.  
- **GroupDocs.Search .NET** – works hand‑in‑hand with Redaction for indexing.

### Environment Setup Requirements
- **IDE**: Visual Studio 2019 or later.  
- **Framework**: .NET Core 3.1, .NET 5, or .NET 6.  
- **OS Compatibility**: Windows, Linux, macOS.

### Knowledge Prerequisites
Basic C# skills and a high‑level understanding of faceted search concepts will help, but the step‑by‑step guide is friendly to newcomers as well.

## Setting Up GroupDocs.Redaction for .NET

### Installation Information
You can add the GroupDocs.Redaction package using any of the following methods:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Search for "GroupDocs.Redaction" and install the latest version.

### License Acquisition Steps
To unlock all features, start with a free trial or obtain a permanent license:

1. Visit [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) to explore licensing options.  
2. Follow the on‑screen instructions to receive your trial or purchased license file.

### Basic Initialization and Setup
Once the package is installed, initialize the Redactor in your application:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## How to create search index groupdocs

Below we break the implementation into two parts: **Simple Faceted Search** and **Complex Query**. Each part shows how to **create a search index groupdocs**, add documents, and run queries.

### Feature 1: Simple Faceted Search

**Overview**  
Faceted search lets users narrow results by selecting multiple criteria. This section demonstrates a straightforward approach using GroupDocs.Search.

#### Step 1: Define Index and Documents Folders
Set up the folder paths where the index will live and where your source documents reside.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Step 2: Create an Index
Initialize the search index in the folder you defined.

```csharp
Index index = new Index(indexFolder);
```

#### Step 3: Add Documents to the Index
Load your documents so they become searchable.

```csharp
index.Add(documentsFolder);
```

#### Step 4: Perform a Text Query Search
Run a basic text query against the **content** field.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Step 5: Execute an Object Query Search
Use object‑oriented queries for finer control.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Feature 2: Complex Query

**Overview**  
When you need to combine multiple filters—such as filename patterns and phrase matches—you can build a complex query using logical operators.

#### Step 1: Define Index and Documents Folders
Reuse the same folder structure for a more advanced scenario.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Step 2: Create an Index and Add Documents
(See steps 2‑3 from the simple example; they remain the same.)

#### Step 3: Execute Text Query Search
Run a compound text query that mixes filename and content criteria.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Step 4: Build and Execute Object Queries
Construct the same logic programmatically.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Continue combining phrases, ranges, and boolean operators to match your exact business rules.

## Practical Applications

1. **E‑Commerce Platforms** – Filter products by category, price, and rating.  
2. **Document Management Systems** – Locate contracts by author, date, or confidentiality level.  
3. **Content Portals** – Let readers drill down by tags, topics, and publication dates.

## Performance Considerations

- **Index Refresh**: Regularly re‑index new or updated files to keep search fast.  
- **Memory Management**: Dispose of `Index` objects when done, especially for large data sets.  
- **Asynchronous Indexing**: Use `Task.Run` or background services to avoid UI freezes during heavy indexing.

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **Index not found** | Verify `indexFolder` path and ensure the folder has write permissions. |
| **No results returned** | Check that the fields you query (e.g., `Content`, `Filename`) are indexed. |
| **Out‑of‑memory errors** | Process documents in batches and consider increasing the .NET GC heap size. |

## Frequently Asked Questions

**Q: What is faceted search?**  
A: Faceted search allows users to refine results using multiple, independent filters such as category, date, or author.

**Q: How do I handle large datasets with GroupDocs.Search?**  
A: Use incremental indexing, batch processing, and asynchronous operations to keep memory usage low and performance high.

**Q: Can I integrate GroupDocs functionalities into existing .NET applications?**  
A: Yes, the libraries are designed for seamless integration with any .NET project.

**Q: What are some common issues with faceted search?**  
A: Complex query syntax and ensuring all relevant fields are indexed are typical challenges; proper testing and index maintenance mitigate them.

**Q: How do I acquire a temporary license for GroupDocs?**  
A: Visit the [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) to apply for a trial license that unlocks full functionality during evaluation.

## Resources
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Last Updated:** 2026-04-02  
**Tested With:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Author:** GroupDocs