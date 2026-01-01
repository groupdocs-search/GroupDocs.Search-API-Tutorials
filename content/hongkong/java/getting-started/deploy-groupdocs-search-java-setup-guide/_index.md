---
date: '2025-12-26'
description: 學習如何使用 GroupDocs.Search for Java 建立可搜尋的 Java 索引、將檔案加入搜尋以及將目錄加入節點。
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: 建立可搜尋索引（Java） – 部署 GroupDocs.Search for Java
type: docs
url: /zh-hant/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# 建立可搜尋索引 Java – 部署 GroupDocs.Search for Java

在當今資料驅動的世界，**creating a searchable index java** 應用程式需要有效地處理大量文件集合。無論您是構建企業級搜尋服務還是較小的專案，良好配置的搜尋網路都能顯著提升檢索速度與相關性。本指南將逐步說明如何設定 **GroupDocs.Search for Java**，從將檔案加入搜尋到將目錄加入節點，讓您立即開始為文件建立索引。

## 快速解答
- **What is the primary purpose of GroupDocs.Search?** 它提供一個可擴展的、基於 Java 的引擎，用於在分散式網路中對文件進行索引和搜尋。  
- **Which version should I use?** 建議新專案使用最新的穩定版（例如 25.4）。  
- **Do I need a license?** 提供 30 天免費試用；正式環境需購買永久授權。  
- **Can I add both files and whole directories?** 可以 – 使用 `addFiles` 與 `addDirectories` 輔助方法匯入內容。  
- **What Java version is required?** 需要 Java 8 或更高版本，並使用 Maven 進行相依管理。

## 什麼是 “create searchable index java”？
在 Java 中建立可搜尋索引是指構建一種資料結構，將詞彙映射到包含該詞彙的文件，以實現快速的全文查詢。GroupDocs.Search 抽象化了繁重的工作，讓您專注於提供文件與調整搜尋行為。

## 為什麼要使用 GroupDocs.Search for Java？
- **Scalable network architecture** – 部署多個節點以分擔索引工作負載。  
- **Rich document format support** – 支援 PDF、Word、Excel、PowerPoint、影像等多種文件格式。  
- **Event‑driven updates** – 訂閱節點事件，以即時保持索引最新。  
- **Simple Maven integration** – 在 `pom.xml` 中加入少量程式碼即可開始索引。

## 前置條件
- **JDK 8+** 已安裝於開發機器上。  
- 如 **IntelliJ IDEA** 或 **Eclipse** 等 IDE。  
- 具備 **Java** 與 **Maven** 的基礎知識。  
- 取得 **GroupDocs.Search for Java** 函式庫（下載或透過 Maven）。

## 設定 GroupDocs.Search for Java

### Maven 依賴
將儲存庫與相依加入您的 `pom.xml`：

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

> **Pro tip:** 請透過官方發佈頁面保持版本號為最新。

您也可以直接從官方網站下載 JAR 檔案：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權
- **Free Trial:** 30 天評估。  
- **Temporary License:** 申請延長測試。  
- **Purchase:** 正式部署需購買授權。

### 基本初始化
建立一個指向儲存索引檔案的資料夾並定義基礎通訊埠的設定物件：

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## 如何使用 GroupDocs.Search 建立 searchable index java？
以下我們將分解您需要的核心功能，包括 **add files to search** 與 **add directories to node**，同時部署可擴展的網路。

### 功能 1 – 配置與網路設定
配置搜尋網路是建立可搜尋索引的第一步。

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – 用於持久化索引資料的目錄。  
- **`basePort`** – 起始埠號；每個節點會在此基礎上遞增。

### 功能 2 – 部署搜尋網路節點
部署節點可將索引工作負載分散至多台機器或多個程序。

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

每個 `SearchNetworkNode` 都會執行自己的索引服務，使您能夠 **create a searchable index java** 以水平擴展。

### 功能 3 – 訂閱節點事件
即時更新可保持索引與檔案系統變更同步。

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

透過監聽事件，您可以在新檔案到達時自動觸發重新索引。

### 功能 4 – 將目錄加入網路節點
使用此輔助方法 **add directories to node**，遞迴收集所有支援的文件。

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### 功能 5 – 將檔案加入網路節點
當需要細粒度控制時，可個別 **add files to search**：

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

此方法讓您能彈性地索引來自串流、雲端儲存或臨時位置的檔案。

## 常見問題與解決方案
| 問題 | 原因 | 解決方法 |
|-------|--------|-----|
| **搜尋結果未顯示文件** | 索引未提交 | 在加入檔案後呼叫 `node.getIndexer().commit()`。 |
| **埠衝突錯誤** | 其他服務使用了 `basePort` | 選擇不同的 `basePort` 或確認可用埠號。 |
| **不支援的檔案格式** | 函式庫缺少相應的解析器 | 確保檔案副檔名受支援，或加入自訂的擷取器。 |

## 常見問答

**Q: Can I use GroupDocs.Search on a cloud‑based Java application?**  
A: 是的。此函式庫可在任何 Java 執行環境下運作，且您可以將 `basePath` 指向網路掛載的資料夾或本機掛載的雲端儲存。

**Q: How do I update the index when a file changes?**  
A: 訂閱節點事件（參見功能 3），並對已修改的路徑再次呼叫 `addFiles` 或 `addDirectories`。

**Q: Is there a limit to the number of nodes I can deploy?**  
A: 實際上，限制取決於您的硬體與網路頻寬。API 本身沒有硬性上限。

**Q: Do I need to restart nodes after adding new files?**  
A: 不需要。加入檔案會自動觸發索引；若延遲提交，則需手動呼叫 commit。

**Q: Which document formats are supported out of the box?**  
A: 支援 PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、TXT、HTML 以及多種影像格式。完整清單請參考官方文件。

---

**Last Updated:** 2025-12-26  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs