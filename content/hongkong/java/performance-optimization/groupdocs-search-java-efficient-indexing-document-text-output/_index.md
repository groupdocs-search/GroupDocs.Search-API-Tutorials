---
date: '2026-01-14'
description: 學習如何使用 GroupDocs.Search for Java 高效地建立 Java 索引與提取 Java 文字。優化文件搜尋、將文字輸出至檔案，並處理結構化文字提取。
keywords:
- GroupDocs.Search for Java
- efficient document search
- index creation in Java
title: 如何使用 GroupDocs.Search for Java 建立索引
type: docs
url: /zh-hant/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# 精通使用 GroupDocs.Search for Java 的高效文件搜尋

在文件管理的世界裡，快速在大量文件中找到特定內容至關重要。無論您在管理法律合約還是學術論文，**create index java** 功能都能節省大量人工時間。本教學深入探討如何使用 **GroupDocs.Search for Java**，這是一個強大的 **java search library**，可協助您建立索引、**add documents to index**，以及**extract text java** 從檔案中高效提取文字。完成本指南後，您將了解如何使用自訂設定建立索引，並以多種格式輸出文件文字，包括結構化文字提取。

## 快速解答
- **主要目的為何？** 透過 **create index java** 快速檢索文件內容。  
- **應使用哪個函式庫？** **GroupDocs.Search for Java** **java search library**。  
- **可以將文字輸出至檔案嗎？** 可以，使用提供的 **output text to file** 介面。  
- **支援結構化提取嗎？** 當然可以——使用 **structured text extraction** 介面。  
- **需要授權嗎？** 生產環境必須使用試用或永久授權。

## 您將學到
- 如何使用 GroupDocs.Search for Java **create index java** 並 **add documents to index**。  
- **output text to file**、串流、字串與結構化資料的技術。  
- 提升搜尋效能與記憶體管理的最佳化技巧。  
- 這些功能的實務應用案例。

### 前置條件
在開始教學前，請確保您已具備以下條件：
- **Java Development Kit (JDK)**：建議使用 8 版或以上。  
- **GroupDocs.Search for Java** 函式庫。  
- **Maven**：用於相依性管理與專案建置。  
- 基本的 Java 程式設計知識，特別是檔案 I/O 操作。

### 設定 GroupDocs.Search for Java
要開始使用 GroupDocs.Search for Java，您需要將必要的相依性加入專案。以下示範如何使用 Maven 進行設定：

**Maven 設定**  
在您的 `pom.xml` 檔案中加入以下儲存庫與相依性設定：

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

若您偏好直接下載，可從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 取得最新版本。

**授權取得**  
使用 GroupDocs.Search 時，建議取得免費試用或暫時授權。若需正式購買，請前往官方網站取得永久授權。

## 如何使用自訂設定 **create index java**
本節將帶您建立索引、加入文件，並設定壓縮以達到最佳儲存效能。

### 索引建立與文件索引

#### 概觀
建立索引可讓您有效搜尋文件。以下範例示範如何以高壓縮方式 **create index java**，再 **add documents to index**。

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**說明**  
- **Index Settings**：我們啟用高壓縮以儲存文字，優化磁碟空間使用。  
- **Adding Documents**：`index.add()` 方法 **adds documents to index**，會遞迴掃描資料夾。

## 如何將文字輸出至檔案、串流、字串與結構化格式
以下示範四種常見方式，讓您在 **created index java** 後取得並儲存提取的內容。

### 文件文字輸出至檔案

#### 概觀
此範例說明如何以 HTML 格式 **output text to file**，方便視覺檢查或後續處理。

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**說明**  
- **FileOutputAdapter**：將索引文件的文字轉換為 HTML，並寫入指定的檔案路徑。

### 文件文字輸出至串流

#### 概觀
當需要在記憶體中處理（例如產生動態網頁內容）時，輸出至串流是理想選擇。

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**說明**  
- **StreamOutputAdapter**：將文件文字串流至 `ByteArrayOutputStream`，可在不觸及檔案系統的情況下彈性處理。

### 文件文字輸出至字串

#### 概觀
若僅需記錄或顯示內容，將結果轉為 `String` 是最快的方式。

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**說明**  
- **StringOutputAdapter**：將文件文字捕獲於 `String`，方便嵌入日誌或 UI 元件。

### 文件文字輸出至結構化格式

#### 概觀
若需進階解析（如提取欄位、表格或自訂中繼資料），請使用結構化輸出介面。

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**說明**  
- **StructuredOutputAdapter**：將文件文字提取為 **structured text extraction** 格式，支援細緻分析或下游資料管線。

## 常見問題與解決方案
| 問題 | 原因 | 解決方式 |
|------|------|----------|
| **未建立索引** | 資料夾路徑錯誤或缺少寫入權限 | 確認 `indexFolder` 已存在且應用程式具備寫入權限 |
| **未返回文件** | 未呼叫 `index.add()` 或來源資料夾錯誤 | 確保 `documentsFolder` 指向正確目錄且內含支援的檔案類型 |
| **輸出檔案為空** | 輸出介面路徑無效或缺少目錄 | 在執行前建立目標目錄 (`YOUR_OUTPUT_DIRECTORY`) |
| **大型檔案導致記憶體激增** | 整個檔案一次載入記憶體 | 使用串流介面 (`StreamOutputAdapter`) 逐步處理資料 |

## 常見問答

**Q: 可以在 Kotlin 或 Scala 等其他 JVM 語言中使用 GroupDocs.Search 嗎？**  
A: 可以，該函式庫純粹以 Java 實作，能無縫運作於任何 JVM 語言。

**Q: 壓縮會影響搜尋速度嗎？**  
A: 高壓縮可減少磁碟使用量，但在建立索引時可能略增 CPU 負載。搜尋效能仍保持快速，因為函式庫會即時解壓縮。

**Q: 能否在不重新建立的情況下更新現有索引？**  
A: 當然可以。使用 `index.add()` 新增檔案，使用 `index.remove()` 刪除過時檔案。

**Q: 哪種輸出格式最適合後續自然語言處理？**  
A: 透過 **structured text extraction** 介面取得的 `PlainText`，提供乾淨且語言中立的內容，最適合 NLP 流程。

**Q: 開發與測試是否需要授權？**  
A: 開發與評估階段可使用免費試用授權。正式上線的生產環境則需購買授權。

---

**最後更新：** 2026-01-14  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs