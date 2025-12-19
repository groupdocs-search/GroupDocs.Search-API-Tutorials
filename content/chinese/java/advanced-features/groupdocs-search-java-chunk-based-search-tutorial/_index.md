---
date: '2025-12-19'
description: 学习如何使用 GroupDocs.Search 在 Java 中将文档添加到索引并启用基于块的搜索，以提升大文档集的性能。
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: 在 Java 中使用基于块的搜索将文档添加到索引
type: docs
url: /zh/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# 在 Java 中使用块级搜索将文档添加到索引

在当今数据驱动的世界中，能够快速 **将文档添加到索引** 并随后执行块级搜索，对于处理大量文件的任何应用程序都是必不可少的。无论您是处理法律合同、客户支持档案，还是庞大的研究文库，本教程将向您展示如何为 Java 设置 GroupDocs.Search，以便高效地索引文档并以块状方式检索相关信息。

## 您将学习的内容
- 如何在指定文件夹中创建搜索索引。  
- 从多个位置 **将文档添加到索引** 的步骤。  
- 配置搜索选项以启用块级搜索。  
- 执行初始和后续的块级搜索。  
- 块级文档搜索发挥优势的真实场景。  

## 快速答疑
- **第一步是什么？** 创建搜索索引文件夹。  
- **如何包含多个文件？** 对每个文档文件夹使用 `index.add()`。  
- **哪个选项启用块级搜索？** `options.setChunkSearch(true)`。  
- **我可以在第一个块之后继续搜索吗？** 可以，使用该 token 调用 `index.searchNext()`。  
- **我需要许可证吗？** 免费试用或临时许可证可用于开发；生产环境需要正式许可证。  

## 前置条件
要遵循本指南，请确保您具备：

- **必需库**：GroupDocs.Search for Java 25.4 或更高版本。  
- **环境设置**：已安装兼容的 Java Development Kit (JDK)。  
- **知识前置**：基本的 Java 编程和 Maven 使用经验。  

## 为 Java 设置 GroupDocs.Search
首先，使用 Maven 将 GroupDocs.Search 集成到项目中：

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

或者，从 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下载最新版本。

### 许可证获取
- **免费试用** – 在不作承诺的情况下测试核心功能。  
- **临时许可证** – 为开发提供延长访问。  
- **购买** – 用于生产的完整许可证。  

### 基础初始化与设置
在您希望存放可搜索数据的文件夹中创建索引：

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## 如何将文档添加到索引
索引已创建，接下来的合乎逻辑的步骤是从文件所在位置 **将文档添加到索引**。

### 1. 创建索引
**概述**：为搜索索引设置目录。

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. 将文档添加到索引
**概述**：从多个源文件夹导入文件。

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. 为块级搜索配置搜索选项
通过调整 options 对象来启用块级搜索。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. 执行初始块级搜索
使用已启用块级的选项运行首次查询。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. 继续块级搜索
遍历剩余块，直至搜索完成。

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 为什么使用块级搜索？
块级搜索将庞大的文档集合拆分为可管理的块，降低 **内存** 压力并加快响应时间。它在以下情况下尤为有益：

1. **法律团队** 需要在成千上万的合同中定位特定条款。  
2. **客户支持门户** 必须即时呈现相关的知识库文章。  
3. **研究人员** 在不将整个文件加载到内存的情况下筛选庞大的数据集。  

## 性能考虑因素
- **内存管理** – 为大型索引分配足够的堆空间（`-Xmx`）。  
- **资源监控** – 在索引和搜索操作期间关注 CPU 使用情况。  
- **索引维护** – 定期重建或清理索引，以丢弃过时数据。  

## 常见陷阱与故障排除
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` 在索引期间 | 堆大小过小 | 增加 JVM 堆大小（`-Xmx2g` 或更高）。 |
| 未返回结果 | 块 token 未被处理 | 确保 `while` 循环运行至 `getNextChunkSearchToken()` 为 `null`。 |
| 搜索性能慢 | 索引未优化 | 批量添加后运行 `index.optimize()`。 |

## 常见问题解答

**问：什么是块级搜索？**  
A: 块级搜索将数据集划分为更小的片段，使得在不将整个文档加载到内存的情况下，对大规模数据进行高效查询。

**问：如何使用新文件更新我的索引？**  
A: 只需使用新文档的路径调用 `index.add()`；索引会自动将其纳入。

**问：GroupDocs.Search 能处理不同的文件格式吗？**  
A: 是的，它支持 PDF、DOCX、XLSX、PPTX 以及许多其他常见格式。

**问：典型的性能瓶颈是什么？**  
A: 内存限制和未优化的索引是最常见的问题；请分配足够的堆空间并定期优化索引。

**问：在哪里可以找到更详细的文档？**  
A: 请访问官方的 [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) 获取深入的指南和 API 参考。

## 资源
- **文档**： [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API 参考**： [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **下载**： [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**： [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免费支持**： [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **临时许可证**： [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2025-12-19  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs