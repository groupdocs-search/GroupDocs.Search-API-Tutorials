---
date: '2026-07-26'
description: 了解如何使用 GroupDocs.Search 在 .NET 中建立索引，並結合 GroupDocs.Redaction 進行編輯，實現快速的文件搜尋與資料處理。
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: 了解如何使用 GroupDocs.Search 在 .NET 中建立索引，並結合 GroupDocs.Redaction 進行編輯，實現快速的文件搜尋與資料處理。
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: 如何在 .NET 中使用 GroupDocs Search API 建立索引
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: 如何在 .NET 中使用 GroupDocs Search API 建立索引
type: docs
url: /zh-hant/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# 如何在 .NET 中使用 GroupDocs Search API 建立索引

在本教學中，您將了解**建立索引**為您的 .NET 應用程式使用 GroupDocs.Search，並使用 GroupDocs.Redaction 保護敏感內容。完成本指南後，您將能夠建立、更新與修剪可搜尋的索引，並了解為何將搜尋與遮蔽結合是安全文件管理的最佳實踐。

## 快速解答
- **「建立索引」是什麼意思？** 它指的是建立一個可搜尋的資料結構，將文件內容映射到快速查詢鍵。  
- **需要哪些函式庫？** GroupDocs.Search 與 GroupDocs.Redaction for .NET（NuGet 套件）。  
- **我可以索引 PDF、Word 與圖像嗎？** 可以——內建支援超過 150 種格式。  
- **如何從索引中刪除文件？** 呼叫 `Delete` 方法，傳入文件的路徑或 ID。  
- **遮蔽是在索引之前還是之後執行？** 應先執行遮蔽，以確保受保護的資料不會進入索引。

## 「建立索引」是什麼？
「**建立索引**」一詞指的是產生可搜尋資料結構的過程，該結構儲存詞彙與文件之間的映射，以便快速檢索。在 GroupDocs 中，這個結構存放於磁碟上，且可增量更新，無需重新建構整個集合。

## 為何同時使用 GroupDocs.Search 與 GroupDocs.Redaction？
GroupDocs.Search 支援 **150+ 種檔案格式** 的索引，且可處理超過 **10 GB** 的索引，同時將記憶體使用量維持在 200 MB 以下，因為它以串流方式處理檔案，而非一次載入全部。加入 GroupDocs.Redaction 可確保任何機密文字、圖像或中繼資料在進入索引前即被移除，從而保證符合 GDPR、HIPAA 及其他法規。

## 前置條件
- **函式庫與版本** – 安裝最新的 **GroupDocs.Search** 與 **GroupDocs.Redaction** NuGet 套件，需相容於 .NET 6 或更新版本。  
- **IDE** – Visual Studio 2022（或任何支援 .NET 6 的開發環境）。  
- **知識** – 基本的 C# 技能、熟悉檔案 I/O，並了解索引概念。

## 設定 GroupDocs.Redaction for .NET

### 安裝

**使用 .NET CLI：**  
```bash
dotnet add package GroupDocs.Redaction
```  

**在 Visual Studio 的套件管理員主控台中使用：**  
```powershell
Install-Package GroupDocs.Redaction
```  

您也可以在 NuGet 套件管理員 UI 中找到「GroupDocs.Redaction」，並安裝最新的穩定版。

### 取得授權

您可以取得免費試用或申請臨時授權，以無限制探索所有功能。請前往 [GroupDocs 購買頁面](https://purchase.groupdocs.com/temporary-license/) 了解取得授權的更多資訊。

### 基本初始化

Redactor 是執行文件遮蔽操作的主要類別。以下程式碼片段展示了開始使用 GroupDocs.Redaction 所需的最少程式碼：  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

這個簡單的設定即是開始使用 GroupDocs.Redaction 所需的一切。

## 實作指南

### 如何建立索引？

`Index` 代表可搜尋的容器，內含詞彙字典與文件中繼資料。載入或建立 `Index` 物件，指向儲存索引檔案的資料夾，然後呼叫 `Create`。此操作會寫入必要的中繼資料檔案，並為文件寫入做好準備。  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### 步驟 1：建立索引
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### 如何將文件加入索引？

`Add` 會將單一文件插入索引，而 `AddFolder` 會處理目錄中的所有檔案。您可以透過呼叫 `Add` 或 `AddFolder` 來加入檔案。引擎會讀取每個支援的檔案，提取文字，並更新詞彙字典。  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### 步驟 2：加入文件資料夾
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### 如何取得已索引的路徑？

`GetIndexedPaths` 會回傳索引中所有文件路徑的集合。取得已索引檔案路徑清單可讓您驗證哪些文件目前可被搜尋。  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### 步驟 3：顯示已索引的路徑
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### 如何從索引中刪除文件？

`Delete` 會依照路徑或識別碼從索引中移除文件。當檔案被刪除或過時時，應刪除其條目以確保搜尋結果的正確性。  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### 步驟 4：刪除特定路徑
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### 如何在刪除後驗證剩餘的已索引路徑？

刪除後，您可以重新執行取得方法，以確保索引反映當前狀態。  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### 步驟 5：驗證剩餘路徑
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## 實務應用

1. **文件管理系統** – 在數百萬檔案中快速定位合約、發票或手冊。  
2. **法律文件審查** – 在索引前先遮蔽特權資訊，以避免意外洩漏。  
3. **檔案保存解決方案** – 為歷史紀錄保留可搜尋的中繼資料，且無需將整個檔案載入記憶體。  
4. **內容管理平台** – 為部落格、知識庫與多媒體庫提供全站搜尋功能。  
5. **資料合規稽核** – 確保僅有已清理的內容可被搜尋，符合規範要求。

## 效能考量

- **最佳化索引** – 安排每晚執行增量索引；使用 `AddFolder` 並將批次大小設為 100 個檔案，以降低 I/O 峰值。  
- **資源管理** – 監控 CPU 與記憶體；GroupDocs.Search 以串流方式處理檔案，即使是 10 GB 的索引，峰值記憶體也維持在 200 MB 以下。  
- **最佳實踐** – 將索引儲存於 SSD 上以達到次秒級查詢回應，並啟用壓縮 (`index.Compression = true`) 以將磁碟使用量減半。

## 常見問題

**Q: 我可以使用 GroupDocs 索引非文字檔案嗎？**  
A: 可以，GroupDocs.Search 能索引超過 150 種格式，包括 PDF、DOCX、PPTX、XLSX 以及各類圖像，必要時會透過 OCR 提取內嵌文字。

**Q: 如何處理大量文件？**  
A: 使用可設定批次大小的 `AddFolder`，在背景服務中執行索引，並定期呼叫 `Optimize()` 以合併小的索引段落。

**Q: 結合遮蔽與索引有何好處？**  
A: 遮蔽會在資料進入索引前移除個人可識別資訊，確保搜尋結果永不洩露受保護的資料。

**Q: 可以自訂搜尋演算法嗎？**  
A: GroupDocs.Search 提供同義詞字典、自訂分詞器與正規表達式過濾器，讓您微調相關性評分。

**Q: 如何排除常見的索引問題？**  
A: 檢查資料夾權限，確保 .NET 執行環境與函式庫目標相符，並查看索引資料夾中產生的日誌檔以取得詳細錯誤訊息。

## 資源

- **文件**: [GroupDocs Redaction .NET Docs](https://docs.groupdocs.com/search/net/)  
- **API 參考**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **下載**: [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **免費支援**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權**: [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

探索這些資源以加深了解，並提升在 .NET 中實作 GroupDocs.Search 與 Redaction 的能力。祝開發愉快！

---

**最後更新:** 2026-07-26  
**測試環境:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**作者:** GroupDocs

## 相關教學

- [精通索引建立與合併：使用 GroupDocs.Redaction .NET 提升文件管理效率](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [精通 GroupDocs.Redaction .NET：高效索引建立與別名管理，提升進階文件搜尋](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [精通 GroupDocs Search 與 Redaction 在 .NET 中的應用：文件管理完整指南](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)