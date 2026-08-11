---
date: '2026-03-06'
description: 了解如何新增多個別名、將文件加入索引，並使用 GroupDocs.Search for Java 有效管理可搜尋的索引。
keywords:
- GroupDocs.Search Java
- index management
- alias dictionary
title: 如何在 GroupDocs.Search for Java 中新增多個別名並將文件加入索引
type: docs
url: /zh-hant/java/indexing/groupdocs-search-java-efficient-index-alias-management/
weight: 1
---

# 在 GroupDocs.Search Java 中新增多個別名與將文件加入索引：完整指南

在當今以數據為驅動的世界中，能夠在 **add multiple aliases** 同時 **add documents to index**，為您的搜尋解決方案帶來明顯的效能優勢。無論您是要索引成千上萬的合約、產品目錄或研究論文，GroupDocs.Search for Java 都能讓您 **create searchable index** 結構，並透過別名字典微調查詢——同時保持實作簡單且快速。

## 快速解答
- **開始使用 GroupDocs.Search 的第一步是什麼？** 加入 Maven 相依性並初始化 `Index` 物件。  
- **如何將文件加入索引？** 使用 `index.add("<folder_path>")`，將包含檔案的資料夾傳入。  
- **我可以為複雜查詢建立別名嗎？** 可以——使用別名字典將短代號映射到完整的查詢表達式，且您也可以批次 **add multiple aliases**。  
- **是否可以匯出與匯入別名字典？** 當然可以——使用 `exportDictionary` 與 `importDictionary` 方法。  
- **需要哪個版本的 GroupDocs.Search？** 版本 25.4 或更新（本教學使用 25.4）。  

## 什麼是「add documents to index」？
將文件加入索引是指將原始檔案（PDF、DOCX、TXT 等）輸入至 GroupDocs.Search，讓程式庫分析其內容並建立 **searchable index**。索引完成後，您即可對所有文件執行快速的全文查詢。

## 為什麼要管理別名？
別名讓您將冗長且重複的查詢片段取代為簡短、易記的代號（例如 `@t` → `(gravida OR promotion)`）。這不僅能縮短搜尋字串，還能提升可讀性、可維護性，以及 **optimizes search performance**，尤其在查詢變得複雜時更為顯著。

## 如何新增多個別名？
GroupDocs.Search 提供便利的 `addRange` 方法，讓您一次插入多組別名‑取代對。相較於逐一新增別名，此批次操作可減少開銷。

## 前置條件

- **GroupDocs.Search for Java** ≥ 25.4.  
- **JDK**（任何近期版本，例如 11+）。  
- IDE，例如 **IntelliJ IDEA** 或 **Eclipse**。  
- 具備基本的 Java 與 Maven 知識。  

## 設定 GroupDocs.Search for Java

### 使用 Maven
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

### 直接下載
或者，從官方網站下載最新的 JAR：  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### 取得授權步驟
1. **Free Trial** – 無需承諾即可體驗所有功能。  
2. **Temporary License** – 申請短期金鑰以進行評估。  
3. **Full Purchase** – 取得永久授權以供正式環境使用。  

### 基本初始化與設定

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        // Specify the directory to store indices
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
        
        // Create or open an index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## 實作指南

以下提供每項功能的完整步驟說明。先閱讀說明，然後複製相對應的程式碼區塊。

### 建立或開啟索引

**如何將文件加入索引 – 首先您需要一個已啟動的 Index 實例。**

#### 步驟 1：匯入 Index 類別
```java
import com.groupdocs.search.Index;
```

#### 步驟 2：定義索引檔案的存放位置
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
```

#### 步驟 3：建立新索引或開啟現有索引
```java
Index index = new Index(indexFolder);
```

### 將文件加入索引

索引已建立，現在讓我們 **add documents to index**。

#### 步驟 1：指向來源資料夾
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/Documents";
```

#### 步驟 2：將該資料夾內所有支援的檔案加入
```java
index.add(documentsFolder);
```

> **專業提示：** 每當有新檔案到達時執行此步驟。GroupDocs.Search 只會索引新內容，既有條目保持不變。這正是 **incremental indexing java** 的核心。

### 管理別名字典

別名讓您將短代號映射至複雜的查詢字串。我們將說明如何清除舊條目、加入單一別名，以及批次 **add multiple aliases**。

#### 清除現有別名
```java
if (index.getDictionaries().getAliasDictionary().getCount() > 0) {
    index.getDictionaries().getAliasDictionary().clear();
}
```

#### 新增單一別名
```java
index.getDictionaries().getAliasDictionary().add("t", "(gravida OR promotion)");
index.getDictionaries().getAliasDictionary().add("e", "(viverra OR farther)");
```

#### 新增多個別名
```java
AliasReplacementPair[] pairs = new AliasReplacementPair[] {
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};
index.getDictionaries().getAliasDictionary().addRange(pairs);
```

### 查詢別名取代

您可以取得任意已定義別名的完整文字：

```java
if (index.getDictionaries().getAliasDictionary().contains("e")) {
    String replacement = index.getDictionaries().getAliasDictionary().getText("e");
}
```

### 匯出與匯入別名字典

匯出對於備份或在不同環境間共享非常便利。

#### 匯出別名
```java
String fileName = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.getDictionaries().getAliasDictionary().exportDictionary(fileName);
```

#### 匯入別名
```java
index.getDictionaries().getAliasDictionary().importDictionary(fileName);
```

### 使用別名查詢進行搜尋

有了別名後，您的搜尋字串會變得更簡潔：

```java
String query = "@t OR @e";
SearchResult result = index.search(query);
```

`@` 符號告訴 GroupDocs.Search 在執行搜尋前，先將代號取代為其完整表達式。

## 實務應用

| 情境 | 別名的幫助方式 |
|----------|-------------------|
| **法律文件管理** | 將案件編號（`@case123`）映射至複雜的布林條件，加速檢索。 |
| **電子商務產品搜尋** | 將常見屬性組合（`@sale`）取代為 `(discounted OR clearance)`。 |
| **研究資料庫** | 使用 `@year2020` 展開為跨多篇論文的日期範圍過濾。 |

## 效能考量

- **Incremental Indexing**：僅加入新檔或已變更的檔案，避免完整重新索引。  
- **JVM Tuning**：為大型語料庫分配足夠的堆記憶體（例如 `-Xmx4g`）。  
- **Batch Alias Updates**：使用 `addRange` 一次插入多個別名，降低開銷。  
- **Optimize Search Performance**：保持別名字典精簡，明智地重複使用代號，以減少查詢解析時間。  

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| 新檔案無法搜尋 | 再次執行 `index.add(newFolder)`；GroupDocs.Search 只會索引尚未見過的檔案。 |
| 別名返回空結果 | 確認別名鍵（`@`）正確加上前綴，且字典中包含該代號。 |
| 批次索引期間記憶體使用量高 | 增加 JVM 堆記憶體（`-Xmx`），並考慮分批較小的索引作業。 |

## 常見問答

**Q: 使用 GroupDocs.Search for Java 的主要好處是什麼？**  
A: 它提供強大的即時索引與全文搜尋功能，讓您能快速 **add documents to index**，並以高效能查詢。

**Q: 我可以將 GroupDocs.Search 與資料庫結合使用嗎？**  
A: 可以——從任何來源（SQL、NoSQL、CSV）擷取資料，並使用相同的 `add` 方法將其送入索引。

**Q: 別名如何提升搜尋效率？**  
A: 別名讓您將複雜的查詢邏輯儲存一次，並以短代號重複使用，減少查詢解析時間，並在 **search with aliases** 時降低人工錯誤。

**Q: 是否可以在不重新建構整個字典的情況下更新現有別名？**  
A: 當然可以——只要使用相同的鍵呼叫 `add`，函式庫會覆寫先前的值。

**Q: 若搜尋結果不如預期，我該怎麼辦？**  
A: 檢查別名定義是否正確，重新索引任何新加入的文件，並檢查分析器設定是否有斷詞問題。

---

**最後更新：** 2026-03-06  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs