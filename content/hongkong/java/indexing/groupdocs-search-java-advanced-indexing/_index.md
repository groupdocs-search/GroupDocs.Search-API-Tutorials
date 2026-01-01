---
date: '2025-12-29'
description: 學習如何利用 GroupDocs.Search for Java 的進階索引功能優化搜尋效能，包括取消、非同步操作、多執行緒及中繼資料自訂。
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: 使用 GroupDocs.Search for Java 的進階索引技術優化搜尋效能
type: docs
url: /zh-hant/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# 使用 GroupDocs.Search for Java 的進階索引技術優化搜尋效能

在當今節奏快速的數位環境中，**優化搜尋效能**對於向使用者即時提供結果至關重要。無論您是構建自訂搜尋引擎還是增強現有的文件管理系統，正確的索引策略都能顯著降低延遲與資源消耗。在本教學中，我們將逐一說明 GroupDocs.Search for Java 最強大的功能——取消、非同步索引、多執行緒以及中繼資料自訂——讓您能更快速且更有效率地**add documents index**。

**您將學習**

- 如何在指定時間後取消索引作業
- 執行非同步索引作業並處理狀態變更
- 設定多執行緒以加速索引
- 自訂中繼資料索引選項

在深入程式碼之前，先確保您已具備所有必需的條件。

## 前置條件

- **GroupDocs.Search Library** – 版本 25.4 或更新。  
- **Java Development Environment** – 建議使用 JDK 8 或以上。  
- 具備 Java 基礎知識以及索引概念。

### 設定 GroupDocs.Search for Java

#### Maven 安裝

將儲存庫與相依性加入您的 `pom.xml` 檔案：

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

或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR。

**授權取得** – 可先使用免費試用版，或申請臨時授權以解鎖完整功能。

### 基本初始化與設定

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

## 快速問答

- **取消功能的作用是什麼？** 在設定的時間後停止索引，以釋放資源。  
- **我可以非同步索引文件嗎？** 可以 – 設定 `options.setAsync(true)`。  
- **可以使用多少執行緒？** 任意正整數；大多數伺服器的典型值為 2‑4。  
- **中繼資料索引是可選的嗎？** 當然可以 – 您可以依欄位啟用或微調。  
- **使用這些功能需要授權嗎？** 試用版可用於測試；正式環境需購買完整授權。

## 在此情境下「優化搜尋效能」是什麼意思？

優化搜尋效能是指設定索引過程，使其在消耗適當的 CPU、記憶體與時間的同時，即時提供最相關的結果。透過控制取消、非同步執行、執行緒與中繼資料處理，您可以直接影響引擎多快能夠**add documents index** 並回應查詢。

## 為何使用進階索引功能？

- **降低延遲** – 非同步與多執行緒索引讓您的應用程式保持回應。  
- **更佳資源管理** – 取消功能可防止程式失控執行。  
- **客製化搜尋相關性** – 中繼資料選項讓您突顯最重要的資訊。

## 實作指南

### 取消屬性

**概觀** – 在指定的時間後取消索引，以避免過度消耗資源。

#### 步驟 1：設定環境

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：建立具取消功能的索引選項

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

**重點說明**

- `setCancellation()` 會啟用此功能。  
- `cancelAfter(int milliseconds)` 定義逾時時間（本例為 3 秒）。

### 非同步屬性

**概觀** – 在背景執行緒上執行索引，並監聽狀態變更。

#### 步驟 1：設定環境

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：訂閱狀態變更事件

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

#### 步驟 3：設定非同步選項

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### 執行緒屬性

**概觀** – 利用多個 CPU 核心加速索引。

#### 步驟 1：設定環境

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：設定多執行緒

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### 中繼資料索引選項屬性

**概觀** – 微調哪些文件中繼資料會被索引以及其儲存方式。

#### 步驟 1：設定環境

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 步驟 2：設定中繼資料選項

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
2. **內容搜尋引擎** – 套用取消功能，以防止長時間執行的工作在高峰期間佔用伺服器資源。  
3. **大規模匯入管線** – 利用多執行緒以規模化 **add documents index**，大幅縮短處理時間。

## 效能考量

- **執行緒管理** – 監控 CPU 使用率；過多執行緒可能導致上下文切換開銷。  
- **記憶體占用** – 中繼資料限制（例如 `setMaxBytesToIndexField`）有助於保持記憶體使用可預測。  
- **垃圾回收** – 在索引大量語料庫時使用適當的 JVM 參數（`-Xmx`、`-XX:+UseG1GC`）。

## 常見問題與解決方案

| 症狀 | 可能原因 | 解決方案 |
|---------|--------------|-----|
| 索引永遠不會完成 | 取消時間設定過低 | 增加 `cancelAfter` 值或對長時間作業移除取消功能 |
| 非同步模式下沒有狀態更新 | 事件處理器未正確掛載 | 確保在呼叫 `index.add` 前先執行 `index.getEvents().StatusChanged.add(...)` |
| 記憶體不足錯誤 | 執行緒過多或中繼資料限制過高 | 減少 `options.setThreads` 並降低中繼資料欄位限制 |
| 結果中缺少中繼資料 | 中繼資料索引被停用 | 檢查 `options.getMetadataIndexingOptions()` 已正確設定且未設定為忽略欄位 |

## 常見問答

**Q: 我該如何取得 GroupDocs.Search 的臨時授權？**  
A: 前往 [GroupDocs 的臨時授權頁面](https://purchase.groupdocs.com/temporary-license/)。

**Q: 我可以在索引作業進行中途取消嗎？**  
A: 可以 – 使用 `cancelAfter()` 的取消屬性，或以程式方式呼叫 `Cancellation.cancel()`。

**Q: 非同步索引有哪些使用案例？**  
A: 即時文件檢索、背景批次處理以及需要 UI 保持回應的應用程式，都能從非同步索引中受益。

**Q: 在共享伺服器上提升執行緒數量是否安全？**  
A: 請逐步增加並監控 CPU 負載；在高度共享的環境中，建議將執行緒數量保持在適度範圍（2‑4）。

**Q: 中繼資料索引如何影響搜尋相關性？**  
A: 正確索引的中繼資料（作者、建立日期、標籤）可在查詢中賦予更高權重，提升結果的準確度。

## 結論

透過善用 GroupDocs.Search for Java 的這些進階功能，您將在各種情境下**優化搜尋效能**——從快速文件匯入到精細的中繼資料控制。請嘗試不同的設定、監控資源使用，並依據您的工作負載調整參數，以獲得最佳效果。

---

**最後更新：** 2025-12-29  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs