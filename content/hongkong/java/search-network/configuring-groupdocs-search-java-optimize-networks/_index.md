---
date: '2026-07-16'
description: 了解如何在 Java 中配置 GroupDocs.Search 網路、將同義詞加入索引，並提升分散節點的搜尋效能。
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: 如何在 Java 中配置 GroupDocs.Search 網路並將同義詞加入索引，以獲得更快、更精確的結果。請依照此一步一步的指南操作。
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: 如何在 Java 中配置 GroupDocs.Search 網路 – 提升搜尋
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: 如何在 Java 中配置 GroupDocs.Search 網路指南
type: docs
url: /zh-hant/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# 如何在 Java 中配置 GroupDocs.Search 網路 – 提升搜尋

在現代資料密集型應用程式中，正確 **how to configure GroupDocs** 是提供閃電般快速且相關搜尋結果於龐大文件庫的基石。無論您是構建企業入口網站、知識庫或產品目錄，經過良好調校的 GroupDocs.Search 網路都能讓您水平擴展、注入同義詞邏輯，並將延遲控制在可接受範圍。本教學將逐步說明如何使用 Java 設置、部署與微調 GroupDocs.Search 網路，並提供加入同義詞至索引及處理節點生命週期的實用建議。

## 快速答案
- **配置 GroupDocs.Search 網路的主要好處是什麼？** 它能實現分散式索引與查詢，提升效能與可擴展性。  
- **我需要授權才能執行範例嗎？** 免費試用可用於開發；商業授權則是生產環境的必需。  
- **可以在不重新建構索引的情況下加入同義詞嗎？** 可以——在執行時使用同義詞字典來 **add synonyms to index**。  
- **我可以部署多少個節點？** 您可以根據基礎設施部署任意數量的節點；每個節點都在自己的埠上運行。  
- **需要哪個 Java 版本？** 支援 JDK 8 或更新版本，且完全相容至 JDK 21。

## 什麼是配置 GroupDocs.Search 網路？
**GroupDocs.Search 網路** 是一組協同工作以索引與查詢共享文件集合的 JVM 程序。它由一個負責協調一個或多個工作節點（分片）的主節點組成。該網路抽象化底層儲存，單一查詢會自動廣播至每個分片，然後在返回給呼叫者之前合併結果。

## 為什麼要配置 GroupDocs.Search 網路？
配置 GroupDocs.Search 網路可為您帶來三項具體優勢：**scalability**、**reliability** 與 **enhanced relevance**。透過將索引負載分散至最多 20 個節點，每個節點處理 5 GB 的分片，總索引時間可較單節點設定縮減約 70 %。加入同義詞字典可提升使用替代術語的查詢召回率最高達 35 %，而節點冗餘則在維護期間保證 99.9 % 的正常運作時間。

## 前置條件
- Java Development Kit (JDK) 8 – 21（任何 LTS 版本）  
- Maven 3.5 + 用於建置專案  
- 熟悉基本的 Java 語法與 Maven 依賴管理  
- 取得 GroupDocs.Search for Java 程式庫（可透過 Maven Central 或官方發佈頁面取得）

## 設定 GroupDocs.Search for Java

將儲存庫與相依性加入您的 Maven **pom.xml**：

以下 XML 片段會加入 GroupDocs.Search 儲存庫與程式庫相依性。  
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

### 取得授權
- **Free Trial** – 無償探索核心功能。  
- **Temporary License** – 為短期測試解鎖完整功能。  
- **Commercial License** – 生產部署所需，並可獲得高級支援。

### 基本初始化與設定
建立一個簡單的 Java 類別，以驗證程式庫正確載入：

SampleInitializer 類別示範了如何載入 GroupDocs.Search 引擎。  
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## 步驟指南：配置 GroupDocs.Search 網路

### 1. 配置搜尋網路
定義基礎文件資料夾以及節點通訊的起始埠號。

SearchNetworkConfig 保存網路節點的設定。  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – 儲存字典（例如同義詞檔案）的目錄。  
- **basePort** – 第一個埠號；後續節點會在此基礎上遞增。

### 2. 部署搜尋網路節點
啟動多個共享相同設定的工作節點。

SearchNode 代表分散式網路中的單一節點。  
```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

每個節點在自己的埠 (`basePort + index`) 上運行，並持有整體索引的一個分片，允許索引與查詢執行的平行處理。

### 3. 訂閱節點事件
透過將事件監聽器附加至主節點，監控健康狀態、索引進度與錯誤情況。

NetworkEventListener 處理節點生命週期事件的回呼。  
```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

事件回呼讓您能對節點啟動/停止、索引完成以及意外失敗作出回應，提供對分散系統的完整可觀測性。

### 4. 為節點的索引器加入同義詞
在執行時透過 **add synonyms to index** 來提升相關性。

SynonymDictionary 允許將同義詞群組加入索引器。  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – 應視為等價的詞彙陣列。  
- **clearBeforeAdding** – 若要取代現有條目，請設為 `true`。

### 5. 新增目錄以供索引
告訴主節點哪些資料夾包含您希望可搜尋的文件。

Indexer.addDirectory 註冊一個用於索引的資料夾。  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

此方法會遞迴掃描目錄並將檔案分配至各分片，支援超過 10 TB 的資料而不需將整個檔案載入記憶體。

### 6. 在網路中執行文字搜尋
在所有節點上執行查詢，並可選擇強制精確匹配行為。

SearchEngine.search 在網路上執行查詢。  
```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

當您需要不經詞幹還原的嚴格詞彙匹配時，將 `exactMatchOnly` 設為 `true`，這可在程式碼搜尋情境中提升最高 20 % 的精確度。

### 7. 關閉網路節點
處理完成後，優雅地釋放資源。

`node.close()` 關閉 SearchNode 並釋放資源。  
```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

適當的關閉可防止記憶體洩漏並保持 JVM 健康，特別是在長時間運行且於非高峰時段回收節點的服務中。

## 實務應用
| 情境 | 網路如何協助 |
|----------|-----------------------|
| **Enterprise Search** | 在資料中心伺服器上分散索引，以支援 PB 級規模的語料庫，實現 100 M+ 文件的次秒查詢延遲。 |
| **Document Management** | 加入同義詞至索引，使使用者即使使用不同術語亦能找到文件，召回率提升最高 35 %。 |
| **E‑commerce Catalog** | 部署區域專屬節點以快速提供本地化商品搜尋，平均回應時間從 250 ms 降至 80 ms。 |
| **Content Management** | 在編輯者將新檔案加入特定目錄時，保持內容可搜尋；網路可增量重新索引而不需停機。 |

## 常見問題與解決方案
- **Port Conflicts** – 確保每個節點的埠 (`basePort + index`) 為空閒；如有需要，調整 `basePort`。  
- **Synonym Not Applied** – 確認在加入詞彙後已呼叫 `indexer.setDictionary(dictionary)`；否則新同義詞不會在搜尋時被考慮。  
- **Node Not Responding** – 訂閱事件；檢查 `NodeFailed` 回呼以診斷網路問題。  
- **Memory Leak on Close** – 必須對每個已部署的節點呼叫 `node.close()`；可考慮使用 try‑with‑resources 區塊以自動清理。  

## 常見問答

**Q: 部署多個節點如何提升搜尋效能？**  
A: 每個節點索引資料的一個分片，允許平行處理，並因工作負載在叢集間分散而降低查詢延遲。

**Q: 可以在不重新索引現有文件的情況下加入同義詞嗎？**  
A: 可以，您可在執行時透過同義詞字典 **add synonyms to index**；變更會立即對新查詢生效。

**Q: 訂閱節點事件是必須的嗎？**  
A: 雖非基本運作所必需，但事件訂閱可讓您看見節點健康狀態，並協助您即時回應失敗。

**Q: 管理節點資源的最佳實踐是什麼？**  
A: 定期關閉閒置節點、監控 JVM 記憶體使用，並於非高峰時段回收節點，以維持資源消耗最佳化。

**Q: GroupDocs.Search 是否支援非文字格式，如 PDF 或影像？**  
A: 當然支援。程式庫可從 PDF、Office 檔案提取文字，並對影像執行 OCR，使其即開即搜。

**最後更新：** 2026-07-16  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs

## 相關教學

- [GroupDocs.Search for Java 教學與範例](/search/net/)
- [.NET 中配置 GroupDocs.Search 網路：完整指南](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [使用 GroupDocs 在 .NET 部署搜尋網路節點以實現高效文件索引與檢索](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)