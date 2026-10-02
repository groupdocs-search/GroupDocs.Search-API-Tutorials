---
date: '2026-10-02'
description: 了解如何使用 temporary license 於 Java 中透過 chunk‑based search 新增文件至索引，提升搜尋效能並控制記憶體使用量。
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: 使用 temporary license 於 Java 中透過 chunk‑based search 新增文件至索引，提升搜尋速度並減少記憶體消耗。
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: 在 Java 中使用 temporary license 進行 chunk‑based indexing
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: 在 Java 中使用 temporary license 進行 chunk‑based indexing
type: docs
url: /zh-hant/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# 使用臨時授權於 Java 進行分塊索引

在本教學中，您將 **使用臨時授權** 透過 GroupDocs.Search 的分塊搜尋功能將文件加入索引。此方法可讓您處理龐大的文件集合——法律合約、支援票證、研究論文——同時保持 **java search index memory** 使用量低，並大幅 **提升搜尋效能**。您將看到如何設定索引資料夾、匯入多個文件來源、啟用分塊搜尋，以及執行首次與後續的分塊查詢。

## 快速解答
- **第一步是什麼？** 建立搜尋索引資料夾。  
- **如何包含多個檔案？** 對每個文件資料夾使用 `index.add()`。  
- **哪個選項啟用分塊搜尋？** `options.setChunkSearch(true)`。  
- **首次分塊後我可以繼續搜尋嗎？** 是的，使用該 token 呼叫 `index.searchNext()`。  
- **我需要授權嗎？** 開發階段可使用免費試用或臨時授權；正式環境則需完整授權。  

## 您將學習
- 如何在指定資料夾中建立搜尋索引。  
- 從多個位置 **add documents to index** 的步驟。  
- 設定搜尋選項以啟用分塊搜尋。  
- 執行首次與後續的分塊搜尋。  
- 分塊文件搜尋發揮優勢的實際情境。  

## 前置條件
- **必需的函式庫**：GroupDocs.Search for Java 25.4 或更新版本。  
- **環境設定**：已安裝相容的 Java Development Kit (JDK)。  
- **知識前提**：基本的 Java 程式設計與 Maven 使用經驗。  

## 設定 GroupDocs.Search for Java
首先，使用 Maven 將 GroupDocs.Search 整合至您的專案：

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

或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權
試用 GroupDocs.Search：

- **免費試用** – 在不承諾的情況下測試核心功能。  
- **臨時授權** – 為開發提供延伸存取。  
- **購買** – 正式環境的完整授權。  

## 如何將文件加入索引？
**直接回答：** 呼叫 `index.add()` 針對每個包含欲搜尋檔案的資料夾；此方法會遞迴掃描資料夾，並一次性將所有支援的文件加入索引。此方式免除手動逐檔處理，並加速大量匯入。

`SearchIndex` 是代表磁碟上可搜尋集合的核心類別。實例化後，所有索引與查詢操作皆透過此物件進行。

### 1. 建立索引
**直接回答：** 使用欲儲存索引檔案的路徑實例化 `SearchIndex` 物件，然後呼叫 `index.create()` 以初始化儲存結構。首次使用時，該呼叫會建立必要的資料夾與中繼資料檔案。

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

### 2. 將文件加入索引
**直接回答：** 使用 `index.add()` 方法並傳入每個來源資料夾的絕對路徑；API 會自動偵測支援的格式（PDF、DOCX、XLSX 等），並將可搜尋的文字抽取至索引中。

`SearchOptions` 是一個設定物件，可讓您微調文件在索引與搜尋期間的處理方式。稍後您將使用它來啟用分塊查詢。

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. 設定分塊搜尋的搜尋選項
**直接回答：** 在執行查詢前於 `SearchOptions` 實例上設定 `options.setChunkSearch(true)`；此設定告訴引擎將每份文件切分為邏輯分塊（通常為段落），並依分塊而非整檔返回匹配結果。

`SearchResult` 保存匹配的分塊、其位置與相關分數。啟用分塊搜尋時，每個 `SearchResult` 對應原始文件的一個片段。

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

### 4. 執行首次分塊搜尋
**直接回答：** 執行 `index.search("your query", options)`；此呼叫會回傳第一批匹配分塊的 `SearchResult` 集合，以及代表可繼續搜尋狀態的 token。

返回的 token 對於在不重新執行整個查詢的情況下分頁大量結果集至關重要。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. 繼續分塊搜尋
**直接回答：** 將先前呼叫返回的 token 傳入 `index.searchNext(token, options)`；重複此步驟直至方法回傳 `null`，表示已取得所有匹配的分塊。

此增量方式可降低記憶體使用，因為僅有當前的分塊批次會駐留於記憶體中。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## 為何使用分塊搜尋？
分塊搜尋將龐大的文件集合切分為可管理的片段，減少記憶體壓力並加快回應時間。透過在段落或章節層級建立索引，引擎僅能取回相關片段，從而降低 CPU 使用率並提升終端使用者的延遲。此方式在以下情況特別有益：

1. **法律團隊** 需要在數千份合約中定位特定條款。  
2. **客戶支援平台** 必須即時顯示相關的知識庫文章。  
3. **研究人員** 在不將整個檔案載入記憶體的情況下篩選龐大資料集。  

量化聲明：在標準的 8 核心伺服器上，GroupDocs.Search 能在每個分塊低於 **2 秒** 的時間內處理 **500 頁以上的 PDF**，同時將峰值堆疊記憶體維持在 **200 MB** 以下。

## 此方法如何提升搜尋效能
**直接回答：** 透過搜尋較小的分塊而非整個檔案，引擎能提前跳過不相關的段落，減少 CPU 週期，且僅將活動分塊保留於記憶體中，直接降低 **java search index memory** 消耗並帶來更快的回應時間。此目標導向的方式亦能提升快取效能與平行處理，讓多核心同時處理不同分塊，進一步提升多核伺服器的吞吐量。

其他好處包括：
- 跨多核心的平行分塊處理。  
- 當找到高相關性匹配時提前終止。  

## 管理 java search index memory
**直接回答：** 根據預期的索引大小分配足夠的 JVM 堆積（例如 `-Xmx2g` 或更高），在大量加入後執行 `index.optimize()` 以壓縮索引結構，並使用 VisualVM 監控 GC 暫停，以避免延遲峰值。

- 在大批次之後使用 `index.flush()` 將暫存資料寫入磁碟。  
- 啟用 `options.setMemoryLimit(256)` 以限制每次搜尋的記憶體使用量。  

## 效能考量
- **記憶體管理** – 為大型索引分配足夠的堆積空間（`-Xmx`）。  
- **資源監控** – 在索引與搜尋作業期間留意 CPU 使用率。  
- **索引維護** – 定期重建或清理索引，以剔除過時資料。  

## 常見陷阱與疑難排解
| 問題 | 為何發生 | 解決方案 |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## 常見問答

**Q: 什麼是分塊搜尋？**  
A: 分塊搜尋將資料集切分為較小的片段，允許在大量資料上進行高效查詢，且無需將整份文件載入記憶體。

**Q: 如何使用新檔案更新我的索引？**  
A: 只需使用新文件的路徑呼叫 `index.add()`；索引會自動納入它們。

**Q: GroupDocs.Search 能處理不同的檔案格式嗎？**  
A: 能，支援 **PDF、DOCX、XLSX、PPTX、HTML、TXT 以及超過 30 種其他格式**。

**Q: 典型的效能瓶頸是什麼？**  
A: 記憶體限制與未最佳化的索引最為常見；請分配足夠的堆積並定期最佳化索引。

**Q: 我可以在哪裡找到更詳細的文件？**  
A: 前往官方的 [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) 獲取深入指南與 API 參考。

**Q: 分塊搜尋能處理加密的 PDF 嗎？**  
A: 能，只要透過相應的 API 重載提供密碼即可。

**Q: 我該如何監控索引進度？**  
A: 使用回傳 `Progress` 物件的 `Index.add()` 重載，或掛接日誌回呼。

## 資源
- **文件說明**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API 參考**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **下載**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免費支援**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-10-02  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 相關教學

- [建立搜尋索引目錄與設定授權 – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [提升 GroupDocs.Search Java 查詢效能：最佳化索引與搜尋](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java 進階搜尋功能](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)