---
date: '2026-07-07'
description: 了解如何停用 stop words java 並使用 GroupDocs.Search for Java 新增文件至索引，以提升搜尋準確度與效能。
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: 停用 stop words java 並使用 GroupDocs.Search for Java 新增文件至索引。遵循此一步一步的指南，以提升查詢準確度與效能。
og_title: 停用 Stop Words Java – 使用 GroupDocs 新增文件至索引
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: 停用 Stop Words Java – 使用 GroupDocs 新增文件至索引
type: docs
url: /zh-hant/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# 停用 Java 停用詞 – 使用 GroupDocs 將文件加入索引

在本教學中，您將學會在使用 GroupDocs.Search for Java 時 **disable stop words java**，同時將檔案加入可搜尋的索引。關閉內建的停用詞過濾器後，所有詞彙——包括「on」、「by」或「the」等常見詞——都會被索引，這對法律合約、電子商務目錄或技術手冊等專業領域的結果相關性提升極大。

## 快速解答
- **“將文件加入索引”是什麼意思？** 這表示將您的來源檔案載入可搜尋的索引，以便能有效地查詢。  
- **為什麼要停用停用詞？** 為了在搜尋時納入常見詞彙（例如 “on”、 “the”），當這些詞在您的領域中具有意義時。  
- **需要哪個版本的函式庫？** GroupDocs.Search for Java 25.4 或更新版本。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。  
- **可以在 Maven 專案中使用嗎？** 可以，只需在下方加入倉庫與相依性設定。

## 搜尋中的停用詞是什麼，為什麼可能想要停用它們？

停用詞是高頻率的詞彙，許多搜尋引擎會自動過濾它們以加快查詢處理。停用它們可確保 **每個詞**——包括傳統上被忽略的詞——都會貢獻至搜尋索引，當這些詞在特定領域具有意義時尤為重要。例如，在法律合約中，「by」可用來區分當事人；在產品目錄中，「on」可能是型號名稱的一部份。

## 在 GroupDocs.Search 中，將文件加入索引的運作方式是什麼？

當您加入文件時，GroupDocs.Search 會讀取每個檔案，將內容切分為詞彙，並將這些詞彙儲存在優化的倒排索引中。即使是包含 **數十萬檔案** 的集合，也能在次秒內完成檢索。此函式庫亦支援增量更新，讓您無需重新建構索引即可保持索引最新。

## 先決條件

- **必需的函式庫**：GroupDocs.Search for Java 25.4（或更新版本）。  
- **開發環境**：IntelliJ IDEA、Eclipse，或您偏好的任何 Java IDE。  
- **基本知識**：熟悉 Java 語法與索引概念。

## 設定 GroupDocs.Search for Java

### Maven 安裝

如果您使用 Maven，請在 `pom.xml` 中加入以下內容：

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

#### 取得授權步驟
- **免費試用** – 立即開始測試。  
- **臨時授權** – 取得時間限制的金鑰以獲得完整功能。  
- **購買** – 取得永久授權以供正式使用。

## 基本初始化與設定

IndexSettings 是一個設定類別，用於定義索引的建構方式、搜尋方式以及啟用的功能。

建立 `IndexSettings` 的實例以控制索引的行為：

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## 如何在搜尋中停用停用詞（Java）？

IndexSettings 是控制搜尋索引行為的設定物件。預設情況下會啟用內建的停用詞過濾器。若要關閉此過濾器，只需在 `IndexSettings` 實例上呼叫 `setUseStopWords(false)` 方法。這一呼叫即可停用停用詞移除，確保每個詞彙——包括像 “on” 或 “the” 這類常見詞——都會被索引並可供查詢。

## 如何將文件加入索引

將文件加入索引的方式是先建立帶有所需 `IndexSettings` 的 `Index` 物件，然後對每個檔案或資料夾呼叫其 `add` 方法。函式庫會讀取每份文件，將內容切分為詞彙，並將產生的詞彙儲存於倒排索引中，立即可供搜尋。您可以將索引指向特定的輸出目錄，並指定包含待索引檔案的來源資料夾。

### 定義輸出目錄

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### 指定文件目錄

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## 執行搜尋查詢

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

由於已啟用 `disable stop words java`，包含詞彙 “on” 的查詢將被評估，返回原本會被預設過濾器忽略的匹配結果。

## 實務應用

1. **企業文件搜尋** – 保留預設停用詞清單會剔除的關鍵術語。  
2. **電商平台** – 透過索引描述、型號與規格中的每個詞彙，提高產品可發現性。  
3. **法律研究工具** – 捕捉每個法律術語，即使是常被視為停用詞的詞彙，也能避免遺漏關鍵條款。

## 效能考量

- **最佳化建議**：定期更新與修剪索引，以保持高搜尋速度。GroupDocs.Search 可處理 **高達 100 萬文件**，仍能維持次秒查詢時間。  
- **資源使用**：監控 JVM 堆積大小；大型索引可能需要 4 GB 或更高的最大堆積 (`-Xmx`)。  
- **Java 記憶體管理**：對於極大規模的語料庫，使用堆外儲存選項，以將堆內佔用維持在 2 GB 以下。

## 常見問題與解決方案

| 症狀 | 可能原因 | 解決方式 |
|---|---|---|
| 常見詞無搜尋結果 | `setUseStopWords(true)`（預設） | 如上所示，呼叫 `setUseStopWords(false)`。 |
| 索引期間記憶體不足錯誤 | 一次索引過多大型檔案 | 分批索引檔案；增加 `-Xmx` JVM 參數。 |
| 搜尋返回過時資料 | 新增檔案後未刷新索引 | 呼叫 `index.update()` 或重新加入變更的文件。 |

## 常見問答

**Q: 什麼是停用詞？**  
A: 停用詞是常見的詞彙（例如 “the”、 “is”、 “on”），許多搜尋引擎會忽略它們以加快查詢速度。停用它們即可將每個詞彙視為可搜尋的。

**Q: 為什麼要在搜尋索引中停用停用詞？**  
A: 當需要精確片語匹配時——例如在法律或技術文件中——每個詞都有意義，因此必須包含停用詞。

**Q: GroupDocs.Search 如何處理大型資料集？**  
A: 此函式庫使用優化的資料結構與增量索引，即使面對 **數百萬文件**，也能保持低記憶體使用量。

**Q: 我可以將 GroupDocs.Search 整合到其他 Java 應用程式嗎？**  
A: 可以，API 設計為易於嵌入任何基於 Java 的系統，從 Web 服務到桌面應用程式皆可。

**Q: 如果搜尋結果不精確，我該怎麼辦？**  
A: 確認索引已包含所有必要的檔案（`add documents to index`），在需要時確保已停用停用詞過濾，並在重大變更後考慮重新建構索引。

## 其他資源

- **文件說明**： [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API 參考**： [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **下載**： [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- **GitHub 倉庫**： [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免費支援**： [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權**： [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

透過本指南，您現在已了解如何 **add documents to index** 與 **disable stop words java**，以在 Java 應用程式中提供更精確的搜尋結果。

**最後更新：** 2026-07-07  
**測試環境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs  

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## 相關教學

- [語言處理 Java – 使用 GroupDocs.Search 建立同義詞字典](/search/java/dictionaries-language-processing/)  
- [如何在 Java 中使用 GroupDocs.Search 透過 Metadata Indexing 將文件加入索引](/search/java/indexing/groupdocs-search-java-metadata-indexing/)  
- [如何使用 GroupDocs.Search for Java 將文件加入索引](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)