---
date: '2026-04-05'
description: 学习如何使用 GroupDocs.Redaction 在 .NET 中创建密码字典，并从字典中移除密码，以实现安全的文档处理。
keywords:
- create password dictionary .net
- remove password from dictionary
- GroupDocs Redaction password management
title: 使用 GroupDocs Redaction 在 .NET 中创建密码字典
type: docs
url: /zh/net/advanced-features/master-document-password-management-net-groupdocs/
weight: 1
---

# 使用 GroupDocs Redaction 创建 .NET 密码字典

在当今数字化的世界，保护敏感文档至关重要，**您将学习如何使用 GroupDocs.Redaction 创建 .NET 密码字典**。无论您是保护公司报告的商务专业人士，还是保护个人文件的个人用户，强大的密码字典可以帮助您控制访问并简化安全索引。

**您将学习**
- 如何使用 GroupDocs **创建 .NET 密码字典**
- 在不再需要时的 **从字典中移除密码** 技术
- 使用嵌入密码安全索引文档的步骤
- 如何高效搜索受密码保护的文件

## 快速答案
- **什么是密码字典？** 一个将文件路径映射到其密码的键值存储。  
- **为什么使用 GroupDocs.Redaction？** 它在一个 API 中集成了编辑和密码管理。  
- **我需要许可证吗？** 试用版可用于测试；生产环境需要完整许可证。  
- **我可以索引大型文件夹吗？** 可以——只需确保管理好字典的大小。  
- **是否支持 .NET Core？** 当然，GroupDocs.Redaction 支持 .NET Core 及更高版本。  

## GroupDocs 中的密码字典是什么？
密码字典是一个简单的内存中或磁盘上的集合，用于将每个文档的位置与其打开密码关联。GroupDocs.Search 在索引期间读取此字典，从而能够自动打开加密文件。

## 为什么要在 .NET 中创建密码字典？
创建密码字典可以集中凭证管理，减少重复代码，并实现批量操作，例如在多个受保护文件中搜索，而无需每次手动指定密码。

## 先决条件
- **Libraries**: `GroupDocs.Search` 和 `GroupDocs.Redaction` NuGet 包。  
- **Environment**: .NET Core 3.1+（或 .NET 6/7）。  
- **Knowledge**: 基础 C# 和文件 I/O 概念。

## 为 .NET 设置 GroupDocs.Redaction

### 安装包
**使用 .NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console（Visual Studio）**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet 包管理器 UI**
- 搜索 “GroupDocs.Redaction” 并安装最新版本。

### 获取许可证
- **Free Trial:** 开始使用临时试用许可证以探索功能。  
- **Purchase:** 超出试用期后继续使用，请考虑购买完整许可证。详细说明可在其 [purchase page](https://purchase.groupdocs.com/temporary-license/) 找到。

### 初始化和设置
```csharp
using GroupDocs.Redaction;

// Basic initialization of the Redactor
RedactorSettings settings = new RedactorSettings();
var redactor = new Redactor("path/to/document.pdf", settings);
```

现在环境已准备就绪，让我们深入核心实现。

## 如何在 .NET 中创建密码字典

### 步骤 1：初始化索引
```csharp
using GroupDocs.Search;
using System.IO;

string indexFolder = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Index");
Index index = new Index(indexFolder);
```
*说明：* 我们创建一个 `Index` 对象，用于保存我们的密码字典和其他搜索元数据。

### 步骤 2：清除现有密码（如果有）
```csharp
if (index.Dictionaries.DocumentPasswords.Count > 0)
{
    index.Dictionaries.DocumentPasswords.Clear();
}
```
*说明：* 删除过期条目可确保干净的起始状态，防止意外使用旧密码。

### 步骤 3：向字典添加密码
```csharp
string key1 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "English.docx"));
index.Dictionaries.DocumentPasswords.Add(key1, "123456");
```
*说明：* 这将文档路径（`key1`）映射到其密码（`"123456"`）。对每个受保护文件重复此步骤。

### 步骤 4：检索并移除密码
```csharp
if (index.Dictionaries.DocumentPasswords.Contains(key1))
{
    string password = index.Dictionaries.DocumentPasswords.GetPassword(key1);
    index.Dictionaries.DocumentPasswords.Remove(key1);
}
```
*说明：* 当需要时可以获取存储的密码，并在文档不再需要访问时 **从字典中移除密码**。

## 如何向字典添加多个密码
```csharp
string key2 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "English.docx"));
index.Dictionaries.DocumentPasswords.Add(key2, "123456");
string key3 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Lorem ipsum.docx"));
index.Dictionaries.DocumentPasswords.Add(key3, "123456");
```
*说明：* 一次添加多个条目可让您批量管理许多文件的访问权限。

## 如何使用密码索引文档
```csharp
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
index.Add(documentsFolder);
```
*说明：* `Add` 方法读取每个文件，自动使用字典中的密码，并构建可搜索的索引。

## 如何在已索引的受密码保护的文档中搜索
```csharp
string query = "ipsum OR increasing";
SearchResult result = index.Search(query);
```
*说明：* 索引完成后，您可以对所有文档运行常规搜索查询，无论其是否加密。

## 常见问题及解决方案
- **密码未应用** – 验证用作字典键的文件路径是否与实际文件位置完全匹配（使用 `Path.GetFullPath`）。  
- **大型字典影响性能** – 定期清除未使用的条目，并在字典变得非常大时考虑将其持久化到轻量级数据库。  
- **许可证错误** – 确保在应用程序启动时正确引用您的试用或完整许可证文件。

## 常见问答

**问：我可以免费使用 GroupDocs.Redaction 吗？**  
**答：** 您可以使用临时试用许可证开始。若需长期使用，需要购买完整许可证。

**问：如何高效处理大型文档集？**  
**答：** 使用高效的索引和内存管理实践，以有效处理更大的数据集。

**问：GroupDocs.Redaction 是否兼容所有 .NET 版本？**  
**答：** 是的，它支持最新的 .NET Core 版本。请始终检查兼容性更新。

**问：我可以无缝搜索受密码保护的文档吗？**  
**答：** 可以，一旦使用密码进行索引，您就可以使用 GroupDocs.Search 进行搜索，毫无问题。

**问：在设置 GroupDocs.Redaction 时有哪些常见的故障排除技巧？**  
**答：** 确保您的许可证已激活，且文档目录的路径正确指定。有关更多帮助，请参阅 [support forum](https://forum.groupdocs.com/)。

## 结论
通过遵循上述步骤，您现在了解如何 **创建 .NET 密码字典**，以及在适当时 **从字典中移除密码**。此方法集中管理凭证，提升安全性，并实现对加密文件的强大搜索。探索与云存储或文档管理系统的进一步集成，以扩展您的解决方案。

---

**最后更新：** 2026-04-05  
**测试环境：** GroupDocs.Redaction 23.2 for .NET  
**作者：** GroupDocs