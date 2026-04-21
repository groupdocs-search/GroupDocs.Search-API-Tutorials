---
date: '2026-04-21'
description: 了解如何使用 GroupDocs.Redaction for .NET 过滤文件，包括按创建日期、文件大小、修改日期进行过滤，以及如何应用
  NOT 过滤器。
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: 如何使用 GroupDocs.Redaction for .NET 过滤文件
type: docs
url: /zh/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# 使用 GroupDocs.Redaction for .NET 过滤文件的方法

在当今快速发展的数字环境中，**如何过滤文件**的效率可以决定您的生产力。无论您是需要按扩展名、创建日期、大小或修改日期来隔离文档，稳健的过滤策略都能节省时间、降低存储成本，并保持搜索索引整洁。在本教程中，我们将通过使用 GroupDocs.Redaction for .NET 的真实案例，向您展示如何准确地过滤文件以满足常见业务需求。

## 快速答案
- **需要哪个库？** GroupDocs.Redaction for .NET（通过 NuGet 安装）。  
- **可以按创建日期过滤吗？** 可以——使用 `CreateCreationTimeRange`。  
- **如何排除某些类型？** 使用 `DocumentFilter.CreateNot` 应用 NOT 过滤器。  
- **是否支持文件大小过滤？** 当然，使用 `CreateFileLengthRange` 或上下界限。  
- **需要许可证吗？** 生产环境使用需要试用版或正式许可证。

## 什么是使用 GroupDocs.Redaction 的文件过滤？
文件过滤允许您根据扩展名、日期、路径模式或大小等元数据告诉索引引擎哪些文档应包含或忽略。通过定义精确的 `DocumentFilter` 规则，您可以保持索引精简，搜索快速。

## 为什么使用 GroupDocs.Redaction for .NET？
- **内置过滤助手**——无需编写自定义文件系统代码。  
- **逻辑运算符**——使用 AND、OR 和 NOT 组合多个条件。  
- **性能优化**——过滤在索引期间应用，而不是之后。  
- **跨平台**——兼容 .NET Framework、.NET Core 和 .NET 5/6+。

## 前置条件
- 已安装 .NET Framework 4.6+ 或 .NET Core 3.1+。  
- Visual Studio 或您喜欢的 C# IDE。  
- 基础 C# 知识。  

### 必需的库与设置
使用您喜欢的方法安装 NuGet 包：

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **专业提示：** 安装后，将许可证文件添加到项目根目录，并在创建任何 Redactor 或 Index 对象之前调用 `License.SetLicense("license-file-path")`。

## 设置 GroupDocs.Redaction for .NET

首先，创建指向您要处理的文档的 `Redactor` 实例：

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **为什么重要：** 初始化 Redactor 可确保库在后续工作流中准备好应用过滤器和编辑规则。

## 如何按扩展名过滤文件

按文件扩展名过滤是缩小文档集合的最常见方式。下面我们仅保留 FB2、EPUB 和 TXT 文件。

### 按文件扩展名过滤

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何使用 NOT 过滤器排除不需要的类型

如果您需要**应用 NOT 过滤**逻辑——例如排除 HTML 和 PDF 文件——请使用 `CreateNot`。

### 排除 HTM、HTML 和 PDF 文件

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何按创建日期过滤文件

当您需要**按创建日期过滤**时，指定起始和结束的 `DateTime`。

### 按创建日期范围过滤

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何按修改日期过滤文件

与创建日期类似，您可以将结果限制为在特定时间点之前修改的文件。

### 按修改日期过滤

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何使用正则表达式按路径过滤文件

如果您的文件夹结构遵循命名约定，正则表达式可以定位特定路径。

### 按文件路径模式过滤

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何按文件大小过滤

在处理带宽或存储限制时，控制文档大小至关重要。

### 按文件大小过滤（50 KB – 100 KB）

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何使用 AND 组合多个条件

当您需要一次使用多个条件**过滤文件**时，使用 `CreateAnd` 将它们组合起来。

### 逻辑 AND 示例

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何使用 OR 组合多个条件

当任意规则满足即可时，使用 `CreateOr`。

### 逻辑 OR 示例

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 常见问题与解决方案
- **过滤未应用：** 确保在创建 `Index` 实例 **之前** 分配 `settings.DocumentFilter`。  
- **出现意外文件：** 再次检查文件扩展名是否包含前导点（`.txt`）。  
- **性能下降：** 使用 AND 组合过滤器，以在索引管道的早期减少扫描的文件数量。  
- **正则表达式错误：** 在路径模式中转义特殊字符，或使用 `RegexOptions.IgnoreCase` 进行不区分大小写的匹配。

## 常见问答

**问：** 我可以将 NOT 过滤器与 AND 过滤器组合吗？  
**答：** 可以。先构建 NOT 过滤器（`DocumentFilter.CreateNot`），然后将其作为参数之一传递给 `DocumentFilter.CreateAnd`。

**问：** 如何过滤大于 10 MB 的文件？  
**答：** 使用 `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` 仅包含超过该大小的文件。

**问：** 是否可以同时按创建日期和修改日期过滤？  
**答：** 当然。分别创建每个过滤器，然后使用 `CreateAnd` 将它们组合。

**问：** 这些过滤器能用于云存储路径吗？  
**答：** 过滤器在本地文件系统上工作。对于云来源，请先将文件下载到临时文件夹，然后再应用相同的过滤器。

**问：** 更改过滤器是否需要重新索引？  
**答：** 是的。过滤器在调用 `index.Add` 时评估。更改过滤器意味着需要重新构建索引以反映新条件。

## 结论

通过掌握使用 GroupDocs.Redaction for .NET **如何过滤文件**——无论是按扩展名、创建日期、修改日期、文件大小，还是使用 NOT 逻辑——您都可以简化文档管理，保持索引高性能，并专注于真正重要的内容。尝试使用逻辑运算符将过滤定制为符合您的业务规则，您将立即在速度和存储效率上获得提升。

---

**最后更新：** 2026-04-21  
**测试版本：** GroupDocs.Redaction 24.11 for .NET  
**作者：** GroupDocs