---
date: '2026-02-24'
description: 學習如何使用 GroupDocs.Search 以屬性 Java 進行搜尋。本指南示範批次更新文件屬性，並於索引時新增與修改屬性。
keywords:
- GroupDocs.Search Java
- document attribute modification
- Java indexing techniques
title: 使用 GroupDocs.Search 的 Java 屬性搜尋指南
type: docs
url: /zh-hant/java/document-management/groupdocs-search-java-modify-attributes-indexing/
weight: 1
---

# Search by Attribute Java with GroupDocs.Search 指南

您是否希望透過 Java 動態修改與索引文件屬性，以提升文件管理系統？您來對地方了！本教學深入探討如何運用功能強大的 GroupDocs.Search for Java 函式庫來 **search by attribute java**、變更已索引的文件屬性，並在索引過程中加入屬性。無論您是構建可搜尋的入口網站、合規存檔系統，或是智慧內容驅動的應用程式，掌握這些技巧都能為您節省時間並提升效能。

## Quick Answers
- **什麼是 “search by attribute java”？** 它是使用附加於每個文件的自訂中繼資料來篩選搜尋結果的能力。  
- **索引後我可以修改屬性嗎？** 可以 — 使用 `AttributeChangeBatch` 以批次方式更新文件屬性。  
- **在索引時如何加入屬性？** 訂閱 `FileIndexing` 事件，並以程式方式設定屬性。  
- **我需要授權嗎？** 免費試用版可用於評估；正式環境需購買永久授權。  
- **需要哪個版本的 Java？** 建議使用 Java 8 或更新版本。

## 什麼是 “search by attribute java”？
**Search by attribute java** 讓您能根據文件的中繼資料（屬性）而非僅內容來查詢文件。透過將 `public`、`main` 或 `key` 等鍵值對附加於每個檔案，即可快速將結果縮小至最相關的子集。

## 為何使用動態中繼資料標記？
- **動態分類** – 讓中繼資料與不斷變化的業務規則保持同步。  
- **更快的篩選** – 屬性過濾在全文搜尋之前執行，可提升回應速度。  
- **合規追蹤** – 為文件加上保留政策或稽核需求的標記。  
- **批次更新屬性** – 一次操作即可變更多個文件，而無需重新索引全部。

## 前置條件

- **Java 8+**（JDK 8 或更新版本）  
- **GroupDocs.Search for Java** 函式庫（請參閱下方 Maven 設定）  
- 具備 Java 與索引概念的基本認識  

## 設定 GroupDocs.Search for Java

### Maven 設定

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

或者，從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。  
如果您不想使用 Maven 等建置工具，可從 [GroupDocs website](https://releases.groupdocs.com/search/java/) 下載 JAR。

### 取得授權

- 先使用免費試用版以探索功能。  
- 若需長期使用，請透過 [license page](https://purchase.groupdocs.com/temporary-license) 取得臨時或正式授權。

### 基本初始化

```java
import com.groupdocs.search.Index;

// Initialize an index in a specified directory
Index index = new Index("YOUR_OUTPUT_DIRECTORY/ChangeAttributes");
```

## 如何修改文件屬性（批次更新）

### Search by Attribute Java – 變更文件屬性

您可以在已索引的文件上新增、移除或取代屬性，從而在不重新索引整個集合的情況下實現 **batch update document attributes**。

### 步驟說明

**步驟 1：將文件加入索引**  

```java
index.add("YOUR_DOCUMENT_DIRECTORY");
```

**步驟 2：取得已索引文件資訊**  

```java
import com.groupdocs.search.results.DocumentInfo;

DocumentInfo[] documents = index.getIndexedDocuments();
```

**步驟 3：批次更新文件屬性**  

```java
import com.groupdocs.search.common.AttributeChangeBatch;
import com.groupdocs.search.SearchOptions;

AttributeChangeBatch batch = new AttributeChangeBatch();
batch.addToAll("public"); // Add 'public' to all documents
batch.remove(documents[0].getFilePath(), "public"); // Remove 'public' from a specific document
batch.add(documents[0].getFilePath(), "main", "key"); // Add 'main' and 'key' attributes

// Apply changes
index.changeAttributes(batch);
```

**步驟 4：使用屬性過濾搜尋**  

```java
import com.groupdocs.search.results.SearchResult;

SearchOptions options = new SearchOptions();
options.setSearchDocumentFilter(SearchDocumentFilter.createAttribute("main"));
String query = "length";
SearchResult result = index.search(query, options); // Perform the search
```

### 使用 AttributeChangeBatch 進行批次更新文件屬性
`AttributeChangeBatch` 類別是執行 **batch update document attributes** 的核心工具。將變更彙總為單一批次，可減少 I/O 開銷並保持索引一致性。

## 如何在索引過程中加入屬性

### Search by Attribute Java – 索引時加入屬性

透過掛接 `FileIndexing` 事件，在每個檔案加入索引時指派自訂屬性。

### 步驟說明

**步驟 1：訂閱 FileIndexing 事件**  

```java
import com.groupdocs.search.events.EventHandler;
import com.groupdocs.search.events.FileIndexingEventArgs;

index.getEvents().FileIndexing.add(new EventHandler<FileIndexingEventArgs>() {
    @Override
    public void invoke(Object sender, FileIndexingEventArgs args) {
        if (args.getDocumentFullPath().endsWith("Lorem ipsum.pdf")) {
            args.setAttributes(new String[] { "main", "key" });
        }
    }
});
```

**步驟 2：索引文件**  

```java
index.add("YOUR_DOCUMENT_DIRECTORY");
```

## 實務應用

1. **文件管理系統** – 在匯入過程中加入中繼資料，以自動化分類。  
2. **大型內容檔案庫** – 使用屬性過濾縮小搜尋範圍，顯著縮短回應時間。  
3. **合規與報告** – 動態為文件加上保留排程或稽核追蹤的標記。  

## 效能考量

- **記憶體管理** – 監控 JVM 堆積，並根據需要調整 `-Xmx`。  
- **批次處理** – 使用 `AttributeChangeBatch` 將屬性變更分組，以減少索引寫入次數。  
- **函式庫更新** – 保持 GroupDocs.Search 為最新版本，以獲得效能修補。  

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方法 |
|-------|----------------|------------|
| **屬性未套用** | 索引前未註冊事件處理程式 | 確保在呼叫 `index.add(...)` 之前先執行 `index.getEvents().FileIndexing.add(...)`。 |
| **搜尋未返回結果** | 屬性名稱不匹配（區分大小寫） | 建立過濾條件時使用完全相同的屬性名稱（例如 `createAttribute("main")`）。 |
| **大量批次導致記憶體不足** | 單一批次變更過多 | 將大型更新拆分為較小的 `AttributeChangeBatch` 實例。 |
| **授權未被識別** | 使用試用版 JAR 卻未套用授權檔案 | 在任何索引操作之前呼叫 `License license = new License(); license.setLicense("path/to/license.file");`。 |

## 常見問答

**Q: 使用 GroupDocs.Search for Java 的前置條件是什麼？**  
A: 您需要 Java 8+、GroupDocs.Search 函式庫，以及索引概念的基本知識。

**Q: 如何透過 Maven 安裝 GroupDocs.Search？**  
A: 在 `pom.xml` 中加入 Maven 設定段落所示的儲存庫與相依性。

**Q: 文件索引後我可以修改屬性嗎？**  
A: 可以，使用 `AttributeChangeBatch` 以批次方式更新文件屬性，無需重新索引。

**Q: 如果我的索引過程很慢該怎麼辦？**  
A: 優化 JVM 記憶體設定、使用批次更新，並確保使用最新版本的函式庫。

**Q: 我可以在哪裡找到更多關於 GroupDocs.Search for Java 的資源？**  
A: 前往 [official documentation](https://docs.groupdocs.com/search/java/) 或參與社群論壇。

## 資源

- 文件說明： [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)
- API 參考： [API Reference](https://reference.groupdocs.com/search/java)
- 下載： [Latest Releases](https://releases.groupdocs.com/search/java/)
- GitHub： [GitHub GroupDocs.Search](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- 免費支援論壇： [GroupDocs Forums](https://forum.groupdocs.com/c/search/10)
- 臨時授權： [License Page](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-02-24  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs