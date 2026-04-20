---
date: '2026-02-16'
description: 學習如何在 GroupDocs.Search 中使用 Java 布林運算子建立搜尋索引、執行內容搜尋與分面查詢，提升效能與使用者體驗。
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: 布林運算子 Java – 建立搜尋索引與分面搜尋
type: docs
url: /zh-hant/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean Operators Java – 建立搜尋索引與分面搜尋

Implementing a powerful **search experience** in Java can feel overwhelming, especially when you need to **create a search index Java** that supports **boolean operators Java** for faceted and complex queries. In this tutorial we’ll walk through setting up **GroupDocs.Search for Java**, building an index, adding documents, and crafting both simple faceted searches and sophisticated multi‑criteria queries that use Boolean logic. By the end you’ll understand how to leverage **content search Java**, **filename search Java**, and even **update index java** operations to keep your data fresh.

## Quick Answers
- **What is a faceted search?** 透過預先定義的類別（例如檔案類型或日期）來過濾結果的方式。  
- **How do I create a search index Java?** 初始化指向資料夾的 `Index` 物件並加入文件。  
- **Can I combine multiple criteria with boolean operators?** 可以 — 使用基於物件的查詢或在文字查詢中使用 Boolean 運算子。  
- **Do I need a license?** 免費試用版可用於開發；商業授權則移除限制。  
- **Which IDE works best?** 任意 Java IDE（IntelliJ IDEA、Eclipse、NetBeans）皆可順利使用。

## What is “create search index java”?
在 Java 中建立搜尋索引即是構建可搜尋的資料結構，儲存文件的中繼資料與內容，讓使用者查詢時能快速取得。使用 GroupDocs.Search 時，索引儲存在磁碟上，可增量更新，且支援諸如分面、**boolean operators Java** 以及複雜 Boolean 邏輯等進階功能。

## Why use GroupDocs.Search for faceted and complex queries?
- **Out‑of‑the‑box faceting** – 依檔名、大小或自訂中繼資料等欄位過濾。  
- **Rich query language** – 使用 AND/OR/NOT 運算子混合文字、片語與欄位查詢（即 **boolean operators java** 的核心）。  
- **Scalable performance** – 可索引數百萬文件，同時保持低延遲。  
- **Pure Java** – 無原生相依性，可在任何執行 JDK 8+ 的平台上運作。  
- **Easy index maintenance** – 在新增或刪除檔案後呼叫 `index.update()` 以 **update index java**。

## Prerequisites

- **JDK 8 或更新版本** 已安裝並在 IDE 中設定。  
- **Maven**（或 Gradle）用於相依性管理。  
- **GroupDocs.Search for Java** ≥ 25.4。  
- 具備 Java OOP 概念與 Maven 專案結構的基本認識。

## Setting Up GroupDocs.Search for Java

### Maven Setup
Add the repository and dependency to your `pom.xml` file:

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

### Direct Download
Alternatively, download the latest JAR from the official release page:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### License Acquisition
To unlock full functionality:

1. **Free trial** – 適合開發與測試的免費試用。  
2. **Temporary evaluation license** – 延長試用限制。  
3. **Commercial license** – 移除生產環境的所有限制。

### Basic Initialization and Setup
The following snippet shows how to **create a search index Java** by instantiating the `Index` class:

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

## How to use boolean operators java – Simple Faceted Search

Faceted search lets end‑users narrow results by selecting values from predefined categories (facets). Below is a step‑by‑step walk‑through.

### Step 1: Create an Index
First, point the `Index` to a folder where the index files will be stored.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Step 2: Add Documents to the Index
Tell GroupDocs.Search where your source documents live. All supported file types (PDF, DOCX, TXT, etc.) will be indexed automatically.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Step 3: Perform a Search in the Content Field with a Text Query
A quick text query filters by the `content` field. The syntax `content: Pellentesque` limits results to documents containing the word *Pellentesque* in their body text.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Step 4: Perform a Search Using an Object Query
Object‑based queries give you fine‑grained control. Here we build a word query, wrap it in a field query, and execute it.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## How to use boolean operators java – Complex Query Search

Complex queries combine multiple fields, Boolean operators, and phrase searches. This is ideal for scenarios like e‑commerce filters or legal document research.

### Step 1: Create an Index for Complex Queries
Reuse the same folder structure; you can share the index across both simple and complex scenarios.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Step 2: Perform a Search with a Text Query
The following query looks for files named *lorem* **and** *ipsum* **or** content containing either of two exact phrases.

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

### Step 3: Perform a Search with an Object Query
Object‑based construction mirrors the textual query but offers type safety and IDE assistance.

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

## Practical Applications of Faceted & Complex Searches

| 情境 | 分面如何協助 | 範例查詢 |
|----------|-------------------|---------------|
| **電商目錄** | 依類別、價格、品牌過濾 | `category: Electronics AND price:[100 TO 500]` |
| **法律文件庫** | 依案件編號、司法管轄區縮小範圍 | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **研究檔案庫** | 結合作者、出版年份與關鍵字 | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **企業內部網路** | 依檔案類型與部門搜尋 | `filetype: pdf AND department: HR` |

These examples illustrate why mastering **boolean operators java** and **filename search java** techniques is a game‑changer for any data‑intensive application.

## Common Pitfalls & Troubleshooting

- **Empty results** – 確認文件已成功加入（可使用 `index.getDocumentCount()` 來檢查）。  
- **Stale index** – 在新增或刪除檔案後，呼叫 `index.update()` 以 **update index java**，保持索引同步。  
- **Incorrect field names** – 使用 `CommonFieldNames` 常數（`Content`、`FileName` 等）避免拼寫錯誤。  
- **Performance bottlenecks** – 對於龐大集合，考慮啟用 `index.setCacheSize()` 或使用專用 SSD 作為索引資料夾。  
- **Missing highlights** – 若要 **highlight search results java**，可透過 `SearchResult.getFragments()` 取得匹配片段（此處未示範，但 API 中提供）。

## Frequently Asked Questions

**Q: 可以在 Spring Boot 中使用 GroupDocs.Search 嗎？**  
**A:** 當然可以。加入 Maven 相依性，將索引配置為 Spring Bean，並在需要搜尋功能的地方注入它。

**Q: 此函式庫支援自訂中繼資料欄位嗎？**  
**A:** 支援 — 你可以在索引時加入使用者自訂欄位，之後再以分面方式使用它們。

**Q: 索引可以長到多大？**  
**A:** 索引為磁碟基礎，可處理數百萬文件；只要確保足夠的儲存空間並監控快取設定即可。

**Q: 有沒有方法依相關性排序結果？**  
**A:** GroupDocs.Search 會自動為匹配項目打分；可透過 `SearchResult.getDocument(i).getScore()` 取得分數。

**Q: 若索引加密的 PDF 會發生什麼？**  
**A:** 在加入文件時提供密碼：`index.add(filePath, password)`。

## Conclusion

現在你應該已能熟練使用 GroupDocs.Search **create a search index Java**，加入文件，並打造簡單的分面查詢與使用 **boolean operators java** 的複雜布林搜尋。這些功能讓你能在各種應用中提供快速、精確且使用者友善的搜尋體驗，無論是電商平台還是企業知識庫。

準備好進一步了嗎？探索 **GroupDocs.Search** 的進階功能，如 **highlighting**、**suggestions** 與 **real‑time indexing**，進一步提升應用程式的搜尋效能。

---

**最後更新：** 2026-02-16  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs