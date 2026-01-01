---
date: '2025-12-20'
description: 學習如何在 Java 中使用 GroupDocs.Search 啟用拼寫校正、將文件加入索引，並設定最大錯誤數以提升搜尋準確度。
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: 如何在 Java 中使用 GroupDocs.Search 啟用拼寫功能
type: docs
url: /zh-hant/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Search 啟用拼寫校正

精確的搜尋結果對任何現代應用程式都至關重要。在本教學中，您將學習 **啟用拼寫** 校正在 Java 中使用 GroupDocs.Search，讓使用者即使輸入錯字也能得到正確的結果。我們將逐步說明建立索引、 **將文件加入索引**、設定拼寫選項，以及執行自動校正錯誤的搜尋。

## 快速解答
- **「啟用拼寫」是什麼意思？** 它會啟動內建的拼寫檢查器，在搜尋過程中校正使用者的錯字。  
- **哪個函式庫提供此功能？** GroupDocs.Search for Java。  
- **我需要授權嗎？** 免費試用授權可用於評估；正式環境需購買正式授權。  
- **我可以控制容錯程度嗎？** 可以 – 使用 `setMaxMistakeCount` 來定義允許的錯字數量。  
- **它適用於大型索引嗎？** 當然 – 引擎已針對高效能的索引與搜尋進行最佳化。

## 在 GroupDocs.Search 中「啟用拼寫」是什麼？
啟用拼寫會指示搜尋引擎在查詢包含錯誤時，尋找最接近的正確詞彙。此功能能顯著提升使用者體驗，即使輸入錯字也能返回相關結果。

## 為何在 Java 應用程式中啟用拼寫校正？
- **提升使用者滿意度** – 使用者不必輸入完全正確的文字。  
- **降低跳出率** – 更精確的結果能讓訪客持續參與。  
- **適用於各種領域** – 從圖書館目錄到電子商務商品搜尋皆可。

## 前置條件
- 已安裝 Java Development Kit (JDK)。  
- 具備基本的 Java 與 Maven 知識。  
- 了解索引概念。  
- 具備 GroupDocs.Search 試用或授權金鑰。

### 設定 GroupDocs.Search for Java
將函式庫整合至您的 Maven 專案中。

**Maven 設定**  
將儲存庫與相依性加入您的 `pom.xml` 檔案：

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
取得免費試用授權以進行評估。正式環境使用時，請購買正式授權或向官方網站申請臨時金鑰。

## 如何將文件加入索引
建立索引是任何具備搜尋功能的應用程式的基礎。以下是一個最小範例，示範如何從資料夾 **將文件加入索引**。

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

*提示:* 請確認路徑正確，且應用程式對索引資料夾具有寫入權限。

## 如何設定拼寫校正（設定最大錯字數）
您可以透過啟用拼寫檢查器並設定錯誤容忍度來微調校正行為。

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

*為何 `setMaxMistakeCount` 重要:* 它定義引擎可容忍的錯字數量。請根據您的領域常見的錯誤模式調整此值。

## 如何執行拼寫校正的搜尋
索引已就緒且拼寫選項已設定後，執行可能包含錯字的查詢。

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

`search()` 呼叫會回傳一個 `SearchResult`，其中包含校正後的詞彙以及最相關的文件。

## 實務應用
1. **圖書館系統：** 校正錯誤的書名或作者姓名。  
2. **電子商務平台：** 修正使用者在商品搜尋中的錯字，以提升轉換率。  
3. **內容管理系統：** 提升編輯人員的文章檢索效率。

## 效能考量
- **保持索引即時更新** – 定期重新索引新檔案或已變更的檔案。  
- **調整 JVM 記憶體設定** – 為大型索引分配足夠的堆積記憶體。  
- **監控資源使用情況** – 如有需要，調整垃圾回收器參數。

## 常見問與答

**Q: 什麼是 GroupDocs.Search？**  
A: 它是一個 Java 函式庫，提供快速索引、進階搜尋功能，以及內建的拼寫校正。

**Q: 如何取得 GroupDocs.Search 的授權？**  
A: 前往官方網站下載免費試用或購買正式授權。

**Q: 我可以將 GroupDocs.Search 整合至其他 Java 框架嗎？**  
A: 可以，它可與 Spring、Jakarta EE 以及任何標準的 Java 應用程式一起使用。

**Q: 設定索引時常見的問題是什麼？**  
A: 資料夾路徑不正確、檔案權限不足，或 `pom.xml` 中缺少相依性。

**Q: 拼寫校正如何提升搜尋結果？**  
A: 它會自動將錯字查詢重新寫成最接近的正確詞彙，返回更相關的結果。

## 其他資源
- [文件說明](https://docs.groupdocs.com/search/java/)
- [API 參考文件](https://reference.groupdocs.com/search/java)
- [下載](https://releases.groupdocs.com/search/java/)
- [GitHub 程式庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2025-12-20  
**測試版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs