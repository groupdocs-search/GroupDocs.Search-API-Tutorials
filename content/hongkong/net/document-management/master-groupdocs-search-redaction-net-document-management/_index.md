---
date: '2026-07-16'
description: 了解如何在 .NET 中使用 GroupDocs Search 與 Redaction 進行文件遮蔽，並突出顯示搜尋結果，以加快文件管理。
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: 了解如何在 .NET 中使用 GroupDocs Search 與 Redaction 進行文件遮蔽，並突出顯示搜尋結果，以加快文件管理。
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: 如何在 .NET 中使用 GroupDocs Search 進行文件遮蔽
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: 如何在 .NET 中使用 GroupDocs Search 進行文件遮蔽
type: docs
url: /zh-hant/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# 如何在 .NET 中使用 GroupDocs Search 進行文件遮蔽

在現代企業中，**快速且安全地遮蔽文件**是一項日常挑戰。結合 .NET 版的 GroupDocs.Search 與 GroupDocs.Redaction 可為您提供一個即開即用的強大解決方案，不僅能遮蔽敏感內容，還能執行模糊搜尋並在 HTML 中**突顯搜尋結果**。本教學將帶您完成安裝函式庫、建立索引、執行模糊查詢以及產生突顯輸出——全部以清晰、可投入生產的程式碼範例示範。

## 快速解答
- **第一步是什麼？** 安裝 GroupDocs.Search 與 GroupDocs.Redaction NuGet 套件。  
- **我可以遮蔽 PDF 與 Word 檔案嗎？** 可以，兩種格式皆即開即用支援。  
- **模糊搜尋可用嗎？** 當然可以——您可以將準確度調整至 0 % 至 100 %。  
- **開發時需要授權嗎？** 測試可使用免費試用授權；正式環境則需付費授權。  
- **此解決方案能在 .NET 6 上運作嗎？** 可以，函式庫相容於 .NET Framework 4.5+、.NET Core 3.1+、.NET 5+ 與 .NET 6+。

## 什麼是 GroupDocs.Search？
GroupDocs.Search 是一套 .NET 函式庫，提供快速索引與全文搜尋，支援超過 100 種檔案格式。它可在不將整個檔案載入記憶體的情況下處理高達 2 GB 的文件，適合大規模資料庫。函式庫支援增量索引、多語言分析，且能無縫整合至 .NET 應用程式，讓開發者以最少程式碼打造強大的搜尋體驗。

## 為何使用 GroupDocs.Redaction 進行文件遮蔽？
GroupDocs.Redaction 提供超過 30 種內建遮蔽樣式，並支援批次處理，確保個人資料、機密條款或法規標記能永久移除。根據效能測試，在一般伺服器上遮蔽 500 頁的 PDF 僅需不到 2 秒。此引擎直接作用於文件內容串流，確保被遮蔽的區域無法復原，且保留原始格式與版面配置。

## 前置條件
- **必備函式庫：** GroupDocs.Search、GroupDocs.Redaction  
- **支援平台：** .NET Framework 4.5+、.NET Core 3.1+、.NET 5+、.NET 6+  
- **IDE：** Visual Studio 2022 或更新版本（任何版本）  
- **基本技能：** 熟悉 C#、檔案 I/O 與物件導向概念  

## 如何在 .NET 專案中設定 GroupDocs.Search 與 GroupDocs.Redaction？
透過 .NET CLI、Package Manager Console 或 UI 安裝 NuGet 套件，然後將授權檔案加入專案。這兩步驟的設定即為撰寫任何索引或遮蔽程式碼前的全部需求。安裝套件後，請將授權檔案放置於應用程式根目錄，並在程式碼檔案中引用相應的命名空間。

## 設定 GroupDocs.Redaction 於 .NET
若要在 .NET 應用程式中開始使用 GroupDocs.Search 與 GroupDocs.Redaction，請依照以下安裝步驟：

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet 套件管理員 UI**  
搜尋「GroupDocs.Redaction」並安裝最新版本。

### 取得授權步驟
1. **免費試用**：於 [GroupDocs](https://www.groupdocs.com) 註冊以取得臨時授權。  
2. **購買**：欲完整使用，請於 GroupDocs 官方網站購買授權。  
3. **臨時授權**：可透過提供的連結取得，用於評估目的。  

#### 基本初始化與設定
`Index` 類別代表儲存在磁碟上的可搜尋索引，提供新增、更新與查詢文件的方法。安裝完成後，使用必要的設定初始化專案：  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## 實作指南

### 建立與索引文件
**概述**  
此功能示範如何透過為包含多個檔案的資料夾建立索引，來有效組織文件。

#### 步驟 1：定義路徑  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### 模糊搜尋設定與執行
**概述**  
模糊搜尋允許您即使搜尋詞有輕微差異仍能找到文件。此功能展示如何設定具可調整準確度的模糊搜尋。

#### 步驟 1：啟用模糊搜尋  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### 以 HTML 格式突顯搜尋結果
**概述**  
突顯搜尋結果會在檔案中以視覺方式標記相關段落，方便快速分析。

#### 步驟 1：設定高壓縮  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### 步驟 2：突顯並輸出  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### 疑難排解技巧
- 確認路徑正確指定，以避免找不到檔案的錯誤。  
- 確認已設定目錄的讀寫權限。  

## 實務應用
1. **法律文件審查** – 快速在龐大的法律資料庫中定位案件相關詞彙。  
2. **學術研究** – 在數千篇論文中搜尋特定方法論。  
3. **商業智慧** – 從季報中抽取關鍵指標，免除手動挖掘。  
4. **客戶支援** – 掃描支援票據以找出常見問題，並在分析前遮蔽個人資料。  
5. **內容管理系統 (CMS)** – 透過模糊搜尋與自動遮蔽敏感片段提升內容檢索。  

## 效能考量
- 優化索引儲存設定，以在速度與磁碟使用之間取得平衡。  
- 定期更新索引以保持資料最新，減少不必要的處理。  
- 及時釋放未使用的物件以防止記憶體洩漏，特別是在處理大量批次時。  

## 如何使用 GroupDocs Redaction 從 PDF 中遮蔽敏感資訊？
`Redactor` 是用於對支援的文件格式套用遮蔽樣式的主要類別。使用 `Redactor redactor = new Redactor("file.pdf")` 載入目標 PDF，定義遮蔽樣式（例如 `redactor.AddRedaction(new RedactionPhrase("confidential"))`），然後呼叫 `redactor.Apply()`——函式庫會在保留版面配置的同時覆寫原始檔案為已遮蔽內容。此一步驟工作流程保證不會留下受保護詞彙的任何痕跡。

## 如何在模糊查詢後於 HTML 中突顯搜尋結果？
`SearchResultHighlighter` 提供產生從搜尋匹配結果中突顯 HTML 片段的工具。執行模糊查詢，取得匹配的片段，並將其傳入 `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")`。此方法會以提供的標籤包裹每個出現的詞彙，產生一段 HTML 片段，讓所有相關詞彙以視覺方式強調。突顯的 HTML 可直接嵌入網頁或另存為報告，方便最終使用者查看每筆匹配的上下文。

## 常見問題

**Q: 什麼是模糊搜尋？**  
A: 模糊搜尋找出近似匹配，容忍拼寫錯誤或查詢詞的輕微變化。

**Q: 我可以在商業專案中使用這些函式庫嗎？**  
A: 可以，有效的 GroupDocs 授權允許商業使用權。

**Q: 如何有效處理大量文件集合？**  
A: 使用增量索引，調整 `IndexingOptions` 的批次大小，並排程定期重建索引以維持最佳效能。

**Q: GroupDocs.Search 支援哪些檔案格式？**  
A: 支援超過 100 種格式，包括 PDF、DOCX、XLSX、PPTX、HTML、TXT，以及 JPEG、PNG 等影像類型。

**Q: 是否支援多語言的搜尋與遮蔽？**  
A: 有，函式庫內含超過 30 種語言的分析器，讓全球內容的搜尋與遮蔽皆能精確執行。

## 資源
- [文件說明](https://docs.groupdocs.com/search/net/)  
- [文件說明](https://docs.groupdocs.com/search/net/)  
- [支援論壇](https://forum.groupdocs.com/c/search/10)  
- [API 參考](https://reference.groupdocs.com/redaction/net)  
- [下載](https://www.groupdocs.com/products/search-net)

---

**最後更新：** 2026-07-16  
**測試環境：** GroupDocs.Search 2.0.0 與 GroupDocs.Redaction 2.0.0 for .NET  
**作者：** GroupDocs

## 相關教學

- [在 .NET 文件中使用 GroupDocs.Search 與 Redaction 突顯搜尋結果](/search/net/highlighting/highlight-search-results-net-groupdocs/)  
- [精通 GroupDocs Redaction 與 Search 在 .NET 中的應用：高效文件管理與安全搜尋](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)  
- [精通 GroupDocs.Redaction .NET 文件遮蔽：索引與別名管理以實現安全文件管理](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)