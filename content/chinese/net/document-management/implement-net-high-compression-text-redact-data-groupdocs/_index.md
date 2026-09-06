---
date: '2026-06-07'
description: 了解如何在 .NET 应用程序中使用 GroupDocs.Search 和 GroupDocs.Redaction 实现高压缩文本存储并对机密数据进行编辑。
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
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
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 使用 GroupDocs 实现高压缩 .NET：文本与 Redaction 指南
type: docs
url: /zh/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# 实现高压缩 .NET 与 GroupDocs：文本与编辑指南

在现代 .NET 解决方案中，**实现高压缩 .net** 在需要存储海量文本集合而不占用过多磁盘空间时至关重要。同时，保护敏感信息——如个人标识符或财务数字——需要可靠的编辑。本教程将一步步展示如何使用 **GroupDocs.Search** 配置高压缩文本存储，以及如何使用 **GroupDocs.Redaction** 安全地编辑机密数据。完成后，您将能够将索引文本压缩高达 90 %，并从 PDF、Word 文件以及许多其他格式中删除私人内容。

## 快速答案
- **提供高压缩索引的库是什么？** GroupDocs.Search for .NET。  
- **哪个工具用于编辑敏感数据？** GroupDocs.Redaction for .NET。  
- **我可以自动将文档添加到索引吗？** 是——在文件夹扫描循环中使用 `AddDocument` API。  
- **压缩对搜索是无损的吗？** 是的，压缩后文本仍然可以完全搜索。  
- **生产环境需要许可证吗？** 商业使用需要永久的 GroupDocs 许可证。

## 什么是“实现高压缩 .NET”？
实现高压缩 .net 意味着配置 GroupDocs.Search 索引引擎，以压缩形式存储提取的文本内容。这显著降低磁盘上的索引大小，同时保持文本完全可搜索。压缩是无损的，查询相关性和摘要提取的效果与未压缩索引完全相同。

## 为什么使用 GroupDocs 进行压缩和编辑？
GroupDocs.Search 支持超过五十种输入格式，并可将索引文本压缩高达百分之九十，使大型文档集合仅占原始大小的一小部分。GroupDocs.Redaction 则通过永久擦除或遮蔽超过三十种文件类型中的敏感信息，帮助您在无需额外工具的情况下满足 GDPR、HIPAA 等严格合规要求。

## 前提条件
- **开发环境：** Visual Studio 2022 或更高版本，.NET 6+（或 .NET Framework 4.7.2）。  
- **库：** `GroupDocs.Search` 和 `GroupDocs.Redaction` NuGet 包。  
- **权限：** 对包含源文档的文件夹和索引输出位置具有读/写访问权限。  
- **基础知识：** C# 语法、文件 I/O，以及熟悉 .NET 项目结构。

## 如何使用 GroupDocs 实现高压缩 .NET？
要使用 GroupDocs 实现高压缩 .NET，首先创建 `TextStorageSettings` 实例并将其 `CompressionLevel` 设置为 `High`。然后实例化 `Index` 对象，传入设置和存放索引的文件夹。索引准备好后，使用 `AddDocument` 添加文档，最后使用 `Search` 方法执行搜索，整个过程引擎会透明地处理压缩与解压。

### 步骤 1：安装所需的 NuGet 包
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**包管理器**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet 包管理器 UI**  
- 搜索 “GroupDocs.Search” 并点击 **Install**。  

### 步骤 2：安装 GroupDocs.Redaction（用于数据编辑）
- 打开 **NuGet 包管理器**。  
- 搜索 **GroupDocs.Redaction** 并安装最新的稳定版本。  

### 步骤 3：获取并应用许可证
- **免费试用：** 在 GroupDocs 门户注册获取 30 天试用密钥。  
- **临时许可证：** 为开发环境请求临时密钥。  
- **永久许可证：** 购买生产许可证以去除评估限制。  

### 步骤 4：两库的基本初始化
`Search` 和 `Redaction` 引擎共享相同的授权模型。请在应用启动时初始化它们：

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

## 功能 1：高压缩文本存储设置

### 设置索引配置
`TextStorageSettings` 是告诉 GroupDocs.Search 如何保存提取文本的类。启用高压缩可在不影响搜索速度的情况下将索引大小降低至 **10 倍**。

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

**说明：**  
- `CompressionLevel.High` 启用基于 ZSTD 的算法，高效压缩文本块。  
- `UseMemoryCache = false` 强制引擎从磁盘流式读取数据，适用于大规模部署。

### 创建和管理索引
`Index` 对象代表磁盘上的可搜索仓库。您需要指定索引文件的存放文件夹，并传入上述压缩设置。

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**说明：**  
- `indexFolder` 决定压缩索引文件的存放位置。  
- `settings` 注入高压缩配置，确保每个添加的文档都受益。

## 功能 2：向索引添加文档

### 向索引添加文档
`AddDocument` 将单个文件添加到索引，提取其文本、根据配置压缩并存储。GroupDocs.Search 能够从目录树中摄取文件。以下循环遍历 `documentsFolder`，为每个文件调用 `AddDocument` 并记录进度。

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

**说明：**  
- `AddDocument` 解析文件，提取可搜索文本，根据 `TextStorageSettings` 压缩并存入索引。  
- 此方法适用于 **PDF、DOCX、TXT、HTML**，以及超过 **30** 种其他格式。

## 功能 3：执行搜索查询

### 执行搜索
`Search` 对压缩索引运行查询，并返回包含相关度分数和高亮摘要的 `DocumentResult` 集合。索引填充后，您即可运行快速查询。`Search` 方法返回的 `DocumentResult` 包含文件路径和高亮片段。

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

**说明：**  
- 搜索引擎直接扫描压缩文本，即使索引包含 **数百万页**，查询延迟仍保持低水平。  
- `Score` 表示相关性；数值越高匹配度越好。

## 如何使用 GroupDocs.Redaction 对机密数据进行编辑？
使用 GroupDocs.Redaction 编辑机密数据的第一步是为目标文件创建 `Redactor` 实例。定义一个或多个描述待删除文本的 `SearchPattern`（例如用于社会安全号码的正则表达式）。使用 `Redact` 应用每个模式，指定 `RedactionType`（如 `BlackOut`），并将结果保存为新文档，确保原始文件保持不变。

`Redactor` 是 GroupDocs.Redaction 中用于加载文档并执行编辑操作的主要类。  
`SearchPattern` 定义用于识别待编辑文本的正则表达式。

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

**说明：**  
- `SearchPattern` 使用正则表达式定位社会安全号码。  
- `RedactionType.BlackOut` 用实心黑色矩形替换匹配的文本，确保数据无法恢复。

## 实际应用
1. **法律文档管理：** 自动压缩海量案件文件并在归档前编辑客户标识。  
2. **医疗记录：** 将多年患者笔记存入压缩索引，并在与研究合作方共享前删除 PHI（受保护的健康信息）。  
3. **财务报告：** 通过编辑账号来保护季度报告，同时保留可搜索文本以供审计查询。

## 性能考虑因素
- **压缩影响：** 高压缩可将索引大小降低至 **90 %**，降低 SSD 磨损并加快备份。  
- **内存使用：** 对于超大索引禁用内存缓存，以将进程占用保持在 **500 MB** 以下。  
- **I/O 优化：** 将文档批量添加为每组 100 条，以减少磁盘抖动。  
- **异步处理：** 将 `AddDocument` 调用包装在 `Task.Run` 中，以保持桌面应用的 UI 线程响应。

## 常见陷阱与故障排除
- **文件路径错误：** 确认 `documentsFolder` 和 `indexFolder` 为绝对路径且应用具有读写权限。  
- **许可证错误：** 确保 `.lic` 文件与可执行文件一起部署或嵌入为资源。  
- **搜索无结果：** 检查 `TextStorageSettings` 的压缩级别是否与索引时使用的相匹配；不匹配会导致反序列化失败。  

## 常见问答

**问：我可以在初始构建后向索引添加文档吗？**  
**答：** 可以——只需对新文件调用 `index.AddDocument`，引擎会增量更新压缩索引。

**问：编辑会改变原始文件吗？**  
**答：** 不会——原始文件保持不变，编辑后的版本另存为新文件，保留文档完整性。

**问：GroupDocs.Redaction 支持哪些格式？**  
**答：** 超过 **30** 种格式，包括 PDF、DOCX、PPTX、XLSX、图像（PNG、JPEG）和纯文本。

**问：高压缩会影响搜索相关性吗？**  
**答：** 不会。文本压缩是无损的，相关性分数与未压缩索引相同。

**问：我能索引的文档大小有上限吗？**  
**答：** GroupDocs.Search 可通过流式处理支持多 GB 文件；但需确保压缩索引有足够磁盘空间（约为原始大小的 10 %）。

## 资源
- [Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction for .NET](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/)

**最后更新：** 2026-06-07  
**测试环境：** GroupDocs.Search 23.12 和 GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs

## 相关教程

- [在 .NET 中实现 GroupDocs.Search 与 Redaction 用于文档管理](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [如何优化 GroupDocs.Redaction for .NET：高效索引与拼写管理指南](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [精通 GroupDocs Redaction 与 Search in .NET：高效文档管理与安全搜索](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)