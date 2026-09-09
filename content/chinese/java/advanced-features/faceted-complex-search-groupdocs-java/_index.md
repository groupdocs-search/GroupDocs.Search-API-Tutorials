---
date: '2026-08-26'
description: 了解 Java 布尔运算符如何帮助您构建高速搜索索引、执行内容搜索（Java），并使用 GroupDocs.Search 运行分面查询。
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: 了解 Java 布尔运算符如何帮助您构建高速搜索索引、执行内容搜索（Java）并使用 GroupDocs.Search 执行分面查询。
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Java 布尔运算符 – 构建搜索索引和分面搜索
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Java 布尔运算符 – 创建搜索索引和分面搜索
type: docs
url: /zh/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# 布尔运算符 Java – 创建搜索索引和分面搜索

实现强大的 **search experience** 在 Java 中可能让人感到压力山大，尤其是当你需要 **create a search index Java** 来支持用于分面和复杂查询的 **boolean operators Java** 时。在本教程中，我们将演示如何设置 **GroupDocs.Search for Java**，构建索引、添加文档，并创建简单的分面搜索和使用布尔逻辑的复杂多条件查询。结束时，你将了解如何利用 **content search Java**、**filename search Java**，甚至 **update index Java** 操作来保持数据的最新。

## 快速答案
- **What is a faceted search?** 通过预定义的类别（如文件类型或日期）来过滤结果的一种方式。  
- **How do I create a search index Java?** 初始化指向文件夹的 `Index` 对象并添加文档。  
- **Can I combine multiple criteria with boolean operators?** 是的——使用基于对象的查询或文本查询中的 Boolean 运算符。  
- **Do I need a license?** 免费试用可用于开发；商业许可证可消除限制。  
- **Which IDE works best?** 任意 Java IDE（IntelliJ IDEA、Eclipse、NetBeans）均可良好工作。

## 什么是 “create search index java”？

创建搜索索引 Java 意味着构建一个基于磁盘的结构，用于存储文档文本和元数据，从而通过查询实现对匹配文档的即时检索。索引将词项映射到文档标识符，支持快速查找，并且可以在文件更改时增量更新，为强大的搜索功能提供基础。

## 为什么在分面和复杂查询中使用 GroupDocs.Search？

GroupDocs.Search for Java 提供内置的分面、Boolean 查询支持以及高性能索引，能够处理多达 1000 万文档，同时在典型服务器硬件上保持查询延迟低于 200 ms。它提供开箱即用的字段过滤、丰富的查询语言和纯 Java 兼容性，使其成为企业级搜索场景的理想选择。

## 前置条件

- **JDK 8 或更高版本** 已在你的 IDE 中安装并配置。  
- **Maven**（或 Gradle）用于依赖管理。  
- **GroupDocs.Search for Java** ≥ 25.4。  
- 基本熟悉 Java 面向对象概念和 Maven 项目结构。

## 设置 GroupDocs.Search for Java

### Maven 设置
将仓库和依赖添加到你的 `pom.xml` 文件中：

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
或者，从官方发布页面下载最新的 JAR：

[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### 获取许可证
解锁全部功能：

1. **Free trial** – 适用于开发和测试的完美选择。  
2. **Temporary evaluation license** – 延长试用限制。  
3. **Commercial license** – 消除生产使用的所有限制。

### 基本初始化和设置
`Index` 类是表示存储在磁盘上的可搜索索引的核心组件。下面的代码片段展示了如何通过实例化 `Index` 类 **create a search index Java**：

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

索引准备好后，我们可以继续进行实际的分面和复杂查询。

## 如何使用 boolean operators java – 简单分面搜索

加载索引、添加文档并发出字段查询；两步模式让你在一次调用中检索分面计数和过滤结果。这种方法为用户提供了一种直观的方式，通过文件类型、作者或自定义元数据等类别缩小结果范围。

### 步骤 1：创建索引
首先，将 `Index` 指向用于存储索引文件的文件夹。

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### 步骤 2：向索引添加文档
告诉 GroupDocs.Search 你的源文档所在位置。所有支持的文件类型（PDF、DOCX、TXT 等）都会自动被索引。

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### 步骤 3：使用文本查询在 content 字段执行搜索
快速的文本查询按 `content` 字段过滤。语法 `content: Pellentesque` 将结果限制为正文中包含单词 *Pellentesque* 的文档。

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### 步骤 4：使用对象查询执行搜索
基于对象的查询提供细粒度控制。这里我们构建一个词查询，将其包装在字段查询中并执行。

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## 如何使用 boolean operators java – 复杂查询搜索

要执行复杂查询，需要使用 AND/OR/NOT 运算符组合多个字段条件，并可选地包含短语搜索。你可以使用字段查询指定每个条件，使用 Boolean 运算符嵌套它们，并通过提升（boosting）控制相关性，从而仅检索满足所有必需条件的最相关文档。

### 步骤 1：为复杂查询创建索引
复用相同的文件夹结构；你可以在简单和复杂场景之间共享同一索引。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### 步骤 2：使用文本查询执行搜索
以下查询查找文件名为 *lorem* **and** *ipsum* **or** 内容包含任意两个精确短语之一的文件。

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### 步骤 3：使用对象查询执行搜索
基于对象的构建方式与文本查询相对应，但提供类型安全和 IDE 辅助。

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## 分面与复杂搜索的实际应用

| 场景 | 分面如何帮助 | 示例查询 |
|----------|-------------------|---------------|
| **E‑commerce catalog** | 按类别、价格、品牌过滤 | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | 按案件编号、司法管辖区缩小范围 | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | 组合作者、出版年份、关键字 | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | 按文件类型和部门搜索 | `filetype: pdf AND department: HR` |

## 常见陷阱与故障排除

`SearchResult` 对象包含匹配查询的文档，并提供对其相关性分数和高亮片段的访问。  
`CommonFieldNames` 类定义了 API 中使用的标准字段名称，如 `Content` 和 `FileName`。

- **Empty results** – 验证文档是否已成功添加（`index.getDocumentCount()` 可帮助检查）。  
- **Stale index** – 添加或删除文件后，调用 `index.update()` 以 **update index java** 并保持索引同步。  
- **Incorrect field names** – 使用 `CommonFieldNames` 常量（`Content`、`FileName` 等）以避免拼写错误。  
- **Performance bottlenecks** – 对于巨大的集合，考虑启用 `index.setCacheSize()` 或为索引文件夹使用专用 SSD。  
- **Missing highlights** – 要 **highlight search results java**，通过 `SearchResult.getFragments()` 检索匹配的片段（此处未展示，但 API 中可用）。

## 常见问题

**Q: Can I use GroupDocs.Search with Spring Boot?**  
A: 当然可以。添加 Maven 依赖，将索引配置为 Spring Bean，并在需要搜索功能的地方注入它。

**Q: Does the library support custom metadata fields?**  
A: 是的——你可以在索引期间添加用户定义的字段，然后对其进行分面。

**Q: How large can the index grow?**  
A: 基于磁盘的索引可处理多达 1000 万文档；只需确保足够的存储空间并监控缓存设置。

**Q: Is there a way to rank results by relevance?**  
A: GroupDocs.Search 会自动为匹配项打分；你可以通过 `SearchResult.getDocument(i).getScore()` 获取分数。

**Q: What happens if I index encrypted PDFs?**  
A: 添加文档时提供密码：`index.add(filePath, password)`。

## 结论

现在，你应该已经能够熟练使用 GroupDocs.Search **create a search index Java**，添加文档，并使用 **boolean operators java** 构建简单的分面查询和复杂的 Boolean 搜索。这些功能使你能够在各种应用中提供快速、准确且用户友好的搜索体验——从电子商务平台到企业知识库。

准备好下一步了吗？探索 **GroupDocs.Search** 的高级功能，如 **highlighting**、**suggestions** 和 **real‑time indexing**，进一步提升应用的搜索能力。

---

**最后更新:** 2026-08-26  
**测试环境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs

## 相关教程

- [Wildcard Search Java with GroupDocs.Search – 高级功能](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [如何使用 GroupDocs.Search 更新 Index Java – 综合指南](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [如何实现 java 全文搜索：使用 GroupDocs.Search 创建索引目录](/search/java/indexing/groupdocs-search-java-create-index/)