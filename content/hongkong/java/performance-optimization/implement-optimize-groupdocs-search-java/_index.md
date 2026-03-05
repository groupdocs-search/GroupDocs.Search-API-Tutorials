---
date: '2026-01-16'
description: 學習如何使用 GroupDocs.Search for Java 執行文字搜尋並優化搜尋效能。內容包括設定搜尋網路、建立可搜尋的索引以及刪除文件索引的步驟。
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: 使用 GroupDocs.Search for Java 進行文字搜尋
type: docs
url: /zh-hant/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# 使用 GroupDocs.Search for Java 執行文字搜尋
## 效能優化

## 如何在 GroupDocs.Search for Java 中實作與優化搜尋網路

### 介紹
在當今資料驅動的世界，能夠 **執行文字搜尋** 並快速遍歷龐大的文件集合是一項競爭優勢。無論您是構建內部知識庫、法律案件儲存庫，或是電商商品目錄，良好調校的搜尋網路都能顯著提升使用者滿意度。在本指南中，您將學會如何 **設定搜尋網路**、**建立可搜尋索引**、**優化搜尋效能**，以及在需要時 **刪除文件索引**——全部使用 GroupDocs.Search for Java。

**您將學到的內容**
- 使用 GroupDocs.Search 設定搜尋網路  
- 在網路中部署節點  
- 高效索引文件 (`index documents java`)  
- 在網路中執行文字搜尋 (`perform text search`)  
- 從索引中刪除特定文件 (`delete documents index`)  

讓我們一起深入了解如何利用這些功能打造最佳化的搜尋體驗。

## 快速答覆
- **GroupDocs.Search for Java 的主要目的為何？** 它提供跨多種文件格式的全文搜尋功能。  
- **如何在分散式環境中執行文字搜尋？** 部署搜尋網路，在主節點建立索引，然後向任意節點發出查詢。  
- **我可以在不重新建立索引的情況下刪除文件嗎？** 可以，使用 Delete API 移除選定的檔案。  
- **需要哪個 Java 版本？** JDK 8 或更高。  
- **生產環境需要授權嗎？** 需要有效的 GroupDocs.Search 授權；亦提供免費試用版。

## 什麼是「執行文字搜尋」？
執行文字搜尋是指對全文索引進行查詢，以取得包含指定關鍵字或片語的文件。GroupDocs.Search 會建立倒排索引，使這類查找即使在數千個檔案中也能極速完成。

## 為什麼要設定搜尋網路？
搜尋網路會將索引與查詢工作負載分散至多個節點，讓您 **優化搜尋效能**、水平擴展，並維持高可用性。此架構特別適合企業級文件儲存庫，對延遲與吞吐量都有嚴格要求。

### 前置條件
- **必備函式庫：** GroupDocs.Search for Java 版本 25.4（最新）。  
- **環境：** Java JDK 8+、Maven。  
- **知識：** 基本的 Java 程式設計與網路概念。

### 設定 GroupDocs.Search for Java
首先，使用以下方式將 GroupDocs.Search 整合至您的 Java 專案。

#### Maven 設定
在 `pom.xml` 檔案中加入儲存庫與相依性：

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
或者，您也可以直接從 GroupDocs 下載最新版本：[download the latest version directly from GroupDocs](https://releases.groupdocs.com/search/java/)。

#### 取得授權
GroupDocs 提供免費試用，讓您在購買前先評估功能。您可依照其 [purchase page](https://purchase.groupdocs.com/temporary-license/) 上的步驟取得臨時授權，於測試階段啟用完整功能。

#### 基本初始化與設定
在 Java 應用程式中這樣初始化 GroupDocs.Search：

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

### 實作指南

#### 設定搜尋網路
**概述：** 建立基礎路徑與埠號，讓節點之間能順暢通訊。

##### 步驟 1：定義基礎設定

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **參數說明：**  
  - `basePath`：網路操作的目錄路徑。  
  - `basePort`：搜尋網路使用的埠號。

##### 步驟 2：故障排除
確保您指定的埠號未被防火牆阻擋或被其他應用佔用，必要時調整以避免衝突。

#### 部署搜尋網路節點
**概述：** 依照先前的設定，在網路中部署節點，以實現分散式索引與搜尋。

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **關鍵設定選項：**  
  - **基礎路徑與埠號：** 這些值必須與最初的設定保持一致，以確保相容性。

#### 索引文件（`create searchable index`）
**概述：** 使用主節點將文件高效加入搜尋索引。

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **目的說明：**  
  - `masterNode`：負責文件索引的主要節點。  
  - `documentsPath`：存放文件的目錄路徑。

##### 故障排除小技巧
確認文件路徑正確且可存取，且目錄權限允許讀取。

#### 在網路中搜尋文字（`perform text search`）
**概述：** 在已建立的索引網路中執行全面的文字搜尋。

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **參數說明：**  
  - `query`：您要搜尋的文字。  
  - `masterNode`：執行搜尋的節點。

#### 從索引中刪除文件（`delete documents index`）
**概述：** 依照檔案路徑將特定文件從索引中移除。

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
  - `filePaths`：欲從索引中移除的文件路徑。

##### 故障排除
確保檔案路徑精確且檔案確實存在於目錄中；若問題持續，請檢查網路權限與連線狀態。

### 實務應用
1. **企業文件管理：** 精簡內部知識檢索。  
2. **法律案件分析：** 快速定位多個儲存庫中的相關案件檔案。  
3. **電商平台：** 透過索引商品說明與評論提升搜尋速度。  
4. **學術研究：** 高效搜尋大型數位圖書館中的論文與學位論文。  
5. **客服系統：** 讓客服人員即時搜尋過往工單，縮短回應時間。

### 效能考量
- **優化索引速度：** 在非高峰時段逐步加入新文件，以降低延遲。  
- **資源使用指引：** 監控 CPU 與記憶體，特別是在擴增節點數量時。  
- **Java 記憶體管理：** 依工作負載調整 JVM 堆積設定（例如 `-Xmx2g` 以支援中等規模索引）。

### 結論
透過本指南，您已學會如何 **設定搜尋網路**、**建立可搜尋索引**、**執行文字搜尋**，以及 **刪除文件索引**，全部使用 GroupDocs.Search for Java。這些功能讓您在分散式環境中實現快速、可靠的文件檢索。

**後續步驟**
- 嘗試不同的節點配置，以找出最適合您工作負載的平衡點。  
- 深入探索進階索引選項，如自訂分析器與相關度調校。  
- 探索與其他 GroupDocs 產品的整合，打造端到端的文件處理流程。

## 常見問題

**Q: GroupDocs.Search for Java 的主要使用情境是什麼？**  
A: 它提供跨多種文件格式的全文搜尋，讓您能在大型儲存庫中 **執行文字搜尋**。

**Q: 如何提升大型網路的搜尋速度？**  
A: 部署更多節點、調整 JVM 堆積，並在低流量時段排程索引，以 **優化搜尋效能**。

**Q: 能否在不重新建立整個集合的情況下刪除單一文件？**  
A: 可以，使用本文範例中的 **delete documents index** API 即可移除特定檔案。

**Q: 開發階段需要授權嗎？**  
A: 測試時使用免費試用授權即可；正式上線則需購買商業授權。

**Q: 能否同時索引 PDF、Word 檔與電子郵件？**  
A: 完全可以——GroupDocs.Search 內建支援多種格式。

---

**最後更新：** 2026-01-16  
**測試版本：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs