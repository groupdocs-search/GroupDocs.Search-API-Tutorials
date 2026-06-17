---
date: '2026-02-21'
description: 學習如何使用 GroupDocs.Search for Java 實作 Java 檔案副檔名過濾器，涵蓋邏輯運算子、建立/修改日期以及路徑過濾。
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: 使用 GroupDocs.Search 的 Java 檔案副檔名過濾器 – 指南
type: docs
url: /zh-hant/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

 Should we translate? Probably keep as is? The rule: translate all text content, but keep URLs unchanged. So we can translate link text. But it's a proper name; maybe keep English. I'd translate to "GroupDocs.Search for Java 版本". But maybe keep original. Safer to keep as is? The instruction: "Keep technical terms in English". "GroupDocs.Search for Java releases" is a title; could keep English. I'll keep as is.

Similarly bullet points with technical terms.

Let's produce translation.

# 精通 GroupDocs.Search 的 java file extension filter

管理日益增長的文件庫很快會變得難以應付，尤其是當您只需要索引特定檔案類型時。**The java file extension filter** 讓您告訴 GroupDocs.Search 要包含或排除哪些副檔名，從而對索引流程進行精確控制。本指南將逐步說明如何為 Java 設定 GroupDocs.Search，並展示如何將檔案副檔名過濾與邏輯 AND、OR、NOT 運算子以及日期範圍與路徑過濾結合使用。

## 快速回答
- **什麼是 java file extension filter？** 一種設定，可告訴 GroupDocs.Search 在索引過程中要包含或排除哪些檔案副檔名。  
- **哪個程式庫提供此功能？** GroupDocs.Search for Java。  
- **需要授權嗎？** 免費試用可用於評估；正式環境需購買完整授權。  
- **可以結合多種過濾器嗎？** 可以 – 您可以將副檔名、日期、大小與路徑過濾器以 AND、OR、NOT 方式串接。  
- **支援 Maven 嗎？** 完全支援 – 只需將 GroupDocs.Search 相依加入 `pom.xml`。

## 什麼是 java file extension filter？
**java file extension filter** 是一組規則，會在檔案送入索引引擎前先檢查其副檔名。透過指定 `.txt`、`.pdf`、`.epub` 等副檔名，您可以 **include files by extension** 或 **exclude files by extension**，讓索引更聚焦、搜尋結果更相關。

## 為何在 GroupDocs.Search 中使用檔案副檔名過濾？
- **效能提升：** 跳過不需要的檔案可減少 I/O，加快索引速度。  
- **節省儲存空間：** 只將相關文件寫入索引，降低磁碟使用量。  
- **合規性：** 防止意外索引機密或不支援的檔案類型。  
- **彈性：** 可與 **date range filter java** 功能結合，針對特定期間內建立或修改的檔案。

## 前置條件

在開始之前，請確保您已具備以下項目：

### 必要的程式庫與相依
- **GroupDocs.Search for Java**：版本 25.4 或更新版本  
- **Java Development Kit (JDK)**：相容的版本已安裝  

### 環境設定
- 整合開發環境 (IDE)：IntelliJ IDEA、Eclipse，或任何支援 Maven 的 IDE。

### 知識前提
- 基本的 Java 程式設計  
- 熟悉 Java 的檔案 I/O  
- 了解正規表達式與日期時間處理  

## 設定 GroupDocs.Search for Java
要開始使用 GroupDocs.Search，必須將其加入專案相依。

### Maven 設定
在 `pom.xml` 中加入以下 repository 與 dependency 設定：

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
或是直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

#### 取得授權
1. **Free Trial** – 免費體驗全部功能。  
2. **Temporary License** – 獲得有限期間的完整功能。  
3. **Purchase** – 取得永久授權以供正式使用。  

### 基本初始化與設定
加入程式庫後，初始化索引環境：

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## 實作指南
以下將逐一說明每種過濾器的用途，並提供可直接複製到專案的步驟說明程式碼。

### 檔案副檔名過濾
在索引過程中依副檔名過濾檔案。適用於只想處理電子書 (`.fb2`、`.epub`) 與純文字檔 (`.txt`) 的情境。

#### 概觀
使用 `DocumentFilter.createFileExtension` 來建立白名單。

#### 實作步驟
1. **建立過濾器**：

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **初始化索引並加入文件**：

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical NOT 過濾器
在不需要的搜尋情境下，排除特定副檔名（例如網頁與 PDF）。

#### 實作步驟
1. **建立排除過濾器**：

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **套用至 Index Settings**：

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **加入文件**：

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical AND 過濾器
結合多項條件——建立日期、副檔名與檔案大小——使 **only files that meet all criteria** 被索引。

#### 概觀
`DocumentFilter.createAnd` 可將多個過濾器合併為單一規則。

#### 實作步驟
1. **定義過濾器**：

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **合併過濾器**：

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **索引文件**：

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical OR 過濾器
包含符合 **any** 指定條件的檔案——適合同時捕捉小型文字檔與較大非文字檔的情況。

#### 實作步驟
1. **定義過濾器**：

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **以邏輯條件合併過濾器**：

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **完成 OR 過濾器**：

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 建立時間過濾器
針對特定期間內建立的檔案——典型的 **date range filter java** 情境。

#### 實作步驟
1. **定義日期範圍過濾器**：

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **索引文件**：

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 修改時間過濾器
排除在某個截止日期之後被修改的檔案。

#### 實作步驟
1. **定義過濾器**：

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **索引文件**：

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 檔案路徑過濾器
限制索引僅針對特定資料夾或符合特定模式的檔案——非常適合在特定目錄層級內 **include files by extension**。

#### 實作步驟
1. **定義檔案路徑過濾器**：

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **初始化索引並加入文件**：

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## 常見問題與技巧

- **絕對路徑與相對路徑** 切勿混用於同一過濾器設定，否則可能導致意外排除。  
- 在切換過濾器組合時，**務必重設 `IndexSettings`**，否則先前的過濾器會持續生效。  
- **將長度上限與副檔名過濾結合**，可在大型集合中降低記憶體使用。  
- **啟用日誌** (`LoggingOptions.setEnabled(true)`) 以了解檔案被拒絕的原因。  

## 常見問答

**Q: 可以在建立索引後變更過濾條件嗎？**  
A: 可以。重新建立索引並使用新的 `DocumentFilter`，或以增量索引方式套用更新的設定。

**Q: java file extension filter 能作用於壓縮檔案 (如 ZIP) 嗎？**  
A: GroupDocs.Search 能索引支援的壓縮檔格式，但副檔名過濾僅針對壓縮檔本身，而非內部檔案。若需更細緻的控制，請使用巢狀過濾器。

**Q: 如何偵錯某個檔案被排除的原因？**  
A: 開啟程式庫的日誌 (`LoggingOptions.setEnabled(true)`) 並檢查日誌內容，裡面會說明是哪個過濾器拒絕了該檔案。

**Q: 可以將 java file extension filter 與自訂正規表達式過濾器結合嗎？**  
A: 完全可以。將正規表達式過濾器包在 `DocumentFilter.createAnd()` 中，與副檔名過濾器一起使用。

**Q: 加入大量過濾器會對效能產生什麼影響？**  
A: 每個過濾器在索引時會帶來少量額外開銷，但因為減少了被索引的資料量，通常整體效能會提升。建議以具代表性的樣本測試，找出最佳平衡點。

---

**最後更新：** 2026-02-21  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs