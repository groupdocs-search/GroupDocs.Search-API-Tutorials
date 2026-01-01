---
date: '2025-12-19'
description: 了解如何在 Java 中使用 GroupDocs.Search 將文件加入索引並啟用分段搜尋，以提升大型文件集的效能。
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: 在 Java 中使用基於區塊的搜尋將文件加入索引
type: docs
url: /zh-hant/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# 使用 Java 進行分塊搜尋，將文件加入索引

在當今以資料為驅動的世界中，能夠快速 **add documents to index** 並執行分塊搜尋，對於處理大量檔案的任何應用程式都是必不可少的。無論您是處理法律合約、客戶支援檔案庫，或是龐大的研究資料庫，本教學將逐步說明如何設定 GroupDocs.Search for Java，以高效建立索引並以分塊方式取得相關資訊。

## 您將學習
- 如何在指定資料夾中建立搜尋索引。  
- 從多個位置 **add documents to index** 的步驟。  
- 設定搜尋選項以啟用分塊搜尋。  
- 執行首次及後續的分塊搜尋。  
- 分塊文件搜尋發揮效益的實際案例。  

## 快速答覆
- **What is the first step?** 建立搜尋索引資料夾。  
- **How do I include many files?** 使用 `index.add()` 為每個文件資料夾加入。  
- **Which option enables chunk search?** `options.setChunkSearch(true)`。  
- **Can I continue searching after the first chunk?** 是的，使用 token 呼叫 `index.searchNext()`。  
- **Do I need a license?** 開發階段可使用免費試用或臨時授權；正式上線需購買正式授權。  

## 前置條件
為了跟隨本指南，請確保您已具備：

- **Required Libraries**: GroupDocs.Search for Java 25.4 或更新版本。  
- **Environment Setup**: 已安裝相容的 Java Development Kit (JDK)。  
- **Knowledge Prerequisites**: 基本的 Java 程式設計與 Maven 使用經驗。  

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

或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權
要試用 GroupDocs.Search：

- **Free Trial** – 無需承諾即可測試核心功能。  
- **Temporary License** – 為開發提供延長存取。  
- **Purchase** – 正式環境使用的完整授權。  

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
索引已建立後，接下來的合理步驟是從檔案所在位置 **add documents to index**。

### 1. 建立索引
**概述**：為搜尋索引設定目錄。

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

### 3. 設定分塊搜尋的搜尋選項
透過調整 options 物件以啟用分塊搜尋。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. 執行首次分塊搜尋
使用已啟用分塊的 options 執行首次查詢。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. 繼續分塊搜尋
持續遍歷剩餘的分塊，直至搜尋完成。

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 為什麼使用分塊搜尋？
分塊搜尋將龐大的文件集合切分為可管理的片段，降低記憶體壓力並加快回應速度。此方式在以下情境特別有益：

1. **Legal teams** 需要在數千份合約中快速定位特定條款。  
2. **Customer support portals** 必須即時顯示相關的知識庫文章。  
3. **Researchers** 在不載入整個檔案至記憶體的情況下，篩選龐大資料集。  

## 效能考量
- **Memory Management** – 為大型索引分配足夠的堆積空間 (`-Xmx`)。  
- **Resource Monitoring** – 於索引與搜尋過程中監控 CPU 使用率。  
- **Index Maintenance** – 定期重建或清理索引，以移除過時資料。  

## 常見問題與除錯
| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| `OutOfMemoryError` 於索引期間發生 | 堆積大小不足 | 增加 JVM 堆積 (`-Xmx2g` 或更高) |
| 未返回結果 | 分塊 token 未被處理 | 確保 `while` 迴圈執行至 `getNextChunkSearchToken()` 為 `null` 為止 |
| 搜尋效能緩慢 | 索引未最佳化 | 大量新增後執行 `index.optimize()` |

## 常見問答

**Q: What is chunk‑based searching?**  
A: 分塊搜尋將資料集切分為較小的片段，允許在不將整個文件載入記憶體的情況下，對大量資料進行高效查詢。

**Q: How do I update my index with new files?**  
A: 只需使用新文件的路徑呼叫 `index.add()`，索引會自動納入它們。

**Q: Can GroupDocs.Search handle different file formats?**  
A: 可以，支援 PDF、DOCX、XLSX、PPTX 以及其他多種常見格式。

**Q: What are typical performance bottlenecks?**  
A: 記憶體限制與未最佳化的索引是最常見的瓶頸；請分配足夠的堆積並定期最佳化索引。

**Q: Where can I find more detailed documentation?**  
A: 前往官方的 [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) 取得深入指南與 API 參考。

## 資源
- **文件說明**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API 參考**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **下載**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免費支援**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2025-12-19  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs