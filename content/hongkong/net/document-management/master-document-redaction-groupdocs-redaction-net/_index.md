---
date: '2026-07-02'
description: 了解如何使用 GroupDocs.Redaction 與 Aspose.Search.NET 建立 .NET 搜尋索引、將文件加入索引、管理別名，並確保資料安全。
keywords:
- create search index .net
- add documents to index
- groupdocs redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to create search index .NET using GroupDocs.Redaction and
    Aspose.Search.NET, add documents to index, manage aliases, and ensure data security.
  headline: 'Create Search Index .NET with GroupDocs.Redaction: Indexing and Managing
    Aliases for Secure Document Management'
  type: TechArticle
- questions:
  - answer: Yes, both GroupDocs.Redaction and Aspose.Search.NET fully support .NET
      Core 3.1, .NET 5, .NET 6, and later.
    question: Can I use this solution with .NET Core?
  - answer: The engine is tested with indexes containing over 1 million documents,
      maintaining sub‑second query times on standard server hardware.
    question: How many documents can the index handle?
  - answer: Aliases can contain wildcard characters (`*` and `?`) but not full regex
      patterns; for complex patterns, build the query programmatically.
    question: Do aliases support regular expressions?
  - answer: Absolutely. Retrieve the document ID from the search result, load it with
      GroupDocs.Redaction, apply redaction rules, and save the protected version.
    question: Is it possible to redact after searching?
  - answer: GroupDocs offers volume‑based licensing with unlimited developers and
      deployment sites; contact sales for a custom quote.
    question: What licensing model applies to large enterprises?
  type: FAQPage
title: 使用 GroupDocs.Redaction 建立 .NET 搜尋索引：索引與管理別名以確保文件安全管理
type: docs
url: /zh-hant/net/document-management/master-document-redaction-groupdocs-redaction-net/
weight: 1
---

# 使用 GroupDocs.Redaction 建立 .NET 搜尋索引：索引與管理別名以確保文件安全管理

管理大量文件同時保持敏感資訊機密可能具挑戰性。使用 **GroupDocs.Redaction for .NET**，您可以 **create search index .NET** 專案，對文件集合進行遮蔽與搜尋。此教學將指導您如何使用 Aspose.Search.NET 建立或開啟索引、將文件加入索引、管理別名字典，並整合遮蔽功能——同時確保嚴格的資料安全。

## 快速解答
- **本指南的主要目的為何？** 說明如何使用 **create search index .NET** 專案、將文件加入索引，並使用 GroupDocs.Redaction 管理別名。  
- **需要哪些函式庫？** GroupDocs.Redaction and Aspose.Search.NET, both available via NuGet。  
- **需要授權嗎？** 免費試用可用於評估；正式環境需購買完整授權。  
- **能處理大量文件嗎？** 可以——兩個函式庫皆支援處理多百頁檔案，且不需將整個檔案載入記憶體。  
- **此解決方案相容 .NET‑Core 嗎？** 當然相容；可在 .NET 5、.NET 6 及更高版本上執行。

## 介紹

在深入探討之前，先說明為何 **creating a search index .NET** 解決方案重要。索引能讓您在毫秒內於數千個檔案中定位精確片語、模式或已遮蔽的內容，極大加速合規審查、法律取證與內部稽核。結合 Aspose.Search.NET 強大的索引引擎與 GroupDocs.Redaction 完備的遮蔽工具，即可獲得同時保護與即時搜尋資料的單一流程。

## GroupDocs.Redaction for .NET 是什麼？

GroupDocs.Redaction for .NET 是一套函式庫，可程式化遮蔽文字、影像與中繼資料，支援超過 30 種文件格式，包括 PDF、DOCX、PPTX 與 HTML。它可處理高達 2 GB 的檔案，且無需將整個文件載入記憶體，確保企業工作負載的高效能運作。

## 為何使用 Aspose.Search.NET 建立 .NET 搜尋索引？

Aspose.Search.NET 能索引 **50+** 種檔案類型，且支援增量更新，意味著您可將新檔案加入現有索引，而無需重新建置。相較於完整重新索引，可降低最高 70 % 的 CPU 使用率，且對含有 500 k+ 文件的索引，查詢回應時間維持在 200 ms 以下。

## 前置條件

### 必要函式庫、版本與相依性
- **GroupDocs.Redaction** – 最新的 NuGet 版本，兼容 .NET 5/6/7。  
- **Aspose.Search.NET** – 最新的 NuGet 版本，支援 .NET Standard 2.0+ 與 .NET Core。  

兩個函式庫必須針對相同的 .NET 執行時版本，以避免繫結衝突。

### 環境設定需求
- Visual Studio 2022（或任何支援 .NET 6+ 的 IDE）。  
- 取得包含您欲索引與遮蔽之文件的資料夾存取權限。  

### 知識前提
- 熟悉 C# 語法與 .NET 專案結構。  
- 了解索引、搜尋與文件遮蔽的基本概念。

## 如何建立 .NET 搜尋索引？

載入或實例化 `Index` 物件，指向資料夾，並呼叫 `CreateOrOpen`——此一步即可在磁碟上建立或重新開啟可搜尋的儲存區。此操作預設於背景執行緒執行，讓 UI 在索引數千檔案時仍保持回應。

`Index` 代表儲存在磁碟上的可搜尋集合。

### 定義錨點
`Index` 類別是 Aspose.Search.NET 的核心元件，代表磁碟上文件的可搜尋集合。所有索引與查詢操作皆透過此物件進行。

```bash
dotnet add package GroupDocs.Redaction
```

## 如何將文件加入索引？

`AddDocument` 會將檔案加入索引並擷取其可搜尋內容。

透過對每個檔案路徑呼叫 `Index.AddDocument` 來加入文件；此方法會自動擷取文字、元資料與可選的 OCR 內容。您可在 `foreach` 迴圈中批次加入檔案，索引將以增量方式更新，而不會重新建置現有條目。此程序亦會回傳狀態物件，指示成功或錯誤，讓您能以程式方式處理失敗。

```powershell
Install-Package GroupDocs.Redaction
```

## 取得授權步驟

- **免費試用** – 30 天內免費探索所有功能。  
- **臨時授權** – 使用限時金鑰以延長測試。  
- **完整授權** – 生產環境部署必須，且移除所有評估限制。

安裝完成後，請依下列方式初始化 GroupDocs.Redaction：

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Set up additional configuration as needed
```

## 實作指南

我們將依功能將實作分解為可管理的章節。

### 建立或開啟索引

#### 概觀
建立或開啟搜尋索引是有效文件管理與搜尋的基礎。它讓您能快速操作已索引的資料。

#### 步驟說明

**1. 建立/開啟索引**

```csharp
using GroupDocs.Search;

// Specify the directory where your index will be stored
string indexPath = "YOUR_INDEX_DIRECTORY";

// Initialize or open an existing index
Index index = new Index(indexPath);

// Explanation: The Index object is initialized with a directory path,
// which serves as a storage location for all indexed data.
```

**2. 將文件加入索引**

```csharp
using GroupDocs.Search;

// Specify your document directory
string docPath = "YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index
index.Add(docPath);

// Explanation: The Add method indexes all documents within the provided path,
// making them searchable.
```

### 管理別名字典

#### 概觀
別名字典中的別名允許您為複雜的搜尋查詢定義簡寫詞彙，提升搜尋效率與可讀性。

#### 步驟說明

**1. 清除現有別名**

```csharp
using GroupDocs.Search.Dictionaries;

// Check if there are existing aliases and clear them
if (index.Dictionaries.AliasDictionary.Count > 0)
{
    index.Dictionaries.AliasDictionary.Clear();
}

// Explanation: This ensures you start with a clean slate when managing aliases.
```

**2. 新增單一別名條目**

```csharp
index.Dictionaries.AliasDictionary.Add("t", "(gravida OR promotion)");
index.Dictionaries.AliasDictionary.Add("e", "(viverra OR farther)");

// Explanation: Each alias is mapped to an expression that defines its search scope.
```

**3. 使用陣列新增多筆別名**

```csharp
AliasReplacementPair[] pairs = new AliasReplacementPair[]
{
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};

index.Dictionaries.AliasDictionary.AddRange(pairs);

// Explanation: AddRange allows bulk addition of aliases, streamlining the setup process.
```

### 取得與匯出別名

#### 概觀
將別名字典匯出至檔案可讓您在團隊或不同環境間共享搜尋詞彙，而取得特定條目則有助於驗證查詢邏輯。

**取得別名**

```csharp
if (index.Dictionaries.AliasDictionary.Contains("e"))
{
    string replacement = index.Dictionaries.AliasDictionary.GetText("e");
}

// Explanation: Use Contains to check existence before retrieval.
```

**匯出別名**

```csharp
string exportPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ExportDictionary(exportPath);

// Explanation: ExportDictionary saves the alias dictionary for future use or sharing.
```

### 匯入別名並使用別名字典搜尋

#### 概觀
從檔案匯入別名，以使用預先定義的簡寫詞彙簡化搜尋作業，接著執行引用這些別名的查詢。

**1. 匯入別名**

```csharp
string importPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ImportDictionary(importPath);

// Explanation: This method loads existing alias definitions into the dictionary.
```

**2. 使用別名搜尋**

```csharp
string query = "@t OR @e"; // Use aliases in your search query
SearchResult result = index.Search(query);

// Explanation: Leverage aliases to perform complex searches with simple queries.
```

## 常見問題與解決方案

- **索引路徑錯誤** – 確認資料夾路徑為絕對路徑，且應用程式具備讀寫權限。  
- **記憶體洩漏** – 使用完畢後務必呼叫 `Dispose()` 釋放 `Index` 物件，尤其在長時間執行的服務中。  
- **別名未被識別** – 確認別名檔案使用 UTF‑8 編碼，且每行皆符合 `key=value` 格式。

## 常見問答

**Q: 我可以在 .NET Core 上使用此解決方案嗎？**  
A: 可以，GroupDocs.Redaction 與 Aspose.Search.NET 完全支援 .NET Core 3.1、.NET 5、.NET 6 及更高版本。

**Q: 索引能處理多少文件？**  
A: 引擎已在超過 100 萬文件的索引上測試，於標準伺服器硬體上仍能維持次秒級查詢時間。

**Q: 別名支援正規表達式嗎？**  
A: 別名可包含通配符 (`*` 與 `?`)，但不支援完整的正規表達式；若需複雜模式，請以程式方式建構查詢。

**Q: 能在搜尋後進行遮蔽嗎？**  
A: 完全可以。從搜尋結果取得文件 ID，使用 GroupDocs.Redaction 載入，套用遮蔽規則，並儲存受保護的版本。

**Q: 大型企業適用何種授權模式？**  
A: GroupDocs 提供以授權數量為基礎的方案，允許無限制的開發人員與部署站點；請聯絡業務取得客製化報價。

## 結論

透過精通 **GroupDocs.Redaction** 與 **Aspose.Search.NET** 的整合，打造 **create search index .NET** 解決方案，您可大幅提升文件安全性、合規性與可發現性。現在您已具備建立索引、將文件加入索引、管理別名字典，以及套用遮蔽規則的工具——全部於單一高效能 .NET 應用程式中完成。

接下來的步驟？在測試專案中實作程式碼片段，嘗試自訂別名模式，並以您的正式資料集進行索引速度效能測試。

---

**最後更新：** 2026-07-02  
**測試環境：** GroupDocs.Redaction 23.10 for .NET, Aspose.Search.NET 24.5  
**作者：** GroupDocs

## 相關教學

- [精通 GroupDocs.Redaction .NET 的文件索引與進階搜尋查詢](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [精通 GroupDocs.Redaction .NET 的索引建立與合併，以提升文件管理效率](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [在 .NET 中實作 GroupDocs.Search 與 Redaction 以進行文件管理](/search/net/document-management/groupdocs-search-redaction-net-guide/)