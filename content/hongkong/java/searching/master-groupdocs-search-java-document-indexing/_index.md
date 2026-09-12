---
date: '2026-09-11'
description: 了解如何在 Java 中突顯搜尋結果，並使用 GroupDocs.Search for Java 以同步與非同步方式索引文件。
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: 使用 GroupDocs.Search 在 Java 中突顯搜尋結果。了解同步與非同步索引、即時更新，以及在 Java 應用程式中的結果突顯。
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: 在 Java 中突顯搜尋結果 – 快速同步與非同步索引
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: 在 Java 中突顯搜尋結果 – 同步與非同步索引
type: docs
url: /zh-hant/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# 突顯搜尋結果 Java – 同步與非同步索引

在本指南中，您將了解如何使用 GroupDocs.Search 函式庫 **highlight search results Java**，以及一步步了解如何以同步和非同步方式對 Java 文件進行索引。無論您是構建小型桌面工具還是大型企業搜尋服務，這些技術都能讓您即時提供視覺上清晰的匹配結果，且不會阻塞應用程式執行緒。

## 快速解答
- **What does “highlight search results Java” mean?** 它表示在返回的摘要中將每個匹配的詞彙以標記（例如 `<mark>`）包裹起來，讓使用者能即時看到命中的上下文。  
- **When should I use synchronous indexing?** 在需要文件一加入即能搜尋的小至中等規模集合時使用同步索引。  
- **When is asynchronous indexing preferable?** 在大量批次或 UI 執行緒必須保持回應、索引在背景建構時選擇非同步索引。  
- **Do I need a license?** 免費試用可用於開發；完整授權則移除限制並解鎖進階功能。  
- **Which Java version is supported?** Java 8 或更新版本。

## 什麼是 “highlight search results Java”？
`highlight search results java` 是從 GroupDocs.Search 取得原始匹配資料，並在每個找到的詞彙周圍插入視覺提示——通常是 HTML `<mark>` 標籤的過程。這使得結果摘要在網頁或 Swing 元件中即時可讀，提升使用者體驗，清楚顯示查詢出現的位置。

## 為何在 Java 中使用 GroupDocs.Search？
GroupDocs.Search 提供高效能、語言無關的引擎，能 **每秒處理高達 5 000 份文件**、**支援 30 多種檔案格式**，以及 **索引 1,000 萬文件的集合**，且不需將整個語料庫載入記憶體。其內建的突顯功能、即時索引與多語言分析器，使其成為內容管理系統、電子商務目錄與企業文件儲存庫的理想選擇。

## 先決條件
- **Java Development Kit** (JDK 8 或更新) 已安裝且 `JAVA_HOME` 正確設定。  
- 如 **IntelliJ IDEA** 或 **Eclipse** 等 IDE。  
- 一個資料夾（例如 `documents/`）包含您想要索引的檔案——純文字、PDF、DOCX 等。  
- 用於相依管理的 Maven（或手動加入 JAR）。

### 必要的函式庫與相依性
將 GroupDocs.Search 加入您的 Maven `pom.xml`：

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

如需直接下載，請從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 取得最新版本。

### 環境設定
- 確認 `JAVA_HOME` 指向相容的 JDK。  
- 建立新的 Maven 專案，並將上述程式碼片段貼入 `<dependencies>` 區段。  
- 將範例檔案放置於類似 `src/main/resources/documents/` 的目錄中。

## 如何設定 GroupDocs.Search for Java
`Index` 是代表儲存在磁碟上的可搜尋集合的核心類別。

建立指向磁碟資料夾的 `Index` 實例，若有授權則套用授權，並可選擇性設定語言特定的分詞分析器。此準備步驟確保引擎能有效且正確地讀寫與搜尋索引。

`Index` 類別是代表磁碟上可搜尋集合的核心元件。實例化後，所有索引與查詢操作皆透過此物件執行。

1. **Install the library** – 使用上述 Maven 片段或從 [GroupDocs](https://releases.groupdocs.com/search/java/) 下載 JAR。  
2. **Obtain a license** – 先使用試用授權；在部署前以正式金鑰取代。  
3. **Initialize the index** – 以下程式碼片段示範如何建立（或開啟）索引資料夾：

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## 如何以同步索引突顯搜尋結果 Java
`DocumentHighlighter` 是產生搜尋結果突顯摘要的工具類別。

載入索引，使用 `index.add(documentPath)` 新增文件，執行查詢，然後呼叫 `DocumentHighlighter` 以在 `<mark>` 標籤中包裹匹配項目。整個流程在呼叫執行緒上執行，因而文件在 `add` 回傳後即能立即搜尋供最終使用者使用。

### 步驟 1：建立索引並附加錯誤處理
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### 步驟 2：新增文件並執行搜尋
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### 步驟 3：處理結果並突顯搜尋結果 Java
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## 如何以非同步索引突顯搜尋結果 Java
`IndexingOptions` 設定索引過程的執行方式，包括同步或非同步模式。

將 `IndexingOptions` 設定為背景模式，訂閱 `StatusChanged` 事件，讓引擎在 UI 繼續處理其他請求時進行檔案索引。當狀態變為 `Ready` 後，即可執行搜尋並取得突顯的摘要，與同步模式相同。

`AsyncIndexingListener` 接收進度更新，讓您能顯示進度條或記錄狀態，而不會阻塞主執行緒。

### 步驟 1：設定索引並加入事件監聽器
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### 步驟 2：啟用非同步模式並開始索引
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## 如何以 Java 索引文件 – 實用技巧
`index.update(path)` 會使用指定路徑的檔案更新索引中已存在的文件。

將大型集合分割為 1 000–5 000 檔案的批次，依副檔名過濾以避免不必要的解析，並對變更的檔案使用 `index.update(path)` 而非重新建構整個索引。這些做法可降低記憶體使用並使索引時間可預測，以維持一致性。

- **Batch size**：對於龐大集合，將資料夾分割為較小批次以避免記憶體激增。  
- **File filters**：使用 `IndexingOptions.setFileExtensions` 只包含所需的格式（例如 `.pdf`、`.docx`）。  
- **Re‑indexing**：文件變更時，呼叫 `index.update(documentPath)` 而非從頭重新建立索引。

## 效能考量
- **Memory**：監控堆積使用量；若同時處理大量大型檔案，請增加 `-Xmx`。  
- **CPU**：非同步索引將工作負載分散至多執行緒，但仍會消耗 CPU——可使用 JVisualVM 追蹤使用情況。  
- **Result highlighting**：突顯會帶來適度的額外開銷（約每筆結果 2–5 ms）。若需重複顯示相同摘要，請快取產生的 HTML。

## 常見問題
**Q: Can I combine synchronous and asynchronous indexing in the same application?**  
A: 是的。對於小型、頻繁更新的集合使用同步索引，對於大量匯入或背景工作則使用非同步索引。

**Q: How do I customize the highlight style?**  
A: 提供自訂的 `DocumentHighlighter` 實作，讓其在匹配的詞彙周圍寫入所需的 HTML、CSS 或 XML 標籤。

**Q: What file types does GroupDocs.Search support out of the box?**  
A: 文字、PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、HTML，以及透過內建解析器支援的更多格式——總計超過 30 種。

**Q: Is it possible to search in multiple languages simultaneously?**  
A: 絕對可以。GroupDocs.Search 包含多語言分析器，只要在建立索引時設定相應的 `Analyzer` 即可。

**Q: How do I secure the index folder?**  
A: 將索引存放於受保護的目錄，設定嚴格的檔案系統權限，並可選擇使用函式庫的安全功能加密索引。

---

**最後更新:** 2026-09-11  
**測試環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs

## 相關教學

- [如何使用 GroupDocs.Search API for Java 建立文件索引並新增文件](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [如何使用 GroupDocs.Search 建立 Java 索引儲存庫：高效文件索引與搜尋](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [高效文件索引搜尋 Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)