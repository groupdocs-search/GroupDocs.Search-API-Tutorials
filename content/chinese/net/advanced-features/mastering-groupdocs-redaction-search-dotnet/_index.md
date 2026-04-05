---
date: '2026-04-05'
description: 学习如何使用 GroupDocs.Search 和 GroupDocs.Redaction 在 .NET 中创建搜索索引、向索引添加文档以及对查询中的特殊字符进行转义。
keywords:
- create search index .net
- add documents to index
- escape special characters query
title: 使用 GroupDocs Redaction 与 Search 在 .NET 中创建搜索索引
type: docs
url: /zh/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/
weight: 1
---

# 掌握 GroupDocs Redaction 与 Search 在 .NET 中的使用：高效文档管理与安全搜索

## 快速答案
- **“create search index .NET” 是什么意思？** 它指在磁盘上构建可搜索的数据结构，使您的 .NET 应用能够快速定位文档。  
- **哪个库负责脱敏？** GroupDocs.Redaction 从文档中删除或遮蔽敏感数据。  
- **如何将文档添加到索引？** 使用 `index.Add(yourFolderPath)` 自动导入文件。  
- **查询中需要转义特殊字符吗？** 是的——请转义 `&`、`|`、`(`、`)` 等字符，以避免解析错误。  
- **这种方法适用于大数据集吗？** 绝对可以；索引可以扩展并增量更新。

## 什么是 “create search index .NET”？
在 .NET 中创建搜索索引意味着构建一种持久化结构，将词汇映射到出现这些词汇的文档上。该索引能够实现快速全文搜索，无需在每次查询时扫描所有文件。

## 为什么将 GroupDocs.Search 与 GroupDocs.Redaction 结合使用？
- **安全第一：** 在展示搜索结果之前先对个人数据进行脱敏。  
- **性能：** 搜索索引经过优化以提升速度，而脱敏仅在需要时对原始文件执行。  
- **灵活性：** 两个库开箱即支持多种文件格式（PDF、DOCX、图像等）。

## 前置条件
- **GroupDocs.Search** 版本 21.8+  
- **GroupDocs.Redaction** for .NET（兼容版本）  
- .NET Core SDK 3.1 或更高版本  
- 包含待索引文档的文件夹  

## 为 .NET 设置 GroupDocs.Redaction
### 安装
```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

### 获取许可证
1. **免费试用** – 测试核心功能。  
2. **临时许可证** – 扩展试用限制。  
3. **正式许可证** – 解锁生产就绪功能。

### 基本初始化
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the file path of the document
Redactor redactor = new Redactor("path/to/document.pdf");
```

## 如何创建 search index .NET
以下是逐步演示，详细说明如何 **create search index .NET** 项目、配置特殊字符处理以及准备查询。

### 步骤 1：创建索引
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchForSpecialCharacters";

// Create an index at the specified path. The second parameter 'true' allows overwriting existing indexes.
Index index = new Index(indexFolder, true);
```
*此行创建物理索引文件夹并为文档导入做好准备。*

### 步骤 2：配置字符类型
```csharp
// Configure character types for '&' as a letter and '-' as a separator within the alphabet dictionary of the index.
index.Dictionaries.Alphabet.SetRange(new char[] { '&' }, CharacterType.Letter);
index.Dictionaries.Alphabet.SetRange(new char[] { '-' }, CharacterType.Separator);
```
*自定义字符处理可确保诸如 “rock&roll‑music” 的查询被正确解析。*

### 步骤 3：将文档添加到索引
```csharp
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index.
index.Add(documentsFolder);
```
*此处我们批量 **add documents to index**，使所有受支持的文件可被搜索。*

### 步骤 4：在查询中定义并转义特殊字符
```csharp
using System.Text;

string word = "rock&roll-music";
StringBuilder result = new StringBuilder();

// Replace separators with space characters in the query string.
for (int i = 0; i < word.Length; i++)
{
    char character = word[i];
    CharacterType characterType = index.Dictionaries.Alphabet.GetCharacterType(character);
    if (characterType == CharacterType.Separator)
    {
        result.Append(' ');
    }
    else
    {
        result.Append(character);
    }
}

// Escape special characters.
const string specialCharacters = "():\"&|!^~*?\\";
for (int i = result.Length - 1; i >= 0; i--)
{
    char c = result[i];
    if (specialCharacters.Contains(c.ToString()))
    {
        result.Insert(i, '\\');
    }
}

string query = result.ToString();
if (query.Contains(" "))
{
    query = "\"" + query + "\"";
}
```
*此代码块的 **escape special characters query** 逻辑确保搜索引擎正确解析输入。*

### 步骤 5：执行搜索查询
```csharp
// Perform the search using the prepared query string.
SearchResult searchResult = index.Search(query);
```
*`SearchResult` 对象现在包含所有匹配的文档，可用于后续处理或展示。*

## 实际应用
1. **法律文档管理** – 在数千份合同中定位条款，同时对个人数据进行脱敏。  
2. **医疗记录搜索** – 快速查找患者笔记，然后在共享前脱敏 PHI。  
3. **电子商务目录** – 通过对 SKU 代码和品牌名称进行自定义分词，实现强大的产品搜索。

## 性能考虑
- **索引刷新：** 当文件更改时重新运行 `index.Add()` 或使用增量更新。  
- **内存管理：** 完成后释放 `Index` 对象，尤其在高负载服务中。  
- **异步操作：** 将搜索调用包装在 `Task.Run` 中，以实现非阻塞 UI 或 API 响应。

## 常见问题及解决方案
| 问题 | 解决方案 |
|-------|----------|
| 查询包含 `&` 或 `-` 的词时没有返回结果 | 确保字符类型按 **步骤 2** 所示进行配置。 |
| 大型 PDF 导致高内存使用 | 启用流式模式 (`index.Options.UseStreaming = true`) 并批量处理结果。 |
| 脱敏未应用于搜索片段 | 先对原始文件进行脱敏，然后重新构建索引以反映已清理的内容。 |

## 常见问答

**Q: 如何在我的搜索索引中自定义字符处理？**  
A: 使用 `index.Dictionaries.Alphabet.SetRange()` 将字符标记为字母、分隔符或标点符号。

**Q: 我可以索引多种文档格式吗？**  
A: 可以——GroupDocs.Search 支持 PDF、Word、Excel、PowerPoint、图像等多种格式。

**Q: 在搜索查询中应如何处理特殊字符？**  
A: 遵循 **步骤 4：在查询中定义并转义特殊字符**，将分隔符替换为空格，并在保留符号前加反斜杠 (`\`)。

**Q: 搜索时会自动进行脱敏吗？**  
A: 脱敏是独立的步骤；您可以先对文档进行脱敏并重新构建索引，或在检索后对结果进行脱敏。

**Q: 我应该多久重建或更新一次索引？**  
A: 每当源文件更改时就更新索引；大多数环境中，夜间增量重建效果良好。

## 结论
现在，您已经拥有一份完整的、可投入生产的 **create search index .NET** 项目指南，能够集成强大的脱敏功能。通过配置字符处理、安全转义查询字符串并定期更新索引，您可以为任何文档密集型应用提供快速且安全的搜索体验。

---

**最后更新：** 2026-04-05  
**测试环境：** GroupDocs.Search 21.8+, GroupDocs.Redaction latest release  
**作者：** GroupDocs