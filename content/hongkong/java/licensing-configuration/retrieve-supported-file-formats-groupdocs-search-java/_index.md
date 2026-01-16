---
date: '2026-01-16'
description: 學習如何使用 GroupDocs，並透過 GroupDocs.Search for Java 取得所有支援的檔案格式，以獲得 Java 的檔案副檔名。此內容特別適合整合文件處理函式庫的開發人員。
keywords:
- GroupDocs.Search for Java
- retrieve supported file formats
- Java document processing
title: 如何在 Java 中使用 GroupDocs 取得支援的檔案格式
type: docs
url: /zh-hant/java/licensing-configuration/retrieve-supported-file-formats-groupdocs-search-java/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 取得支援的檔案格式

如果您想了解 **如何使用 GroupDocs** 來查詢應用程式可處理的檔案類型，您來對地方了。本教學將示範如何使用 GroupDocs.Search for Java 取得完整的支援格式清單，讓您能在 UI 中自信地顯示或驗證檔案副檔名。

## 快速回答
- **此功能做什麼？** 回傳 GroupDocs.Search 能索引的所有檔案副檔名。  
- **為什麼有用？** 可動態告知使用者支援的上傳類型，避免不支援的檔案錯誤。  
- **需要授權嗎？** 免費試用可用於測試；正式環境需購買完整授權。  
- **需要哪個 Java 版本？** Java 8 或以上。  
- **需要額外設定嗎？** 不需要——只要加入相依性並呼叫 API 即可。

## 什麼是 GroupDocs.Search？
GroupDocs.Search 是一套 Java 函式庫，提供跨多種文件格式的快速全文搜尋。它抽象化了 PDF、Word、試算表等多種檔案的解析複雜度，提供簡易的 API 供索引與查詢使用。

## 為什麼要取得支援的檔案格式？
掌握完整的副檔名清單可讓您：
- 建立只允許支援檔案的動態上傳元件。  
- 為最終使用者產生精確的文件說明。  
- 減少因嘗試索引不支援格式而產生的執行時錯誤。

## 前置條件
- **Java Development Kit (JDK) 8+**  
- **Maven** 用於相依性管理  
- **IDE** 如 IntelliJ IDEA 或 Eclipse  

具備基本的 Java 與 Maven 概念會讓步驟更順利。

## 設定 GroupDocs.Search for Java

### Maven 設定
在 `pom.xml` 中加入 GroupDocs 的儲存庫與相依性：

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
如果您偏好手動方式，可直接從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新版本。

### 授權取得步驟
- **免費試用** – 體驗核心功能。  
- **臨時授權** – 測試時不受功能限制。  
- **完整授權** – 解鎖正式環境所需功能。

#### 基本初始化與設定
加入相依性後，您即可建立索引並加入文件：

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

### 取得支援的檔案格式
以下步驟示範如何取得 GroupDocs.Search 支援的完整副檔名清單。

#### 步驟 1 – 匯入所需類別
```java
import com.groupdocs.search.results.FileType;
```

#### 步驟 2 – 取得支援類型的集合
```java
Iterable<FileType> supportedFileTypes = FileType.getSupportedFileTypes();
```

#### 步驟 3 – 迭代並列印每種格式
```java
for (FileType fileType : supportedFileTypes) {
    System.out.println(fileType.getExtension() + " - " + fileType.getDescription());
}
```

執行此程式碼會印出類似 `pdf - Portable Document Format` 的行，讓您可直接用於 UI 下拉選單或驗證邏輯。

### 疑難排解小技巧
- **Class Not Found** – 確認 Maven 相依性已正確解析。  
- **Path Issues** – 確保索引資料夾路徑已存在且可寫入。  

## 實務應用
1. **文件管理系統** – 動態列出支援的上傳類型。  
2. **Web‑Based 檔案上傳** – 使用取得的清單在客戶端驗證檔案類型。  
3. **備份解決方案** – 在歸檔前過濾不支援的檔案。

## 效能考量
- 若需頻繁存取，建議將取得的清單緩存於記憶體；呼叫本身相當輕量。  
- 保持 GroupDocs.Search 函式庫為最新版本，以獲得效能改進。

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|------|------|----------|
| `FileType` 類別遺失 | 未加入相依性 | 在加入相依性後重新執行 `mvn clean install` |
| 沒有輸出結果 | IDE 中抑制了 `System.out` | 檢查主控台設定或改以命令列執行 |

## 常見問答

**Q: 什麼是 GroupDocs.Search？**  
A: 這是一套 Java 函式庫，可在多種文件格式間執行全文搜尋，無需額外的解析器。

**Q: 如何更新函式庫版本？**  
A: 在 `pom.xml` 中修改 `<version>` 標籤，然後執行 `mvn clean install`。

**Q: 能否在非 Java 專案中使用此功能？**  
A: 此範例為 Java 專用，但 GroupDocs 亦提供 .NET、Python 等平台的類似功能。

**Q: 若缺少所需的檔案類型該怎麼辦？**  
A: 請聯絡 GroupDocs 支援團隊；他們會在後續版本中持續加入新格式。

**Q: 正式環境是否需要商業授權？**  
A: 是的，完整授權可移除試用限制並取得商業使用權。

## 資源
- [GroupDocs Search 文件](https://docs.groupdocs.com/search/java/)
- [API 參考文件](https://reference.groupdocs.com/search/java)
- [下載最新版本](https://releases.groupdocs.com/search/java/)
- [GitHub 原始碼庫](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)
- [臨時授權取得](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-01-16  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs