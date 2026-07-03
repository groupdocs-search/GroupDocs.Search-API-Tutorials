---
date: '2026-02-21'
description: 了解如何在 Java 中使用 GroupDocs.Search 将文档添加到索引，并通过基于块的搜索提升搜索性能，优化大型文档集的 Java
  搜索索引内存。
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: 在 Java 中使用基于块的搜索将文档添加到索引
type: docs
url: /zh/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# 使用基于块的搜索在 Java 中向索引添加文档

在现代应用中，需要快速 **add documents to index** 并随后执行快速的基于块的查询时，您希望使用一种能够在不耗尽内存的情况下扩展的解决方案。本教程将指导您设置 GroupDocs.Search for Java，添加多个文档文件夹，并配置引擎以 **increase search performance**，同时保持 **java search index memory** 使用受控。无论是对法律合同、支持工单还是研究论文进行索引，以下步骤都能提供可投入生产的实现。

## 快速答案
- **第一步是什么？** 创建搜索索引文件夹。  
- **如何包含多个文件？** 对每个文档文件夹使用 `index.add()`。  
- **哪个选项启用块搜索？** `options.setChunkSearch(true)`。  
- **我可以在第一个块之后继续搜索吗？** 是的，使用该 token 调用 `index.searchNext()`。  
- **我需要许可证吗？** 免费试用或临时许可证可用于开发；生产环境需要完整许可证。  

## 您将学习
- 如何在指定文件夹中创建搜索索引。  
- 从多个位置 **add documents to index** 的步骤。  
- 配置搜索选项以启用基于块的搜索。  
- 执行初始和后续的基于块的搜索。  
- 基于块的文档搜索在实际场景中的优势。  

## 前提条件
- **必需的库**：GroupDocs.Search for Java 25.4 或更高版本。  
- **环境设置**：已安装兼容的 Java Development Kit (JDK)。  
- **知识前提**：基本的 Java 编程和 Maven 使用经验。  

## 设置 GroupDocs.Search for Java
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

### 获取许可证
试用 GroupDocs.Search：

- **免费试用** – 在不作承诺的情况下测试核心功能。  
- **临时许可证** – 为开发提供延长访问。  
- **购买** – 用于生产的完整许可证。  

### 基本初始化和设置
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

## 如何向索引添加文档
现在索引已经存在，接下来的合乎逻辑的步骤是从文件所在位置 **add documents to index**。

### 1. 创建索引
**概述**：为搜索索引设置目录。

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. 向索引添加文档
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

### 3. 为块搜索配置搜索选项
通过调整 options 对象来启用基于块的搜索。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. 执行初始基于块的搜索
使用启用块的选项运行第一次查询。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. 继续基于块的搜索
迭代剩余块，直至搜索完成。

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 为什么使用基于块的搜索？
基于块的搜索将庞大的文档集合拆分为可管理的片段，降低内存压力并加快响应时间。尤其在以下情况下受益显著：

1. **法律团队** 需要在数千份合同中定位特定条款。  
2. **客户支持门户** 必须即时呈现相关的知识库文章。  
3. **研究人员** 在不将整个文件加载到内存的情况下筛选大量数据集。  

## 此方法如何 **提升搜索性能**
通过搜索较小的块而非整个文件，引擎能够：

- 及早跳过无关章节，减少 CPU 周期。  
- 仅在内存中保留活动块，从而直接降低 **java search index memory** 消耗。  
- 在多核机器上并行处理块，以获得更快的结果。  

## 管理 **java search index memory**
虽然基于块的搜索已经降低了内存占用，但您仍可进一步调优 JVM：

- 根据索引大小分配足够的堆内存（如 `-Xmx2g` 或更高）。  
- 在批量添加后使用 `index.optimize()` 压缩索引结构。  
- 使用 VisualVM 等工具监控 GC 暂停，以避免延迟峰值。  

## 性能考虑
- **内存管理** – 为大型索引分配足够的堆空间（`-Xmx`）。  
- **资源监控** – 在索引和搜索操作期间关注 CPU 使用率。  
- **索引维护** – 定期重建或清理索引，以丢弃过时数据。  

## 常见陷阱与故障排除

| 问题 | 发生原因 | 解决方案 |
|------|----------|----------|
| 索引期间的 `OutOfMemoryError` | 堆大小太小 | 增加 JVM 堆内存（`-Xmx2g` 或更高） |
| 未返回结果 | 块 token 未被处理 | 确保 `while` 循环运行至 `getNextChunkSearchToken()` 为 `null` |
| 搜索性能慢 | 索引未优化 | 在批量添加后运行 `index.optimize()` |

## 常见问答

**Q: 什么是基于块的搜索？**  
A: 基于块的搜索将数据集划分为更小的片段，使得在不将整个文档加载到内存的情况下，对大规模数据进行高效查询。

**Q: 如何使用新文件更新我的索引？**  
A: 只需使用新文档的路径调用 `index.add()`；索引会自动将其纳入。

**Q: GroupDocs.Search 能处理不同的文件格式吗？**  
A: 可以，它支持 PDF、DOCX、XLSX、PPTX 以及许多其他常见格式。

**Q: 常见的性能瓶颈是什么？**  
A: 内存限制和未优化的索引是最常见的；分配足够的堆内存并定期优化索引。

**Q: 在哪里可以找到更详细的文档？**  
A: 请访问官方的 [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) 获取深入指南和 API 参考。

**Q: 基于块的搜索能用于加密的 PDF 吗？**  
A: 可以，只要通过相应的 API 重载提供密码即可。

**Q: 我如何监控索引进度？**  
A: 使用返回 `Progress` 对象的 `Index.add()` 重载，或挂接日志回调。

## 资源
- **文档**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API 参考**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **下载**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免费支持**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **临时许可证**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最后更新：** 2026-02-21  
**测试环境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

---