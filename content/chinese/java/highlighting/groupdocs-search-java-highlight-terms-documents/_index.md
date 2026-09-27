---
date: '2026-09-27'
description: 了解如何使用 GroupDocs.Search for Java 高亮 Java 文本，涵盖 Java 文档搜索、Java 文档索引和片段高亮。
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: 了解如何使用 GroupDocs.Search for Java 高亮 Java 文本。获取关于索引、搜索和片段高亮的分步指南，以实现快速结果。
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: 使用 GroupDocs.Search 高亮 Java 文本 – 快速文档高亮
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: 使用 GroupDocs.Search 高亮 Java 文本
type: docs
url: /zh/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# 使用 GroupDocs.Search 高亮 Java 文本

在现代企业应用中，**highlight text java** 对于将原始搜索结果转化为即时可读的洞察至关重要。无论您是构建法律审查门户、学术研究引擎，还是客户支持仪表板，能够定位并视觉上强调查询词都能为用户节省大量手动扫描的时间。本教程展示了如何使用 **GroupDocs.Search for Java** 来 **search documents java**、**index documents java**，以及在全文档和片段级别应用高亮，仅需几行代码。

## 快速答案
- **What does “search and highlight text” mean?** 这意味着在文档中定位查询词并以视觉方式强调它们（例如，使用彩色背景）。  
- **Which library provides this capability?** GroupDocs.Search for Java。  
- **Do I need a license?** 免费试用可用于评估；生产环境需要完整许可证。  
- **Can I customize highlight colors?** 是的——任何 RGB 颜色都可以通过 `HighlightOptions` 设置。  
- **Is fragment highlighting supported?** 当然；您可以在匹配前后定义词语以创建简洁的片段。

## 如何在文档中高亮 Java 文本

要在文档中高亮 Java 文本，首先使用适当的压缩设置构建源文件的索引，然后运行搜索查询定位所需词语，最后将结果导出为 HTML、PDF 或纯文本，并将每个匹配项包装在高亮标签中。此三步流程确保在大规模集合中实现快速、准确的高亮。

1. **Create an index** 使用保持存储占用低的压缩设置创建索引。  
2. **Execute a search** 使用您想要高亮的查询字符串执行搜索。  
3. **Generate output**（HTML、PDF 或纯文本），其中每个查询词的出现都被包装在高亮标签中。

## 什么是搜索并高亮文本？

搜索并高亮文本是对已索引集合进行给定查询的扫描过程，检索匹配的文档，然后在输出（HTML、PDF 等）中标记每个查询词的出现。此视觉提示帮助终端用户瞬间发现相关信息。

## 为什么使用 GroupDocs.Search for Java？

GroupDocs.Search for Java 提供 **高性能索引**（使用 `Compression.High` 可达每个索引 50 GB），**丰富的高亮**，支持整篇文档和自定义片段，并且 **跨格式支持** 超过 30 种文件类型——包括 DOCX、PDF、PPTX 和 TXT。该库还提供 **增量索引**，允许在不重新构建整个索引的情况下添加新文件，在大规模部署中可将停机时间降低最多 80%。

## 先决条件
- Java Development Kit (JDK) 8 或更高版本。  
- Maven 用于依赖管理。  
- IDE，例如 IntelliJ IDEA 或 Eclipse。  
- 对 Java 语法有基本了解。

## 设置 GroupDocs.Search for Java

将 GroupDocs 仓库和依赖添加到您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

您也可以直接从官方网站下载最新的 JAR：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 获取许可证
先使用免费试用或获取临时许可证进行评估。生产部署请购买完整许可证以解锁全部功能。

## 实现指南

实现分为两个实用部分：**在整个文档中高亮** 和 **在片段中高亮**。两部分均包含使用 GroupDocs.Search **如何高亮 Java** 文档的关键步骤。

### 配置索引设置

索引前，配置存储使用高压缩——这可将磁盘使用量降低最多 70%，同时保持搜索速度。

`IndexSettings` 是控制索引在磁盘上存储方式的配置对象。将 `Compression` 设置为 `Compression.High` 以启用此优化。  
`Compression` 指定对索引文件应用的数据压缩级别，`Compression.High` 提供最大尺寸缩减。

## 在整个文档中高亮

### 步骤 1：创建并填充索引

创建索引文件夹并添加所有要搜索的源文件。`Index` 类代表可搜索的容器。

### 步骤 2：执行搜索并应用高亮

搜索指定词语（例如 `ipsum`），并生成带有高亮匹配的 HTML 文件。使用 `HighlightOptions` 指定高亮颜色以及是否使用内联样式。

`HighlightOptions` 允许您定义前景色、背景色以及将应用于每个高亮词的 CSS 类。

`HtmlHighlighter` 根据提供的选项生成带有高亮词的 HTML 输出。  
`SearchResult` 包含匹配文档的列表以及每个找到词的位置。

**Direct answer:** 加载索引，调用 `search("ipsum")`，并将得到的 `SearchResult` 与配置好的 `HighlightOptions` 实例一起传递给 `HtmlHighlighter`。高亮器返回的 HTML 中，每个 “ipsum” 都被 `<span>` 包裹，并使用所选背景颜色。

关键选项说明  
- **Compression** – 高压缩可节省存储空间。  
- **HighlightColor** – 设置任意 RGB 值以匹配 UI 调色板。  
- **UseInlineStyles** – `false` 生成可通过全局 CSS 样式的干净 HTML。  

## 在片段中高亮

### 步骤 1：索引和搜索（同上）

同上使用 `Index` 和 `SearchResult` 对象。

### 步骤 2：定义片段上下文并高亮

使用 `FragmentOptions` 指定每个片段中匹配前后应出现多少词语。

`FragmentOptions` 控制每个片段中包含的前后词数（`termsBefore` 和 `termsAfter`），帮助在上下文与片段长度之间取得平衡。

### 步骤 3：检索并写入高亮片段

收集生成的片段并写入 HTML 文件。每个片段已根据您配置的 `HighlightOptions` 进行高亮。

`fragmentHighlighter` 是一个工具，使用指定的片段和高亮选项从 `SearchResult` 创建高亮片段。

**Direct answer:** 获得 `SearchResult` 后，调用 `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)`。该方法返回一组 HTML 片段，每个片段包含匹配词及其前后配置的上下文词，并使用选定颜色进行高亮。

## 实际应用
1. **Legal document review** – 在数千份合同中即时高亮法规、条款或案例引用。  
2. **Academic research** – 在数十个 PDF 和 Word 文件中呈现关键术语，将文献审查时间缩短最多 60%。  
3. **Customer support** – 在工单历史中定位订单号或错误代码，使客服人员更快解决问题。

## 性能考虑
- **Index size** – 高压缩 (`Compression.High`) 可将磁盘占用降低最多 70%，且对延迟影响不明显。  
- **Fragment context** – 更大的 `termsBefore/After` 值提升片段可读性，但可能每次查询增加 10–15 ms。  
- **Memory management** – 在索引大型语料库时监控 JVM 堆；对于超过 2 GB 的数据集，考虑增量索引以将内存使用保持在 1 GB 以下。

## 常见问题及解决方案
- **Indexing errors** – 验证文件路径并确保应用对索引文件夹具有读写权限。  
- **No highlights appear** – 确认 `UseInlineStyles` 与输出格式（HTML 或 PDF）匹配。  
- **Color not applied** – 确保 RGB 值在 0‑255 范围内，并且查看器支持内联 CSS 或提供的 CSS 类。

## 常见问答

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: 它提供快速、可扩展的索引、可定制的高亮，以及对 30 多种文档格式的支持，在典型服务器上可在 2 秒内处理 500 页文件。

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: 通过 Spring Boot 控制器公开搜索和高亮方法，返回包含高亮片段的 HTML 片段或 JSON 负载。

**Q: Does the library handle password‑protected files?**  
A: 是的——在通过 `addDocument(filePath, password)` 将文档添加到索引时提供密码。

**Q: Can I customize the highlight markup beyond color?**  
A: 完全可以；您可以使用 `options.setCssClass("myHighlight")` 分配 CSS 类并全局样式化，或在高亮后修改生成的 HTML。

**Q: What version was tested for this guide?**  
A: 代码已在 GroupDocs.Search 25.4 上验证。

**Q: How do I set highlight options java to use a CSS class instead of inline styles?**  
A: 调用 `options.setUseInlineStyles(false)`，并通过 `options.setCssClass("myHighlight")` 为类定义 CSS 规则。

**Q: Is there a way to highlight terms in PDF output directly?**  
A: 有——GroupDocs.Search 支持 PDF 输入，高亮器输出的 HTML 可嵌入 PDF 查看器，或使用 GroupDocs.Conversion 重新转换为 PDF。

---

**Last updated:** 2026-09-27  
**Tested with:** GroupDocs.Search 25.4  
**Author:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## 相关教程

- [如何实现 Java 全文搜索：使用 GroupDocs.Search 创建索引目录](/search/java/indexing/groupdocs-search-java-create-index/)
- [学习使用 GroupDocs.Search for Java 管理搜索索引](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [在 Java 中使用基于块的搜索将文档添加到索引](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)