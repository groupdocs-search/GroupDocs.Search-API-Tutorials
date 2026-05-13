---
date: '2026-01-26'
description: 學習如何使用 GroupDocs.Search for Java 建立索引並將文件加入索引。啟用同音字搜尋，以提升文件檢索效果。
keywords:
- GroupDocs.Search Java
- homophone search implementation
- document retrieval
title: 如何使用 GroupDocs.Search Java 建立索引：實作同音字搜尋
type: docs
url: /zh-hant/java/searching/groupdocs-search-java-homophone-guide/
weight: 1
---

# 如何使用 GroupDocs.Search Java 建立索引並啟用同音字搜尋

在現代企業中，**如何建立索引** 能夠快速且可靠地完成，往往決定了能否找到關鍵資訊，或是完全錯過。無論是處理法律合約、客戶回饋，或是內部報告，使用 GroupDocs.Search for Java 建立的完善搜尋索引，都能即時、精確地提供結果。本教學將逐步說明整個流程——從設定函式庫、建立索引、將文件加入索引，到最後啟用同音字搜尋以提升查詢智慧。

## 快速答覆
- **建立索引的第一步是什麼？** 使用資料夾路徑初始化 `Index` 物件。  
- **哪個方法可將檔案加入索引？** `index.add(yourDocumentsFolder)`。  
- **如何啟用同音字搜尋？** 設定 `options.setUseHomophoneSearch(true)`。  
- **需要授權嗎？** 免費試用或暫時授權即可用於評估。  
- **需要哪個 Java 版本？** JDK 8 或更新版本。

## GroupDocs.Search 中的索引是什麼？
索引是一種結構化資料存儲，將字詞與其在文件集合中的位置對映，讓查詢如同書本目錄般閃電般快速。建立索引是任何以搜尋為核心的應用程式的基礎。

## 為什麼要啟用同音字搜尋？
同音字搜尋會將查詢語言擴展至發音相似的字詞（例如 “write” 與 “right”）。在使用者可能拼寫錯誤或使用替代拼寫的情境下，能提升召回率，讓結果更完整，且不需額外操作。

## 前置條件
- **Java Development Kit** 8 或更新版本。  
- **GroupDocs.Search for Java** 函式庫（可透過 Maven 取得）。  
- 具備基本的 Java 語法與專案設定知識。  

## 設定 GroupDocs.Search for Java

首先，將 GroupDocs.Search Maven 套件庫與相依性加入 `pom.xml`：

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

或者，您也可以[從 GroupDocs.Search for Java 釋出頁面下載最新版本](https://releases.groupdocs.com/search/java/)。

**授權取得**：GroupDocs 提供免費試用授權或暫時授權供評估使用。欲購買請前往官方網站。

### 基本初始化與設定

建立一個簡易的 Java 類別以初始化搜尋索引：

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        // Specify the path to store index files
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\HomophoneSearch";
        
        // Create an instance of Index
        Index index = new Index(indexFolder);
        
        System.out.println("Index created successfully!");
    }
}
```

## 如何使用 GroupDocs.Search Java 建立索引

建立索引只需要將 `Index` 建構子指向一個資料夾，讓函式庫能在其中存放內部檔案。

### 步驟 1：定義索引路徑
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\HomophoneSearch";
```
將 `YOUR_DOCUMENT_DIRECTORY` 替換為您機器上的絕對路徑。

### 步驟 2：實例化 Index 物件
```java
Index index = new Index(indexFolder);
```
此行**建立索引**，之後會儲存所有可搜尋的內容。

## 如何將文件加入索引

索引建立完成後，需要將欲搜尋的文件餵入索引。

### 步驟 1：指向來源文件資料夾
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```
此資料夾應包含您要索引的檔案（PDF、DOCX、TXT 等）。

### 步驟 2：將資料夾內所有檔案加入
```java
index.add(documentsFolder);
```
`add` 方法會遞迴掃描目錄，將每個支援的檔案建立索引。這是**將文件加入索引**的核心操作。

## 啟用同音字搜尋

當索引已填充完畢，即可開啟同音字支援。

### 步驟 1：建立 SearchOptions
```java
import com.groupdocs.search.SearchOptions;

SearchOptions options = new SearchOptions();
```

### 步驟 2：啟動同音字搜尋
```java
options.setUseHomophoneSearch(true);
```
設定此旗標後，搜尋引擎在處理查詢時會考慮語音相近的字詞。

## 實務應用
1. **法律文件管理** – 即使使用者輸入 “leas”，也能找出包含 “lease” 的合約。  
2. **客戶回饋分析** – 捕捉調查回應中 “price” 與 “prise” 等變形。  
3. **內容管理系統** – 透過匹配 “write” 與 “right” 提升網站搜尋品質。

## 效能考量
- **定期重建** 索引以因應大量文件更新。  
- **監控記憶體** 使用情形；大型索引可考慮增量索引。  
- 遵循 Java 最佳實踐（例如適當的例外處理、使用 try‑with‑resources）以保持應用程式穩定。

## 結論
現在您已了解**如何建立索引**、**如何將文件加入索引**，以及如何使用 GroupDocs.Search for Java 啟用同音字搜尋。這些功能讓您能在任何文件庫上構建快速、智慧的搜尋體驗。

### 後續步驟
- 嘗試**自訂分析器**以微調斷詞規則。  
- 結合**分面搜尋**與同音字支援，實現更豐富的篩選功能。  
- 探索**GroupDocs.Search REST API**以支援跨平台情境。

## 常見問答
1. **什麼是 GroupDocs.Search 中的索引？**  
   - 索引是一種資料結構，允許快速搜尋文件，類似書本的目錄。  
2. **如何使用新文件更新我的索引？**  
   - 使用 `index.add()` 方法加入新文件或重新索引既有文件。  
3. **GroupDocs.Search 能處理大量資料嗎？**  
   - 能，該產品設計具備可擴充性，可有效管理大型資料集。  
4. **搜尋功能中的同音字是什麼？**  
   - 同音字指發音相似但可能意義不同的詞彙，例如 “write” 與 “right”。  
5. **如何排除索引錯誤？**  
   - 檢查檔案路徑、確保文件可存取，並檢視日誌檔以取得具體錯誤訊息。

## 資源
- [文件說明](https://docs.groupdocs.com/search/java/)  
- [API 參考文件](https://reference.groupdocs.com/search/java)  
- [下載最新版本](https://releases.groupdocs.com/search/java/)  
- [GitHub 程式庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)  
- [暫時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-01-26  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

---