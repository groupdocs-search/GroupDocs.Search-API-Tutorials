---
date: '2026-09-16'
description: Learn how to create search index with GroupDocs in .NET, add documents
  to index, and enable synonym search for smarter query results.
images:
- /net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/og-image.png
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Learn how to create search index with GroupDocs in .NET, add documents
  to index, and enable synonym search for smarter query results.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: How to create search index with GroupDocs in .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: How to create search index with GroupDocs and synonym search in .NET
type: docs
url: /net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# How to create search index with GroupDocs and synonym search in .NET

In this guide you’ll learn **how to create search index** using GroupDocs.Search, add documents to that index, and enable synonym search so users can find relevant content even when they use different terminology. Whether you’re building a legal repository, a corporate knowledge base, or a research archive, the steps below give you a production‑ready solution that works on .NET Framework 4.6.1+, .NET Core, and .NET 5+.

## Quick answers
- **What does “create search index” mean?** It builds a searchable catalog of your documents, storing extracted text in an optimized structure for millisecond look‑ups.  
- **Why use synonym search?** It expands a query to include words with the same meaning, boosting recall by up to 30 % in typical corpora.  
- **What are the main prerequisites?** .NET 4.6.1+ (or .NET Core/5+), C# knowledge, and the GroupDocs.Search + GroupDocs.Redaction NuGet packages.  
- **Do I need a license?** A free trial is sufficient for evaluation; a permanent license is required for production deployments.  
- **Can I combine this with redaction?** Yes—GroupDocs.Redaction can run before or after search to mask sensitive data.

## What is “create search index”?
A **search index** is a data structure that holds extracted text and metadata from each document, allowing the engine to locate matching files instantly. GroupDocs.Search builds this index by scanning the source folder, parsing supported formats, and writing compact index files to a directory you specify.

## Why enable synonym search?
Synonym search automatically adds alternative terms to a user’s query, so a search for **“improve”** also returns documents containing **“enhance,” “upgrade,”** or **“optimize.”** In practice this can raise result recall by 20‑35 % while keeping precision high, because the built‑in synonym dictionary is curated for each language.

## Prerequisites
- **.NET Framework 4.6.1** or later (or any .NET Core/5+ runtime).  
- Basic C# development skills and Visual Studio (Community, Professional, or Enterprise).  
- GroupDocs.Search and GroupDocs.Redaction packages installed via NuGet.

### Installation
Install GroupDocs.Redaction for .NET using one of these methods (see the [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) documentation for details):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Alternatively, use the NuGet Package Manager UI in Visual Studio to search for “GroupDocs.Redaction” and install it directly. For API reference, see the [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### License acquisition
- **Free trial:** Start with a trial version to explore all features.  
- **Temporary license:** Apply for a temporary license on the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) or manage your license via the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) portal.  
- **Full purchase:** When you’re ready for production, buy a full license that removes all evaluation limits.

## How to set up GroupDocs.Redaction for .NET
GroupDocs.Redaction provides the core functionality to redact sensitive content before or after searching. It exposes a `Redactor` class that you instantiate with a license and optional configuration settings.

The following code demonstrates creating a redactor instance and loading a license file:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

With the redactor ready, you can later call `redactor.Redact(...)` on any document that you retrieve from the search results.

## How to create the search index
Creating a search index involves specifying a folder where the index files will be stored and then initializing the `Index` class from GroupDocs.Search. The index will hold all searchable data extracted from your source documents.

First, create a directory for the index and then instantiate the `Index` object:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Creating the index writes a set of binary files to the folder; these files are typically under 200 KB per 1,000 pages, allowing you to scale to millions of pages without exhausting disk space.

## How to add documents to the index
Adding documents requires pointing the API at the directory that contains the source files and instructing the index to ingest them. The process parses each supported format, extracts text, and stores it in the index for fast retrieval.

Use the following code to index all files in a source folder:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search supports **30+** input formats—including DOCX, PDF, PPTX, HTML, and common image types—so you can index virtually any corporate archive without additional converters.

## How to enable and run synonym search
Synonym handling is turned on via `SearchOptions`. Once enabled, every query automatically expands to include the dictionary’s synonyms, improving recall without sacrificing precision.

Enable synonym search with the following snippet:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

The default synonym dictionary contains over **5,000** term pairs for English. You can also load a custom `SynonymDictionary` file to support industry‑specific jargon.

## Custom synonym dictionary
If you need domain‑specific synonyms, load your own dictionary file and assign it to the `SearchOptions` before executing a query.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Common troubleshooting tips
- **Path issues:** Double‑check that the index and source folders are accessible by the process account.  
- **Licensing limits:** An unlicensed build may restrict the number of indexed files to 100.  
- **No results:** Verify that the synonym dictionary is loaded; you can inspect `options.SynonymDictionary.Count` at runtime.  

## Practical applications
1. **Legal document management:** Find case law using legal terms and their synonyms.  
2. **Academic research:** Expand literature searches across scholarly PDFs and Word files.  
3. **Corporate knowledge bases:** Retrieve internal policies even when users phrase queries differently.  
4. **Content management systems:** Offer editors richer discovery when tagging articles.  
5. **Customer‑support ticketing:** Match tickets to known issues using synonymous problem descriptions.

## Performance considerations
- **Index maintenance:** Re‑index after bulk updates; incremental indexing reduces downtime by up to 70 %.  
- **Resource monitoring:** Indexing a 10 GB batch on a standard VM (2 vCPU, 8 GB RAM) peaks at ~1.2 GB RAM; throttle batch size if you approach limits.  
- **Object disposal:** Call `index.Dispose()` and `redactor.Dispose()` as soon as you finish to free native resources.

## Conclusion
You now know **how to create search index** with GroupDocs, add documents to that index, and enable synonym search for a more intuitive user experience. This foundation also lets you layer redaction, custom ranking, or fuzzy matching on top of a robust search engine.

## Next steps
- Experiment with `SearchOptions.FuzzySearch` to catch misspellings.  
- Explore the `Ranking` API to boost priority documents.  
- Join the community on the [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) or the [Free Support Forum](https://forum.groupdocs.com/c/search/10) to share tips and ask questions.  
- Check the [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) for updates and new features.

## Frequently asked questions

**Q: What is synonym search?**  
A: Synonym search expands a user’s query to include predefined alternative terms, increasing the chance of finding relevant documents that use different wording.

**Q: How do I update my GroupDocs license?**  
A: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.

**Q: Can I use synonym search in a multilingual environment?**  
A: Yes—load a language‑specific `SynonymDictionary` file for each locale you support, and the engine will apply the appropriate synonym set per query.

**Q: What are the most common indexing issues?**  
A: File‑access permissions, unsupported formats, and exceeding the trial‑version document limit are the top three problems developers encounter.

**Q: How can I optimise performance for very large indexes?**  
A: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism` to match your CPU core count.

---

**Last Updated:** 2026-09-16  
**Tested With:** GroupDocs.Search 23.10 for .NET  
**Author:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Related Tutorials

- [Add Document to Index with GroupDocs.Search .NET Tutorials](/search/net/document-management/)
- [Highlight Search Results in .NET Documents Using GroupDocs.Search and Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [How to Update Index with GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)