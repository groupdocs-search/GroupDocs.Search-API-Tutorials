---
date: '2026-09-27'
description: 了解如何使用 GroupDocs.Search for Java 突顯 Java 文字，涵蓋 search documents java、index
  documents java 以及 fragment highlighting。
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: 了解如何使用 GroupDocs.Search for Java 突顯 Java 文字。提供 indexing、searching
  與 fragment highlighting 的逐步指引，快速取得結果。
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: 使用 GroupDocs.Search 突顯 Java 文字 – 快速文件突顯
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
title: 使用 GroupDocs.Search 突顯 Java 文字
type: docs
url: /zh-hant/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# 使用 GroupDocs.Search 在 Java 中突顯文字

在現代企業應用程式中，**highlight text java** 是將原始搜尋結果轉換為即時可讀洞見的關鍵。無論您是構建法律審查平台、學術研究引擎，或是客戶支援儀表板，能夠定位並視覺上強調查詢詞彙，都能為使用者節省大量手動掃描的時間。本教學將示範如何使用 **GroupDocs.Search for Java** 來 **search documents java**、**index documents java**，以及同時套用全文與片段層級的突顯，只需幾行程式碼。

## 快速解答
- **什麼是「search and highlight text」？** 意味著在文件中定位查詢詞彙，並以視覺方式強調它們（例如使用彩色背景）。  
- **哪個函式庫提供此功能？** GroupDocs.Search for Java。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買完整授權。  
- **我可以自訂突顯顏色嗎？** 可以——任何 RGB 顏色皆可透過 `HighlightOptions` 設定。  
- **支援片段突顯嗎？** 當然可以；您可以設定匹配前後的詞彙數量，以產生精簡的摘要。

## 如何在文件中突顯文字 java

要在文件中突顯文字 java，首先使用適當的壓縮設定建立來源檔案的索引，接著執行搜尋查詢以定位目標詞彙，最後將結果匯出為 HTML、PDF 或純文字，並將每個匹配項包裹在突顯標籤中。此三步驟流程確保在大型集合中快速且精確的突顯。

1. **建立索引**，使用可降低儲存空間的壓縮設定。  
2. **執行搜尋**，使用您想要突顯的查詢字串。  
3. **產生輸出**（HTML、PDF 或純文字），其中每個查詢詞的出現都被包裹在突顯標籤中。

## 什麼是搜尋與突顯文字？

搜尋與突顯文字是掃描已索引集合以尋找特定查詢、取得匹配文件，然後在輸出（HTML、PDF 等）中標記每個查詢詞出現的過程。此視覺提示可協助最終使用者即時發現相關資訊。

## 為何使用 GroupDocs.Search for Java？

GroupDocs.Search for Java 提供 **高效能索引**（每個索引最高可達 50 GB，使用 `Compression.High`）、**豐富的突顯功能**，可在整篇文件及自訂片段上運作，並支援超過 30 種檔案類型的 **跨格式支援**——包括 DOCX、PDF、PPTX 與 TXT。此函式庫亦提供 **增量索引**，讓您在不重新建構整個索引的情況下新增檔案，於大型部署中可降低高達 80 % 的停機時間。

## 前置條件
- Java Development Kit (JDK) 8 或更新版本。  
- 用於相依管理的 Maven。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 基本的 Java 語法知識。

## 設定 GroupDocs.Search for Java

將 GroupDocs 儲存庫與相依性加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

您也可以直接從官方網站下載最新的 JAR 檔案：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權
先使用免費試用版或取得臨時授權以進行評估。正式部署時，請購買完整授權以解鎖全部功能。

## 實作指南

實作分為兩個實用章節：**整篇文件的突顯** 與 **片段的突顯**。兩個章節皆包含使用 GroupDocs.Search **如何突顯 Java** 文件的必要步驟。

### 設定索引參數

在索引之前，設定儲存使用高壓縮——可在保留搜尋速度的同時將磁碟使用量降低最高 70 %。

`IndexSettings` 是控制索引在磁碟上儲存方式的設定物件。將 `Compression` 設為 `Compression.High` 以啟用此最佳化。  
`Compression` 指定套用於索引檔案的資料壓縮等級，`Compression.High` 提供最大的尺寸縮減。

## 整篇文件的突顯

### 步驟 1：建立並填充索引

建立索引資料夾，並加入所有欲搜尋的來源檔案。`Index` 類別代表可搜尋的容器。

### 步驟 2：執行搜尋並套用突顯

搜尋指定詞彙（例如 `ipsum`），並產生含有突顯匹配項的 HTML 檔案。使用 `HighlightOptions` 來指定突顯顏色以及是否使用內聯樣式。

`HighlightOptions` 允許您定義前景與背景顏色，並可設定套用於每個突顯詞彙的 CSS 類別。

`HtmlHighlighter` 依據提供的選項產生含有突顯詞彙的 HTML 輸出。  
`SearchResult` 包含匹配文件的清單以及每個找到詞彙的位置。

**直接答案：** 載入您的索引，呼叫 `search("ipsum")`，並將產生的 `SearchResult` 與已設定好的 `HighlightOptions` 實例一起傳遞給 `HtmlHighlighter`。突顯器會回傳 HTML，將每個 “ipsum” 出現包裹在帶有選定背景顏色的 `<span>` 中。

說明關鍵選項  
- **Compression** – 高壓縮可節省儲存空間。  
- **HighlightColor** – 設定任意 RGB 值以符合您的 UI 調色板。  
- **UseInlineStyles** – `false` 會產生可透過全域 CSS 樣式化的乾淨 HTML。

## 片段的突顯

### 步驟 1：索引與搜尋（同上）

使用相同的索引與搜尋步驟；您會重複使用 `Index` 與 `SearchResult` 物件。

### 步驟 2：定義片段上下文並突顯

使用 `FragmentOptions` 指定每個片段中匹配前後應顯示的詞彙數量。

`FragmentOptions` 控制每個摘要中包含的前後詞彙數量（`termsBefore` 與 `termsAfter`），讓您在上下文與摘要長度之間取得平衡。

### 步驟 3：取得並寫入突顯片段

收集產生的片段並寫入 HTML 檔案。每個片段已根據您設定的 `HighlightOptions` 進行突顯。

`fragmentHighlighter` 是一個工具，可根據指定的片段與突顯選項，從 `SearchResult` 建立突顯摘要。

**直接答案：** 取得 `SearchResult` 後，呼叫 `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)`。此方法會回傳 HTML 摘要清單，每個摘要包含匹配詞彙，前後以設定的上下文字數環繞，並以選定的顏色突顯。

## 實務應用
1. **Legal document review** – 即時突顯數千份合約中的法條、條款或案例參考。  
2. **Academic research** – 在數十份 PDF 與 Word 檔案中找出關鍵術語，將文獻回顧時間縮短最高 60 %。  
3. **Customer support** – 在客服單歷史中快速定位訂單號碼或錯誤代碼，讓客服人員更快解決問題。

## 效能考量
- **Index size** – 高壓縮 (`Compression.High`) 可將磁碟佔用降低最高 70 %，且對延遲影響不明顯。  
- **Fragment context** – 較大的 `termsBefore/After` 數值提升摘要可讀性，但可能每次查詢額外增加 10–15 ms。  
- **Memory management** – 索引大型語料庫時監控 JVM 堆積；對於超過 2 GB 的資料集，考慮使用增量索引以將記憶體使用量維持在 1 GB 以下。

## 常見問題與解決方案
- **Indexing errors** – 檢查檔案路徑，並確保應用程式對索引資料夾具有讀寫權限。  
- **No highlights appear** – 確認 `UseInlineStyles` 與您的輸出格式（HTML 或 PDF）相符。  
- **Color not applied** – 確認 RGB 值在 0‑255 範圍內，且檢視器支援內聯 CSS 或提供的 CSS 類別。

## 常見問答

**Q: 使用 GroupDocs.Search for Java 有什麼好處？**  
A: 它提供快速且可擴展的索引、可自訂的突顯功能，支援超過 30 種文件格式，能在一般伺服器上於 2 秒內處理 500 頁的檔案。

**Q: 如何將 GroupDocs.Search 整合至 REST API？**  
A: 透過 Spring Boot 控制器公開搜尋與突顯方法，回傳包含突顯片段的 HTML 摘要或 JSON 資料。

**Q: 函式庫能處理受密碼保護的檔案嗎？**  
A: 可以——在使用 `addDocument(filePath, password)` 將文件加入索引時提供密碼。

**Q: 我能自訂突顯標記（除顏色外）嗎？**  
A: 當然可以；您可以使用 `options.setCssClass("myHighlight")` 指定 CSS 類別並全域樣式化，或在突顯後修改產生的 HTML。

**Q: 本指南測試使用的版本是什麼？**  
A: 程式碼已在 GroupDocs.Search 25.4 版本上驗證。

**Q: 如何設定 highlight options java 使用 CSS 類別而非內聯樣式？**  
A: 呼叫 `options.setUseInlineStyles(false)`，並透過 `options.setCssClass("myHighlight")` 為指定的類別定義 CSS 規則。

**Q: 有辦法直接在 PDF 輸出中突顯詞彙嗎？**  
A: 可以——GroupDocs.Search 支援 PDF 輸入，且突顯器會產生可嵌入 PDF 檢視器的 HTML，或使用 GroupDocs.Conversion 重新轉換為 PDF。

---

**最後更新：** 2026-09-27  
**測試版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs

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

## 相關教學

- [如何使用 GroupDocs.Search 在 Java 中實作全文搜尋：建立索引目錄](/search/java/indexing/groupdocs-search-java-create-index/)
- [學習使用 GroupDocs.Search for Java 管理搜尋索引](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [在 Java 中使用基於區塊的搜尋將文件加入索引](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)