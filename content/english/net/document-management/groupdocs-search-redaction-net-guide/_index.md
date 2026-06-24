---
title: "GroupDocs.Search & Redaction in .NET – redact sensitive data"
description: "Learn how to redact sensitive data in .NET using GroupDocs.Search and Redaction, and discover how to add documents to index for searching large documents."
date: "2026-04-27"
weight: 1
url: "/net/document-management/groupdocs-search-redaction-net-guide/"
keywords:
  - redact sensitive data
  - add documents to index
  - search large documents
type: docs
---

# GroupDocs.Search & Redaction in .NET – redact sensitive data

Managing vast amounts of documents can be daunting, especially when you need to **redact sensitive data** while still providing fast search capabilities. In this guide we’ll walk through setting up GroupDocs.Search together with GroupDocs.Redaction, show you how to **add documents to index**, perform efficient **search large documents** operations, and keep everything compliant with privacy requirements.

## Quick Answers
- **What does “redact sensitive data” mean?** It means permanently removing or masking confidential information from documents.
- **Which libraries do I need?** GroupDocs.Search and GroupDocs.Redaction for .NET (available via NuGet).
- **Can I index .NET projects automatically?** Yes – see the “How to index .NET” section for step‑by‑step guidance.
- **How do I handle huge files?** Use chunk‑based searching to process data in manageable portions.
- **Is a license required for production?** A valid GroupDocs license is needed for production use; free trials are available.

## What is redact sensitive data?
Redacting sensitive data is the process of permanently removing or obscuring personal, financial, or classified information from a document so that it cannot be recovered or viewed by unauthorized users.

## Why combine GroupDocs.Search with Redaction?
- **Speed:** Build searchable indexes that return results in milliseconds.  
- **Security:** Apply redaction rules before documents are shared or stored.  
- **Scalability:** Chunk search lets you work with terabytes of text without exhausting memory.  
- **Compliance:** Meet GDPR, HIPAA, and other regulations by ensuring confidential data never leaks.

## Prerequisites
- .NET development environment (Visual Studio recommended).  
- Basic C# knowledge.  
- Access to NuGet to install the required packages.

## Setting Up GroupDocs.Redaction for .NET

### Installation via .NET CLI
```bash
dotnet add package GroupDocs.Redaction
```

### Package Manager Installation
```powershell
Install-Package GroupDocs.Redaction
```

### NuGet Package Manager UI
Search for **"GroupDocs.Redaction"** and install the latest version.

### License Acquisition Steps
- **Free Trial:** Start with a free trial to explore features.  
- **Temporary License:** Request a temporary license for extended access.  
- **Purchase:** Consider purchasing for long‑term production use.

### Basic Initialization and Setup
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## Implementation Guide

### How to index .NET projects with GroupDocs.Search
Below we break the implementation into clear, numbered steps so you can follow along easily.

#### Step 1: Specify the Index Folder
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*Why?* Defining a dedicated folder keeps your index organized and isolated from raw documents.

#### Step 2: Create and Configure the Index
```csharp
Index index = new Index(indexFolder);
```
*Purpose:* Instantiates a new searchable index at the location you defined.

#### Step 3: **Add documents to index**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*Explanation:* Each call adds a file (or a folder) to the index, making its content searchable.

### Search large documents with Chunk Search
Chunk search lets you break massive files into smaller pieces, keeping memory usage low.

#### Step 1: Define the Search Query
```csharp
string query = "invitation";
```
*Purpose:* The term you are looking for across all indexed files.

#### Step 2: Configure Chunk Search Options
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*Explanation:* Enabling `IsChunkSearch` tells the engine to process data in chunks.

#### Step 3: Execute Initial Search
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*Result:* Shows how many documents contain the term and how many total occurrences were found.

#### Step 4: Continue with Subsequent Chunks
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*Why this loop?* It ensures you retrieve results from every chunk until the entire dataset is processed.

### How to redact sensitive data with GroupDocs.Redaction
After you locate the information you need to protect, apply redaction rules.

#### Step 1: Initialize Redaction Settings
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### Step 2: Apply Redactions
Use the `Redactor` class (not shown here to keep the original code intact) to define patterns, text, or images you want to mask.  
*Pro tip:* Test your redaction rules on a copy of the document first to avoid accidental data loss.

## Practical Applications
These capabilities shine in many industries:

1. **Legal Document Management** – Search case files quickly while redacting client‑confidential details.  
2. **Healthcare Data Handling** – Protect patient PHI while allowing clinicians to find relevant records.  
3. **Financial Auditing** – Index massive transaction logs and redact account numbers or personal identifiers.

## Performance Considerations
- **Optimize Indexing:** Re‑index only changed files to keep the index fresh without unnecessary work.  
- **Manage Resources:** Adjust chunk sizes (`options.ChunkSize`) based on your server’s RAM.  
- **Async Operations:** For large batches, use asynchronous indexing to keep your UI responsive.

## Frequently Asked Questions

**Q: How do I handle large files efficiently?**  
A: Use chunk‑based searches (`IsChunkSearch = true`) to process data in smaller pieces, reducing memory pressure.

**Q: Can GroupDocs.Redaction work with encrypted documents?**  
A: Yes – decrypt the file first, apply redaction, then re‑encrypt if needed.

**Q: What licensing options are available?**  
A: Free trial, temporary license for evaluation, and full commercial licenses for production.

**Q: How can I troubleshoot index errors?**  
A: Verify that the index folder path is correct, ensure the application has read/write permissions, and check that all document formats are supported.

**Q: Is it possible to customize search queries further?**  
A: Absolutely. You can combine Boolean operators, wildcards, and proximity searches using the `SearchOptions` API.

## Resources
- **Documentation:** [GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **API Reference:** [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/net/)  
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Request Here](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-04-27  
**Tested With:** GroupDocs.Search 23.9 and GroupDocs.Redaction 23.9 for .NET  
**Author:** GroupDocs