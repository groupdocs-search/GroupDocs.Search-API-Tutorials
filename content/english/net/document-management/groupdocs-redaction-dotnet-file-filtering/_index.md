---
title: "How to Filter Files with GroupDocs.Redaction for .NET"
description: "Learn how to filter files using GroupDocs.Redaction for .NET, including filter by creation date, file size, modification date, and how to apply NOT filters."
date: "2026-04-21"
weight: 1
url: "/net/document-management/groupdocs-redaction-dotnet-file-filtering/"
keywords:
  - how to filter files
  - filter by creation date
  - filter by file size
  - filter by modification date
  - apply not filter
type: docs
---

# How to Filter Files with GroupDocs.Redaction for .NET

In today’s fast‑moving digital environment, **how to filter files** efficiently can make or break your productivity. Whether you need to isolate documents by extension, creation date, size, or modification date, a solid filtering strategy saves time, reduces storage costs, and keeps your search index tidy. In this tutorial we’ll walk through real‑world examples using GroupDocs.Redaction for .NET, showing you exactly how to filter files to meet common business needs.

## Quick Answers
- **What library do I need?** GroupDocs.Redaction for .NET (install via NuGet).  
- **Can I filter by creation date?** Yes – use `CreateCreationTimeRange`.  
- **How do I exclude certain types?** Apply a NOT filter with `DocumentFilter.CreateNot`.  
- **Is file size filtering supported?** Absolutely, via `CreateFileLengthRange` or upper/lower bounds.  
- **Do I need a license?** A trial or full license is required for production use.

## What is file filtering with GroupDocs.Redaction?
File filtering lets you tell the indexing engine which documents to include or ignore based on metadata such as extension, dates, path patterns, or size. By defining precise `DocumentFilter` rules, you keep your index lean and your searches fast.

## Why use GroupDocs.Redaction for .NET?
- **Built‑in filter helpers** – no need to write custom file‑system code.  
- **Logical operators** – combine multiple criteria with AND, OR, and NOT.  
- **Performance‑optimized** – filters are applied during indexing, not after.  
- **Cross‑platform** – works with .NET Framework, .NET Core, and .NET 5/6+.

## Prerequisites
- .NET Framework 4.6+ or .NET Core 3.1+ installed.  
- Visual Studio or your preferred C# IDE.  
- Basic C# knowledge.  

### Required Libraries & Setup
Install the NuGet package using your preferred method:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Pro tip:** After installing, add your license file to the project root and call `License.SetLicense("license-file-path")` before creating any Redactor or Index objects.

## Setting Up GroupDocs.Redaction for .NET

First, create a `Redactor` instance that points to the document you want to work with:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Why this matters:** Initializing the Redactor guarantees the library is ready to apply filters and redaction rules later in the workflow.

## How to filter files by extension

Filtering by file extension is the most common way to narrow down a document set. Below we only keep FB2, EPUB, and TXT files.

### Filter by file extension

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## How to apply NOT filter to exclude unwanted types

If you need to **apply NOT filter** logic—say, exclude HTML and PDF files—use `CreateNot`.

### Exclude HTM, HTML, and PDF files

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## How to filter files by creation date

When you need to **filter by creation date**, specify a start and end `DateTime`.

### Filter by creation date range

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## How to filter files by modification date

Similar to creation dates, you can limit results to files modified before a certain point.

### Filter by modification date

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## How to filter files by path using regular expressions

If your folder structure follows naming conventions, a regex can target specific paths.

### Filter by file path pattern

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## How to filter files by size

Controlling document size is essential when dealing with bandwidth or storage limits.

### Filter by file size (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## How to combine multiple conditions with AND

When you need **how to filter files** using several criteria at once, combine them with `CreateAnd`.

### Logical AND example

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## How to combine multiple conditions with OR

Use `CreateOr` when any of several rules should pass.

### Logical OR example

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Common Issues and Solutions
- **Filter not applied:** Ensure you assign `settings.DocumentFilter` **before** creating the `Index` instance.  
- **Unexpected files appear:** Double‑check file extensions include the leading dot (`.txt`).  
- **Performance slowdown:** Combine filters with AND to reduce the number of files scanned early in the indexing pipeline.  
- **Regex errors:** Escape special characters in your path pattern or use `RegexOptions.IgnoreCase` for case‑insensitive matches.

## Frequently Asked Questions

**Q: Can I combine a NOT filter with an AND filter?**  
A: Yes. Build the NOT filter first (`DocumentFilter.CreateNot`) and then include it as one of the arguments to `DocumentFilter.CreateAnd`.

**Q: How do I filter files larger than 10 MB?**  
A: Use `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` to include only files exceeding that size.

**Q: Is it possible to filter by both creation and modification dates simultaneously?**  
A: Absolutely. Create each filter separately and combine them with `CreateAnd`.

**Q: Do these filters work with cloud storage paths?**  
A: The filters operate on the local file system. For cloud sources, download files to a temporary folder first, then apply the same filters.

**Q: Will changing the filter require re‑indexing?**  
A: Yes. Filters are evaluated when you call `index.Add`. Changing a filter means you need to rebuild the index to reflect the new criteria.

## Conclusion

By mastering **how to filter files** with GroupDocs.Redaction for .NET—whether by extension, creation date, modification date, file size, or using NOT logic—you can streamline document management, keep indexes performant, and focus on the content that truly matters. Experiment with the logical operators to tailor the filtering to your exact business rules, and you’ll see immediate gains in speed and storage efficiency.

---

**Last Updated:** 2026-04-21  
**Tested With:** GroupDocs.Redaction 24.11 for .NET  
**Author:** GroupDocs  

---