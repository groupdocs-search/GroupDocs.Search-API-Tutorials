---
date: '2026-09-27'
description: 了解如何使用 GroupDocs.Search for Java 實作 Java 全文搜尋、加入檔案以供搜尋、設定目錄，並啟用即時索引。
keywords:
- java full text search
- event driven indexing
- java search engine
- add files to search
- real time indexing java
lastmod: '2026-09-27'
og_description: 使用 GroupDocs.Search 實作 Java 全文搜尋。了解如何加入檔案、設定節點，並在數分鐘內啟用即時索引。
og_image_alt: Guide to setting up java full text search with GroupDocs.Search
og_title: 如何使用 GroupDocs.Search 在 Java 中實作全文搜尋
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to implement java full text search using GroupDocs.Search
    for Java, add files to search, configure directories, and enable real time indexing.
  headline: How to implement java full text search with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: Yes. The library works with any Java runtime, and you can point `basePath`
      to a network‑mounted folder or a cloud storage mount.
    question: Can I use GroupDocs.Search on a cloud‑based Java application?
  - answer: Subscribe to node events (see Feature 3) and call `addFiles` or `addDirectories`
      again for the modified paths.
    question: How do I update the index when a file changes?
  - answer: Practically, the limit is defined by your hardware and network bandwidth.
      The API imposes no hard cap.
    question: Is there a limit to the number of nodes I can deploy?
  - answer: No. Adding files triggers indexing automatically; you only need to commit
      if you defer the operation.
    question: Do I need to restart nodes after adding new files?
  - answer: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, and many image types—over
      50 formats in total.
    question: Which document formats are supported out of the box?
  type: FAQPage
tags:
- java full text search
- GroupDocs.Search
- search indexing
title: 如何使用 GroupDocs.Search 在 Java 中實作全文搜尋
type: docs
url: /zh-hant/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 GroupDocs.Search 實作 Java 全文搜尋

在資料驅動的應用程式時代，**java full text search** 是將龐大的文件集合轉換為即時可搜尋知識庫的關鍵。無論您是構建企業級入口網站或輕量級桌面工具，良好配置的搜尋網路都能將查詢延遲從秒級降低至毫秒級，並在資料增長時保持結果相關性。本教學將帶您部署 **GroupDocs.Search for Java**、將檔案加入搜尋、在節點上配置目錄，並啟用即時索引，使索引保持最新，無需手動干預。

> **為何重要：** A java full text search index reduces query latency, scales with data volume, and brings powerful full‑text capabilities to any Java‑based solution—web portals, desktop apps, or cloud microservices.

## 快速回答
- **GroupDocs.Search 的主要目的為何？** 它提供可擴展的 java 搜尋引擎，能在分散式網路中索引與搜尋文件。  
- **我應該使用哪個版本？** 建議在新專案中使用最新的穩定版（例如 25.4）。  
- **我需要授權嗎？** 提供 30 天免費試用；正式環境需購買永久授權。  
- **我可以同時新增檔案與整個目錄嗎？** 是 — 使用 `addFiles` 與 `addDirectories` 輔助方法來匯入內容。  
- **需要哪個 Java 版本？** Java 8 或更高版本，並使用 Maven 進行相依管理。  
- **即時索引 java 如何運作？** 透過訂閱節點事件，可在檔案變更時自動觸發重新索引。

## 什麼是「create searchable index java」？
在 Java 中建立可搜尋索引意味著構建一個資料結構，將詞彙映射到包含它們的文件，以實現快速的全文查詢。**GroupDocs.Search for Java** 抽象化繁重的工作，讓您專注於提供文件與調整搜尋行為。

## 為何使用 GroupDocs.Search for Java？
GroupDocs.Search 提供可水平擴展的 java 搜尋引擎，支援超過 50 種輸入與輸出格式，並提供事件驅動的索引功能。部署多個節點可分散索引工作負載，內建健康檢查確保網路可靠。同時提供 RESTful API 與可自訂的分析器，以微調相關性。

## 前置條件
- **JDK 8+** 已安裝於您的開發機器上。  
- 開發環境（IDE），例如 **IntelliJ IDEA** 或 **Eclipse**。  
- 具備 **Java** 與 **Maven** 的基本知識。  
- 取得 **GroupDocs.Search for Java** 函式庫（下載或 Maven）。

## 設定 GroupDocs.Search for Java

### Maven 相依性
將儲存庫與相依性加入您的 `pom.xml`：

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

> **小技巧：** 透過檢查官方發行頁面，保持版本號為最新。

您也可以直接從官方網站下載 JAR：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權
- **Free trial（免費試用）：** 30 天評估。  
- **Temporary license（臨時授權）：** 申請延長測試。  
- **Purchase（購買）：** 生產環境部署必須購買。

### 基本初始化
建立一個配置物件，指向儲存索引檔案的資料夾，並定義基礎通訊埠：

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## 如何使用 GroupDocs.Search 建立 searchable index java？
載入 `SearchConfiguration` 物件，啟動 `SearchNetworkNode`，並呼叫 `node.getIndexer().addFiles(...)` 以填充索引。此單行程式碼即可啟動完整功能的 java 全文搜尋網路，立即接受查詢。之後可透過新增共享相同基礎路徑與埠範圍的節點來擴展規模。

### 功能 1 – 配置與網路設定
`SearchConfiguration` 類別保存啟動節點所需的所有設定。

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – 索引資料將被持久化的目錄。  
- **`basePort`** – 起始埠號；每個節點會在此基礎上遞增。

### 功能 2 – 部署搜尋網路節點
`SearchNetworkNode` 代表可在任何機器上執行的單一索引服務。

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

`SearchNetworkNode` 是承載索引、處理新增/移除事件並回應搜尋查詢的核心執行元件。部署多個節點可讓您 **create java full text search** 叢集水平擴展。

### 功能 3 – 訂閱節點事件
即時更新可使索引與檔案系統變更保持同步。

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

透過監聽事件，當新檔案到達時可自動觸發重新索引，實現 **event driven indexing**，無需手動腳本。

### 功能 4 – 向網路節點新增目錄
使用此輔助方法 **add directories to node**，遞迴收集所有支援的文件。

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### 功能 5 – 向網路節點新增檔案
當您需要細緻控制時，可逐一 **add files to search**：

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 常見使用情境
- **企業文件入口網站** 需要在數千個 PDF 與 Office 檔案中即時搜尋。  
- **法律電子取證平台** 持續新增證據，且必須即時可搜尋。  
- **內容管理系統** 儲存影像、簡報與試算表，且需要全文查詢。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|--------|-----|
| **搜尋結果未顯示文件** | 索引未提交 | 在新增檔案後呼叫 `node.getIndexer().commit()`。 |
| **埠衝突錯誤** | 其他服務使用 `basePort` | 選擇不同的 `basePort` 或確認埠是否空閒。 |
| **不支援的檔案格式** | 函式庫缺少解析器 | 確保檔案副檔名受支援，或加入自訂擷取器。 |

## 疑難排解技巧
- **驗證節點健康狀態：** 使用內建健康檢查端點 (`http://localhost:{port}/health`) 以確認每個節點正在運行。  
- **監控記憶體使用量：** 大批量文件可能導致記憶體激增；請分批索引並定期呼叫 `commit()`。  
- **檢查日誌：** GroupDocs.Search 會將詳細日誌寫入 `basePath` 資料夾——檢視其中的解析錯誤或網路逾時資訊。

## 常見問答

**Q: 我可以在雲端 Java 應用程式中使用 GroupDocs.Search 嗎？**  
A: 可以。此函式庫相容任何 Java 執行環境，且可將 `basePath` 指向網路掛載的資料夾或雲端儲存掛載點。

**Q: 檔案變更時，我該如何更新索引？**  
A: 訂閱節點事件（參見功能 3），並對已修改的路徑再次呼叫 `addFiles` 或 `addDirectories`。

**Q: 我可以部署的節點數量有限制嗎？**  
A: 實務上受限於硬體與網路頻寬，API 本身沒有硬性上限。

**Q: 新增檔案後需要重新啟動節點嗎？**  
A: 不需要。新增檔案會自動觸發索引；若延遲提交，僅需呼叫 commit。

**Q: 預設支援哪些文件格式？**  
A: PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、TXT、HTML 以及多種影像類型——總計超過 50 種格式。

**Q: 如何為持續接收上傳的資料夾啟用即時索引 java？**  
A: 實作檔案系統監控器（例如 `java.nio.file.WatchService`），在偵測到新檔案時呼叫 `DirectoryAdder.addDirectories(node, path)`。

---

**最後更新：** 2026-09-27  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs

## 相關教學

- [如何實作 java 全文搜尋：使用 GroupDocs.Search 建立索引目錄](/search/java/indexing/groupdocs-search-java-create-index/)
- [在 Java 中實作全文搜尋：GroupDocs Search](/search/java/searching/implement-full-text-search-java-groupdocs-search/)
- [如何在 Java 中使用 GroupDocs.Search 配置搜尋 - 配置與部署指南](/search/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}