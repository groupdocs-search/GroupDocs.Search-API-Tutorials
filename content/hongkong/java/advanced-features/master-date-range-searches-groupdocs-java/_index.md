---
date: '2025-12-18'
description: 學習如何使用 GroupDocs.Search 在 Java 中實作自訂日期格式搜尋，包括日期範圍查詢、自訂模式以及效能技巧。
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 自訂日期格式 Java：使用 GroupDocs 進行日期範圍搜尋
type: docs
url: /zh-hant/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# 自訂日期格式 Java：使用 GroupDocs 的日期範圍搜尋

依日期搜尋文件是常見需求——無論您是在建構檔案保存系統、財務報表工具，或是內容管理平台。在本教學中，您將學習使用 GroupDocs.Search 的 **custom date format java** 技術，涵蓋日期範圍查詢、自訂模式定義，以及 **optimize search performance** 的技巧。完成後，您即可讓使用者取得落在任何日期區間的記錄，無論其使用的格式為何。

## 快速解答
- **索引的主要類別是什麼？** `Index` from the `com.groupdocs.search` package.  
- **如何定義自訂日期模式？** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **可以使用文字查詢嗎？** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **需要哪些 Maven 坐標？** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **開發需要授權嗎？** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## 什麼是 **custom date format java**？
A **custom date format java** 告訴 GroupDocs.Search 如何解讀不符合預設 ISO 格式 (YYYY‑MM‑DD) 的日期字串。透過定義您自己的模式——例如 `MM/dd/yyyy` 或 `dd‑MM‑yyyy`——即可讓引擎辨識文件中使用區域或舊版格式的日期。

## 為何使用 GroupDocs.Search 進行日期範圍查詢？
- **速度：** Built‑in indexing makes look‑ups O(log n).  
- **彈性：** Supports both text‑based and object‑based query creation.  
- **多格式支援：** Handles PDFs, Word, Excel, plain text, and more without extra code。  

## 如何使用 GroupDocs.Search **search documents by date**
以下您將看到一步一步的指南，說明如何設定函式庫、建立索引檔案，以及執行簡易與進階的日期範圍搜尋。

### 前置條件
- 安裝 Java 8 或更新版本。  
- 使用 Maven 進行相依管理。  
- 取得 GroupDocs.Search 授權（試用或臨時授權可用於開發）。  

### 設定 GroupDocs.Search for Java

#### 透過 Maven 安裝
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

#### 直接下載
或者，您也可以直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

#### 基本初始化與設定
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## 功能 1：建立日期範圍搜尋查詢

### 使用文字形式查詢
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**說明**：`daterange` 語法需要 `YYYY‑MM‑DD` 格式的日期。它會回傳所有索引日期落在該區間的文件。

### 使用查詢物件
For programmatic control and custom parsing, build a `SearchQuery` object:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**說明**：`createDateRangeQuery` 允許您提供 `java.util.Date` 物件，讓您在時區與特定語系處理上擁有完整彈性。

## 功能 2：指定 **custom date format java** 模式

### 設定自訂日期格式
Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**說明**：透過清除預設格式並加入使用 `/` 作為分隔符的 `DateFormat`，引擎即可辨識寫成 `MM/dd/yyyy` 的日期。這對於在偏好月在前的地區執行 **search documents by date** 極為重要。

## 提升 **optimize search performance** 的技巧
- **Index Incrementally**：將新檔案加入現有索引，而非重新建構。  
- **Prune Stale Data**：定期移除不再需要的文件。  
- **Adjust Memory Settings**：在處理大型索引時，提升 JVM 記憶體堆疊 (`-Xmx`)。  

## 常見問題與解決方案
- **Date Parsing Errors**：確認文件中的日期字串完全符合您所定義的自訂模式。  
- **Missing Results**：確保索引欄位包含日期中繼資料，否則引擎無法匹配日期查詢。  
- **Index Access Exceptions**：確認 `indexFolder` 路徑可寫且未被其他程序鎖定。  

## 實務應用
1. **Archival Systems** – 取得特定歷史時期的記錄。  
2. **Content Management** – 支援如 `dd/MM/yyyy` 的區域日期格式，以符合歐洲使用者。  
3. **Financial Software** – 快速依財務季或年度篩選交易。  

## 結論
您現在擁有完整的 **custom date format java** 工具箱，可用於使用 GroupDocs.Search 建置強大的日期範圍搜尋。實作這些模式、微調效能，您的應用程式即可為任何時間查詢提供快速、精確的結果。

## 常見問答

**Q: 文字形式與物件式日期查詢有何差異？**  
A: 文字形式快速且簡易，但僅限於預設 ISO 格式；物件式查詢允許您提供 `Date` 物件與自訂格式，以獲得更大彈性。

**Q: 可以在單一查詢中搜尋多個日期範圍嗎？**  
A: 可以，將 `daterange` 子句與 `AND` 或 `OR` 等邏輯運算子結合，即可建立複雜查詢。

**Q: 自訂日期格式會降低搜尋速度嗎？**  
A: 會有少量額外的解析開銷，但對於一般工作負載影響微乎其微，且精確度提升的好處遠大於此。

**Q: GroupDocs.Search 適合大規模部署嗎？**  
A: 絕對適合。只要採取適當的索引策略與 JVM 調校，即可支援數百萬文件。

**Q: 在哪裡可以找到更多 Java 範例？**  
A: 前往 [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) 探索更多範例與使用情境實作。

---

**資源**
- **Documentation**： [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference**： [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**： [Get the latest version here](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository**： [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum**： [Join the discussion](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**： [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2025-12-18  
**測試版本：** GroupDocs.Search Java 25.4  
**作者：** GroupDocs