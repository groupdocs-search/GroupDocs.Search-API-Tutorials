---
date: '2026-05-28'
description: 了解如何使用 GroupDocs.Search for Java 以通配符模式搜尋片語。內容包括建立搜尋索引、加入文件，以及執行精確片語和通配符查詢。
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: 如何在 GroupDocs.Search for Java 中使用通配符搜尋片語
type: docs
url: /zh-hant/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# 如何在 GroupDocs.Search for Java 中使用通配符搜尋片語

在現代以文件為中心的應用程式中，快速且精確地 **how to search phrase** 是影響使用者體驗的關鍵因素。無論您是建立知識庫、電子商務目錄，或是合規性驅動的資料庫，能夠定位精確的片語—或其彈性變體—都能提升使用者生產力並減少支援負擔。本教學將帶您安裝 **GroupDocs.Search for Java**、建立搜尋索引、載入文件，並執行精確片語與通配符增強查詢，全部提供清晰、可投入生產環境的程式碼範例。

## 快速解答
- **What is the primary benefit of phrase searches?** 精確匹配詞序與接近度，確保僅返回包含完整序列的文件。  
- **Can wildcards be used inside a phrase?** 是的—通配符允許您跳過或取代詞彙，同時保留整體順序。  
- **Do I need a license for development?** 免費試用可用於測試；正式部署需購買完整授權。  
- **Which Maven version should I use?** 使用最新的 GroupDocs.Search for Java 版本（例如撰寫時的 25.4）。  
- **Is this approach suitable for large document sets?** 絕對可以—GroupDocs.Search 能在索引最佳化後，處理數十萬文件的集合，且查詢延遲維持在秒以下。  

## 什麼是 “how to search phrase”？
**搜尋片語是指在文件中尋找特定的詞序。**  
當您執行片語查詢時，搜尋引擎會檢查詞彙是否以精確的順序且在定義的接近範圍內出現，從而排除在不同語境中出現相同詞彙的無關結果。這使得片語搜尋非常適合定位法律條款、產品代碼或任何順序重要的文字。

## 為何在片語與通配符查詢中使用 GroupDocs.Search？
GroupDocs.Search 提供 **在一般伺服器硬體上，對多達 100 萬文件進行高吞吐量索引，同時保持子秒級查詢回應時間**。其查詢語言支援精確片語、簡單的 `*` 與 `?` 通配符，以及如數值範圍 (`*2~5`) 的進階模式。此函式庫可透過 Maven 或直接下載 JAR 與任何 Java 應用程式整合，且在 Java 8+ 環境下執行，無需外部服務。

## 前置條件
- Java 8 或更新版本（建議使用 Java 11 LTS）。  
- Maven 3 或以上（若您偏好相依管理）。  
- 基本了解 Java 專案結構與物件導向概念。  

## 設定 GroupDocs.Search for Java

### 使用 Maven
在 `pom.xml` 中加入官方儲存庫與 GroupDocs.Search 相依性：

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### 直接下載
或者，從官方發行頁面下載最新的 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權
- **Free Trial:** 適合快速實驗；索引資料上限為 100 MB。  
- **Temporary License:** 從 GroupDocs 入口網站申請 30 天評估金鑰。  
- **Full License:** 正式使用及無限制索引容量時必須購買。  

## 基本初始化與設定
建立一個用於存放索引檔案的資料夾，並實例化 `Index` 物件。`Index` 類別代表儲存在磁碟上的可搜尋索引，提供新增、更新與查詢文件的方法。

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

加入您想要搜尋的文件：

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## 如何在 GroupDocs.Search 中使用通配符搜尋片語
本節示範三種片語搜尋層級——精確匹配、簡單通配符與進階通配符模式——說明如何建立索引、加入文件，並以簡潔的 Java 程式碼執行各種查詢。範例同時展示文字型查詢與物件型查詢的建構方式，讓開發者能將彈性搜尋功能整合至應用程式中。

### 簡易片語搜尋

#### 概述
當您需要 **精確匹配** 詞序時（例如法律條款或產品型號），可使用此方法。

#### 直接答案
載入索引，使用帶引號的片語呼叫 `search`（例如 `"quick brown fox"`），引擎僅返回包含該精確序列的文件，保留詞序與間距。即使在包含數十萬檔案的索引上，查詢也能在毫秒內完成。

#### 步驟 1：建立索引
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### 步驟 2：將文件加入索引
```java
Index index = new Index(indexFolder);
```

#### 步驟 3：搜尋特定片語（文字形式）
```java
index.add(documentsFolder);
```

#### 步驟 4：物件型查詢（搜尋精確片語）
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### 使用通配符的片語搜尋

#### 概述
通配符佔位符（`*` 代表任意數量字元，`?` 代表單一字元）讓您 **跳過可變詞彙**，同時仍保留前後的順序。

#### 直接答案
在帶引號的片語中插入通配符 (`*`)——例如 `"quick * fox"`——即可匹配 *quick* 與 *fox* 之間的任意詞彙。引擎於查詢時展開通配符，只掃描符合模式的索引詞彙，效能與純片語查詢相當。

#### 步驟 1：建立索引
*(同簡易片語搜尋。)*

#### 步驟 2：將文件加入索引
*(同上。)*

#### 步驟 3：文字形式搜尋通配符
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### 步驟 4：物件型查詢使用通配符（Wildcard Search Java）
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### 進階通配符搜尋

#### 概述
結合數值範圍、可選字元與自訂類正規表達式的模式，以實現 **複雜匹配**，例如版本號或產品代碼。

#### 直接答案
使用擴充的通配符語法 `*min~max` 定義允許的詞距範圍，或使用 `?` 匹配單一字元。例如，`"error *2~5 code"` 會找到 *error* 後接任意兩到五個詞，再接 *code*。此精確度可降低誤報，同時保有彈性。

#### 步驟 1：建立索引
*(為清晰起見重複。)*

#### 步驟 2：將文件加入索引
*(重複。)*

#### 步驟 3：文字形式搜尋複雜通配符模式
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### 步驟 4：物件型查詢使用進階通配符
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## 實務應用
- **Content Management Systems:** 編輯者可快速定位精確條款或彈性摘錄，無需手動掃描數百頁。  
- **E‑commerce Catalogs:** 消費者即使省略描述詞或使用同義詞，也能透過通配符容錯找到商品。  
- **Legal & Compliance:** 快速分離在合約中可能出現微小變化的條款文字。  

## 效能考量
- **Create Search Index** 僅在穩定的文件集合上建立一次；所有查詢皆重用同一個 `Index` 實例。  
- **Add Documents Incrementally** 當有新檔案時增量加入—避免重新建構整個索引以降低 CPU 使用率。  
- **Design Precise Wildcard Patterns**；較寬鬆的模式（`*`）會增加詞彙展開次數，可能提升 CPU 負載。  
- **Call `index.optimize()`** 定期（若支援）壓縮索引，控制記憶體使用。  

## 常見問題與解決方案
| 問題 | 解決方案 |
|-------|----------|
| 通配符查詢未返回結果 | 確認通配符語法 (`*min~max`) 並確保目標詞彙在定義的距離內存在。 |
| 檔案更新後索引變舊 | 使用 `index.add(updatedFolder)` 或增量更新 API 只刷新已變更的檔案。 |
| 大型資料集記憶體消耗過高 | 增加 JVM 堆積大小（`-Xmx4g` 或更高），並考慮將索引分割為多個分片以平行處理。 |

## 常見問答

**Q: 通配符與片語搜尋有何不同？**  
A: 片語搜尋要求精確的詞序與間距，而通配符允許在保持順序的前提下取代或跳過詞彙，提供彈性匹配。

**Q: 可以在搜尋中對數值資料使用通配符嗎？**  
A: 可以—通配符範圍參數（`*min~max`）同樣適用於數字與詞彙，支援如 `"version *1~3"` 的查詢。

**Q: 如何處理極大型的文件集合？**  
A: 保持索引最佳化，執行增量更新，並設計具體的通配符模式以限制詞彙展開。GroupDocs.Search 能在標準硬體上索引 100 萬文件，且查詢延遲維持在 200 ms 以下。

**Q: GroupDocs.Search 適用於即時搜尋情境嗎？**  
A: 絕對適用—索引建好後，查詢在毫秒內完成，非常適合互動式搜尋框與自動完成功能。

**Q: 我可以將此函式庫整合到現有的 Java 專案嗎？**  
A: 可以。加入 Maven 相依或 JAR，如示範般實例化 `Index`，即可開始查詢，無需修改既有程式碼。

**最後更新:** 2026-05-28  
**測試環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## 相關教學

- [建立搜尋索引 Java – GroupDocs.Search 教學](/search/java/)
- [將文件加入索引 – GroupDocs.Search Java 教學](/search/java/document-management/)
- [建立搜尋索引 - GroupDocs.Search Java 教學](/search/java/advanced-features/)