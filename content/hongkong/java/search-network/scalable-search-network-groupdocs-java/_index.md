---
date: '2026-05-17'
description: 了解如何為可擴展的 GroupDocs.Search Java 網路配置基礎埠 groupdocs、優化檢索速度，並設置多節點系統。
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: 在 Java Search Network 中配置基礎埠 groupdocs
type: docs
url: /zh-hant/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# 在 Java 搜尋網路中設定 GroupDocs 基礎埠

在現代資料密集的應用程式中，**configure base port groupdocs** 是建立快速且可靠搜尋基礎設施的第一步。無論您是索引數千份 PDF，或是擴展至多台伺服器，指派唯一的埠號與目錄可避免節點之間的衝突，並保持叢集健康。本教學將帶您了解前置條件、安裝步驟，以及使用 GroupDocs.Search for Java 完成完整的多節點設定，讓您立即啟動真正可擴展的搜尋網路。

## 快速解答
- **主要目的為何？** 為每個搜尋節點指派唯一的埠號與基礎目錄，以消除衝突。  
- **需要授權嗎？** 需要 – 生產環境部署必須使用試用或正式授權。  
- **支援哪個 Java 版本？** Java 8 或更新版本（建議使用 Java 11 以上）。  
- **可以在雲端伺服器上執行嗎？** 當然可以 – 只需在雲端安全群組中開放所選埠號。  
- **可以新增多少節點？** 沒有硬性上限；僅受硬體與網路容量限制。

## 「configure base port groupdocs」是什麼？

**Configure base port groupdocs** 是指為每個搜尋節點指派起始 TCP 埠號，並為後續節點遞增。此簡單步驟可消除「埠已被使用」的錯誤，為乾淨且水平可擴展的搜尋叢集奠定基礎，確保每個節點皆透過唯一端點通訊。

## 為何使用 GroupDocs.Search 來建構可擴展的網路？

GroupDocs.Search 提供 **高效能索引**（在標準 8 核心伺服器上最高可達 50 GB/分鐘），並支援 **超過 50 種檔案格式**，包括 PDF、DOCX、PPTX 與 HTML。其模組化架構允許您在節點間混合索引器、搜尋器、分片與抽取器，隨著硬體擴充即可線性擴展。此函式庫亦內建壓縮選項，可將磁碟使用量降低至最高 70 %，同時在一般工作負載下將查詢延遲維持在 200 ms 以下。

## 前置條件
- **Java Development Kit (JDK)** 8 或更新（建議使用 Java 11+ 以獲得更佳的垃圾回收）。  
- **IDE** 如 IntelliJ IDEA 或 Eclipse。  
- **GroupDocs.Search for Java** 函式庫（版本 25.4 或更新）透過 Maven 或手動下載安裝。  
- 基本的網路知識（TCP 埠號、localhost 與遠端主機）。  
- 有效的 **GroupDocs.Search** 授權（試用或正式）。

## 設定 GroupDocs.Search for Java

### 安裝說明

**Maven 設定：**

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

**直接下載：**

或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權

- **Free Trial** – 立即開始測試。  
- **Temporary License** – 在 [Temporary License](https://purchase.groupdocs.com/temporary-license) 取得延長試用。  
- **Full Purchase** – 生產環境部署必須購買正式授權。

### 基本初始化與設定

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## 實作指南

### 如何設定 configure base port groupdocs？

要設定基礎埠號，請編輯網路設定檔或以程式方式將 `basePort` 屬性設定為高且未被使用的值，例如 49100。對於每個後續節點，將埠號遞增一（或固定偏移），使每個節點綁定其獨立的 TCP 端點，消除埠衝突錯誤並簡化防火牆規則。

#### 設定基礎路徑

在撰寫任何程式碼之前，先決定一致的資料夾布局。例如，為索引器 (`Indexer0`)、搜尋器 (`Searcher0`) 與抽取器 (`Extractor0`) 建立獨立目錄。此結構可讓每個節點快速解析其檔案。

- **Why**: 可預測的目錄層級可防止節點在不同機器上啟動時出現「找不到檔案」錯誤。

#### 設定基礎埠號

選擇較高的起始埠號以避免與常見服務衝突（HTTP 80、SSH 22 等）。對於每個新增的節點，遞增埠號。

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: 從較高的埠號（例如 49100）開始，可降低與現有服務衝突的機會，並簡化防火牆規則的建立。

#### 定義主機位址

開發階段使用 `localhost` 即可。正式環境請改為伺服器的 IP 位址或 DNS 名稱，以便遠端節點互相連線。

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: 使用真實的主機位址可實現跨機器通訊，這對雲端或本地叢集至關重要。

#### 建立網路設定

`NetworkConfig` 類別將所有網路選項——基礎埠號、主機以及可選的 SSL 設定——彙集於單一物件，供搜尋引擎使用。

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Why**: 集中這些選項可使設定可重複使用，且在多節點間更易維護。

#### 新增節點

`SearchNode` 代表 GroupDocs.Search 叢集中的單一節點，執行索引或搜尋等特定功能。為每個角色（索引器、搜尋器、抽取器）實例化 `SearchNode`，並將其註冊至 `SearchEngine`。將工作分散至各節點可提升平行度與容錯能力。

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Why**: 將工作分散至專屬節點可減少競爭，讓每台機器專注於單一任務，提升整體吞吐量。

#### 完成設定

在新增所有節點後，呼叫 `engine.start()` 以啟動網路。引擎會自動將每個節點綁定至其指定的埠號，並驗證連線性。

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### 常見問題與解決方案

- **Port Conflicts** – 每個新節點皆遞增 `basePort`。可使用 `netstat` 或作業系統的網路監控工具確認開放的埠號。  
- **Missing Directories** – 確保每個資料夾（`Indexer0`、`Searcher0` 等）皆已存在，且 Java 行程具備讀寫權限。  
- **Network Reachability** – 在轉為多機器設定時，將 `127.0.0.1` 改為實際主機 IP，並在防火牆開放所選埠號。  

## 實務應用

| 情境                     | 設定基礎埠號的好處                                 |
|--------------------------|---------------------------------------------------|
| 企業文件管理             | 跨部門無停機無縫擴展                               |
| 大型 CMS 平台            | 索引分散，使內容檢索更快                           |
| 法律案件管理             | 平行抽取 PDF，降低搜尋延遲                         |

## 效能考量

- **Monitor CPU/Memory** – 使用 Java 的 JMX 或效能分析工具監控執行緒使用情況。  
- **Adjust Compression** – `Compression.High` 可節省磁碟空間，但可能增加 CPU 負載；請測試 `High` 與 `Normal` 兩種設定以找出最佳平衡。  
- **Regular Updates** – 新版 GroupDocs.Search 常包含效能修補，請保持函式庫為最新版本。  

## 結論

您現在已學會如何 **configure base port groupdocs**，以及使用 GroupDocs.Search for Java 建立多節點搜尋網路。可嘗試新增更多節點、微調索引設定，並將此網路整合至現有應用程式，打造真正可擴展的搜尋解決方案。

## 常見問答

**Q: 為何在索引時停用停用詞？**  
A: 停用停用詞可保留在特定領域可能關鍵的常見詞彙，提升搜尋精確度。

**Q: 新增多個節點時，如何處理埠衝突？**  
A: 從較高的 `basePort`（例如 49100）開始，對每個後續節點遞增，確保每個節點擁有唯一的 TCP 端點。

**Q: 可以將此設定用於雲端應用程式嗎？**  
A: 可以——只需確保所選埠號在雲端安全群組中開放，並將 `127.0.0.1` 替換為相應的公有或私有 IP。

**Q: NormalIndex 與其他索引類型有何差異？**  
A: `NormalIndex` 在速度與記憶體使用之間提供平衡的取捨，而專門的索引（例如 `FastIndex`）則針對特定效能情境。

**Q: 新增節點的數量有上限嗎？**  
A: 技術上沒有；上限取決於您的硬體資源與網路頻寬。

---

**最後更新：** 2026-05-17  
**測試環境：** GroupDocs.Search Java 25.4  
**作者：** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## 相關教學

- [如何使用 GroupDocs.Search 與 Redaction 設定 .NET 搜尋網路](/search/net/search-network/configure-net-search-network-groupdocs/)
- [如何在 .NET 中使用 GroupDocs.Search 為文件管理系統實作搜尋網路](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [在 .NET 中使用 GroupDocs 部署搜尋網路節點以高效文件索引與檢索](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)