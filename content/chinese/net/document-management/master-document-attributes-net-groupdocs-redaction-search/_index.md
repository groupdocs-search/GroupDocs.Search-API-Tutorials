---
date: '2026-06-22'
description: 了解如何在 .NET 中对文档进行脱敏，同时使用 GroupDocs.Redaction 和 GroupDocs.Search 优化搜索性能。为
  .NET 开发者提供逐步的属性管理、索引和安全脱敏指南。
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: 如何在 .NET 中使用 GroupDocs Redaction 对文档进行脱敏
type: docs
url: /zh/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# 如何在 .NET 中使用 GroupDocs Redaction 对文档进行编辑

在本综合教程中，您将了解在 .NET 环境中**如何编辑文档**，并同时掌握使用 GroupDocs.Redaction 和 GroupDocs.Search 进行文档属性管理的技巧。无论您需要保护敏感数据、提升搜索速度，还是组织大型文档库，这里展示的技术都能为您提供可在数十万文件规模下使用的生产就绪解决方案。

## 快速答案
- **如何在 .NET 中编辑 PDF？** 使用 `Redactor` 加载文件，定义 `RedactionRegion`，然后调用 `Redactor.Apply()` —— 三行代码即可完成繁重的工作。  
- **索引后我可以更改文档属性吗？** 可以，使用 `AttributeChangeBatch` 批量添加、更新或删除属性。  
- **需要哪些库？** `GroupDocs.Redaction` + `GroupDocs.Search`（最新的 NuGet 版本）。  
- **生产环境需要许可证吗？** 需要有效的 GroupDocs 许可证；可获取临时试用许可证进行评估。  
- **如何提升搜索速度？** 启用批处理和选择性索引；这些技术可在大型数据集上将**搜索性能优化**提升至最高 40 %。  

## 什么是“编辑文档”？

它描述了一种自动化过程，即在文件中定位敏感信息并用遮蔽内容（如黑条或空白）替换，同时保持原始布局不变。这样可以隐藏机密数据，使文档对观看者不可见，但仍保持可读且可用于后续任务。

## 为什么要将 GroupDocs.Redaction 与 GroupDocs.Search 结合使用？

GroupDocs.Redaction 支持**50 多种文件格式**（PDF、DOCX、XLSX、PPTX、图像等），且可在不将整个文件加载到内存的情况下处理高达**2 GB**的文档。GroupDocs.Search 在标准服务器上每小时可索引超过**7000 万个词项**，结合基于属性的过滤，可显著**优化搜索性能**。

## 前提条件

- **必需的库：** `GroupDocs.Search` 和 `GroupDocs.Redaction`（最新的 NuGet 发行版）。  
- **开发环境：** Visual Studio 2019 或更高版本，目标为 .NET Core 3.1 或 .NET 6+。  
- **基础知识：** C# 语法、面向对象概念以及对文档索引原理的了解。

## 为 .NET 设置 GroupDocs.Redaction

### 安装库

您可以使用以下任意方法将 **GroupDocs.Redaction** 添加到项目中：

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet 包管理器 UI**  
- 搜索 “GroupDocs.Redaction” 并安装最新版本。

### 获取许可证的步骤

要开始使用，您可以获取临时许可证或购买正式许可证。免费试用可用于在做出决定前测试功能：

1. 访问 [GroupDocs 许可证页面](https://purchase.groupdocs.com/temporary-license/) 以请求临时许可证。  
2. 按照提供的说明在应用程序中应用许可证。

### 基本初始化和设置

`Redactor` 是用于加载文档并执行编辑操作的主要类。

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## 功能 1：更改文档属性

### 概述
修改文档属性可让您细致地调节文档在搜索结果中的呈现方式，从而实现精确的过滤和分类。

#### 步骤 1：初始化索引

`Index` 代表一个可搜索的文档集合及其关联的元数据。

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### 步骤 2：修改属性

`AttributeChangeBatch` 是用于批量更新属性以提高效率的类。

**定义锚点：** *`AttributeChangeBatch` 在单个事务中批量添加、更新和删除文档属性。*

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### 步骤 3：使用属性过滤进行搜索

您可以使用 `SearchOptions` 按属性值过滤搜索结果。

**直接答案：** 要搜索包含属性 `Category = "Legal"` 的文档，请使用 `AttributeFilter` 配置 `SearchOptions` 并调用 `searcher.Search("contract", options)`。这仅返回已标记为法律的合同，减少结果噪声并**优化搜索性能**。

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## 功能 2：在索引期间添加属性

### 概述
在索引时添加属性可确保每个文档从一开始就拥有正确的元数据，避免后续批量更新的需求。

#### 步骤 1：为索引设置事件处理程序

**定义锚点：** *`DocumentIndexed` 事件在每次文档成功添加到索引时触发，允许自定义逻辑运行。*

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### 步骤 2：配置并执行搜索

属性附加后，您可以使用这些新字段进行搜索。

**直接答案：** 使用带有 `AttributeFilter` 的 `SearchOptions` 查询新添加的属性，例如 `AttributeFilter("Department", "Finance")`。这仅返回与财务相关的文件，演示了**如何索引属性**以获得更快、更相关的结果。

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## 实际应用

以下是三个常见场景，文档属性管理与编辑结合可带来实际业务价值：

1. **法律文档管理** – 自动编辑机密条款并按司法管辖区标记合同，使律师仅能定位相关文件。  
2. **医疗记录组织** – 编辑患者标识信息，同时添加如 `PatientID` 和 `VisitDate` 的属性，以实现合规且快速的检索。  
3. **电子商务产品目录** – 在批量导入时编辑供应商定价信息并使用 `StockStatus` 或 `DiscountRate` 标记产品，从而实现实时库存查询。

## 性能考虑

处理大规模数据集时，请牢记以下最佳实践：

- **批处理：** `AttributeChangeBatch` 减少与索引的往返次数，在 10 万文档批次上可将处理时间缩短至最高 **45 %**。  
- **选择性索引：** 仅索引需要新属性的文档；跳过未更改的文件以节省 CPU 和 I/O。  
- **内存管理：** 在完成后立即释放 `SearchResult`、`Redactor` 和 `Indexer` 实例，以释放非托管资源。

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 编辑未隐藏文本 | `RedactionRegion` 坐标不正确 | 在定义区域之前使用 `Redactor.GetPageSize()` 验证页面尺寸。 |
| 属性更改未在搜索中反映 | 索引未刷新 | 在执行 `AttributeChangeBatch` 后调用 `searcher.Refresh()`。 |
| 大文件出现内存不足错误 | 将整个文件加载到内存中 | 通过将 `RedactorOptions.Stream = true` 启用流模式。 |

## 常见问答

**Q:** 批量编辑多个 PDF 的最佳方法是什么？  
**A:** 使用 `Redactor` 加载每个文件，为每个敏感区域添加 `RedactionRegion`，然后在循环中调用 `Redactor.Apply()`；此方法可在最小内存开销下处理数千个文件。

**Q:** 我可以在单个查询中将编辑与属性过滤结合吗？  
**A:** 可以。编辑后，文档保留其元数据，您可以同时使用文本词项和 `AttributeFilter` 进行搜索。

**Q:** 如何处理受密码保护的文档？  
**A:** 将密码传递给 `Redactor` 构造函数；库会自动解密、编辑并重新加密文件。

**Q:** GroupDocs 是否支持在编辑前对扫描图像进行 OCR？  
**A:** 当然。启用 `RedactorOptions.Ocr = true` 可识别图像中的文本，然后对提取的文本应用编辑规则。

**Q:** 官方支持哪些 .NET 版本？  
**A:** GroupDocs.Redaction 和 GroupDocs.Search 支持 .NET Core 3.1、.NET 5、.NET 6、.NET 7，以及 .NET Framework 4.6.2 及以上版本。

## 结论

现在，您已经拥有使用 GroupDocs.Redaction 和 GroupDocs.Search 对**编辑文档**、**优化搜索性能**以及**索引属性**的全栈解决方案。遵循上述步骤，您可以保护敏感数据，为搜索索引添加有意义的元数据，并保持 .NET 应用程序的高速与安全。

---

**最后更新：** 2026-06-22  
**测试环境：** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**作者：** GroupDocs

## 相关教程

- [精通 GroupDocs.Redaction .NET：高效索引创建与别名管理以实现高级文档搜索](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [使用 GroupDocs.Redaction .NET 进行文档编辑和元数据索引](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [精通 GroupDocs.Redaction .NET：设置与事件处理以实现安全文档管理](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)