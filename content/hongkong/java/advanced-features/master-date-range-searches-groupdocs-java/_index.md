---
date: '2026-10-07'
description: 了解如何使用 GroupDocs 實作自訂日期格式 Java 搜尋，涵蓋日期範圍查詢、自訂模式及效能技巧。
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: 自訂日期格式 Java 教學示範如何為 Java 設定 GroupDocs.Search、執行日期範圍查詢並提升效能。請參考逐步示例。
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: 自訂日期格式 Java – 使用 GroupDocs 進行日期範圍搜尋的指南
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: 自訂日期格式 Java | 使用 GroupDocs 進行日期範圍搜尋
type: docs
url: /zh-hant/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# 自訂日期格式 java | 使用 GroupDocs 的日期範圍搜尋

按日期搜尋文件是常見需求——無論您是構建檔案系統、財務報表工具，或內容管理入口網站。在本教學中，您將學習使用 GroupDocs.Search 的 **custom date format java** 技術，涵蓋日期範圍查詢、自訂模式定義，以及 **優化搜尋效能** 的技巧。完成後，您將能讓使用者檢索落在任何日期區間的記錄，無論使用何種格式。

## 快速解答
- **什麼是索引的主要類別？** `Index` 來自 `com.groupdocs.search` 套件。  
- **如何定義自訂日期模式？** 使用 `DateFormat` 搭配 `DateFormatElement` 物件與分隔符。  
- **我可以使用文字查詢嗎？** 可以，`daterange(start ~~ end)` 語法可直接在查詢字串中使用。  
- **需要哪些 Maven 坐標？** `com.groupdocs:groupdocs-search:25.4`（或更新版本）。  
- **開發是否需要授權？** 免費試用或臨時授權足以進行測試；正式環境則需商業授權。

## 什麼是 custom date format java？
Custom date format java 告訴 GroupDocs.Search 如何解讀不符合預設 ISO 格式 (YYYY‑MM‑DD) 的日期字串。透過定義自己的模式，例如 `MM/dd/yyyy` 或 `dd‑MM‑yyyy`，即可讓引擎辨識文件中使用區域或舊版格式的日期。此功能使您能在不同來源間一致地索引與查詢日期，提升以日期為中心的搜尋的召回率與精確度。

## 為何使用 GroupDocs.Search 進行日期範圍查詢？
GroupDocs.Search 結合高速索引與彈性查詢構造，十分適合日期範圍的情境。即使日期出現在自由文字或中繼資料欄位，引擎也能快速定位包含指定區間日期的文件。內建對多種檔案格式的支援與可自訂的日期解析器，讓您無需撰寫特定格式程式碼即可處理多樣的文件集合，同時在大型索引上仍能達到次秒回應時間。

## 如何使用 GroupDocs.Search 依日期搜尋文件
您將設定函式庫、索引範例資料夾，然後執行簡易文字形式查詢與較為豐富的物件型查詢。流程從建立 `Index` 實例、設定所需的自訂日期格式開始，接著以純字串或結構化的 `SearchQuery` 呼叫搜尋 API。此方式讓您依應用需求選擇適合的控制層級。

### 前置條件
- 已安裝 Java 8 或更新版本。  
- 用於相依管理的 Maven。  
- 取得 GroupDocs.Search 授權（試用或臨時授權可用於開發）。  

### 為 Java 設定 GroupDocs.Search

#### 使用 Maven 安裝
將儲存庫與相依項目加入您的 `pom.xml`：

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
或者，您也可以直接從 [GroupDocs.Search for Java 版本發布](https://releases.groupdocs.com/search/java/) 下載最新版本。

#### 基本初始化與設定
建立 `Index` 實例並加入您的文件：

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**定義說明：** `Index` 類別是核心容器，儲存您加入的每個檔案的可搜尋中繼資料，讓大型集合的快速查找成為可能。

## 功能 1：建立日期範圍搜尋查詢

### 使用文字形式查詢
最簡單的方式是直接在查詢字串中嵌入日期範圍：

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

**直接答案：** 載入您的索引，然後呼叫 `search("daterange(2022-01-01 ~~ 2022-12-31)")` 以取得所有索引日期介於 2022 年 1 月 1 日至 2022 年 12 月 31 日之間的文件。此單行查詢即開箱即用，且會依相關性排序返回結果。

**說明：** `daterange` 語法要求日期採用 `YYYY‑MM‑DD` 格式。它會返回所有索引日期落在該區間的文件。

### 使用查詢物件
若需程式化控制與自訂解析，可建立 `SearchQuery` 物件。`SearchQuery` 類別代表結構化查詢，可結合關鍵字、篩選條件與日期範圍等多種條件。

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

**直接答案：** 使用 `createDateRangeQuery(startDate, endDate)` 建立 `SearchQuery`，其中 `startDate` 與 `endDate` 為 `java.util.Date` 例項；然後將此查詢傳遞給 `index.search(query)`，即可取得考慮時區偏移與本地化曆法的精確結果。

**定義說明：** `SearchQuery` 類別封裝所有搜尋條件，讓您能將日期範圍與關鍵字篩選、布林運算子及提升規則結合。

**說明：** `createDateRangeQuery` 允許您提供 `java.util.Date` 物件，從而在時區與本地化處理上擁有完整彈性。

## 功能 2：指定 custom date format java 模式

### 設定自訂日期格式
`DateFormat` 類別告訴引擎如何根據元素順序與分隔符號拆分與解讀日期字串。定義與文件日期表示相符的 `DateFormat`：

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

**直接答案：** 使用 `dateFormat.clear()` 清除預設格式，然後加入由 `DateFormatElement` 物件（月份、日期、年份）組成的新 `DateFormat`，並將分隔符設定為 `/`。如此一來，引擎在索引與查詢時都能正確解析寫成 `MM/dd/yyyy` 的日期。

**定義說明：** `DateFormat` 為設定物件，告訴 GroupDocs.Search 如何根據元素順序與分隔符號拆分與解讀日期字串。

**說明：** 透過清除預設格式並加入使用 `/` 為分隔符的 `DateFormat`，引擎即可理解寫成 `MM/dd/yyyy` 的日期。這對於在偏好月在前表示法的地區執行 **依日期搜尋文件** 至關重要。

## 優化搜尋效能的技巧
- **增量索引：** 將新檔案加入現有索引，而非重新建置；每日更新可降低高達 70 % 的 CPU 使用率。  
- **修剪過期資料：** 定期移除不再需要的文件；精簡的索引可提升快取命中率並降低查詢延遲。  
- **調整記憶體設定：** 當索引大於 5 GB 時，將 JVM 堆積 (`-Xmx4g` 或更高) 提升，以避免記憶體不足錯誤。  
- **啟用多執行緒索引：** 使用 `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` 讓文件處理平行化，索引時間可縮減約等於 CPU 核心數的比例。

## 常見問題與解決方案
- **日期解析錯誤：** 確認文件的日期字串完全符合您定義的自訂模式；分隔符不符或缺少前導零會導致失敗。  
- **結果缺失：** 確認已索引的欄位包含日期中繼資料；若文件僅在自由文字段落中出現日期，請在索引時啟用 `ExtractDateMetadata` 選項。  
- **索引存取例外：** 確認 `indexFolder` 路徑可寫且未被其他程序鎖定；為每個環境（開發、測試、正式）使用專屬資料夾以避免衝突。

## 實務應用
1. **檔案系統** – 在不需手動正規化日期的情況下，檢索特定歷史時期的記錄。  
2. **內容管理** – 支援歐洲使用者常見的區域日期格式如 `dd/MM/yyyy`，提升使用者滿意度。  
3. **金融軟體** – 快速依財務季或年度篩選交易，實現即時報表儀表板。

## 為何這很重要
實作 **custom date format java** 處理可消除跨文件日期表示不一致所帶來的阻礙。它讓您能在單一索引中 **處理多種日期格式**，確保最終使用者無論原始日期如何記錄，都能取得精確結果。此彈性提升搜尋相關性、減少前置處理工作，縮短以日期為核心的應用程式的價值實現時間。

## 後續步驟
- 探索使用 `AND`、`OR`、`NOT` 運算子進行更進階的查詢組合。  
- 若需索引額外時間中繼資料（如嵌入 XML 標籤的時間戳記），可嘗試自訂分析器。  
- 參閱官方文件中的效能調校指南，將解決方案擴展至百萬文件與多租戶環境。

## 常見問答

**Q: 文字形式與物件型日期查詢有何差異？**  
A: 文字形式快速且簡便，但僅限於預設 ISO 格式；物件型查詢允許提供 `Date` 物件與自訂格式，具更高彈性。

**Q: 我可以在單一查詢中搜尋多個日期範圍嗎？**  
A: 可以，將 `daterange` 子句與 `AND` 或 `OR` 等邏輯運算子結合，即可建立複雜查詢。

**Q: 自訂日期格式會降低搜尋速度嗎？**  
A: 會有少量額外解析開銷，但對一般工作負載影響微乎其微，且精確度提升的好處遠大於此。

**Q: GroupDocs.Search 適合大規模部署嗎？**  
A: 絕對適合。透過適當的索引策略與 JVM 調校，可支援百萬文件，同時保持次秒級查詢回應時間。

**Q: 我在哪裡可以找到更多 Java 範例？**  
A: 前往 [GroupDocs GitHub 倉庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) 探索更多範例與使用案例實作。

---

**資源**
- **文件說明：** [GroupDocs Search 文件說明](https://docs.groupdocs.com/search/java/)
- **API 參考：** [GroupDocs API 參考](https://reference.groupdocs.com/search/java)
- **下載：** [在此取得最新版本](https://releases.groupdocs.com/search/java/)
- **GitHub 倉庫：** [GroupDocs GitHub 倉庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **在 GitHub 上檢視：** [在 GitHub 上檢視](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **免費支援論壇：** [加入討論](https://forum.groupdocs.com/c/search/10)
- **臨時授權：** [在此取得臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-10-07  
**測試環境：** GroupDocs.Search Java 25.4  
**作者：** GroupDocs  

## 相關教學
- [Groupdocs Search Java 進階搜尋功能](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Java 全文搜尋函式庫 – 使用 GroupDocs.Search 優化索引](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [如何在 Java 中使用 GroupDocs.Search 以中繼資料索引將文件加入索引](/search/java/indexing/groupdocs-search-java-metadata-indexing/)