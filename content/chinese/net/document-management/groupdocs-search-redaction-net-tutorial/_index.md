---
date: '2026-06-12'
description: 了解如何使用 GroupDocs.Search 和 GroupDocs.Redaction 创建 search index .NET 并对
  PDF 进行 redaction。解释 Setup、deployment、indexing 和 advanced search。
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: 使用 GroupDocs Search 和 Redaction 创建 Search Index .NET – 综合指南
type: docs
url: /zh/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# 使用 GroupDocs Search 和 Redaction 创建搜索索引 .NET – 综合指南

在当今的数字环境中，**创建搜索索引 .NET** 解决方案能够快速定位信息并保护敏感数据，是任何组织的首要任务。本教程将指导您配置可扩展的 GroupDocs.Search 网络、部署节点、索引文档，并使用 GroupDocs.Redaction **对 PDF 进行脱敏**——全部在 .NET 环境中完成。

## 快速答案
- **创建搜索索引 .NET 的第一步是什么？** 定义基础路径和端口，然后部署网络节点。  
- **如何使用 GroupDocs 对 PDF 进行脱敏？** 初始化 `Redactor` 实例，加载 PDF，并使用所需的模式调用 `Redact`。  
- **我可以在多台机器上运行搜索网络吗？** 可以——在不同服务器上部署节点，让主节点协调索引和查询。  
- **生产环境是否需要许可证？** 生产环境需要有效的 GroupDocs 许可证；可使用临时试用许可证进行评估。  
- **支持哪些 .NET 版本？** 完全支持 .NET Framework 4.7.2+、.NET Core 3.1+ 以及 .NET 5/6/7。

## 什么是 “create search index .net”？
*Creating a search index .NET* 指使用 .NET 库构建可搜索的文档元数据和内容仓库，该库会提取文本、对词项进行分词，并将其存储在优化的索引结构中。这使得在分布式节点之间能够即时响应查询，支持多种文件格式，并在企业应用中实现可扩展的高性能文档检索。

## 为什么要将 GroupDocs Search 与 Redaction 结合使用？
GroupDocs.Search 支持 **50 多种文件格式**——包括 DOCX、PDF、PPTX 和 HTML，并且能够在不将整个文件加载到内存的情况下索引数百页的文档。结合 GroupDocs.Redaction，它可以在每页不足 200 ms 的时间内 **对 PDF 进行脱敏**，为您提供安全且高性能的文档管理流水线。

## 前提条件

### 必需的库和依赖项
要按照本教程操作，请安装以下包：
- **GroupDocs.Search**（适用于 .NET）
- **GroupDocs.Redaction**（适用于 .NET）

您可以使用以下任意方法安装所需库：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜索 “GroupDocs.Search” 和 “GroupDocs.Redaction”，并安装最新版本。

### 环境设置要求
- .NET Framework 4.7.2 或更高（或 .NET Core 3.1+）  
- Visual Studio IDE（Community、Professional 或 Enterprise）

### 知识前提
- 基础 C# 编程  
- 面向对象概念  
- 熟悉网络配置和文档管理系统

## 为 .NET 设置 GroupDocs.Redaction

### 安装信息
要在应用程序中集成脱敏功能，请首先添加 GroupDocs.Redaction 库：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜索 “GroupDocs.Redaction” 并安装。

### 获取许可证
要开始使用免费试用或临时许可证，请按以下步骤操作：
- 访问 [GroupDocs 网站](https://purchase.groupdocs.com/temporary-license/) 申请临时许可证。  
- 如需购买选项，请前往其 [定价页面](https://groupdocs.com/pricing)。

获取许可证文件后，在应用程序设置中应用它：

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### 基本初始化
要初始化 GroupDocs.Redaction 以进行基本操作，请使用以下代码片段：

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## 实现指南

### 配置设置

#### 概述
此功能使用基础路径和端口号配置搜索网络，构成文档管理系统的基础。

#### 定义锚点
`SearchNetworkDeployment` 是在网络中协调搜索节点部署的类。

#### 步骤 1：定义基础路径和端口  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### 步骤 2：配置网络
使用 `Configure` 方法，以指定的路径和端口设置搜索网络：

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### 网络节点部署

#### 概述
在已配置的搜索网络中部署节点，以实现分布式文档搜索。

#### 定义锚点
`SearchNetworkNode` 表示与主节点通信的单个可搜索节点。

#### 步骤 1：初始化部署  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### 主节点事件订阅

#### 概述
在主节点上订阅事件，以有效监控和管理网络操作。

#### 定义锚点
`SearchNetworkNodeEvents` 提供索引、查询执行和错误处理的回调。

#### 步骤 1：识别主节点
选择第一个节点作为主节点：

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### 步骤 2：订阅事件
订阅事件使用：

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### 索引文档

#### 概述
对文档进行索引以实现高效的搜索操作。此步骤对于确保网络能够快速检索所需数据至关重要。

#### 定义锚点
`SearchIndex` 是存储每个已索引文件的可搜索标记和元数据的核心对象。

#### 步骤 1：添加目录到索引  
```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### 搜索功能 – 基本用法

#### 概述
在网络中的节点上执行基本搜索操作。

#### 直接答案
在主节点上调用 `SearchNetwork.Query("your term")` 可即时检索匹配的文档。该方法返回包含文件路径和相关性分数的 `SearchResult` 对象集合。  
`SearchNetwork.Query` 是在整个网络上执行搜索查询并返回匹配结果的方法。

#### 步骤 1：定义搜索参数  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### 高级搜索功能

#### 概述
使用可自定义参数的高级搜索技术，以获得更精确的结果。

#### 直接答案
实现一个方法，构建 `SearchOptions` 对象，设置 `UseFuzzySearch`、`Highlight` 和 `PageSize` 属性，然后将其传递给 `SearchNetwork.QueryAdvanced`。这将产生带分页、突出显示且启用模糊匹配的结果。  
`SearchNetwork.QueryAdvanced` 是一个使用模糊匹配和分页等高级选项运行查询的方法。

#### 步骤 1：实现高级搜索方法  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### 对 PDF 文件进行脱敏

#### 概述
在 PDF 内容存储或共享之前，通过脱敏来保护敏感信息。

#### 直接答案
创建 `Redactor` 实例，加载目标 PDF，定义 `RedactionPattern`（例如 SSN 正则），调用 `redactor.Apply(pattern)`，最后保存脱敏后的文档。此过程确保个人数据被永久删除。

#### 定义锚点
`Redactor` 是 GroupDocs.Redaction 中处理文档并应用脱敏规则的主要类。

#### 示例工作流（无新代码块）  
1. 使用您的许可证初始化 `Redactor`。  
2. 使用 `redactor.Load("sample.pdf")` 加载 PDF。  
3. `RedactionPattern` 表示指定要脱敏的文本或模式的规则。定义如 `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")` 的模式。  
4. 执行 `redactor.Apply(pattern)`。  
5. 使用 `redactor.Save("sample_redacted.pdf")` 保存输出。

### 实际应用

#### 实际使用案例
1. **法律文档管理** – 高效搜索合同并自动脱敏客户标识。  
2. **医疗记录** – 定位患者笔记，同时确保符合 HIPAA 的 PHI 脱敏。  
3. **企业合规** – 扫描内部沟通内容以查找禁止词汇，并在归档前进行脱敏。

## 结论 
本指南提供了一个完整的路径，帮助您 **创建搜索索引 .NET** 解决方案，实现可扩展、快速索引，并通过脱敏保护数据。通过配置节点、索引文档、利用高级搜索功能以及应用脱敏，开发者可以显著提升文档管理工作流，同时遵守严格的安全标准。

## 常见问题

**问：如何在 .NET 中使用 GroupDocs 设置分布式搜索网络？**  
答：定义基础路径和端口，然后调用 `SearchNetworkDeployment.Deploy()` 在多台机器上启动主节点和工作节点。

**问：我可以在 GroupDocs 中使用多个参数进行高级搜索吗？**  
答：可以——使用 `SearchOptions` 在单个查询中结合模糊匹配、通配符支持和结果高亮。

**问：是否可以在主节点上监控网络活动？**  
答：完全可以——订阅 `SearchNetworkNodeEvents`（如 `IndexingCompleted` 和 `QueryExecuted`）以获取实时洞察。

**问：如何使用 GroupDocs 对 PDF 文件进行脱敏？**  
答：初始化 `Redactor`，加载 PDF，定义 `RedactionPattern` 对象（正则或文字字符串），调用 `Apply`，并保存已清理的文档。

**问：在网络环境中提升搜索性能的最简方法是什么？**  
答：在查询前完整索引文档集，分布节点以利用并行处理，并调优 `SearchOptions` 以实现缓存和分页。

---

**最后更新:** 2026-06-12  
**测试环境:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**作者:** GroupDocs

## 相关教程

- [掌握 .NET 文档索引与 GroupDocs.Search：综合指南](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [掌握文档索引和高级搜索查询与 GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [精通 GroupDocs Search 与 Redaction 在 .NET 中：高级文档管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)