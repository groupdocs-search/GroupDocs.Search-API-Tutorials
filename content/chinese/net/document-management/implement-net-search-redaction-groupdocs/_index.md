---
date: '2026-06-12'
description: 了解如何在 .NET 中使用 GroupDocs.Search 和 GroupDocs.Redaction 搜索和脱敏文档，优化搜索性能并处理索引错误。
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: 如何在 .NET 中使用 GroupDocs.Search 和 GroupDocs.Redaction 搜索和脱敏文档
type: docs
url: /zh/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# 在 .NET 中使用 GroupDocs.Search 与 GroupDocs.Redaction 搜索和编辑文档

在现代企业环境中，**search and redact** 功能对于在保护敏感信息的同时保持文档易于检索至关重要。本教程将指导您构建一个强大的 .NET 解决方案，结合 GroupDocs.Search 实现快速全文搜索，并使用 GroupDocs.Redaction 安全地删除机密数据。完成后，您将了解如何设置库、创建自定义文本分段器、执行高性能搜索以及安全地应用编辑。

## 快速答案
- **“search and redact” 是什么意思？** 它指在文档中查找文本并永久遮蔽它。  
- **需要哪些库？** GroupDocs.Search 和 GroupDocs.Redaction for .NET。  
- **我可以处理多语言内容吗？** 是的——使用自定义文本分段器来正确拆分单词。  
- **如何提升搜索速度？** 只需一次索引，重复使用该索引，并启用 `optimize search performance` 设置。  
- **如果索引失败怎么办？** 请遵循故障排除章节中的 “handle indexing errors” 指南。

## 什么是 “search and redact”？

Search and redact 是在文档集合中定位特定术语，然后永久遮蔽或删除这些术语以保护隐私或满足监管合规要求的过程。它将全文搜索用于发现敏感信息，并使用编辑工具在保持文档原始布局的同时替换内容。

## 为什么要将 GroupDocs.Search 与 GroupDocs.Redaction 结合使用？

GroupDocs.Search 支持 **50+ 文件格式**，并且能够在典型服务器硬件上在一分钟内索引 **100,000+ 文档**，而 GroupDocs.Redaction 能在 **PDF、DOCX、PPTX 等** 格式上进行编辑而不改变原始布局。将两者结合提供了一个 **优化搜索性能** 并且 **优雅处理索引错误** 的一体化解决方案。

## 前置条件

- Visual Studio 2022 或更高版本，支持 .NET 6+。  
- NuGet 包：**GroupDocs.Search** 和 **GroupDocs.Redaction**（最新稳定版本）。  
- 有效的 GroupDocs 许可证（试用或已购买）。  

### 必需的库
- **GroupDocs.Search** – 提供索引、查询和自定义分段功能。  
- **GroupDocs.Redaction** – 在支持的格式中提供文本、图像和元数据的编辑功能。  

### 环境设置要求
确保您的开发机器对存放索引的文件夹具有写入权限。

### 知识前提
- 熟悉 C# 和 .NET 项目结构。  
- 对文档处理概念有基本了解（可选，但有帮助）。

## 如何为 .NET 安装 GroupDocs.Redaction？

您可以使用 .NET CLI 或 NuGet 包管理器将 Redaction 包添加到项目中。该命令会下载最新的稳定版本并将其注册到项目文件中，使 API 可立即使用。  

```bash
dotnet add package GroupDocs.Redaction
```  

## 如何获取 GroupDocs 许可证？

GroupDocs 提供三种授权方式：用于评估的免费试用、用于扩展开发测试的临时许可证，以及用于生产环境的完整商业许可证。试用版功能受限，临时密钥可延长评估期，购买的许可证则解锁全部功能并提供优先支持。

## 如何在我的应用程序中初始化 GroupDocs.Redaction？

`Redaction` 类是对支持的文档执行编辑的主要入口。它加载文件、准备编辑对象并执行编辑过程，返回一个在保持原始布局的同时已修改的文档。您还可以配置颜色、覆盖层和元数据移除等编辑选项，以满足特定合规要求。  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## 如何使用 GroupDocs.Search 设置索引？

`Index` 类表示存储在磁盘上的可搜索仓库。它管理索引的创建、更新和查询，允许您添加文档、重建索引并在大型集合中执行快速搜索。索引文件夹可以位于本地或网络存储，并且您可以配置压缩和加密设置以保护索引数据。  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## 什么是自定义文本分段器，为什么要使用它？

自定义文本分段器决定原始文本如何被拆分为可搜索的标记。通过为特定语言或领域定制分段规则，可提升标记化准确性，从而在搜索结果中获得更高的召回率和相关性。这对日语、阿拉伯语等词界复杂的语言尤为重要，因为默认分词器可能会错误拆分单词。  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## 如何使用自定义分段器执行全文搜索？

`SearchQuery` 对象封装用户的查询，并与自定义分段器协作定位匹配项。它支持模糊匹配、短语查询和加权，返回包含文档 ID、命中位置和相关性分数的结果集。您还可以应用文件类型或日期范围等过滤器，以实现更精确的定位。  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## 在找到敏感文本后如何应用编辑？

`Redaction` API 允许您在支持的文档中替换或移除文本、图像和元数据。识别出敏感术语后，创建编辑对象并应用，然后保存编辑后的文件，确保机密信息被永久隐藏。编辑选项包括覆盖黑框、使用自定义颜色或在保留文档结构的同时删除整个对象。  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## 常见问题及索引错误处理方法

- **Index Not Found:** 验证索引路径是否存在且应用程序具有读/写权限。  
- **Search Returns No Results:** 重新运行索引过程，并确保自定义分段器已正确注册。  
- **Redaction Fails on Certain Formats:** 确认文件类型受支持；对于 PDF，请使用最新的 Redaction 版本以处理 PDF 2.0 功能。

## 实际应用

1. **Legal Document Management:** 在合同中搜索 “non‑disclosure”，并在对外共享前自动编辑相关条款。  
2. **Academic Research:** 在手稿中定位未发表的数据，并在同行评审过程中隐藏它。  
3. **Business Contracts:** 批量处理数千份协议，编辑个人标识信息，同时保留法律语言。

## 如何针对大型文档集优化搜索性能？

为最大化性能，请一次性索引文档并在后续查询中重复使用同一索引。启用并行处理、配置缓存，并调优索引设置以降低延迟、提升多核服务器上的吞吐量。此外，设置 `EnableMemoryMapping` 标志以允许索引进行内存映射，从而加速大数据集的读取操作。

## 在处理大文件时如何管理 .NET 内存？

有效的内存管理对处理大型文档至关重要。将 `Index` 和 `Redaction` 对象放在 `using` 语句块中以确保确定性释放，并将文件作为流处理而不是一次性加载整个文档。监控性能计数器有助于提前发现内存峰值，从而调整批处理大小或进行垃圾回收调优。

## 常见问题

**Q: 我可以在 GroupDocs.Search 中使用非文本元数据吗？**  
A: 是的——元数据字段可以与文档内容一起被索引，从而实现类似 “author:JohnDoe” 的搜索。

**Q: GroupDocs.Redaction 支持在 Web API 中进行实时编辑吗？**  
A: 支持；您可以对小文件同步调用 Redaction API，或将较大的任务排队进行异步处理。

**Q: 如果索引损坏该怎么办？**  
A: 删除损坏的索引文件夹并使用相同的索引流程重新构建；库会记录详细的错误信息，帮助您定位原因。

**Q: 是否可以在保存前预览已编辑的文档？**  
A: 当然可以——调用 `redaction.Apply()` 并传入 `preview` 标志即可生成临时预览版本供审查。

**Q: 官方支持哪些 .NET 版本？**  
A: GroupDocs.Search 和 GroupDocs.Redaction 支持 .NET 6、.NET 5、.NET Core 3.1 和 .NET Framework 4.6.2+。

## 资源

- **文档:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API 参考:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **下载:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)
- **免费支持:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **临时许可证:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-06-12  
**已测试版本：** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## 相关教程

- [精通 GroupDocs Search 与 Redaction 在 .NET 中的高级文档管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [在 .NET 中实现 GroupDocs.Search 与 Redaction：更新和管理文档索引](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [使用 GroupDocs.Redaction 在 .NET 中优化文档索引：取消、异步和线程](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)