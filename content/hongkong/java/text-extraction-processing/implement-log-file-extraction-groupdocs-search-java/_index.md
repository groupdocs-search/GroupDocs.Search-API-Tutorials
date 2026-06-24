---
date: '2026-03-28'
description: 學習如何使用 GroupDocs.Search for Java 高效提取日誌。本指南涵蓋設定、實作與效能技巧。
keywords:
- log file extraction
- GroupDocs.Search Java
- Java log analysis
title: 使用 GroupDocs.Search 在 Java 中提取日誌的全面指南
type: docs
url: /zh-hant/java/text-extraction-processing/implement-log-file-extraction-groupdocs-search-java/
weight: 1
---

# 如何使用 GroupDocs.Search 在 Java 中提取日誌：完整指南

有效管理與**學習如何提取日誌**對於 Java 應用程式的除錯、監控與分析至關重要。本指南將說明如何設定 **GroupDocs.Search**、從日誌檔案中提取關鍵欄位，以及處理不支援的情況——同時兼顧效能。

## 快速回答
- **什麼函式庫可以協助在 Java 中提取日誌？** GroupDocs.Search for Java.  
- **我需要授權嗎？** 提供免費試用；正式環境需購買永久授權。  
- **預設支援哪種檔案類型？** `.log` 檔案。  
- **我可以從 InputStream 索引日誌嗎？** 目前不支援——此功能尚未實作。  
- **建議使用哪個 Java 版本？** Java 8 或更高版本，搭配 Maven 進行相依管理。  

## 什麼是使用 GroupDocs.Search 「提取日誌」？
提取日誌是指讀取原始日誌檔案，抽取有用的中繼資料（例如檔名）與日誌內容，並將這些資訊建立索引，以便日後搜尋或分析。GroupDocs.Search 提供快速且具可擴充性的索引，能處理數百萬筆日誌條目。

## 為何使用 GroupDocs.Search 進行日誌提取？
- **高效能索引** – 為大型文字檔案最佳化。  
- **豐富的查詢功能** – 全文搜尋、過濾與標記。  
- **無縫的 Java 整合** – 可與 Maven、Gradle 或手動加入 JAR 使用。  
- **可擴充的欄位提取** – 由您決定要儲存哪些文件欄位。  

## 前置條件
- **Java Development Kit (JDK) 8+**  
- **Maven**（相依管理）  
- **GroupDocs.Search for Java**（版本 25.4 或更新）  
- 具備 Java I/O 與 Maven `pom.xml` 檔案的基本知識  

## 設定 GroupDocs.Search for Java

### Maven 設定

Add the repository and dependency to your `pom.xml`:

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

或者，從官方發佈頁面下載最新的 JAR 檔案：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### 授權取得
- **Free Trial**（免費試用） – 無需付費即可探索核心功能。  
- **Temporary License**（臨時授權） – 使用限時金鑰進行延長測試。  
- **Full License**（完整授權） – 正式部署時必須取得。  

### 基本初始化與設定

Once the library is on the classpath, create an index and add your log folder:

```java
import com.groupdocs.search.*;

public class SearchInitialization {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        // Add documents to the index (e.g., log files)
        index.add("path/to/log/files/");
    }
}
```

## 如何使用 GroupDocs.Search 提取日誌

### 日誌檔案副檔名

#### 概觀
定義提取器應處理的副檔名。本例僅關注 `.log` 檔案。

#### 實作步驟
1. **建立列出支援副檔名的類別。**

```java
import java.util.Arrays;

public class LogFileExtensions {
    private final String[] extensions = new String[]{".log"};

    public String[] getExtensions() {
        return Arrays.copyOf(extensions, extensions.length);
    }
}
```

*說明*：`LogFileExtensions` 類別儲存支援的檔案類型，並回傳防禦性副本以避免意外修改。

### 從檔案路徑提取文件欄位

#### 概觀
我們需要從每個日誌檔案中抽取有用資訊——例如完整檔名與文字內容——以便索引將其儲存為可搜尋的欄位。

#### 實作步驟
1. **實作讀取檔案並建立 `DocumentField` 物件的欄位提取器。**

```java
import com.groupdocs.search.common.DocumentField;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class DocumentFieldsExtractor {
    private static final String[] LOG_EXTENSIONS = new String[]{".log"};

    public DocumentField[] getFields(String filePath) {
        File file = new File(filePath);
        String content = extractContent(filePath);

        return new DocumentField[]{
            new DocumentField("FileName", file.getAbsolutePath()),
            new DocumentField("Content", content),
        };
    }

    private String extractContent(String filePath) {
        try {
            return new String(Files.readAllBytes(Paths.get(filePath)));
        } catch (IOException ex) {
            return "";
        }
    }
}
```

*說明*：`DocumentFieldsExtractor` 會將整個日誌檔案讀入字串（優雅地處理 `IOException`），並回傳兩個可搜尋的欄位：絕對檔名與原始內容。

### 不支援 InputStream 欄位提取

#### 概觀
有時您可能想索引從其他服務串流而來的日誌。此實作**不**支援直接從 `InputStream` 提取欄位。

#### 實作步驟
1. **以明確的例外拋出此限制。**

```java
class UnsupportedInputStreamExtraction {
    public DocumentField[] getFieldsFromStream() {
        throw new UnsupportedOperationException("Not supported yet.");
    }
}
```

*說明*：拋出 `UnsupportedOperationException` 可明確表明此限制，讓呼叫端能優雅地處理（例如回退至基於檔案的提取）。

## 實務應用
- **除錯與事件調查** – 快速在龐大的日誌檔案中定位錯誤訊息。  
- **合規稽核** – 索引日誌以證明保存政策，並可隨時取回證據。  
- **系統健康監控** – 將提取的日誌資料輸入儀表板或警示管線。  

## 效能考量
- **優化索引** – 僅重新索引變更的檔案；使用增量更新。  
- **資源管理** – 調整 JVM 堆積大小，並在大型批次作業中啟用 G1GC。  
- **批次處理** – 將日誌分組處理（例如每批 500 檔），以減少 I/O 負載。  

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|----------|
| **內容欄位為空** | 讀取檔案時發生 `IOException` | 確認檔案權限與路徑正確性；將例外記錄下來以供除錯。 |
| **記憶體不足錯誤** | 一次性索引極大的日誌 | 將大型檔案切分為較小的區塊，或增加堆積大小（`-Xmx2g`）。 |
| **不支援的檔案類型** | 未使用 `.log` 副檔名的檔案 | 擴充 `LogFileExtensions` 以包含其他模式（例如 `.txt`）。 |

## 常見問答

**Q: 我可以使用 GroupDocs.Search 索引儲存在雲端儲存（例如 AWS S3）的日誌嗎？**  
A: 可以。先將物件下載至暫存本機目錄，然後將索引指向該資料夾。

**Q: 此函式庫支援即時日誌串流嗎？**  
A: 即時串流目前未內建支援；您需要自行撰寫將串流緩衝至暫存檔的自訂封裝。

**Q: GroupDocs.Search 如何處理日誌中的 Unicode 字元？**  
A: 函式庫使用平台預設的字元集讀取檔案。對於非 UTF‑8 的日誌，請在讀取檔案時指定字元集。

**Q: 有方法限制索引內容的大小嗎？**  
A: 有。您可以在建立 `DocumentField` 前於 `extractContent` 中截斷內容字串。

**Q: 本指南測試使用的 GroupDocs.Search 版本為何？**  
A: 版本 25.4，為撰寫時最新的穩定版。

## 結論

我們已說明 **如何使用 GroupDocs.Search for Java 提取日誌**——從設定 Maven 相依、定義支援的副檔名、提取檔案層級欄位，到處理不支援的串流提取。依循這些步驟即可建立具彈性的日誌搜尋解決方案，隨應用需求擴展。  
接下來，可探索進階查詢功能（通配符、模糊搜尋），並考慮將索引整合至 REST API，以提供即時日誌檢索。

---

**Last Updated:** 2026-03-28  
**測試環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs