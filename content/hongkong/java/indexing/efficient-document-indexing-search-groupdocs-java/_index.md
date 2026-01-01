---
date: '2025-12-29'
description: 了解如何使用 GroupDocs.Search for Java 索引 Java 文件並建立搜尋索引。本指南涵蓋設定、索引、搜尋以及高效管理文件的方式。
keywords:
- GroupDocs.Search Java
- document indexing
- Java document search
title: 如何使用 GroupDocs.Search 索引 Java 文件 – 高效搜尋
type: docs
url: /zh-hant/java/indexing/efficient-document-indexing-search-groupdocs-java/
weight: 1
---

# 使用 GroupDocs.Search 索引 Java 文件 – 高效搜尋

## 介紹

您是否被大量文件淹沒，並想快速了解 **how to index java** 檔案的方式？許多企業與個人每天都面臨此挑戰。**GroupDocs.Search for Java** 提供高效的解決方案，簡化文件搜尋，使過程更快速且更易管理。

在本教學中，我們將指導您如何使用 GroupDocs.Search for Java 建立文件的索引儲存庫。您將學會如何從檔案系統載入文件、執行搜尋、管理刪除，以及高效且可擴展地取得索引資料。

**您將學到的內容：**
- 設定與配置 GroupDocs.Search for Java。  
- **建立搜尋索引** 並從串流索引文件。  
- 從檔案系統載入文件。  
- 在索引上 **執行關鍵字搜尋**。  
- **如何刪除索引** 中特定文件的條目。  
- 刪除後取得剩餘的索引文件。

準備好徹底改變文件搜尋的管理方式了嗎？讓我們先從前置條件開始吧！

## 快速回答
- **主要目的為何？** 高效索引與搜尋 Java 文件。  
- **需要哪個函式庫？** GroupDocs.Search for Java（v25.4 以上）。  
- **需要授權嗎？** 提供免費試用或臨時授權；正式環境需購買永久授權。  
- **可以從索引中刪除文件嗎？** 可以，使用 `delete` 方法搭配文件鍵即可。  
- **Apache Commons IO 必須嗎？** 建議使用，以便處理檔案相關工具。

## 什麼是 “how to index java”？
索引 Java 文件是指建立一個可搜尋的資料結構（索引），將文件內容對應到可搜尋的詞彙，從而能夠根據關鍵字查詢快速取得相關檔案。

## 為何使用 GroupDocs.Search for Java？
- **速度：** 最佳化演算法即使在大型集合上也能快速回傳查詢結果。  
- **可擴展性：** 能處理數千份文件而不影響效能。  
- **彈性：** 支援多種檔案格式，並提供大型檔案的延遲載入。  
- **易於整合：** Maven 設定簡單，API 直觀。

## 前置條件

在開始之前，請確保您具備以下條件：

### 必要的函式庫與相依性
- **GroupDocs.Search for Java**：請確保安裝 25.4 或更新版本。  
- **Apache Commons IO**：用於檔案處理工具。

### 環境設定需求
- Java Development Kit (JDK) 8 以上。  
- IntelliJ IDEA、Eclipse 等整合開發環境 (IDE)。

### 知識前提
- 具備基本的 Java 程式設計與物件導向概念。  
- 熟悉 Maven 相依性管理者佳，但非必須。

## 設定 GroupDocs.Search for Java

使用 Maven 設定專案環境的步驟如下：

**Maven 設定：**  
在 `pom.xml` 中加入以下倉庫與相依性：

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

**直接下載：**  
或是直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權的步驟
- **免費試用：** 先取得免費試用版以測試功能。  
- **臨時授權：** 申請臨時授權以無限制探索全部功能。  
- **購買授權：** 若符合需求，可考慮購買正式授權。

**基本初始化與設定：**  

環境就緒後，使用以下程式碼初始化 GroupDocs.Search：

```java
import com.groupdocs.search.*;

public class DocumentIndexing {
    public static void main(String[] args) {
        Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\DeleteIndexedDocuments");
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## 如何使用 GroupDocs.Search 索引 Java 文件

### 建立與索引文件

**概觀：** 了解如何在指定資料夾建立索引，並從串流加入文件，簡化 **create search index** 的流程。

#### 步驟 1：建立索引
```java
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\DeleteIndexedDocuments", true);
```
- **參數說明：** 第一個參數為索引儲存的目錄路徑；第二個布林值表示若索引已存在則自動更新。

#### 步驟 2：從串流載入並加入文件
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY\\English.docx";
DocumentLoader documentLoader = new DocumentLoader(filePath);
Document document = Document.createLazy(DocumentSourceKind.Stream, documentLoader.getDocumentKey(), documentLoader);
Document[] documents = new Document[]{document};
index.add(documents, new IndexingOptions());
```
- **說明：** 這裡建立 `DocumentLoader` 讀取檔案並為索引作準備。`createLazy` 方法用於有效處理大型檔案。

### 從檔案系統載入文件

**概觀：** 實作自訂載入器，直接使用 Apache Commons IO 工具從檔案系統讀取文件。

#### 步驟 1：定義 Document Loader
```java
class DocumentLoader {
    private final String filePath;
    private final String documentKey;

    public DocumentLoader(String filePath) {
        this.filePath = filePath;
        documentKey = FilenameUtils.getName(filePath);
    }

    public String getDocumentKey() { return documentKey; }

    public Document loadDocument() throws IOException {
        Path path = Paths.get(filePath);
        byte[] buffer = Files.readAllBytes(path);
        ByteArrayInputStream stream = new ByteArrayInputStream(buffer);
        return Document.createFromStream(documentKey, new Date(System.currentTimeMillis()), "." + FilenameUtils.getExtension(filePath), stream);
    }
}
```
- **細節：** 此類別將檔案讀取為位元組陣列，並以此建立 `Document` 物件。

### 在索引中執行關鍵字搜尋

**概觀：** 在已索引的文件上執行搜尋，以快速取得相關資訊。

#### 步驟 1：執行搜尋
```java
String query = "moment";
SearchResult searchResult1 = index.search(query);
```
- **說明：** 使用 `search` 方法搭配簡單文字查詢，從索引資料中取得結果。此方式適用於 **java document search** 場景。

### 如何刪除索引條目

**概觀：** 透過文件鍵刪除特定文件，以管理索引內容。

#### 步驟 1：刪除文件
```java
String[] documentKeys = new String[]{documentLoader.getDocumentKey()};
DeleteResult deleteResult = index.delete(new UpdateOptions(), documentKeys);
```
- **參數說明：** 傳入欲從索引中移除的文件鍵陣列。`UpdateOptions` 提供彈性的刪除策略。

### 刪除後取得剩餘的索引文件

**概觀：** 刪除文件後，取得剩餘索引檔案清單，以確保資料完整性。

#### 步驟 1：取得剩餘文件
```java
DocumentInfo[] indexedDocuments2 = index.getIndexedDocuments();
```
- **說明：** 此步驟協助驗證刪除後索引的當前狀態。

## 實務應用

GroupDocs.Search for Java 多功能且彈性，常見應用包括：

1. **企業文件管理：** 快速搜尋公司文件，提高工作效率。  
2. **法律文件分析：** 高效篩選案件檔案與法律文本，找出相關判例。  
3. **圖書館目錄系統：** 索引與管理大量書籍與手稿，方便存取。

## 效能考量

為取得最佳效能，請留意：

- **索引最佳化：** 定期更新索引以反映最新文件變更。  
- **記憶體管理：** 透過妥善管理資源密集操作，善用 Java 垃圾回收。  
- **可擴展性：** 確保索引策略能處理大量資料而不降低效能。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|----------|
| **未返回結果** | 查詢詞未被索引或被停用詞過濾 | 檢查 `IndexingOptions` 並調整停用詞清單 |
| **記憶體不足錯誤** | 未使用延遲載入即載入過大檔案 | 使用 `Document.createLazy` 或增大 JVM 堆積大小 |
| **已刪除的文件仍出現** | 刪除後索引未重新整理 | 呼叫 `index.optimize()` 或重新開啟索引 |

## 常見問答

**Q: 可以同時索引 PDF、DOCX 與 PPTX 嗎？**  
A: 可以，GroupDocs.Search 內建支援多種格式。

**Q: “how to delete index” 的底層運作原理是什麼？**  
A: `delete` 方法根據文件鍵移除條目，並更新內部倒排表以維持索引一致性。

**Q: 有辦法監控索引大小嗎？**  
A: 使用 `index.getStatistics()` 可取得文件數量與儲存空間資訊。

**Q: 每次刪除後都需要重新建構整個索引嗎？**  
A: 不需要，`delete` 會增量更新索引，保留其餘資料。

**Q: 若需要在變更結構後重新索引所有文件，該怎麼做？**  
A: 建立一個不同資料夾路徑的 `Index` 實例，然後重新加入所有文件。

## 結論

現在，您已掌握 **how to index java** 文件的核心概念，並能使用 GroupDocs.Search for Java 執行快速搜尋。此強大函式庫能徹底改變您管理與檢索大型文件集合的方式，成為任何組織不可或缺的工具。

**後續步驟：**  
- 嘗試不同文件類型與複雜查詢。  
- 探索進階功能，如分面搜尋、Metadata 索引與自訂分析器。  

準備好展開您的索引之旅了嗎？立即實作本教學，體驗更快、更精準的文件檢索！

---

**最後更新：** 2025-12-29  
**測試環境：** GroupDocs.Search Java 25.4  
**作者：** GroupDocs