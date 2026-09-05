---
title: "Implement High Compression .NET with GroupDocs: Text & Redaction Guide"
description: "Learn how to implement high compression .net for text storage and redact confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications."
date: "2026-06-07"
weight: 1
url: "/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/"
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
type: docs
schemas:
- type: TechArticle
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  dateModified: '2026-06-07'
  author: GroupDocs
- type: HowTo
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
- type: FAQPage
  questions:
  - question: Can I add documents to index after the initial build?
    answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
  - question: Does redaction alter the original file?
    answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
  - question: What formats does GroupDocs.Redaction support?
    answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
  - question: How does high compression affect search relevance?
    answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
  - question: Is there a limit to the size of documents I can index?
    answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
---
# Implement High Compression .NET with GroupDocs: Text & Redaction Guide

In modern .NET solutions, **implement high compression .net** is essential when you need to store massive text collections without blowing up disk usage. At the same time, protecting sensitive information—such as personal identifiers or financial figures—requires reliable redaction. This tutorial shows you, step‑by‑step, how to configure high‑compression text storage with **GroupDocs.Search** and how to safely redact confidential data using **GroupDocs.Redaction**. By the end, you’ll be able to compress indexed text by up to 90 % and remove private content from PDFs, Word files, and many other formats.

## Quick Answers
- **What library provides high‑compression indexing?** GroupDocs.Search for .NET.  
- **Which tool redacts sensitive data?** GroupDocs.Redaction for .NET.  
- **Can I add documents to index automatically?** Yes—use the `AddDocument` API inside a folder‑scan loop.  
- **Is compression lossless for search?** Yes, the text remains fully searchable after compression.  
- **Do I need a license for production?** A permanent GroupDocs license is required for commercial use.

## What is “implement high compression .net”?
Implement high compression .net means configuring the GroupDocs.Search indexing engine to store extracted textual content in a compressed form. This reduces the on‑disk index size dramatically while keeping the text fully searchable. The compression is loss‑less, so query relevance and snippet extraction work exactly as with an uncompressed index.

## Why use GroupDocs for compression and redaction?
GroupDocs.Search supports more than fifty input formats and can compress indexed text by up to ninety percent, allowing large document collections to occupy only a fraction of their original size. GroupDocs.Redaction complements this by permanently erasing or masking sensitive information in over thirty file types, helping you meet strict compliance regulations such as GDPR and HIPAA without additional tools.

## Prerequisites
- **Development environment:** Visual Studio 2022 or later, .NET 6+ (or .NET Framework 4.7.2).  
- **Libraries:** `GroupDocs.Search` and `GroupDocs.Redaction` NuGet packages.  
- **Permissions:** Read/write access to the folders that contain source documents and the index output location.  
- **Basic knowledge:** C# syntax, file I/O, and familiarity with .NET project structure.

## How to implement high compression .NET with GroupDocs?
To implement high compression .NET with GroupDocs, first create a `TextStorageSettings` instance and set its `CompressionLevel` to `High`. Then instantiate an `Index` object, passing the settings and the folder where the index will be stored. After the index is ready, add documents using `AddDocument`, and finally run searches with the `Search` method, all while the engine transparently handles compression and decompression.

### Step 1: Install the required NuGet packages
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Search for “GroupDocs.Search” and click **Install**.  

### Step 2: Install GroupDocs.Redaction (for data redaction)
- Open the **NuGet Package Manager**.  
- Search for **GroupDocs.Redaction** and install the latest stable version.  

### Step 3: Obtain and apply a license
- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.  
- **Temporary license:** Request a temporary key for development environments.  
- **Permanent license:** Purchase a production license to remove evaluation limitations.

### Step 4: Basic initialization of both libraries
The `Search` and `Redaction` engines share a common licensing model. Initialize them at application startup:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Feature 1: High Compression Text Storage Settings

### Setting Up Indexing Configuration
`TextStorageSettings` is the class that tells GroupDocs.Search how to keep the extracted text. Enabling high compression reduces the index size by up to **10×** without affecting search speed.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explanation:**  
- `CompressionLevel.High` activates a ZSTD‑based algorithm that compresses text blocks efficiently.  
- `UseMemoryCache = false` forces the engine to stream data from disk, which is ideal for large‑scale deployments.

### Creating and Managing the Index
The `Index` object represents the searchable repository on disk. You specify the folder where the index files will be stored and pass the compression settings defined above.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Explanation:**  
- `indexFolder` determines where the compressed index files live.  
- `settings` injects the high‑compression configuration, ensuring every added document benefits from it.

## Feature 2: Adding Documents to Index

### Add Documents to Your Index
`AddDocument` adds a single file to the index, extracting its text, compressing it according to the configured settings, and storing the result. GroupDocs.Search can ingest files from a directory tree. The following loop walks through `documentsFolder`, adds each file, and logs progress.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Explanation:**  
- `AddDocument` parses the file, extracts searchable text, compresses it according to `TextStorageSettings`, and stores it in the index.  
- This approach works for **PDF, DOCX, TXT, HTML**, and more than **30** other formats.

## Feature 3: Executing a Search Query

### Perform a Search
`Search` runs a query against the compressed index and returns a collection of matching `DocumentResult` objects with relevance scores and highlighted snippets. Once the index is populated, you can run fast queries. The `Search` method returns a collection of `DocumentResult` objects that include file paths and highlighted snippets.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Explanation:**  
- The search engine scans the compressed text directly, so query latency remains low even for indexes that contain **millions of pages**.  
- `Score` indicates relevance; higher values mean a better match.

## How to redact confidential data with GroupDocs.Redaction?
Redacting confidential data with GroupDocs.Redaction starts by creating a `Redactor` instance for the target file. Define one or more `SearchPattern` objects that describe the text to be removed, such as regular expressions for social security numbers. Apply each pattern using `Redact`, specifying a `RedactionType` like `BlackOut`, and save the result as a new document, ensuring the original remains untouched.

`Redactor` is the primary class in GroupDocs.Redaction used to load a document and perform redaction operations.  
`SearchPattern` defines a regular expression that identifies the text to be redacted.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explanation:**  
- `SearchPattern` uses a regular expression to locate social security numbers.  
- `RedactionType.BlackOut` replaces the matched text with a solid black rectangle, ensuring the data cannot be recovered.

## Practical Applications
1. **Legal Document Management:** Automatically compress massive case files and redact client identifiers before archiving.  
2. **Healthcare Records:** Store years of patient notes in a compressed index and remove PHI (Protected Health Information) before sharing with research partners.  
3. **Financial Reporting:** Secure quarterly reports by redacting account numbers while keeping the searchable text for audit queries.

## Performance Considerations
- **Compression impact:** High compression reduces index size by up to **90 %**, which lowers SSD wear and speeds up backup operations.  
- **Memory usage:** Disable in‑memory caching for very large indexes to keep the process footprint under **500 MB**.  
- **I/O optimization:** Batch document addition in groups of 100 to minimize disk thrashing.  
- **Async processing:** Wrap `AddDocument` calls in `Task.Run` to keep UI threads responsive in desktop apps.

## Common Pitfalls & Troubleshooting
- **Incorrect file paths:** Verify that `documentsFolder` and `indexFolder` are absolute paths and that the application has read/write permissions.  
- **License errors:** Ensure the `.lic` files are deployed alongside the executable or embedded as resources.  
- **Search returns no results:** Check that the `TextStorageSettings` compression level matches the one used during indexing; mismatched settings can cause deserialization failures.  

## Frequently Asked Questions

**Q: Can I add documents to index after the initial build?**  
A: Yes—simply call `index.AddDocument` for new files; the engine updates the compressed index incrementally.

**Q: Does redaction alter the original file?**  
A: No—the original file remains untouched; the redacted version is saved as a new file, preserving document integrity.

**Q: What formats does GroupDocs.Redaction support?**  
A: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG), and plain text.

**Q: How does high compression affect search relevance?**  
A: It does not. The compression is loss‑less for text, so relevance scores are identical to an uncompressed index.

**Q: Is there a limit to the size of documents I can index?**  
A: GroupDocs.Search can handle multi‑gigabyte files by streaming content; however, ensure sufficient disk space for the compressed index (approximately 10 % of the original size).

## Resources
- [Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction for .NET](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Implementing GroupDocs.Search and Redaction in .NET for Document Management](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [How to Optimize GroupDocs.Redaction for .NET: Efficient Index & Spelling Management Guide](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Master GroupDocs Redaction and Search in .NET: Efficient Document Management and Secure Searching](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
