---
title: "Filter by file extension in .NET using GroupDocs.Redaction"
description: "Learn how to filter by file extension and search only txt files with GroupDocs.Redaction for .NET—boost document management efficiency."
date: "2026-04-02"
weight: 1
url: "/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/"
keywords:
- filter by file extension
- how to filter documents
- search only txt files
type: docs
---
# Filter by file extension in .NET using GroupDocs.Redaction

Searching through a massive collection of files can feel overwhelming, especially when you only need results from specific file types. In this tutorial you’ll discover **how to filter by file extension** with GroupDocs.Redaction for .NET, allowing you to search only txt files or any other extension you choose. We’ll walk through setting up both file‑type and path‑based filters, so you can quickly locate exactly the documents you need.

## Quick Answers
- **What does “filter by file extension” do?** It limits a search to documents that match a given file extension (e.g., *.txt).  
- **Why use GroupDocs.Redaction for this?** It provides built‑in filtering APIs that are fast and easy to integrate.  
- **Do I need a license?** A free trial works for testing; a paid license is required for production.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Can I combine file‑type and path filters?** Yes—apply multiple filters for highly precise searches.

## What you’ll learn
- How to **filter by file extension** so only text files are searched.  
- How to set up **file path filters** to narrow results to specific folders or naming patterns.  
- Tips for keeping your index fast and memory‑efficient.

## Prerequisites

Before diving in, make sure you have:

- **GroupDocs.Redaction Library** installed and compatible with your .NET project.  
- A development environment such as Visual Studio or VS Code.  
- Basic C# knowledge and familiarity with .NET project structure.

## Setting Up GroupDocs.Redaction for .NET

First, add the library to your project.

**Using .NET CLI:**
```bash
dotnet add package GroupDocs.Redaction
```

**Using Package Manager:**
```bash
Install-Package GroupDocs.Redaction
```

Or locate “GroupDocs.Redaction” in the NuGet Package Manager UI and install the latest version.

### License Acquisition

You can start with a free trial or request a temporary license. For long‑term projects, purchase a license from the official site.

### Basic Initialization

After the package is installed, create an index that will hold references to your documents:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Implementation Guide

### Feature 1: Setting a filter for text documents (.txt)

#### How to filter by file extension for text documents

1. **Define the index and document folders**  
   Set the paths where your source files live:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Create an Index**  
   Load all files from the source folder into the index:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Configure Search Options with a file‑extension filter**  
   Tell the engine to consider only *.txt files:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Perform the search**  
   Run a query; the filter ensures non‑text files are ignored:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explanation*: The `Search` method returns matches that satisfy the filter, dramatically reducing noise and improving performance.

### Feature 2: FilePath Filters

#### Why use file path filters?

Sometimes you need to limit searches to a particular department folder or a set of files that share a naming convention. Path filters let you do exactly that.

1. **Define the index and document folders**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Create an Index**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Configure Search Options with a path‑based regular expression**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   This regular expression matches any file whose full path contains the word “Lorem”, letting you target specific sub‑folders.

4. **Execute the path‑based search**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Practical Applications
- **Legal Document Management** – Quickly locate relevant contracts stored as plain‑text files.  
- **Academic Research** – Pull only *.txt research notes that belong to a particular project folder.  
- **Corporate Reporting** – Filter internal reports by department path (e.g., `/Finance/2025/`).  

## Performance Considerations
- Index only the document types you actually need; unnecessary files increase index size and search time.  
- Keep your index up‑to‑date with a scheduled job that calls `index.Add()` for new or changed files.  
- Use simple regular expressions; overly complex patterns can slow down the search engine.  
- Dispose of `Index` objects when they’re no longer needed to free memory.

## Conclusion
You now know how to **filter by file extension** and apply **file path filters** using GroupDocs.Redaction for .NET. These techniques give you fine‑grained control over large document collections, making searches faster and more relevant. Next, experiment with combining multiple filters or integrating the search into a larger application workflow.

## FAQ Section

**Q1: Can I filter documents other than text files?**  
A1: Yes, GroupDocs.Redaction supports many formats. Change the argument in `CreateFileExtension` to the desired extension (e.g., ".pdf").

**Q2: How do I update my search index regularly?**  
A2: Schedule a background service or a cron job that runs `index.Add()` on the directories you want to keep fresh.

**Q3: Is there a performance impact when filtering by file path?**  
A3: Properly optimized regular expressions have minimal impact, but always benchmark with your own data set.

**Q4: Can I combine multiple filters for more refined searches?**  
A4: Absolutely. You can chain filters or create composite filters to target both file type and path simultaneously.

**Q5: Where can I find more resources on GroupDocs.Redaction?**  
A5: Visit the official documentation at [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) for detailed guides and API references.

## Frequently Asked Questions

**Q: Does the `SearchDocumentFilter` work with encrypted files?**  
A: The filter itself operates on file metadata, so encrypted files are still indexed if you provide the necessary decryption credentials during indexing.

**Q: Can I use wildcards instead of a regular expression for path filtering?**  
A: The API currently requires a regular expression, but you can simulate simple wildcards (e.g., `.*` for any characters).

**Q: How large can the index be before I need to consider sharding?**  
A: Indexes of several hundred gigabytes may benefit from splitting into multiple logical indexes; test performance as your collection grows.

**Q: Are there built‑in methods to remove documents from the index?**  
A: Yes—call `index.Delete(documentId)` or `index.DeleteAll()` to manage stale entries.

**Q: Is there a way to preview search results before loading the full document?**  
A: The `SearchResult` object includes snippet information that you can display in UI without opening the entire file.

## Resources
- **Documentation**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-04-02  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs