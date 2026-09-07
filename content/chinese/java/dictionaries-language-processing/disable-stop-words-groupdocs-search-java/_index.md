---
date: '2026-07-07'
description: 了解如何使用 GroupDocs.Search for Java 禁用 stop words java 并将文档添加到索引，从而提升搜索准确性和性能。
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: 使用 GroupDocs.Search for Java 禁用 stop words java 并将文档添加到索引。按照此 step‑by‑step
  指南提升查询准确性和性能。
og_title: 禁用 Stop Words Java – 使用 GroupDocs 将文档添加到索引
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: 禁用 Stop Words Java – 使用 GroupDocs 将文档添加到索引
type: docs
url: /zh/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# 禁用停用词 Java – 将文档添加到索引（使用 GroupDocs）

在本教程中，您将了解如何在使用 GroupDocs.Search for Java 将文件添加到可搜索索引时**禁用停用词 java**。通过关闭内置的停用词过滤器，所有标记——包括诸如 “on”、 “by” 或 “the” 等常见词——都可以被搜索，这显著提升了在法律合同、电子商务目录或技术手册等专业领域的结果相关性。

## 快速答案
- **“add documents to index” 是什么意思？** 它指将源文件加载到可搜索的索引中，以便高效查询。  
- **为什么我要禁用停用词？** 当这些词在您的领域中具有重要意义时，将常见词（例如 “on”、 “the”）包含在搜索中。  
- **需要哪个库版本？** GroupDocs.Search for Java 25.4 或更高版本。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要永久许可证。  
- **我可以在 Maven 项目中使用吗？** 可以——只需添加下面显示的仓库和依赖即可。

## 什么是搜索中的停用词，为什么可能想要禁用它们？

停用词是高频词，许多搜索引擎会自动过滤它们以加快查询处理。禁用它们可确保**每个词**——包括传统上被忽略的词——都贡献到搜索索引中，这在这些词具有特定领域含义时尤为重要。例如，在法律合同中，“by”可以区分当事方，而在产品目录中，“on”可能是型号名称的一部分。

## 将文档添加到索引在 GroupDocs.Search 中是如何工作的？

当您添加文档时，GroupDocs.Search 会读取每个文件，对内容进行分词，并将标记存储在优化的倒排索引中。即使是包含**数十万文件**的集合，也能实现亚秒级检索。该库还支持增量更新，您可以在不从头重建的情况下保持索引最新。

## 前置条件

- **必需的库**：GroupDocs.Search for Java 25.4（或更新版本）。  
- **开发环境**：IntelliJ IDEA、Eclipse 或您喜欢的任何 Java IDE。  
- **基础知识**：熟悉 Java 语法和索引概念。

## 设置 GroupDocs.Search for Java

### Maven 安装

如果您使用 Maven，请在 `pom.xml` 中加入以下内容：

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

#### 获取许可证的步骤
- **免费试用** – 立即开始测试。  
- **临时许可证** – 获取限时密钥以获得完整功能。  
- **购买** – 获得用于生产的永久许可证。

## 基本初始化和设置

IndexSettings 是一个配置类，定义了索引的构建方式、搜索方式以及启用的功能。

创建 `IndexSettings` 实例以控制索引的行为：

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## 如何在搜索中禁用停用词（Java）？

IndexSettings 是控制搜索索引行为的配置对象。默认情况下它启用了内置的停用词过滤器。要关闭此过滤器，请在 `IndexSettings` 实例上调用 `setUseStopWords(false)` 方法。此单一调用会禁用停用词移除，确保每个标记——包括诸如 “on” 或 “the” 等常见词——都被索引并可查询。

## 如何将文档添加到索引

将文档添加到索引的方式是使用所需的 `IndexSettings` 创建 `Index` 对象，然后对每个文件或文件夹调用其 `add` 方法。库会读取每个文档，对其内容进行分词，并将生成的词项存储在倒排索引中，使其立即可搜索。您可以将索引指向特定的输出目录，并指定包含待索引文件的源文件夹。

### 定义输出目录

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### 指定文档目录

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## 执行搜索查询

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

由于已启用 `disable stop words java`，包含词语 `"on"` 的查询将被评估，返回原本会被默认过滤器忽略的匹配项。

## 实际应用

1. **企业文档搜索** – 保留默认停用词列表会剥离的关键术语。  
2. **电子商务平台** – 通过对描述、型号和规格中的每个词进行索引，提高产品可发现性。  
3. **法律研究工具** – 捕获每个法律术语，即使是常被视为停用词的，也能避免遗漏关键条款。

## 性能考虑

- **优化技巧**：定期更新和修剪索引以保持搜索速度。GroupDocs.Search 能处理**多达 1 百万文档**，仍保持亚秒级查询时间。  
- **资源使用**：监控 JVM 堆大小；大型索引可能需要 4 GB 或更高的最大堆 (`-Xmx`)。  
- **Java 内存管理**：对超大语料库使用堆外存储选项，以将堆内占用保持在 2 GB 以下。

## 常见问题及解决方案

| 症状 | 可能原因 | 解决方案 |
|---|---|---|
| 常用词无结果 | `setUseStopWords(true)`（默认） | 如上所示，调用 `setUseStopWords(false)`。 |
| 索引期间内存不足错误 | 一次索引过多大型文件 | 分批索引文件；增加 `-Xmx` JVM 参数。 |
| 搜索返回过时数据 | 添加新文件后索引未刷新 | 调用 `index.update()` 或重新添加已更改的文档。 |

## 常见问答

**Q: 什么是停用词？**  
A: 停用词是常见术语（例如 “the”、 “is”、 “on”），许多搜索引擎会忽略它们以加快查询。禁用它们可让您将每个标记视为可搜索的。

**Q: 为什么在搜索索引中禁用停用词？**  
A: 当需要精确短语匹配——如在法律或技术文档中——每个词都有意义，因此需要包含停用词。

**Q: GroupDocs.Search 如何处理大规模数据集？**  
A: 该库使用优化的数据结构和增量索引，即使在**数百万文档**的情况下也能保持低内存使用。

**Q: 我可以将 GroupDocs.Search 集成到其他 Java 应用程序吗？**  
A: 可以，API 设计为易于嵌入任何基于 Java 的系统，从 Web 服务到桌面应用程序。

**Q: 如果搜索结果不准确，我该怎么办？**  
A: 验证索引已包含所有必需的文件（`add documents to index`），确保在需要时已禁用停用词过滤，并考虑在重大更改后重新构建索引。

## 其他资源

- **文档**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API 参考**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **下载**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **GitHub 仓库**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **免费支持**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **临时许可证**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

通过本指南，您现在了解如何**将文档添加到索引**以及**禁用停用词 java**，以在 Java 应用程序中提供更准确的搜索结果。

---

**最后更新：** 2026-07-07  
**测试环境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs  

---

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## 相关教程

- [语言处理 Java – 使用 GroupDocs.Search 创建同义词词典](/search/java/dictionaries-language-processing/)
- [使用 GroupDocs.Search 在 Java 中通过元数据索引将文档添加到索引](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [使用 GroupDocs.Search for Java 将文档添加到索引](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)