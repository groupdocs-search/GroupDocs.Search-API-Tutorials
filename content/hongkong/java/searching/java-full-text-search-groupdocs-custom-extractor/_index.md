---
date: '2026-08-05'
description: 了解如何使用 GroupDocs.Search 在 Java 中建立 log file extractor 以進行 full-text search。將文件加入索引、優化搜尋效能，並有效處理大型
  log files。
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Full text search java 教學示範如何使用 GroupDocs.Search 建立自訂 log file extractor、將文件加入索引，並為大量
  log archives 優化搜尋效能。
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: Full text search java：使用 GroupDocs 的 log file extractor
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: Full text search java：使用 GroupDocs 的 log file extractor
type: docs
url: /zh-hant/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Full text search java：使用 GroupDocs 的日誌檔抽取器

Full‑text search java 是任何必須在海量文件集合中快速定位資訊的系統的基石。在本教學中，您將學習如何設定 GroupDocs.Search、建立自訂的日誌檔抽取器、將文件加入索引，以及在處理數 GB 的日誌資料時優化搜尋效能。

## 您將學到的內容
- 設定並配置 GroupDocs.Search for Java。  
- 實作一個 **log file extractor**，以您需要的方式解析純文字日誌。  
- **Add documents to index** 與 PDF、DOCX 及其他格式一起使用。  
- 實際情境中，**log file extractor** 能帶來可衡量的價值。  
- 實證技巧，**optimise search performance** 用於多 GB 的日誌檔案。

## 快速回答
- **What is a log file extractor?** 一個自訂元件，告訴 GroupDocs.Search 如何讀取與索引純文字日誌檔案。  
- **Why use GroupDocs.Search?** 它支援 50 多種格式的索引、提供自動重新索引，且能在低於 2 GB 記憶體的情況下處理高達 10 GB 的索引。  
- **Do I need a license?** 是的——需要試用或正式授權才能啟用此函式庫。  
- **Can I index other file types simultaneously?** 絕對可以；在同一索引中混合 PDF、DOCX 以及自訂日誌檔。  
- **How to improve performance?** 使用增量索引、調整 `IndexSettings`，並啟用 `autoReindex` 旗標。

## 前置條件

在開始之前，請確保您具備以下項目：

### 必要的函式庫
在 `pom.xml` 中加入 GroupDocs.Search 的 Maven 依賴項。使用與您專案 Java 版本相符的最新版本。

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

或者，直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 環境設定
- JDK 8 或更高版本。  
- 熟悉 Java 程式設計及基本檔案處理概念。

### 取得授權
首先下載免費試用授權，以探索 GroupDocs.Search 功能。若用於正式環境，請購買正式授權或透過 [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/) 申請臨時授權。

## 設定 GroupDocs.Search for Java

首先，初始化函式庫並套用您的授權檔案：

1. **Maven setup** – 確認先前步驟中的依賴已存在。  
2. **License initialisation** – 在任何其他 API 呼叫之前載入授權檔案。

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

環境就緒後，您即可開始建構自訂的 **log file extractor**。

## 什麼是 log file extractor？

log file extractor 是一段程式碼，告訴 GroupDocs.Search 如何讀取原始日誌檔（通常為 `.log`）並將其內容轉換為可搜尋的文字。自行提供抽取器即可完整掌控解析規則、過濾雜訊，並僅抽取對搜尋使用情境重要的資訊。

## 建立 log file extractor

GroupDocs.Search 允許您為任何檔案類型插入自訂文字抽取器。請依照以下步驟為日誌檔建立抽取器。

### 步驟 1：定義自訂抽取器
`TextExtractorBase` 為您繼承以建立自訂抽取器的抽象基底類別。它宣告抽取器支援的檔案副檔名，並包含核心抽取邏輯。

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**重點**  
- `getFileExtensions()` 為 `.log` 檔案註冊抽取器。  
- `extractText` 是您可以去除時間戳記、過濾除錯行，或套用任何前處理以 **search large log files** 的地方。

### 步驟 2：使用抽取器設定索引參數
將您的抽取器加入 `IndexSettings`，並啟用 `autoReindex`，使新日誌能自動索引，無需手動介入。

`IndexSettings` 設定索引行為，例如記憶體限制與自訂抽取器。  
`autoReindex` 會在來源檔案變更時自動更新索引。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### 步驟 3：將文件加入索引
現在索引已能辨識日誌檔，您可以像處理其他支援格式一樣 **add documents to index**。

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### 步驟 4：搜尋索引
執行純文字查詢。自訂抽取器確保每筆日誌條目皆可被搜尋。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## 優化搜尋效能的技巧

- **Incremental indexing** – 僅新增或變更的日誌檔，而非重新建構整個索引。  
- **Memory management** – `autoReindex` 旗標透過將中間資料寫入磁碟，降低 RAM 使用量。  
- **Index settings** – 根據伺服器容量調整 `setMaxMemoryUsage`；一般設定為 10 GB 索引使用 1 GB 記憶體。  
- **Query optimisation** – 在搜尋大量日誌檔案時，使用片語查詢、萬用字元或過濾條件以縮小結果。

## 實務應用

GroupDocs.Search 可應用於多種實務情境，例如：

- **Log management** – 在數秒內於數 GB 的日誌資料中定位錯誤訊息、使用者操作或特定時間戳記。  
- **Document retrieval systems** – 維護一個包含 PDF、Word 文件、試算表與自訂日誌檔的單一可搜尋儲存庫。  
- **Content analysis** – 執行關鍵字頻率報告或偵測串流日誌資料中的異常。

## 效能考量

在大規模部署 GroupDocs.Search 時，請留意以下最佳實踐：

- 將索引儲存在高速 SSD 上，以減少讀寫延遲。  
- 監控 JVM 堆積使用情況；若記憶體成為瓶頸，考慮將大型索引卸載至獨立程序。  
- 啟用 `autoReindex`（如前所示），使索引保持最新，無需手動重建。

## 結論

至此，您已建立 **log file extractor**、學會如何 **add documents to index**，並發現可為大型日誌檔案 **optimise search performance** 的方法。此組合讓您的 Java 應用程式能在任何文件類型上提供快速、精確的全文搜尋。

欲深入了解，請參考官方的 [GroupDocs documentation](https://docs.groupdocs.com/search/java/)，或嘗試不同的抽取器實作，以符合您的獨特使用情境。

## 常見問答
1. **What file types can I index using GroupDocs.Search?**  
   您可以索引 PDF、Word 文件、試算表及其他多種格式，亦可透過文字抽取器索引自訂日誌檔。  
2. **How do I handle large document collections efficiently?**  
   使用增量更新、分割索引，並調整 `IndexSettings` 以有效管理資源。  
3. **Can GroupDocs.Search be integrated with other systems?**  
   可以，它提供乾淨的 Java API，可嵌入現有服務、微服務或 Web 應用程式。  
4. **What is a temporary license, and how do I acquire one?**  
   臨時授權提供完整功能供評估使用，且無時間限制。可透過 [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/) 申請。

## 常見問題

**Q: How does a log file extractor differ from the default extractor?**  
A: 預設抽取器處理常見格式（PDF、DOCX 等）。自訂的 log file extractor 讓您精確定義純文字日誌條目的解析與索引方式。

**Q: Can I index compressed log archives (e.g., .zip)?**  
A: 可以，透過在送入索引前加入解壓縮的前置處理步驟，以提取檔案。

**Q: What’s the best way to keep the index up‑to‑date with continuously generated logs?**  
A: 啟用 `autoReindex`，並排程背景監控程式，在有新檔案出現時呼叫 `index.add(newLogFile)`。

**Q: Is there a limit to the size of a single log file that can be indexed?**  
A: 實務上受限於可用記憶體。建議在索引前將極大的日誌切分為較小的區塊。

**Q: Does GroupDocs.Search support fuzzy or wildcard searches?**  
A: 是的，搜尋 API 包含模糊匹配、萬用字元與相近查詢，以提升結果相關性。

---

**最後更新：** 2026-08-05  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs

## 相關教學

- [Java 全文搜尋：使用 GroupDocs.Search 建立索引](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [如何使用 GroupDocs.Search for Java 將文件加入索引](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [使用 GroupDocs.Search Java 提升查詢效能：最佳化索引與搜尋](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)