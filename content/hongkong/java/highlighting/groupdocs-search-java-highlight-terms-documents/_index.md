---
date: '2025-12-26'
description: 學習如何使用 GroupDocs.Search for Java 在文件中搜尋並突出顯示文字。探索完整文件與片段突出顯示的技巧。
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: 使用 GroupDocs.Search for Java 進行搜尋與文字突顯
type: docs
url: /zh-hant/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# 使用 GroupDocs.Search for Java 在文件中搜尋與標記文字

在當今的數位時代，跨大量文件集合的 **search and highlight text** 已成為常見需求。無論您正在構建法律審查工具、學術研究平台，或是客戶支援儀表板，能即時定位並強調關鍵詞彙都能大幅提升使用體驗。在本完整指南中，您將了解如何使用 GroupDocs.Search for Java 實作 **search and highlight text**——涵蓋整份文件的標記以及片段層級的標記，以提供聚焦的上下文。

## 快速解答
- **What does “search and highlight text” mean?** 它指的是在文件中定位查詢詞彙，並以視覺方式強調它們（例如使用背景色）。  
- **Which library provides this capability?** GroupDocs.Search for Java.  
- **Do I need a license?** 免費試用可用於評估；正式環境需購買完整授權。  
- **Can I customize highlight colors?** 可以——任何 RGB 顏色皆可透過 `HighlightOptions` 設定。  
- **Is fragment highlighting supported?** 當然支援；您可以定義匹配前後的詞彙數量，以產生精簡的片段。  

## 什麼是 Search and Highlight Text？
Search and highlight text 是掃描文件索引以尋找特定查詢、取得匹配文件，並在文件輸出（HTML、PDF 等）中標記每個查詢詞彙出現的位置的過程。此視覺提示可協助最終使用者即時發現相關資訊。

## 為何使用 GroupDocs.Search for Java？
- **High‑performance indexing** 具可配置的壓縮功能。  
- **Rich highlighting API** 可於整份文件及自訂片段上使用。  
- **Cross‑format support**（支援 DOCX、PDF、PPTX、TXT 等多種格式）。  
- **Easy Maven integration** 以及清晰的 Java 為中心 API。  

## 前置條件
- Java Development Kit (JDK) 8 或更新版本。  
- 用於相依管理的 Maven。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 具備基本的 Java 語法知識。  

## 設定 GroupDocs.Search for Java
將 GroupDocs 儲存庫與相依項目加入您的 `pom.xml`：

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

您也可以直接從官方網站下載最新的 JAR 檔案：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權
先使用免費試用版或取得臨時授權以進行評估。正式上線時，請購買完整授權以解鎖全部功能。

## 實作指南
實作分為兩個實用章節：**highlighting in entire documents** 與 **highlighting in fragments**。兩個章節皆包含使用 GroupDocs.Search 進行 **how to highlight Java** 文件的關鍵步驟。

### 設定索引參數
在建立索引之前，先設定儲存使用高壓縮——可減少磁碟空間同時保持搜尋速度。

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### 在整份文件中標記

#### 步驟 1：建立並填充索引
建立索引資料夾，並加入所有欲搜尋的來源檔案。

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### 步驟 2：執行搜尋並套用標記
搜尋指定詞彙（例如 `ipsum`），並產生含有標記匹配結果的 HTML 檔案。

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
- **HighlightColor** – 設定任意 RGB 值以符合您的 UI 配色。  
- **UseInlineStyles** – 設為 `false` 會產生乾淨的 HTML，可透過全域 CSS 進行樣式設定。  

### 在片段中標記

#### 步驟 1：索引與搜尋（同上）

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### 步驟 2：定義片段上下文與標記
指定每個片段中匹配前後應顯示的詞彙數量。

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

#### 步驟 3：取得並寫入標記片段
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
1. **Legal Document Review** – 即時標記法規、條款或案例參考。  
2. **Academic Research** – 在數十份 PDF 與 Word 檔中顯示關鍵術語。  
3. **Customer Support** – 在工單歷史中快速定位訂單號碼或錯誤代碼。  

## 效能考量
- **Index Size** – 高壓縮（`Compression.High`）可減少磁碟佔用。  
- **Fragment Context** – 較大的 `termsBefore/After` 數值可提升準確度，但可能影響速度。  
- **Memory Management** – 索引大型語料庫時監控 JVM 堆積；對於極大集合可考慮增量索引。  

## 常見問題與解決方案
- **Indexing Errors** – 檢查檔案路徑並確保應用程式具備讀寫權限。  
- **No Highlights Appear** – 確認 `UseInlineStyles` 與您的輸出格式（HTML 或 PDF）相符。  
- **Color Not Applied** – 確認 RGB 值在 0‑255 範圍內，且 HTML 檢視器支援該樣式。  

## 常見問答

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: 它提供快速且可擴展的索引、可自訂的標記，以及支援多種文件格式的能力。

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: 透過 Spring Boot 控制器公開搜尋與標記方法，回傳 HTML 或 JSON 資料。

**Q: Does the library handle password‑protected files?**  
A: 會——在將文件加入索引時提供密碼即可。

**Q: Can I customize the highlight markup beyond color?**  
A: 當然可以；您可以透過 `HighlightOptions` 注入 CSS 類別，或在產生後自行修改 HTML。

**Q: What version was tested for this guide?**  
A: 程式碼已在 GroupDocs.Search 25.4 版本上驗證。

---

**Last Updated:** 2025-12-26  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs