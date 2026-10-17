---
date: '2026-10-17'
description: 了解如何在 Java 中使用 GroupDocs.Search 的 synonyms、匯入 synonym dictionaries、管理
  synonym groups，並優化搜尋索引以提升相關性。
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: 了解如何在 Java 中使用 GroupDocs.Search 的 synonyms、匯入 synonym dictionaries、管理
  synonym groups，並優化搜尋索引以提升相關性。
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: 如何在 Java 中使用 GroupDocs.Search 的 synonyms
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: 如何在 Java 中使用 GroupDocs.Search 的 synonyms
type: docs
url: /zh-hant/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 GroupDocs.Search 的同義詞

如果您希望使用者即使輸入不同的詞彙仍能找到正確的內容，**search with synonyms**就是答案。在本指南中，您將學習如何建立同義詞字典、匯入或匯出它、管理同義詞群組，並執行自動使用這些同義詞擴展查詢的搜尋。無論您是在建構 CMS、電子商務目錄，或是法律文件庫，加入同義詞支援都能顯著提升相關性與轉換率。

## 快速答案
- **添加同義詞的第一步是什麼？** 建立 `Index` 實例並使用 `SynonymDictionary` API。  
- **我可以匯入現成的同義詞字典嗎？** 是的 – 呼叫 `importDictionary(path)` 並提供檔案位置。  
- **如何開啟支援同義詞的搜尋？** 啟用 `SearchOptions.setUseSynonymSearch(true)`。  
- **是否可以在執行時編輯同義詞群組？** 當然可以 – 您可以透過字典 API 清除、加入或取得群組。  
- **在擴充索引時應該監控什麼？** 定期清除未使用的條目，並針對大型同義詞檔案調整 JVM 堆積大小。

## 什麼是 search with synonyms？
**Search with synonyms** 意味著引擎將一組詞彙或片語視為可互換。當使用者輸入 **“better”** 時，引擎也會搜尋 **“improve”**、**“enhance”** 或您在同一同義詞群組中定義的任何其他詞彙，提供更豐富的結果而不改變使用者的查詢。

## 為什麼在 GroupDocs.Search 中啟用同義詞支援？
啟用同義詞支援可讓引擎自動擴展查詢，包含等價的詞彙，從而提升結果相關性、增加使用者滿意度，並有助於提升電子商務或內容導向網站的轉換率。它同時集中管理術語，減少跨多個應用程式的維護負擔。

## 前置條件
- GroupDocs.Search for Java 版本 **25.4** 或更新。  
- 具備 Maven 支援的 Java IDE（IntelliJ IDEA、Eclipse 等）。  
- 基本的 Java 知識以及熟悉 Maven 專案結構。

### 必要的函式庫與版本
- GroupDocs.Search for Java **25.4** 或以上。

### 環境設定
- 您選擇的 IDE（IntelliJ IDEA、Eclipse 等）。  
- Maven 用於相依性管理。

### 知識需求
- Java 的物件導向程式設計。  
- 基本的檔案 I/O 操作。

## 設定 GroupDocs.Search for Java

### 安裝資訊
將儲存庫與相依性加入您的 `pom.xml`：

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

**直接下載** – 您也可以從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR。

### 取得授權
- **免費試用**：在未取得授權的情況下測試核心功能。  
- **臨時授權**：在評估期間延長試用功能。  
- **購買**：生產環境使用及完整功能集所必需。

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

### 功能 1：建立與索引索引
`Index` 類別代表儲存在磁碟或記憶體中的可搜尋文件集合。  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### 功能 2：取得單字的同義詞
`SynonymDictionary` 管理同義詞群組，並提供查詢詞彙同義詞的方法。  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### 功能 3：取得同義詞群組
`SynonymDictionary.getGroups()` 會回傳所有已定義同義詞群組及其識別碼的列表。  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### 功能 4：管理同義詞字典條目
`add(word, synonym)` 將新的同義詞關係插入字典。`clear()` 會移除所有條目，`remove(word)` 則刪除字典中特定的詞彙。  

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
`exportDictionary(path)` 將目前的同義詞字典寫入指定位置的二進位 .dat 檔案。  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### 功能 6：從檔案匯入同義詞
`importDictionary(path)` 會載入先前匯出的 .dat 檔案至同義詞字典。  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### 功能 7：執行支援同義詞的搜尋
`SearchOptions` 設定查詢行為，包括是否啟用同義詞擴展。`setUseSynonymSearch(true)` 為即將執行的查詢開啟同義詞感知搜尋。  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## 如何使用同義詞搜尋
載入您的 `Index`，啟用同義詞搜尋，並執行查詢。引擎會自動使用您建立或匯入的同義詞字典擴展查詢，回傳所有相關詞彙的匹配結果。

## 如何匯入同義詞字典
如果您已經有其他環境準備好的 `.dat` 檔案，只需呼叫 `importDictionary(path)`。這非常適合在開發、測試與生產伺服器之間同步字典。

## 如何管理同義詞群組
同義詞群組讓您將一組詞彙視為單一邏輯實體。加入、清除或取得群組皆透過 `SynonymDictionary` API 完成，如上方程式碼片段所示。

## 如何最佳化搜尋索引
- **定期清除未使用的條目**：在大量更新前使用 `clear()`。  
- **調整 JVM 堆積**：大型字典可能需要更多記憶體，請相應增加 `-Xmx` 參數。  
- **保持函式庫為最新**：新版本包含效能提升與錯誤修正。

## 實務應用
1. **內容管理系統 (CMS)：** 使用者即使使用替代術語也能找到文章。  
2. **電子商務平台：** 產品搜尋能容忍同義詞，例如 “laptop” 與 “notebook”。  
3. **文件庫：** 法律或醫療檔案可受益於領域特定的同義詞群組，提升專業人員的可發現性。

## 效能考量
- **最佳化索引儲存**：定期重建索引以移除過時資料。  
- **管理記憶體使用**：載入大型同義詞檔案時監控堆積消耗；500 MB 的字典通常需要在 64 位元 JVM 上配置 2 GB 堆積。  
- **定期更新**：使用最新的 GroupDocs.Search 版本以獲得錯誤修正與效能提升。

## 常見問題與解決方案

| 問題 | 可能原因 | 解決方案 |
|-------|--------------|-----|
| 未出現同義詞匹配 | `setUseSynonymSearch(true)` 未設定或字典未匯入 | 確認已啟用此選項且字典檔案存在。 |
| 匯入期間發生記憶體不足錯誤 | 非常大的 `.dat` 檔案超出 JVM 堆積 | 增加 `-Xmx` 堆積大小或分批匯入較小檔案。 |
| 結果中出現重複條目 | 相同詞彙出現在多個同義詞群組中 | 使用 `clear()` 後再 `addRange()` 合併重疊的群組。 |

## 常見問答

**Q: 使用 GroupDocs.Search 的最低系統需求是什麼？**  
A: 任何具備相容 JDK（Java 8 或更新版）的現代作業系統皆可。

**Q: 我應該多久刷新一次同義詞字典？**  
A: 每當有新術語出現時即更新——使用 `clear()` 後接 `addRange()` 進行全新刷新。

**Q: 我可以在未購買授權的情況下執行 GroupDocs.Search 嗎？**  
A: 免費試用可用於評估，但生產環境部署需要授權。

**Q: 索引大型資料集的最佳實踐是什麼？**  
A: 將資料分割成邏輯批次，監控堆積使用，並安排定期的索引維護。

**Q: 我未看到預期的同義詞匹配——應該檢查什麼？**  
A: 確認字典已正確匯入、`setUseSynonymSearch(true)` 已啟用，且詞彙已存在於同義詞群組中。

**資源**  
- [文件說明](https://docs.groupdocs.com/search/java/)  
- [API 參考](https://reference.groupdocs.com/search/java)  
- [下載 GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- [GitHub 儲存庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)  
- [取得臨時授權](https://purchase.groupdocs.com/temporary-license/) 

---

**最後更新：** 2026-10-17  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs

## 相關教學

- [建立與管理 Groupdocs Search Java 索引](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Java 全文搜尋庫 – 使用 GroupDocs.Search 最佳化索引](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Java 模糊搜尋：使用 GroupDocs.Search 將文件加入索引](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}