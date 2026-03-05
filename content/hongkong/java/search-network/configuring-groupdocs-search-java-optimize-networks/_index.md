---
date: '2026-01-16'
description: 學習如何在 Java 中配置 GroupDocs 搜尋網路，並將同義詞加入索引，以提升搜尋效率。
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: 在 Java 中配置 GroupDocs.Search 網路 – 提升搜尋
type: docs
url: /zh-hant/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# 在 Java 中配置 GroupDocs.Search 網路 – 提升搜尋

在當今以資料為驅動的應用程式中，**configure groupdocs search network** 是提供快速、精確結果於龐大文件集合的關鍵步驟。無論您是建立企業級搜尋入口網站或是擴充現有解決方案，良好配置的 GroupDocs.Search 網路可讓您水平擴展、加入同義詞支援，並保持低延遲。在本教學中，您將學習如何使用 Java 設定、部署與微調 GroupDocs.Search 網路，以及加入同義詞至索引與管理節點生命週期的實用技巧。

## 快速答覆
- **配置 GroupDocs.Search 網路的主要好處是什麼？** 它允許分散式索引與查詢，提升效能與可擴展性。  
- **執行範例是否需要授權？** 免費試用可用於開發；商業授權則是正式環境的必要條件。  
- **可以在不重新建立索引的情況下加入同義詞嗎？** 可以 — 在執行期間使用同義詞字典來 **add synonyms to index**。  
- **我可以部署多少個節點？** 您可以依基礎建設的容許度部署任意數量的節點；每個節點皆在獨立的埠口上運行。  

## 什麼是配置 GroupDocs.Search 網路？
配置 GroupDocs.Search 網路是指定義資料夾結構、埠口與節點設定，使多個 JVM 實例能協同進行索引與搜尋。此設定會建立一個 master‑node，協調 workers（分片），並確保查詢在整個資料集上執行。

## 為何要配置 GroupDocs.Search 網路？
- **Scalability** – 在多台機器上分散索引負載。  
- **Reliability** – 可在不中斷服務的情況下新增或移除節點。  
- **Search relevance** – **Add synonyms to index** 以獲得更豐富的結果。  
- **Performance** – 平行查詢執行可降低回應時間。  

## 前置條件
- Java Development Kit (JDK) 8 或更新版本  
- Maven 用於建置專案  
- 具備基本的 Java 語法知識  
- 取得 GroupDocs.Search for Java 函式庫（透過 Maven 或官方發佈頁面下載）  

## 設定 GroupDocs.Search for Java

將儲存庫與相依性加入您的 Maven **pom.xml**：

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
- **Commercial License** – 正式環境部署所必需的授權。  

### 基本初始化與設定
建立一個簡易的 Java 類別，以驗證函式庫正確載入：

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

### 1. 設定搜尋網路
定義基礎文件資料夾以及節點通訊的起始埠口。

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

- **basePath** – 儲存字典（例如同義詞檔案）的路徑。  
- **basePort** – 第一個埠口；之後的節點會在此基礎上遞增。  

### 2. 部署搜尋網路節點
啟動多個共用相同設定的 worker 節點。

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

每個節點在其獨立的埠口（basePort + index）上運行，並持有整體索引的一個分片。

### 3. 訂閱節點事件
透過將事件監聽器附加至 master node，監控狀態、索引進度與錯誤情況。

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

事件回呼讓您能對節點啟動/停止、索引完成以及意外失敗作出回應。

### 4. 為節點的 Indexer 加入同義詞  
在執行期間透過 **add synonyms to index** 提升相關性。

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

### 5. 新增索引目錄
告訴 master node 哪些資料夾包含您希望可搜尋的文件。

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

此方法會遞迴掃描目錄，並將檔案分配至各分片。

### 6. 在網路中執行文字搜尋
在所有節點上執行查詢，亦可選擇強制精確匹配行為。

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

當您需要不經詞幹化的嚴格詞彙匹配時，將 `exactMatchOnly` 設為 `true`。

### 7. 關閉網路節點
處理完成後，優雅地釋放資源。

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

正確的關閉可防止記憶體洩漏，並保持 JVM 健康。

## 實務應用
| 情境 | 網路如何協助 |
|----------|-----------------------|
| **Enterprise Search** | 在資料中心伺服器上分散索引，以支援 PB 級規模語料庫。 |
| **Document Management** | 加入同義詞至索引，讓使用者即使使用不同術語也能找到文件。 |
| **E‑commerce Catalog** | 部署區域性節點，以快速提供本地化的商品搜尋。 |
| **Content Management** | 在編輯者將新檔案加入特定目錄時，仍能保持內容可搜尋。 |

## 常見問題與解決方案
- **Port Conflicts** – 確認每個節點的埠口（basePort + index）皆未被佔用；如有需要，調整 `basePort`。  
- **Synonym Not Applied** – 確認在加入詞彙後已呼叫 `indexer.setDictionary(dictionary)`。  
- **Node Not Responding** – 訂閱事件；檢查 `NodeFailed` 回呼以診斷網路問題。  
- **Memory Leak on Close** – 針對每個已部署的節點，務必呼叫 `node.close()`。  

## 常見問答

**Q: 部署多個節點如何提升搜尋效能？**  
A: 每個節點索引資料的一個分片，允許平行處理，並因工作負載分散而降低查詢延遲。

**Q: 可以在不重新索引現有文件的情況下加入同義詞嗎？**  
A: 可以，您可於執行期間透過同義詞字典 **add synonyms to index**；變更會立即對新查詢生效。

**Q: 必須訂閱節點事件嗎？**  
A: 雖非基本操作的必要條件，訂閱事件可讓您掌握節點健康狀態，並及時對失敗作出回應。

**Q: 管理節點資源的最佳實踐是什麼？**  
A: 定期關閉閒置節點、監控 JVM 記憶體使用情況，並在非高峰時段回收節點，以維持資源消耗最佳化。

**Q: GroupDocs.Search 是否支援非文字格式，如 PDF 或影像？**  
A: 當然支援。函式庫可從 PDF、Office 檔案擷取文字，甚至對影像執行 OCR，使其即時可搜尋。

**最後更新:** 2026-01-16  
**測試環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs