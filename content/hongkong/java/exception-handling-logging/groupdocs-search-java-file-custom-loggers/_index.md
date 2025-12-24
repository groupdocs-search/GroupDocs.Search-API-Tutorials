---
date: '2025-12-24'
description: 了解如何限制日誌檔案大小以及在 GroupDocs.Search for Java 中使用 Java 控制台記錄器。本指南涵蓋日誌設定、故障排除技巧與效能優化。
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: 使用 GroupDocs.Search Java 記錄器限制日誌檔案大小
type: docs
url: /zh-hant/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# 限制日誌檔案大小的 GroupDocs.Search Java 記錄器

在管理大型文件集合時，高效的日誌記錄至關重要，特別是當您需要 **限制日誌檔案大小** 以控制儲存空間時。**GroupDocs.Search for Java** 提供強大的解決方案，透過其強大的搜尋功能處理日誌。本教學指導您如何使用 GroupDocs.Search 實作檔案與自訂記錄器，提升應用程式追蹤事件與除錯問題的能力。

## 快速解答
- **「限制日誌檔案大小」是什麼意思？** 它會限制日誌檔案的最大容量，防止磁碟上無限制增長。  
- **哪個記錄器可以限制日誌檔案大小？** 內建的 `FileLogger` 接受最大容量參數。  
- **如何在 Java 中使用 console logger？** 建立 `ConsoleLogger` 並將其設定於 `IndexSettings`。  
- **我需要 GroupDocs.Search 的授權嗎？** 試用版可用於評估；正式環境需購買商業授權。  
- **第一步是什麼？** 將 GroupDocs.Search 相依性加入您的 Maven 專案。

## 什麼是限制日誌檔案大小？
限制日誌檔案大小是指設定記錄器，使檔案在達到預先定義的門檻（例如 4 MB）後停止增長或進行輪替。這可讓您的應用程式儲存空間使用保持可預測，並避免效能下降。

## 為何在 GroupDocs.Search 中使用檔案與自訂記錄器？
- **可審計性：** 保留索引與搜尋事件的永久記錄。  
- **除錯：** 透過檢視精簡的日誌快速定位問題。  
- **彈性：** 可在持久檔案日誌與即時 console 輸出（`use console logger java`）之間選擇。  

## 前置條件
- **GroupDocs.Search for Java** ≥ 25.4。  
- JDK 8 或更新版本，IDE（IntelliJ IDEA、Eclipse 等）。  
- 具備基本的 Java 與 Maven 知識。  

## 設定 GroupDocs.Search for Java

使用以下任一方法將函式庫加入您的專案。

**Maven Setup**

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

**直接下載：**  
從官方網站下載最新的 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權
取得試用版或透過 [授權頁面](https://purchase.groupdocs.com/temporary-license/) 購買授權。

## 如何使用檔案記錄器限制日誌檔案大小
以下是逐步指南，說明如何設定 `FileLogger`，使日誌檔案永不超過您指定的大小。

### 1️⃣ 匯入必要的套件
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ 使用檔案記錄器設定 Index Settings
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ 建立或載入 Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ 將文件加入 Index
```java
index.add(documentsFolder);
```

### 5️⃣ 執行搜尋查詢
```java
SearchResult result = index.search(query);
```

**重點：** `FileLogger` 建構子中的第二個參數（`4.0`）定義了以 MB 為單位的最大日誌檔案大小，直接滿足 **限制日誌檔案大小** 的需求。

## 如何在 Java 中使用 console logger
如果您希望在終端機中即時取得回饋，可將檔案記錄器換成 console 記錄器。

### 1️⃣ 匯入 Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ 使用 Console Logger 設定 Index Settings
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ 建立或載入 Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ 加入文件並執行搜尋
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**提示：** console 記錄器在開發期間非常理想，因為它會即時列印每筆日誌，協助您驗證索引與搜尋的行為是否如預期。

## 實務應用
1. **文件管理系統：** 保留每個已索引文件的審計追蹤。  
2. **企業搜尋引擎：** 即時監控查詢效能與錯誤率。  
3. **法律與合規軟體：** 記錄搜尋關鍵字以供法規報告。  

## 效能考量
- **日誌大小：** 透過限制日誌檔案大小，可避免過度磁碟使用，防止應用程式變慢。  
- **非同步記錄：** 若需要更高吞吐量，可考慮將記錄器包裝於非同步佇列中（本指南未涵蓋）。  
- **記憶體管理：** 在 `Index` 物件不再需要時釋放，以降低 JVM 記憶體佔用。  

## 常見問題與解決方案
- **日誌路徑無法存取：** 確認目錄存在且應用程式具備寫入權限。  
- **記錄器未觸發：** 確保在建立 `Index` 物件 *之前* 呼叫 `settings.setLogger(...)`。  
- **Console 輸出缺失：** 確認您在能顯示 `System.out` 的終端機執行應用程式。  

## 常見問答

**Q: `FileLogger` 的第二個參數控制什麼？**  
A: 它設定日誌檔案的最大大小（以 MB 為單位），讓您能限制日誌檔案大小。

**Q: 我可以同時使用檔案與 console 記錄器嗎？**  
A: 可以，透過建立自訂記錄器將訊息同時轉發至兩個目的地。

**Q: 初始建立後，如何將文件加入 index？**  
A: 隨時呼叫 `index.add(pathToNewDocs)`；記錄器會記錄此操作。

**Q: `ConsoleLogger` 是執行緒安全的嗎？**  
A: 它直接寫入 `System.out`，而 `System.out` 由 JVM 同步，對大多數使用情境而言是安全的。

**Q: 限制日誌檔案大小會影響儲存資訊的量嗎？**  
A: 當達到大小上限時，新的條目可能會被丟棄或檔案會輪替，這取決於記錄器的實作方式。

## 資源
- [文件說明](https://docs.groupdocs.com/search/java/)
- [API 參考文件](https://reference.groupdocs.com/search/java/)

---

**最後更新：** 2025-12-24  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs