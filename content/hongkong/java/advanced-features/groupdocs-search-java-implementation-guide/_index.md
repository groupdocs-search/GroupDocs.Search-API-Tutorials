---
date: '2025-12-18'
description: 學習如何使用 GroupDocs.Search for Java 建立文件索引，涵蓋文字提取、序列化以及 Java 全文搜尋功能。
keywords:
- GroupDocs.Search for Java
- document indexing in Java
- text extraction with GroupDocs
title: 使用 GroupDocs.Search for Java 建立文件索引
type: docs
url: /zh-hant/java/advanced-features/groupdocs-search-java-implementation-guide/
weight: 1
---

# 使用 GroupDocs.Search for Java 建立文件索引：完整指南

在當今的數位時代，能夠快速 **create document index** 並高效搜尋，對任何組織而言都是顛覆性的。無論您是構建文件管理系統或自訂搜尋引擎，GroupDocs.Search for Java 都提供了提取文字、序列化資料以及輕鬆執行 full‑text search Java 操作的工具。本教學將逐步說明每個步驟——從提取 PDF 文字到將資料加入索引，再到搜尋已索引的文件。

## 快速解答
- **主要目的為何？** 使用 GroupDocs.Search for Java 建立可搜尋的文件索引。  
- **使用哪個函式庫版本？** GroupDocs.Search 25.4 (or the latest release)。  
- **是否需要授權？** A free trial works for development; a full license is required for production。  
- **可以索引 PDF 嗎？** Yes—extract pdf text and add it to the index。  
- **如何執行搜尋？** Use the `index.search(query)` method after adding data。

## 什麼是文件索引？
文件索引是一個從檔案中提取的可搜尋詞彙的結構化集合。透過建立文件索引，您可以在大型資料庫中快速執行 full‑text searches，顯著提升檢索速度與準確度。

## 為何使用 GroupDocs.Search for Java？
- **強大的抽取** – 支援 PDF、Word、Excel 等多種格式。  
- **簡易序列化** – 將抽取的資料儲存為位元組陣列，以便日後重用。  
- **可擴充的索引** – 高效索引數百萬份文件。  
- **強大的查詢語言** – 支援複雜的 full‑text search Java 查詢。

## 前置條件
- **GroupDocs.Search for Java**（版本 25.4 或更新）。  
- **Java Development Kit (JDK)** 與您的 GroupDocs 版本相容。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 用於相依管理的 Maven。

## 設定 GroupDocs.Search for Java
首先，將函式庫加入您的專案。

**Maven 設定**  
在您的 `pom.xml` 檔案中加入以下內容：

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
或是從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權
- **免費試用** – 使用臨時授權測試所有功能。  
- **購買** – 獲得完整存取權與優先支援。

## 步驟實作

### 如何從 PDF（及其他文件）抽取文字
抽取原始或格式化文字是建立文件索引的第一步。

```java
String documentPath = "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf";
Extractor extractor = new Extractor();
Document document = Document.createFromFile(documentPath);
```

```java
ExtractionOptions extractionOptions = new ExtractionOptions();
extractionOptions.setUseRawTextExtraction(false); // Extract with formatting
ExtractedData extractedData = extractor.extract(document, extractionOptions);
```

> **提示：** 若需要純文字且不含格式，請設定 `setUseRawTextExtraction(true)`。

### 如何序列化抽取的資料
序列化可讓您將抽取的資料儲存起來，以便日後索引。

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
extractedData.serialize(outputStream);
byte[] serializedArray = outputStream.toByteArray();
```

### 如何反序列化抽取的資料
當您準備好建立索引時，將位元組陣列轉回物件。

```java
ByteArrayInputStream inputStream = new ByteArrayInputStream(serializedArray);
ExtractedData deserializedData = ExtractedData.deserialize(inputStream);
```

### 如何建立文件索引
現在您已擁有 `deserializedData`，即可建立用來保存可搜尋詞彙的索引。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/SeparateDataExtraction";
com.groupdocs.search.Index index = new com.groupdocs.search.Index(indexFolder);
```

### 如何將資料加入索引並執行搜尋
將資料加入索引並查詢索引，即完成 **create document index** 工作流程。

```java
ExtractedData[] dataToIndex = new ExtractedData[] { deserializedData };
index.add(dataToIndex, new IndexingOptions());
```

```java
String query = "ipsum";
SearchResult result = index.search(query);
```

> **進階提示：** 使用 `index.search("your query", SearchOptions)` 以微調相關性排名。

## 常見使用情境
1. **文件管理系統** – 快速定位合約、發票或政策文件。  
2. **內容導向搜尋引擎** – 以 full‑text search Java 功能為內部知識庫提供動力。  
3. **資料歸檔解決方案** – 索引歷史紀錄，以即時檢索。

## 效能考量
- **記憶體管理：** 為大量文件批次調整 JVM 堆積大小。  
- **索引選項：** 停用不必要的功能（例如 term vectors）以加速索引。  
- **定期更新：** 保持 GroupDocs.Search 為最新版本，以獲得效能修補。

## 常見問與答

**Q: 如何有效處理非常大的 PDF 檔案？**  
A: 使用 `Extractor` 串流檔案並分塊處理；必要時亦可增加 JVM 堆積。

**Q: 我可以自訂搜尋查詢語法嗎？**  
A: 可以——GroupDocs.Search 支援布林運算子、萬用字元與相近搜尋。

**Q: 若序列化失敗該怎麼辦？**  
A: 確認所有物件皆實作 `Serializable`，並捕捉 `IOException` 以記錄細節。

**Q: 能否只索引文件的特定部分？**  
A: 完全可以——在索引前設定 `ExtractionOptions` 以過濾頁面或章節。

**Q: 如何升級至較新版本的 GroupDocs.Search？**  
A: 在 `pom.xml` 中更新版本號，然後執行 `mvn clean install`；請檢視遷移指南以了解破壞性變更。

## 資源
- **文件說明**: [GroupDocs Documentation](https://docs.groupdocs.com/search/java/)  
- **API 參考**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **下載**: [GroupDocs Downloads](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免費支援**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2025-12-18  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs