---
date: '2026-01-29'
description: 学习如何使用 GroupDocs.Search for Java 实现 Java 布尔 AND/OR 查询，向索引添加文档并提升文档检索效果。
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: Java 布尔与或：使用 GroupDocs.Search for Java 精通布尔搜索
type: docs
url: /zh/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or：使用 GroupDocs.Search for Java 掌握布尔搜索

在海量文档集合中搜索常常像大海捞针。使用 **java boolean and or** 查询，你可以精确告诉引擎你的需求——返回同时包含*两个*词的文档、包含*任意*词的文档，或*排除*不需要的词。在本指南中，我们将演示如何设置 **GroupDocs.Search for Java**、将文档添加到索引，以及构建强大的布尔查询，以提升你的 **document retrieval java** 工作流。

## 快速答案
- **What is a boolean AND query?** 仅返回包含*所有*指定词的文档。  
- **How does OR differ from AND?** OR 匹配包含*任意*词的文档，扩大结果集。  
- **When should I use NOT?** 使用 NOT 过滤掉包含不需要词的文档。  
- **Do I need a license?** 免费试用可用于测试；生产环境需要商业许可证。  
- **Which Java version is required?** 支持 Java 8+；推荐使用 JDK 11+。

## 什么是 **java boolean and or**？
**java boolean and or** 查询结合逻辑运算符（AND、OR、NOT）来细化搜索结果。通过构造查询，你可以明确告知 GroupDocs.Search 各词之间的关系，从而精确控制检索过程。

## 为什么使用 GroupDocs.Search for Java？
- **High performance** 在大规模文档集上表现出色。  
- **Rich API** 支持基于文本和基于对象的查询。  
- **Built‑in language support** 提供词干提取、停用词和模糊匹配。  
- **Easy integration** 可轻松集成 Maven 或直接下载 JAR。

## 前置条件
在开始之前，请确保已具备以下条件：

- **GroupDocs.Search for Java**（v25.4 或更高）——请参阅下方下载链接。  
- 已安装 JDK 8+ 并在 IDE（IntelliJ IDEA、Eclipse 等）中配置。  
- 基础的 Java 知识以及用于依赖管理的 Maven。

## 设置 GroupDocs.Search for Java

### Maven 设置
在你的 `pom.xml` 中添加仓库和依赖：

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
或者，从官方网站下载最新的 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 获取许可证
先使用免费试用许可证来体验全部功能。生产环境请购买商业许可证以解锁完整功能。

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

## java boolean and or：实现布尔搜索

下面我们将介绍 **AND**、**OR**、**NOT** 和 **complex** 查询。每个章节都会展示纯文本查询和等价的对象查询，方便你根据代码库选择合适的方式。

### 布尔 AND 搜索
使用 **AND** 组合词语，以仅检索包含*所有*关键字的文档。

#### 概述
AND 查询会缩小结果范围，在需要匹配多个条件的文档时提升相关性。

#### 实现步骤
1. **Initialize Index** – 这也演示了 **add documents to index** 在 AND 场景下的使用。  
```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**  
```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – 使用纯字符串语法。  
```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – 在程序化构建查询时很有用（**search with and java**）。  
```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### 布尔 OR 搜索
使用 **OR** 扩大结果范围，匹配任意提供的词语。

#### 概述
OR 查询适用于探索性搜索，旨在捕获包含多个关键词中任意一个的文档（**search with or java**）。

#### 实现步骤
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

### 布尔 NOT 搜索
使用 **NOT** 排除不需要的词，以过滤结果中的噪音。

#### 概述
NOT 查询帮助你剔除不相关的文档，例如过滤掉竞争对手的品牌名称（**boolean search examples java**）。

#### 实现步骤
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

### 复杂布尔查询
结合 **AND**、**OR** 和 **NOT**，构建复杂的搜索逻辑，以满足高度特定的检索需求。

#### 概述
复杂查询可以模拟真实的搜索场景，例如“查找积极的体育文章，但排除提及特定运动员的内容”。

#### 实现步骤
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

## java boolean and or 查询的实际应用
- **Document Management Systems** – 查找同时包含 “confidential” **AND** “renewal” 的合同。  
- **Legal Research** – 使用 **AND**/**OR** 过滤案例法，并通过 **NOT** 排除过时的法规。  
- **Customer Support** – 检索提及 “login” **AND** “error” 但不包含 “resolved” 的工单。  
- **Content Curation** – 收集关于 “cloud” **OR** “serverless” 的博客文章，用于通讯。

## 常见陷阱与故障排除
- **Missing Index Refresh** – 添加新文档后，调用 `index.update()` 以确保可搜索。  
- **Incorrect Operator Spacing** – GroupDocs.Search 需要在运算符周围留有空格（`AND`、`OR`、`NOT`）。  
- **Case Sensitivity** – 查询默认不区分大小写，但自定义分析器可能会影响此行为。  
- **Large Result Sets** – 使用分页（`search(query, 0, 100)`）以避免内存溢出。

## 常见问题

**Q: 我可以在 AND 查询中组合超过两个词吗？**  
A: 当然可以。你可以使用 `createAndQuery` 将多个 `createWordQuery` 对象串联，或者在文本查询中直接写 `"term1 AND term2 AND term3"`。

**Q: GroupDocs.Search 支持通配符或模糊搜索吗？**  
A: 支持。使用 `*` 表示通配符（例如 `promot*`），或使用 `~` 表示模糊匹配（例如 `comfort~`）。

**Q: 我如何将搜索限制在特定文件类型？**  
A: 使用 `FileTypeQuery` 类将结果限制为 PDF、DOCX 等，并将其与布尔查询组合使用。

**Q: 监控索引性能的最佳方式是什么？**  
A: 启用内置日志记录器（`index.getLogger().setLevel(Level.INFO)`），并在每次 `add` 操作后查看时间指标。

**Q: 有办法提升某些词的相关性吗？**  
A: 有。将重要词语用 `BoostQuery` 包裹，以在评分算法中提升其权重。

---

**最后更新：** 2026-01-29  
**测试环境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs