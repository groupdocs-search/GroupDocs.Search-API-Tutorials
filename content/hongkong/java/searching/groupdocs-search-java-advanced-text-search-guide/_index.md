---
date: '2026-01-24'
description: 了解如何使用 GroupDocs.Search 在 Java 中將文件加入索引並執行進階文字搜尋。設定索引、啟用詞形變化，並優化效能。
keywords:
- GroupDocs.Search Java
- advanced text search
- Java indexing
title: 使用 GroupDocs.Search Java 將文件加入索引
type: docs
url: /zh-hant/java/searching/groupdocs-search-java-advanced-text-search-guide/
weight: 1
---

？.Search Java？**連結）。

## 什麼是「將文件新增至索引」？
將文件新增至索引即是掃描來源檔案、擷取可搜尋的文字，並將這些資訊以結構化格式儲存，以便快速查找。GroupDocs.Search 內建支援多種檔案類型，讓您專注於業務邏輯，而不必自行處理解析。

## 為何要使用進階文字搜尋 Java 技術？
進階文字搜尋 Java 功能（如詞形辨識、模糊匹配與自訂排序）能在使用者的查詢與文件內容不完全相符時仍提供正確結果，提升使用者滿意度，減少搜尋文件的時間。

## 前置條件
- **必備程式庫**：GroupDocs.Search for Java 25.4。
- **環境設定**：Java JDK 8 或更新版本、Maven（或手動管理 JAR）。
- **知識前置**：基本的 Java 程式設計與 Maven 依賴管理。

## 設定 GroupDocs.Search for Java
在撰寫程式碼之前，先確保程式庫已加入您的專案。

### Maven 設定
在 `pom.xml` 檔案中加入以下設定：

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
若不想使用 Maven，可從官方頁面直接下載最新的 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權步驟
1. **免費試用** – 無償探索 API。  
2. **暫時授權** – 延長試用期以進行更深入測試。  
3. **購買** – 取得正式商業授權以供生產環境使用。

## 步驟式實作指南

### 1. 建立並設定索引
索引是任何搜尋解決方案的核心，負責儲存斷詞後的文字與中繼資料，以便快速檢索。

#### 概觀
我們將在磁碟上建立一個資料夾，用來存放索引檔案。

#### 程式碼
```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/SearchForDifferentWordForms";
Index index = new Index(indexFolder);
```

*說明*：`Index` 建構子指向一個資料夾，所有索引資料將持久化於此。請將 `YOUR_DOCUMENT_DIRECTORY` 替換為您機器上的實際路徑。

### 2. 如何將文件新增至索引
索引建立完成後，需要 **將文件新增至索引**，才能讓它們可被搜尋。

#### 概觀
GroupDocs.Search 會掃描指定的目錄，將每一個支援的檔案類型加入索引。

#### 程式碼
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
index.add(documentsFolder);
```

*說明*：`add` 方法會遞迴處理資料夾、擷取文字並寫入索引。請確認路徑正確且應用程式具備讀取權限。

### 3. 設定詞形搜尋選項
為了讓搜尋容忍語法變化（例如 “wish”、 “wished”、 “wishes”），請啟用詞形搜尋。

#### 概觀
我們將調整 `SearchOptions` 以開啟此功能。

#### 程式碼
```java
import com.groupdocs.search.SearchOptions;

SearchOptions options = new SearchOptions();
options.setUseWordFormsSearch(true); // Enables search for different grammatical variations of words.
```

*說明*：設定 `setUseWordFormsSearch(true)` 後，搜尋引擎會將查詢展開至已知的詞形變化，提高召回率。

### 4. 執行搜尋
索引已填充且選項已設定好，現在可以執行查詢。

#### 概觀
我們將搜尋關鍵字 “wished”，並取得符合的文件。

#### 程式碼
```java
import com.groupdocs.search.SearchResult;

String query = "wished";
SearchResult result = index.search(query, options);
```

*說明*：`search` 方法使用先前定執行查詢。回傳的 `SearchResult` 包含一系列命中結果，每筆結果都帶有文件參考與文字片段。

## 常見問題與除錯
- **路徑錯誤** – 請不同能透 讓引分配足夠的堆記憶體。  
- 定期呼叫 `index.optimize()`（若有提供）以壓縮索引檔案。

## 結論
現在您已掌握 **將文件新增至索引**、啟用進階文字搜尋以及微調 GroupDocs.Search for Java 的方法。這些技巧能協助您在任何文件集合上打造即時、功能豐富的搜尋體驗。

### 後續步驟
- 嘗試模糊匹配與自訂排序。  
- 將搜尋模組整合至 REST API，供前端呼叫。  
- 透過設定語言專屬分析器，探索多語言支援。

## 常見問答

**Q1：GroupDocs.Search 支援哪些檔案格式？**  
A1：支援包括 DOCX、PDF、PPTX、TXT 等多種格式，完整列表請參考官方文件。

**Q2：如何將新文件加入已存在的索引？**  
A2：只需再次呼叫 `index.add(newDocumentsFolder)`，程式庫會自動加入新檔或已變更的檔案。

**Q3：我可以進一步自訂搜尋查詢嗎？**  
A3：可以——`SearchOptions` 提供模糊搜尋、大小寫敏感與分頁等設定。

**Q4：我的搜尋速度很慢，該怎麼辦？**  
A4：確保索引儲存在高速 SSD、提升 JVM 堆記憶體、並避免索引不必要的大檔案。

**Q5：哪裡可以取得社群支援？**  
A5：請使用官方支援論壇： [GroupDocs Support Forum](https://forum.groupdocs.com/c/search/10)。

## 資源
- **文件說明**：前往 [GroupDocs Documentation](https://docs.groupdocs.com/search/java/) 瀏覽深入指南

---

**最後更新：** 2026-01-24  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs