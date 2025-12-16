---
date: '2025-12-16'
description: 學習如何在 Java 中使用 GroupDocs.Search 建立搜尋索引，並實作分面與複雜搜尋，提升搜尋效能與使用者體驗。
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: 建立搜尋索引（Java）– 分面與複雜搜尋
type: docs
url: /zh-hant/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# 建立 Java 搜尋索引 – 分面與複雜搜尋

在 Java 中實作強大的 **search experience** 可能會讓人感到壓力，尤其是當您需要 **create search index Java** 專案來處理大量文件集合時。幸運的是，**GroupDocs.Search for Java** 提供了功能豐富的 API，讓您只需幾行程式碼即可建立分面與複雜查詢。在本教學中，您將學會如何設定函式庫、**create a search index Java**、加入文件，並執行簡單的分面搜尋與高階的多條件查詢。

## 快速解答
- **What is a faceted search?** 透過預先定義的類別（例如檔案類型、日期）來篩選結果的方式。  
- **How do I create a search index Java?** 初始化指向資料夾的 `Index` 物件並加入文件。  
- **Can I combine multiple criteria?** 可以——在文字查詢中使用基於物件的查詢或布林運算子。  
- **Do I need a license?** 免費試用版可用於開發；商業授權則移除所有限制。  
- **Which IDE works best?** 任何 Java IDE（IntelliJ IDEA、Eclipse、NetBeans）皆可順利使用。

## 什麼是 “create search index java”？
在 Java 中建立搜尋索引即是建構一個可搜尋的資料結構，用以儲存文件的中繼資料與內容，從而能根據使用者查詢快速取得結果。使用 GroupDocs.Search 時，索引會存放於磁碟上，可增量更新，並支援如分面與複雜布林邏輯等進階功能。

## 為何使用 GroupDocs.Search 進行分面與複雜查詢？
- **Out‑of‑the‑box faceting** – 依檔名、大小或自訂中繼資料等欄位進行篩選。  
- **Rich query language** – 使用 AND/OR/NOT 運算子混合文字、片語與欄位查詢。  
- **Scalable performance** – 能索引數百萬文件，同時保持低搜尋延遲。  
- **Pure Java** – 無原生相依性，可在任何執行 JDK 8+ 的平台上運作。

## 先決條件

在開始之前，請確保您具備以下條件：

- **JDK 8 或更新版本** 已安裝並在您的 IDE 中設定。  
- **Maven**（或 Gradle）用於相依性管理。  
- **GroupDocs.Search for Java** ≥ 25.4。  
- 具備 Java 物件導向概念與 Maven 專案結構的基本認識。

## 設定 GroupDocs.Search for Java

### Maven 設定
將儲存庫與相依性加入您的 `pom.xml` 檔案：

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
或者，從官方發行頁面下載最新的 JAR：  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### 取得授權
解鎖全部功能：

1. **Free trial** – 適合開發與測試的免費試用版。  
2. **Temporary evaluation license** – 延長試用限制的臨時評估授權。  
3. **Commercial license** – 移除生產環境使用的所有限制。

### 基本初始化與設定
以下程式碼示範如何透過實例化 `Index` 類別 **create a search index Java**：

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

索引建立完成後，我們即可進入實務上的分面與複雜查詢。

## 如何建立搜尋索引 Java – 簡易分面搜尋

分面搜尋讓最終使用者透過選取預先定義的類別（facet）值來縮小結果範圍。以下為逐步說明。

### 步驟 1：建立索引
首先，將 `Index` 指向用於儲存索引檔案的資料夾。

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### 步驟 2：將文件加入索引
告訴 GroupDocs.Search 您的來源文件所在位置。所有支援的檔案類型（PDF、DOCX、TXT 等）都會自動被索引。

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### 步驟 3：使用文字查詢在 Content 欄位執行搜尋
快速的文字查詢會依 `content` 欄位過濾。語法 `content: Pellentesque` 會將結果限制為正文中包含 *Pellentesque* 一詞的文件。

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### 步驟 4：使用物件查詢執行搜尋
基於物件的查詢提供更細緻的控制。此處我們建立一個字詞查詢，將其包裝於欄位查詢中，然後執行。

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## 如何建立搜尋索引 Java – 複雜查詢搜尋

複雜查詢結合多個欄位、布林運算子與片語搜尋。這在電商過濾或法律文件研究等情境中非常適用。

### 步驟 1：為複雜查詢建立索引
重複使用相同的資料夾結構；您可以在簡易與複雜情境間共用同一索引。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### 步驟 2：使用文字查詢執行搜尋
以下查詢尋找檔名為 *lorem* **且** *ipsum* **或** 內容包含兩個精確片語之一的檔案。

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### 步驟 3：使用物件查詢執行搜尋
基於物件的建構方式與文字查詢相同，但提供型別安全與 IDE 輔助。

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## 分面與複雜搜尋的實務應用

| Scenario | How Faceting Helps | Example Query |
|----------|-------------------|---------------|
| **電商目錄** | 依類別、價格、品牌篩選 | `category: Electronics AND price:[100 TO 500]` |
| **法律文件庫** | 依案件編號、司法管轄區縮小範圍 | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **研究檔案庫** | 結合作者、出版年份、關鍵字 | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **企業內部網路** | 依檔案類型與部門搜尋 | `filetype: pdf AND department: HR` |

這些範例說明了為何精通 **create search index java** 技術對任何資料密集型應用都是顛覆性的。

## 常見陷阱與除錯

- **Empty results** – 確認文件已成功加入（可使用 `index.getDocumentCount()` 來協助檢查）。  
- **Stale index** – 在新增或移除檔案後，呼叫 `index.update()` 以保持索引同步。  
- **Incorrect field names** – 使用 `CommonFieldNames` 常數（`Content`、`FileName` 等）以避免拼寫錯誤。  
- **Performance bottlenecks** – 對於龐大集合，考慮啟用 `index.setCacheSize()` 或使用專用 SSD 作為索引資料夾。

## 常見問答

**Q: 我可以在 Spring Boot 中使用 GroupDocs.Search 嗎？**  
A: 當然可以。只需加入 Maven 相依性，將索引配置為 Spring Bean，然後在需要的地方注入即可。

**Q: 此函式庫支援自訂中繼資料欄位嗎？**  
A: 支援——您可以在索引時加入使用者自訂欄位，之後再對其進行分面。

**Q: 索引可以長到多大？**  
A: 索引為磁碟基礎，可處理數百萬文件；只需確保有足夠的儲存空間並監控快取設定。

**Q: 有沒有方式依相關性排序結果？**  
A: GroupDocs.Search 會自動為匹配項目打分；您可以透過 `SearchResult.getDocument(i).getScore()` 取得分數。

**Q: 若索引加密的 PDF 會發生什麼情況？**  
A: 在加入文件時提供密碼：`index.add(filePath, password)`。

## 結論

現在您應該已能熟練使用 GroupDocs.Search **create a search index Java**，加入文件，並編寫簡單的分面查詢與複雜的布林搜尋。這些功能讓您能在各種應用中提供快速、精確且使用者友善的搜尋體驗，從電商平台到企業知識庫皆是如此。

準備好下一步了嗎？探索 **GroupDocs.Search** 的進階功能，如 **highlighting**、**suggestions** 與 **real‑time indexing**，進一步提升應用程式的搜尋效能。

---

**最後更新：** 2025-12-16  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs