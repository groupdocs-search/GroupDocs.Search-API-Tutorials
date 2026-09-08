---
date: '2026-07-16'
description: 了解如何使用 GroupDocs，透過 GroupDocs.Search for Java 取得所有支援的檔案格式，並獲取 Java 的檔案副檔名。適合整合文件處理函式庫的開發人員。
keywords:
- how to use groupdocs
- get file extensions java
- validate file extensions java
lastmod: '2026-07-16'
og_description: 如何使用 GroupDocs 取得 Java 中完整的支援檔案格式清單。本指南提供逐步設定說明、程式碼範例，以及驗證應用程式中檔案副檔名的實用技巧。
og_image_alt: Guide showing Java code to list GroupDocs supported file extensions
og_title: 如何使用 GroupDocs – 取得 Java 中支援的檔案格式
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to use GroupDocs and get file extensions java by retrieving
    all supported file formats with GroupDocs.Search for Java. Ideal for developers
    integrating document processing libraries.
  headline: How to Use GroupDocs to Retrieve Supported File Formats in Java
  type: TechArticle
- description: Learn how to use GroupDocs and get file extensions java by retrieving
    all supported file formats with GroupDocs.Search for Java. Ideal for developers
    integrating document processing libraries.
  name: How to Use GroupDocs to Retrieve Supported File Formats in Java
  steps:
  - name: '**Document Management Systems** – Dynamically list supported uploads.'
    text: '**Document Management Systems** – Dynamically list supported uploads.'
  - name: '**Web‑Based File Uploads** – Validate file types client‑side using the
      retrieved list.'
    text: '**Web‑Based File Uploads** – Validate file types client‑side using the
      retrieved list.'
  - name: '**Backup Solutions** – Filter out unsupported files before archiving.'
    text: '**Backup Solutions** – Filter out unsupported files before archiving.'
  type: HowTo
- questions:
  - answer: It’s a Java library that enables full‑text search across many document
      formats without needing separate parsers.
    question: What is GroupDocs.Search?
  - answer: Change the `<version>` tag in `pom.xml` and run `mvn clean install`.
    question: How do I update the library version?
  - answer: The API shown is Java‑specific, but GroupDocs provides similar capabilities
      for .NET, Python, and other platforms.
    question: Can I use this feature in a non‑Java project?
  - answer: Contact GroupDocs support; they frequently add new formats in subsequent
      releases.
    question: What if a needed file type is missing?
  - answer: Yes, a full license removes trial limitations and grants commercial usage
      rights.
    question: Is a commercial license required for production?
  type: FAQPage
tags:
- convert PDF
- GroupDocs.Search
- Java document processing
title: 如何在 Java 中使用 GroupDocs 取得支援的檔案格式
type: docs
url: /zh-hant/java/licensing-configuration/retrieve-supported-file-formats-groupdocs-search-java/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 取得支援的檔案格式

如果你想了解 **如何使用 GroupDocs** 來找出應用程式能處理的精確檔案類型，你來對地方了。在本教學中，我們將示範如何使用 GroupDocs.Search for Java 取得完整的支援格式清單，讓你能自信地在 UI 中顯示或驗證檔案副檔名。完成後，你將擁有一段可重複使用的程式碼片段，能返回所有支援的副檔名，並提供快取結果以提升高效能情境的技巧。

## 快速回答
- **此功能的作用是什麼？** 返回 GroupDocs.Search 能索引的所有檔案副檔名。  
- **為什麼它有用？** 讓你能動態告知使用者支援的上傳類型，避免不支援的檔案錯誤。  
- **需要授權嗎？** 免費試用可用於測試；正式環境需購買完整授權。  
- **需要哪個 Java 版本？** Java 8 或以上。  
- **需要額外設定嗎？** 不需要——只要加入 Maven 依賴並呼叫 API 即可。  

## 什麼是 GroupDocs.Search？
GroupDocs.Search 是一個 Java 函式庫，提供快速的全文搜尋，支援多種文件格式。它抽象化了解析 PDF、Word、試算表以及其他許多類型的複雜性，提供簡單的 API 進行索引與查詢。

## 為什麼要取得支援的檔案格式？
取得支援的檔案格式可為你提供關於函式庫可索引檔案的唯一真實來源。它讓你能以程式方式產生 UI 元素、驗證規則與文件說明，而不必硬編碼值，確保未來函式庫的更新會自動反映在你的應用程式中。

GroupDocs.Search 支援 **超過 120** 種不同的檔案副檔名，涵蓋從常見辦公文件到特殊影像與壓縮檔格式。了解此清單可讓你：
- 建立僅允許支援檔案的動態上傳元件。  
- 為最終使用者產生精確的文件說明。  
- 減少因嘗試索引不支援格式而產生的執行時錯誤。  
- 透過匯出清單為 CSV，快速稽核合規需求。  

## 前置條件
- **Java Development Kit (JDK) 8+**  
- **Maven** 用於相依管理  
- **IDE** 如 IntelliJ IDEA 或 Eclipse  

熟悉基本的 Java 與 Maven 概念將使步驟更順暢。

## 為 Java 設定 GroupDocs.Search

### Maven 設定
將 GroupDocs 儲存庫與相依加入你的 `pom.xml`：

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
如果你偏好，也可以直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 取得授權步驟
- **免費試用** – 探索核心功能。  
- **臨時授權** – 在不受功能限制的情況下測試。  
- **完整授權** – 解鎖正式環境可用的功能。  

#### 基本初始化與設定
加入相依後，你即可建立索引並加入文件：

```java
import com.groupdocs.search.*;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("path/to/index/folder");
        
        // Add documents to the index from a folder
        index.add("path/to/documents/folder");
    }
}
```

## 如何在 Java 中使用 GroupDocs 取得檔案副檔名
只需三行程式碼即可載入支援的副檔名。此方法輕量、毫秒級執行，可在應用程式啟動或按需時呼叫。

### 取得支援的檔案格式
以下步驟示範如何取得 GroupDocs.Search 支援的完整檔案副檔名清單。

#### 步驟 1 – 匯入所需類別
`FileType` 類別提供每種支援檔案格式的中繼資料，包括副檔名與友善說明。

```java
import com.groupdocs.search.results.FileType;
```

#### 步驟 2 – 取得支援類型的集合
呼叫 `FileType.getSupportedFileTypes()` 會返回一個唯讀集合，內含 GroupDocs.Search 能索引的所有格式。

```java
Iterable<FileType> supportedFileTypes = FileType.getSupportedFileTypes();
```

#### 步驟 3 – 迭代並列印每種格式
遍歷該集合，輸出副檔名及其說明。你可以將結果存入 `List<String>` 以供日後重複使用。

```java
for (FileType fileType : supportedFileTypes) {
    System.out.println(fileType.getExtension() + " - " + fileType.getDescription());
}
```

執行此程式碼片段會印出類似 `pdf - Portable Document Format` 的行，提供可直接用於 UI 下拉選單或驗證邏輯的清單。

## 疑難排解技巧
- **Class Not Found** – 確認 Maven 相依已正確解析。  
- **Path Issues** – 確認索引資料夾路徑存在且可寫入。  

## 實務應用
1. **文件管理系統** – 動態列出支援的上傳檔案。  
2. **基於 Web 的檔案上傳** – 使用取得的清單在客戶端驗證檔案類型。  
3. **備份解決方案** – 在歸檔前過濾不支援的檔案。  

## 效能考量
- 如果需要頻繁存取，請將取得的清單儲存在記憶體中；此呼叫本身輕量（在一般伺服器上低於 10 ms）。  
- 保持 GroupDocs.Search 函式庫為最新版本，以獲得效能提升——每個主要版本大約新增 5 種新格式，並將索引延遲降低最多 15 %。  

## 常見問題與解決方案
| 問題 | 原因 | 解決方式 |
|-------|-------|-----|
| `FileType` 類別遺失 | 未加入相依 | 加入相依後重新執行 `mvn clean install` |
| 未列印輸出 | `System.out` 在 IDE 中被抑制 | 檢查主控台設定或從命令列執行 |

## 常見問答

**Q: 什麼是 GroupDocs.Search？**  
A: 它是一個 Java 函式庫，能在多種文件格式上執行全文搜尋，無需額外的解析器。

**Q: 如何更新函式庫版本？**  
A: 在 `pom.xml` 中修改 `<version>` 標籤，然後執行 `mvn clean install`。

**Q: 可以在非 Java 專案中使用此功能嗎？**  
A: 此 API 為 Java 專用，但 GroupDocs 亦提供 .NET、Python 等平台的類似功能。

**Q: 若缺少所需的檔案類型該怎麼辦？**  
A: 請聯絡 GroupDocs 支援團隊；他們會在後續版本中持續加入新格式。

**Q: 正式環境是否需要商業授權？**  
A: 是的，完整授權可移除試用限制並授予商業使用權。

## 資源
- [GroupDocs Search 文件說明](https://docs.groupdocs.com/search/java/)
- [API 參考](https://reference.groupdocs.com/search/java)
- [下載最新版本](https://releases.groupdocs.com/search/java/)
- [GitHub 程式庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)
- [取得臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-07-16  
**測試版本：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

---

## 相關教學

- [設定授權 Java – GroupDocs.Search Java 設定指南](/search/java/licensing-configuration/)
- [java 檔案副檔名過濾與 GroupDocs.Search – 指南](/search/java/advanced-features/master-java-file-filtering-groupdocs-search/)
- [建立與管理 GroupDocs.Search Java 索引](/search/java/indexing/create-manage-groupdocs-search-java-index/)