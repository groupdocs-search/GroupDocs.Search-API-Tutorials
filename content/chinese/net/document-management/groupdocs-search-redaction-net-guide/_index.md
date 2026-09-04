---
date: '2026-04-27'
description: 学习如何在 .NET 中使用 GroupDocs.Search 和 Redaction 对敏感数据进行编辑，并了解如何将文档添加到索引以搜索大型文档。
keywords:
- redact sensitive data
- add documents to index
- search large documents
title: GroupDocs.Search 与 .NET 中的脱敏 – 敏感数据脱敏
type: docs
url: /zh/net/document-management/groupdocs-search-redaction-net-guide/
weight: 1
---

# GroupDocs.Search 与 Redaction 在 .NET 中 – 敏感数据编辑

管理海量文档可能令人望而生畏，尤其是当您需要 **编辑敏感数据** 同时仍提供快速搜索功能时。本指南将演示如何设置 GroupDocs.Search 与 GroupDocs.Redaction，展示如何 **将文档添加到索引**，执行高效的 **搜索大型文档** 操作，并确保所有内容符合隐私要求。

## 快速答案
- **“编辑敏感数据”是什么意思？** 它表示永久删除或遮蔽文档中的机密信息。  
- **我需要哪些库？** GroupDocs.Search 和 GroupDocs.Redaction for .NET（可通过 NuGet 获取）。  
- **我可以自动索引 .NET 项目吗？** 可以——请参阅 “如何索引 .NET” 部分获取分步指南。  
- **我该如何处理超大文件？** 使用基于块的搜索将数据分成可管理的部分进行处理。  
- **生产环境需要许可证吗？** 生产使用需要有效的 GroupDocs 许可证；提供免费试用。

## 什么是编辑敏感数据？
编辑敏感数据是指永久删除或遮蔽文档中的个人、财务或机密信息，使其无法被未授权用户恢复或查看。

## 为什么将 GroupDocs.Search 与 Redaction 结合使用？
- **速度：** 构建可在毫秒内返回结果的可搜索索引。  
- **安全性：** 在文档共享或存储之前应用编辑规则。  
- **可扩展性：** 块搜索让您在不耗尽内存的情况下处理 TB 级文本。  
- **合规性：** 通过确保机密数据不泄露，满足 GDPR、HIPAA 等法规要求。

## 先决条件
- .NET 开发环境（推荐使用 Visual Studio）。  
- 基础 C# 知识。  
- 可访问 NuGet 以安装所需的包。

## 在 .NET 中设置 GroupDocs.Redaction

### 通过 .NET CLI 安装
```bash
dotnet add package GroupDocs.Redaction
```

### Package Manager 安装
```powershell
Install-Package GroupDocs.Redaction
```

### NuGet 包管理器 UI
搜索 **"GroupDocs.Redaction"** 并安装最新版本。

### 获取许可证的步骤
- **免费试用：** 开始免费试用以探索功能。  
- **临时许可证：** 请求临时许可证以获得更长的访问期限。  
- **购买：** 考虑购买以用于长期生产环境。

### 基本初始化和设置
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## 实现指南

### 如何使用 GroupDocs.Search 索引 .NET 项目
下面我们将实现过程分解为清晰的编号步骤，便于您轻松跟随。

#### 步骤 1：指定索引文件夹
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*Why?* 定义专用文件夹可使索引保持组织有序，并与原始文档隔离。

#### 步骤 2：创建并配置索引
```csharp
Index index = new Index(indexFolder);
```
*Purpose:* 在您指定的位置实例化一个新的可搜索索引。

#### 步骤 3：**将文档添加到索引**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*Explanation:* 每次调用都会将文件（或文件夹）添加到索引，使其内容可搜索。

### 使用块搜索搜索大型文档
块搜索让您将大型文件拆分为更小的块，从而保持低内存使用。

#### 步骤 1：定义搜索查询
```csharp
string query = "invitation";
```
*Purpose:* 您在所有已索引文件中寻找的词语。

#### 步骤 2：配置块搜索选项
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*Explanation:* 启用 `IsChunkSearch` 告诉引擎以块方式处理数据。

#### 步骤 3：执行初始搜索
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*Result:* 显示包含该词的文档数量以及找到的总出现次数。

#### 步骤 4：继续处理后续块
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*Why this loop?* 它确保您从每个块检索结果，直至处理完整数据集。

### 如何使用 GroupDocs.Redaction 编辑敏感数据
定位到需要保护的信息后，应用编辑规则。

#### 步骤 1：初始化编辑设置
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### 步骤 2：应用编辑
使用 `Redactor` 类（此处未显示以保持原始代码完整）来定义您想要遮蔽的模式、文本或图像。  
*Pro tip:* 在文档副本上先测试编辑规则，以避免意外的数据丢失。

## 实际应用
这些功能在多个行业中大放异彩：

1. **法律文档管理** – 快速搜索案件文件，同时编辑客户机密细节。  
2. **医疗数据处理** – 保护患者 PHI，同时让临床医生查找相关记录。  
3. **金融审计** – 索引海量交易日志并编辑账户号码或个人标识信息。

## 性能考虑因素
- **优化索引：** 仅对已更改的文件重新索引，以保持索引新鲜且避免不必要的工作。  
- **管理资源：** 根据服务器内存调整块大小 (`options.ChunkSize`)。  
- **异步操作：** 对于大批量，使用异步索引以保持 UI 响应。

## 常见问题

**Q: 如何高效处理大文件？**  
A: 使用基于块的搜索 (`IsChunkSearch = true`) 将数据分成更小的块处理，降低内存压力。

**Q: GroupDocs.Redaction 能处理加密文档吗？**  
A: 可以——先解密文件，应用编辑，然后如有需要再重新加密。

**Q: 有哪些许可证选项？**  
A: 免费试用、用于评估的临时许可证，以及用于生产的完整商业许可证。

**Q: 如何排查索引错误？**  
A: 确认索引文件夹路径正确，确保应用具有读写权限，并检查所有文档格式是否受支持。

**Q: 能进一步自定义搜索查询吗？**  
A: 当然。您可以使用 `SearchOptions` API 结合布尔运算符、通配符和邻近搜索。

## 资源
- **文档：** [GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **API 参考：** [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)  
- **下载：** [Latest Releases](https://releases.groupdocs.com/search/net/)  
- **免费支持：** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **临时许可证：** [Request Here](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-04-27  
**测试环境：** GroupDocs.Search 23.9 and GroupDocs.Redaction 23.9 for .NET  
**作者：** GroupDocs