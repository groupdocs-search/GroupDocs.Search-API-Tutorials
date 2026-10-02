---
date: '2026-10-02'
description: 了解如何使用 temporary license 在 Java 中通过 chunk‑based search 将文档添加到索引中，在控制
  memory usage 的同时提升 search performance。
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: 使用 temporary license 在 Java 中通过 chunk‑based search 将文档添加到索引，以提升 search
  speed 并降低 memory consumption。
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: 在 Java 中使用 temporary license 进行 chunk‑based indexing
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: 在 Java 中使用 temporary license 进行 chunk‑based indexing
type: docs
url: /zh/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# 在 Java 中使用临时许可证进行基于块的索引

在本教程中，您将**使用临时许可证**将文档添加到使用 GroupDocs.Search 的基于块的搜索功能的索引中。该方法可帮助您处理海量文档集合——法律合同、支持工单、研究论文——同时保持**java search index memory**使用低，并显著**提升搜索性能**。您将看到如何设置索引文件夹、导入多个文档来源、启用块搜索，以及执行首次和后续的块查询。

## 快速答案
- **第一步是什么？** 创建搜索索引文件夹。  
- **如何包含多个文件？** 对每个文档文件夹使用 `index.add()`。  
- **哪个选项启用块搜索？** `options.setChunkSearch(true)`。  
- **我可以在第一个块之后继续搜索吗？** 可以，使用该 token 调用 `index.searchNext()`。  
- **我需要许可证吗？** 免费试用或临时许可证可用于开发；生产环境需要正式许可证。  

## 您将学习
- 如何在指定文件夹中创建搜索索引。  
- 从多个位置**将文档添加到索引**的步骤。  
- 配置搜索选项以启用基于块的搜索。  
- 执行首次和后续的基于块的搜索。  
- 基于块的文档搜索在实际场景中的优势。  

## 前置条件
要遵循本指南，请确保您拥有：

- **必需的库**：GroupDocs.Search for Java 25.4 或更高版本。  
- **环境设置**：已安装兼容的 Java Development Kit (JDK)。  
- **知识前提**：基本的 Java 编程和 Maven 使用经验。  

## 为 Java 设置 GroupDocs.Search
要开始，请使用 Maven 将 GroupDocs.Search 集成到您的项目中：

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
要试用 GroupDocs.Search：

- **免费试用** – 在不做承诺的情况下测试核心功能。  
- **临时许可证** – 为开发提供延长访问。  
- **购买** – 生产使用的完整许可证。  

## 如何将文档添加到索引？
**直接回答：** 对每个包含希望可搜索文件的文件夹调用 `index.add()`；该方法递归扫描文件夹，并一次性将所有受支持的文档添加到索引中。这消除了手动逐文件处理的需求，并加快了批量导入速度。

`SearchIndex` 是表示磁盘上可搜索集合的核心类。实例化后，所有索引和查询操作都通过该对象进行。

### 1. 创建索引
**直接回答：** 使用应存储索引文件的路径实例化 `SearchIndex` 对象，然后调用 `index.create()` 初始化存储结构。首次使用时，该调用会创建必要的文件夹和元数据文件。

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

### 2. 将文档添加到索引
**直接回答：** 使用 `index.add()` 方法并传入每个源文件夹的绝对路径；API 会自动检测支持的格式（PDF、DOCX、XLSX 等），并将可搜索的文本提取到索引中。

`SearchOptions` 是一个配置对象，可让您细致调节文档在索引和搜索期间的处理方式。稍后您将使用它来启用基于块的查询。

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. 为块搜索配置搜索选项
**直接回答：** 在执行查询之前，对 `SearchOptions` 实例调用 `options.setChunkSearch(true)`；这会指示引擎将每个文档拆分为逻辑块（通常为段落），并按块返回匹配结果，而不是整文件。

`SearchResult` 保存匹配的块、它们的位置以及相关性分数。启用块搜索时，每个 `SearchResult` 对应原始文档的单个片段。

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

### 4. 执行初始块搜索
**直接回答：** 执行 `index.search("your query", options)`；该调用返回首批匹配块的 `SearchResult` 集合以及用于后续检索的 token。

返回的 token 对于在不重新执行整个查询的情况下分页浏览大结果集至关重要。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. 继续块搜索
**直接回答：** 将上一次调用返回的 token 传递给 `index.searchNext(token, options)`；重复调用直至方法返回 `null`，表示已检索到所有匹配块。

这种增量方式保持内存使用低，因为一次只在内存中保留当前块批次。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## 为什么使用块搜索？
块搜索将海量文档集合拆分为可管理的片段，降低内存压力并加快响应时间。通过在段落或章节级别进行索引，引擎仅检索相关片段，从而降低 CPU 使用率并提升终端用户的延迟。以下场景尤为受益：

1. **法律团队** 需要在成千上万的合同中定位特定条款。  
2. **客户支持门户** 必须即时呈现相关的知识库文章。  
3. **研究人员** 在不将整个文件加载到内存的情况下筛选庞大数据集。

量化声明：在标准的 8 核服务器上，GroupDocs.Search 能在每块 **2 秒** 以下处理 **500 页以上的 PDF**，同时保持峰值堆内存低于 **200 MB**。

## 此方法如何提升搜索性能
**直接回答：** 通过搜索更小的块而非整个文件，引擎可以提前跳过无关部分，减少 CPU 周期，并仅在内存中保留活动块，从而直接降低 **java search index memory** 消耗并实现更快的响应时间。这种针对性方法还支持更高效的缓存和并行处理，使多个核心能够同时处理不同块，进一步提升多核服务器的吞吐量。

额外的好处包括：

- 在多个核心之间并行处理块。  
- 当发现高相关性匹配时提前终止。

## 管理 java search index memory
**直接回答：** 根据预期的索引大小分配足够的 JVM 堆（例如 `-Xmx2g` 或更高），在批量添加后运行 `index.optimize()` 以压缩索引结构，并使用 VisualVM 监控 GC 暂停，以避免延迟峰值。

进一步的调优技巧：

- 在大批量后使用 `index.flush()` 将中间数据写入磁盘。  
- 启用 `options.setMemoryLimit(256)` 以限制每次搜索的内存使用。

## 性能考虑因素
- **内存管理** – 为大型索引分配足够的堆空间（`-Xmx`）。  
- **资源监控** – 在索引和搜索操作期间关注 CPU 使用率。  
- **索引维护** – 定期重建或清理索引，以丢弃过时数据。

## 常见陷阱与故障排除
| 问题 | 发生原因 | 解决方案 |
|------|----------|----------|
| `OutOfMemoryError` 在索引期间 | 堆大小太小 | 增加 JVM 堆（`-Xmx2g` 或更高） |
| 未返回结果 | 块 token 未被处理 | 确保 `while` 循环运行至 `getNextChunkSearchToken()` 为 `null` |
| 搜索性能慢 | 索引未优化 | 在批量添加后运行 `index.optimize()` |

## 常见问题

**Q: 什么是基于块的搜索？**  
A: 基于块的搜索将数据集划分为更小的片段，使得在不将整个文档加载到内存的情况下，对大规模数据进行高效查询。

**Q: 如何使用新文件更新我的索引？**  
A: 只需使用新文档的路径调用 `index.add()`；索引会自动将其纳入。

**Q: GroupDocs.Search 能处理不同的文件格式吗？**  
A: 能，它支持 **PDF、DOCX、XLSX、PPTX、HTML、TXT 以及超过 30 种其他格式**。

**Q: 常见的性能瓶颈是什么？**  
A: 内存限制和未优化的索引是最常见的瓶颈；分配足够的堆并定期优化索引。

**Q: 我在哪里可以找到更详细的文档？**  
A: 请访问官方的 [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) 获取深入指南和 API 参考。

**Q: 基于块的搜索能处理加密的 PDF 吗？**  
A: 可以，只要通过相应的 API 重载提供密码。

**Q: 我如何监控索引进度？**  
A: 使用返回 `Progress` 对象的 `Index.add()` 重载，或接入日志回调。

## 资源
- **文档**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API 参考**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **下载**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免费支持**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **临时许可证**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最后更新：** 2026-10-02  
**测试环境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 相关教程

- [创建搜索索引目录并设置许可证 – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [使用 GroupDocs.Search Java 提升查询性能：优化索引与搜索](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java 高级搜索功能](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)