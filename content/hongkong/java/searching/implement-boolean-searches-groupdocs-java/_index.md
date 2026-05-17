---
date: '2026-01-29'
description: 學習如何使用 GroupDocs.Search for Java 實作 Java 布林 AND/OR 查詢、將文件加入索引並提升文件檢索效果。
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: Java 布林 AND OR：精通使用 GroupDocs.Search for Java 進行布林搜尋
type: docs
url: /zh-hant/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or：使用 GroupDocs.Search for Java 掌握布林搜尋

在龐大的文件集合中搜尋，常常像大海撈針。透過 **java boolean and or** 查詢，你可以精確告訴搜尋引擎你的需求——取得同時包含 *兩個* 關鍵字的文件、包含 *任一* 關鍵字的文件，或是排除不想要的詞彙。本文將示範如何設定 **GroupDocs.Search for Java**、將文件加入索引，並撰寫強大的布林查詢，提升 **document retrieval java** 工作流程。

## 快速解答
- **什麼是布林 AND 查詢？** 只回傳同時包含 *所有* 指定詞彙的文件。  
- **OR 與 AND 有何不同？** OR 會匹配包含 *任一* 詞彙的文件，擴大結果集。  
- **什麼時候使用 NOT？** 使用 NOT 可過濾掉包含不想要詞彙的文件。  
- **需要授權嗎？** 免費試用可用於測試；正式上線需購買商業授權。  
- **需要哪個 Java 版本？** 支援 Java 8 以上；建議使用 JDK 11 以上。

## 什麼是 **java boolean and or**？
**java boolean and or** 查詢結合了邏輯運算子（AND、OR、NOT），用以細化搜尋結果。透過組合查詢，你可以告訴 GroupDocs.Search 各詞彙之間的關係，從而精確控制檢索過程。

## 為什麼選擇 GroupDocs.Search for Java？
- **高效能**，適用於大型文件集合。  
- **豐富的 API**，同時支援文字型與物件型查詢。  
- **內建語言支援**，包括詞幹分析、停用詞與模糊匹配。  
- **易於整合**，支援 Maven 或直接下載 JAR。

## 前置條件
在開始之前，請確保你已具備：

- **GroupDocs.Search for Java**（v25.4 或更新）——請參考下方下載連結。  
- 已安裝並在 IDE（IntelliJ IDEA、Eclipse 等）中設定好 JDK 8+。  
- 基本的 Java 知識與 Maven 依賴管理能力。  

## 設定 GroupDocs.Search for Java

### Maven 設定
在 `pom.xml` 中加入倉庫與相依性：

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
或是從官方網站下載最新 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權
先使用免費試用授權探索所有功能。正式上線時，請購買商業授權以解鎖完整功能。

### 基本初始化與設定
建立索引資料夾並實例化 `Index` 物件：

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or：實作布林搜尋

以下說明 **AND**、**OR**、**NOT** 與 **複合** 查詢。每個章節同時提供純文字查詢與等價的物件查詢，讓你依需求選擇最合適的寫法。

### 布林 AND 搜尋
使用 **AND** 結合關鍵字，僅取得同時包含 *所有* 關鍵字的文件。

#### 概述
AND 查詢會縮小結果範圍，當需要同時符合多項條件時，可提升相關性。

#### 實作步驟

1. **初始化 Index** – 同時示範 **add documents to index** 的 AND 情境。

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **加入文件至索引**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **執行文字查詢** – 使用純字串語法。

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **執行物件查詢** – 於程式碼中動態建構查詢時相當有用（**search with and java**）。

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### 布林 OR 搜尋
使用 **OR** 擴大結果，匹配任一提供的關鍵字。

#### 概述
OR 查詢適合探索性搜尋，能捕捉包含至少一個關鍵字的文件（**search with or java**）。

#### 實作步驟

1. **初始化 Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **加入文件至索引**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **執行文字查詢**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **執行物件查詢**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### 布林 NOT 搜尋
使用 **NOT** 排除不想要的詞彙，過濾掉噪音。

#### 概述
NOT 查詢可剔除不相關文件，例如過濾掉競爭對手的品牌名稱（**boolean search examples java**）。

#### 實作步驟

1. **初始化 Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **加入文件至索引**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **執行文字查詢**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **執行物件查詢**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### 複合布林查詢
結合 **AND**、**OR** 與 **NOT**，打造高度客製化的搜尋邏輯，以滿足極為特定的檢索需求。

#### 概述
複合查詢能模擬真實情境，例如「找出正面評價的運動文章，但排除任何提及特定運動員的內容」。

#### 實作步驟

1. **初始化 Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **加入文件至索引**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **執行文字查詢**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **執行物件查詢**

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

## java boolean and or 查詢的實務應用
- **文件管理系統** – 找出同時包含「confidential」**AND**「renewal」的合約。  
- **法律研究** – 使用 **AND**/**OR** 篩選案例，同時以 **NOT** 排除過時法條。  
- **客服支援** – 取得同時提及「login」**AND**「error」但不含「resolved」的工單。  
- **內容策展** – 蒐集關於「cloud」**OR**「serverless」的部落格文章，用於電子報。

## 常見問題與除錯
- **忘記更新索引** – 新增文件後，請呼叫 `index.update()` 以確保可被搜尋。  
- **運算子間距錯誤** – GroupDocs.Search 需要在運算子前後保留空格（`AND`、`OR`、`NOT`）。  
- **大小寫敏感** – 預設不區分大小寫，但自訂分析器可能會影響此行為。  
- **結果過大** – 使用分頁 (`search(query, 0, 100)`) 以避免記憶體過載。

## 常見問答

**Q: 可以在 AND 查詢中結合超過兩個詞彙嗎？**  
A: 當然可以。你可以使用多個 `createWordQuery` 物件搭配 `createAndQuery`，或直接在文字查詢中寫 `"term1 AND term2 AND term3"`。

**Q: GroupDocs.Search 支援通配符或模糊搜尋嗎？**  
A: 支援。使用 `*` 作為通配符（例如 `promot*`），或使用 `~` 進行模糊匹配（例如 `comfort~`）。

**Q: 如何限制搜尋僅針對特定檔案類型？**  
A: 使用 `FileTypeQuery` 類別限制結果為 PDF、DOCX 等，並與布林查詢結合。

**Q: 監控索引效能的最佳方式是什麼？**  
A: 開啟內建日誌 (`index.getLogger().setLevel(Level.INFO)`) 並在每次 `add` 操作後檢視時間指標。

**Q: 有辦法提升特定詞彙的相關性嗎？**  
A: 可以。將重要詞彙包裹在 `BoostQuery` 中，以提升其在排序演算法中的權重。

---

**最後更新：** 2026-01-29  
**測試環境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs