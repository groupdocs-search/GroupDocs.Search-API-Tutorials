---
date: '2026-03-20'
description: 學習如何在 Java 中使用 GroupDocs.Search 啟用模糊搜尋，設定步驟函式，將文件加入索引，並遵循模糊搜尋的最佳實踐。
keywords:
- fuzzy search in Java
- GroupDocs.Search for Java
- implement fuzzy search with GroupDocs
title: 在 Java 中使用 GroupDocs.Search 啟用模糊搜尋 – 全面指南
type: docs
url: /zh-hant/java/searching/master-fuzzy-search-java-groupdocs/
weight: 1
---

# 在 Java 中使用 GroupDocs.Search 啟用模糊搜尋

在現代應用程式中，用戶期望搜尋功能能*容忍*拼寫錯誤、打字錯誤及輕微變化。學會如何在 Java 中使用 GroupDocs.Search **啟用模糊搜尋**，即可為用戶提供更流暢、更寬容的體驗，同時保持結果的準確與快速。

## 介紹
在當今的數位時代，快速且精確的資訊存取至關重要。用戶在搜尋文件時常會遇到輕微的拼寫錯誤或打字錯誤。傳統的完全匹配搜尋在此類情況下可能無法滿足需求。本教學將向您介紹 GroupDocs.Search for Java——一個強大的函式庫，為您的應用程式提供模糊搜尋功能。透過運用模糊演算法，您可以在文字檢索上獲得更大的彈性與準確度。

**您將學會：**
- 如何使用指定的相似度等級設定模糊搜尋。
- 為不同字長的模糊搜尋設定步驟函式。
- 在 Java 應用程式中實作 GroupDocs.Search 的實用範例。
- 使用模糊演算法優化效能的最佳實踐。

## 快速解答
- **「啟用模糊搜尋」是什麼意思？** 它會在查詢處理時容忍拼寫錯誤。  
- **哪個函式庫提供此功能？** GroupDocs.Search for Java。  
- **我需要授權嗎？** 提供免費試用；商業授權則需於正式環境使用。  
- **我可以自訂錯誤容忍度嗎？** 可以——透過相似度等級或步驟函式設定。  
- **是否相容於 Java 8+？** 完全相容，可在 JDK 8 及以上版本執行。

## 為何使用 GroupDocs.Search 啟用模糊搜尋？
模糊搜尋彌合了使用者意圖與精確文字之間的差距。它在以下情境中特別有價值：  
- **文件管理系統**：檔案名稱或內容可能出現人工錯誤。  
- **電子商務網站**：購物者常會打錯商品名稱。  
- **內容管理系統**：服務多元使用者群體，打字習慣各異。  

啟用模糊搜尋可減少「無結果」的挫折感，提升整體使用者滿意度。

## 前置條件
在實作模糊搜尋之前，請確保您已具備以下條件：

### 必要的函式庫與相依性
透過 Maven 或直接下載方式整合 GroupDocs.Search for Java。對於 Maven 使用者，請在 `pom.xml` 檔案中加入以下設定：
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
或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 環境設定
確保開發環境已安裝 JDK 8 或更新版本，並準備好 IntelliJ IDEA 或 Eclipse 等 IDE。

### 知識前置條件
具備 Java 程式設計的基本概念並熟悉 Maven 專案設定將有助於學習。曾有搜尋演算法經驗者更佳，但非必要。

## 設定 GroupDocs.Search for Java
要開始使用 GroupDocs.Search for Java，請依照以下步驟：

### 透過 Maven 或直接下載安裝
若使用 Maven，請參考上述的相依程式碼片段。若直接下載，請前往 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 取得 JAR 檔並整合至您的專案中。

### 取得授權
- **免費試用**：先使用 30 天免費試用，以探索 GroupDocs 功能。  
- **臨時授權**：可於官方網站申請臨時授權，以延長評估期間。  
- **購買**：商業使用時請考慮購買授權。詳情請參閱 [GroupDocs Licensing](https://purchase.groupdocs.com/temporary-license/)。

### 基本初始化
建立索引目錄以儲存可搜尋的資料：
```java
import com.groupdocs.search.Index;
Index index = new Index("path_to_your_index_directory");
```
這是設定搜尋環境的第一步，之後即可進一步自訂與索引文件。

## 實作指南

### 功能 1：使用相似度等級設定模糊搜尋演算法

#### 如何使用相似度等級啟用模糊搜尋
透過指定相似度等級來啟用模糊搜尋，以容納搜尋時的輕微拼寫錯誤或變化。當在大型資料集搜尋且精確匹配稀少時，此功能可提升使用者體驗。
```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

// Create an index in the specified folder
dIndex index = new Index("YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Searching/FuzzySearch/SettingFuzzySearchAlgorithm");

// Add documents to be indexed\index.add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");

// Configure fuzzy search options
SearchOptions options = new SearchOptions();
options.getFuzzySearch().setEnabled(true); // Enable fuzzy search
options.getFuzzySearch().setFuzzyAlgorithm(new SimilarityLevel(0.8)); // Set similarity level

// Execute the search with configured options
String query = "nulla";
SearchResult result = index.search(query, options);
```
**說明：**  
- **相似度等級 (0.8)**：允許搜尋查詢最多 20 % 的變化。  
- **參數**：`setEnabled(true)` 會啟用模糊搜尋；`setFuzzyAlgorithm(new SimilarityLevel(0.8))` 設定容忍度。

#### 疑難排解提示
- 確認索引路徑指向可寫入的資料夾。  
- 確認在執行查詢前已 **add documents to index** 文件。

### 功能 2：為模糊搜尋演算法設定步驟函式

#### 如何為模糊搜尋設定步驟函式
步驟函式允許您根據字長定義不同的錯誤容忍度，從而精細控制模糊行為。
```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

// Create an index in the specified folder
dIndex index = new Index("YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Searching/FuzzySearch/SettingStepFunction");

// Add documents to be indexed\index.add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");

// Configure fuzzy search options using step functions
SearchOptions options = new SearchOptions();
options.getFuzzySearch().setEnabled(true); // Enable fuzzy search

// Define the step function for different word lengths
options.getFuzzySearch().setFuzzyAlgorithm(new TableDiscreteFunction(1,
    new Step(5, 2),
    new Step(8, 3)));

// Execute the search with configured options
String query = "nulla";
SearchResult result = index.search(query, options);
```
**說明：**  
- **步驟函式**：依字長定義錯誤容忍度：  
  - 1‑4 個字元的詞 → 最多 1 個錯誤。  
  - 5‑7 個字元的詞 → 最多 2 個錯誤。  
  - 8 個以上字元的詞 → 最多 3 個錯誤。

#### 疑難排解提示
- 再次確認步驟參數是否符合資料集的特性。  
- 嘗試不同設定，以在準確度與效能之間取得平衡。

## 實務應用
1. **文件管理系統** – 透過實作模糊搜尋提升 CRM 或 ERP 系統的搜尋功能，改善在大量客戶資訊資料庫中的使用者體驗。  
2. **電子商務平台** – 讓購物者即使拼錯商品名稱或描述仍能找到商品。  
3. **內容管理系統 (CMS)** – 提升網站或內部網路的內容搜尋準確度與彈性，容納使用者多樣的輸入方式。

## 效能考量

### 優化效能的技巧
- 定期更新索引，使其與來源資料保持同步。  
- 在索引前將極大的文件切割成較小的片段，以減少記憶體壓力。

### 資源使用指引
在大量搜尋操作期間監控記憶體與 CPU 使用情況。如發現垃圾回收暫停過長，請調整 Java 堆積設定。

### 模糊搜尋的最佳實踐
- **從中等相似度等級（例如 0.8）開始**，並根據實際查詢日誌進行調整。  
- **將模糊搜尋與篩選條件**（日期範圍、類別）結合，以保持結果集的相關性。  
- **在語料樣本上分析步驟函式**，找出召回率與精確度之間的最佳平衡點。

## 常見問題與解決方案

| 問題 | 可能原因 | 解決方案 |
|-------|--------------|----------|
| 未返回結果 | 索引為空或文件未 **add documents to index** | 確保在搜尋前對每個來源檔案呼叫 `index.add(...)`。 |
| 查詢回應緩慢 | 相似度等級或步驟函式過於寬鬆 | 降低容忍度或使用非模糊條件先行篩選結果。 |
| 記憶體使用過高 | 整個大型索引全部載入記憶體 | 使用支援磁碟儲存的 `Index` 建構子重載，或增加堆積大小。 |

## 常見問答

**Q: 我該如何在現有專案中 **implement fuzzy search java**？**  
A: 加入 Maven 相依性，初始化 `Index`，透過 `SearchOptions` 啟用模糊搜尋，然後如程式範例所示呼叫 `index.search()`。

**Q: 我可以在初始建置後 **add documents to index** 嗎？**  
A: 可以——隨時呼叫 `index.add(...)`，然後重新執行 `index.save()` 以保存變更。

**Q: **similarity level** 與 **step function** 有何不同？**  
A: 相似度等級在所有詞彙上套用統一的容忍度，而步驟函式則可依字長變化容忍度。

**Q: 有關大型資料集的 **best practices fuzzy search** 推薦嗎？**  
A: 使用步驟函式限制短詞的錯誤數量，保持索引最佳化，並將模糊查詢與其他篩選條件結合。

**Q: 啟用模糊搜尋會影響索引速度嗎？**  
A: 索引速度不受影響，模糊設定僅影響查詢執行。

## 結論
您現在已學會如何在 Java 中使用 GroupDocs.Search **啟用模糊搜尋**，以及如何透過相似度等級與步驟函式進行微調，並套用效能與準確度的最佳實踐。將這些技術整合至您的應用程式，即可提供更智慧、更寬容的搜尋體驗。

---

**最後更新：** 2026-03-20  
**測試版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs