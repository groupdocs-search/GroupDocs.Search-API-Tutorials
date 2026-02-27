---
date: '2026-02-27'
description: 學習如何使用 GroupDocs.Search for Java 建立可搜尋的 Java 索引、將檔案加入搜尋、將目錄新增至節點，並啟用即時索引功能。
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: 建立可搜尋索引（Java） – 部署 GroupDocs.Search for Java
type: docs
url: /zh-hant/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# 建立可搜尋索引 (Java) – 部署 GroupDocs.Search for Java

在當今資料驅動的世界，**建立可搜尋索引 (Java)** 的應用程式需要有效處理大量文件集合。無論您是建置企業級搜尋服務或較小的專案，良好配置的搜尋網路都能顯著提升檢索速度與相關性。本指南將一步步說明如何設定 **GroupDocs.Search for Java**，從將檔案加入搜尋到將目錄加入節點，讓您立即開始為文件建立索引。

> **為何重要：** 可搜尋索引可將查詢延遲從秒級降低至毫秒級，隨資料成長而擴展，並讓任何基於 Java 的解決方案（無論是網站入口、桌面應用程式或雲端微服務）都能加入強大的全文功能。

## 快速答覆
- **GroupDocs.Search 的主要目的為何？** 提供一個可擴展、基於 Java 的引擎，用於在分散式網路中索引與搜尋文件。  
- **應該使用哪個版本？** 建議在新專案中使用最新的穩定版（例如 25.4）。  
- **需要授權嗎？** 提供 30 天免費試用；正式上線需購買永久授權。  
- **可以同時加入檔案與整個目錄嗎？** 可以 — 使用 `addFiles` 與 `addDirectories` 輔助方法匯入內容。  
- **需要哪個 Java 版本？** Java 8 或以上，並使用 Maven 管理相依性。  
- **即時索引 (Java) 如何運作？** 透過訂閱節點事件，可在檔案變更時自動觸發重新索引。

## 什麼是「建立可搜尋索引 (Java)」？
在 Java 中建立可搜尋索引意味著構建一個將詞彙映射到包含該詞彙的文件的資料結構，從而支援快速的全文查詢。GroupDocs.Search 負責繁重的工作，讓您專注於提供文件與調校搜尋行為。

## 為何使用 GroupDocs.Search for Java？
- **可擴展的網路架構** – 部署多個節點共同分擔索引工作負載。  
- **豐富的文件格式支援** – PDF、Word、Excel、PowerPoint、影像等多種格式。  
- **事件驅動的更新** – 訂閱節點事件，即時保持索引最新。  
- **簡易的 Maven 整合** – 在 `pom.xml` 中加入幾行即可開始索引。

## 使用 GroupDocs.Search 的即時索引 (Java)
GroupDocs.Search 會在檔案新增、更新或移除時觸發事件。處理這些事件即可自動呼叫 `addFiles` 或 `addDirectories`，確保索引與檔案系統同步，無需人工介入。此方式特別適合文件管理系統、內容入口網站以及任何資料變動頻繁的應用程式。

## 前置條件
- **JDK 8+** 已安裝於開發機器。  
- 使用 **IntelliJ IDEA** 或 **Eclipse** 等 IDE。  
- 具備 **Java** 與 **Maven** 的基本知識。  
- 取得 **GroupDocs.Search for Java** 函式庫（下載或透過 Maven）。

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

> **小技巧：** 請定期檢查官方發行頁面，保持版本號為最新。

您也可以直接從官方網站下載 JAR 檔案： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 授權取得
- **免費試用：** 30 天評估。  
- **臨時授權：** 申請延長測試。  
- **購買授權：** 正式上線必須購買。

### 基本初始化
建立一個指向索引檔案儲存資料夾，並定義基礎通訊埠的設定物件：

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

## 如何使用 GroupDocs.Search 建立可搜尋索引 (Java)？

以下說明您在 **將檔案加入搜尋** 與 **將目錄加入節點** 時所需的核心功能，同時部署可擴展的網路。

### 功能 1 – 設定與網路建置
設定搜尋網路是建立可搜尋索引的第一步。

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

- **`basePath`** – 索引資料將被持久化的目錄。  
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

每個 `SearchNetworkNode` 都會執行自己的索引服務，使您能 **建立可搜尋索引 (Java)**，實現水平擴展。

### 功能 3 – 訂閱節點事件
即時更新可讓索引與檔案系統變更保持同步。

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
使用此輔助方法 **將目錄加入節點**，遞迴收集所有支援的文件。

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
若需要更細緻的控制，可 **將檔案逐一加入搜尋**：

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

此方法讓您能彈性索引來自串流、雲端儲存或暫存位置的檔案。

## 常見使用情境
- **企業文件入口**：需要即時搜尋上千份 PDF 與 Office 檔案。  
- **法律 e‑discovery 平台**：新證據持續加入，必須即時可搜尋。  
- **內容管理系統**：儲存影像、簡報與試算表，需支援全文查詢。

## 常見問題與解決方案
| 問題 | 原因 | 解決方式 |
|------|------|----------|
| **搜尋結果中未顯示任何文件** | 索引未提交 | 在加入檔案後呼叫 `node.getIndexer().commit()`。 |
| **埠衝突錯誤** | 其他服務佔用了 `basePort` | 改用其他 `basePort`，或確認可用埠號。 |
| **不支援的檔案格式** | 函式庫缺少相應解析器 | 確認檔案副檔名受支援，或自行加入自訂擷取器。 |

## 疑難排解小技巧
- **驗證節點健康狀態：** 使用內建的健康檢查端點 (`http://localhost:{port}/health`) 確認每個節點是否正常運作。  
- **監控記憶體使用量：** 大批文件可能導致記憶體激增，建議分批索引並定期呼叫 `commit()`。  
- **檢查日誌：** GroupDocs.Search 會將詳細日誌寫入 `basePath` 資料夾，請檢視其中的解析錯誤或網路逾時資訊。

## 常見問答

**Q: 可以在雲端的 Java 應用程式上使用 GroupDocs.Search 嗎？**  
A: 可以。此函式庫相容任何 Java 執行環境，您只需將 `basePath` 指向網路掛載資料夾或本機掛載的雲端儲存即可。

**Q: 檔案變更時要如何更新索引？**  
A: 訂閱節點事件（參見功能 3），然後對修改過的路徑再次呼叫 `addFiles` 或 `addDirectories`。

**Q: 部署的節點數量有上限嗎？**  
A: 實際上限取決於您的硬體與網路頻寬，API 本身並無硬性上限。

**Q: 加入新檔案後需要重新啟動節點嗎？**  
A: 不需要。加入檔案會自動觸發索引，只有在延遲提交時才需要手動呼叫 `commit()`。

**Q: 預設支援哪些文件格式？**  
A: PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、TXT、HTML 以及多種影像格式。完整列表請參閱官方文件。

**Q: 如何為持續上傳檔案的資料夾啟用即時索引 (Java)？**  
A: 實作檔案系統監聽器（例如 `java.nio.file.WatchService`），在偵測到新檔案時呼叫 `DirectoryAdder.addDirectories(node, path)`。

---

**最後更新：** 2026-02-27  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs