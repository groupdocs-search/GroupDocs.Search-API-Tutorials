---
date: '2026-07-02'
description: 了解如何為 GroupDocs.Search 取得臨時授權、將目錄加入索引，以及在管理 Java 搜尋網路節點時新增自訂文件屬性。
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: 取得臨時授權 GroupDocs – Master Search Nodes (Java)
type: docs
url: /zh-hant/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# 取得 GroupDocs 臨時授權 – 主搜尋節點 (Java)

在本完整指南中，您將**取得 GroupDocs.Search 的臨時授權**、配置多節點搜尋網路，並學習如何使用 Java **將目錄加入索引**以及**新增自訂文件屬性**。無論您是構建企業文件管理系統或可搜尋的商品目錄，掌握這些步驟都能讓您在無限制的情況下評估平台，並快速擴展搜尋功能。

## 快速解答
- **開始使用 GroupDocs.Search 的第一步是什麼？** 從 GroupDocs 入口網站取得臨時授權。  
- **哪個 Maven 套件庫提供此函式庫？** `https://releases.groupdocs.com/search/java/`。  
- **如何將目錄加入索引？** 在主節點呼叫 `addDirectoriesToIndex` 輔助方法。  
- **我可以新增自訂文件屬性嗎？** 可以——使用文件鍵與屬性名稱呼叫 `addAttribute`。  
- **如何安全關閉節點？** 呼叫 `closeNodes` 釋放資源。

## 什麼是臨時授權以及為何需要它？
臨時授權讓您在沒有任何評估限制的情況下評估 GroupDocs.Search。它非常適合開發、測試或概念驗證專案，在正式購買前先行驗證。此授權在有限時間內提供完整功能存取，讓您能夠衡量效能、測試整合點，並確保解決方案符合需求，且無需金錢承諾。

## 前置條件

在開始之前，請確保已具備以下前置條件：

### 必要的函式庫與相依性
要在 Java 中使用 GroupDocs.Search，請加入必要的 Maven 相依性：
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
您也可以直接從 [GroupDocs.Search for Java 版本](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 環境設定
- 確保已安裝相容的 JDK（Java 8 或更新版本）。  
- 設定您的 IDE 以支援 Maven 專案。

### 知識前置條件
具備 Java 程式設計的基本概念與 Maven 專案管理的熟悉度將會有幫助。若您對這些概念尚不熟悉，建議先參考入門資源以開始學習。

## 如何取得臨時授權
取得臨時授權的方式是前往 GroupDocs 入口網站，填寫簡短的申請表，並將收到的 `.lic` 檔案放入專案的 `resources` 資料夾。接著以幾行程式碼初始化授權（請參考下方程式碼片段）。申請表請使用官方頁面：[GroupDocs 臨時授權](https://purchase.groupdocs.com/temporary-license/)。

## 設定 GroupDocs.Search for Java

### 安裝資訊
要在專案中開始使用 GroupDocs.Search for Java，請依照上述 Maven 步驟操作，或直接從官方發佈頁面下載最新版本。

#### 授權取得步驟
1. **免費試用** – 在無需承諾的情況下探索功能。  
2. **臨時授權** – 取得短期測試金鑰（請參閱上節）。  
3. **購買** – 若於正式環境使用，請從 **[GroupDocs 購買頁面](https://purchase.groupdocs.com/)** 購買完整授權。

### 基本初始化與設定
使用以下方式初始化您的專案與 GroupDocs.Search：
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
此初始化步驟至關重要，可確保所有元件在搜尋網路中順利運作。

## 實作指南
現在，我們將把整個流程拆解為可管理的章節，每個章節聚焦於部署與管理搜尋網路節點的特定功能。

### 功能 1：設定配置
**概述：** 為搜尋網路設定配置是部署節點的第一步。此設定涉及指定對節點部署至關重要的路徑與埠號。

#### 實作步驟：
##### 步驟 1：定義基礎路徑與埠號
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### 步驟 2：配置搜尋網路
`configureSearchNetwork` 函式會準備部署節點所需的配置物件。  
`Configuration` 是一個類別，保存所有設定，例如索引資料夾、網路埠號與節點角色。  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **參數：** 基礎路徑與埠號用於定位資源與建立通訊管道。  
- **回傳值：** 依您的部署需求調整的 `Configuration` 物件。

### 功能 2：搜尋網路部署
**概述：** 部署節點對於在不同環境或資料區段擴展搜尋能力至關重要。

#### 實作步驟：
##### 步驟 1：部署節點
`deploySearchNetwork` 函式會初始化並回傳搜尋網路節點的陣列。  
`SearchNetworkNodes` 代表參與分散式搜尋叢集的每個節點實例。  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **參數：** 基礎路徑、埠號與配置用於決定部署環境。  
- **回傳值：** 包含已初始化 `SearchNetworkNodes` 的陣列。

### 功能 3：訂閱網路事件
**概述：** 監控搜尋網路的活動對於維持最佳效能與可靠性至關重要。

#### 實作步驟：
##### 步驟 1：訂閱主節點事件
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **目的：** 此步驟確保您能收到搜尋網路內重大事件或變更的通知。

### 功能 4：文件索引
**概述：** 將包含文件的目錄加入索引，可在整個網路中實現高效的資料檢索。

#### 如何將目錄加入索引
`addDirectoriesToIndex` 是在主節點註冊用於索引的資料夾路徑的輔助方法。  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **目的：** 促進指定目錄內所有文件的快速存取與可搜尋性。

### 功能 5：為文件新增屬性
**概述：** 自訂屬性可增強文件的中繼資料，使搜尋更具彈性與資訊性。

#### 如何為文件新增自訂屬性
`addAttribute` 為索引中指定的文件新增自訂中繼資料屬性。  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **參數：** 指定節點、文件鍵與欲新增的屬性。  
- **目的：** 透過為文件添加額外中繼資料，擴充搜尋功能。

### 功能 6：取得已索引文件
**概述：** 高效取得並列出已索引文件，以確保資料的正確性與完整性。

#### 實作步驟：
##### 步驟 1：取得已索引文件
```java
getIndexedDocuments(nodes[0]);
```  
- **目的：** 驗證搜尋網路中所有必要文件已成功索引。

### 功能 7：關閉網路節點
**概述：** 正確關閉節點對於資源管理與防止記憶體洩漏至關重要。

#### 實作步驟：
##### 步驟 1：關閉所有節點
`closeNodes` 會關閉所有活動的搜尋節點並釋放已分配的資源。  
```java
closeNodes(nodes);
```  
- **目的：** 釋放每個節點佔用的資源，確保乾淨的關閉流程。

## 為何使用 GroupDocs.Search 的臨時授權？
臨時授權提供 **30 天的完整功能存取**，且支援最多 **50,000 份已索引文件**，不會受到效能限制。這讓您能在實際資料上衡量索引速度、查詢延遲與可擴充性，於購買正式授權前進行基準測試。它亦會移除評估水印，讓您真實體驗最終產品的功能。

## 常見使用情境
1. **企業文件管理** – 索引跨部門的數百萬內部檔案，實現即時全文搜尋。  
2. **電子商務平台** – 建立跨多個倉庫與第三方資料源的可搜尋商品目錄。  
3. **法律事務所** – 使用自訂中繼資料整理案件檔案、合約與證據，以快速檢索。

與其他系統的整合可能性包括 CRM 平台、內容管理系統（CMS）以及資料分析工具，皆可利用 GroupDocs.Search for Java 所提供的強大索引與搜尋功能。

## 效能考量
使用 GroupDocs.Search for Java 時，優化效能的方式如下：
- **最佳化配置** – 依您的特定部署環境調整配置設定。  
- **監控資源使用** – 定期檢查 CPU、記憶體與 I/O，以防止瓶頸或記憶體洩漏。  
- **遵循最佳實踐** – 符合 Java 記憶體管理指南，確保系統資源的有效利用。

## 常見問答

**Q: 臨時授權的有效期限是多久？**  
A: 臨時授權通常有效 30 天，足以讓您充分評估產品。

**Q: 我可以在不重新安裝的情況下，從臨時授權切換為完整授權嗎？**  
A: 可以——將臨時授權檔案替換為完整授權檔案，然後重新啟動應用程式。

**Q: 套用新授權後需要重新索引文件嗎？**  
A: 不需要，索引保持不變；授權僅影響使用權限。

**Q: 若忘記關閉節點會發生什麼情況？**  
A: 未釋放的資源可能導致記憶體洩漏；關閉時務必呼叫 `closeNodes`。

**Q: 是否可以為每個文件新增多個自訂屬性？**  
A: 當然可以——使用不同的屬性名稱多次呼叫 `addAttribute`。

---

**最後更新：** 2026-07-02  
**測試版本：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs

## 相關教學

- [在 .NET 中部署搜尋網路節點以實現高效文件索引與檢索](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [如何在 .NET 中使用 GroupDocs.Search 實作文件管理系統的搜尋網路](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [設定 Aspose.Search 網路與使用 GroupDocs.Redaction 為 .NET 新增文件屬性：完整指南](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)