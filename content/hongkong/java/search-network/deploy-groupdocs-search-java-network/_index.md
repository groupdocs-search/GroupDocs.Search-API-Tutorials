---
date: '2026-01-19'
description: 學習如何配置分散式搜尋，並使用 GroupDocs.Search for Java 部署強大的搜尋網路，以提升效能與可擴展性。
keywords:
- GroupDocs.Search Java network
- search performance enhancement
- distributed search architecture
title: 使用 GroupDocs.Search Java 網絡配置分散式搜尋
type: docs
url: /zh-hant/java/search-network/deploy-groupdocs-search-java-network/
weight: 1
---

引您設置一個強大的 GroupDocs.Search for Java 網路，說明如何 **how to deploy search** 跨多個節點、將文件加入索引，以及 **configure TCP settings** 以確保可靠的通訊。完成後，您將擁有可投入生產的可擴展搜尋解決方案。

## 快速解答
- **What is configure distributed search?** 它是設定多個搜尋節點共同工作以有效索引與查詢資料的過程。  
- **How many nodes are recommended?** 通常 3‑5 個節點可提供性能與容錯的良好平衡。  
- **Do I need a license?** 是 – 需要臨時或正式授權才能在生產環境使用。  
- **Which ports should I use?** 請選擇伺服器上未被佔用的埠口；範例使用 49136‑49139。  
- **Can I add new documents after deployment?** 當然可以 – 您可以隨時 **add documents to index**，而無需重新啟動網路。

## 什麼是 configure distributed search？
設定分散式搜尋架構意味著將多個獨立的搜尋節點連結起來，使其共同分擔索引工作並集體回應查詢。這可減輕單一機器的負載，並提升吞吐量與可靠性。

## 為何使用 GroupDocs.Search for Java？
- **High performance** – 原生 Java 實作優化了索引速度。  
- **Scalable design** – 可在不進行大幅重新設定的情況下新增或移除節點。  
- **Rich document support** – 支援 PDF、Word 檔案、電子郵件等多種文件。  
- **Simple TCP communication** – 內建的 `TcpSettings` 讓您微調網路延遲。

## 前置條件

### 必要的函式庫與相依性
您需要 **GroupDocs.Search for Java** 版本 25.4 或更新版本。請確保開發環境已安裝 Java。

### 環境設定需求
- 已在機器上安裝 Java Development Kit (JDK)  
- 使用 IntelliJ IDEA 或 Eclipse 等 IDE  

### 知識前提
具備基本的 Java 程式設計技能以及對網路設定的基本了解，將有助於您順利完成以下步驟。

## 設定 GroupDocs.Search for Java
要開始使用，請將 GroupDocs.Search for Java 加入您的專案。您可以透過 Maven 或直接下載函式庫來完成。

**Maven 設定**  
在您的 `pom.xml` 檔案中加入以下儲存庫與相依性設定：

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

**直接下載**  
或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權
為了完整使用 GroupDocs.Search，您可以取得臨時授權或購買正式授權。請前往 [GroupDocs's licensing page](https://purchase.groupdocs.com/temporary-license/) 了解如何取得免費試用或正式授權的更多資訊。

### 基本初始化與設定
讓我們在 Java 應用程式中初始化 GroupDocs.Search：

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        // Add documents to the index
        index.add("YOUR_DOCUMENT_DIRECTORY");
    }
}
```

## 實作指南
本節將引導您使用 GroupDocs.Search for Java 設定與部署搜尋網路。

### 如何使用 GroupDocs.Search 設定分散式搜尋
在搜尋架構中部署多個節點可實現分散式索引與搜尋，提升效能與可擴展性。本指南示範如何有效設定這些節點。

#### 設定網路
首先設定基礎路徑與埠口的組態。此步驟同時 **configures TCP settings**，定義節點之間的通訊方式：

```java
Configuration configuration = ConfiguringSearchNetwork.configure("YOUR_DOCUMENT_DIRECTORY", 49136);
```

#### 部署節點
接著，使用先前設定的參數部署搜尋網路節點：

```java
public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
    // Define timeouts for sending and receiving data over the network.
    int sendTimeout = 3000;
    int receiveTimeout = 3000;

    // Create and start three nodes that can run on separate servers or together.
    SearchNetworkNode node1 = new SearchNetworkNode(
        1,
        basePath + "Node1",
        new TcpSettings(basePort + 1, sendTimeout, receiveTimeout)
    );
    node1.start();

    SearchNetworkNode node2 = new SearchNetworkNode(
        2,
        basePath + "Node2",
        new TcpSettings(basePort + 2, sendTimeout, receiveTimeout)
    );
    node2.start();

    SearchNetworkNode node3 = new SearchNetworkNode(
        3,
        basePath + "Node3",
        new TcpSettings(basePort + 3, sendTimeout, receiveTimeout)
    );
    node3.start();

    // Create and configure the main configuration node.
    SearchNetworkNode node0 = new SearchNetworkNode(
        0,
        basePath + "Node0",
        new TcpSettings(basePort, sendTimeout, receiveTimeout),
        new ConsoleLogger(),
        configuration
    );

    // Add an event handler to notify when the configuration is complete.
    node0.getEvents().ConfigurationCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            // Event handling logic here (e.g., logging)
        }
    });

    // Configure all nodes in the network using the main configuration node.
    node0.configureAllNodes();

    // Start the search network by launching all configured nodes.
    node0.start();

    // Return an array of all deployed nodes.
    return new SearchNetworkNode[] {node0, node1, node2, node3};
}
```

### 疑難排解技巧
- 確認每個節點的目錄已正確指定且可存取。  
- 檢查網路設定，特別是埠口設定，以避免衝突。  
- 監控日誌以發現任何組態錯誤或警告。  

## 實務應用
部署分散式搜尋網路在多種情境下皆有益處：

1. **Large‑Scale Enterprise Systems** – 加強在龐大文件庫中的搜尋能力。  
2. **Content Management Platforms** – 在高流量且資料量巨大的網站上提升效能。  
3. **E‑commerce Websites** – 加速商品搜尋，提供更順暢的客戶體驗。  

## 效能考量
為了讓您的 **configure distributed search** 環境高效運作：

- 定期更新索引以反映資料變更。  
- 監控 CPU、記憶體與磁碟使用情況；必要時調整 `TcpSettings` 超時設定。  
- 根據工作負載套用 Java 記憶體調校旗標（`-Xmx`、`-Xms`）。

## 結論
透過本教程，您已學會 **configure distributed search** 並部署可擴展的 GroupDocs.Search Java 網路。此解決方案能顯著提升應用程式搜尋功能的速度與可靠性。

### 後續步驟
探索進階功能，如自訂分析器、同義詞處理與即時索引，以進一步優化搜尋體驗。

### 行動呼籲
立即在您的專案中實作此強大解決方案，親身體驗效能提升！

## 常見問答
**Q1: What is GroupDocs.Search for Java?**  
**A1:** GroupDocs.Search for Java 是一套功能強大的函式庫，可在各種文件格式中執行文字搜尋，提供高效的索引與查詢能力。

**Q2: How do I obtain a temporary license for GroupDocs.Search?**  
**A2:** 前往 [GroupDocs licensing page](https://purchase.groupdocs.com/temporary-license/) 取得免費試用或正式授權。

**Q3: Can this network configuration be used with other document types?**  
**A4:** 是的，GroupDocs.Search 支援多種文件格式，具備廣泛的應用彈性。

**Q4: What**  
**A4:** 常見問題確以避免此