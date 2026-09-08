---
date: '2026-07-21'
description: 本教學說明如何使用 GroupDocs.Search for Java 實作 boolean AND、OR、NOT 搜尋、將文件加入 index，並
  boost 文件檢索。
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: 本教學逐步說明如何使用 GroupDocs.Search for Java 建立 AND、OR、NOT 查詢、將文件加入 index，並提升檢索效能。
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: 建立 Boolean Query Java – 掌握 GroupDocs.Search 的 Boolean 搜尋
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 建立 Boolean Query Java：掌握 GroupDocs.Search for Java 的 Boolean 搜尋
type: docs
url: /zh-hant/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# 建立布林查詢 Java：使用 GroupDocs.Search for Java 精通布林搜尋

搜尋大量文件集合可能會像在大海撈針般困難。**Create Boolean Query Java** 讓您精確告訴引擎您的需求——文件必須同時包含 *both* 詞彙、*either* 詞彙，或 *exclude* 不想要的詞語。在本指南中，我們將逐步說明如何設定 **GroupDocs.Search for Java**、將文件加入索引，以及打造強大的布林查詢，以提升您的 **document retrieval java** 工作流程。完成後，您將能夠僅用幾行程式碼撰寫乾淨且易於維護的 Java 布林查詢程式碼。

## 快速解答
- **什麼是 boolean AND 查詢？** 僅返回包含 *all*（全部）指定詞彙的文件。  
- **OR 與 AND 有何不同？** OR 會匹配包含 *any*（任意）詞彙的文件，擴大結果集。  
- **何時應使用 NOT？** 使用 NOT 可過濾掉包含不想要詞語的文件。  
- **我需要授權嗎？** 免費試用版可用於測試；正式環境需購買商業授權。  
- **需要哪個 Java 版本？** 支援 Java 8 以上；建議使用 JDK 11 以上。

## 什麼是 **create boolean query java**？
`create boolean query java` 指在 Java 中構建結合 AND、OR、NOT 等邏輯運算子的搜尋查詢，使用 GroupDocs.Search API。透過組合這些運算子，您可以精確控制匹配的文件，實現進階篩選、相關性調整與複雜搜尋情境。

## 為何使用 GroupDocs.Search for Java？
- **High performance** 在大型文件集合上表現卓越——在標準伺服器上可於一分鐘內索引與搜尋 500 GB 文字。  
- **Rich API** 支援文字型與物件型查詢，讓您選擇最符合架構的方式。  
- **Built‑in language support** 提供 30 多種語言的詞幹、停用詞與模糊匹配支援。  
- **Easy integration** 可透過 Maven 或直接下載 JAR 整合，僅需幾行程式碼即可開始使用。

## 先決條件
在深入之前，請確保您已具備：

- **GroupDocs.Search for Java** (v25.4 或更新版本) – 請參閱以下下載連結。  
- 已安裝 JDK 8+，並在 IDE（IntelliJ IDEA、Eclipse 等）中設定。  
- 基本的 Java 知識與 Maven 依賴管理。  

## 設定 GroupDocs.Search for Java

### Maven 設定
Add the repository and dependency to your `pom.xml`:

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
或者，從官方網站下載最新的 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權
先使用免費試用授權以探索全部功能。正式環境則需購買商業授權以解鎖完整功能。

### 基本初始化與設定
Create an index folder and instantiate the `Index` object:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## 如何建立 boolean query java？
`Index` 類別代表儲存在磁碟上的可搜尋文件集合。`BooleanQuery` 結合多個子查詢與邏輯運算子。`createAndQuery`、`createOrQuery` 與 `createNotQuery` 分別構造 AND、OR、NOT 子查詢。載入或建立 `Index` 實例、加入文件，然後使用 `createAndQuery`、`createOrQuery` 或 `createNotQuery` 建立 `BooleanQuery` 物件。呼叫 `index.search(query)` 以取得匹配的文件。此模式適用於簡單與複雜情境，只需三個邏輯步驟：索引初始化、文件加入與查詢執行。

## 布林 AND 搜尋

### 概述
AND 查詢會縮小結果範圍，當您需要符合多項條件的文件時，可提升相關性。

### 實作步驟

1. **Initialize Index** – 這同時示範 **add documents to index** 在 AND 情境下的使用。

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – 使用純文字字串語法。

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – 在程式化建構查詢時很有用（**search with and java**）。

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## 布林 OR 搜尋

### 概述
OR 查詢適用於探索性搜尋，當您想捕捉包含多個關鍵字中任意一個的文件時（**search with or java**）。

### 實作步驟

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## 布林 NOT 搜尋

### 概述
NOT 查詢可協助您剔除不相關的文件，例如過濾掉競爭對手的品牌名稱（**boolean search examples java**）。

### 實作步驟

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## 複雜布林查詢

### 概述
複雜查詢讓您模擬真實的搜尋情境，例如「找出正面報導的運動文章，但排除任何提及特定運動員的內容」。

### 實作步驟

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## **java boolean and or** 查詢的實務應用
- **Document Management Systems** – 找出同時包含「confidential」 **AND** 「renewal」的合約。  
- **Legal Research** – 使用 **AND** / **OR** 篩選案例法，並利用 **NOT** 排除過時法規。  
- **Customer Support** – 取得同時提及「login」 **AND** 「error」但不含「resolved」的工單。  
- **Content Curation** – 收集關於「cloud」 **OR** 「serverless」的部落格文章，以供電子報使用。

## 常見陷阱與疑難排解
- **Missing Index Refresh** – 新增文件後，呼叫 `index.update()` 以確保可搜尋。  
- **Incorrect Operator Spacing** – GroupDocs.Search 需要在運算子前後保留空格（`AND`、`OR`、`NOT`）。  
- **Case Sensitivity** – 查詢預設不區分大小寫，但自訂分析器可能會影響此行為。  
- **Large Result Sets** – 使用分頁（`search(query, 0, 100)`）以避免記憶體過載。  

## 常見問答

**Q: 可以在 AND 查詢中結合超過兩個詞彙嗎？**  
A: 當然可以。您可以使用 `createAndQuery` 連接多個 `createWordQuery` 物件，或直接在文字查詢中寫入 `"term1 AND term2 AND term3"`。

**Q: GroupDocs.Search 支援萬用字元或模糊搜尋嗎？**  
A: 支援。使用 `*` 作為萬用字元（例如 `promot*`），或使用 `~` 進行模糊匹配（例如 `comfort~`）。

**Q: 如何限制搜尋特定檔案類型？**  
`FileTypeQuery` 限制搜尋結果僅包含特定檔案格式，如 PDF 或 DOCX。  
A: 使用 `FileTypeQuery` 類別將結果限制為 PDF、DOCX 等，並與您的布林查詢結合使用。

**Q: 監控索引效能的最佳方法是什麼？**  
A: 啟用內建記錄器（`index.getLogger().setLevel(Level.INFO)`），並在每次 `add` 操作後檢視時間指標。

**Q: 有沒有方法提升特定詞彙的相關性？**  
`BoostQuery` 提升搜尋查詢中指定詞彙的相關性分數。  
A: 有。將重要詞彙包裹在 `BoostQuery` 中，以提升其在計分演算法中的權重。

---

**最後更新：** 2026-07-21  
**測試環境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs

## 相關教學

- [Boolean Operators Java – 建立搜尋索引與分面搜尋](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java：高效文件搜尋與索引管理](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - 精通 GroupDocs.Search Java – 建立與管理搜尋索引](/search/java/indexing/groupdocs-search-java-create-index-guide/)