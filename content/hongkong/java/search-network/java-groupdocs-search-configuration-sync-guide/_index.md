---
date: '2026-05-17'
description: 了解如何新增 GroupDocs Maven 依賴、設置 Java 搜尋網路，並將目錄加入索引，以實現快速且可擴展的文件檢索。
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: 如何為搜尋網路添加 GroupDocs Maven 依賴
type: docs
url: /zh-hant/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# 如何為搜尋網路新增 GroupDocs Maven 依賴項

在本完整指南中，您將了解 **如何新增 groupdocs Maven 依賴項**，使用 GroupDocs.Search 配置強大的 Java 搜尋網路，並保持分片同步。無論您是索引法律簡報、財務報表或學術論文，以下步驟將協助您建立可搜尋的索引、在節點之間分配查詢負載，並以最小的努力維持資料一致性。

## 快速解答
- **什麼是 GroupDocs Maven 依賴項？** 一個將 GroupDocs.Search 函式庫打包於 Java 專案中的 Maven 套件。  
- **為什麼要使用搜尋網路？** 它將索引與查詢負載分散至多個節點，提升速度與可靠性。  
- **如何將目錄加入索引？** 在主節點上使用 `IndexingDocuments.addDirectories`。  
- **如何同步分片？** 在每個節點的 `Indexer` 上呼叫 `SynchronizeOptions`。  
- **我需要授權嗎？** 是的，生產環境使用需具備試用或商業授權。

## 什麼是 GroupDocs Maven 依賴項？

`GroupDocs Maven 依賴項` 是一個將 GroupDocs.Search 函式庫打包於 Java 專案中的 Maven 套件。  
它提供建立可搜尋索引、管理網路節點與執行快速查詢所需的全部類別，且 Maven 會自動解析傳遞性依賴，使您只需在 `pom.xml` 中加入幾行程式碼，即可獲得即用型搜尋引擎。

## 如何新增 GroupDocs Maven 依賴項

將儲存庫與依賴項條目加入您的 `pom.xml`，然後執行 `mvn clean install`；Maven 會下載 `groupdocs-search` JAR 及其所需的函式庫，讓 API 在您的專案中可用。建置成功後，即可立即開始使用 `com.groupdocs.search` 類別。

### Maven 設定

將儲存庫與依賴項加入您的 `pom.xml`：

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

> **專業提示：** 請透過官方發行頁面保持版本號為最新。

您也可以直接從官方網站下載 JAR：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## 為什麼使用搜尋網路？

搜尋網路透過將索引切分為位於不同節點的分片，實現水平擴充。GroupDocs.Search 能處理 **50+ 種輸入格式**，並在不將整個檔案載入記憶體的情況下處理 **數百頁文件**，即使資料量增長亦能提供次秒級的查詢回應。

## 前置條件

- **JDK** (11 或更新版本) 已安裝。  
- IntelliJ IDEA 或 Eclipse 等 IDE。  
- 基本的 Java 知識、Maven 使用經驗，以及對網路節點概念的了解。  
- 有效的 GroupDocs.Search 授權（免費試用或商業版）。

## 基本初始化與設定

首先建立索引目錄：

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

此簡單步驟為後續的網路設定做好環境準備。

## 實作指南

### 功能 1：搜尋網路設定

#### 概觀

設定搜尋網路會指定節點之間通訊所使用的檔案路徑與埠號。

##### 設定路徑與埠號

Configuration 是一個保存搜尋叢集網路路徑、埠號及其他設定的類別。  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
`configuration` 物件現在包含搜尋網路所需的全部設定。

### 功能 2：部署搜尋網路節點

#### 概觀

部署節點以在您的網路中分散工作負載。主節點負責管理操作與事件。

##### 部署程式碼

SearchNetworkNode 代表搜尋網路中的一個節點，可作為主節點或工作節點。  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### 功能 3：訂閱搜尋網路節點事件

#### 概觀

監聽事件可讓您動態處理網路中的變更或更新。

##### 訂閱實作

SearchNetworkNodeEvents 提供節點生命週期與索引動作的事件掛鉤。  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### 功能 4：將目錄加入索引

#### 概觀

加入目錄是使文件可搜尋的核心步驟。

##### 文件加入

`IndexingDocuments.addDirectories` 將資料夾路徑加入索引以供處理。  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### 功能 5：在搜尋網路節點同步分片

#### 概觀

同步確保所有分片之間的資料一致性。

##### 同步程式碼

`SynchronizeOptions` 設定分片在節點之間的同步方式。  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### 功能 6：關閉搜尋網路節點

#### 概觀

正確關閉節點可釋放資源並防止記憶體洩漏。

##### 節點關閉

`close()` 釋放資源並關閉搜尋網路節點。  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## 實務應用

1. **Legal Document Management** – 快速檢索案件檔案與先例。  
2. **Financial Record Keeping** – 在數秒內取得報表與稽核紀錄。  
3. **Academic Research** – 在數千篇論文中搜尋以找到相關引用。

## 效能考量

- **Optimize Queries** – 撰寫簡潔的查詢以減少回應時間。  
- **Memory Management** – 監控 JVM 堆積使用情況；對大型索引考慮 GC 調校。  
- **Scaling Strategy** – 依資料量與查詢負載成比例新增節點。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| 節點無法連線 | 埠號衝突 | 將 `basePort` 更改為未使用的值 |
| 索引未更新 | 缺少事件訂閱 | 確保已呼叫 `SearchNetworkNodeEvents.subscribe(masterNode)` |
| 延遲過高 | 分片不足 | 增加節點數量並平衡文件分配 |

## 常見問答

**Q: 使用 GroupDocs.Search 的主要好處是什麼？**  
A: 它提供快速且具擴充性的搜尋功能，能在大型文件集合上以最小的設定完成搜尋。

**Q: 我可以在搜尋網路中自訂節點設定嗎？**  
A: 可以，您可以透過 `Configuration` 物件設定自訂路徑、埠號及其他選項。

**Q: 網路運行後，如何將目錄加入索引？**  
A: 每當需要索引新資料夾時，呼叫 `IndexingDocuments.addDirectories(masterNode, "path")`。

**Q: 當新節點加入網路時，如何同步分片？**  
A: 在新加入的節點上使用上述的 `synchronizeShards` 方法。

**Q: 開發階段需要授權嗎？**  
A: 測試階段使用免費試用授權即可；生產環境則需商業授權。

## 結論

透過本指南，您現在已了解如何 **新增 groupdocs Maven 依賴項**、配置多節點搜尋網路、索引目錄，並保持分片同步。這些步驟為高效能文件搜尋解決方案奠定基礎，且能隨組織需求成長。

---

**最後更新：** 2026-05-17  
**測試版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs

## 相關教學

- [GroupDocs.Search for Java 教學與範例](/search/net/)
- [.NET 中設定 GroupDocs.Search 網路：完整指南](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [.NET 中使用 GroupDocs.Search 實作文件管理系統的搜尋網路](/search/net/search-network/implement-search-network-groupdocs-dotnet/)