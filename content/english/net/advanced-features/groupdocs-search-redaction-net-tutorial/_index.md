---
title: "Search Legal Documents with GroupDocs Search & Redaction for .NET"
description: "Learn how to search legal documents and manage indexes using GroupDocs.Search, and integrate redaction for medical records with GroupDocs.Redaction in .NET."
date: "2026-04-04"
weight: 1
url: "/net/advanced-features/groupdocs-search-redaction-net-tutorial/"
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
type: docs
---
# Search Legal Documents with GroupDocs Search & Redaction in .NET

In today’s data‑driven environment, **searching legal documents** quickly and securely is a critical requirement for any organization. Whether you’re handling contracts, court filings, or compliance reports, GroupDocs.Search gives you a fast, scalable index, while GroupDocs.Redaction ensures sensitive information stays hidden. This tutorial walks you through setting up a searchable index, adding documents from multiple folders, and configuring redaction so you can safely search medical records and other confidential files.

## Quick Answers
- **What does GroupDocs.Search do?** It creates a full‑text searchable index for a wide range of document formats.  
- **Can I redact information before searching?** Yes – use GroupDocs.Redaction to mask or remove sensitive data.  
- **How do I add documents to the index?** Call `index.Add("folderPath")` for each folder you want to include.  
- **What file types are supported?** PDFs, DOCX, PPTX, TXT, and many more.  
- **Do I need a license for production?** A temporary trial is available; a permanent license is required for commercial use.

## Prerequisites
To follow this tutorial, make sure you have:
- .NET Core SDK (3.1 or later) installed.
- Visual Studio Code, Visual Studio, or another IDE that supports .NET.
- Basic familiarity with C# programming.

### License Acquisition
You can start with a free trial of both libraries. For extended usage, consider acquiring a temporary license or purchasing one from the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

## Installing the Required Packages

**GroupDocs.Search Installation:**  
Using **.NET CLI**, run:
```bash
dotnet add package GroupDocs.Search
```
Alternatively, use the Package Manager Console in Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction Installation:**  
- Use .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Or, through Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Visit the NuGet Package Manager UI and search for "GroupDocs.Redaction" to install it if you prefer a GUI.

## Configure Redactor Settings
Before you start redacting, you may want to tweak the redactor behavior (e.g., set the redaction color or define custom patterns). The following snippet shows the basic initialization:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Pro tip:** Adjust `redactorSettings` to match your organization’s compliance policies (e.g., replace text with black boxes, apply OCR before redaction, etc.).

## Implementation Guide

### How to Search Legal Documents?
Creating a searchable index is the foundation for fast retrieval of legal documents. GroupDocs.Search lets you point to any folder, build an index, and then execute complex queries across thousands of files.

### How to Add Documents to Index
Adding documents is straightforward—simply point the library at the directories that hold your files. You can add multiple folders, which is handy when your legal corpus is spread across different locations.

#### Creating and Managing an Index
**Overview:**  
Creating an index is the first step toward efficient document search operations. GroupDocs.Search allows you to create a searchable index in any directory of your choice, enabling quick retrieval of documents.

##### Step 1: Create the Index
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Explanation:* `Index` initializes a search index at the specified directory. Ensure the path reflects your project's folder structure.

##### Step 2: Adding Documents to an Index
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Explanation:* The `Add` method scans the given folder and includes every supported document in the index. Use this to **add documents to index** from multiple sources, such as contracts, case files, or medical records.

### Retrieving and Displaying Indexing Reports
**Overview:**  
Indexing reports give you insight into how many documents were processed, total term count, and storage size—essential metrics for performance tuning.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Explanation:* `GetIndexingReports` returns an array of reports that detail the indexing process, helping you monitor and optimize performance.

## Practical Applications
1. **Legal Document Management:** Automate indexing of case files for instant retrieval of statutes, briefs, and judgments.  
2. **Medical Records System:** Search patient records while preserving privacy using GroupDocs.Redaction to mask PHI.  
3. **Corporate HR Portal:** Combine searchable employee files with redaction to protect personal data.

## Performance Considerations
- **Optimizing Index Size:** Periodically prune outdated entries and rebuild the index to keep it lean.  
- **Memory Management:** Leverage .NET’s garbage collector; dispose of `Index` objects when they’re no longer needed.  
- **Scalability Best Practices:** Store the index on fast SSD storage and consider sharding large corpora across multiple indexes.

## Frequently Asked Questions

**Q: What are the primary uses of GroupDocs.Search?**  
A: It’s ideal for creating searchable indexes from large document collections, enabling fast retrieval of legal and medical files.

**Q: How does GroupDocs.Redaction ensure data privacy?**  
A: It lets you define redaction patterns that permanently remove or mask sensitive information before the document is indexed or shared.

**Q: Can I use these libraries in a cloud environment?**  
A: Yes—both libraries work in Azure, AWS, or any containerized .NET deployment with proper licensing.

**Q: What file formats are supported by GroupDocs.Search?**  
A: PDFs, Word, Excel, PowerPoint, TXT, HTML, and many more enterprise formats.

**Q: How do I troubleshoot indexing errors?**  
A: Verify folder paths, check file permissions, and review the console output from `IndexingReport` for specific error codes.

## Resources
- **Documentation:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API Reference:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Last Updated:** 2026-04-04  
**Tested With:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs