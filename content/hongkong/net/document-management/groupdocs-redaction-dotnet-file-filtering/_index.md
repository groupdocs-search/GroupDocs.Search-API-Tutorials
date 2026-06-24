---
date: '2026-04-21'
description: 了解如何使用 GroupDocs.Redaction for .NET 來過濾檔案，包括依建立日期、檔案大小、修改日期過濾，以及如何套用
  NOT 過濾條件。
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: 如何使用 GroupDocs.Redaction for .NET 篩選檔案
type: docs
url: /zh-hant/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# 如何使用 GroupDocs.Redaction for .NET 篩選檔案

在當今快速變化的數位環境中，**如何篩選檔案**可能會左右您的工作效率。無論您需要依檔案副檔名、建立日期、大小或修改日期來分離文件，完善的篩選策略都能節省時間、降低儲存成本，並保持搜尋索引的整潔。在本教學中，我們將透過使用 GroupDocs.Redaction for .NET 的實務範例，向您展示如何精確篩選檔案以滿足常見的商業需求。

## 快速解答
- **需要什麼函式庫？** GroupDocs.Redaction for .NET (install via NuGet).  
- **可以依建立日期篩選嗎？** Yes – use `CreateCreationTimeRange`.  
- **如何排除特定類型？** Apply a NOT filter with `DocumentFilter.CreateNot`.  
- **支援檔案大小篩選嗎？** Absolutely, via `CreateFileLengthRange` or upper/lower bounds.  
- **需要授權嗎？** A trial or full license is required for production use.

## 使用 GroupDocs.Redaction 進行檔案篩選是什麼？
檔案篩選讓您告訴索引引擎根據副檔名、日期、路徑模式或大小等中繼資料，哪些文件要納入或忽略。透過定義精確的 `DocumentFilter` 規則，您可以保持索引精簡，搜尋速度更快。

## 為什麼要使用 GroupDocs.Redaction for .NET？
- **內建篩選輔助工具** – no need to write custom file‑system code.  
- **邏輯運算子** – combine multiple criteria with AND, OR, and NOT.  
- **效能最佳化** – filters are applied during indexing, not after.  
- **跨平台** – works with .NET Framework, .NET Core, and .NET 5/6+.

## 前置條件
- .NET Framework 4.6+ 或 .NET Core 3.1+ 已安裝。  
- Visual Studio 或您偏好的 C# IDE。  
- 基本的 C# 知識。  

### 必要的函式庫與設定
使用您偏好的方式安裝 NuGet 套件：

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **專業提示：** 安裝完成後，將授權檔案加入專案根目錄，並在建立任何 Redactor 或 Index 物件之前呼叫 `License.SetLicense("license-file-path")`。

## 設定 GroupDocs.Redaction for .NET

首先，建立一個指向您想要處理的文件的 `Redactor` 實例：

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **為什麼這很重要：** 初始化 Redactor 可確保函式庫已準備好在後續工作流程中套用篩選與遮蔽規則。

## 如何依副檔名篩選檔案

依副檔名篩選是縮小文件集合最常見的方式。以下範例僅保留 FB2、EPUB 與 TXT 檔案。

### 依副檔名篩選

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何套用 NOT 篩選以排除不需要的類型

如果您需要**套用 NOT 篩選**邏輯，例如排除 HTML 與 PDF 檔案，請使用 `CreateNot`。

### 排除 HTM、HTML 與 PDF 檔案

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何依建立日期篩選檔案

當您需要**依建立日期篩選**時，請指定起始與結束的 `DateTime`。

### 依建立日期範圍篩選

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何依修改日期篩選檔案

與建立日期類似，您可以將結果限制為在特定時間點之前被修改的檔案。

### 依修改日期篩選

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何使用正規表達式依路徑篩選檔案

如果您的資料夾結構遵循命名慣例，正規表達式可用於定位特定路徑。

### 依檔案路徑模式篩選

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何依檔案大小篩選

在處理頻寬或儲存空間限制時，控制文件大小是必須的。

### 依檔案大小篩選（50 KB – 100 KB）

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何使用 AND 結合多個條件

當您需要一次使用多個條件篩選檔案時，請使用 `CreateAnd` 結合它們。

### AND 邏輯範例

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 如何使用 OR 結合多個條件

當任一規則符合時，使用 `CreateOr`。

### OR 邏輯範例

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 常見問題與解決方案
- **篩選未套用：** 確保在建立 `Index` 實例之前 **先** 指定 `settings.DocumentFilter`。  
- **出現未預期的檔案：** 再次確認檔案副檔名包含前置的點 (`.txt`)。  
- **效能下降：** 使用 AND 結合篩選，以減少在索引流程早期掃描的檔案數量。  
- **正規表達式錯誤：** 在路徑模式中跳脫特殊字元，或使用 `RegexOptions.IgnoreCase` 以進行不區分大小寫的比對。

## 常見問答

**Q: 可以將 NOT 篩選與 AND 篩選結合嗎？**  
A: 可以。先建立 NOT 篩選 (`DocumentFilter.CreateNot`)，再將其作為 `DocumentFilter.CreateAnd` 的其中一個參數。

**Q: 如何篩選大於 10 MB 的檔案？**  
A: 使用 `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` 只包含超過該大小的檔案。

**Q: 能同時依建立日期與修改日期篩選嗎？**  
A: 當然可以。分別建立每個篩選，然後使用 `CreateAnd` 結合它們。

**Q: 這些篩選能用於雲端儲存路徑嗎？**  
A: 這些篩選在本機檔案系統上運作。若是雲端來源，請先將檔案下載至暫存資料夾，再套用相同的篩選。

**Q: 更改篩選需要重新索引嗎？**  
A: 需要。篩選會在呼叫 `index.Add` 時評估。變更篩選意味著必須重新建構索引，以反映新的條件。

## 結論

掌握使用 GroupDocs.Redaction for .NET **篩選檔案** 的技巧——無論是依副檔名、建立日期、修改日期、檔案大小，或是使用 NOT 邏輯——都能簡化文件管理，保持索引效能，並專注於真正重要的內容。嘗試運用邏輯運算子，將篩選調整至符合您的業務規則，您將立即感受到速度與儲存效率的提升。

---

**最後更新：** 2026-04-21  
**測試版本：** GroupDocs.Redaction 24.11 for .NET  
**作者：** GroupDocs