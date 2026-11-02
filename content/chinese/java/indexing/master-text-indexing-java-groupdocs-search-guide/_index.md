---
date: '2026-11-02'
description: 了解如何在 Java 中使用 GroupDocs.Search 将文件夹添加到索引，配置高压缩，并运行快速全文查询。
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: 了解如何在 Java 中使用 GroupDocs.Search 将文件夹添加到索引，配置压缩，并执行快速全文搜索。适用于大型文档集。
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: 如何在 Java 中使用 GroupDocs.Search 将文件夹添加到索引
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: 如何在 Java 中使用 GroupDocs.Search 将文件夹添加到索引
type: docs
url: /zh/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# 如何使用 GroupDocs.Search 在 Java 中将文件夹添加到索引

如果您需要能够扩展到数百万文档的 **java full text search**，那么您来对地方了。在本教程中，您将学习如何使用 GroupDocs.Search **add folder to index**，配置高压缩存储，并运行闪电般快速的查询。完成后，您将拥有一个可直接嵌入任何 Java 项目的生产就绪方案。

## 快速答案
- **主要库是什么？** GroupDocs.Search for Java  
- **如何将文件夹添加到索引？** Use `index.add(folderPath)`  
- **我可以配置文本压缩吗？** Yes, via `TextStorageSettings(Compression.High)`  
- **需要哪个 Java 版本？** JDK 8 or higher  
- **在哪里获取试用许可证？** From the GroupDocs website or the repository page  

## 什么是 java full text search 以及它为何重要？

Java full text search 将原始文档转换为倒排索引，使得在数千个文件中对任何词语的检索能够在亚秒级完成。这一能力对于法律文库、研究图书馆以及企业知识库至关重要，因为用户期望即时得到结果。它还能提升现代应用的生产力。

## 为什么在 java full text search 中使用 groupdocs.search？

GroupDocs.Search 提供高吞吐量的索引和查询执行，同时内置高压缩功能。它支持 **50+ 输入和输出格式**——包括 PDF、DOCX、EML 和 HTML，并且能够在不将整个文件加载到内存的情况下处理数百页的文档，使得典型工作负载的内存占用保持在 200 MB 以下。

## 前置条件

- **GroupDocs.Search for Java** (version 25.4 or later) – 提供索引和搜索功能的核心库。  
- **JDK 8+** 已安装并配置 – SDK 所需的最低运行时。  
- **Maven** 用于依赖管理 – 简化将库添加到项目中。  
- 一个 IDE，例如 **IntelliJ IDEA** 或 **Eclipse** – 用于编写和调试 Java 代码。  

## 为 java 设置 GroupDocs.Search

### Maven 设置
Add the repository and dependency to your `pom.xml` file:

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

### 直接下载
或者，从 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下载最新版本。

#### 许可证获取
- **Free trial** – 在不做承诺的情况下探索所有功能。  
- **Temporary license** – 延长的测试期。  
- **Purchase** – 解锁完整的生产功能。  

### 基本初始化和设置
`Index` 是用于创建、打开和管理搜索索引的核心类。

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## 使用自定义压缩对文本建立索引

### 步骤 1：定义索引文件夹
选择一个用于存放索引文件的目录：

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### 步骤 2：配置索引设置
`TextStorageSettings` 配置文本在索引中的存储方式，包括压缩级别。`Compression` 是一个枚举，用于指定所需的压缩算法。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### 步骤 3：使用自定义设置创建索引
使用上述配置实例化索引：

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## 如何将文件夹添加到索引

`Index` 是表示可搜索索引的主要类。

加载已有索引（或创建新索引），然后在 `Index` 对象上调用 `add` 方法。`add` 操作会扫描提供的目录，从每个支持的文件中提取文本，并将其存储在压缩索引中，准备进行即时搜索。

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## 如何搜索已索引的文档

`SearchResult` 表示单个匹配项，包含文档路径和相关性。

定义一个搜索查询字符串，表示您想要定位的词或短语，然后在 `Index` 实例上调用 `search` 方法。该方法返回一个 `SearchResult` 对象集合，每个对象包含文档路径、相关性得分以及高亮匹配的片段。

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## 实际应用

在以下真实场景中，**java full text search** 大放异彩：

1. **Legal document management** – 案件文件的即时检索。  
2. **Academic research libraries** – 论文和学位论文的快速查找。  
3. **Enterprise knowledge bases** – 手册和常见问题的快速访问。  
4. **Content management systems** – 大型站点的高效内容发现。  
5. **Customer service archives** – 过去工单和聊天记录的快速搜索。  

## 性能考虑因素

- **Compression vs. speed**: 高压缩可节省高达 70 % 的磁盘空间，但会增加适度的索引开销；请针对您的数据量运行基准测试。  
- **Memory management**: 为大于 10 GB 的索引分配至少 2 GB 的堆内存，以避免 `OutOfMemoryError`。  
- **Index updates**: 使用 `index.add()` 增量添加新文档，并定期调用 `index.optimize()` 以保持索引紧凑。  
- **Query optimization**: 使用高级查询语法（通配符、邻近、模糊搜索）来缩小结果范围并降低响应时间。  

## 常见陷阱与专业提示

- **Pitfall:** 在批量添加后忘记调用 `index.optimize()`。  
  **Pro tip:** 每晚运行 `index.optimize()` 以保持索引紧凑。  

- **Pitfall:** 在大规模数据集上使用默认（低）压缩。  
  **Pro tip:** 在生产环境中切换到 `Compression.High` 以降低存储成本。  

- **Pitfall:** 在从网络共享添加文件时未处理 `IOException`。  
  **Pro tip:** 将 `index.add()` 包裹在 try‑catch 块中，并记录任何失败以供后续审查。  

## 常见问题解答

**Q: 什么是 GroupDocs.Search？**  
A: 它是一个强大的 Java 库，提供高级全文搜索功能，包括索引、压缩和复杂查询支持。

**Q: 如何使用 GroupDocs.Search 处理大规模数据集？**  
A: 启用高压缩 (`Compression.High`) 并定期提交更改以保持索引精简。同时，分配足够的堆内存（例如，对超过 20 GB 的索引分配 4 GB）。

**Q: 我可以将 GroupDocs.Search 集成到现有的企业系统中吗？**  
A: 可以，库可以嵌入任何基于 Java 的后端、REST 服务或微服务架构中。

**Q: 如果我的索引变得过时怎么办？**  
A: 使用 `index.add()` 方法追加新文件，使用 `index.delete()` 删除过时文件，如有需要，重新运行 `index.optimize()`。

**Q: 我可以在哪里获得帮助或支持？**  
A: 访问社区论坛 [GroupDocs forums](https://forum.groupdocs.com/c/search/10) 进行故障排除和获取最佳实践技巧。

## 其他资源

- 详细使用指南: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- 完整 API 参考: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- 保持对新功能的了解: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**最后更新:** 2026-11-02  
**测试环境:** GroupDocs.Search 25.4  
**作者:** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## 相关教程

- [Groupdocs Search Java 创建索引指南](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [精通 Groupdocs Search Java 索引管理指南](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java 全文搜索库 – 使用 GroupDocs.Search 优化索引](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)