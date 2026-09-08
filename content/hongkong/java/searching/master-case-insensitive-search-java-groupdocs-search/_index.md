---
date: '2026-07-31'
description: 了解如何透過使用 GroupDocs.Search 將文件加入索引，並使用字元取代在索引過程中正規化文字，來實作 Java 的不分大小寫搜尋。
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Java 不分大小寫搜尋讓您能將文件加入索引並查詢，而無需擔心字母大小寫。本指南說明 GroupDocs.Search 如何在索引時正規化文字，以獲得快速且可靠的結果。
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Java 不分大小寫搜尋 – 使用 GroupDocs 索引文件
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: 在 Java 中將文件加入索引以進行不分大小寫搜尋
type: docs
url: /zh-hant/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# 在 Java 中將文件新增至索引以實現不區分大小寫的搜尋

當您需要 **case insensitive search java** 能可靠地在使用者輸入方式不同的情況下找到資訊時，關鍵是將文件新增至索引同時正規化文字。在本教學中，我們將說明如何設定 GroupDocs.Search for Java，使每個被索引的文件在建立索引時自動轉為小寫（或其他轉換），從而保證不分大小寫的搜尋結果，無需額外的查詢時邏輯。

## 快速解答
- **What does “add documents to index” mean?** 這表示將來源檔案載入可搜尋的資料結構，以便之後進行查詢。  
- **Why use character replacement?** 它會正規化每個字元——通常轉為小寫——讓搜尋自動忽略大小寫差異。  
- **Do I need a license?** 免費試用可用於開發；正式環境需購買完整授權。  
- **Which Java version is required?** Java 8 或更新版本；此函式庫最佳化於 Java 11+。  
- **Can I switch to case‑sensitive search when needed?** 可以——搜尋選項允許在每次查詢時切換大小寫敏感度。

## 在 GroupDocs.Search 中，「add documents to index」是什麼意思？

將您的來源檔案（PDF、DOCX、TXT 等）載入可搜尋的索引，使引擎能快速取回。將文件新增至索引會解析每個檔案、擷取純文字，並將其儲存於最佳化的資料結構中，以支援快速查找。

## 為什麼在建立索引時啟用字元取代？

字元取代會在建立索引的同時將每個字元轉換為預先定義的等價字元——最常見的是小寫。這可確保大小寫、變音符號或特定語系符號的差異不會影響搜尋結果。透過在索引階段正規化文字，引擎即可對一致的詞彙集合進行比對，提供快速且可靠的不分大小寫行為，且不需在每次搜尋時額外處理。

## 前置條件
- **GroupDocs.Search for Java** 版本 25.4 或更新（此函式庫支援 30 多種檔案格式，且可在不將整個檔案載入記憶體的情況下索引上百頁的文件）。  
- **Java Development Kit (JDK)** 8 或以上已安裝。  
- 具備基本的 **Maven** 使用經驗（或能手動加入 JAR）。

## 設定 GroupDocs.Search for Java

### Maven 設定
將 GroupDocs 套件庫與相依性加入您的 `pom.xml`：

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
如果您不想使用 Maven，可從官方網站取得最新的 JAR：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權
- **Free Trial** – 下載試用授權以開始實驗。  
- **Temporary License** – 從 GroupDocs 入口網站申請延長測試授權。  
- **Full License** – 準備上線時購買正式授權。

### 基本初始化（建立索引）
以下程式碼片段會建立索引資料夾並啟用字元取代：

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## 實作指南

### 在索引設定中啟用字元取代
啟用此功能會告訴引擎在建立索引時取代字元，這是實現不分大小寫行為的核心步驟。

#### 步驟 1：設定 `IndexSettings`
`IndexSettings` 為控制索引如何儲存與處理文字的設定物件。將 `useCharacterReplacements` 設為 **true** 後，即會開啟自動小寫（或您自訂的對應）功能。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### 設定字元取代
將每個字元映射至其小寫對應（或任何您需要的自訂對應）。

#### 步驟 2：定義並新增取代配對
取代字典會保存類似 `'A' → 'a'`、`'É' → 'e'` 等配對。於索引前加入這些配對，可確保每個詞彙皆已正規化。

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### 索引文件
現在索引已就緒，您可以從任意資料夾 **add documents to index**。

#### 步驟 3：新增文件以進行索引
GroupDocs.Search 會掃描目標目錄，從每種支援的檔案類型擷取文字，套用取代映射，並將詞彙寫入索引儲存空間。

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### 執行區分大小寫的搜尋（可選）

#### 步驟 4：執行區分大小寫的搜尋
`SearchOptions` 會設定查詢行為，例如切換大小寫敏感度，讓您能細緻控制搜尋方式。  
`SearchOptions.setUseCaseSensitiveSearch(true)` 會在特定查詢中強制引擎將大小寫視為不同，覆寫預設的不分大小寫行為。

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## 實務應用
1. **行銷活動** – 正規化產品名稱，讓業務團隊在搜尋資產時不必在意大小寫。  
2. **客服支援** – 為客服系統的搜尋框提供即時回應，無論使用者輸入「login」或「Login」皆能正確找到相關文章。  
3. **電商目錄** – 確保購物者不論如何輸入商品標題都能找到商品，提高轉換率。

## 效能考量
- **組織來源檔案** – 整齊的資料夾層級可減少 **add documents to index** 階段的掃描時間。  
- **監控記憶體** – 大規模索引會佔用大量 RAM；將檔案分批（500 – 1 000 件）處理可控制堆積使用量。  
- **非同步索引** – 若支援，請在背景執行索引作業，以保持 UI 響應並避免阻塞使用者操作。

## 常見問題與故障排除
| 症狀 | 可能原因 | 解決方案 |
|---------|--------------|-----|
| 已知關鍵字未返回結果 | 未啟用字元取代 | 確認 `settings.setUseCharacterReplacements(true)` 已設定，且取代字典包含所需字元。 |
| 索引期間發生記憶體不足錯誤 | 同時索引過多大型檔案 | 改為分較小批次索引，或提升 JVM 堆積大小（`-Xmx4g`）。 |
| 搜尋意外返回區分大小寫的結果 | 設定了 `SearchOptions.setUseCaseSensitiveSearch(true)` | 移除或改為 `false`，恢復預設的不分大小寫行為。 |
| 索引載入時間過長 | 資料夾布局效率低或未使用 SSD | 重新整理檔案結構、移除不必要的文件，並將索引存放於高速 SSD。 |
| 特殊字元被忽略 | 取代字典缺少 Unicode 條目 | 為如 “é”、 “ß”、 “ø” 等字元新增對應映射。 |

## 常見問答

**Q: How do I handle special characters (e.g., “é”, “ß”) during indexing?**  
A: 在取代字典中加入這些字元，將其映射為 ASCII 等價或依需求保持不變。

**Q: Can I limit character replacement to a specific language?**  
A: 可以。先建立僅包含目標語言字元的自訂取代陣列，再加入字典。

**Q: What should I do if the index takes a long time to load?**  
A: 優化資料夾結構、移除不必要的檔案，並將索引存放於高速 SSD。增量索引亦可減少載入負擔。

**Q: Is it possible to revert the character replacements after indexing?**  
A: 不行。取代已寫入索引資料，若要變更必須以新設定重新建立索引。

**Q: Where can I find more detailed API documentation?**  
A: 官方文件與 API 參考提供完整說明（請參考下方資源）。

## 資源
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/) 

---

**Last Updated:** 2026-07-31  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

## 相關教學

- [Character Replacement in GroupDocs.Search Java: A Comprehensive Guide to Enhance Text Search and Indexing](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Add documents to index: case‑sensitive Java search with GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)