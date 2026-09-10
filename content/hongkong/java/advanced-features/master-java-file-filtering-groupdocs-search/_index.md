---
date: '2026-09-06'
description: 了解如何使用 GroupDocs.Search for Java 過濾 java 檔案副檔名，涵蓋邏輯 AND、OR、NOT 運算子、日期範圍過濾以及路徑過濾。
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: 使用 GroupDocs.Search 過濾 java 檔案副檔名。了解如何在 Java 中結合副檔名、日期範圍與路徑過濾，並使用邏輯運算子。
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: 使用 GroupDocs.Search 過濾 java 檔案副檔名 – 完整指南
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: 如何使用 GroupDocs.Search 過濾 java 檔案副檔名
type: docs
url: /zh-hant/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# 使用 GroupDocs.Search 過濾 Java 檔案副檔名

在本完整教學中，您將學習如何在使用 GroupDocs.Search 索引文件時 **filter file extensions java**。完成本指南後，您將能只保留所需的檔案類型、排除不需要的格式，並可使用 AND、OR、NOT 邏輯運算子將這些規則與日期範圍和路徑過濾結合。此方法可讓索引保持精簡、加快搜尋速度，並協助您遵守資料處理政策。

## 快速解答
- **What is the java file extension filter?** 它是一條規則，告訴 GroupDocs.Search 在索引時要包含或排除哪些檔案副檔名。  
- **Which library provides this feature?** GroupDocs.Search for Java。  
- **Do I need a license?** 免費試用可用於評估；正式環境需要完整授權。  
- **Can I combine filters?** 是的 – 您可以將副檔名、日期、大小和路徑過濾器以 AND、OR、NOT 邏輯串接。  
- **Is it Maven‑compatible?** 絕對相容 – 將 GroupDocs.Search 相依性加入您的 `pom.xml`。

## 什麼是 java file extension filter？
**java file extension filter** 是一組規則，用於在檔案送入索引引擎前評估其副檔名。透過指定如 `.txt`、`.pdf` 或 `.epub` 等副檔名，您可以 **include files by extension** 或 **exclude files by extension**，以保持索引的聚焦並使搜尋結果更相關。

## 為何在 GroupDocs.Search 中使用檔案副檔名過濾？
檔案副檔名過濾透過排除不相關的格式提升索引效率，減少儲存需求，並藉由防止不需要的內容進入索引，協助符合合規規範。由於搜尋引擎處理的資料集較小且更相關，亦可加快查詢回應速度。

- **Performance:** 跳過不需要的檔案可減少 I/O，並在大型資料庫上將索引速度提升最高 40 %。  
- **Storage savings:** 僅將相關文件存入索引，可平均降低磁碟使用量 30 %。  
- **Compliance:** 防止機密或不支援的檔案類型被意外索引。  
- **Flexibility:** 可結合 **date range filter java** 功能，以針對特定期間內建立或修改的檔案。

## 前置條件

在開始之前，請確保您具備以下條件：

### 必要的程式庫與相依性
- **GroupDocs.Search for Java** – 版本 25.4 或更新（支援 60+ 輸入格式）。  
- **Java Development Kit (JDK)** – 任意相容版本（8 或更新）。

### 環境設定
- 整合開發環境 (IDE)：IntelliJ IDEA、Eclipse，或任何相容 Maven 的 IDE。

### 知識前提
- 基本的 Java 程式設計。  
- 熟悉 Java 的檔案 I/O。  
- 了解正規表達式與日期時間處理。

## 設定 GroupDocs.Search for Java
要開始使用 GroupDocs.Search，您需要在專案中加入其相依性。

### Maven 設定
將以下儲存庫與相依性設定加入您的 `pom.xml` 檔案：

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
或者，直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

#### 取得授權
1. **Free trial** – 免費試用功能。  
2. **Temporary license** – 在有限期間內取得完整功能。  
3. **Purchase** – 取得永久授權以供正式使用。

### 基本初始化與設定
加入程式庫後，初始化您的索引環境。`IndexSettings` 類別包含所有設定選項，包括過濾器。

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## 實作指南
以下我們將深入各種過濾類型，說明 **why it matters**，並提供可直接複製到專案中的逐步說明。

### 檔案副檔名過濾
在索引過程中依副檔名過濾檔案。當您只想處理電子書（`.fb2`、`.epub`）與純文字檔（`.txt`）時，此功能非常適合。

#### 概觀
`DocumentFilter.createFileExtension` 會建立副檔名白名單。

#### 實作步驟
1. **Create filter** – 定義您想保留的副檔名。

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – 在建構 `IndexSettings` 時套用過濾器。

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 邏輯 NOT 過濾器
在搜尋情境中不需要時，排除特定副檔名，例如網頁與 PDF。

#### 實作步驟
1. **Create exclusion filter** – 指定要排除的副檔名。

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – 將 NOT 過濾器與其他規則結合。

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – 只有通過組合過濾器的檔案會被索引。

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 邏輯 AND 過濾器
結合多項條件——建立日期、副檔名與檔案大小——使 **only files that meet all criteria** 被索引。

#### 概觀
`DocumentFilter.createAnd` 將多個過濾器合併為單一規則。

#### 實作步驟
1. **Define filters** – 為每個條件建立個別過濾器。

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – 使用 AND 運算子以要求全部條件。

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – 將組合過濾器傳入索引流程。

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 邏輯 OR 過濾器
納入符合 **any** 指定條件的檔案——當您想同時捕捉小型文字檔與較大非文字檔時非常有用。

#### 實作步驟
1. **Define filters** – 為每個備選條件建立獨立過濾器。

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – 使用 OR 運算子。

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – 將組合過濾器附加至索引設定。

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 建立時間過濾器
針對在特定期間內建立的檔案——典型的 **date range filter java** 情境。

#### 實作步驟
1. **Define date‑range filter** – 指定開始與結束日期。

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – 只有建立時間落在範圍內的檔案會被索引。

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 修改時間過濾器
排除在特定截止日期之後被修改的檔案。

#### 實作步驟
1. **Define filter** – 設定最大修改時間戳記。

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – 超過截止日期的檔案會被忽略。

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 檔案路徑過濾
限制索引僅包含位於特定資料夾或符合模式的檔案——適用於在特定目錄層級內 **include files by extension**。

#### 實作步驟
1. **Define file‑path filter** – 使用 glob 或正規表達式模式匹配目錄。

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – 在其他規則同時套用路徑過濾器。

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## 常見陷阱與技巧

- **Never mix absolute and relative paths** 在同一過濾設定中混用絕對與相對路徑——可能導致意外排除。  
- **Reset the `IndexSettings`** 在切換過濾組時重設；否則先前的過濾器可能仍然存在。  
- **Combine a length upper bound with an extension filter** 於大型集合中結合長度上限與副檔名過濾，以降低記憶體使用。  
- LoggingOptions 控制 GroupDocs.Search 的日誌設定。  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) 以查看檔案被拒絕的原因。  

## 常見問答

**Q: Can I change the filter criteria after the index is created?**  
A: 是的。使用新的 `DocumentFilter` 重新建立索引，或使用增量索引並套用更新的設定。

**Q: Does the java file extension filter work on compressed archives (e.g., ZIP)?**  
A: GroupDocs.Search 能索引支援的壓縮檔格式，但副檔名過濾器僅套用於壓縮檔本身，而非內部檔案。若需更深入的控制，可使用巢狀過濾器。

**Q: How do I debug why a particular file was excluded?**  
A: 開啟程式庫的日誌 (`LoggingOptions.setEnabled(true)`) 並檢查日誌——它會報告是哪個過濾器拒絕了每個檔案。

**Q: Is it possible to combine the java file extension filter with custom regex filters?**  
A: 絕對可以。將正規表達式過濾器與副檔名過濾器一起包在 `DocumentFilter.createAnd()` 中。

**Q: What performance impact does adding many filters have?**  
A: 每個過濾器在索引時會帶來適度的開銷，但減少索引資料量通常能抵消此成本。請使用具代表性的樣本測試，以找出最佳平衡點。

---

**Last Updated:** 2026-09-06  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## 相關教學

- [自訂日期格式 Java | 使用 GroupDocs 的日期範圍搜尋](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or：精通 GroupDocs.Search for Java 的布林搜尋](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [使用進階索引技術優化 GroupDocs.Search for Java 的搜尋效能](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

