---
date: '2026-07-26'
description: 了解如何在 .NET 中使用 GroupDocs.Search 创建索引，并集成 redaction 与 GroupDocs.Redaction，实现快速
  document search 和 data handling。
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: 了解如何在 .NET 中使用 GroupDocs.Search 创建索引，并集成 redaction 与 GroupDocs.Redaction，实现快速
  document search 和 data handling。
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: 如何在 .NET 中使用 GroupDocs Search API 创建索引
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: 如何在 .NET 中使用 GroupDocs Search API 创建索引
type: docs
url: /zh/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# 如何在 .NET 中使用 GroupDocs Search API 创建索引

在本教程中，您将发现 **how to create index** 用于您的 .NET 应用程序，使用 GroupDocs.Search 并随后使用 GroupDocs.Redaction 保护敏感内容。通过本指南，您将能够构建、更新和修剪可搜索的索引，并且您将理解为何将搜索和脱敏结合是安全文档管理的最佳实践。

## 快速答案
- **What does “how to create index” mean?** 它指的是构建一个可搜索的数据结构，将文档内容映射到快速查找键。  
- **Which libraries are required?** 需要 .NET 的 GroupDocs.Search 和 GroupDocs.Redaction（NuGet 包）。  
- **Can I index PDFs, Word, and images?** 是的——开箱即支持超过 150 种格式。  
- **How do I delete a document from the index?** 调用 `Delete` 方法并传入文档的路径或 ID。  
- **Is redaction performed before or after indexing?** 脱敏应在索引之前进行，以确保受保护的数据永不进入索引。

## 什么是 “how to create index”？
短语 **how to create index** 指的是生成可搜索的数据结构的过程，该结构存储术语到文档的映射，以实现快速检索。在 GroupDocs 中，此结构保存在磁盘上，并且可以增量更新，无需重新构建整个集合。

## 为什么要将 GroupDocs.Search 与 GroupDocs.Redaction 一起使用？
GroupDocs.Search 支持对 **150+ 文件格式** 进行索引，并且能够处理超过 **10 GB** 的索引，同时将内存使用保持在 200 MB 以下，因为它采用流式读取文件而不是一次性加载。加入 GroupDocs.Redaction 可确保在内容进入索引之前移除任何机密文本、图像或元数据，从而保证符合 GDPR、HIPAA 等法规的要求。

## 前置条件

- **Libraries & Versions** – 安装兼容 .NET 6 或更高版本的最新 **GroupDocs.Search** 和 **GroupDocs.Redaction** NuGet 包。  
- **IDE** – Visual Studio 2022（或任何支持 .NET 6 的 IDE）。  
- **Knowledge** – 基本的 C# 技能、文件 I/O 的熟悉程度以及对索引概念的理解。

## 为 .NET 设置 GroupDocs.Redaction

### 安装

**Using .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Using Package Manager Console in Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

您也可以在 NuGet 包管理器 UI 中找到 “GroupDocs.Redaction”，并安装最新的稳定版本。

### 许可证获取

您可以获取免费试用或请求临时许可证，以无限制地探索所有功能。访问 [GroupDocs' Purchase Page](https://purchase.groupdocs.com/temporary-license/) 了解获取许可证的更多详情。

### 基本初始化

Redactor 是执行文档脱敏操作的主要类。  
以下代码片段展示了开始使用 GroupDocs.Redaction 所需的最小代码：  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

## 实施指南

### 如何创建索引？

`Index` 表示保存术语字典和文档元数据的可搜索容器。  
加载或创建一个 `Index` 对象，指向存放索引文件的文件夹，然后调用 `Create`。该操作会写入必要的元数据文件并为文档导入做好准备。  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### 步骤 1：创建索引
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### 如何向索引添加文档？

`Add` 将单个文档插入索引，而 `AddFolder` 处理目录中的所有文件。  
您可以通过调用 `Add` 或 `AddFolder` 添加文件。引擎会读取每个受支持的文件，提取文本并更新术语字典。  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### 步骤 2：添加文档文件夹
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### 如何检索已索引的路径？

`GetIndexedPaths` 返回索引中存储的所有文档路径的集合。  
检索已索引文件路径的列表可让您验证当前哪些文档是可搜索的。  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### 步骤 3：显示已索引的路径
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### 如何从索引中删除文档？

`Delete` 通过路径或标识符从索引中移除文档。  
当文件被删除或变得过时时，您应删除其条目以保持搜索结果的准确性。  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### 步骤 4：删除特定路径
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### 如何在删除后验证剩余的已索引路径？

删除后，您可以重新运行检索方法，以确保索引反映当前状态。  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### 步骤 5：验证剩余路径
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## 实际应用

1. **Document Management Systems** – 快速定位数百万文件中的合同、发票或手册。  
2. **Legal Document Review** – 在索引之前脱敏特权信息，以避免意外泄露。  
3. **Archival Solutions** – 为历史记录保留可搜索的元数据，而无需将整个档案加载到内存中。  
4. **Content Management Platforms** – 为博客、知识库和多媒体库提供全站搜索功能。  
5. **Data Compliance Audits** – 确保仅搜索已清理的内容，以满足监管要求。

## 性能考虑因素

- **Optimize Indexing** – 安排每晚进行增量索引；使用批量大小为 100 文件的 `AddFolder` 以降低 I/O 峰值。  
- **Resource Management** – 监控 CPU 和内存；GroupDocs.Search 以流式方式处理文件，即使是 10 GB 的索引，峰值内存也保持在 200 MB 以下。  
- **Best Practices** – 将索引存储在 SSD 上以实现亚秒级查询响应，并启用压缩 (`index.Compression = true`) 将磁盘使用量减半。

## 常见问题

**Q: 我可以使用 GroupDocs 索引非文本文件吗？**  
A: 可以，GroupDocs.Search 能够索引超过 150 种格式——包括 PDF、DOCX、PPTX、XLSX 以及图像类型——必要时通过 OCR 提取嵌入的文本。

**Q: 我该如何处理大量文档？**  
A: 使用可配置批量大小的 `AddFolder`，在后台服务中运行索引，并定期调用 `Optimize()` 合并小的索引段。

**Q: 将脱敏与索引结合使用有什么好处？**  
A: 脱敏在数据进入索引之前移除个人身份信息，确保搜索结果永不暴露受保护的数据。

**Q: 可以自定义搜索算法吗？**  
A: GroupDocs.Search 提供同义词词典、自定义分词器和正则表达式过滤器，允许您微调相关性评分。

**Q: 我该如何排查常见的索引问题？**  
A: 验证文件夹权限，确保 .NET 运行时与库的目标匹配，并检查索引文件夹中生成的日志文件以获取详细错误信息。

## 资源

- **Documentation**: [GroupDocs Redaction .NET Docs](https://docs.groupdocs.com/search/net/)  
- **API Reference**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **Download**: [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

浏览这些资源以加深理解并提升在 .NET 中实现 GroupDocs.Search 与 Redaction 的能力。祝编码愉快！

---

**最后更新：** 2026-07-26  
**测试环境：** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**作者：** GroupDocs

## 相关教程

- [掌握索引创建与合并，使用 GroupDocs.Redaction .NET 实现高效文档管理](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)  
- [精通 GroupDocs.Redaction .NET：高效索引创建与别名管理，实现高级文档搜索](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)  
- [精通 GroupDocs Search 与 Redaction 在 .NET 中的使用：文档管理综合指南](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)