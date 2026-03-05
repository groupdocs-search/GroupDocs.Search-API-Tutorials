---
date: '2026-02-24'
description: 了解如何在 GroupDocs.Search for Java 中建立自訂記錄器、設定最大日誌大小，以及配置主控台或檔案記錄器。
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: 如何使用 GroupDocs.Search Java 建立自訂記錄器並限制日誌檔案大小
type: docs
url: /zh-hant/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# 限制 GroupDocs.Search Java 記錄器的日誌檔案大小

在本指南中，您將 **建立自訂 logger** 實作，並學習在使用 GroupDocs.Search for Java 時 **限制日誌檔案大小**。控制日誌增長對於大規模文件索引至關重要，內建的 logger 允許您 **設定最大日誌大小**、**輪替日誌檔案**，或切換為 **使用 console logger** 以即時取得回饋。讓我們從 Maven 設定到執行搜尋查詢，完整示範如何在加入文件索引時使用 logger。

## 快速回答
- **「限制日誌檔案大小」是什麼意思？** 它會限制日誌檔案的最大容量，防止磁碟上無限制增長。  
- **哪個 logger 可以限制日誌檔案大小？** 內建的 `FileLogger` 接受最大容量參數。  
- **如何使用 console logger java？** 建立 `ConsoleLogger` 並在 `IndexSettings` 上設定它。  
- **使用 GroupDocs.Search 是否需要授權？** 試用版可供評估；正式環境需購買商業授權。  
- **第一步是什麼？** 將 GroupDocs.Search 相依性加入您的 Maven 專案。

## 什麼是限制日誌檔案大小？
限制日誌檔案大小是指設定 logger，使得當檔案達到預先定義的門檻（例如 4 MB）時，停止增長或進行輪替。這可讓您的應用程式儲存空間使用保持可預測，避免效能下降。

## 為什麼在 GroupDocs.Search 中使用檔案與自訂 logger？
- **可稽核性：** 保留索引與搜尋事件的永久紀錄。  
- **除錯：** 透過精簡的日誌快速定位問題。  
- **彈性：** 可在永久檔案日誌與即時 console 輸出（`use console logger`）之間選擇。

## 前置條件
- **GroupDocs.Search for Java** ≥ 25.4。  
- JDK 8 或更新版本，IDE（IntelliJ IDEA、Eclipse 等）。  
- 基本的 Java 與 Maven 知識。

## 設定 GroupDocs.Search for Java

使用以下任一方式將函式庫加入專案。

**Maven 設定：**

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
從官方網站下載最新 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 授權取得
透過 [licensing page](https://purchase.groupdocs.com/temporary-license/) 取得試用或購買正式授權。

## 如何為 GroupDocs.Search 建立自訂 logger
GroupDocs.Search 允許您插入任何實作 `ILogger` 介面的類別。透過繼承 `FileLogger` 或 `ConsoleLogger`，您可以加入額外行為——例如輪替日誌檔案或將訊息轉發至遠端監控服務。正因如此，許多團隊 **建立自訂 logger** 以符合其營運需求。

## 如何使用 File Logger 限制日誌檔案大小
以下為逐步說明，示範如何 **設定檔案 logger**，使日誌檔案永不超過您指定的大小。

### 1️⃣ 匯入必要的套件
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ 使用 File Logger 設定 Index Settings
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

**重點：** `FileLogger` 建構子第二個參數（`4.0`）即為 **設定最大日誌大小**（單位為 MB），直接滿足 **限制日誌檔案大小** 的需求。

## 如何使用 console logger java
如果您希望在終端機即時取得回饋，只需將檔案 logger 換成 console logger。

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

**小技巧：** console logger 在開發階段非常理想，因為它會即時印出每筆日誌，協助您驗證索引與搜尋的行為是否如預期。

## 實務應用
1. **文件管理系統：** 為每個被索引的文件保留稽核追蹤。  
2. **企業搜尋引擎：** 即時監控查詢效能與錯誤率。  
3. **法律與合規軟體：** 記錄搜尋關鍵字以供法規報告使用。

## 效能考量
- **日誌大小：** 透過 **設定最大日誌大小**，避免過度磁碟使用導致應用程式變慢。  
- **非同步記錄：** 若需更高吞吐量，可考慮將 logger 包裝於非同步佇列（本指南未涵蓋）。  
- **記憶體管理：** 當 `Index` 物件不再使用時釋放，以降低 JVM 記憶體佔用。

## 常見問題與解決方案
- **日誌路徑無法存取：** 確認目錄已存在且應用程式具備寫入權限。  
- **logger 未觸發：** 確保在建立 `Index` 物件 *之前* 呼叫 `settings.setLogger(...)`。  
- **console 輸出缺失：** 確認您是在能顯示 `System.out` 的終端機執行程式。

## 常見問答

**Q: `FileLogger` 的第二個參數控制什麼？**  
A: 它設定日誌檔案的最大容量（單位 MB），讓您 **設定最大日誌大小**。

**Q: 我可以同時使用檔案與 console logger 嗎？**  
A: 可以，透過自訂 logger 同時將訊息轉發至兩個目的地。

**Q: 如何在初始建立之後再加入文件到索引？**  
A: 隨時呼叫 `index.add(pathToNewDocs)`；logger 會記錄此操作。

**Q: `ConsoleLogger` 是否具備執行緒安全性？**  
A: 它直接寫入 `System.out`，而 `System.out` 由 JVM 同步處理，對大多數情境而言是安全的。

**Q: 限制日誌檔案大小會影響資訊儲存量嗎？**  
A: 當達到大小上限時，新的條目可能被捨棄或依 logger 實作 **輪替日誌檔案**。

## 資源
- [Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**最後更新：** 2026-02-24  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs