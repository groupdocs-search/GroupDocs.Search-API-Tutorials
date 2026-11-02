---
date: '2026-11-02'
description: 了解如何在 Java 中使用 GroupDocs.Search 將資料夾加入索引、設定高壓縮，並執行快速全文查詢。
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: 了解如何在 Java 中使用 GroupDocs.Search 將資料夾加入索引、設定壓縮，並執行快速全文搜尋。適用於大型文件集。
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: 如何在 Java 中使用 GroupDocs.Search 將資料夾加入索引
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: 如何在 Java 中使用 GroupDocs.Search 將資料夾加入索引
type: docs
url: /zh-hant/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# 如何使用 GroupDocs.Search 在 Java 中將資料夾加入索引

如果您需要能夠擴展至數百萬文件的 **java full text search**，此處正是您所需要的。在本教學中，您將學習如何使用 GroupDocs.Search **add folder to index**，設定高壓縮儲存，並執行閃電般快速的查詢。完成後，您將擁有可直接嵌入任何 Java 專案的生產就緒解決方案。

## 快速解答
- **主要的程式庫是什麼？** GroupDocs.Search for Java  
- **如何將資料夾加入索引？** Use `index.add(folderPath)`  
- **我可以設定文字壓縮嗎？** Yes, via `TextStorageSettings(Compression.High)`  
- **需要哪個 Java 版本？** JDK 8 or higher  
- **在哪裡取得試用授權？** From the GroupDocs website or the repository page  

## 什麼是 java full text search 以及為何重要？
Java full text search 會將原始文件轉換為倒排索引，讓任何詞彙在數千個檔案中都能在毫秒內檢索。此功能對於法律資料庫、研究圖書館以及企業知識庫等使用者期望即時結果的情境至關重要。它亦能提升現代應用程式的生產力。

## 為何使用 groupdocs.search 進行 java full text search？
GroupDocs.Search 提供高吞吐量的索引與查詢執行，同時內建高壓縮功能。它支援 **50+ 種輸入與輸出格式**——包括 PDF、DOCX、EML 與 HTML，且能在不將整個檔案載入記憶體的情況下處理數百頁的文件，讓一般工作負載的記憶體佔用保持在 200 MB 以下。

## 前置條件
- **GroupDocs.Search for Java** (version 25.4 or later) – 提供索引與搜尋功能的核心程式庫。  
- **JDK 8+** 已安裝並設定 – SDK 所需的最低執行環境。  
- **Maven** 用於相依管理 – 簡化將程式庫加入專案的流程。  
- 如 **IntelliJ IDEA** 或 **Eclipse** 等 IDE – 用於編寫與除錯 Java 程式碼。  

## 設定 GroupDocs.Search for java
### Maven 設定
將儲存庫與相依項目加入您的 `pom.xml` 檔案：

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
或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

#### 取得授權
- **Free trial** – 無需承諾即可探索全部功能。  
- **Temporary license** – 延長測試期間。  
- **Purchase** – 解鎖完整的生產功能。  

### 基本初始化與設定
`Index` 是用於建立、開啟與管理搜尋索引的核心類別。

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## 使用自訂壓縮索引文字
### 步驟 1：定義索引資料夾
選擇一個用於存放索引檔案的目錄：

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### 步驟 2：設定索引參數
`TextStorageSettings` 設定文字在索引中的儲存方式，包括壓縮等級。`Compression` 為列舉型別，用以指定所需的壓縮演算法。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### 步驟 3：使用自訂設定建立索引
使用上述設定建立索引實例：

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## 如何將資料夾加入索引
`Index` 是代表可搜尋索引的主要類別。

載入現有索引（或建立新索引），然後對 `Index` 物件呼叫 `add` 方法。`add` 操作會掃描指定目錄，從每個支援的檔案中擷取文字，並將其儲存於壓縮索引中，隨時可供即時搜尋。

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## 如何搜尋已索引的文件
`SearchResult` 代表單一匹配項目，包含文件路徑與相關性。

定義要搜尋的查詢字串（代表您想定位的詞彙或片語），然後在 `Index` 實例上呼叫 `search` 方法。該方法會回傳 `SearchResult` 物件的集合，每個物件包含文件路徑、相關性分數與突顯匹配的摘要。

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## 實務應用
**java full text search** 發揮優勢的實務情境：
1. **Legal document management** – 即時取得案件檔案。  
2. **Academic research libraries** – 快速查找論文與學位論文。  
3. **Enterprise knowledge bases** – 快速存取手冊與常見問題。  
4. **Content management systems** – 為大型網站提供高效的內容發現。  
5. **Customer service archives** – 快速搜尋過往工單與聊天記錄。  

## 效能考量
- **Compression vs. speed**：高壓縮可節省高達 70 % 的磁碟空間，但會增加少量的索引開銷；請針對您的資料量執行效能測試。  
- **Memory management**：對於超過 10 GB 的索引，請配置至少 2 GB 的堆記憶體，以避免 `OutOfMemoryError`。  
- **Index updates**：使用 `index.add()` 逐步加入新文件，並定期呼叫 `index.optimize()` 以保持索引緊湊。  
- **Query optimization**：利用進階查詢語法（萬用字元、相近度、模糊搜尋）縮小結果範圍，降低回應時間。  

## 常見陷阱與專業提示
- **Pitfall:** 大量新增後忘記呼叫 `index.optimize()`。  
  **Pro tip:** 每晚執行 `index.optimize()` 以保持索引緊湊。  

- **Pitfall:** 在大規模資料集上使用預設（低）壓縮。  
  **Pro tip:** 在生產環境中切換至 `Compression.High` 以降低儲存成本。  

- **Pitfall:** 從網路共享加入檔案時未處理 `IOException`。  
  **Pro tip:** 將 `index.add()` 包裹於 try‑catch 區塊，並記錄任何失敗以供日後檢查。  

## 常見問答
**Q: GroupDocs.Search 是什麼？**  
A: 它是一個強大的 Java 程式庫，提供先進的全文搜尋功能，包括索引、壓縮與複雜查詢支援。

**Q: 如何使用 GroupDocs.Search 處理大型資料集？**  
A: 啟用高壓縮 (`Compression.High`) 並定期提交變更以保持索引精簡。同時，配置足夠的堆記憶體（例如，對於超過 20 GB 的索引，建議 4 GB）。

**Q: 我可以將 GroupDocs.Search 整合到現有的企業系統嗎？**  
A: 可以，該程式庫可嵌入任何基於 Java 的後端、REST 服務或微服務架構中。

**Q: 如果我的索引過時該怎麼辦？**  
A: 使用 `index.add()` 方法加入新檔案，使用 `index.delete()` 移除過時檔案，必要時重新執行 `index.optimize()`。

**Q: 我可以在哪裡取得協助或支援？**  
A: 前往 [GroupDocs forums](https://forum.groupdocs.com/c/search/10) 社群論壇，尋求除錯與最佳實踐建議。

## 其他資源
- 詳細使用指南： [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- 完整 API 參考： [API Reference Guide](https://reference.groupdocs.com/search/java)  
- 保持最新功能： [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**最後更新：** 2026-11-02  
**測試環境：** GroupDocs.Search 25.4  
**作者：** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## 相關教學
- [Groupdocs Search Java 建立索引指南](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [精通 Groupdocs Search Java 索引管理指南](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java 全文搜尋函式庫 – 使用 GroupDocs.Search 最佳化索引](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)