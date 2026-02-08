---
date: '2026-02-08'
description: 了解如何使用 GroupDocs.Search for Java 在 Java 中對搜尋結果進行高亮顯示，以及如何透過同步與非同步索引來索引文件。
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: 突出顯示搜尋結果 Java – 同步與非同步索引
type: docs
url: /zh-hant/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Highlight Search Results Java – Synchronous & Async Indexing

透過功能強大的 GroupDocs.Search 程式庫，為您的 Java 應用程式 **highlight search results Java** 加上醒目標示。無論是少量檔案或龐大儲存庫，熟悉同步與非同步索引皆能讓您在不阻塞執行緒的情況下，提供快速且精確的搜尋結果。

## Quick Answers
- **What does “highlight search results Java” mean?** 它指的是在搜尋結果中以視覺提示（例如 HTML `<mark>` 標籤）呈現匹配的關鍵字，讓使用者一眼看出查詢字詞在每份文件中的出現位置。  
- **When should I use synchronous indexing?** 適用於小至中等規模的資料集，且需要即時取得新加入文件的情況。  
- **When is asynchronous indexing preferable?** 當處理大型文件集合或在 UI 執行緒上執行時，需要保持應用程式的回應性。  
- **Do I need a license?** 開發階段可使用免費試用版；完整授權可解鎖進階功能並移除使用限制。  
- **Which Java version is supported?** Java 8 或更新版本。

## What is “highlight search results Java”?
在 Java 中對搜尋結果進行醒目標示，意指將 GroupDocs.Search 回傳的原始匹配項目以 HTML（或其他標記）包裹，使其在 UI 或網頁上顯示時更加突出。此舉可即時呈現每筆命中的上下文，提升使用者體驗。

## Why use GroupDocs.Search for Java?
GroupDocs.Search 提供高效能、語言無關的搜尋引擎，具備以下特點：
- 即時索引與搜尋  
- 大量工作負載的非同步處理  
- 內建結果醒目標示  
- 多語言與自訂分析器支援  

這些功能使其非常適合內容管理系統、電子商務目錄與企業文件庫等應用場景。

## Prerequisites
開始之前，請確保您已具備：

- 已安裝 **Java Development Kit**（JDK 8 或更新版本）。  
- 如 **IntelliJ IDEA** 或 **Eclipse** 等開發環境。  
- 包含欲索引文件的資料夾。  
- 用於相依管理的 Maven（或自行下載 JAR）。

### Required Libraries and Dependencies
將 GroupDocs.Search 加入您的 Maven 專案：

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

若直接下載，請前往 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 取得最新版本。

### Environment Setup
- 確認 **JAVA_HOME** 指向相容的 JDK。  
- 在 IDE 中建立專案，並加入上述 Maven 設定。  
- 準備一個目錄（例如 `documents/`），內放範例文字、PDF 或 Word 檔案。

## How to set up GroupDocs.Search for Java
1. **Install the Library** – 使用上方的 Maven 片段或從 [GroupDocs](https://releases.groupdocs.com/search/java/) 下載 JAR。  
2. **Obtain a License** – 先取得試用授權，正式上線時再升級為正式授權。  
3. **Initialize the Index** – 以下程式碼示範如何建立（或開啟）索引資料夾：

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## How to highlight search results Java – Synchronous Indexing
同步索引會立即處理文件，使新加入的檔案即時可被搜尋。

### Step 1: Create the index and attach error handling
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Step 2: Add documents and run a search
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Step 3: Process results and **highlight search results Java**
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

`DocumentHighlighter` 會自動以 `<mark>` 標籤（或您自訂的格式）包裹匹配的字詞，產生 **highlighted search results**，即可直接顯示。

## How to highlight search results Java – Asynchronous Indexing
面對數千檔案時，阻塞主執行緒並非理想做法。非同步索引讓引擎在背景執行。

### Step 1: Set up the index with event listeners
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Step 2: Enable asynchronous mode and start indexing
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

索引建構期間，您的應用程式仍可處理其他請求。當 `StatusChanged` 事件回報 `Ready` 後，即可安全執行搜尋並取得 **highlighted search results Java**。

## How to **index documents java** – Practical Tips
- **Batch size**：對於龐大集合，將資料夾切分為較小批次，以避免記憶體激增。  
- **File filters**：使用 `IndexingOptions.setFileExtensions` 僅納入所需格式（例如 `.pdf`、`.docx`）。  
- **Re‑indexing**：文件變更時，呼叫 `index.update(documentPath)` 而非重新建立整個索引。

## Performance Considerations
- **Memory**：留意堆積使用量；若處理大量大型檔案，請調整 `-Xmx`。  
- **CPU**：非同步索引會分散工作負載，但仍會佔用 CPU，建議使用 JVisualVM 監控。  
- **Result Highlighting**：醒目標示會產生少量額外開銷；若需頻繁顯示結果，可快取產生的 HTML。

## Frequently Asked Questions

**Q: Can I combine synchronous and asynchronous indexing in the same application?**  
A: 可以。對於小型且頻繁更新的資料集使用同步索引，對於大量匯入或背景工作則使用非同步索引。

**Q: How do I customize the highlight style?**  
A: 實作自訂的 `DocumentHighlighter`，在匹配字詞周圍寫入您想要的 HTML、CSS 或 XML 標籤。

**Q: What file types does GroupDocs.Search support out of the box?**  
A: 支援 Text、PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、HTML 等多種格式，亦可透過內建解析器擴充更多類型。

**Q: Is it possible to search in multiple languages simultaneously?**  
A: 完全可以。GroupDocs.Search 內建多語言分析器，只要在建立索引時設定相應的 `Analyzer` 即可。

**Q: How do I secure the index folder?**  
A: 將索引存放於受保護的目錄，設定正確的檔案系統權限，並可使用程式庫提供的加密功能對索引進行加密。

---

**Last Updated:** 2026-02-08  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs