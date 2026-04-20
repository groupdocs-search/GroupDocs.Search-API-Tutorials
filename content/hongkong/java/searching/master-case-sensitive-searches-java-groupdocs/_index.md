---
date: '2026-02-06'
description: 學習如何在 Java 中使用 GroupDocs.Search 將文件加入索引並啟用大小寫區分搜尋，提升應用程式的準確性。
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 將文件新增至索引：使用 GroupDocs 的區分大小寫 Java 搜尋
type: docs
url: /zh-hant/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# 新增文件至索引：精通 Java 中的大小寫敏感搜尋（使用 GroupDocs）

從龐大的文件集合中檢索正確資訊是現代應用程式的核心需求。在本指南中，您將學習 **如何將文件新增至索引** 以及使用 GroupDocs.Search for Java 執行 **大小寫敏感搜尋**。無論您是構建法律文件庫、電子商務目錄，或是內容管理系統，精確的搜尋結果都能讓使用者滿意，並確保資料的可信度。

## 快速解答
- **開始搜尋的首要步驟是什麼？** 使用 `index.add(...)` 將文件新增至索引。
- **如何啟用大小寫敏感搜尋？** 設定 `options.setUseCaseSensitiveSearch(true)`。
- **我可以跨多個目錄搜尋嗎？** 可以 — 為每個想要納入的資料夾呼叫 `index.add()`。
- **哪個方法允許使用物件進行搜尋？** 使用 `SearchQuery.createWordQuery(...)`。
- **測試是否需要授權？** 可取得臨時授權供試用使用。

## 「將文件新增至索引」是什麼意思？
將文件新增至索引是指將您的來源檔案（PDF、Word 文件、純文字等）輸入至 GroupDocs.Search，讓其建立可搜尋的資料結構。完成索引後，搜尋引擎即可執行快速查詢，包括大小寫敏感的查詢。

## 為什麼在 Java 中啟用大小寫敏感搜尋？
- **精確詞彙匹配** — 區分「Apple」（公司）與「apple」（水果）。  
- **符合法規要求** — 某些產業需要精確片語匹配。  
- **提升相關性** — 使用者在技術或法律情境中常期待大小寫特定的結果。

## 前置條件
- JDK（建議使用 Java 17 或更新版本）  
- Maven（用於相依管理）  
- IDE，例如 IntelliJ IDEA 或 Eclipse  
- 具備基本的 Java 程式設計知識  

## 設定 GroupDocs.Search for Java
First, add the GroupDocs repository and dependency to your `pom.xml`:

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

或者，您也可以直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 授權
若要開始試用，請前往 GroupDocs 取得臨時授權。這樣即可在無限制的情況下測試所有功能。

## 如何將文件新增至索引 — 文字查詢搜尋

### 步驟 1：建立索引並新增文件
建立一個用於存放索引檔案的資料夾，然後加入包含欲搜尋文件的來源目錄。

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **專業提示：** 您可以多次呼叫 `index.add()`，以在單一索引中 **跨多個目錄搜尋**。

### 步驟 2：啟用大小寫敏感搜尋
設定搜尋選項以遵守字母大小寫。

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 步驟 3：執行大小寫敏感的文字查詢
執行一個能區分「Advantages」與「advantages」的查詢。

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

此迴圈會印出每個包含完全相符大小寫詞彙的文件完整路徑。

## 如何將文件新增至索引 — 物件查詢搜尋

物件查詢提供更大的彈性，特別是當您需要結合多個條件時。

### 步驟 1：初始化第二個索引（可選）
如果您希望將基於物件的搜尋分開管理，請建立另一個索引資料夾。

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### 步驟 2：重複使用大小寫敏感選項
相同的 `SearchOptions` 實例同樣適用於物件查詢。

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 步驟 3：建立並執行物件查詢
建立一個字詞查詢物件，並將其傳遞給搜尋引擎。

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

使用 `createWordQuery` 可讓您稍後將其與片語、萬用字元或布林查詢結合，以應對更複雜的情境。

## 實務應用
- **法律文件管理：** 取得在大小寫重要的特定案例法條。  
- **電子商務平台：** 區分如「PRO‑X」與「pro‑x」的商品 SKU。  
- **內容管理系統（CMS）：** 確保作者能找到精確的標題或標籤。

## 效能考量
- **保持索引即時更新** — 當新增檔案或現有檔案變更時重新索引。  
- **監控記憶體使用** — 大型語料庫受惠於增量索引與適當的 JVM 堆積大小設定。  
- **善用 Java 的垃圾回收機制** — 當 `Index` 物件不再需要時釋放它們。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| `useCaseSensitiveSearch` 似乎被忽略 | 請確認您使用的是最新的 GroupDocs.Search 版本，且在變更選項後已重新建立索引。 |
| 已知詞彙未返回結果 | 確保詞彙的大小寫完全匹配，且文件已成功加入索引。 |
| 搜尋大量資料夾導致速度變慢 | 使用 `index.add()` 個別加入每個資料夾，並考慮將索引拆分為多個分片以應對極大型資料集。 |

## 常見問答

**Q:** 我該如何使用 GroupDocs.Search 處理大型資料集？  
**A:** 使用索引分割、調整 JVM 記憶體設定，並定期壓縮索引以維持最佳效能。

**Q:** 我能同時跨多個目錄搜尋嗎？  
**A:** 可以 — 為每個想要納入的目錄呼叫 `index.add()`，然後對合併後的索引執行單一查詢。

**Q:** 設定大小寫敏感搜尋時常見的陷阱是什麼？  
**A:** 啟用 `useCaseSensitiveSearch` 後忘記重新建立索引，或在查詢字串中使用錯誤的大小寫。

**Q:** 我該如何排除搜尋錯誤？  
**A:** 檢查 GroupDocs.Search 產生的日誌檔以取得堆疊追蹤，並確認所有 Maven 相依項目已正確解析。

**Q:** GroupDocs.Search 適用於即時應用程式嗎？  
**A:** 只要採取適當的索引策略（增量更新與記憶體快取），即可提供近即時的搜尋結果。

## 資源
- **文件說明：** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API 參考：** [Java API Reference](https://reference.groupdocs.com/search/java)
- **下載：** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub 程式庫：** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **支援論壇：** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **臨時授權：** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-02-06  
**測試版本：** GroupDocs.Search 25.4  
**作者：** GroupDocs