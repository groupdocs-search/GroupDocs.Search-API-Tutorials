---
date: '2026-08-26'
description: 了解 Boolean operators Java 如何協助您建立快速的搜尋索引、執行 content search Java，並使用 GroupDocs.Search
  進行分面查詢。
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: 了解 Boolean operators Java 如何協助您建立快速的搜尋索引、執行 content search Java，並使用
  GroupDocs.Search 執行分面查詢。
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – 建立搜尋索引與分面搜尋
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – 建立搜尋索引與分面搜尋
type: docs
url: /zh-hant/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean operators Java – 建立搜尋索引與分面搜尋

在 Java 中實作強大的 **search experience** 可能會讓人感到壓力，特別是當你需要 **create a search index Java** 並支援 **boolean operators Java** 以進行分面和複雜查詢時。在本教學中，我們將逐步說明如何設定 **GroupDocs.Search for Java**、建立索引、加入文件，並打造簡單的分面搜尋以及使用布林邏輯的複雜多條件查詢。最後，你將了解如何運用 **content search Java**、**filename search Java**，甚至 **update index Java** 操作來保持資料的即時性。

## 快速回答
- **什麼是分面搜尋？** 以預先定義的類別（如檔案類型或日期）過濾結果的方式。  
- **如何建立 search index Java？** 初始化指向資料夾的 `Index` 物件並加入文件。  
- **可以使用布林運算子結合多個條件嗎？** 可以——使用基於物件的查詢或文字查詢中的 Boolean 運算子。  
- **需要授權嗎？** 免費試用可用於開發；商業授權可移除限制。  
- **哪個 IDE 最適合？** 任意 Java IDE（IntelliJ IDEA、Eclipse、NetBeans）皆可。  

## 什麼是「create search index java」？

建立 search index Java 意指建構一個基於磁碟的結構，用來儲存文件文字與中繼資料，讓查詢能即時取得符合條件的文件。索引將詞彙映射至文件識別碼，支援快速查找，且可隨檔案變更逐步更新，為強大的搜尋功能奠定基礎。

## 為什麼使用 GroupDocs.Search 進行分面與複雜查詢？

GroupDocs.Search for Java 內建分面、布林查詢支援，以及高效能索引，能處理多達 1000 萬文件，同時在一般伺服器硬體上將查詢延遲維持在 200 ms 以下。它提供即時的欄位過濾、豐富的查詢語言，且純 Java 相容，適合企業級搜尋情境。

## 前置條件

在開始之前，請確保你已具備以下環境：

- **JDK 8 或更新版本** 已安裝並在 IDE 中設定。  
- **Maven**（或 Gradle）用於相依管理。  
- **GroupDocs.Search for Java** ≥ 25.4。  
- 基本的 Java OOP 概念與 Maven 專案結構認識。

## 設定 GroupDocs.Search for Java

### Maven 設定
將儲存庫與相依加入你的 `pom.xml` 檔案：

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
或者，從官方發行頁面下載最新 JAR：  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### 取得授權
解鎖完整功能：

1. **免費試用** – 適合開發與測試。  
2. **臨時評估授權** – 延長試用限制。  
3. **商業授權** – 移除所有生產環境限制。

### 基本初始化與設定
`Index` 類別是代表磁碟上可搜尋索引的核心元件。以下程式碼示範如何透過實例化 `Index` 類別 **create a search index Java**：

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

索引建立完成後，我們即可進入實務的分面與複雜查詢。

## 如何使用 boolean operators java – 簡易分面搜尋

載入索引、加入文件，並發送欄位查詢；兩步驟模式讓你在一次呼叫中取得分面計數與過濾結果。此方式為使用者提供直觀的方式，依檔案類型、作者或自訂中繼資料等類別縮小結果範圍。

### 步驟 1：建立索引
首先，將 `Index` 指向將儲存索引檔案的資料夾。

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### 步驟 2：將文件加入索引
告訴 GroupDocs.Search 你的來源文件所在位置。所有支援的檔案類型（PDF、DOCX、TXT 等）都會自動被索引。

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### 步驟 3：使用文字查詢在 content 欄位執行搜尋
簡易文字查詢會以 `content` 欄位過濾。語法 `content: Pellentesque` 會限制結果僅包含正文中出現 *Pellentesque* 的文件。

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### 步驟 4：使用物件查詢執行搜尋
基於物件的查詢提供更細緻的控制。我們在此建立字詞查詢，將其包裝於欄位查詢，然後執行。

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## 如何使用 boolean operators java – 複雜查詢搜尋

要執行複雜查詢，只需將多個欄位條件以 AND/OR/NOT 運算子結合，並可選擇加入片語搜尋。你可以使用欄位查詢指定每個條件，透過布林運算子巢狀組合，並以 boost 調整相關性，從而只取得符合所有必要條件的最相關文件。

### 步驟 1：為複雜查詢建立索引
重複使用相同的資料夾結構；索引可同時供簡易與複雜情境使用。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### 步驟 2：使用文字查詢執行搜尋
以下查詢尋找檔名為 *lorem* **且** *ipsum* **或** 內容包含任一精確片語的文件。

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

| 情境 | 分面如何協助 | 範例查詢 |
|----------|-------------------|---------------|
| **電商目錄** | 依類別、價格、品牌過濾 | `category: Electronics AND price:[100 TO 500]` |
| **法律文件庫** | 依案號、司法管轄區縮小範圍 | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **研究檔案庫** | 結合作者、出版年份、關鍵字 | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **企業內部網** | 依檔案類型與部門搜尋 | `filetype: pdf AND department: HR` |

這些範例說明了精通 **boolean operators java** 與 **filename search java** 技術，對任何資料密集型應用都是顛覆性的助力。

## 常見問題與除錯

`SearchResult` 物件包含符合查詢的文件，並提供相關分數與突顯片段的存取。  
`CommonFieldNames` 類別定義了 API 中常用的標準欄位名稱，如 `Content` 與 `FileName`。

- **結果為空** – 確認文件已成功加入（`index.getDocumentCount()` 可協助檢查）。  
- **索引過時** – 新增或移除文件後，呼叫 `index.update()` 以 **update index java** 並保持同步。  
- **欄位名稱錯誤** – 使用 `CommonFieldNames` 常數（`Content`、`FileName` 等）避免拼寫錯誤。  
- **效能瓶頸** – 面對龐大集合時，可考慮啟用 `index.setCacheSize()` 或使用專屬 SSD 作為索引資料夾。  
- **缺少突顯** – 若要 **highlight search results java**，可透過 `SearchResult.getFragments()` 取得匹配片段（此處未示範，但 API 中可用）。  

## 常見問答

**Q: 可以在 Spring Boot 中使用 GroupDocs.Search 嗎？**  
A: 當然可以。加入 Maven 相依，將索引配置為 Spring Bean，然後在需要搜尋功能的地方注入即可。

**Q: 函式庫支援自訂中繼資料欄位嗎？**  
A: 支援——在索引時加入使用者自訂欄位，之後即可在分面時使用。

**Q: 索引最大可以多大？**  
A: 基於磁碟的索引可處理多達 1000 萬文件；只要確保有足夠的儲存空間並監控快取設定即可。

**Q: 有方法依相關性排序結果嗎？**  
A: GroupDocs.Search 會自動為匹配項目計分；你可以透過 `SearchResult.getDocument(i).getScore()` 取得分數。

**Q: 若索引加密的 PDF 會怎樣？**  
A: 在加入文件時提供密碼：`index.add(filePath, password)`。

## 結論

現在你應該已熟悉如何使用 GroupDocs.Search **create a search index Java**、加入文件，並利用 **boolean operators java** 來構建簡易分面查詢與複雜布林搜尋。這些功能讓你能在各種應用中提供快速、精確且使用者友善的搜尋體驗——從電商平台到企業知識庫皆適用。

準備好進一步探索嗎？深入了解 **GroupDocs.Search** 的進階功能，如 **highlighting**、**suggestions** 與 **real‑time indexing**，進一步提升應用的搜尋效能。

---

**最後更新：** 2026-08-26  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs

## 相關教學

- [Wildcard Search Java with GroupDocs.Search – Advanced Features](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [How to Update Index Java with GroupDocs.Search – A Comprehensive Guide](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [How to implement java full text search: create index directory with GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)