---
date: '2026-09-16'
description: 了解如何在 .NET 中使用 GroupDocs 建立 search index、將文件加入索引，並啟用 synonym search 以獲得更智慧的查詢結果。
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: 了解如何在 .NET 中使用 GroupDocs 建立 search index、將文件加入索引，並啟用 synonym search
  以獲得更智慧的查詢結果。
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: 如何在 .NET 中使用 GroupDocs 建立 search index
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: 如何在 .NET 中使用 GroupDocs 建立 search index
type: docs
url: /zh-hant/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# 如何使用 GroupDocs 及同義詞搜尋在 .NET 中建立搜尋索引

在本指南中，您將學習 **如何建立搜尋索引**，使用 GroupDocs.Search，將文件加入索引，並啟用同義詞搜尋，讓使用者即使使用不同的術語也能找到相關內容。無論您是建立法律資料庫、企業知識庫或研究檔案，以下步驟都提供可在 .NET Framework 4.6.1+、.NET Core 與 .NET 5+ 上運行的生產就緒解決方案。

## 快速回答
- **「建立搜尋索引」是什麼意思？** 它會建立一個可搜尋的文件目錄，將抽取的文字以最佳化結構儲存，以毫秒級的速度查找。  
- **為什麼要使用同義詞搜尋？** 它會將查詢擴展為具有相同意義的詞彙，於典型語料庫中可提升最高 30 % 的召回率。  
- **主要前置條件是什麼？** .NET 4.6.1+（或 .NET Core/5+）、C# 基礎知識，以及 GroupDocs.Search + GroupDocs.Redaction NuGet 套件。  
- **需要授權嗎？** 評估階段使用免費試用版即可；正式上線則需購買永久授權。  
- **可以與遮蔽功能結合嗎？** 可以——GroupDocs.Redaction 可在搜尋前或搜尋後執行，以遮蔽敏感資料。

## 什麼是「建立搜尋索引」？
**搜尋索引** 是一種資料結構，保存每份文件的抽取文字與中繼資料，使引擎能即時定位符合的檔案。GroupDocs.Search 會透過掃描來源資料夾、解析支援的格式，並將緊湊的索引檔寫入您指定的目錄來建立此索引。

## 為什麼要啟用同義詞搜尋？
同義詞搜尋會自動將替代詞加入使用者的查詢，例如搜尋 **「improve」** 時，同時返回包含 **「enhance」**、**「upgrade」** 或 **「optimize」** 的文件。實務上可將結果召回率提升 20‑35 %，同時保持高精確度，因為內建的同義詞字典已針對每種語言精心編輯。

## 前置條件
- **.NET Framework 4.6.1** 或更新版本（或任何 .NET Core/5+ 執行環境）。  
- 基本的 C# 開發技能與 Visual Studio（Community、Professional 或 Enterprise）。  
- 透過 NuGet 安裝 GroupDocs.Search 與 GroupDocs.Redaction 套件。

### 安裝
使用以下任一方式安裝 GroupDocs.Redaction for .NET（詳情請參閱 [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) 文件）：

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

或者，在 Visual Studio 中使用 NuGet 套件管理員 UI，搜尋「GroupDocs.Redaction」並直接安裝。API 參考請見 [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)。

### 授權取得
- **免費試用：** 先使用試用版探索全部功能。  
- **臨時授權：** 前往 [GroupDocs 網站](https://purchase.groupdocs.com/temporary-license/) 申請臨時授權，或於 [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) 入口管理授權。  
- **正式購買：** 生產環境就緒時，購買完整授權以移除所有評估限制。

## 如何設定 GroupDocs.Redaction for .NET
GroupDocs.Redaction 提供在搜尋前或搜尋後遮蔽敏感內容的核心功能。它會公開一個 `Redactor` 類別，您可使用授權與可選的設定參數來實例化。

以下程式碼示範如何建立 Redactor 實例並載入授權檔案：

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Redactor 準備好後，您即可在搜尋結果取得的任何文件上呼叫 `redactor.Redact(...)`。

## 如何建立搜尋索引
建立搜尋索引的流程包括指定索引檔案儲存的資料夾，然後初始化 GroupDocs.Search 的 `Index` 類別。索引會保存所有從來源文件抽取的可搜尋資料。

首先，為索引建立目錄，接著實例化 `Index` 物件：

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

建立索引會將一組二進位檔寫入資料夾；每 1,000 頁的檔案通常不超過 200 KB，讓您在不耗盡磁碟空間的情況下擴展至百萬頁。

## 如何將文件加入索引
將文件加入索引需要指向包含來源檔案的資料夾，並指示索引將它們匯入。此過程會解析每種支援的格式，抽取文字，並將其存入索引以供快速檢索。

使用以下程式碼索引來源資料夾中的所有檔案：

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search 支援 **30+** 種輸入格式，包括 DOCX、PDF、PPTX、HTML 以及常見影像類型，讓您幾乎可以索引任何企業檔案庫，無需額外轉換器。

## 如何啟用並執行同義詞搜尋
同義詞處理透過 `SearchOptions` 開啟。啟用後，每次查詢都會自動擴展為包含字典中的同義詞，提升召回率而不犧牲精確度。

使用以下程式碼片段啟用同義詞搜尋：

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

預設同義詞字典包含超過 **5,000** 個英文詞對。您也可以載入自訂的 `SynonymDictionary` 檔案，以支援特定產業術語。

## 自訂同義詞字典
若需領域專屬的同義詞，請載入自己的字典檔，並在執行查詢前將其指派給 `SearchOptions`。

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## 常見故障排除技巧
- **路徑問題：** 再次確認索引與來源資料夾對執行帳號是可存取的。  
- **授權限制：** 未授權的建置可能會將可索引的檔案數限制為 100。  
- **無結果返回：** 確認已載入同義詞字典；您可以在執行時檢查 `options.SynonymDictionary.Count`。

## 實務應用
1. **法律文件管理：** 使用法律術語及其同義詞搜尋案例法。  
2. **學術研究：** 在學術 PDF 與 Word 檔案中擴展文獻搜尋。  
3. **企業知識庫：** 即使使用者以不同方式表述，也能找回內部政策。  
4. **內容管理系統：** 為編輯者提供更豐富的標籤發現功能。  
5. **客服工單系統：** 透過同義問題描述將工單匹配至已知問題。

## 效能考量
- **索引維護：** 大量更新後重新索引；增量索引可將停機時間縮減至 70 % 以內。  
- **資源監控：** 在標準 VM（2 vCPU、8 GB RAM）上索引 10 GB 批次時，記憶體峰值約為 1.2 GB；若接近上限請調整批次大小。  
- **物件釋放：** 完成後立即呼叫 `index.Dispose()` 與 `redactor.Dispose()`，釋放原生資源。

## 結論
您現在已掌握 **如何使用 GroupDocs 建立搜尋索引**、將文件加入索引，以及啟用同義詞搜尋以提供更直觀的使用者體驗。此基礎亦可在其上層加入遮蔽、自訂排序或模糊匹配等功能，打造堅實的搜尋引擎。

## 後續步驟
- 嘗試 `SearchOptions.FuzzySearch` 以捕捉拼寫錯誤。  
- 探索 `Ranking` API 以提升優先文件的排名。  
- 加入 [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) 或 [Free Support Forum](https://forum.groupdocs.com/c/search/10) 社群，分享技巧並提出問題。  
- 查看 [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) 以取得最新更新與功能。

## 常見問答

**Q: 什麼是同義詞搜尋？**  
A: 同義詞搜尋會將使用者的查詢擴展為預先定義的替代詞，增加找到使用不同措辭的相關文件的機會。

**Q: 如何更新我的 GroupDocs 授權？**  
A: 前往 [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) 入口，上傳新授權檔案，使用 `License.SetLicense("path/to/license.lic")` 進行設定。

**Q: 可以在多語言環境中使用同義詞搜尋嗎？**  
A: 可以——為每個支援的語系載入對應的 `SynonymDictionary` 檔案，引擎會在每次查詢時套用相應的同義詞集合。

**Q: 最常見的索引問題是什麼？**  
A: 檔案存取權限、格式不支援，以及超過試用版文件數量限制是開發者最常遇到的三大問題。

**Q: 如何優化超大型索引的效能？**  
A: 使用增量索引、將索引儲存於 SSD，並將 `IndexingOptions.MaxDegreeOfParallelism` 設為與 CPU 核心數相同的值。

---

**最後更新：** 2026-09-16  
**測試環境：** GroupDocs.Search 23.10 for .NET  
**作者：** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## 相關教學

- [Add Document to Index with GroupDocs.Search .NET Tutorials](/search/net/document-management/)
- [Highlight Search Results in .NET Documents Using GroupDocs.Search and Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [How to Update Index with GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)