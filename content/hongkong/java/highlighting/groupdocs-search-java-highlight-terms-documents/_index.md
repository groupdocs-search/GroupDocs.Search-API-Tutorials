---
date: '2026-02-27'
description: 了解如何使用 GroupDocs.Search for Java 來突出顯示文字，內容包括 Java 文件搜尋、Java 文件索引與片段高亮。
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: 使用 GroupDocs.Search 在 Java 中突出顯示文字
type: docs
url: /zh-hant/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# 使用 GroupDocs.Search 於 Java 文字高亮

在當今節奏快速的數位環境中，能夠在大量檔案集合中 **highlight text java** 是必備功能。無論您是構建法律審查平台、學術研究引擎，或是客戶支援主控台，即時找出使用者所尋找的關鍵詞，都能大幅提升使用體驗。本教學將帶您使用 **GroupDocs.Search for Java** 來 **search documents java**、**index documents java**，並套用豐富的高亮顯示——包括整份文件以及特定片段。

## 快速解答
- **「search and highlight text」是什麼意思？** 它指的是在文件中定位查詢詞彙，並以視覺方式（例如背景色）強調這些詞彙。  
- **哪個函式庫提供此功能？** GroupDocs.Search for Java。  
- **需要授權嗎？** 免費試用可用於評估；正式上線需購買完整授權。  
- **可以自訂高亮顏色嗎？** 可以——任何 RGB 顏色皆可透過 `HighlightOptions` 設定。  
- **支援片段高亮嗎？** 完全支援；您可以自行定義匹配前後的詞彙數量，以產生簡潔的摘要片段。

## 如何在文件中使用 Java 文字高亮
文字高亮（Java）涉及三個核心步驟：

1. **Index the source files** so they can be searched quickly.  
2. **Run a query** against the index to find matching documents.  
3. **Render the results with visual cues** using the highlighter API.

以下將逐步說明每個步驟，先說明整份文件的輸出方式，接著說明片段層級的摘要。

## 什麼是搜尋與文字高亮？
搜尋與文字高亮是指掃描文件索引以尋找特定查詢，取得符合的文件，然後在文件輸出（HTML、PDF 等）中標記每一次出現的查詢詞彙。此視覺提示可協助最終使用者即時發現相關資訊。

## 為何使用 GroupDocs.Search for Java？
- **High‑performance indexing** with configurable compression (`index documents java`)。  
- **Rich highlighting API** that works on whole documents and on custom fragments (`highlight search terms java`)。  
- **Cross‑format support**（支援 DOCX、PDF、PPTX、TXT 等多種格式）。  
- **Simple Maven integration** and a clean Java‑centric design。

## 前置條件
- Java Development Kit (JDK) 8 或更新版本。  
- 用於相依管理的 Maven。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 基本的 Java 語法熟悉度。

## 設定 GroupDocs.Search for Java

將 GroupDocs 的儲存庫與相依加入您的 `pom.xml`：

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

您也可以直接從官方網站下載最新的 JAR 檔案：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權
先使用免費試用或取得臨時授權以進行評估。正式上線時，請購買完整授權以解鎖全部功能。

## 實作指南

實作分為兩個實務部分：**整份文件的高亮** 與 **片段的高亮**。兩個部分皆說明使用 GroupDocs.Search **how to highlight Java** 文件的必要步驟。

### 設定索引參數
在建立索引之前，先將儲存設定為高壓縮——可減少磁碟使用量，同時維持搜尋速度。

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### 整份文件的高亮顯示

#### 步驟 1：建立並填充索引
建立索引資料夾，並加入所有欲搜尋的來源檔案。

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### 步驟 2：執行搜尋並套用高亮
搜尋指定詞彙（例如 `ipsum`），並產生含有高亮匹配結果的 HTML 檔案。

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

**關鍵選項說明**  
- **Compression** – 高壓縮可節省儲存空間。  
- **HighlightColor** – 設定任意 RGB 值以配合您的 UI 配色。  
- **UseInlineStyles** – `false` 會產生乾淨的 HTML，方便以全域 CSS 進行樣式設定。

### 片段的高亮顯示

#### 步驟 1：索引與搜尋（同上）

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### 步驟 2：定義片段上下文並高亮
指定每個片段在匹配前後要顯示多少個詞彙。

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

#### 步驟 3：取得並寫入高亮片段
收集產生的片段，並寫入 HTML 檔案。

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

## 實務應用
1. **Legal Document Review** – 即時高亮法條、條款或案例參考。  
2. **Academic Research** – 在數十份 PDF 與 Word 檔中快速找出關鍵術語。  
3. **Customer Support** – 精準定位工單歷史中的訂單編號或錯誤代碼。

## 效能考量
- **Index Size** – 高壓縮 (`Compression.High`) 可減少磁碟佔用。  
- **Fragment Context** – 較大的 `termsBefore/After` 數值提升精確度，但可能影響速度。  
- **Memory Management** – 索引大型語料庫時請監控 JVM 堆積，必要時採用增量索引以因應極大資料集。

## 常見問題與解決方案
- **Indexing Errors** – 核對檔案路徑，確保應用程式具備讀寫權限。  
- **No Highlights Appear** – 確認 `UseInlineStyles` 與您的輸出格式（HTML vs. PDF）相符。  
- **Color Not Applied** – 確認 RGB 值在 0‑255 之間，且 HTML 檢視器支援相應樣式。

## 常見問答

**Q: 使用 GroupDocs.Search for Java 有什麼好處？**  
A: 它提供快速且可擴充的索引、可自訂的高亮功能，且支援多種文件格式。

**Q: 如何將 GroupDocs.Search 與 REST API 整合？**  
A: 透過 Spring Boot 控制器將搜尋與高亮方法公開，回傳 HTML 或 JSON 資料。

**Q: 函式庫能處理受密碼保護的檔案嗎？**  
A: 能——在將文件加入索引時提供相應的密碼即可。

**Q: 除了顏色外，我能自訂高亮標記的其他屬性嗎？**  
A: 當然可以；您可以透過 `HighlightOptions` 注入 CSS 類別，或在產生後自行修改 HTML。

**Q: 本指南測試的是哪個版本？**  
A: 程式碼已在 GroupDocs.Search 25.4 上驗證通過。

**Q: 如何設定 `highlight options java` 使用 CSS 類別而非行內樣式？**  
A: 設定 `options.setUseInlineStyles(false)`，並為您透過 `options.setCssClass("myHighlight")` 指定的類別加入相應的 CSS 規則。

**Q: 有沒有辦法在來源為 PDF 時直接 **highlight terms pdf java**？**  
A: 有——GroupDocs.Search 支援 PDF 輸入，高亮器會輸出 HTML，您可將其嵌入 PDF 檢視器，或使用 GroupDocs.Conversion 轉回 PDF。

---

**最後更新：** 2026-02-27  
**測試版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs