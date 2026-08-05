---
date: '2026-03-01'
description: 學習如何透過 GroupDocs.Search for Java 的進階索引功能（包括取消、非同步操作、多執行緒及自訂中繼資料）來優化搜尋效能與降低搜尋延遲。
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: 在 GroupDocs.Search for Java 中使用先進索引技術優化搜尋效能
type: docs
url: /zh-hant/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# 使用 GroupDocs.Search for Java 的進階索引技術優化搜尋效能

在當今快速變化的數位環境中，**優化搜尋效能** 是提供即時結果給使用者的關鍵。無論您是構建自訂搜尋引擎，或是強化現有的文件管理系統，正確的索引策略都能大幅降低延遲、減少資源消耗，並 **提升搜尋延遲**。在本教學中，我們將逐步說明 GroupDocs.Search for Java 最強大的功能——取消、非同步索引、多執行緒與中繼資料自訂——讓您能更快、更有效率地 **add documents index**。

**您將學到的內容**

- 如何在指定時間後取消索引作業  
- 執行非同步索引作業並處理狀態變更  
- 設定多執行緒以加速索引  
- 自訂中繼資料索引選項  

在深入程式碼之前，先確保您已備妥所有必需項目。

## 前置條件

- **GroupDocs.Search Library** – 版本 25.4 或更新。  
- **Java 開發環境** – 建議使用 JDK 8 以上。  
- 具備基本的 Java 知識與索引概念。

### 設定 GroupDocs.Search for Java

#### Maven 安裝

將以下儲存庫與相依性加入 `pom.xml` 檔案：

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

或是從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR。

**取得授權** – 可先使用免費試用版，或申請臨時授權以解鎖完整功能。

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
- **取消功能是什麼？** 在設定時間後停止索引，以釋放資源。  
- **可以非同步索引文件嗎？** 可以 – 設定 `options.setAsync(true)`。  
- **可以使用多少執行緒？** 任意正整數；大多數伺服器建議 2‑4 個。  
- **中繼資料索引是可選的嗎？** 絕對可以 – 您可以依欄位啟用或微調。  
- **這些功能需要授權嗎？** 試用版可供測試；正式環境需完整授權。

## 在此情境下「優化搜尋效能」是什麼意思？

優化搜尋效能指的是調整索引流程，使其在 CPU、記憶體與時間的使用上達到最佳平衡，同時即時提供最相關的結果。透過控制取消、非同步執行、執行緒與中繼資料處理，您直接影響引擎 **add documents index** 的速度與回應能力。

## 為什麼要使用進階索引功能？

- **降低延遲** – 非同步與多執行緒索引讓應用保持回應。  
- **更佳資源管理** – 取消功能防止長時間執行的程序佔用過多資源。  
- **客製化搜尋相關性** – 中繼資料選項讓您突顯最重要的資訊。  

## 如何透過進階索引改善搜尋延遲？

當您需要 **提升搜尋延遲** 時，可結合以下技巧：取消長時間執行的工作、在背景執行索引、以及將工作分散至多個 CPU 核心。這種多管齊下的方式通常能帶來最大的速度提升。

## 實作指南

### 取消屬性

**概述** – 在指定時間後取消索引，以避免過度消耗資源。

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

**概述** – 在背景執行緒上執行索引，並監聽狀態變更。

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

**概述** – 利用多個 CPU 核心加速索引。

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

**概述** – 微調哪些文件中繼資料會被索引以及其儲存方式。

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

1. **文件管理系統** – 使用非同步索引，在大量批次於背景處理時保持 UI 的回應性。  
2. **內容搜尋引擎** – 套用取消功能，防止高峰期長時間作業佔用伺服器資源。  
3. **大規模匯入管線** – 透過多執行緒 **add documents index**，大幅縮短處理時間。

## 效能考量

- **執行緒管理** – 監控 CPU 使用率；執行緒過多會產生上下文切換開銷。  
- **記憶體佔用** – 中繼資料限制（例如 `setMaxBytesToIndexField`）有助於保持記憶體使用可預測。  
- **垃圾回收** – 索引大規模語料庫時，使用適當的 JVM 參數（`-Xmx`、`-XX:+UseG1GC`）以降低 GC 影響。

## 常見問題與解決方案

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| 索引永遠不會結束 | 取消時間設定過低 | 增加 `cancelAfter` 數值或移除取消功能以處理長時間作業 |
| 非同步模式下沒有狀態更新 | 事件處理器未正確掛載 | 確認在呼叫 `index.add` 前已執行 `index.getEvents().StatusChanged.add(...)` |
| 記憶體不足錯誤 | 執行緒過多或中繼資料限制過高 | 減少 `options.setThreads` 並降低中繼資料欄位限制 |
| 結果中缺少中繼資料 | 中繼資料索引被停用 | 確認 `options.getMetadataIndexingOptions()` 已正確設定且未被忽略欄位 |

## 常見問答

**Q: 如何取得 GroupDocs.Search 的臨時授權？**  
A: 前往 [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)。

**Q: 可以在索引進行中途取消嗎？**  
A: 可以 – 使用 `cancelAfter()` 取消屬性，或在程式中呼叫 `Cancellation.cancel()`。

**Q: 非同步索引有哪些使用情境？**  
A: 即時文件檢索、背景批次處理以及需要 UI 保持回應的應用程式皆可受惠於非同步索引。

**Q: 在共享伺服器上提升執行緒數量安全嗎？**  
A: 請逐步增加並監控 CPU 負載；在高度共享的環境中，建議維持執行緒數量在 2‑4 之間。

**Q: 中繼資料索引如何影響搜尋相關性？**  
A: 正確索引的中繼資料（作者、建立日期、標籤等）可在查詢時賦予更高權重，提升結果的精確度。

## 結論

透過善用 GroupDocs.Search for Java 的這些進階功能，您將能在各種情境下 **優化搜尋效能**——從快速文件匯入到精細的中繼資料控制。請嘗試不同設定、監測資源使用，並依工作負載調整參數，以取得最佳成效。

---

**最後更新：** 2026-03-01  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs