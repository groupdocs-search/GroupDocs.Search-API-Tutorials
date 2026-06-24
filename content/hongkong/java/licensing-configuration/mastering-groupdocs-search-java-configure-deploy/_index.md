---
date: '2026-05-02'
description: 學習如何使用 GroupDocs.Search for Java 配置搜尋並啟用即時搜尋更新。提供網絡設定、節點部署與索引的逐步指南。
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: 如何在 Java 中使用 GroupDocs.Search 配置搜尋 - 配置與部署指南
type: docs
url: /zh-hant/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Search 配置搜尋

在當今快速變化的數位世界中，**如何配置搜尋**的效率可成就或毀掉一個專案的成功。無論您在處理成千上萬的合約、研究論文或內部報告，完善的搜尋網路都能讓您在數秒內找到正確的文件。本教學將帶您一步步設定搜尋網路、部署節點，並使用 GroupDocs.Search for Java 啟用**即時搜尋更新**。

## 快速解答
- **搜尋網路的主要目的為何？** 將索引與查詢處理分散至多個節點，以提升可擴展性與速度。  
- **需要哪個版本的函式庫？** GroupDocs.Search for Java v25.4 或更新版本。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買商業授權。  
- **即時更新如何處理？** 透過訂閱在索引變更時觸發的節點事件。  
- **我可以即時新增文件資料夾嗎？** 可以 — 使用索引器的 `addDirectories` 方法。

## 在 GroupDocs 情境下，「如何配置搜尋」是什麼？
配置搜尋是指建立一個 **搜尋網路**，讓系統了解文件所在位置、節點之間的通訊方式，以及索引的協調方式。網路配置完成後，您可以在不中斷服務的情況下新增或移除節點，確保持續取得最新的搜尋結果。

## 為何使用 GroupDocs.Search for Java？
- **可擴展性：** 將工作負載分散至多台機器。  
- **即時更新：** 立即在整個網路中反映新索引的檔案。  
- **易於整合：** 簡單的 Maven 設定與清晰的 Java API。  
- **企業級：** 能處理大型語料庫與複雜的查詢情境。

## 前置條件
- **Java Development Kit (JDK) 8+** 已安裝。  
- **Maven** 用於相依管理。  
- 具備 Java、Maven 與搜尋概念的基本了解。

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

**直接下載：** 您也可以從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 取得此函式庫。

### 取得授權
- **免費試用：** 取得試用授權以探索全部功能。  
- **臨時授權：** 申請延長評估期間。  
- **商業授權：** 正式部署時必須使用。

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
- **參數說明：** `basePath` 指向您的文件資料夾；`basePort` 為節點通訊使用的 TCP 埠號。

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
- **主節點：** 協調所有節點的搜尋與索引。您可以 **配置主節點** 設定，例如分片分配與健康檢查。

## 訂閱節點事件以實現即時搜尋更新

### 步驟 1：匯入事件套件
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### 步驟 2：訂閱主節點事件
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **事件處理：** 讓 **即時搜尋更新** 在文件新增、更新或移除時即時生效。

## 新增目錄以進行索引

### 步驟 1：匯入索引器套件
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### 步驟 2：新增文件目錄
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **動態索引：** 使用 `addDirectories` 方法 **即時新增目錄至索引**，無需重新啟動網路。

## 取得已索引的文件

### 步驟 1：匯入搜尋器套件
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
- **分片管理：** 透過將文件分散至多個分片，有效處理大型資料集。若要 **最佳化分片大小**，請監控分片統計並在未來版本中調整 `shardSize` 設定。

## 為何這對您的專案重要
妥善配置的搜尋網路可消除瓶頸、降低延遲，並確保使用者始終看到文件的最新版本。即時更新以及 **即時新增目錄至索引** 而不需停機的能力，對於法律事務所、研究機構以及任何處理不斷變動文件集合的組織尤為重要。

## 實務應用
1. **企業文件管理：** 在數百萬檔案中集中搜尋。  
2. **法律事務所：** 快速定位案件檔案、合約與證據。  
3. **學術研究：** 索引期刊與論文以即時檢索。

## 效能考量
- **優化索引：** 安排定期的索引刷新並清除過時資料。  
- **記憶體管理：** 監控 JVM 堆積，特別是在處理大型分片時。  
- **可擴展性規劃：** 隨語料庫增長新增節點；網路會自動平衡負載。  
- **最佳化分片大小：** 較小的分片可提升查詢延遲，較大的分片則降低開銷。請根據硬體與查詢模式進行調整。

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| 節點無法連線 | 埠號衝突或防火牆 | 確保 `basePort` 已開放且未被其他服務佔用 |
| 索引未更新 | 缺少事件訂閱 | 在部署後呼叫 `SearchNetworkNodeEvents.subscribe(masterNode)` |
| 記憶體不足錯誤 | 載入過多大型分片 | 減少分片大小或增加 JVM 堆積 (`-Xmx` 參數) |

## 常見問答

**Q: 我可以在網路運行後新增目錄嗎？**  
A: 可以 — 使用 `indexer.addDirectories()` 方法；已訂閱的事件會即時傳播更新。

**Q: 我如何監控節點健康狀態？**  
A: 每個 `SearchNetworkNode` 都提供狀態 API；可整合至您選擇的監控工具。

**Q: 可以在不同機器上執行主節點嗎？**  
A: 完全可以。只要確保所有節點使用相同的 `basePort` 並能在網路上互相連線即可。

**Q: 支援哪些檔案格式？**  
A: GroupDocs.Search 內建支援 PDF、Word、Excel、PowerPoint、純文字等多種格式。

**Q: 新增節點後需要重新啟動網路嗎？**  
A: 不需要 — 節點可動態新增或移除；主節點會自動重新平衡分片。

## 結論
現在您已了解如何使用 GroupDocs.Search for Java **配置搜尋**，即可打造快速、可擴展且可靠的文件搜尋解決方案，跟上組織成長的步伐。將這些模式套用於任何產業，即可實現即時、分散式的搜尋體驗。

---

**最後更新：** 2026-05-02  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs