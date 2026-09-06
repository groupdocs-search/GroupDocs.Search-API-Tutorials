---
date: '2026-06-07'
description: 了解如何使用 GroupDocs.Search 與 Redaction for .NET 高效更新索引，提升您的文件管理系統。
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: 如何使用 GroupDocs.Search 與 Redaction (.NET) 更新索引
type: docs
url: /zh-hant/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# 如何使用 GroupDocs.Search 與 Redaction 更新索引 (.NET)

在現代以數據為驅動的企業中，快速且可靠地 **how to update index** 能夠成敗您的搜尋體驗。無論您在處理成千上萬的合約或龐大的知識庫，將搜尋索引與最新文件變更保持同步對於快速、精確的結果至關重要。本教學將指引您如何在 .NET 中結合使用 GroupDocs.Search 與 GroupDocs.Redaction 來 **update index** 檔案、管理版本化索引，並保護敏感內容——全部在乾淨的 .NET 專案中完成。

## 快速解答
- **What does “how to update index” mean?** 它是修改現有搜尋索引的過程，使新加入或變更的文件在不重新建構索引的情況下即可被搜尋。  
- **Which libraries are required?** GroupDocs.Search 與 GroupDocs.Redaction for .NET（均可透過 NuGet 取得）。  
- **Do I need a license?** 免費試用可用於測試；正式授權可解鎖全部功能。  
- **Can I run this on .NET Core?** 可以，這些函式庫支援 .NET Framework 4.5+、.NET Core 3.1+ 以及 .NET 5/6+。  
- **What performance can I expect?** 使用 2 個執行緒更新 1 GB 的索引，在一般 4 核心伺服器上可於一分鐘內完成。

## “how to update index” 是什麼？
**How to update index** 指的是對現有搜尋索引套用增量變更的技術，而非重新完整建立索引。此方法可減少停機時間、節省 CPU 資源，並在文件新增、編輯或移除時保持搜尋結果即時更新。

## 為何使用 GroupDocs.Search 與 Redaction 進行索引更新？
GroupDocs.Search 支援 **50+ 檔案格式**（PDF、DOCX、XLSX、PPTX、HTML、影像等），且能在不將整個檔案載入記憶體的情況下處理數百頁的文件。結合 GroupDocs.Redaction，您可以在索引前自動移除或遮蔽敏感資料，確保合規同時維持搜尋相關性。

## 前置條件
- **GroupDocs.Search** – 透過 NuGet 安裝。  
- **GroupDocs.Redaction for .NET** – 需要此套件才能執行紅線功能。  
- Visual Studio（或任何 .NET IDE）已安裝 .NET 6+。  
- 基本的 C# 知識與索引概念熟悉度。

### 必要的函式庫與版本
- **GroupDocs.Search** – 從 NuGet 取得最新穩定版。  
- **GroupDocs.Redaction for .NET** – 從 NuGet 取得最新穩定版。

### 環境設定需求
- 具備 .NET SDK 的 Windows 或 Linux 機器。  
- 可存取用於保存索引檔案的資料夾。

### 知識前置條件
- 了解文件索引與搜尋的基本原理。  
- 熟悉企業系統中的文件生命週期管理。

## 設定 GroupDocs.Redaction for .NET

### 安裝套件

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- 搜尋 “GroupDocs.Redaction” 並安裝最新版本。

### 取得授權步驟
1. **Free Trial** – 先使用試用版探索所有功能。  
2. **Temporary License** – 申請臨時金鑰以延長測試時間。  
3. **Purchase** – 取得正式授權以投入生產環境。

### 基本初始化與設定
`Redactor` 是套用文件紅線規則的核心類別。要開始使用，先引用 Redaction 命名空間，並建立一個 `Redactor` 實例：

```csharp
using GroupDocs.Redaction;
```

## 實作指南

我們將說明兩項核心功能：更新已索引的文件以及維護索引版本控制。

### 如何使用 GroupDocs.Search 更新索引？

`Index` 代表磁碟上可搜尋的集合。  
`UpdateOptions` 設定增量更新的執行方式（例如執行緒數）。  
`UpdateDocument` 會對單一文件套用變更，`Commit` 則會提交所有待處理的更新。

**Direct answer (40‑70 words):**  
建立指向索引資料夾的 `Index` 物件，使用 `UpdateOptions` 指定執行緒數，對每個變更的檔案呼叫 `UpdateDocument`，最後呼叫 `Commit` 以永久保存變更。此增量方式僅更新已修改的部分，讓索引保持最新而不必完整重建。

#### 功能 1：更新已索引的文件

##### 概述
更新已索引的文件可確保搜尋結果反映最新內容，即使文件被編輯或取代。

##### 步驟 1：建立 Index
`Index` 類別是代表磁碟上可搜尋集合的最高層物件。

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### 步驟 2：將文件加入 Index
從目錄中加入檔案；函式庫會自動擷取可搜尋的文字。

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### 步驟 3：搜尋與更新
執行查詢、修改來源檔案，然後使用與索引時相同的 `UpdateOptions` 呼叫 `UpdateDocument`。

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**為什麼這樣有效：** 設定 `Threads = 2` 後，更新會利用兩個 CPU 核心，於四核機器上將處理時間大幅減半。

### 如何維護索引版本控制？

`IndexUpdater` 是一個工具類別，用於將舊版索引格式升級至函式庫支援的最新版本。

**Direct answer (40‑70 words):**  
以現有索引的路徑建立 `IndexUpdater`，呼叫 `CanUpdateVersion()` 以驗證相容性，必要時執行 `UpdateVersion()`。升級完成後，重新載入新格式的索引並執行搜尋以確認一切正常。此流程確保在函式庫升級時可無縫遷移。

#### 功能 2：維護索引版本控制

##### 概述
版本控制確保舊版索引在函式庫升級後仍可被搜尋。

##### 步驟 1：檢查相容性
`IndexUpdater` 會檢查目前的索引是否能升級至最新格式。

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### 步驟 2：載入並搜尋
升級後，載入更新後的索引並執行查詢以驗證完整性。

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**為什麼這樣有效：** `CanUpdateVersion` 防護機制可避免因索引結構不匹配而產生的執行時例外，提供安全的升級路徑。

## 實務應用

在實務情境中，**how to update index** 非常重要：

1. **Legal Document Management** – 在合約修訂後快速重新索引，同時對機密條款進行紅線處理。  
2. **Corporate Archives** – 保持歷史紀錄可搜尋，無需重新處理數百萬檔案。  
3. **Content Management Systems (CMS)** – 當作者發布新文章時，將增量更新推送至搜尋索引。

## 效能考量

- **Threading Options:** 根據 CPU 核心數調整 `UpdateOptions.Threads`；更多執行緒可提升吞吐量，但會增加記憶體使用。  
- **Resource Usage:** 監控 RAM；函式庫以串流方式處理檔案，即使是 500 頁的 PDF 記憶體峰值亦相當低。  
- **Best Practices:** 定期排程增量更新，並清除過時的索引版本，以維持最佳效能。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|----------|
| **Index not found** | 資料夾路徑錯誤 | 確認 `Index` 建構子指向正確的目錄。 |
| **Version mismatch error** | 使用較舊的索引搭配較新的函式庫 | 在正常索引前執行 `IndexUpdater` 流程。 |
| **Redaction not applied** | 紅線規則在索引之後才載入 | 在將文件加入索引之前 **先** 套用紅線。 |

## 常見問答

**Q: What is the difference between `UpdateDocument` and `Rebuild`?**  
A: `UpdateDocument` 只修改變更的檔案，而 `Rebuild` 會從頭重新建立整個索引，耗時且佔用更多資源。

**Q: Can I update multiple documents in parallel?**  
A: 可以，將 `UpdateOptions.Threads` 設為欲使用的核心數量；函式庫會在內部處理平行運算。

**Q: Does GroupDocs.Search support encrypted PDFs?**  
A: 當然支援。載入文件時可透過 `SearchOptions.Password` 提供密碼。

**Q: How do I verify that redaction was successful before indexing?**  
A: 呼叫 `Redactor.Apply()` 後檢查輸出檔案大小；檔案變小通常表示紅線成功。

**Q: What .NET versions are officially supported?**  
A: 支援 .NET Framework 4.5+、.NET Core 3.1+、.NET 5 以及 .NET 6+。

## 結論

您現在已擁有一套完整、可投入生產的 **how to update index** 指南，說明如何使用 GroupDocs.Search 以及如何透過 GroupDocs.Redaction for .NET 讓索引保持版本相容。依循上述步驟，即可確保您的搜尋層保持快速、精確，且符合資料隱私法規。

**下一步：**  
- 嘗試不同的 `Threads` 設定，以找出最適合您硬體的平衡點。  
- 在索引前探索進階的紅線模式（例如使用正規表達式移除 SSN）。  
- 將索引更新流程整合至 CI/CD 管線，實現文件管理全自動化。

---

**最後更新：** 2026-06-07  
**測試環境：** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**作者：** GroupDocs  

## 資源
- [文件說明](https://docs.groupdocs.com/search/net/)
- [API 參考](https://reference.groupdocs.com/redaction/net)
- [下載 GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

## 相關教學

- [精通 GroupDocs.Redaction .NET：高效索引建立與別名管理以提升文件搜尋](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [使用 GroupDocs.Redaction .NET 實作同義詞搜尋以增強文件管理](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [精通 GroupDocs Search 與 Redaction 在 .NET 中的應用：進階文件管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)