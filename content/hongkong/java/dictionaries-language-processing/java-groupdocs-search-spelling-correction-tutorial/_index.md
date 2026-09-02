---
date: '2026-09-02'
description: 了解如何使用 GroupDocs.Search 建立 search index java 並啟用拼寫校正。按照步驟說明新增文件、設定 max
  mistake count，提升 search accuracy。
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: 了解如何使用 GroupDocs.Search 建立 search index java 並啟用拼寫校正。按照步驟說明新增文件、設定
  max mistake count，提升 search accuracy。
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: 如何建立 search index java 並啟用拼寫校正
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: 如何建立 search index java 並啟用拼寫校正
type: docs
url: /zh-hant/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# 如何在 Java 中建立搜尋索引並啟用拼寫校正

在現代 Java 應用程式中，提供精確的搜尋結果是必備功能。本教學示範 **如何在 Java 中建立搜尋索引** 並使用 GroupDocs.Search 開啟拼寫校正，讓使用者即使輸入錯字也能收到相關結果。您將會看到如何設定函式庫、加入文件、配置最大錯誤數量，並執行容錯搜尋——全部不需額外撰寫任何設定程式碼。

## 快速解答
- **「啟用拼寫」的作用是什麼？** 它會啟動內建的拼寫檢查器，於搜尋時將錯拼的詞彙重新寫成最接近的正確形式。  
- **哪個函式庫提供此功能？** GroupDocs.Search for Java。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買完整授權。  
- **我可以控制容錯程度嗎？** 可以——使用 `setMaxMistakeCount` 來定義每個查詢允許的錯字數量。  
- **它適用於大型索引嗎？** 完全適用——引擎可處理數百萬筆記錄的索引，且在一般伺服器硬體上查詢延遲保持在 100 ms 以下。

## GroupDocs.Search 是什麼？
GroupDocs.Search 是一套 Java 函式庫，提供快速的全文索引與進階搜尋功能，包含內建的拼寫校正。它支援超過 50 種輸入格式，且能在不將整個檔案載入記憶體的情況下處理數百頁的文件。

## 為何在 Java 應用程式中啟用拼寫校正？
- **提升使用者滿意度** – 即使輸入不完整，訪客仍能取得正確結果。  
- **降低跳出率** – 精準的搜尋結果讓使用者停留更久。  
- **跨領域適用** – 從圖書館目錄到電商商品搜尋，拼寫校正皆能提升相關性。

## 前置條件
- 已安裝 Java Development Kit（JDK）。  
- 具備基本的 Java 與 Maven 知識。  
- 了解索引概念。  
- 具備 GroupDocs.Search 試用或授權金鑰。

### 設定 GroupDocs.Search for Java
將函式庫整合至您的 Maven 專案中。

**Maven 設定**  
將以下儲存庫與相依性加入您的 `pom.xml` 檔案：

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

**直接下載**  
或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權
取得免費試用授權以供評估。正式環境使用時，需購買完整授權或向官方網站申請臨時金鑰。

## 如何在 Java 中建立搜尋索引？
`SearchIndex` 是代表儲存在磁碟上的可搜尋索引的主要類別。  
建立指向磁碟資料夾的 `SearchIndex` 實例，然後從來源目錄加入文件。引擎會建構倒排索引以提供快速查詢。您可以對每個檔案呼叫 `index.add()`；函式庫會根據檔案類型自動擷取文字。

## 如何啟用拼寫校正？
`getSpellingOptions()` 會回傳索引的拼寫設定物件，讓您能啟用或微調拼寫檢查功能。  
透過呼叫 `index.getSpellingOptions().setEnabled(true)` 來啟用拼寫校正。此設定會指示引擎分析查詢詞彙，並在偵測到不匹配時提供校正建議。此功能對函式庫支援的所有已索引語言皆即時可用。

## 最大錯誤數量設定是什麼？
`setMaxMistakeCount` 設定拼寫檢查器每個詞彙可容忍的最大字元編輯次數。  
`setMaxMistakeCount(int)` 定義拼寫檢查器每個詞彙可容忍的最大字元編輯（插入、刪除、取代）次數。將其設定為 **2**，即可讓引擎修正常見的兩字元錯字，同時避免過度積極的校正導致不相關的結果。

## 如何執行拼寫校正搜尋
`search()` 會對索引執行查詢，並回傳包含匹配結果與任何校正詞彙的 `SearchResult` 物件。  
使用 `search()` 方法執行搜尋查詢。若查詢包含錯字，引擎會回傳包含校正詞彙與最相關文件清單的 `SearchResult`。您可以同時向使用者顯示原始查詢與校正後的版本，以提升透明度。  
`SearchResult` 保存匹配文件的清單以及查詢校正的相關資訊。

## 實務應用
1. **圖書館系統** – 自動修正錯拼的書名或作者姓名。  
2. **電商平台** – 校正商品名稱錯字，以提升轉換率。  
3. **內容管理** – 協助編輯人員即使關鍵字不完整亦能找到文章。

## 效能考量
- **保持索引即時更新** – 定期重新索引新檔或已變更的檔案。  
- **調整 JVM 記憶體設定** – 為大型索引分配足夠的堆積記憶體（例如 `-Xmx4g`）。  
- **監控資源使用情況** – 若在大量索引時發現暫停，可調整垃圾回收器參數。

## 常見問題與除錯
| 症狀 | 可能原因 | 解決方案 |
|---------|--------------|-----|
| 啟用拼寫後無結果 | 索引資料夾路徑錯誤或為空 | 確認 `indexFolder` 指向有效的索引且 `index.add()` 已成功執行 |
| 拼寫檢查器未校正明顯錯字 | `setMaxMistakeCount` 設定過低 | 將數量提升至 2 或 3，以獲得更寬容的校正 |
| 應用程式在大型文件集上當機 | JVM 堆積不足 | 增加 `-Xmx` 參數（例如 `-Xmx4g`） |

## 常見問答

**Q: 什麼是 GroupDocs.Search？**  
A: GroupDocs.Search 是一套 Java 函式庫，提供快速索引、進階查詢功能，並為任何 Java 應用程式內建拼寫校正。

**Q: 如何取得 GroupDocs.Search 的授權？**  
A: 前往官方網站下載免費試用或購買完整授權；亦可取得臨時金鑰以進行短期測試。

**Q: 我可以將 GroupDocs.Search 整合至其他 Java 框架嗎？**  
A: 可以，它能無縫搭配 Spring、Jakarta EE 以及任何標準的 Java 應用程式。

**Q: 設定索引時常見的問題是什麼？**  
A: 常見原因包括資料夾路徑錯誤、檔案權限不足，或缺少 Maven 相依性。

**Q: 拼寫校正如何提升搜尋結果？**  
A: 它會自動將錯拼的查詢重新寫成最接近的正確詞彙，返回更相關的結果，減少使用者的挫折感。

## 其他資源
- [文件說明](https://docs.groupdocs.com/search/java/)
- [API 參考](https://reference.groupdocs.com/search/java)
- [下載](https://releases.groupdocs.com/search/java/)
- [GitHub 程式庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-09-02  
**測試版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## 相關教學

- [如何使用 GroupDocs.Search API for Java 建立文件索引並加入文件](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Java 語言處理 – 使用 GroupDocs.Search 建立同義詞字典](/search/java/dictionaries-language-processing/)
- [搜尋中的停用詞：使用 GroupDocs.Search Java 將文件加入索引](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)