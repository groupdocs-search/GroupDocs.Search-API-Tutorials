---
date: '2026-04-04'
description: 学习如何使用 GroupDocs.Search 搜索法律文档并管理索引，以及在 .NET 中使用 GroupDocs.Redaction
  对医疗记录进行脱敏处理。
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: 使用 GroupDocs Search 与 Redaction for .NET 搜索法律文档
type: docs
url: /zh/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# 使用 GroupDocs Search 与 Redaction 在 .NET 中搜索法律文档

在当今数据驱动的环境中，**搜索法律文档** 快速且安全是任何组织的关键需求。无论您处理的是合同、法院文件还是合规报告，GroupDocs.Search 为您提供快速、可扩展的索引，而 GroupDocs.Redaction 确保敏感信息保持隐藏。本教程将指导您设置可搜索索引、从多个文件夹添加文档，并配置脱敏，以便安全地搜索医疗记录和其他机密文件。

## 快速答案
- **GroupDocs.Search 的作用是什么？** 它为各种文档格式创建全文可搜索索引。  
- **我可以在搜索前进行脱敏吗？** 可以——使用 GroupDocs.Redaction 来遮蔽或删除敏感数据。  
- **如何将文档添加到索引？** 对每个文件夹调用 `index.Add("folderPath")`。  
- **支持哪些文件类型？** PDF、DOCX、PPTX、TXT 等多种格式。  
- **生产环境需要许可证吗？** 提供临时试用版；商业使用需要永久许可证。

## 前置条件
要跟随本教程，请确保您拥有：
- .NET Core SDK（3.1 或更高）已安装。  
- Visual Studio Code、Visual Studio 或其他支持 .NET 的 IDE。  
- 具备 C# 编程的基本知识。

### 许可证获取
您可以先免费试用这两个库。若需长期使用，请考虑获取临时许可证或从 [GroupDocs 网站](https://purchase.groupdocs.com/temporary-license/) 购买。

## 安装所需的包

**GroupDocs.Search 安装：**  
使用 **.NET CLI**，运行：
```bash
dotnet add package GroupDocs.Search
```
或者，在 Visual Studio 中使用包管理器控制台：
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction 安装：**  
- 使用 .NET CLI：
```bash
dotnet add package GroupDocs.Redaction
```
- 或者，通过包管理器：
```powershell
Install-Package GroupDocs.Redaction
```

如果您更喜欢使用 GUI，可访问 NuGet 包管理器 UI，搜索 “GroupDocs.Redaction” 并进行安装。

## 配置 Redactor 设置
在开始脱敏之前，您可能需要微调脱敏行为（例如，设置脱敏颜色或定义自定义模式）。以下代码片段展示了基本初始化：

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **专业提示：** 调整 `redactorSettings` 以符合组织的合规政策（例如，用黑框替换文本、在脱敏前应用 OCR 等）。

## 实施指南

### 如何搜索法律文档？
创建可搜索索引是快速检索法律文档的基础。GroupDocs.Search 让您指向任意文件夹，构建索引，然后在成千上万的文件中执行复杂查询。

### 如何将文档添加到索引
添加文档非常直接——只需将库指向保存文件的目录即可。您可以添加多个文件夹，这在法律语料库分布在不同位置时非常方便。

#### 创建和管理索引
**概述：**  
创建索引是实现高效文档搜索操作的第一步。GroupDocs.Search 允许您在任意选择的目录中创建可搜索索引，从而快速检索文档。

##### 步骤 1：创建索引
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*说明：* `Index` 在指定目录初始化搜索索引。确保路径符合项目的文件夹结构。

##### 步骤 2：向索引添加文档
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*说明：* `Add` 方法会扫描给定文件夹并将所有支持的文档加入索引。可用于从多个来源（如合同、案件文件或医疗记录）**将文档添加到索引**。

### 检索和显示索引报告
**概述：**  
索引报告让您了解处理了多少文档、总词项数以及存储大小——这些都是性能调优的关键指标。

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*说明：* `GetIndexingReports` 返回一个报告数组，详细说明索引过程，帮助您监控并优化性能。

## 实际应用
1. **法律文档管理：** 自动对案件文件进行索引，实现法规、简报和判决的即时检索。  
2. **医疗记录系统：** 使用 GroupDocs.Redaction 对患者记录进行脱敏搜索，保护隐私。  
3. **企业人力资源门户：** 将可搜索的员工文件与脱敏功能结合，保护个人数据。

## 性能考虑因素
- **优化索引大小：** 定期清理过期条目并重建索引，以保持精简。  
- **内存管理：** 利用 .NET 垃圾回收器；在不再需要时释放 `Index` 对象。  
- **可扩展性最佳实践：** 将索引存储在高速 SSD 上，并考虑将大型语料库分片到多个索引。

## 常见问题

**Q: GroupDocs.Search 的主要用途是什么？**  
A: 它非常适合从大型文档集合创建可搜索索引，实现对法律和医疗文件的快速检索。

**Q: GroupDocs.Redaction 如何确保数据隐私？**  
A: 它允许您定义脱敏模式，在文档被索引或共享之前永久删除或遮蔽敏感信息。

**Q: 我可以在云环境中使用这些库吗？**  
A: 可以——这两个库都可以在 Azure、AWS 或任何具备适当许可证的容器化 .NET 部署中使用。

**Q: GroupDocs.Search 支持哪些文件格式？**  
A: PDF、Word、Excel、PowerPoint、TXT、HTML 等众多企业格式。

**Q: 我该如何排查索引错误？**  
A: 核实文件夹路径、检查文件权限，并查看 `IndexingReport` 的控制台输出以获取具体错误代码。

## 资源
- **文档：** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API 参考：** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **下载：** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **免费支持：** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **临时许可证：** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**最后更新：** 2026-04-04  
**测试环境：** GroupDocs.Search 23.12，GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs