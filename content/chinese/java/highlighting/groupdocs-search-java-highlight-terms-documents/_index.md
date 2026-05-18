---
date: '2026-02-27'
description: 学习如何使用 GroupDocs.Search for Java 对文本进行高亮显示，涵盖 Java 文档搜索、Java 文档索引以及片段高亮。
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: 使用 GroupDocs.Search 在 Java 中高亮文本
type: docs
url: /zh/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

A: Yes—GroupDocs.Search works with PDF input, and the highlighter will output HTML that you can embed in a PDF viewer or convert back to PDF using GroupDocs.Conversion. ->

Translate each.

Next final lines:

**Last Updated:** 2026-02-27  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs

Translate labels but keep dates.

**最后更新：** 2026-02-27  
**测试版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs

Now produce final markdown with translations.

Make sure to keep all placeholders unchanged.

Let's craft final answer.# 使用 GroupDocs.Search 的 Java 文本高亮

在当今快节奏的数字环境中，能够在大量文件集合中 **highlight text java** 是必备功能。无论您是在构建法律审查平台、学术研究引擎，还是客户支持控制台，能够即时定位用户搜索的词汇都能大幅提升体验。本教程将指导您使用 **GroupDocs.Search for Java** 来 **search documents java**、**index documents java**，并应用丰富的高亮显示——既可用于整篇文档，也可用于特定片段。

## Quick Answers
- **“search and highlight text” 是什么意思？** 它指在文档中定位查询词并通过视觉方式（例如背景颜色）突出显示它们。  
- **提供此功能的库是哪个？** GroupDocs.Search for Java。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要完整许可证。  
- **我可以自定义高亮颜色吗？** 可以——通过 `HighlightOptions` 可以设置任意 RGB 颜色。  
- **支持片段高亮吗？** 当然支持；您可以定义匹配前后出现的词数，以生成简洁的摘要。

## 在文档中使用 Java 高亮文本
Java 文本高亮涉及三个核心步骤：

1. **索引源文件**，以便快速搜索。  
2. **对索引执行查询**，以查找匹配的文档。  
3. **使用高亮 API 渲染结果**，并提供视觉提示。  

下面我们将详细探讨每一步，首先是整篇文档的输出，其次是片段级别的摘要。

## 什么是搜索并高亮文本？
搜索并高亮文本是指在文档索引中扫描给定查询，检索匹配的文档，然后在文档输出（HTML、PDF 等）中标记每个查询词出现的位置。此视觉提示帮助终端用户即时发现相关信息。

## 为什么使用 GroupDocs.Search for Java？
- **高性能索引**，支持可配置压缩（`index documents java`）。  
- **丰富的高亮 API**，可用于整篇文档和自定义片段（`highlight search terms java`）。  
- **跨格式支持**（DOCX、PDF、PPTX、TXT 等）。  
- **简易的 Maven 集成**，以及清晰的 Java 为中心的设计。

## Prerequisites
- Java Development Kit（JDK）8 或更高版本。  
- 用于依赖管理的 Maven。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 对 Java 语法有基本了解。

## Setting Up GroupDocs.Search for Java

在 `pom.xml` 中添加 GroupDocs 仓库和依赖：

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

您也可以直接从官方网站下载最新的 JAR 包：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
先使用免费试用或获取临时许可证进行评估。生产部署时，需要购买完整许可证以解锁全部功能。

## Implementation Guide

实现分为两个实用部分：**整篇文档高亮**和**片段高亮**。两个部分都包含使用 GroupDocs.Search 对 **Java 文档进行高亮** 的关键步骤。

### Configuring Index Settings
在索引之前，配置存储使用高压缩——这可以在保持搜索速度的同时降低磁盘使用量。

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Highlighting in Entire Documents

#### Step 1: Create and Populate the Index
创建索引文件夹并添加所有需要搜索的源文件。

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Step 2: Perform Search and Apply Highlighting
搜索指定词（例如 `ipsum`），并生成带有高亮匹配的 HTML 文件。

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

**关键选项说明**  
- **Compression** – 高压缩可节省存储空间。  
- **HighlightColor** – 设置任意 RGB 值以匹配您的 UI 调色板。  
- **UseInlineStyles** – `false` 会生成干净的 HTML，可通过全局 CSS 样式进行美化。  

### Highlighting in Fragments

#### Step 1: Index and Search (same as above)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Step 2: Define Fragment Context and Highlight
指定每个片段中匹配前后应出现的词数。

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

#### Step 3: Retrieve and Write Highlighted Fragments
收集生成的片段并写入 HTML 文件。

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

## Practical Applications
1. **法律文档审查** – 即时高亮法规、条款或案例引用。  
2. **学术研究** – 在数十个 PDF 和 Word 文件中快速呈现关键术语。  
3. **客户支持** – 在工单历史中快速定位订单号或错误代码。  

## Performance Considerations
- **索引大小** – 高压缩（`Compression.High`）可减小磁盘占用。  
- **片段上下文** – 更大的 `termsBefore/After` 值提升准确性，但可能影响速度。  
- **内存管理** – 在索引大规模语料库时监控 JVM 堆；对极大数据集可考虑增量索引。  

## Common Issues and Solutions
- **索引错误** – 检查文件路径并确保应用拥有读写权限。  
- **未出现高亮** – 确认 `UseInlineStyles` 与您的输出格式（HTML 或 PDF）匹配。  
- **颜色未生效** – 确认 RGB 值在 0‑255 范围内，并且 HTML 查看器支持该样式。  

## Frequently Asked Questions

**Q: 使用 GroupDocs.Search for Java 有哪些好处？**  
A: 它提供快速、可扩展的索引、可定制的高亮以及对多种文档格式的支持。

**Q: 如何将 GroupDocs.Search 与 REST API 集成？**  
A: 通过 Spring Boot 控制器公开搜索和高亮方法，返回 HTML 或 JSON 负载。

**Q: 该库能处理受密码保护的文件吗？**  
A: 能——在将文档添加到索引时提供密码即可。

**Q: 我可以自定义高亮标记的样式（除颜色外）吗？**  
A: 完全可以；可以通过 `HighlightOptions` 注入 CSS 类，或在生成后修改 HTML。

**Q: 本指南使用的测试版本是什么？**  
A: 代码已在 GroupDocs.Search 25.4 上验证。

**Q: 如何将 highlight options java 设置为使用 CSS 类而非内联样式？**  
A: 设置 `options.setUseInlineStyles(false)`，并通过 `options.setCssClass("myHighlight")` 为其分配的类添加 CSS 规则。

**Q: 是否有办法在源文件为 PDF 时直接高亮 terms pdf java？**  
A: 有——GroupDocs.Search 支持 PDF 输入，高亮器会输出 HTML，您可以将其嵌入 PDF 查看器或使用 GroupDocs.Conversion 再转换回 PDF。

**Last Updated:** 2026-02-27  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs