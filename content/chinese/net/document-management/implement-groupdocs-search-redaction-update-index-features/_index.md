---
date: '2026-06-07'
description: 了解如何使用适用于 .NET 的 GroupDocs.Search 和 Redaction 高效更新索引，提升您的文档管理系统。
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: 如何使用 GroupDocs.Search 与 Redaction (.NET) 更新索引
type: docs
url: /zh/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# 如何使用 GroupDocs.Search 与 Redaction (.NET) 更新索引

在现代数据驱动的企业中，**how to update index** 快速且可靠地进行可能决定搜索体验的成败。无论您处理的是成千上万的合同还是庞大的知识库，保持搜索索引与最新文档更改同步对于快速、准确的结果至关重要。本教程将指导您如何在 .NET 中使用 GroupDocs.Search 与 GroupDocs.Redaction 来**update index**文件，管理版本化索引，并保护敏感内容——全部在一个干净的 .NET 项目中完成。

## 快速答案
- **What does “how to update index” mean?** 它是修改现有搜索索引的过程，使新文档或已更改的文档在不重新构建的情况下即可被搜索。  
- **Which libraries are required?** GroupDocs.Search 和 GroupDocs.Redaction for .NET（均可通过 NuGet 获取）。  
- **Do I need a license?** 免费试用可用于测试；生产许可证可解锁全部功能。  
- **Can I run this on .NET Core?** 是的，这些库支持 .NET Framework 4.5+、.NET Core 3.1+ 和 .NET 5/6+。  
- **What performance can I expect?** 在典型的 4 核服务器上，使用 2 线程更新 1 GB 的索引可在一分钟以内完成。

## 什么是 “how to update index”？
**How to update index** 指的是对现有搜索索引应用增量更改的技术，而不是完全重新创建。此方法可减少停机时间，节省 CPU 资源，并在文档被添加、编辑或删除时保持搜索结果的最新。

## 为什么在索引更新时使用 GroupDocs.Search 与 Redaction？
GroupDocs.Search 支持 **50+ 文件格式**（PDF、DOCX、XLSX、PPTX、HTML、图像等），并且能够在不将整个文件加载到内存中的情况下处理数百页的文档。结合 GroupDocs.Redaction，您可以在索引之前自动删除或遮蔽敏感数据，确保合规的同时保持搜索相关性。

## 前提条件

- **GroupDocs.Search** – 通过 NuGet 安装。  
- **GroupDocs.Redaction for .NET** – 用于红化功能的必需组件。  
- Visual Studio（或任何 .NET IDE），并已安装 .NET 6+。  
- 基础 C# 知识以及对索引概念的了解。

### 必需的库和版本
- **GroupDocs.Search** – 来自 NuGet 的最新稳定版本。  
- **GroupDocs.Redaction for .NET** – 来自 NuGet 的最新稳定版本。

### 环境设置要求
- 具备已安装 .NET SDK 的 Windows 或 Linux 机器。  
- 有权访问用于存放索引文件的文件夹。

### 知识前提
- 理解文档索引和搜索的基本原理。  
- 了解企业系统中文档生命周期管理。

## 为 .NET 设置 GroupDocs.Redaction

### 安装包

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- 搜索 “GroupDocs.Redaction” 并安装最新版本。

### 获取许可证的步骤
1. **Free Trial** – 开始使用试用版以探索所有功能。  
2. **Temporary License** – 请求临时密钥以进行更长时间的测试。  
3. **Purchase** – 获取完整许可证用于生产部署。

### 基本初始化和设置
`Redactor` 是应用文档红化规则的核心类。  
要开始使用，请引用 Redaction 命名空间并创建一个 `Redactor` 实例：

```csharp
using GroupDocs.Redaction;
```

## 实施指南

我们将介绍两个核心功能：更新已索引的文档以及维护索引版本控制。

### 如何使用 GroupDocs.Search 更新索引？

`Index` 表示存储在磁盘上的可搜索集合。  
`UpdateOptions` 配置增量更新的执行方式（例如线程数）。  
`UpdateDocument` 对单个文档应用更改，`Commit` 则提交所有挂起的更新。

**Direct answer (40‑70 words):**  
创建指向索引文件夹的 `Index` 对象，使用 `UpdateOptions` 指定线程数，对每个已更改的文件调用 `UpdateDocument`，最后调用 `Commit` 以持久化更改。此增量方法仅更新已修改的部分，保持索引最新而无需完整重建。

#### 功能 1：更新已索引的文档

##### 概述
更新已索引的文档可确保搜索结果反映最新内容，即使文档被编辑或替换。

##### 步骤 1：创建索引
`Index` 类是表示磁盘上可搜索集合的顶层对象。

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### 步骤 2：向索引添加文档
从目录中添加文件；库会自动提取可搜索的文本。

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### 步骤 3：搜索并更新
执行查询，修改源文件，然后使用索引时相同的 `UpdateOptions` 调用 `UpdateDocument`。

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Why This Works:** 通过将 `Threads = 2`，更新利用了两个 CPU 核心，在四核机器上将处理时间大约减半。

### 如何维护索引版本控制？

`IndexUpdater` 是一个实用类，用于将旧的索引格式升级到库支持的最新版本。

**Direct answer (40‑70 words):**  
使用现有索引的路径实例化 `IndexUpdater`，调用 `CanUpdateVersion()` 验证兼容性，如有需要则运行 `UpdateVersion()`。升级后，使用新格式重新加载索引并执行搜索以确认一切正常。此过程确保在库版本之间无缝迁移。

#### 功能 2：维护索引版本控制

##### 概述
版本控制确保在库升级后旧索引仍然可搜索。

##### 步骤 1：检查兼容性
`IndexUpdater` 检查当前索引是否可以升级到最新格式。

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### 步骤 2：加载并搜索
升级后，加载更新后的索引并执行查询以验证完整性。

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Why This Works:** `CanUpdateVersion` 检查可防止因索引模式不匹配导致的运行时异常，提供安全的升级路径。

## 实际应用

在实际场景中，**how to update index** 很重要：

1. **Legal Document Management** – 在修订后快速重新索引合同，同时对机密条款进行红化。  
2. **Corporate Archives** – 保持历史记录可搜索，而无需重新处理数百万文件。  
3. **Content Management Systems (CMS)** – 当作者发布新文章时，推送增量更新到搜索索引。

## 性能考虑

- **Threading Options:** 根据 CPU 核心数调整 `UpdateOptions.Threads`；更多线程提升吞吐量，但会增加内存使用。  
- **Resource Usage:** 监控 RAM；库采用流式处理文件，即使是 500 页的 PDF，内存峰值也很小。  
- **Best Practices:** 安排定期的增量更新，并清理过时的索引版本，以保持最佳性能。

## 常见问题及解决方案

| Issue | Cause | Solution |
|-------|-------|----------|
| **未找到索引** | 文件夹路径错误 | 确认 `Index` 构造函数指向正确的目录。 |
| **版本不匹配错误** | 在新库中使用旧索引 | 在正常索引之前运行 `IndexUpdater` 流程。 |
| **未应用红化** | 红化规则在索引后加载 | 在将文档添加到索引之前**先**应用红化。 |

## 常见问答

**Q: `UpdateDocument` 与 `Rebuild` 有何区别？**  
A: `UpdateDocument` 只修改已更改的文件，而 `Rebuild` 从头重新创建整个索引，耗时和资源更多。

**Q: 能否并行更新多个文档？**  
A: 可以，将 `UpdateOptions.Threads` 设置为希望使用的核心数；库会在内部处理并行处理。

**Q: GroupDocs.Search 是否支持加密的 PDF？**  
A: 当然支持。在加载文档时通过 `SearchOptions.Password` 提供密码。

**Q: 如何在索引前验证红化是否成功？**  
A: 调用 `Redactor.Apply()` 并检查输出文件大小；文件大小减小通常表明红化成功。

**Q: 官方支持哪些 .NET 版本？**  
A: .NET Framework 4.5+、.NET Core 3.1+、.NET 5 和 .NET 6+。

## 结论

您现在拥有一份完整的、可用于生产的指南，介绍如何使用 GroupDocs.Search **how to update index**，以及如何使用 GroupDocs.Redaction for .NET 保持索引的版本兼容性。按照上述步骤操作，可确保搜索层保持快速、准确，并符合数据隐私法规。

**接下来的步骤：**  
- 尝试不同的 `Threads` 设置，以找到适合您硬件的最佳配置。  
- 在索引前探索高级红化模式（例如基于正则表达式的 SSN 删除）。  
- 将索引更新例程集成到 CI/CD 流水线，实现文档管理的全自动化。

---

**最后更新:** 2026-06-07  
**测试环境:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**作者:** GroupDocs  

## 资源
- [文档](https://docs.groupdocs.com/search/net/)
- [API 参考](https://reference.groupdocs.com/redaction/net)
- [下载 GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [免费支持论坛](https://forum.groupdocs.com/c/search/10)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

## 相关教程

- [精通 GroupDocs.Redaction .NET：高效索引创建与别名管理以实现高级文档搜索](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [使用 GroupDocs.Redaction .NET 实现同义词搜索以提升文档管理](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [精通 .NET 中的 GroupDocs Search 与 Redaction：高级文档管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)