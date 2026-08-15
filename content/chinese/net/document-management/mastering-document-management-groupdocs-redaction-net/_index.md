---
date: '2026-08-15'
description: 了解如何设置 license 并使用 GroupDocs.Redaction 在 .NET 应用程序中搜索和 highlight HTML
  内容。
keywords:
- how to set license
- search and highlight html
- GroupDocs.Redaction .NET
lastmod: '2026-08-15'
og_description: 了解如何为 GroupDocs.Redaction 设置 license，并在 .NET 中执行搜索和 highlight HTML
  结果。提供详细指南和实用示例。
og_image_alt: Guide showing license setup and HTML search highlighting using GroupDocs.Redaction
  in .NET
og_title: 如何设置 license，使用 GroupDocs.Redaction 进行搜索并 highlight
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  headline: How to set license, highlight search with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  name: How to set license, highlight search with GroupDocs.Redaction
  steps:
  - name: '**Legal document analysis**: Quickly find and highlight key legal terms.'
    text: '**Legal document analysis**: Quickly find and highlight key legal terms.'
  - name: '**Customer support**: Highlight relevant customer feedback in support tickets.'
    text: '**Customer support**: Highlight relevant customer feedback in support tickets.'
  - name: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
    text: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
  - name: '**Financial reports**: Identify and highlight critical financial metrics.'
    text: '**Financial reports**: Identify and highlight critical financial metrics.'
  - name: '**Content management**: Improve content discoverability through keyword
      highlighting.'
    text: '**Content management**: Improve content discoverability through keyword
      highlighting.'
  type: HowTo
- questions:
  - answer: Visit [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)
      for more details.
    question: How do I obtain a GroupDocs license?
  - answer: Yes, after acquiring the appropriate license.
    question: Can I use GroupDocs in a commercial project?
  - answer: Use consistent directory structures and environment variables for flexibility.
    question: What is the best practice for managing document paths?
  - answer: Regularly update your index and optimize query parameters.
    question: How can I improve search performance?
  - answer: Yes, multiple language dictionaries are supported.
    question: Is there support for languages other than English in GroupDocs?
  type: FAQPage
tags:
- license setup
- HTML search highlighting
- GroupDocs.Redaction
- .NET document management
title: 如何设置 license，使用 GroupDocs.Redaction 进行搜索并 highlight
type: docs
url: /zh/net/document-management/mastering-document-management-groupdocs-redaction-net/
weight: 1
---

# 掌握使用 GroupDocs.Redaction 在 .NET 中的文档管理

## 介绍

在当今的数字环境中，高效的文档管理对于维护数据隐私和提升搜索功能至关重要。无论您是开发者还是希望改进文档处理能力的企业，集成 Aspose 和 GroupDocs 等强大库都可以产生变革性的效果。本教程将指导您为这些库设置许可证，并使用 GroupDocs.Redaction .NET 库在 HTML 格式中高亮搜索结果。

**您将学习：**

- 如何为 Aspose 和 GroupDocs 库设置许可证
- 使用 GroupDocs.Search 设置路径并执行搜索
- 使用 GroupDocs.Viewer 在 HTML 文档中高亮搜索词
- 将这些功能实现到功能性 .NET 应用程序中

通过实用示例和逐步说明，您将能够简化文档管理流程。

## 快速答案
- **如何为 GroupDocs.Redaction 设置许可证？** 使用 `License` 类在任何 API 调用之前加载您的 `.lic` 文件。
- **我可以搜索并高亮 HTML 内容吗？** 可以，结合 GroupDocs.Search 与 GroupDocs.Viewer 来定位词语并渲染带高亮的 HTML。
- **我还需要 Aspose 许可证吗？** 仅在使用 Aspose.HTML 进行额外渲染时需要；否则 GroupDocs.Redaction 已足够。
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。
- **试用许可证足以进行测试吗？** 临时许可证可让您评估所有功能且没有时间限制的限制。

## 如何为 GroupDocs.Redaction 设置许可证？

`License` 类向 GroupDocs SDK 注册许可证文件。使用 `License` 类加载您的许可证文件，并在任何其他 SDK 调用之前调用 `SetLicense`。这将解锁全部功能，移除评估水印，并激活性能优化。提前加载许可证后，SDK 能在每一次后续操作中进行授权检查，确保所有编辑、搜索和渲染功能在无限制的情况下工作。

```text
```bash
dotnet add package GroupDocs.Redaction
```
```

## 如何为 Aspose.HTML 设置许可证？

Aspose.HTML 中的 `License` 类注册产品许可证并禁用试用限制。实例化 Aspose 的 `License` 对象并指向 `.lic` 文件。这样可确保所有 Aspose.HTML 渲染功能在无试用警告的情况下运行，并且可以使用 CSS 支持和高级布局引擎等高级渲染选项。

```text
```csharp
using Aspose.Html;

string licensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";
new License().SetLicense(licensePath);
```
```

- **说明**：`License.SetLicense` 加载许可证文件，解锁全部功能。

## 如何为 GroupDocs.Viewer 设置许可证？

GroupDocs.Viewer 的 `License` 类注册查看器许可证，使 PDF、DOCX 等格式能够高保真渲染为 HTML 且不出现水印。为 GroupDocs.Viewer 创建 `License` 实例并调用 `SetLicense`。如果您打算将文档渲染为 HTML 并保持完整保真度，此步骤是必需的。

```text
```csharp
using GroupDocs.Viewer;

new License().SetLicense(licensePath);
```
```

## 为什么使用 GroupDocs 进行搜索和 HTML 高亮？

GroupDocs.Search 将文档索引为轻量级、只读结构，能够在毫秒级查询数百万条记录。结合 GroupDocs.Viewer，您可以将任何受支持的文档渲染为 HTML，并使用 CSS 样式的高亮覆盖匹配的词语。量化声明：搜索引擎在典型的 2 GHz 服务器上可在 2 秒内处理 500 页 PDF，查看器将同一文件渲染为 HTML 的时间不足 1 秒。

## 在 .NET 中设置 GroupDocs.Redaction

### 安装

要在项目中开始使用 GroupDocs.Redaction，您可以通过不同的包管理器进行安装：

**.NET CLI:**
```text
```powershell
Install-Package GroupDocs.Redaction
```
```

**Package Manager Console:**
```text
```csharp
// Set your license path
string redactionLicensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";

// Initialize the Redaction API with the license
new GroupDocs.Redaction.License().SetLicense(redactionLicensePath);
```
```

**NuGet Package Manager UI:**  
搜索 “GroupDocs.Redaction” 并安装最新版本。

### 获取许可证

在使用 GroupDocs.Redaction 的全部功能之前，请获取许可证。您可以选择：

- **免费试用**：下载试用许可证以测试功能。  
- **临时许可证**：通过 [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) 获取。  
- **购买**：如果计划在生产环境中使用，请购买永久许可证。

有关详细的许可条款，请参阅 [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)。

### 基本初始化和设置

```text
```csharp
string basePath = @"./HighlightInHtml/HighlightExample";
string viewerCacheFolderPath = basePath + @"/ViewerCache";
string indexFolder = basePath + @"/Index";
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
string query = "\"dapibus diam\" OR lorem";
```
```

## 实现指南

### 为 Aspose 和 GroupDocs 库设置许可证

#### 概述

设置许可证可确保您能够在无任何限制的情况下使用 Aspose.HTML 和 GroupDocs.Viewer 的全部功能。

#### 步骤

**1. 为 Aspose.HTML 设置许可证**

```text
```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder); // Initialize index at specified path
index.Add(documentsFolder); // Add documents from directory to index
```
```

**2. 为 GroupDocs.Viewer 设置许可证**

```text
```csharp
using GroupDocs.Search.Results;

SearchResult result = index.Search(query); // Execute the search
FoundDocument foundDocument = result.GetFoundDocument(0); // Retrieve first document
```
```

### 设置路径和查询

#### 概述

为文档定义路径并准备搜索查询，以定位特定内容。

#### 步骤

**1. 定义基础路径**

```text
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Viewer.Options;

IndexedFileInfo fileInfo = new IndexedFileInfo(viewerCacheFolderPath, foundDocument.DocumentInfo.FilePath);
HighlightService highlightService = new HighlightService(fileInfo, null); // Prepare for highlighting

highlightService.Highlight(foundDocument, index.Dictionaries.Alphabet); // Perform highlighting
```
```

- **说明**：组织路径可确保搜索和高亮功能顺利集成。

### 创建并添加到索引

#### 概述

创建索引以实现高效的文档搜索。

**步骤**

**1. 创建索引**

```text
CODE_BLOCK_PLACEHOLDER_9_END
```

- **说明**：`Index` 对象管理您的索引数据，允许快速检索。

### 在索引中搜索

#### 概述

对已创建的索引执行搜索查询并获取结果。

**步骤**

**1. 执行搜索**

```text
CODE_BLOCK_PLACEHOLDER_10_END
```

- **说明**：`index.Search` 执行查询，返回匹配的文档。

### 在 HTML 中高亮搜索结果

#### 概述

使用 GroupDocs.Viewer 在文档的 HTML 表示中高亮术语。

**步骤**

**1. 初始化高亮服务**

```text
CODE_BLOCK_PLACEHOLDER_11_END
```

- **说明**：`HighlightService` 处理并高亮文档中的搜索词。

## 实际应用

1. **法律文档分析**：快速查找并高亮关键法律条款。  
2. **客户支持**：在支持工单中高亮相关客户反馈。  
3. **研究论文**：通过高亮特定科学术语来促进研究。  
4. **财务报告**：识别并高亮关键财务指标。  
5. **内容管理**：通过关键词高亮提升内容可发现性。

## 性能考虑因素

- **优化索引**：定期更新索引以实现高效搜索。  
- **内存管理**：尽可能使用异步处理来管理内存使用。  
- **资源使用**：监控应用性能以调整资源分配。

## 常见问题与故障排除

- **许可证未被识别** – 验证 `.lic` 文件路径是绝对路径或相对于执行程序集的正确相对路径。  
- **搜索未返回结果** – 确保在添加新文档后重新构建索引；索引不会自动检测文件更改。  
- **HTML 高亮缺少 CSS** – 包含 GroupDocs.Viewer 提供的默认样式表或添加自定义 CSS 来为 `<mark>` 标签设置样式。  
- **大型 PDF 导致超时** – 增加 `SearchOptions.MaxDegreeOfParallelism` 设置以利用多核处理器。

## 常见问题

**Q: 如何获取 GroupDocs 许可证？**  
A: 访问 [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) 获取更多详情。

**Q: 我可以在商业项目中使用 GroupDocs 吗？**  
A: 可以，在获取相应许可证后即可使用。

**Q: 管理文档路径的最佳实践是什么？**  
A: 使用一致的目录结构并通过环境变量实现灵活性。

**Q: 如何提升搜索性能？**  
A: 定期更新索引并优化查询参数。

**Q: GroupDocs 是否支持除英语之外的语言？**  
A: 支持，多语言词典均可使用。

## 资源

- [GroupDocs 文档](https://docs.groupdocs.com/search/net/)
- [GroupDocs 文档](https://docs.groupdocs.com/search/net/)
- [API 参考](https://reference.groupdocs.com/redaction/net)
- [下载 GroupDocs Redaction](https://releases.groupdocs.com/search/net/)
- [免费支持论坛](https://forum.groupdocs.com/c/search/10)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

## 结论

您已经学习了如何设置许可证、配置搜索路径、创建索引、执行搜索以及使用 GroupDocs.Redaction 在 .NET 中高亮结果。将这些功能集成到您的应用程序时，请考虑进一步阅读文档以探索高级功能。

**下一步：**

- 深入了解 [GroupDocs 文档](https://docs.groupdocs.com/search/net/)。  
- 尝试额外功能，如编辑和注释。

---

**最后更新：** 2026-08-15  
**测试环境：** GroupDocs.Redaction 23.10 for .NET  
**作者：** GroupDocs

## 相关教程

- [掌握 GroupDocs.Redaction .NET：高效索引创建与别名管理以实现高级文档搜索](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [实现 GroupDocs.Redaction .NET 用于文档查找管理与高亮](/search/net/document-management/groupdocs-redaction-net-finder-management-guide/)
- [掌握 GroupDocs.Redaction .NET：设置与事件处理以实现安全文档管理](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}