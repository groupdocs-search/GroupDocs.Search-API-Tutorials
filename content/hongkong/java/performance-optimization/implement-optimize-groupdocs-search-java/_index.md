---
date: '2026-07-07'
description: 了解如何使用 GroupDocs.Search for Java 刪除索引、執行 Java 全文搜尋，並優化搜尋效能。提供設定搜尋網絡與建立索引的逐步指南。
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: 如何使用 GroupDocs.Search 刪除索引並執行 Java 全文搜尋。請依照本指南設定搜尋網絡、建立可搜尋的索引，並優化搜尋效能。
og_title: 如何刪除索引並使用 GroupDocs.Search for Java 進行文字搜尋
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: 如何刪除索引並使用 GroupDocs.Search for Java 進行文字搜尋
type: docs
url: /zh-hant/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# 如何刪除索引並使用 GroupDocs.Search for Java 執行文字搜尋

在當今以數據為驅動的世界中，快速 **how to delete index** 同時提供閃電般的 Java 全文搜尋功能是一項競爭優勢。無論您是建立內部知識庫、法律案件儲存庫，或是電商產品目錄，良好調校的搜尋網路都能顯著提升使用者滿意度。在本指南中，您將學習如何 **設置搜尋網路**、**建立可搜尋的索引**、**優化搜尋效能**，以及在需要時 **從索引中刪除文件**——全部使用 GroupDocs.Search for Java。

## 快速答案
- **GroupDocs.Search for Java 的主要目的為何？** 它提供跨超過 50 種文件格式的全文搜尋，實現快速關鍵字檢索。  
- **如何在分散式環境中執行文字搜尋？** 部署搜尋網路，在主節點建立文件索引，然後向任何節點查詢。  
- **我可以在不重新建構索引的情況下刪除索引中的文件嗎？** 可以，使用 Delete API 刪除選定的檔案，實際上就是 *how to delete index* 而無需完整重新索引。  
- **需要哪個 Java 版本？** JDK 8 或更高。  
- **生產環境是否需要授權？** 需要有效的 GroupDocs.Search 授權；亦提供免費試用。  

## 什麼是「執行文字搜尋」？
執行文字搜尋是指對全文索引進行查詢，以取得包含指定關鍵字或片語的文件。GroupDocs.Search 會建立倒排索引，使這類查找即使在數千個檔案中也能極速完成。

## 為何要設置搜尋網路？
搜尋網路會將索引與查詢工作負載分散至多個節點，讓您能 **優化搜尋效能**、水平擴展，並維持高可用性。此架構非常適合對延遲與吞吐量有要求的企業級文件儲存庫。

## 如何使用 GroupDocs.Search for Java 實作與優化搜尋網路
載入您的設定，啟動主節點，然後新增共享相同基礎路徑與埠號的工作節點。以此方式部署網路，可讓任何節點處理索引或查詢請求，即使文件數量增至數十萬，也能提供一致的回應時間。

### 步驟概覽
- **定義基礎設定**，其中包含共享目錄與 TCP 埠號。  
- **啟動主節點**，以管理索引並協調工作節點。  
- **新增工作節點**，連接至主節點，實現平行索引與搜尋。  
- **監控資源使用情況**，並調整 JVM 堆積設定以降低延遲。  

## 如何在 GroupDocs.Search for Java 中刪除索引
`SearchNode` 代表 GroupDocs.Search 網路中的一個節點，負責管理索引與查詢操作。`delete` 方法會從索引中移除指定的文件。

### 直接刪除步驟
- 在 `SearchNode` 實例上呼叫 `delete` 方法。  
- 提供相對檔案路徑的陣列。  
- 提交變更；索引會立即刷新，後續搜尋將不再返回已移除的檔案。  

## 什麼是搜尋網路？
**搜尋網路** 是由相互連接的節點所組成的叢集，共享同一索引儲存庫，允許分散式索引與查詢執行。它為大規模文件集合提供水平擴展與容錯能力。

## 如何建立可搜尋的索引（index documents java）
`add` 方法會將文件索引至搜尋索引中。使用 `add` 方法將文件加入主節點；網路會將變更傳播至所有工作節點。此方式確保每個節點皆能對最新索引提供查詢，且無需額外同步步驟。

### 主要動作
- 將主節點指向包含來源檔案的資料夾。  
- 呼叫索引例行程序；網路會處理每個檔案並更新倒排索引。  
- 確認索引檔案出現在指定的儲存目錄中。  

## 如何移除已索引的檔案（remove indexed files）
當文件過時時，使用其路徑呼叫 `delete` API。系統會從倒排索引中移除該檔案的條目，釋放儲存空間並防止過時結果。

## 設定 GroupDocs.Search for Java
首先，使用以下設定將 GroupDocs.Search 整合至您的 Java 專案中：

### Maven 設定
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

### 直接下載
或者，您可以直接從 GroupDocs [下載最新版本直接從 GroupDocs](https://releases.groupdocs.com/search/java/)。

### 取得授權
GroupDocs 提供免費試用，讓您在購買前評估其功能。您可依照其 [購買頁面](https://purchase.groupdocs.com/temporary-license/) 的步驟取得臨時授權。這將在測試階段啟用完整功能。

### 基本初始化與設定
在您的 Java 應用程式中使用以下程式碼初始化 GroupDocs.Search：

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## 實作指南

### 設定搜尋網路
**概覽：** 為您的搜尋網路建立基礎路徑與埠號，使節點能有效通訊。

#### 步驟 1：定義基礎設定
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **參數：**  
  - `basePath`：網路操作的目錄路徑。  
  - `basePort`：搜尋網路使用的埠號。  

#### 步驟 2：故障排除
確保您指定的埠號未被防火牆阻擋或被其他應用程式佔用。必要時進行調整以避免衝突。

### 部署搜尋網路節點
**概覽：** 使用您的設定，在網路中部署節點以進行分散式索引與搜尋。

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **主要設定選項：**  
  - **基礎路徑與埠號：** 這些值應與您最初的設定相符，以確保一致性。  

### 索引文件（`create searchable index`）
**概覽：** 使用主節點有效地將文件加入搜尋索引。

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **目的：**  
  - `masterNode`：管理文件索引的主要節點。  
  - `documentsPath`：包含文件的目錄路徑。  

#### 故障排除提示
確認您的文件路徑正確且可存取。確保權限允許從這些目錄讀取。

### 在網路中搜尋文字（`perform text search`）
**概覽：** 在已索引的網路中執行全面的文字搜尋。

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **參數：**  
  - `query`：您要搜尋的文字。  
  - `masterNode`：執行搜尋的節點。  

### 從索引中刪除文件（`delete documents index`）
**概覽：** 使用檔案路徑從索引中移除特定文件。

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **方法目的：**  
  - `node`：執行刪除操作的目標節點。  
  - `filePaths`：要從索引中移除的文件路徑。  

#### 故障排除
確保檔案路徑精確且檔案確實存在於目錄中。若問題持續，請檢查網路權限與連線情況。

## 實務應用
- **企業文件管理：** 簡化內部知識檢索。  
- **法律案件分析：** 快速在多個儲存庫中定位相關案件檔案。  
- **電商平台：** 透過索引說明與評論提升產品搜尋速度。  
- **學術研究：** 高效搜尋大型數位圖書館的論文與論文集。  
- **客服系統：** 讓客服人員即時搜尋過往工單，縮短回應時間。  

## 效能考量
- **優化索引速度：** 在非高峰時段逐步新增文件，以保持低延遲。  
- **資源使用指導原則：** 監控 CPU 與記憶體，特別是在擴充節點數量時。  
- **Java 記憶體管理：** 根據工作負載調整 JVM 堆積設定（例如，中等規模索引使用 `-Xmx2g`）。  

## 結論
透過本指南，您已學會如何 **設置搜尋網路**、**建立可搜尋的索引**、**執行文字搜尋**，以及使用 GroupDocs.Search for Java **刪除文件索引**。這些功能讓您在分散式環境中實現快速且可靠的文件檢索。

**後續步驟**
- 嘗試不同的節點配置，以找到最適合您工作負載的平衡點。  
- 深入研究進階索引選項，如自訂分析器與相關性調整。  
- 探索與其他 GroupDocs 產品的整合，以實現端對端的文件處理。  

## 常見問題

**Q: GroupDocs.Search for Java 的主要使用情境是什麼？**  
A: 它提供跨多種文件格式的全文搜尋，讓您能在大型儲存庫中 **執行文字搜尋**。

**Q: 如何提升大型網路的搜尋速度？**  
A: 部署更多節點、調整 JVM 堆積，並在低流量時段排程索引，以 **優化搜尋效能**。

**Q: 是否可以在不重新索引整個集合的情況下刪除單一文件？**  
A: 可以，使用如程式碼範例所示的 **delete documents index** API 來移除特定檔案。

**Q: 開發階段是否需要授權？**  
A: 免費試用授權足以進行測試；商業授權則在生產部署時必須取得。

**Q: 我可以同時索引 PDF、Word 檔案與電子郵件嗎？**  
A: 當然可以——GroupDocs.Search 內建支援多種格式。

---

**最後更新：** 2026-07-07  
**測試版本：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs

## 相關教學

- [如何在 Java 中使用 GroupDocs.Search 指南索引文字](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [使用進階索引技術優化 GroupDocs.Search for Java 的搜尋效能](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [使用 GroupDocs.Search Java 改善查詢效能：優化索引與搜尋](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)