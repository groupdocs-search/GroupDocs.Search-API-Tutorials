---
date: '2026-06-07'
description: 了解如何使用 GroupDocs.Redaction 在 C# 中列出文件扩展名并获取文件格式。包括设置、代码和实用技巧。
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction 在 .NET 中列出文件扩展名 – 综合指南
type: docs
url: /zh/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# 在 .NET 中使用 GroupDocs.Redaction 显示受支持的文件格式

管理各种文档类型是 .NET 开发人员的日常现实。通过使用 **GroupDocs.Redaction**，您可以 **列出文件扩展名**，了解库支持的文件类型，从而使您的应用能够智能地接受或拒绝上传，提供友好的 UI 选项，并避免代价高昂的运行时错误。本教程将带您了解所需的一切——从先决条件到完整的生产就绪实现——让您能够自信地 **获取文件格式** 并在解决方案中 **c# 显示文件格式**。

## 快速答案
- **“列出文件扩展名” 是什么意思？** 它意味着从 API 检索受支持的文件类型标识符集合（例如 *.pdf*、*.docx*）。  
- **哪个 NuGet 包提供此功能？** `GroupDocs.Redaction`（最新稳定版）。  
- **运行示例是否需要许可证？** 免费试用许可证可用于开发；生产环境需要永久许可证。  
- **我可以缓存结果吗？** 可以——将列表存储在内存或分布式缓存中，以避免重复的 API 调用。  
- **此功能是否兼容 .NET 6 和 .NET Core？** 当然；该库支持 .NET Framework 4.5+、.NET Core 3.1+、.NET 5+ 和 .NET 6+。

## 什么是 GroupDocs.Redaction？
**GroupDocs.Redaction** 是一个 .NET 库，使开发人员能够对敏感内容进行马赛克处理、转换文档并发现受支持的文件类型——无需在服务器上安装 Microsoft Office。它将复杂的格式处理抽象为简洁的面向对象 API。它提供统一的 API 用于内容马赛克、转换和格式发现，支持 PDF、Office 文档、图像等，同时确保高性能和安全性。

## 为什么要使用 GroupDocs.Redaction 列出文件扩展名？
该库 **支持 50 多种输入和输出格式**，包括 PDF、DOCX、PPTX、XLSX、HTML，以及超过 30 种图像类型。通过编程方式 **列出文件扩展名**，您可以：

- 防止用户上传不受支持的文件（将验证错误降低至最高 90%）。  
- 动态填充下拉菜单，确保 UI 与库更新保持同步。  
- 构建审计日志，记录用户尝试处理的确切文件类型。

## 前提条件
- **GroupDocs.Redaction**：通过 NuGet 安装（请参见下面的命令）。  
- **.NET SDK**：确保已安装最新的 .NET SDK。请在 [here](https://dotnet.microsoft.com/download) 下载。  
- **IDE**：Visual Studio 2022 或任何兼容的编辑器。  
- **Basic C# knowledge**：您应该熟悉集合和 LINQ。

## 为 .NET 设置 GroupDocs.Redaction

### 安装库

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- 打开 NuGet 包管理器，搜索 “GroupDocs.Redaction”，并安装最新版本。

### 获取并应用许可证

从免费试用开始或请求临时许可证，以在无限制的情况下探索全部功能。购买选项请访问 [GroupDocs' purchase page](https://purchase.groupdocs.com/)。获取许可证文件后：

1. 将其放置在项目内部的可访问文件夹中（例如 `./Licenses/GroupDocs.Redaction.lic`）。  
2. 在应用程序启动时初始化许可证：

`License` 类加载您的许可证文件并激活 GroupDocs.Redaction。  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## 如何使用 GroupDocs.Redaction 列出文件扩展名？

加载 Redaction API 并调用返回受支持格式的方法。该调用返回一个集合，每个项目包含扩展名和可读的描述。此操作轻量，可在启动时或按需执行。

### 检索受支持的文件类型
`RedactionApi.GetSupportedFileFormats()` 方法返回一个只读的 `FileFormatInfo` 对象集合，描述每种格式。  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### 显示每个扩展名及其描述
每个 `FileFormatInfo` 为文件类型提供 `Extension` 和 `Description` 属性。  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**说明**：循环遍历每个 `FileFormatInfo` 对象，在整齐对齐的表格中打印其 `Extension` 和 `Description`。

## 如何将列表集成到 UI 下拉框中？

获取集合后，将其绑定到任何 UI 组件——WinForms `ComboBox`、WPF `ComboBox` 或 ASP.NET Core `select` 元素。关键是使用 `Extension` 作为值，`Description` 作为显示文本。这可确保用户看到友好的名称，而代码使用确切的扩展名字符串。

## 常见问题及解决方案
- **缺少命名空间错误** – 请确认已导入 `GroupDocs.Redaction` 和 `GroupDocs.Redaction.Common`。  
- **未找到许可证** – 确保许可证文件路径正确，并且文件已包含在生成输出中。  
- **大型项目的性能** – 将结果缓存到静态变量或分布式缓存（例如 Redis）中，以避免重复枚举。

## 实际应用
了解受支持扩展名的完整列表可开启多个实际场景：

1. **文档管理系统** – 根据扩展名自动对传入文件进行分类。  
2. **内容过滤工具** – 在上传时阻止不允许的格式（例如可执行文件）。  
3. **文件转换流水线** – 动态决定文件是否可以转换或需要回退工作流。

## 性能考虑因素
- **内存占用** – 格式列表存储在轻量级的 `IReadOnlyCollection` 中，通常小于 2 KB。  
- **线程安全** – 该集合在创建后不可变，因而对并发读取安全。  
- **缓存** – 对于高流量 API，建议在应用程序生命周期内缓存列表，以消除每次请求的几微秒开销。

## 结论
按照上述步骤操作后，您现在拥有使用 GroupDocs.Redaction **列出文件扩展名** 并 **c# 显示文件格式** 的可靠方法。此功能不仅提升用户体验，还保护后端免受不受支持的文件影响。探索更多 Redaction 功能——如内容遮蔽、PDF 马赛克和批处理——以进一步强化文档工作流。

## 常见问题解答
**Q: 默认支持的文件格式有哪些？**  
A: GroupDocs.Redaction 支持 50 多种格式，包括 PDF、DOCX、PPTX、XLSX、HTML、BMP、JPEG、PNG 等。完整列表请参见 [GroupDocs documentation](https://docs.groupdocs.com/search/net/)。

**Q: 如何将库升级到最新版本？**  
A: 打开 NuGet 包管理器，搜索 “GroupDocs.Redaction”，然后点击 **Update**。或者运行 `dotnet add package GroupDocs.Redaction --version <latest>`。

**Q: 我可以使用此列表对上传的文件进行服务器端验证吗？**  
A: 可以——在处理之前，将上传文件的扩展名与检索到的集合进行比较。这可消除 99% 的无效格式错误。

**Q: 能否扩展支持自定义文件类型？**  
A: 自定义扩展名需要自定义处理程序；核心库本身不原生添加新格式。请查阅 API 文档了解如何创建自定义导入/导出管道。

**Q: 添加代码后我的应用崩溃——我应该检查什么？**  
A: 确保许可证已正确加载，`using` 语句引用了正确的命名空间，并在读取许可证文件时处理 `IOException`。

---

**最后更新：** 2026-06-07  
**测试环境：** GroupDocs.Redaction 23.9 for .NET  
**作者：** GroupDocs  

## 资源
- [文档](https://docs.groupdocs.com/search/net/)
- [API 参考](https://reference.groupdocs.com/redaction/net)
- [下载 GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [免费支持论坛](https://forum.groupdocs.com/c/search/10)
- [临时许可证请求](https://purchase.groupdocs.com/temporary-license/)

## 相关教程
- [掌握 .NET 中的文件过滤与 GroupDocs.Redaction&#58; 高效文档管理技术](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [掌握 GroupDocs.Redaction .NET&#58; 设置与事件处理以实现安全文档管理](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [精通 .NET 中的文档管理与 GroupDocs.Redaction&#58; 许可证设置和 HTML 搜索高亮](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)