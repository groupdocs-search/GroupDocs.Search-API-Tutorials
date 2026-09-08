---
date: '2026-07-31'
description: 了解如何通过使用 GroupDocs.Search 将文档添加到索引，并使用字符替换在索引期间规范化文本，以实现 case insensitive
  search java。
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Case insensitive search java 允许您将文档添加到索引并进行查询，而无需担心字母大小写。本指南展示了 GroupDocs.Search
  如何在索引期间规范化文本，以实现快速、可靠的结果。
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Case Insensitive Search Java – 使用 GroupDocs 索引文档
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: 在 Java 中将文档添加到索引以实现 Case‑Insensitive Search
type: docs
url: /zh/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

## 快速答案
- **“add documents to index” 是什么意思？** 它指将源文件加载到可搜索的数据结构中，以便以后进行查询。  
- **为什么使用字符替换？** 它会对每个字符进行规范化——通常转换为小写——从而使搜索自动忽略大小写差异。  
- **我需要许可证吗？** 免费试用可用于开发；生产部署需要完整许可证。  
- **需要哪个 Java 版本？** Java 8 或更高版本；该库针对 Java 11+ 以获得最佳性能。  
- **需要时可以切换为区分大小写的搜索吗？** 可以——搜索选项允许您在每个查询中切换大小写敏感性。

## 在 GroupDocs.Search 中，“add documents to index” 是什么？
将您的源文件（PDF、DOCX、TXT 等）加载到可搜索的索引中，以便引擎能够快速检索。将文档添加到索引会解析每个文件，提取纯文本，并将其存储在优化的数据结构中，从而实现快速查找。

## 为什么在索引期间启用字符替换？
字符替换在构建索引时将每个字符转换为预定义的等价字符——最常见的是小写。这样可以确保大小写、变音符或特定语言符号的差异不会影响搜索结果。通过在索引时对文本进行规范化，引擎能够在一致的标记集合上匹配查询，提供快速、可靠的不区分大小写行为，而无需在每次搜索时进行额外处理。

## 前置条件
- **GroupDocs.Search for Java** 版本 25.4 或更新（库支持 30 多种文件格式，能够在不将整个文件加载到内存的情况下索引数百页的文档）。  
- **Java Development Kit (JDK)** 8 或更高版本已安装。  
- 基本了解 **Maven**（或能够手动添加 JAR）。

## 为 Java 设置 GroupDocs.Search

### Maven 设置
将 GroupDocs 仓库和依赖添加到您的 `pom.xml` 中：

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
如果您不想使用 Maven，可从官方网站获取最新 JAR： [GroupDocs.Search for Java 发布](https://releases.groupdocs.com/search/java/)。

### 许可证获取
- **免费试用** – 下载试用许可证以开始实验。  
- **临时许可证** – 从 GroupDocs 门户请求延长的测试许可证。  
- **完整许可证** – 当您准备上线时购买生产许可证。

### 基本初始化（创建索引）
以下代码片段创建索引文件夹并启用字符替换：

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## 实施指南

### 在索引设置中启用字符替换
激活此功能会告诉引擎在索引时替换字符，这是实现不区分大小写行为的核心步骤。

#### 步骤 1：配置 `IndexSettings`
`IndexSettings` 是控制索引如何存储和处理文本的配置对象。将 `useCharacterReplacements` 设置为 **true** 即可开启自动小写（或您提供的任何自定义映射）。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### 配置字符替换
将每个字符映射到其小写对应字符（或您需要的任何自定义映射）。

#### 步骤 2：定义并添加替换对
替换字典保存诸如 `'A' → 'a'`、`'É' → 'e'` 等对。将在索引前添加这些对，以确保每个标记都已规范化。

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### 索引文档
现在索引已准备就绪，您可以从任意文件夹 **add documents to index**。

#### 步骤 3：添加文档进行索引
GroupDocs.Search 扫描目标目录，从每种受支持的文件类型中提取文本，应用替换映射，并将标记写入索引存储。

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### 执行区分大小写的搜索（可选）

#### 步骤 4：执行区分大小写的搜索
`SearchOptions` 配置查询行为，例如切换大小写敏感性，允许对搜索执行方式进行细粒度控制。  
`SearchOptions.setUseCaseSensitiveSearch(true)` 强制引擎在特定查询期间将大小写字符视为不同，从而覆盖默认的不区分大小写行为。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## 实际应用
1. **营销活动** – 规范化产品名称，使销售团队能够在不考虑大小写的情况下定位资产。  
2. **客户支持** – 为帮助台搜索框提供动力，无论用户输入 “login” 还是 “Login”，都能返回正确的文章。  
3. **电子商务目录** – 确保购物者无论如何输入产品标题都能找到商品，提高转化率。

## 性能考虑因素
- **组织源文件** – 整洁的文件夹层次结构可减少在 **add documents to index** 步骤中扫描所花费的时间。  
- **监控内存** – 索引大型语料库可能消耗大量内存；将文件分批（每批 500 – 1 000 项）处理可保持堆内存使用在可控范围。  
- **异步索引** – 若支持，可在后台线程运行索引，以保持 UI 响应并避免阻塞用户操作。

## 常见问题与故障排除

| 症状 | 可能原因 | 解决方案 |
|---------|--------------|-----|
| 已知词汇未返回结果 | 未启用字符替换 | 验证 `settings.setUseCharacterReplacements(true)` 并确保替换映射包含所需字符。 |
| 索引期间出现内存不足错误 | 一次索引过多大型文件 | 将文件分成更小批次索引或增加 JVM 堆内存（`-Xmx4g`）。 |
| 搜索意外返回区分大小写的结果 | `SearchOptions.setUseCaseSensitiveSearch(true)` 被设置 | 移除或设为 `false` 以恢复默认的不区分大小写行为。 |
| 索引加载时间超出预期 | 文件夹布局低效或未使用 SSD | 重新组织文件，清理未使用的文档，并将索引存储在高速 SSD 上。 |
| 特殊字符被忽略 | 替换映射缺少 Unicode 条目 | 为诸如 “é”、 “ß”、 “ø” 等字符添加映射到所需等价字符。 |

## 常见问答

**问：在索引期间如何处理特殊字符（例如 “é”、 “ß”）？**  
**答：** 将这些字符包含在替换映射中，映射到它们的 ASCII 等价字符，或根据搜索需求保持不变。

**问：我可以将字符替换限制在特定语言吗？**  
**答：** 可以。在将其添加到字典之前，构建仅包含目标语言字符的自定义替换数组。

**问：如果索引加载时间过长该怎么办？**  
**答：** 优化文件夹结构，删除不必要的文件，并将索引存储在高速 SSD 上。增量索引也可降低加载开销。

**问：索引后能否撤销字符替换？**  
**答：** 不能。替换已嵌入索引数据中；若要更改必须使用新设置重新构建索引。

**问：在哪里可以找到更详细的 API 文档？**  
**答：** 官方文档和 API 参考提供了详尽的细节（见下方资源）。

## 资源
- [文档](https://docs.groupdocs.com/search/java/)
- [API 参考](https://reference.groupdocs.com/search/java)
- [下载 GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub 仓库](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [免费支持论坛](https://forum.groupdocs.com/c/search/10)
- [临时许可证信息](https://purchase.groupdocs.com/temporary-license/) 

---

**最后更新：** 2026-07-31  
**测试环境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

---

## 相关教程

- [GroupDocs.Search Java 中的字符替换：提升文本搜索和索引的综合指南](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [将文档添加到索引：使用 GroupDocs 的区分大小写 Java 搜索](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [如何使用 GroupDocs.Search for Java 将文档添加到索引](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)