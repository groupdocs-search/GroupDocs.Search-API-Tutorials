---
date: '2026-01-08'
description: 學習如何使用 GroupDocs.Search for Java 設定搜尋並啟用即時搜尋更新。提供網路設定、節點部署與索引建立的逐步指南。
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 如何在 Java 中使用 GroupDocs.Search 設定搜尋：設定與部署指南
type: docs
url: /zh-hant/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Search 配置搜尋

在當今快速變化的數位世界，**如何配置搜尋**的效率足以左右專案的成敗。無論你在處理成千上萬的合約、研究論文或內部報告，完善的搜尋網路都能讓你在數秒內找到正確的文件。本教學將帶你一步步設定搜尋網路、部署節點，並使用 GroupDocs.Search for Java 啟用**即時搜尋更新**。

## 快速答案
- **搜尋網路的主要目的為何？** 將索引與查詢處理分散至多個節點，以提升可擴展性與速度。  
- **需要哪個版本的函式庫？** GroupDocs.Search for Java v25.4 或更新版本。  
- **是否需要授權？** 免費試用可用於評估；正式上線需購買商業授權。  
- **即時更新如何處理？** 訂閱節點事件，於索引變更時觸發。  
- **可以即時新增文件資料夾嗎？** 可以—使用索引器的 `addDirectories` 方法。

## 在 GroupDocs 中「如何配置搜尋」是什麼意思？
配置搜尋即是建立一個**搜尋網路**，讓系統知道文件所在位置、節點之間的通訊方式，以及索引如何協調。網路配置完成後，你可以在不中斷服務的情況下新增或移除節點，確保搜尋結果持續保持最新。

## 為什麼選擇 GroupDocs.Search for Java？
- **可擴展性：** 將工作負載分散至多台機器。  
- **即時更新：** 新增的檔案會立即在整個網路中同步。  
- **整合簡易：** Maven 設定簡單，Java API 清晰。  
- **企業級：** 能處理大型語料庫與複雜查詢情境。

## 前置條件
- 已安裝 **Java Development Kit (JDK) 8+**。  
- 具備 **Maven** 以管理相依性。  
- 具備基本的 Java、Maven 與搜尋概念。

## 設定 GroupDocs.Search for Java

### Maven 相依性
在 `pom.xml` 中加入儲存庫與相依性：

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

**直接下載：** 也可以從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 取得函式庫。

### 取得授權
- **免費試用：** 取得試用授權以探索全部功能。  
- **臨時授權：** 申請延長評估期間。  
- **商業授權：** 正式上線時必須使用。

### 基本初始化
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## 如何在 Java 中配置搜尋網路

### 步驟 1：匯入必要的套件
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### 步驟 2：配置網路
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **參數說明：** `basePath` 指向你的文件資料夾；`basePort` 為節點通訊使用的 TCP 埠號。

## 部署搜尋網路節點

### 步驟 1：匯入部署套件
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### 步驟 2：部署節點
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **主節點 (Master Node)：** 負責協調所有節點的搜尋與索引工作。

## 訂閱節點事件以實現即時搜尋更新

### 步驟 1：匯入事件套件
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### 步驟 2：訂閱主節點事件
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **事件處理：** 當文件新增、更新或刪除時，即可觸發**即時搜尋更新**。

## 新增索引資料夾

### 步驟 1：匯入索引器套件
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### 步驟 2：加入文件資料夾
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **動態索引：** 可隨需求加入任意數量的資料夾，網路會自動索引。

## 取得已索引的文件

### 步驟 1：匯入搜尋套件
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### 步驟 2：取得文件資訊
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **分片管理：** 透過將文件分散至多個分片，有效處理大規模資料集。

## 實務應用
1. **企業文件管理：** 在數百萬檔案中集中搜尋。  
2. **法律事務所：** 快速定位案件檔、合約與證據。  
3. **學術研究：** 索引期刊與論文，實現即時檢索。

## 效能考量
- **優化索引：** 定期執行索引刷新並清除過期資料。  
- **記憶體管理：** 監控 JVM 堆積，特別是在處理大型分片時。  
- **可擴展性規劃：** 隨語料庫成長增添節點，網路會自動平衡負載。

## 常見問題與解決方案
| 問題 | 原因 | 解決方式 |
|------|------|----------|
| 節點無法連線 | 埠號衝突或防火牆阻擋 | 確認 `basePort` 已開放且未被其他服務佔用 |
| 索引未更新 | 未訂閱事件 | 部署後呼叫 `SearchNetworkNodeEvents.subscribe(masterNode)` |
| 記憶體不足 | 載入過多大型分片 | 減少分片大小或提升 JVM 堆積 (`-Xmx` 參數) |

## 常見問答

**Q: 網路運行中可以新增資料夾嗎？**  
A: 可以—使用 `indexer.addDirectories()` 方法；已訂閱的事件會即時傳播更新。

**Q: 要如何監控節點健康狀態？**  
A: 每個 `SearchNetworkNode` 都提供狀態 API，可整合至你慣用的監控工具。

**Q: 主節點可以部署在不同的機器上嗎？**  
A: 完全可以。只要所有節點使用相同的 `basePort` 並能相互連線即可。

**Q: 支援哪些檔案格式？**  
A: GroupDocs.Search 原生支援 PDF、Word、Excel、PowerPoint、純文字等多種格式。

**Q: 新增節點後需要重新啟動網路嗎？**  
A: 不需要—節點可動態加入或移除，主節點會自動重新平衡分片。

## 結論
現在，你已完整掌握使用 GroupDocs.Search for Java **如何配置搜尋** 的全流程，從初始設定到即時更新與分散式索引。將這些模式套用於各行各業，即可打造快速、可擴展且可靠的文件搜尋解決方案。

---

**最後更新：** 2026-01-08  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs