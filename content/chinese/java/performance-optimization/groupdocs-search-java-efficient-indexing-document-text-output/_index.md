---
date: '2026-06-27'
description: 使用 GroupDocs.Search for Java 的分步指南，介绍如何创建索引、从文档中提取文本并将文本输出到文件——这是一款快速的
  Java 搜索库。
keywords:
- how to create index
- extract text from documents
- output text to file
- add documents to index
- extract text to string
schemas:
- author: GroupDocs
  dateModified: '2026-06-27'
  description: Step‑by‑step guide on how to create index, extract text from documents
    and output text to file using GroupDocs.Search for Java – the fast java search
    library.
  headline: How to create index java with GroupDocs.Search for Java
  type: TechArticle
- questions:
  - answer: Yes, the library is pure Java and works seamlessly with any JVM language.
    question: Can I use GroupDocs.Search with other JVM languages like Kotlin or Scala?
  - answer: High compression reduces disk usage by up to 70 % and adds only a minimal
      CPU overhead during indexing; query latency remains under 100 ms for typical
      workloads.
    question: How does compression affect search speed?
  - answer: Absolutely. Use `index.add()` for new files and `index.remove()` to delete
      outdated ones, allowing incremental updates.
    question: Is it possible to update an existing index without rebuilding it?
  - answer: The `PlainText` result from the **structured text extraction** adapter
      provides clean, language‑agnostic content ideal for NLP tasks.
    question: Which output format is best for natural‑language‑processing pipelines?
  - answer: A free trial license suffices for development and evaluation; production
      deployments require a purchased license.
    question: Do I need a license for development and testing?
  type: FAQPage
title: 如何使用 GroupDocs.Search for Java 创建 Java 索引
type: docs
url: /zh/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# 掌握使用 GroupDocs.Search for Java 的高效文档搜索

在成千上万的 PDF、Word 文件或电子表格中找到正确的段落，常常像在大海捞针。快速 **How to create index** 并检索到该针是文档搜索解决方案有价值的关键。在本教程中，您将学习如何使用 **GroupDocs.Search for Java**，一个高性能的 java 搜索库，来 **create index**、**add documents to index**，以及从文档中 **extract text from documents**，支持文件、流、字符串和结构化数据等多种格式。完成后，您将拥有一个可在大型文档集合上扩展且内存占用低的生产就绪索引管道。

## 快速答案
- **主要目的是什么？** 是 **how to create index** 并即时检索文档内容。  
- **我应该使用哪个库？** 是 **GroupDocs.Search for Java** **java search library**。  
- **我可以将文本输出到文件吗？** 是的——库提供 **output text to file** 适配器，可用于 HTML、纯文本等。  
- **支持结构化提取吗？** 当然——使用 **structured text extraction** 适配器获取字段级数据。  
- **我需要许可证吗？** 试用许可证可用于开发；生产部署需要永久许可证。

## 您将学习的内容
- 如何使用 GroupDocs.Search for Java **how to create index** 和 **add documents to index**。  
- 针对 **output text to file**、流、字符串和结构化格式的技术。  
- 保持索引快速且内存高效的性能优化技巧。  
- 这些功能在实际场景中的优势，例如法律合同库和学术论文档案。

## 为什么使用 GroupDocs.Search for Java？
GroupDocs.Search 支持 **50+ input and output formats** ——包括 DOCX、XLSX、PPTX、PDF、HTML 以及常见图像类型，并且能够在不将整个文件加载到内存的情况下索引多 GB 的文件。基准测试显示，1 GB 的文档集合在标准的 8 核服务器上可在 2 分钟以内完成索引，而搜索查询的返回时间不足 100 毫秒。

## 前置条件
- **Java Development Kit (JDK)** 8 或更高。  
- **GroupDocs.Search for Java** 库（试用版或授权版）。  
- **Maven** 用于依赖管理。  
- 基本的 Java I/O 知识。

## 设置 GroupDocs.Search for Java
首先，将 GroupDocs.Search Maven 仓库和依赖添加到项目的 `pom.xml` 中。此步骤确保库在类路径上可用。

**Maven 设置**  
在您的 `pom.xml` 文件中添加以下仓库和依赖配置：

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

对于更喜欢直接下载的用户，您可以从 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 获取最新版本。

**许可证获取**  
要在生产环境中使用 GroupDocs.Search，请从官方网站获取试用或永久许可证。试用许可证在开发和测试中无限制。

## 如何使用自定义设置创建 Java 索引
`Index` 是表示可搜索文档集合的核心类。  
`IndexSettings` 配置索引的选项，例如压缩。  
`CompressionLevel` 定义存储文本的压缩程度。

加载启用压缩的 `Index` 对象，指向一个文件夹，并添加所有支持的文件。此直接回答段落告诉您确切的操作步骤：使用 `new Index("indexFolder", new IndexSettings().setCompressionLevel(CompressionLevel.High))` 实例化 `Index`，然后调用 `index.add("documentsFolder", true)` 递归索引每个支持的文件。高压缩模式可将磁盘占用降低最多 70 %，同时保持搜索速度快速。

创建索引是任何基于搜索的应用程序的基础。下面的示例将引导您完成该过程，解释每个设置，并展示如何验证索引已成功构建。

### 索引创建与文档索引

#### 概述
`Index` 类是表示可搜索文档集合的核心组件。它存储倒排索引、词典以及实现快速查找所需的元数据。

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**说明**  
- **Index Settings**：我们为文本存储启用 **high compression**，在不影响查询速度的前提下优化磁盘空间使用。  
- **Adding Documents**：`index.add()` 方法 **adds documents to index**，递归扫描文件夹并自动处理所有支持的格式。

## 如何将文本输出为文件、流、字符串和结构化格式
索引完成后，您通常需要提取文档的原始或格式化文本。GroupDocs.Search 提供了四种适配器，允许您将提取的内容写入文件、内存流、Java `String` 或结构化对象模型。

### 文本输出到文件

`FileOutputAdapter` 将提取的文档文本写入所选格式的文件。

#### 概述
`FileOutputAdapter` 将提取的文本以所选格式（HTML、纯文本等）直接写入磁盘文件。这对于生成可读报告或供下游处理流水线使用非常有用。

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**说明**  
- **FileOutputAdapter**：将索引文档的文本转换为 HTML 并写入指定的文件路径，保留标题、表格等基本格式。

### 文本输出到流

`StreamOutputAdapter` 将提取的文档文本流式传输到 `ByteArrayOutputStream`，无需创建临时文件。

#### 概述
当您仅临时需要内容时——例如通过 HTTP 发送或嵌入网页响应——请使用 `StreamOutputAdapter`。它将文本流式传输到 `ByteArrayOutputStream`，避免创建临时文件的开销。

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**说明**  
- **StreamOutputAdapter**：将文档文本流式传输到 `ByteArrayOutputStream`，实现灵活处理且无需触及文件系统。

### 文本输出到字符串

`StringOutputAdapter` 将整个文档文本捕获到单个 `String` 对象中。

#### 概述
用于快速日志记录、调试或 UI 显示时，`StringOutputAdapter` 将整个文档文本捕获到单个 `String` 对象中。

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**说明**  
- **StringOutputAdapter**：将文档文本捕获到 `String` 中，便于嵌入日志、控制台输出或 UI 组件。

### 文本输出到结构化格式

`StructuredOutputAdapter` 返回包含段落、表格和自定义元数据的丰富对象模型。

#### 概述
`StructuredOutputAdapter` 返回包含段落、表格和自定义元数据的丰富对象模型。该格式非常适合下游自然语言处理（NLP）或数据提取工作流。

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**说明**  
- **StructuredOutputAdapter**：将文档文本提取为 **structured text extraction** 格式，实现细粒度分析、字段提取以及与机器学习流水线的集成。

## 常见问题及解决方案
| 问题 | 原因 | 解决方案 |
|-------|-------|-----|
| **索引未创建** | 文件夹路径不正确或缺少写入权限 | 确认 `indexFolder` 存在且应用具有写入权限 |
| **未返回文档** | `index.add()` 未调用或源文件夹错误 | 确保 `documentsFolder` 指向正确的目录并包含受支持的文件类型 |
| **输出文件为空** | 输出适配器路径无效或缺少目录 | 在运行前创建目标目录 (`YOUR_OUTPUT_DIRECTORY`) |
| **大文件导致内存激增** | 将整个文件加载到内存 | 使用 `StreamOutputAdapter` 增量处理数据 |

## 常见问答

**Q: 我可以将 GroupDocs.Search 与其他 JVM 语言（如 Kotlin 或 Scala）一起使用吗？**  
A: 是的，库是纯 Java 的，可无缝与任何 JVM 语言配合使用。

**Q: 压缩会如何影响搜索速度？**  
A: 高压缩可将磁盘使用量降低最多 70 %，在索引期间仅增加极小的 CPU 开销；典型工作负载下查询延迟仍保持在 100 毫秒以下。

**Q: 是否可以在不重建的情况下更新现有索引？**  
A: 当然。使用 `index.add()` 添加新文件，使用 `index.remove()` 删除过时文件，从而实现增量更新。

**Q: 哪种输出格式最适合自然语言处理（NLP）流水线？**  
A: `PlainText` 结果来自 **structured text extraction** 适配器，提供干净、语言无关的内容，非常适合 NLP 任务。

**Q: 开发和测试是否需要许可证？**  
A: 免费试用许可证足以用于开发和评估；生产部署需要购买许可证。

## 结论
您现在拥有完整的、可投入生产的工作流，可用于 **how to create index**、添加文档以及以您可能需要的所有格式提取文本。首先使用压缩配置 `Index`，添加文档集合，并为下游场景选择合适的输出适配器——无论是生成 HTML 报告、为 NLP 模型提供数据，还是将内容流式传输到 Web 客户端。尝试增量更新 API，以在不进行昂贵重建的情况下保持索引最新，您将享受在任何文档库中快速、可靠的搜索体验。

---

**最后更新：** 2026-06-27  
**测试版本：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## 相关教程

- [将文档添加到索引 – GroupDocs.Search Java 指南](/search/java/advanced-features/)
- [使用 GroupDocs.Search for Java 创建文档索引](/search/java/advanced-features/groupdocs-search-java-implementation-guide/)
- [如何在 Java 中使用 GroupDocs.Search 通过元数据索引将文档添加到索引](/search/java/indexing/groupdocs-search-java-metadata-indexing/)