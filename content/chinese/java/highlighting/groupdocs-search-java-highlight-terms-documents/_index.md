---
date: '2025-12-26'
description: 学习如何使用 GroupDocs.Search for Java 在文档中搜索和突出显示文本。探索全文档和片段高亮显示的技术。
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: 使用 GroupDocs.Search for Java 搜索并高亮文本
type: docs
url: /zh/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# 使用 GroupDocs.Search for Java 在文档中搜索并高亮文本

在当今数字时代，跨大规模文档集合进行 **search and highlight text** 是常见需求。无论您是在构建法律审查工具、学术研究门户，还是客户支持仪表板，能够即时定位并强调关键术语都能显著提升可用性。在本综合指南中，您将了解如何使用 GroupDocs.Search for Java 实现 **search and highlight text** ——涵盖全文档高亮和片段级高亮，以提供聚焦的上下文。

## 快速回答
- **What does “search and highlight text” mean?** 它指的是在文档中定位查询词并通过视觉方式（例如背景颜色）进行强调。  
- **Which library provides this capability?** GroupDocs.Search for Java。  
- **Do I need a license?** 免费试用可用于评估；生产环境需要完整许可证。  
- **Can I customize highlight colors?** 可以——任何 RGB 颜色均可通过 `HighlightOptions` 设置。  
- **Is fragment highlighting supported?** 完全支持；您可以定义匹配前后出现的词数，以创建简洁的片段。

## 什么是 Search and Highlight Text？
Search and highlight text 是扫描文档索引以查找给定查询、检索匹配文档，然后在文档输出（HTML、PDF 等）中标记每个查询词出现位置的过程。此视觉提示帮助最终用户即时发现相关信息。

## 为什么使用 GroupDocs.Search for Java？
- **High‑performance indexing** 具备可配置的压缩选项。  
- **Rich highlighting API** 可对整篇文档和自定义片段进行高亮。  
- **Cross‑format support** 支持 DOCX、PDF、PPTX、TXT 等多种格式。  
- **Easy Maven integration** 提供清晰的 Java‑centric API。

## 前置条件
- Java Development Kit (JDK) 8 或更高版本。  
- 用于依赖管理的 Maven。  
- IntelliJ IDEA 或 Eclipse 等 IDE。  
- 基本的 Java 语法熟悉度。

## 设置 GroupDocs.Search for Java

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

您也可以直接从官方网站下载最新的 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 获取许可证
先使用免费试用或获取临时许可证进行评估。生产部署时，请购买完整许可证以解锁全部功能。

## 实施指南

实现分为两个实用部分：**在整个文档中高亮** 和 **在片段中高亮**。两部分均包含使用 GroupDocs.Search **how to highlight Java** 文档的关键步骤。

### 配置索引设置
在索引之前，配置存储使用高压缩——这可以在保持搜索速度的同时降低磁盘使用量。

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### 在整个文档中高亮

#### 步骤 1：创建并填充索引
创建索引文件夹并添加所有需要搜索的源文件。

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### 步骤 2：执行搜索并应用高亮
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
- **UseInlineStyles** – `false` 会生成干净的 HTML，可通过全局 CSS 进行样式化。

### 在片段中高亮

#### 步骤 1：索引并搜索（同上）

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### 步骤 2：定义片段上下文并高亮
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

#### 步骤 3：检索并写入高亮片段
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

## 实际应用
1. **Legal Document Review** – 立即高亮法规、条款或案例引用。  
2. **Academic Research** – 在数十个 PDF 与 Word 文件中快速定位关键术语。  
3. **Customer Support** – 在工单历史中精准定位订单号或错误码。

## 性能考虑
- **Index Size** – 高压缩 (`Compression.High`) 可减少磁盘占用。  
- **Fragment Context** – 较大的 `termsBefore/After` 值提升准确性，但可能影响速度。  
- **Memory Management** – 索引大规模语料库时监控 JVM 堆内存；对超大集合可考虑增量索引。

## 常见问题与解决方案
- **Indexing Errors** – 核实文件路径并确保应用拥有读写权限。  
- **No Highlights Appear** – 确认 `UseInlineStyles` 与输出格式（HTML 与 PDF）匹配。  
- **Color Not Applied** – 确认 RGB 值在 0‑255 范围内，并且 HTML 查看器支持相应样式。

## 常见问答

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: 它提供快速、可扩展的索引、可定制的高亮功能，并支持多种文档格式。

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: 通过 Spring Boot 控制器暴露搜索和高亮方法，返回 HTML 或 JSON 负载。

**Q: Does the library handle password‑protected files?**  
A: 是的——在将文档添加到索引时提供密码即可。

**Q: Can I customize the highlight markup beyond color?**  
A: 完全可以；您可以通过 `HighlightOptions` 注入 CSS 类，或在生成后修改 HTML。

**Q: What version was tested for this guide?**  
A: 代码已在 GroupDocs.Search 25.4 上验证。

---

**Last Updated:** 2025-12-26  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs