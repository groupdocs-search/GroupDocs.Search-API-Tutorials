---
date: '2026-04-02'
description: 学习如何在 .NET 中使用 GroupDocs.Search 和 GroupDocs.Redaction 创建搜索索引（GroupDocs），并向索引添加文档，同时实现分面搜索。
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: 使用遮蔽功能的 GroupDocs 创建搜索索引 .NET 分面搜索
type: docs
url: /zh/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# 创建搜索索引 GroupDocs 与 Redaction .NET 分面搜索

在现代应用程序中，**使用 GroupDocs 创建搜索索引**对于快速、准确的文档检索至关重要。无论您处理的是法律合同、产品目录还是大型知识库，构建良好的索引都能让您**将文档添加到索引**并在几秒钟内运行强大的分面搜索。本教程将带您完整了解整个过程——从设置 GroupDocs.Redaction 到构建简单和复杂的分面查询——帮助您在 .NET 项目中提供响应迅速的搜索体验。

## 快速答案
- **What is the primary purpose?** 创建使用 GroupDocs 的搜索索引并启用分面搜索。  
- **Which libraries are required?** GroupDocs.Redaction 和 GroupDocs.Search for .NET。  
- **How do I add documents to the index?** 在初始化索引后使用 `index.Add(documentsFolder)`。  
- **Can I run complex queries?** 可以，结合对象查询和逻辑运算符实现高级过滤。  
- **Is a license needed?** 开发阶段可使用免费试用版，生产环境需购买商业许可证。

## 什么是分面搜索，为什么要与 GroupDocs 一起使用？
分面搜索让用户通过同时应用多个过滤器（如类别、日期或作者）来细化结果。与 **GroupDocs.Redaction** 结合后，您可以获得安全且可搜索的内容，遵循遮蔽规则，特别适合合规性要求高的环境。

## 前提条件

### 必需的库、版本和依赖项
- **GroupDocs.Redaction .NET** – 最新稳定版。  
- **GroupDocs.Search .NET** – 与 Redaction 紧密配合用于索引。

### 环境设置要求
- **IDE**: Visual Studio 2019 或更高版本。  
- **Framework**: .NET Core 3.1、.NET 5 或 .NET 6。  
- **OS Compatibility**: Windows、Linux、macOS。

### 知识前提
具备基本的 C# 技能并对分面搜索概念有一定了解会有帮助，但本分步指南对新手也非常友好。

## 为 .NET 设置 GroupDocs.Redaction

### 安装信息
您可以使用以下任意方法添加 GroupDocs.Redaction 包：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- 在搜索框中输入 “GroupDocs.Redaction” 并安装最新版本。

### 获取许可证的步骤
要解锁全部功能，请先使用免费试用版或获取永久许可证：

1. 访问 [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) 了解许可证选项。  
2. 按照屏幕指示获取试用或已购买的许可证文件。

### 基本初始化和设置
安装完包后，在应用程序中初始化 Redactor：

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## 如何创建搜索索引 groupdocs

下面我们将实现分为两部分：**简单分面搜索** 和 **复杂查询**。每部分展示如何 **创建搜索索引 groupdocs**、添加文档并执行查询。

### 功能 1：简单分面搜索

**Overview**  
分面搜索让用户通过选择多个条件来缩小结果范围。本节演示使用 GroupDocs.Search 的直接方法。

#### 步骤 1：定义索引和文档文件夹
设置索引所在的文件夹路径以及源文档所在的文件夹路径。

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### 步骤 2：创建索引
在前面定义的文件夹中初始化搜索索引。

```csharp
Index index = new Index(indexFolder);
```

#### 步骤 3：将文档添加到索引
加载文档，使其可被搜索。

```csharp
index.Add(documentsFolder);
```

#### 步骤 4：执行文本查询搜索
对 **content** 字段执行基本的文本查询。

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### 步骤 5：执行对象查询搜索
使用面向对象的查询实现更细粒度的控制。

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### 功能 2：复杂查询

**Overview**  
当需要组合多个过滤条件（如文件名模式和短语匹配）时，可使用逻辑运算符构建复杂查询。

#### 步骤 1：定义索引和文档文件夹
在更高级的场景中复用相同的文件夹结构。

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### 步骤 2：创建索引并添加文档
（参见简单示例的步骤 2‑3，保持不变。）

#### 步骤 3：执行文本查询搜索
运行一个复合文本查询，混合文件名和内容条件。

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### 步骤 4：构建并执行对象查询
以编程方式构造相同的逻辑。

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

继续组合短语、范围和布尔运算符，以匹配您的精确业务规则。

## 实际应用

1. **E‑Commerce Platforms** – 按类别、价格和评分过滤产品。  
2. **Document Management Systems** – 按作者、日期或保密级别定位合同。  
3. **Content Portals** – 让读者通过标签、主题和发布日期进行深入筛选。

## 性能考虑

- **Index Refresh**: 定期对新建或更新的文件重新索引，以保持搜索速度。  
- **Memory Management**: 使用完毕后释放 `Index` 对象，尤其在处理大数据集时。  
- **Asynchronous Indexing**: 使用 `Task.Run` 或后台服务，避免在大量索引时导致 UI 卡顿。

## 常见问题及解决方案

| Issue | Solution |
|-------|----------|
| **Index not found** | 验证 `indexFolder` 路径并确保文件夹具有写入权限。 |
| **No results returned** | 检查查询的字段（如 `Content`、`Filename`）是否已被索引。 |
| **Out‑of‑memory errors** | 将文档分批处理，并考虑增大 .NET GC 堆大小。 |

## 常见问答

**Q: What is faceted search?**  
A: 分面搜索允许用户使用多个独立的过滤器（如类别、日期或作者）来细化结果。

**Q: How do I handle large datasets with GroupDocs.Search?**  
A: 使用增量索引、批处理以及异步操作，以保持低内存占用和高性能。

**Q: Can I integrate GroupDocs functionalities into existing .NET applications?**  
A: 可以，库设计为可无缝集成到任何 .NET 项目中。

**Q: What are some common issues with faceted search?**  
A: 复杂的查询语法以及确保所有相关字段已被索引是常见挑战；通过充分测试和维护索引可减轻这些问题。

**Q: How do I acquire a temporary license for GroupDocs?**  
A: 访问 [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) 申请试用许可证，以在评估期间解锁全部功能。

## 资源
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Last Updated:** 2026-04-02  
**Tested With:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Author:** GroupDocs