---
date: '2025-12-19'
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

# 精通 GroupDocs.Search 的 java 檔案副檔名過濾器

管理日益增長的文件庫很快會變得難以應付。無論您是只需要索引特定文件類型，還是排除不相關的檔案，**java file extension filter** 都能讓您對處理的內容進行精細控制。本指南將說明如何設定 GroupDocs.Search for Java，並展示如何將檔案副檔名過濾與邏輯 AND、OR、NOT 運算子，以及日期範圍與路徑過濾結合使用。

## 快速解答
- **What is the java file extension filter?** 告訴 GroupDocs.Search 在索引過程中要包含或排除哪些檔案副檔名的設定。  
- **Which library provides this feature?** GroupDocs.Search for Java。  
- **Do I need a license?** 免費試用可用於評估；正式環境需購買完整授權。  
- **Can I combine filters?** 可以 — 您可以將副檔名、日期、大小與路徑過濾器以 AND、OR、NOT 邏輯串接。  
- **Is it Maven‑compatible?** 完全相容 — 將 GroupDocs.Search 依賴加入您的 `pom.xml`。

## 介紹

在缺乏合適工具的情況下，管理日益增長的檔案庫、依類型組織文件或在索引時過濾不必要的檔案都相當艱鉅。**GroupDocs.Search for Java** 是一套先進的搜尋函式庫，透過強大的檔案過濾功能簡化這些挑戰。本教學將指導您使用 GroupDocs.Search 實作 .NET 檔案過濾技術，重點說明邏輯 AND、OR、NOT 過濾器。

### 您將學習
- 在 Java 環境中設定 GroupDocs.Search  
- 實作各種過濾器：檔案副檔名、邏輯運算子 (AND、OR、NOT)、建立時間、修改時間、檔案路徑與長度  
- 這些過濾器在實務文件管理中的應用  
- 大型索引任務的效能優化技巧  

準備好釋放 Java 中檔案過濾的全部潛能了嗎？讓我們先來了解前置條件。

## 前置條件

在開始之前，請確保您具備以下項目：

### 必要的函式庫與相依性
- **GroupDocs.Search for Java**：版本 25.4 或更新版本  
- **Java Development Kit (JDK)**：確保系統已安裝相容的版本  

### 環境設定
- 整合開發環境 (IDE)：使用 IntelliJ IDEA、Eclipse，或任何支援 Maven 專案的 IDE。  

### 知識前置條件
- 基本的 Java 程式設計概念  
- 熟悉 Java 的檔案 I/O 操作  
- 了解正規表達式與日期時間的操作  

## 設定 GroupDocs.Search for Java

要開始使用 GroupDocs.Search，必須將其作為相依性加入專案。以下說明步驟：

### Maven 設定
在 `pom.xml` 檔案中加入以下儲存庫與相依性設定：

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
1. **Free Trial**：使用免費試用來探索 GroupDocs.Search 功能。  
2. **Temporary License**：申請臨時授權，以無限制使用完整功能。  
3. **Purchase**：長期使用請購買訂閱。  

### 基本初始化與設定
加入函式庫後，初始化索引環境：

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## 實作指南

現在，我們來探討如何使用 GroupDocs.Search 實作各種檔案過濾功能。

### 檔案副檔名過濾
在索引過程中依副檔名過濾檔案。此功能適用於僅處理特定文件類型，例如 FB2、EPUB 與 TXT。

#### 概觀
使用自訂過濾設定，依檔案副檔名過濾文件。

#### 實作步驟
1. **Create Filter**：

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize Index and Add Documents**：

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 邏輯 NOT 過濾
在索引時排除特定檔案副檔名，例如 HTM、HTML 與 PDF。

#### 實作步驟
1. **Create Exclusion Filter**：

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to Index Settings**：

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add Documents**：

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 邏輯 AND 過濾
結合多項條件，只納入符合所有指定條件的檔案。

#### 概觀
使用邏輯 AND 運算，依建立時間、檔案副檔名與長度過濾檔案。

#### 實作步驟
1. **Define Filters**：

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine Filters**：

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index Documents**：

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 邏輯 OR 過濾
使用邏輯 OR 運算，納入符合任一指定條件的檔案。

#### 實作步驟
1. **Define Filters**：

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine Filters with Logical Conditions**：

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR Filter**：

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 建立時間過濾
依檔案建立時間過濾，只納入位於指定日期範圍內的檔案。

#### 實作步驟
1. **Define Date Range Filter**：

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index Documents**：

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 修改時間過濾
排除在特定日期之後被修改的檔案。

#### 實作步驟
1. **Define Filter**：

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index Documents**：

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 檔案路徑過濾
依檔案路徑過濾，只納入位於特定目錄的檔案。

#### 實作步驟
1. **Define File Path Filter**：

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize Index and Add Documents**：

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## 常見陷阱與技巧

- **Never mix absolute and relative paths** 在同一過濾設定中不要混用絕對路徑與相對路徑——這可能導致意外的排除。  
- **Remember to reset the `IndexSettings`** 當您從一組過濾器切換到另一組時，請記得重設 `IndexSettings`；否則先前的過濾器可能仍然有效。  
- **Large file collections** 結合長度上限與副檔名過濾，可降低記憶體使用量。  

## 常見問題

**Q: Can I change the filter criteria after the index is created?**  
A: 可以。您可以使用新的 `DocumentFilter` 重新建立索引，或以更新的設定執行增量索引。

**Q: Does the java file extension filter work on compressed archives (e.g., ZIP)?**  
A: GroupDocs.Search 能索引支援的壓縮檔格式，但副檔名過濾只套用於壓縮檔本身，而非內部檔案。如有需要，可使用巢狀過濾器。

**Q: How do I debug why a particular file was excluded?**  
A: 開啟函式庫的日誌功能（設定 `LoggingOptions.setEnabled(true)`），檢查產生的日誌——其中會說明是哪個過濾器拒絕了該檔案。

**Q: Is it possible to combine the java file extension filter with custom regex filters?**  
A: 完全可以。您可以將正則表達式過濾器包在 `DocumentFilter.createAnd()` 中，與副檔名過濾器一起使用。

**Q: What performance impact does adding many filters have?**  
A: 每新增一個過濾器會在索引時帶來少量額外開銷，但減少索引大小的好處通常超過成本。建議使用樣本資料測試，以找出最佳平衡點。

---

**最後更新：** 2025-12-19  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs