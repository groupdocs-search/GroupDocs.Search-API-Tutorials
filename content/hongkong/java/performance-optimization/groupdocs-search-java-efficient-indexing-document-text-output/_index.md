---
date: '2026-06-27'
description: 逐步指南，說明如何使用 GroupDocs.Search for Java 建立索引、從文件中提取文字，並將文字輸出至檔案——這是一個快速的
  java 搜尋函式庫。
keywords:
- how to create index
- extract text from documents
- output text to file
- add documents to index
- extract text to string
schemas:
- author: GroupDocs
  dateModified: '2026-06-27'
  description: Step‑by‑step guide on how to create index, extract text from documents
    and output text to file using GroupDocs.Search for Java – the fast java search
    library.
  headline: How to create index java with GroupDocs.Search for Java
  type: TechArticle
- questions:
  - answer: Yes, the library is pure Java and works seamlessly with any JVM language.
    question: Can I use GroupDocs.Search with other JVM languages like Kotlin or Scala?
  - answer: High compression reduces disk usage by up to 70 % and adds only a minimal
      CPU overhead during indexing; query latency remains under 100 ms for typical
      workloads.
    question: How does compression affect search speed?
  - answer: Absolutely. Use `index.add()` for new files and `index.remove()` to delete
      outdated ones, allowing incremental updates.
    question: Is it possible to update an existing index without rebuilding it?
  - answer: The `PlainText` result from the **structured text extraction** adapter
      provides clean, language‑agnostic content ideal for NLP tasks.
    question: Which output format is best for natural‑language‑processing pipelines?
  - answer: A free trial license suffices for development and evaluation; production
      deployments require a purchased license.
    question: Do I need a license for development and testing?
  type: FAQPage
title: 如何使用 GroupDocs.Search for Java 建立 java 索引
type: docs
url: /zh-hant/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# 精通高效文件搜尋：使用 GroupDocs.Search for Java

在成千上萬的 PDF、Word 檔案或試算表中尋找正確的段落，感覺就像在大海撈針。快速 **How to create index** 並找回那根針，正是文件搜尋解決方案的價值所在。在本教學中，您將學習如何使用 **GroupDocs.Search for Java**，這個高效能的 java 搜尋函式庫，來 **create index**、**add documents to index**，以及 **extract text from documents**，支援檔案、串流、字串與結構化資料等多種格式。完成後，您將擁有可在大型文件集合上擴展且記憶體使用率低的生產就緒索引管線。

## 快速解答
- **主要目的為何？** 是 **how to create index** 並即時檢索文件內容。  
- **我應該使用哪個函式庫？** The **GroupDocs.Search for Java** **java search library**。  
- **我可以將文字輸出到檔案嗎？** Yes – the library provides **output text to file** adapters for HTML, plain text, and more。  
- **支援結構化抽取嗎？** Absolutely – use the **structured text extraction** adapter to get field‑level data。  
- **我需要授權嗎？** A trial license works for development; a permanent license is required for production deployments。

## 您將學到的內容
- 如何使用 GroupDocs.Search for Java **how to create index** 與 **add documents to index**。  
- 針對 **output text to file**、串流、字串與結構化格式的技巧。  
- 提升效能的最佳實踐，確保索引快速且記憶體使用效率高。  
- 真實案例展示這些功能的優勢，例如法律合約資料庫與學術論文存檔。

## 為何使用 GroupDocs.Search for Java？
GroupDocs.Search 支援 **50+ 種輸入與輸出格式**，包括 DOCX、XLSX、PPTX、PDF、HTML 以及常見影像類型，且能在不將整個檔案載入記憶體的情況下索引多 GB 檔案。基準測試顯示，1 GB 的文件集合可在標準 8 核心伺服器上於 2 分鐘內完成索引，而搜尋查詢的回應時間少於 100 毫秒。

## 前置條件
- **Java Development Kit (JDK)** 8 或更新版本。  
- **GroupDocs.Search for Java** 函式庫（試用版或授權版）。  
- **Maven** 用於相依管理。  
- 基本的 Java I/O 知識。

## 設定 GroupDocs.Search for Java
首先，將 GroupDocs.Search 的 Maven 套件庫與相依項目加入您的專案 `pom.xml`。此步驟確保函式庫可於 classpath 中使用。

**Maven 設定**  
在您的 `pom.xml` 檔案中加入以下套件庫與相依設定：

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

若偏好直接下載，可從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 取得最新版本。

**授權取得**  
若要在生產環境使用 GroupDocs.Search，請從官方網站取得試用或永久授權。試用授權在開發與測試階段無限制。

## 如何使用自訂設定建立 Java 索引
`Index` 是代表可搜尋文件集合的核心類別。  
`IndexSettings` 設定索引的選項，例如壓縮。  
`CompressionLevel` 定義儲存文字的壓縮程度。

載入啟用壓縮的 `Index` 物件，指向資料夾，並加入所有支援的檔案。此段落直接告訴您該怎麼做：以 `new Index("indexFolder", new IndexSettings().setCompressionLevel(CompressionLevel.High))` 建立 `Index`，接著呼叫 `index.add("documentsFolder", true)` 以遞迴方式索引每個支援的檔案。高壓縮模式可將磁碟佔用量減少最高 70 %，同時保持搜尋速度。

建立索引是任何以搜尋為核心的應用程式的基礎。以下範例將逐步說明流程、解釋每個設定，並示範如何驗證索引已成功建立。

### 索引建立與文件索引

#### 概觀
`Index` 類別是代表可搜尋文件集合的核心元件。它儲存倒排索引、詞彙字典與快速查找所需的中繼資料。

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
- **Index Settings**：我們啟用 **high compression** 以儲存文字，優化磁碟空間使用，同時不影響查詢速度。  
- **Adding Documents**：`index.add()` 方法 **adds documents to index**，會遞迴掃描資料夾並自動處理所有支援的格式。

## 如何將文字輸出為檔案、串流、字串與結構化格式
索引完成後，您常需要抽取文件的原始或格式化文字。GroupDocs.Search 提供四種適配器，讓您將抽取的內容寫入檔案、記憶體串流、Java `String`，或結構化物件模型。

### 文件文字輸出至檔案

`FileOutputAdapter` 將抽取的文件文字以選定格式寫入檔案。

#### 概觀
`FileOutputAdapter` 直接將抽取的文字以選定格式（HTML、純文字等）寫入磁碟檔案。這對於產生可供人閱讀的報告或供後續處理管線使用非常有用。

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
- **FileOutputAdapter**：將索引文件的文字轉換為 HTML，寫入指定的檔案路徑，保留標題、表格等基本格式。

### 文件文字輸出至串流

`StreamOutputAdapter` 將抽取的文件文字串流至 `ByteArrayOutputStream`，無需產生暫存檔案。

#### 概觀
當您僅需暫時使用內容，例如透過 HTTP 傳送或嵌入 Web 回應時，請使用 `StreamOutputAdapter`。它將文字串流至 `ByteArrayOutputStream`，避免產生暫存檔案的開銷。

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
- **StreamOutputAdapter**：將文件文字串流至 `ByteArrayOutputStream`，允許彈性處理且不觸及檔案系統。

### 文件文字輸出至字串

`StringOutputAdapter` 將整個文件文字捕獲為單一 `String` 物件。

#### 概觀
用於快速日誌、除錯或 UI 顯示時，`StringOutputAdapter` 可將整個文件文字捕獲為單一 `String` 物件。

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
- **StringOutputAdapter**：將文件文字捕獲於 `String`，方便嵌入日誌、主控台輸出或 UI 元件。

### 文件文字輸出至結構化格式

`StructuredOutputAdapter` 回傳包含段落、表格與自訂中繼資料的豐富物件模型。

#### 概觀
`StructuredOutputAdapter` 回傳包含段落、表格與自訂中繼資料的豐富物件模型。此格式非常適合後續的自然語言處理 (NLP) 或資料抽取工作流程。

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
- **StructuredOutputAdapter**：將文件文字抽取為 **structured text extraction** 格式，支援細緻分析、欄位抽取與機器學習管線整合。

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| **Index not created** | 錯誤的資料夾路徑或缺少寫入權限 | 確認 `indexFolder` 已存在且應用程式具有寫入權限 |
| **No documents returned** | 未呼叫 `index.add()` 或來源資料夾錯誤 | 確保 `documentsFolder` 指向正確目錄且包含支援的檔案類型 |
| **Output file empty** | 輸出適配器路徑無效或缺少目錄 | 在執行前建立目標目錄 (`YOUR_OUTPUT_DIRECTORY`) |
| **Memory spikes with large files** | 將整個檔案載入記憶體 | 使用 `StreamOutputAdapter` 以增量方式處理資料 |

## 常見問答

**Q: 我可以將 GroupDocs.Search 與其他 JVM 語言（如 Kotlin 或 Scala）一起使用嗎？**  
A: 可以，該函式庫純粹使用 Java，能無縫與任何 JVM 語言配合使用。

**Q: 壓縮會如何影響搜尋速度？**  
A: 高壓縮可將磁碟使用量降低最高 70 %，且在索引期間僅增加極少的 CPU 開銷；對於一般工作負載，查詢延遲仍保持在 100 毫秒以下。

**Q: 是否可以在不重新建置的情況下更新現有索引？**  
A: 當然可以。使用 `index.add()` 新增檔案，使用 `index.remove()` 刪除過時檔案，即可進行增量更新。

**Q: 哪種輸出格式最適合自然語言處理管線？**  
A: 來自 **structured text extraction** 適配器的 `PlainText` 結果提供乾淨、語言無關的內容，非常適合 NLP 任務。

**Q: 開發與測試是否需要授權？**  
A: 免費試用授權足以支援開發與評估；生產環境部署則需購買授權。

## 結論
您現在擁有完整、可投入生產的工作流程，能 **how to create index**、加入文件，並以您可能需要的各種格式抽取文字。首先以壓縮設定建立 `Index`，加入文件集合，然後依下游需求選擇合適的輸出適配器——無論是產生 HTML 報告、供給 NLP 模型，或將內容串流至 Web 用戶端。嘗試增量更新 API，以免頻繁重建索引，您即可在任何文件庫中享受快速、可靠的搜尋。

---

**最後更新：** 2026-06-27  
**測試版本：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## 相關教學

- [將文件加入索引 – GroupDocs.Search Java 指南](/search/java/advanced-features/)
- [使用 GroupDocs.Search for Java 建立文件索引](/search/java/advanced-features/groupdocs-search-java-implementation-guide/)
- [如何在 Java 中使用 GroupDocs.Search 以中繼資料索引將文件加入索引](/search/java/indexing/groupdocs-search-java-metadata-indexing/)