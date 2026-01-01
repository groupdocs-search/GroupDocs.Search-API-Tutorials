---
date: '2025-12-19'
description: 學習如何在 Java 中使用 GroupDocs.Search 新增同義詞、以同義詞進行搜尋以及管理同義詞組。提升搜尋索引的效能與可靠性。
keywords:
- synonym dictionaries java
- groupdocs.search synonym implementation
- java search functionality enhancement
title: 如何在 Java 中使用 GroupDocs.Search 添加同義詞 – 全面指南
type: docs
url: /zh-hant/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Search 添加同義詞

歡迎閱讀我們的完整指南，了解 **如何在 Java 中使用 GroupDocs.Search 添加同義詞**。無論您是構建內容豐富的 CMS、電商目錄，或是文件倉庫，啟用同義詞支援都能顯著提升資料的可發現性。在本教學中，您將學會建立與管理同義詞字典、匯入同義詞字典檔案，以及優化搜尋索引以獲得快速且精確的結果。

## 快速回答
- **添加同義詞的主要步驟是什麼？** 初始化 `Index` 並使用 `SynonymDictionary` API。  
- **我可以匯入同義詞字典嗎？** 可以 – 使用 `importDictionary(path)` 載入預先建立的檔案。  
- **如何啟用同義詞搜尋？** 設定 `SearchOptions.setUseSynonymSearch(true)`。  
- **可以管理同義詞群組嗎？** 當然可以 – 您可以透過字典 API 清除、添加或取得群組。  
- **優化搜尋索引時需要注意什麼？** 定期修剪未使用的條目，並為大型資料集調整 JVM 堆積大小。  

## 「如何添加同義詞」是什麼？
添加同義詞是指定義替代的單詞或片語，讓搜尋引擎將它們視為等價。這樣一來，查詢 **「better」** 也會匹配包含 **「improve」**、**「enhance」** 或 **「upgrade」** 的文件。

## 為什麼在 GroupDocs.Search 中使用同義詞支援？
- **提升使用者體驗：** 即使用戶使用不同的術語，也能找到相關內容。  
- **提高轉換率：** 電商網站透過匹配多樣的商品查詢，捕獲更多銷售機會。  
- **降低維護成本：** 一個字典可供多個應用程式使用，簡化更新流程。  

## 前置條件
- **GroupDocs.Search for Java** 版本 25.4 或更新版本。  
- 具備 Maven 支援的 Java IDE（IntelliJ IDEA、Eclipse 等）。  
- 基本的 Java 知識與 Maven 專案結構的熟悉度。

### 必要的函式庫與版本
- GroupDocs.Search for Java 版本 25.4 或更高。

### 環境設定
- 您偏好的 IDE（IntelliJ IDEA、Eclipse 等）。  
- 用於相依管理的 Maven。

### 知識需求
- Java 的物件導向程式設計。  
- 基本的檔案 I/O 操作。

## 設定 GroupDocs.Search for Java

### 安裝資訊
在 `pom.xml` 中加入儲存庫與相依性：

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

**直接下載** – 您也可以從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR 檔。

### 取得授權
- **免費試用：** 無需授權即可測試核心功能。  
- **臨時授權：** 在評估期間延長試用功能。  
- **購買授權：** 生產環境使用及完整功能集皆需授權。

#### 基本初始化與設定
建立 `Index` 實例，然後加入可搜尋的文件：

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## 如何將同義詞加入搜尋索引
建立索引是基礎。以下步驟將逐一說明，並提供完整程式碼範例。

### 功能 1：建立與索引 Index
```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### 功能 2：取得單字的同義詞
```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### 功能 3：取得同義詞群組
```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### 功能 4：管理同義詞字典條目
```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### 功能 5：將同義詞匯出至檔案
```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### 功能 6：從檔案匯入同義詞
```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### 功能 7：使用同義詞支援執行搜尋
```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## 如何使用同義詞搜尋
只要將 `setUseSynonymSearch(true)` 設為啟用，搜尋引擎會自動根據您建立或匯入的同義詞字典擴展查詢。此步驟對於在不改變使用者搜尋行為的前提下，提供更豐富的結果至關重要。

## 如何匯入同義詞字典
如果您已有其他環境產生的 `.dat` 檔，只需呼叫 `importDictionary(path)` 即可。此方式非常適合在開發、測試與正式環境之間同步字典。

## 如何管理同義詞群組
同義詞群組允許您將一組詞彙視為單一邏輯實體。透過 `SynonymDictionary` API，您可以依照上述程式碼片段添加、清除或取得群組。

## 如何優化搜尋索引
- **定期修剪未使用的條目：** 在大量更新前使用 `clear()`。  
- **調整 JVM 堆積：** 大型字典可能需要更多記憶體。  
- **保持函式庫為最新版本：** 新版會包含效能改進。

## 實務應用
1. **內容管理系統 (CMS)：** 即使用戶使用替代術語，也能找到文章。  
2. **電商平台：** 商品搜尋能容忍「laptop」與「notebook」等同義詞。  
3. **文件倉庫：** 法律或醫療檔案可受益於領域專屬的同義詞群組。

## 效能考量
- **優化索引儲存：** 定期重建索引以移除過時資料。  
- **管理記憶體使用量：** 載入大型同義詞檔時監控堆積消耗。  
- **定期更新：** 使用最新的 GroupDocs.Search 版本以取得錯誤修正與速度提升。

## 結論
您現在已掌握 **如何添加同義詞**、匯入同義詞字典檔案、管理同義詞群組，以及 **使用同義詞搜尋** 的完整步驟。運用這些技巧可提升相關性、改善使用者滿意度，並確保搜尋索引保持最佳效能。

## 常見問答

**Q: 使用 GroupDocs.Search 的最低系統需求是什麼？**  
A: 任何支援相容 JDK（Java 8 或更新版）的現代作業系統皆可。

**Q: 同義詞字典應該多久更新一次？**  
A: 新術語出現時即更新 – 使用 `clear()` 後搭配 `addRange()` 進行全新刷新。

**Q: 可以在未購買授權的情況下使用 GroupDocs.Search 嗎？**  
A: 免費試用可用於評估，但正式上線必須取得授權。

**Q: 大量資料集的索引最佳實踐是什麼？**  
A: 將資料分批處理，監控堆積使用，並排程定期的索引維護。

**Q: 為何同義詞匹配不到預期結果？我該檢查什麼？**  
A: 確認字典已正確匯入、`setUseSynonymSearch(true)` 已啟用，且相關詞彙已存在於同義詞群組中。

**資源**  
- [Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java)  
- [Download GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)  
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2025-12-19  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  
