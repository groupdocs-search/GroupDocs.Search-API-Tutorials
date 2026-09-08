---
date: '2026-07-21'
description: Create Boolean Query Java 教程展示了如何使用 GroupDocs.Search for Java 实现 boolean
  AND、OR、NOT 搜索，向 index 添加文档，并 boost 文档检索。
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Create Boolean Query Java 教程 step‑by‑step 解释如何使用 GroupDocs.Search
  for Java 构建 AND、OR、NOT 查询，向 index 添加文档，并提升检索性能。
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – 使用 GroupDocs.Search 掌握 Boolean 搜索
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 创建 Boolean 查询（Java）：使用 GroupDocs.Search for Java 掌握 Boolean 搜索
type: docs
url: /zh/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# 创建 Boolean Query Java：使用 GroupDocs.Search for Java 掌握布尔搜索

在海量文档集合中搜索可能像在大海捞针。**Create Boolean Query Java** 让您精确告诉引擎您需要的内容——包含 *both*（两个）词、*either*（任意）词，或 *exclude*（排除）不想要的词的文档。在本指南中，我们将演示如何设置 **GroupDocs.Search for Java**、将文档添加到索引，并构建强大的布尔查询，以提升您的 **document retrieval java** 工作流。完成后，您将能够仅用几行代码编写干净、可维护的 Java 布尔查询。

## 快速答案
- **什么是 boolean AND 查询？** 仅返回包含 *所有* 指定词的文档。  
- **OR 与 AND 有何区别？** OR 匹配包含 *任意* 词的文档，扩大结果集。  
- **何时使用 NOT？** 使用 NOT 过滤掉包含不需要词的文档。  
- **我需要许可证吗？** 免费试用可用于测试；生产环境需要商业许可证。  
- **需要哪个 Java 版本？** 支持 Java 8+；建议使用 JDK 11+。

## 什么是 **create boolean query java**？
`create boolean query java` 指在 Java 中构建搜索查询，使用 GroupDocs.Search API 将 AND、OR、NOT 等逻辑运算符组合起来。通过组装这些运算符，您可以精确控制哪些文档匹配，实现高级过滤、相关性调优和复杂搜索场景。

## 为什么使用 GroupDocs.Search for Java？
- **高性能** 在大型文档集上——它可以在标准服务器上一分钟内对 500 GB 文本进行索引和搜索。  
- **丰富的 API** 支持基于文本和基于对象的查询，让您选择适合架构的风格。  
- **内置语言支持**，支持 30 多种语言的词干提取、停用词和模糊匹配。  
- **易于集成**，使用 Maven 或直接下载 JAR，只需几行代码即可开始。

## 前置条件
- **GroupDocs.Search for Java**（v25.4 或更高）——请参阅下面的下载链接。  
- 已安装 JDK 8+ 并在 IDE（IntelliJ IDEA、Eclipse 等）中配置。  
- 基本的 Java 知识以及用于依赖管理的 Maven。

## 设置 GroupDocs.Search for Java

### Maven 设置
将仓库和依赖添加到您的 `pom.xml`：

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
另外，您可以从官方网站下载最新的 JAR：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 获取许可证
先使用免费试用许可证探索所有功能。生产环境请购买商业许可证以解锁全部功能。

### 基本初始化和设置
创建索引文件夹并实例化 `Index` 对象：

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## 如何创建 boolean query java？
`Index` 类表示存储在磁盘上的可搜索文档集合。`BooleanQuery` 将多个子查询通过逻辑运算符组合。`createAndQuery`、`createOrQuery` 和 `createNotQuery` 分别构建 AND、OR、NOT 子查询。加载或创建 `Index` 实例，添加文档后，使用 `createAndQuery`、`createOrQuery` 或 `createNotQuery` 构建 `BooleanQuery` 对象。调用 `index.search(query)` 检索匹配文档。此模式适用于简单和复杂场景，仅需三步：索引初始化、文档添加、查询执行。

## Boolean AND 搜索

### 概述
AND 查询缩小结果范围，在需要匹配多个条件的文档时提升相关性。

### 实现步骤

1. **Initialize Index** – this also demonstrates **add documents to index** for the AND scenario.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – using the plain string syntax.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – useful when building queries programmatically (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Boolean OR 搜索

### 概述
OR 查询非常适合探索性搜索，能够捕获包含多个关键字中任意一个的文档（**search with or java**）。

### 实现步骤

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Boolean NOT 搜索

### 概述
NOT 查询帮助您剔除不相关的文档，例如过滤掉竞争对手的品牌名称（**boolean search examples java**）。

### 实现步骤

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## 复杂布尔查询

### 概述
复杂查询让您模拟真实的搜索场景，例如“查找积极的体育文章，但排除任何特定运动员的提及”。

### 实现步骤

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## **java boolean and or** 查询的实际应用
- **文档管理系统** – 定位同时包含 “confidential” **AND** “renewal” 的合同。  
- **法律研究** – 使用 **AND** / **OR** 过滤案例法，并使用 **NOT** 排除过时的法规。  
- **客户支持** – 检索提到 “login” **AND** “error” 但不包含 “resolved” 的工单。  
- **内容策划** – 收集关于 “cloud” **OR** “serverless” 的博客文章用于简报。

## 常见陷阱与故障排除

- **缺少索引刷新** – 添加新文档后，调用 `index.update()` 以确保它们可被搜索。  
- **运算符间距错误** – GroupDocs.Search 期望运算符（`AND`、`OR`、`NOT`）两侧有空格。  
- **大小写敏感性** – 查询默认不区分大小写，但自定义分析器可能会影响此行为。  
- **大结果集** – 使用分页（`search(query, 0, 100)`）以避免内存超载。  

## 常见问题

**Q: 可以在 AND 查询中组合超过两个词吗？**  
A: 当然可以。您可以使用 `createAndQuery` 链接多个 `createWordQuery` 对象，或直接在文本查询中写 `"term1 AND term2 AND term3"`。

**Q: GroupDocs.Search 支持通配符或模糊搜索吗？**  
A: 支持。使用 `*` 进行通配符（例如 `promot*`），或使用 `~` 进行模糊匹配（例如 `comfort~`）。

**Q: 如何将搜索限制在特定文件类型？**  
`FileTypeQuery` 限制搜索结果仅包含特定文件格式，如 PDF 或 DOCX。  
A: 使用 `FileTypeQuery` 类将结果限制为 PDF、DOCX 等，并将其与布尔查询组合。

**Q: 监控索引性能的最佳方式是什么？**  
A: 启用内置日志记录器 (`index.getLogger().setLevel(Level.INFO)`) 并在每次 `add` 操作后查看时间指标。

**Q: 有办法提升某些词的相关性吗？**  
`BoostQuery` 提升搜索查询中指定词的相关性得分。  
A: 可以。将重要词语用 `BoostQuery` 包裹，以在评分算法中增加其权重。

---

**最后更新：** 2026-07-21  
**测试版本：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs

## 相关教程

- [Java 布尔运算符 – 创建搜索索引与分面搜索](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [精通 GroupDocs.Search Java：高效文档搜索与索引管理](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - 精通 GroupDocs.Search Java – 创建与管理搜索索引](/search/java/indexing/groupdocs-search-java-create-index-guide/)