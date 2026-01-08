---
date: '2026-01-08'
description: 學習如何在 Java 應用程式中使用 GroupDocs.Search 進行搜尋結果高亮顯示、設定可擴展的搜尋、網絡部署以及結果高亮。
keywords:
- GroupDocs.Search Java
- distributed searching Java
- highlight search results Java
title: 使用 GroupDocs.Search 在 Java 中突顯搜尋結果
type: docs
url: /zh-hant/java/licensing-configuration/groupdocs-search-java-implementation/
weight: 1
---

# 使用 GroupDocs.Search 的 Java 高亮搜尋結果

如果你已厭倦手動篩選無盡的文件，**highlight search results java** 提供了一種快速、可靠的方式，直接顯示你所需的內容。在本教學中，我們將一步步說明如何設定分散式搜尋網路、建立索引、執行查詢，最後在文件內直接高亮匹配項目。完成後，你將擁有一套可在多節點上擴展的生產環境解決方案，讓相關詞彙即時凸顯。

## 快速解答
- **「highlight search results java」是什麼意思？** 它指的是在使用 Java 函式庫（如 GroupDocs.Search）時，程式化地在文件中標記找到的關鍵字。  
- **我可以在同一文件中高亮多個詞彙嗎？** 可以 – 使用 `HighlightOptions` 來定義每個匹配前後顯示多少詞彙。  
- **執行此範例需要授權嗎？** 測試時可使用免費試用或臨時授權；正式上線則需正式授權。  
- **需要哪個 Java 版本？** Java 8 或更新版本。  
- **此方法適用於大型文件集合嗎？** 完全適用 – 搜尋網路會將索引與查詢負載分散到多個節點。

## 什麼是 Highlight Search Results Java？
**Highlight search results java** 是指將搜尋查詢套用於文件，找出匹配的片段，並以視覺方式強調這些片段（例如以標記包圍或回傳高亮的摘要）。這讓最終使用者在不必開啟整個檔案的情況下，快速看到每個匹配的上下文。

## 為什麼使用 GroupDocs.Search 進行高亮？
GroupDocs.Search 提供即時可用的高效能引擎，支援數十種檔案格式、分散式索引與內建的片段高亮功能。它免除自行撰寫解析器或管理底層搜尋基礎設施的需求，讓你專注於提供流暢的使用者體驗。

## 前置條件

- **Java Development Kit (JDK) 8+** – 確認 `java -version` 顯示 1.8 或更高。  
- **Maven** – 用於相依管理。  
- **GroupDocs.Search for Java 25.4** – 本指南所使用的版本。  
- 建議使用 **IntelliJ IDEA** 或 **Eclipse** 等 IDE（非必須）。  
- 具備基本的 Java 與網路概念。

## 設定 GroupDocs.Search for Java

你可以透過 Maven 或直接下載 JAR 檔的方式將函式庫加入專案。

### Maven 設定
將以下儲存庫與相依項目加入 `pom.xml`：

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
或是從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR 檔。

### 取得授權步驟
- **免費試用：** 先取得試用版以探索核心功能。  
- **臨時授權：** 從 [此頁面](https://purchase.groupdocs.com/temporary-license/) 取得延長測試授權。  
- **正式購買：** 為正式上線取得完整授權。

### 基本初始化與設定
建立指向索引資料夾的 `Index` 實例：

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an instance of Index
        Index index = new Index("path/to/index/directory");
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## 實作指南

### 如何在分散式網路中使用 Highlight Search Results Java 進行高亮

#### 設定搜尋網路
首先，定義文件所在位置與網路使用的埠號。

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/HighlightingResultsInNetwork/";
int basePort = 49116; // Change if port is busy

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **`basePath`** – 包含欲索引檔案的根目錄。  
- **`basePort`** – 節點間通訊的 TCP 埠號，請選擇未被佔用的埠號。

#### 部署搜尋網路節點
依照設定部署一個或多個節點，第一個節點會自動成為主節點。

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```

- **`nodes`** – 所有運行中節點的陣列。  
- **`masterNode`** – 負責協調索引與查詢分發。

#### 訂閱搜尋網路節點事件
將監聽器附加到主節點，以即時接收通知（例如索引完成時）。

```java
import com.groupdocs.search.scaling.events.*;

SearchNetworkNodeEvents.subscribe(masterNode);
```

#### 在網路節點中索引目錄
將節點指向欲索引的資料夾。輔助類別 `Utils.DocumentsPath` 會解析為範例資料夾。

```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.options.*;

IndexingDocuments.addDirectories(masterNode, Utils.DocumentsPath);
```

#### 在網路節點間搜尋文字
對 **所有** 節點執行查詢，取得匹配的文件。

```java
import java.util.ArrayList;
import com.groupdocs.search.scaling.results.*;

ArrayList<NetworkFoundDocument> documents = TextSearchInNetwork.searchAll(masterNode, "ipsum", false);
highlightInDocument(masterNode, documents.get(0), 3); // Highlight results from the first found document.
```

- 將 `"ipsum"` 替換為你想搜尋的任意詞彙。  
- 接下來的 `highlightInDocument` 方法會套用高亮。

#### 多關鍵字文件高亮 – Highlighting Search Results
以下方法示範如何在每個匹配周圍取得片段，同時說明如何控制顯示的前後詞彙數量，以滿足 **highlight multiple terms document** 的需求。

```java
import com.groupdocs.search.highlighters.*;
import com.groupdocs.search.options.*;

public static void highlightInDocument(
    SearchNetworkNode node,
    NetworkFoundDocument document,
    int maxFragments) {
    
    Searcher searcher = node.getSearcher();
    FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.PlainText);

    HighlightOptions options = new HighlightOptions();
    options.setTermsAfter(5);
    options.setTermsBefore(5);
    options.setTermsTotal(15);

    searcher.highlight(document, highlighter, options); // Perform highlighting on the document.

    FragmentContainer[] result = highlighter.getResult();
    for (FragmentContainer container : result) {
        if (container.getCount() == 0) continue;

        String[] fragments = container.getFragments();
        int count = Math.min(fragments.length, maxFragments);
        for (int j = 0; j < count; j++) {
            // Print each fragment within the specified limit.
        }
    }
}
```

- **`OutputFormat.PlainText`** – 回傳純文字摘要；如需更豐富的 UI 可改為 HTML。  
- **`HighlightOptions`** – 控制每個匹配前後包含多少字詞（`setTermsBefore`、`setTermsAfter`）。  
- **`maxFragments`** – 限制每份文件顯示的摘要片段數量。

#### 關閉網路節點
完成後，關閉所有節點以釋放資源。

```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## 實務應用

- **企業文件管理：** 集中公司檔案，讓員工即時定位相關合約或政策。  
- **法律案件檔案：** 透過高亮關鍵法律詞彙快速找出先例文件。  
- **研發知識庫：** 研究人員可搜尋專利或技術論文，直接看到高亮摘錄。  
- **電商目錄：** 讓購物者以關鍵字搜尋商品，並在說明中看到高亮匹配。  
- **圖書館系統：** 讀者可跨千本書籍搜尋，無需逐一開啟即可查看高亮段落。

## 效能考量

- **保持索引即時更新：** 每晚重新索引變更的檔案或使用增量更新。  
- **利用多節點：** 分散索引與查詢負載，避免瓶頸。  
- **調整 `HighlightOptions`：** 減少 `termsBefore/After` 可降低大型文件的記憶體使用。

## 常見問題與故障排除

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| 沒有返回結果 | 索引未建立或指向錯誤資料夾 | 檢查 `Utils.DocumentsPath`，重新執行 `IndexingDocuments.addDirectories` |
| 高亮輸出為空 | `HighlightOptions` 設定過低或文件編碼問題 | 增加 `termsTotal`，或確認文件編碼受支援 |
| 埠衝突錯誤 | `basePort` 已被佔用 | 改用其他埠號（例如 49117） |
| 授權例外 | 缺少或過期的授權檔案 | 將有效的 `GroupDocs.Search.lic` 放置於應用程式根目錄 |

## 常見問答

**Q: 可以部署多個搜尋網路節點以做負載平衡嗎？**  
A: 可以，部署多個節點可分散索引與查詢工作，提升可擴充性與回應速度。

**Q: 如何在同一文件中高亮多個搜尋詞彙？**  
A: 將詞彙清單傳入 `highlight` 方法，並使用 `HighlightOptions` 設定每個匹配的前後顯示詞彙數。

**Q: 能否訂閱即時搜尋事件？**  
A: 完全可以。使用 `SearchNetworkNodeEvents.subscribe(masterNode)` 取得索引進度、查詢執行與錯誤的回呼。

**Q: GroupDocs.Search 支援哪些檔案格式進行索引與高亮？**  
A: 超過 50 種格式，包括 DOCX、PDF、HTML、TXT、PPTX 等。

**Q: 如何在超大型集合上提升搜尋速度？**  
A: 定期更新索引、將索引分散到多個節點，並微調 `HighlightOptions` 以限制片段大小。

## 結論
依照本指南，你現在已擁有一套完整、可投入生產環境的 **highlight search results java** 解決方案，使用 GroupDocs.Search 可在網路上擴展、索引任何支援的文件類型、快速查詢，並回傳高亮摘要，協助使用者精準找到所需資訊。接下來可探索將結果整合至 Web UI、加入分面搜尋，或結合 OCR 以支援掃描 PDF。

---

**最後更新：** 2026-01-08  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs