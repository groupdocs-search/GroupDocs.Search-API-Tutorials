---
date: '2026-04-02'
description: 了解如何通过文件扩展名进行过滤，并使用 GroupDocs.Redaction for .NET 仅搜索 txt 文件——提升文档管理效率。
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: 在 .NET 中使用 GroupDocs.Redaction 按文件扩展名过滤
type: docs
url: /zh/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# 在 .NET 中使用 GroupDocs.Redaction 按文件扩展名过滤

在大量文件集合中搜索可能会让人感到不知所措，尤其是当您只需要特定文件类型的结果时。在本教程中，您将了解如何使用 GroupDocs.Redaction for .NET **按文件扩展名过滤**，从而仅搜索 txt 文件或您选择的任何其他扩展名。我们将演示如何设置文件类型和基于路径的过滤器，让您快速定位所需的文档。

## 快速答案
- **“filter by file extension” 是什么作用？** 它将搜索限制为匹配给定文件扩展名的文档（例如 *.txt）。  
- **为什么要使用 GroupDocs.Redaction？** 它提供了内置的过滤 API，快速且易于集成。  
- **我需要许可证吗？** 免费试用可用于测试；生产环境需要付费许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **我可以组合文件类型和路径过滤器吗？** 可以——应用多个过滤器以实现高度精确的搜索。  

## 您将学习的内容
- 如何 **按文件扩展名过滤**，仅搜索文本文件。  
- 如何设置 **文件路径过滤器**，将结果限制在特定文件夹或命名模式。  
- 保持索引快速且内存高效的技巧。  

## 前提条件

在深入之前，请确保您拥有：

- **GroupDocs.Redaction Library** 已安装并与您的 .NET 项目兼容。  
- 开发环境，例如 Visual Studio 或 VS Code。  
- 基本的 C# 知识以及对 .NET 项目结构的了解。  

## 为 .NET 设置 GroupDocs.Redaction

首先，将库添加到您的项目中。

**使用 .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**使用 Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

或者在 NuGet 包管理器 UI 中找到 “GroupDocs.Redaction”，并安装最新版本。

### 许可证获取

您可以先使用免费试用或请求临时许可证。对于长期项目，请从官方网站购买许可证。  

### 基本初始化

安装包后，创建一个索引来保存文档的引用：  
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## 实施指南

### 功能 1：为文本文档 (.txt) 设置过滤器

#### 如何为文本文档按文件扩展名过滤

1. **定义索引和文档文件夹**  
   设置源文件所在的路径：  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **创建索引**  
   将源文件夹中的所有文件加载到索引中：  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **使用文件扩展名过滤器配置搜索选项**  
   指示引擎仅考虑 *.txt 文件：  

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **执行搜索**  
   运行查询；过滤器确保非文本文件被忽略：  

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *说明*: `Search` 方法返回满足过滤条件的匹配项，显著降低噪音并提升性能。  

### 功能 2：文件路径过滤器

#### 为什么使用文件路径过滤器？

有时您需要将搜索限制在特定部门文件夹或共享命名约定的一组文件中。路径过滤器正是为此而设。

1. **定义索引和文档文件夹**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **创建索引**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **使用基于路径的正则表达式配置搜索选项**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   此正则表达式匹配完整路径中包含单词 “Lorem” 的任何文件，使您能够定位特定子文件夹。  

4. **执行基于路径的搜索**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## 实际应用
- **法律文档管理** – 快速定位以纯文本文件形式存储的相关合同。  
- **学术研究** – 仅提取属于特定项目文件夹的 *.txt 研究笔记。  
- **企业报告** – 按部门路径过滤内部报告（例如 `/Finance/2025/`）。  

## 性能考虑
- 仅索引实际需要的文档类型；不必要的文件会增加索引大小和搜索时间。  
- 使用计划任务调用 `index.Add()` 来保持索引最新，以处理新文件或已更改的文件。  
- 使用简单的正则表达式；过于复杂的模式会拖慢搜索引擎。  
- 在不再需要时释放 `Index` 对象以释放内存。  

## 结论
您现在已经了解如何使用 GroupDocs.Redaction for .NET **按文件扩展名过滤** 并应用 **文件路径过滤器**。这些技术让您对大型文档集合进行细粒度控制，使搜索更快、更相关。接下来，尝试组合多个过滤器或将搜索集成到更大的应用工作流中。  

## 常见问题

**Q1: 我可以过滤除文本文件之外的文档吗？**  
A1: 可以，GroupDocs.Redaction 支持多种格式。将 `CreateFileExtension` 中的参数更改为所需的扩展名（例如 “.pdf”）。

**Q2: 我如何定期更新搜索索引？**  
A2: 安排后台服务或 cron 作业，对需要保持最新的目录运行 `index.Add()`。

**Q3: 按文件路径过滤会有性能影响吗？**  
A3: 经过适当优化的正则表达式影响很小，但始终使用自己的数据集进行基准测试。

**Q4: 我可以组合多个过滤器以实现更精细的搜索吗？**  
A4: 当然。您可以链式使用过滤器或创建复合过滤器，以同时针对文件类型和路径。

**Q5: 我在哪里可以找到更多关于 GroupDocs.Redaction 的资源？**  
A5: 访问官方文档 [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) 获取详细指南和 API 参考。  

## 常见问答

**Q: `SearchDocumentFilter` 能处理加密文件吗？**  
A: 过滤器本身作用于文件元数据，只要在索引时提供必要的解密凭证，加密文件仍会被索引。

**Q: 我可以使用通配符而不是正则表达式进行路径过滤吗？**  
A: 当前 API 需要正则表达式，但您可以模拟简单通配符（例如 `.*` 表示任意字符）。

**Q: 索引多大时需要考虑分片？**  
A: 几百 GB 的索引可能受益于拆分为多个逻辑索引；随着集合增长请测试性能。

**Q: 是否有内置方法从索引中删除文档？**  
A: 有——调用 `index.Delete(documentId)` 或 `index.DeleteAll()` 来管理过期条目。

**Q: 是否有办法在加载完整文档前预览搜索结果？**  
A: `SearchResult` 对象包含片段信息，您可以在 UI 中显示而无需打开整个文件。  

## 资源
- **文档**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)  
- **API 参考**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **下载**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)  
- **免费支持**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **临时许可证**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)  

---

**最后更新：** 2026-04-02  
**测试环境：** GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs