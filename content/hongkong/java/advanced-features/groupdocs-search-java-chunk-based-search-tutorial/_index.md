---
date: '2026-02-21'
description: 了解如何在 Java 中使用 GroupDocs.Search 透過分塊搜尋將文件加入索引，提升搜尋效能，並為大型文件集優化 Java 搜尋索引記憶體。
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: 在 Java 中使用分段搜尋將文件加入索引
type: docs
url: /zh-hant/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# 在 Java 中使用基於區塊的搜尋將文件加入索引

在現代應用程式中，需要快速 **將文件加入索引**，並執行快速的基於區塊的查詢時，您會希望有一個能夠在不耗盡記憶體的情況下擴展的解決方案。本教學將指導您設定 GroupDocs.Search for Java、加入多個文件資料夾，並配置引擎以 **提升搜尋效能**，同時將 **java search index memory** 使用量控制在合理範圍。無論您是索引法律合約、支援票證或研究論文，以下步驟都能提供可投入生產環境的實作方式。

## 快速答覆
- **第一步是什麼？** 建立搜尋索引資料夾。  
- **如何加入大量檔案？** 為每個文件資料夾使用 `index.add()`。  
- **哪個選項可啟用區塊搜尋？** `options.setChunkSearch(true)`。  
- **我可以在第一個區塊之後繼續搜尋嗎？** 可以，使用該 token 呼叫 `index.searchNext()`。  
- **我需要授權嗎？** 免費試用或臨時授權可用於開發；正式環境則需完整授權。  

## 您將學習到
- 如何在指定資料夾中建立搜尋索引。  
- 從多個位置 **將文件加入索引** 的步驟。  
- 設定搜尋選項以啟用基於區塊的搜尋。  
- 執行首次及後續的基於區塊的搜尋。  
- 基於區塊的文件搜尋在實務情境中的應用。  

## 前置條件
- **必要函式庫**：GroupDocs.Search for Java 25.4 或更新版本。  
- **環境設定**：已安裝相容的 Java Development Kit (JDK)。  
- **知識前提**：基本的 Java 程式設計與 Maven 使用經驗。  

## 設定 GroupDocs.Search for Java
首先，使用 Maven 將 GroupDocs.Search 整合至您的專案中：

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

或者，從 [GroupDocs.Search for Java 版本發佈頁面](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權
試用 GroupDocs.Search：

- **免費試用** – 測試核心功能，無需承諾。  
- **臨時授權** – 為開發提供延長存取。  
- **購買** – 正式環境的完整授權。  

### 基本初始化與設定
在您希望儲存可搜尋資料的資料夾中建立索引：

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## 如何將文件加入索引
既然索引已建立，接下來的合理步驟是從檔案所在位置 **將文件加入索引**。

### 1. 建立索引
**概述**：設定搜尋索引的目錄。

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. 加入文件至索引
**概述**：從多個來源資料夾匯入檔案。

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. 設定區塊搜尋的搜尋選項
透過調整 options 物件以啟用基於區塊的搜尋。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. 執行首次基於區塊的搜尋
使用已啟用區塊的選項執行首次查詢。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. 繼續基於區塊的搜尋
持續遍歷剩餘的區塊，直至搜尋完成。

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 為何使用基於區塊的搜尋？
基於區塊的搜尋將龐大的文件集合切分為可管理的片段，降低記憶體壓力並加快回應時間。特別適用於以下情況：

1. **法律團隊** 需要在數千份合約中快速定位特定條款。  
2. **客服平台** 必須即時顯示相關的知識庫文章。  
3. **研究人員** 在不將整個檔案載入記憶體的情況下，篩選龐大資料集。  

## 此方法如何 **提升搜尋效能**
透過搜尋較小的區塊而非整個檔案，引擎能夠：

- • 及早跳過不相關的段落，減少 CPU 週期。  
- • 僅在記憶體中保留當前區塊，直接降低 **java search index memory** 消耗。  
- • 在多核心機器上平行處理區塊，以獲得更快的結果。  

## 管理 **java search index memory**
雖然基於區塊的搜尋已降低記憶體佔用，您仍可進一步調整 JVM：

- • 根據索引大小分配足夠的堆積記憶體（例如 `-Xmx2g` 或更高）。  
- • 大量加入後使用 `index.optimize()` 壓縮索引結構。  
- • 使用 VisualVM 等工具監控 GC 暫停，以避免延遲峰值。  

## 效能考量
- **記憶體管理** – 為大型索引分配足夠的堆積空間（`-Xmx`）。  
- **資源監控** – 在索引與搜尋作業期間留意 CPU 使用率。  
- **索引維護** – 定期重建或清理索引，以移除過時資料。  

## 常見問題與故障排除
| 問題 | 為何發生 | 解決方式 |
|-------|----------------|-----|
| 索引期間發生 `OutOfMemoryError` | 堆積大小不足 | 增加 JVM 堆積 (`-Xmx2g` 或更高) |
| 沒有返回結果 | 區塊 token 未被處理 | 確保 `while` 迴圈執行至 `getNextChunkSearchToken()` 為 `null` |
| 搜尋效能緩慢 | 索引未最佳化 | 在大量加入後執行 `index.optimize()` |

## 常見問答

**Q: 什麼是基於區塊的搜尋？**  
A: 基於區塊的搜尋將資料集切分為較小的片段，讓在大量資料上執行高效查詢，而無需將整個文件載入記憶體。

**Q: 如何使用新檔案更新我的索引？**  
A: 只需使用新文件的路徑呼叫 `index.add()`；索引會自動納入這些文件。

**Q: GroupDocs.Search 能處理不同的檔案格式嗎？**  
A: 能，支援 PDF、DOCX、XLSX、PPTX 以及許多其他常見格式。

**Q: 典型的效能瓶頸是什麼？**  
A: 記憶體限制與未最佳化的索引最為常見；請分配足夠的堆積並定期最佳化索引。

**Q: 我可以在哪裡找到更詳細的文件說明？**  
A: 請前往官方的 [GroupDocs.Search 文件說明](https://docs.groupdocs.com/search/java/)，獲取深入指南與 API 參考。

**Q: 基於區塊的搜尋能處理加密的 PDF 嗎？**  
A: 能，只要透過相應的 API 重載提供密碼即可。

**Q: 我如何監控索引進度？**  
A: 使用回傳 `Progress` 物件的 `Index.add()` 重載，或掛接日誌回呼函式。

## 資源
- **文件說明**： [GroupDocs.Search for Java 文件](https://docs.groupdocs.com/search/java/)  
- **API 參考**： [GroupDocs.Search API 參考](https://reference.groupdocs.com/search/java)  
- **下載**： [GroupDocs.Search 版本發佈](https://releases.groupdocs.com/search/java/)  
- **GitHub**： [GroupDocs.Search GitHub 倉庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免費支援**： [GroupDocs 論壇](https://forum.groupdocs.com/c/search/10)  
- **臨時授權**： [取得臨時授權](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-02-21  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

---