---
date: '2026-02-19'
description: 了解如何在搜索中禁用停用词并使用 GroupDocs.Search for Java 将文档添加到索引，以提升查询准确性。
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 搜索中的停用词：使用 GroupDocs.Search Java 将文档添加到索引
type: docs
url: /zh/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# 搜索中的停用词：使用 GroupDocs.Search Java 将文档添加到索引

如果您需要 **将文档添加到索引**，并确保没有重要的词——尤其是常见词——被忽略，那么您来对地方了。在本指南中，我们将展示如何使用 GroupDocs.Search for Java **禁用搜索中的停用词**，使每个标记（即使是 “on”、 “by” 或 “the”）都可被搜索，从而让结果更加准确。

## 快速答疑
- **“将文档添加到索引” 是什么意思？** 这意味着将源文件加载到可搜索的索引中，以便能够高效地进行查询。  
- **为什么要禁用停用词？** 当这些常用词在您的业务领域中具有实际意义时（例如 “on”、 “the”），将它们加入搜索可以提升检索的完整性。  
- **需要哪个库版本？** GroupDocs.Search for Java 25.4 或更高版本。  
- **需要许可证吗？** 评估阶段可使用免费试用版；生产环境必须使用正式许可证。  
- **可以在 Maven 项目中使用吗？** 可以——只需在下面添加仓库和依赖即可。

## 什么是搜索中的停用词，为什么可能需要禁用它们？
停用词是搜索引擎为加快查询速度而自动过滤的高频词。虽然这对通用网页搜索有帮助，但在法律合同、电子商务目录或技术手册等专业领域，这些词（如 “on”、 “by”、 “as”）往往承载真实含义。禁用停用词后，您可以把每个词都视为重要，确保不遗漏任何相关文档。

## 在 GroupDocs.Search 中添加文档到索引是如何工作的？
当您添加文档时，库会读取每个文件，对其内容进行分词，并将分词结果存储在优化的数据结构（即索引）中。完成索引后，搜索引擎能够在毫秒级返回匹配的文档，即使是大型集合也不例外。

## 前置条件

- **必需库**：GroupDocs.Search for Java 25.4（或更新版本）。  
- **开发环境**：IntelliJ IDEA、Eclipse 或您喜欢的任何 Java IDE。  
- **基础知识**：熟悉 Java 语法以及索引的概念。

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

#### 许可证获取步骤
- **免费试用** – 立即开始测试。  
- **临时许可证** – 获取限时密钥以获得完整功能。  
- **购买** – 为生产使用获取永久许可证。

## 基本初始化与设置

创建 `IndexSettings` 实例以控制索引行为：

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## 如何在搜索中禁用停用词（Java）

下面这行代码可关闭内置的停用词过滤器：

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*参数*：`setUseStopWords` 接受布尔值。  
*目的*：确保每个词——包括常见停用词——都被索引并可搜索。

## 如何将文档添加到索引

### 定义输出目录

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### 指定文档目录

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

现在，`YOUR_DOCUMENT_DIRECTORY` 中的每个文件都会 **被添加到索引**，并可供查询使用。

## 执行搜索查询

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

由于已禁用停用词，搜索词 `"on"` 将被纳入检索，返回原本会被忽略的匹配结果。

## 实际应用场景

1. **企业文档搜索** – 确保关键术语不被过滤。  
2. **电子商务平台** – 通过索引产品描述中的每个词提升商品发现率。  
3. **法律检索工具** – 捕获每个法律术语，即使它们通常被视为停用词。

## 性能考虑

- **优化技巧**：定期更新并清理索引，以保持搜索速度。  
- **资源使用**：监控 JVM 堆大小；大型索引可能需要调优垃圾回收设置。  
- **Java 内存管理**：使用高效的数据结构，并在处理超大语料库时考虑离堆存储。

## 常见问题与解决方案

| 症状 | 可能原因 | 解决办法 |
|---|---|---|
| 常用词无搜索结果 | `setUseStopWords(true)`（默认） | 按上述方式调用 `setUseStopWords(false)`。 |
| 索引时出现内存溢出 | 一次性索引过多大文件 | 将文件分批索引；增大 `-Xmx` JVM 参数。 |
| 搜索返回旧数据 | 添加新文件后未刷新索引 | 调用 `index.update()` 或重新添加已更改的文档。 |

## 常见问答

**Q: 什么是停用词？**  
A: 停用词是许多搜索引擎为加快查询速度而忽略的常用词（如 “the”、 “is”、 “on”）。禁用它们后，您可以把每个标记都视为可搜索的。

**Q: 为什么要在搜索索引中禁用停用词？**  
A: 在需要精确短语匹配的场景（如法律或技术文档）中，每个词都有意义，必须包含停用词。

**Q: GroupDocs.Search 如何处理大规模数据集？**  
A: 该库使用优化的数据结构和增量索引技术，即使面对数百万文档也能保持低内存占用。

**Q: 我可以将 GroupDocs.Search 集成到其他 Java 应用吗？**  
A: 可以，API 设计为可轻松嵌入任何基于 Java 的系统，无论是 Web 服务还是桌面应用。

**Q: 如果搜索结果不准确该怎么办？**  
A: 确认索引已包含所有必需文档（`add documents to index`），确保已根据需要禁用停用词过滤，并在重大更改后考虑重新构建索引。

## 其他资源

- **文档**：[GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API 参考**：[GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **下载**：[获取最新的 GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- **GitHub 仓库**：[Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免费支持**：[加入 GroupDocs 论坛](https://forum.groupdocs.com/c/search/10)  
- **临时许可证**：[申请临时许可证](https://purchase.groupdocs.com/temporary-license/)

通过本指南，您已经掌握了如何 **将文档添加到索引** 并 **在搜索中禁用停用词**，从而在 Java 应用中提供更精准的检索结果。

---

**最后更新：** 2026-02-19  
**测试环境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs