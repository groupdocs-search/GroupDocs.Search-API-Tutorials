---
date: '2026-09-21'
description: 了解如何在 GroupDocs.Search for Java 中建立記錄器、設定最大日誌大小，以及使用主控台記錄器。
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: 了解如何在 GroupDocs.Search for Java 中建立記錄器、設定最大日誌大小，以及使用主控台記錄器。遵循一步一步的說明並獲取最佳實踐技巧。
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: 如何在 GroupDocs.Search 中建立記錄器並限制日誌大小
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: 如何在 GroupDocs.Search for Java 中建立記錄器並限制日誌大小
type: docs
url: /zh-hant/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# 如何在 GroupDocs.Search for Java 中建立記錄器並限制日誌檔案大小

在本教學中，您將**建立記錄器**實作以用於 GroupDocs.Search，設定最大日誌檔案大小，並在基於檔案的記錄與主控台記錄之間切換。適當的日誌管理可防止在大型索引作業期間磁碟被寫滿，提升故障排除效率，並在開發時即時提供回饋。我們將從 Maven 設定開始，逐步說明記錄器配置，最後以簡單的搜尋查詢展示記錄器的運作。

## 快速解答
- **「限制日誌檔案大小」是什麼意思？** 它限制日誌檔案的最大容量，防止磁碟上無限制的增長。  
- **哪個記錄器允許限制日誌檔案大小？** 內建的 `FileLogger` 接受最大尺寸參數。  
- **如何在 Java 中使用主控台記錄器？** 建立 `ConsoleLogger` 實例並在 `IndexSettings` 上設定它。  
- **我需要 GroupDocs.Search 的授權嗎？** 試用版可用於評估；正式環境需購買商業授權。  
- **第一步是什麼？** 將 GroupDocs.Search 相依性加入您的 Maven 專案。  

## 什麼是限制日誌檔案大小？
**限制日誌檔案大小** 設定會告訴記錄器在檔案達到設定的門檻（例如 4 MB）後停止寫入新條目。當達到限制時，記錄器會捨棄後續訊息或切換到新檔案，保持磁碟使用量可預測。

## 為什麼在 GroupDocs.Search 中使用檔案與自訂記錄器？
檔案與自訂記錄器提供可稽核性、除錯洞察與彈性。在生產環境中，檔案日誌提供每一次索引與搜尋操作的永久紀錄；而主控台日誌則在開發期間即時回饋。這些日誌協助團隊監控效能、追蹤錯誤，並透過保留詳細活動記錄滿足合規需求。

## 前置條件
- GroupDocs.Search for Java ≥ 25.4。  
- JDK 8 或更新版本，搭配如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 具備 Maven 與 Java 程式開發的基本知識。  

## 設定 GroupDocs.Search for Java

使用以下任一方法將函式庫加入您的專案。

**Maven 設定：**  

```text
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
```

**直接下載：**  
從官方網站下載最新的 JAR 檔案： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權
透過 [licensing page](https://purchase.groupdocs.com/temporary-license/) 取得試用或購買授權。

## 如何為 GroupDocs.Search 建立自訂記錄器
建立自訂記錄器相當簡單，因為 GroupDocs.Search 依賴 `ILogger` 介面。實作此介面，或繼承提供的 `FileLogger` 或 `ConsoleLogger`，即可注入額外行為，例如遠端轉發或日誌輪替。您亦可加入初始化邏輯，如開啟網路連線，並確保在記錄器的關閉方法中釋放資源。此方式讓您能與 ELK 或 Splunk 等監控平台整合。

### 定義錨點
`ILogger` 是 GroupDocs.Search 的核心日誌合約；任何實作其 `log(Level, String)` 方法的類別皆可成為記錄器。

### 範例做法（無程式碼區塊）
1. 建立實作 `ILogger` 的類別。  
2. 覆寫 `log` 方法，將訊息寫入您選擇的目的地（檔案、資料庫、HTTP 端點）。  
3. 在索引設定中，呼叫 `settings.setLogger(new YourCustomLogger())`。  

## 如何使用檔案記錄器限制日誌檔案大小
`FileLogger` 類別將日誌條目寫入磁碟檔案，並接受最大尺寸參數。透過指定尺寸限制，記錄器會在達到門檻時自動停止新增條目或建立新檔案，防止磁碟無限制增長。此行為確保日誌不會干擾索引效能，同時保留簡潔的事件紀錄。

### 定義錨點
`FileLogger` 是內建的記錄器，可將訊息持久化至文字檔，並支援可設定的最大檔案大小。

### 步驟說明
1️⃣ **匯入必要的套件**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **使用檔案記錄器設定索引設定**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **建立或載入索引**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **將文件加入索引**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **執行搜尋查詢**  
```text
```java
SearchResult result = index.search(query);
```
```

**重點：**`FileLogger` 建構式的第二個參數（`4.0`）定義了以兆位元組為單位的 **設定最大日誌大小**，直接滿足 **限制日誌檔案大小** 的需求。

## 如何在 Java 中使用主控台記錄器
當您需要即時檢視日誌事件時，`ConsoleLogger` 會將每則訊息寫入 `System.out`。此記錄器輕量且執行緒安全，適合開發與除錯階段使用。它在不需檔案 I/O 的情況下即時回饋索引進度、搜尋查詢與錯誤狀況，可加速迭代測試。

### 定義錨點
`ConsoleLogger` 是輕量的記錄器，將日誌條目輸出至標準主控台串流，適合除錯階段使用。

### 設定步驟
1️⃣ **匯入主控台記錄器**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **使用主控台記錄器設定索引設定**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **建立或載入索引**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **加入文件並執行搜尋**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**提示：**主控台記錄器在開發期間非常理想，因為它會即時列印每則日誌條目，協助您驗證索引與搜尋的行為是否如預期。

## 實務應用
1. **文件管理系統：**保留每份已索引文件的稽核軌跡，符合合規需求。  
2. **企業搜尋引擎：**即時監控查詢效能與錯誤率，快速執行 SLA 合規檢查。  
3. **法律與合規軟體：**記錄搜尋關鍵字與時間戳記以供法規報告，並保留日誌至規定的保存期限。  

## 效能考量
- **日誌大小：**透過 **設定最大日誌大小**，避免過度磁碟使用，進而防止 JVM 垃圾回收器變慢。  
- **非同步日誌：**在高吞吐量情境下，將記錄器包裝於非同步佇列，以將 I/O 與索引執行緒解耦（本指南未涵蓋實作）。  
- **記憶體管理：**在不再需要時使用 `index.close()` 釋放大型 `Index` 物件，降低 JVM 記憶體佔用。  

## 常見問題與解決方案
- **日誌路徑不可存取：**確認目錄存在，且執行 JVM 的使用者帳號具有寫入權限。  
- **記錄器未觸發：**確保在建立 `Index` 物件之前呼叫 `settings.setLogger(...)`；否則會使用預設記錄器。  
- **主控台輸出缺失：**確認應用程式在能顯示 `System.out` 的終端機執行，且沒有其他日誌框架（如 SLF4J）攔截輸出。  

## 常見問答

**Q: `FileLogger` 的第二個參數控制什麼？**  
A: 它設定日誌檔案的最大容量（以兆位元組為單位），讓您能 **設定最大日誌大小**，防止無限制增長。

**Q: 我可以同時使用檔案與主控台記錄器嗎？**  
A: 可以。建立自訂記錄器，將每個 `log` 呼叫同時轉發至 `FileLogger` 與 `ConsoleLogger`，再於 `IndexSettings` 註冊此組合記錄器。

**Q: 初始建立後，如何將文件加入索引？**  
A: 隨時呼叫 `index.add(pathToNewDocs)`；已設定的記錄器會自動記錄此加入動作。

**Q: `ConsoleLogger` 是執行緒安全的嗎？**  
A: 它直接寫入 `System.out`，JVM 內部已同步處理，對於一般多執行緒使用情境是安全的。

**Q: 限制日誌檔案大小會影響儲存資訊的量嗎？**  
A: 當達到尺寸限制時，新的條目會被捨棄或記錄器切換至新檔案，取決於您選擇的實作方式。

## 資源
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**最後更新：** 2026-09-21  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs  

---

## 相關教學

- [如何實作記錄 - 例外處理與記錄教學 for GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [在 Java 中使用 GroupDocs.Search 實作非同步記錄 – 自訂記錄器指南](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [建立搜尋索引 Java – GroupDocs.Search 教學](/search/java/indexing/)