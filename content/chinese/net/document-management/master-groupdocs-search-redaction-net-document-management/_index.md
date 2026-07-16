---
date: '2026-07-16'
description: 了解如何在 .NET 中使用 GroupDocs Search 和 Redaction 对文档进行脱敏，并突出显示搜索结果，以实现更快速的文档管理。
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: 了解如何在 .NET 中使用 GroupDocs Search 和 Redaction 对文档进行脱敏，并突出显示搜索结果，以实现更快速的文档管理。
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: 如何使用 GroupDocs Search 在 .NET 中对文档进行脱敏
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: 如何使用 GroupDocs Search 在 .NET 中对文档进行脱敏
type: docs
url: /zh/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# 使用 GroupDocs Search 在 .NET 中编辑文档

在现代企业中，**如何快速且安全地编辑文档**是日常挑战。将 GroupDocs.Search 与 GroupDocs.Redaction for .NET 结合使用，可提供一个强大的开箱即用解决方案，不仅可以编辑敏感内容，还能执行模糊搜索并在 HTML 中**高亮搜索结果**。本教程将指导您安装库、创建索引、运行模糊查询以及生成高亮输出——全部配有清晰、可直接用于生产的代码片段。

## 快速答案
- **第一步是什么？** 安装 GroupDocs.Search 和 GroupDocs.Redaction NuGet 包。  
- **我可以编辑 PDF 和 Word 文件吗？** 是的，两个格式均开箱即支持。  
- **模糊搜索可用吗？** 当然可以——您可以将准确度调节在 0% 到 100% 之间。  
- **开发需要许可证吗？** 免费试用许可证可用于测试；生产环境需要付费许可证。  
- **该解决方案在 .NET 6 上可用吗？** 是的，这些库兼容 .NET Framework 4.5+、.NET Core 3.1+、.NET 5+ 和 .NET 6+。

## 什么是 GroupDocs.Search？
GroupDocs.Search 是一个 .NET 库，提供跨 100 多种文件格式的快速索引和全文搜索。它能够在不将整个文件加载到内存的情况下处理高达 2 GB 的文档，非常适合大规模存储库。它支持增量索引、多语言分析，并可无缝集成到 .NET 应用程序中，使开发者能够以最少的代码构建强大的搜索体验。

## 为什么使用 GroupDocs.Redaction 进行文档编辑？
GroupDocs.Redaction 提供超过 30 种内置编辑模式，并支持批量处理，确保个人数据、机密条款或合规标记被永久删除。在基准测试中，对 500 页 PDF 的编辑耗时不足 2 秒，且引擎直接作用于文档内容流，确保编辑区域无法恢复，同时保持原始格式和布局。

## 前置条件
- **必需的库：** GroupDocs.Search, GroupDocs.Redaction  
- **支持的平台：** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE：** Visual Studio 2022 或更高版本（任意版本）  
- **基础技能：** 熟悉 C#、文件 I/O 和面向对象编程概念  

## 如何在 .NET 项目中设置 GroupDocs.Search 和 GroupDocs.Redaction？
通过 .NET CLI、Package Manager Console 或 UI 安装 NuGet 包，然后将许可证文件添加到项目中。这两步设置是编写任何索引或编辑代码之前所需的全部工作。添加包后，请将许可证文件放置在应用程序根目录，并在代码文件中引用相应的命名空间。

## 为 .NET 设置 GroupDocs.Redaction
要在 .NET 应用程序中开始使用 GroupDocs.Search 和 GroupDocs.Redaction，请按照以下安装步骤操作：

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜索 “GroupDocs.Redaction” 并安装最新版本。

### 获取许可证的步骤
1. **免费试用**：在 [GroupDocs](https://www.groupdocs.com) 注册以获取临时许可证。  
2. **购买**：如需完整功能，请在 GroupDocs 网站购买许可证。  
3. **临时许可证**：通过提供的链接获取，用于评估目的。  

#### 基本初始化和设置
`Index` 类表示存储在磁盘上的可搜索索引，并提供添加、更新和查询文档的方法。安装完成后，使用必要的配置初始化项目：  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## 实施指南

### 创建和索引文档
**概述**  
此功能演示如何通过为包含多个文件的文件夹创建索引来高效组织文档。

#### 步骤 1：定义路径  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### 模糊搜索设置与执行
**概述**  
模糊搜索允许在搜索词有细微差异时仍能找到文档。此功能展示了可调准确度的模糊搜索设置。

#### 步骤 1：启用模糊搜索  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### 在 HTML 格式中高亮搜索结果
**概述**  
高亮搜索结果可在文件中直观标记相关章节，便于快速分析。

#### 步骤 1：设置高压缩  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### 步骤 2：高亮并输出  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### 故障排除提示
- 确保路径正确指定，以避免文件未找到错误。  
- 确认已为目录的读写操作设置所有必要的权限。  

## 实际应用
1. **法律文档审查** – 在海量法律文库中快速定位案件相关术语。  
2. **学术研究** – 在数千篇论文中搜索特定方法论。  
3. **商业智能** – 从季度报告中提取关键指标，无需手动挖掘。  
4. **客户支持** – 扫描支持工单以发现重复问题，并在分析前编辑个人数据。  
5. **内容管理系统 (CMS)** – 通过模糊搜索和自动编辑敏感片段提升内容检索。  

## 性能考虑因素
- 优化索引存储设置，以平衡速度和磁盘使用。  
- 定期更新索引以保持数据最新，减少不必要的处理。  
- 及时释放未使用的对象以防止内存泄漏，尤其在处理大批量时。  

## 如何使用 GroupDocs Redaction 对 PDF 进行敏感信息编辑？
`Redactor` 是用于对受支持文档格式应用编辑模式的主要类。使用 `Redactor redactor = new Redactor("file.pdf")` 加载目标 PDF，定义编辑模式（例如 `redactor.AddRedaction(new RedactionPhrase("confidential"))`），然后调用 `redactor.Apply()` —— 库会在保留布局的同时用编辑内容覆盖原文件，确保受保护短语不留痕迹。

## 如何在模糊查询后以 HTML 高亮搜索结果？
`SearchResultHighlighter` 提供生成高亮 HTML 片段的实用工具。执行模糊查询后，获取匹配片段并传递给 `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")`。该方法使用提供的标签包装每个出现的词，生成的 HTML 片段可直接嵌入网页或保存为报告，方便终端用户查看每个匹配的上下文。

## 常见问题

**问：什么是模糊搜索？**  
答：模糊搜索寻找近似匹配，容忍拼写错误或查询词的轻微变体。

**问：我可以在商业项目中使用这些库吗？**  
答：可以，拥有有效的 GroupDocs 许可证即可获得商业使用权。

**问：如何高效处理大型文档集？**  
答：使用增量索引，调优 `IndexingOptions` 的批量大小，并安排定期重建索引以保持最佳性能。

**问：GroupDocs.Search 支持哪些文件格式？**  
答：支持超过 100 种格式，包括 PDF、DOCX、XLSX、PPTX、HTML、TXT，以及 JPEG、PNG 等图像类型。

**问：搜索和编辑是否支持多语言？**  
答：是的，库内置超过 30 种语言的分析器，能够在全球内容中实现准确的搜索和编辑。

## 资源
- [文档](https://docs.groupdocs.com/search/net/)  
- [文档](https://docs.groupdocs.com/search/net/)  
- [支持论坛](https://forum.groupdocs.com/c/search/10)  
- [API 参考](https://reference.groupdocs.com/redaction/net)  
- [下载](https://www.groupdocs.com/products/search-net)

---

**最后更新：** 2026-07-16  
**测试环境：** GroupDocs.Search 2.0.0 和 GroupDocs.Redaction 2.0.0 for .NET  
**作者：** GroupDocs

## 相关教程

- [在 .NET 文档中使用 GroupDocs.Search 和 Redaction 高亮搜索结果](/search/net/highlighting/highlight-search-results-net-groupdocs/)  
- [精通 GroupDocs Redaction 与 Search 在 .NET 中的使用：高效文档管理与安全搜索](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)  
- [使用 GroupDocs.Redaction .NET 精通文档编辑：索引与别名管理，实现安全文档管理](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)