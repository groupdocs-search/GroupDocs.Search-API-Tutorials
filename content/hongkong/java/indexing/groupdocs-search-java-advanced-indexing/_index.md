---
date: '2026-08-15'
description: 了解如何透過 GroupDocs.Search for Java 的進階索引功能提升搜尋延遲，包括 cancellation、async
  operations、multithreading 以及 metadata customization。
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: 透過使用 cancellation、asynchronous indexing、multithreading 及 metadata
  customization，提升 GroupDocs.Search for Java 的搜尋延遲。增強效能並降低資源使用。
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: 使用 GroupDocs 進階索引提升搜尋延遲
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: 使用 GroupDocs 進階索引提升搜尋延遲
type: docs
url: /zh-hant/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# 透過進階索引提升 GroupDocs 的搜尋延遲

在當今快速變化的數位環境中，**提升搜尋延遲**是提供即時結果給使用者的關鍵。無論您是構建自訂搜尋引擎，或是強化現有的文件管理系統，正確的索引策略都能大幅降低延遲、減少資源消耗，並在整體上**提升搜尋延遲**。在本教學中，我們將逐一說明 GroupDocs.Search for Java 最強大的功能——取消、非同步索引、多執行緒以及中繼資料自訂——讓您能更快速且更有效率地**將文件加入索引**。

**您將學習**

- 如何在指定時間後取消索引作業  
- 執行非同步索引作業並處理狀態變更  
- 設定多執行緒以加速索引  
- 自訂中繼資料索引選項以 **自訂搜尋中繼資料**  

在深入程式碼之前，讓我們先確保您已備妥所有必要的項目。

## 快速問答
- **取消功能的作用是什麼？** 它會在設定的逾時後停止索引，釋放 CPU 與記憶體供其他工作使用。  
- **我可以非同步索引文件嗎？** 可以 — 只需使用 `options.setAsync(true)` 來啟用。  
- **我可以使用多少執行緒？** 任意正整數；對大多數伺服器而言，2‑4 個執行緒是常見設定。  
- **中繼資料索引是可選的嗎？** 絕對可以 — 您可以依欄位啟用或微調。  
- **使用這些功能需要授權嗎？** 試用版可用於測試；正式環境需購買完整授權。

## 前置條件

- **GroupDocs.Search 程式庫** – 版本 25.4 或更新。  
- **Java 開發環境** – 建議使用 JDK 8 或以上。  
- 具備 Java 基礎知識以及索引概念的了解。

### 設定 GroupDocs.Search for Java

#### Maven 安裝

將儲存庫與相依性加入您的 `pom.xml` 檔案：

`pom.xml` 設定告訴 Maven 需要下載並納入哪個 GroupDocs.Search 套件至您的專案中。

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

#### 直接下載

或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR 檔案。

**授權取得** – 可先使用免費試用，或申請臨時授權以解鎖完整功能。

### 基本初始化與設定

`SearchIndex` 類別是入口點，代表儲存在磁碟或記憶體中的可搜尋索引。

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## 在此情境下何謂「最佳化搜尋效能」？

最佳化搜尋效能是指調整索引流程，使其在消耗適當的 CPU、記憶體與時間的同時，即時提供最相關的結果。透過控制取消、非同步執行、執行緒與中繼資料處理，您可以直接影響引擎多快能夠 **將文件加入索引** 並回應查詢。

## 為何使用進階索引功能？

非同步與多執行緒索引可保持應用程式的回應性，而取消功能則防止程式無限制執行。精細調校的中繼資料選項讓您呈現最重要的資訊，直接 **提升搜尋延遲** 給最終使用者。此外，這些功能可減少 CPU 峰值、降低記憶體壓力，並在處理大量文件時實現更平順的擴充。

## 如何透過進階索引提升搜尋延遲？

載入您的 `SearchIndex` 實例，使用取消、非同步與執行緒設定來配置 `IndexingOptions`，然後呼叫 `index.add(document)` — 此組合可在一般工作負載下將整體索引時間縮短最高 60 %，且保證長時間執行的工作不會阻塞其他操作。您亦可調整中繼資料索引限制，並透過狀態變更事件監控進度，以確保整個流程符合效能預算。

## 實作指南

### 取消屬性

**概觀** – 在指定的時間後取消索引，以避免過度消耗資源。

#### 步驟 1：設定環境

建立指向索引資料夾的 `SearchIndex` 實例。

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：建立具取消功能的索引選項

`IndexingOptions` 讓您指定索引引擎的行為方式。

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**重點**

- `setCancellation()` 啟用此功能。  
- `cancelAfter(int milliseconds)` 定義逾時時間（本例為 3 秒）。

### 非同步屬性

**概觀** – 在背景執行緒上執行索引，並監聽狀態變更。

#### 步驟 1：設定環境

實例化索引並準備文件集合。

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：訂閱狀態變更事件

`StatusChanged` 事件會在索引工作在不同狀態之間切換時通知您。

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### 步驟 3：配置非同步選項

啟用非同步模式，使呼叫立即返回，處理在背景持續進行。

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### 執行緒屬性

**概觀** – 透過利用多個 CPU 核心加速索引。

#### 步驟 1：設定環境

準備索引，並確保 JVM 具有足夠的堆記憶體。

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：配置多執行緒

設定工作執行緒數量；每個執行緒處理文件的子集。

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### 中繼資料索引選項屬性

**概觀** – 精細調整哪些文件中繼資料會被索引以及其儲存方式。

#### 步驟 1：設定環境

載入包含作者、標題與自訂標籤等中繼資料欄位的文件。

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：配置中繼資料選項

`MetadataIndexingOptions` 讓您啟用或停用個別中繼資料欄位，並定義大小限制。

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## 實務應用

1. **文件管理系統** – 使用非同步索引，使 UI 在大量批次於背景處理時仍保持回應。  
2. **內容搜尋引擎** – 套用取消功能，以防止長時間執行的工作在高峰流量時佔用伺服器資源。  
3. **大規模擷取管線** – 利用多執行緒將 **文件加入索引**，大幅縮短處理時間。

## 效能考量

- **執行緒管理** – 監控 CPU 使用率；過多執行緒可能導致上下文切換開銷。  
- **記憶體占用** – 中繼資料限制（例如 `setMaxBytesToIndexField`）可使記憶體使用更可預測。  
- **垃圾回收** – 在索引大量語料庫時使用適當的 JVM 參數（`-Xmx`、`-XX:+UseG1GC`）。

## 常見問題與解決方案

| 症狀 | 可能原因 | 解決方案 |
|---------|--------------|-----|
| 索引永不完成 | 取消時間設定過低 | 增加 `cancelAfter` 的值，或對長時間作業移除取消功能 |
| 非同步模式下未收到狀態更新 | 事件處理器未正確掛載 | 確保在呼叫 `index.add` 前先執行 `index.getEvents().StatusChanged.add(...)` |
| 記憶體不足錯誤 | 執行緒過多或中繼資料限制過高 | 減少 `options.setThreads` 並降低中繼資料欄位限制 |
| 結果缺少中繼資料 | 中繼資料索引已停用 | 確認已設定 `options.getMetadataIndexingOptions()`，且未將欄位設為忽略 |

## 常見問答

**Q: 我該如何取得 GroupDocs.Search 的臨時授權？**  
A: 前往 [GroupDocs 的臨時授權頁面](https://purchase.groupdocs.com/temporary-license/) 並依照畫面指示操作。

**Q: 我可以在索引作業進行中途取消嗎？**  
A: 可以 — 使用 `cancelAfter()` 之取消屬性，或以程式方式呼叫 `Cancellation.cancel()`。

**Q: 非同步索引有哪些使用情境？**  
A: 即時文件檢索、背景批次處理，以及需要 UI 回應的應用程式，都能受惠於非同步索引。

**Q: 在共享伺服器上提升執行緒數量是否安全？**  
A: 請逐步增加並監控 CPU 負載；在高度共享的環境中，建議將執行緒數量維持在適度範圍（2‑4）。

**Q: 中繼資料索引如何影響搜尋相關性？**  
A: 正確索引的中繼資料（作者、建立日期、標籤）可在查詢中賦予較高權重，提升結果的準確度。

## 結論

透過善用 GroupDocs.Search for Java 的這些進階功能，您將在各種情境下 **提升搜尋延遲**——從快速文件匯入到精細的中繼資料控制。嘗試不同的設定、監控資源使用情況，並依您的工作負載調整參數，以獲得最佳效能。

---

**最後更新：** 2026-08-15  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs

## 相關教學

- [提升查詢效能：使用 GroupDocs.Search Java 優化索引與搜尋](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [如何在 Java 中使用 GroupDocs.Search 透過中繼資料索引將文件加入索引](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [如何在 GroupDocs.Search for Java 中新增多個別名並將文件加入索引](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)