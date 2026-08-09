---
date: '2026-07-02'
description: 了解如何使用 GroupDocs.Redaction 與 GroupDocs.Search for .NET，透過將文件加入索引來執行文件遮蔽並提升搜尋效能。
keywords:
- how to redact documents
- optimize search performance
- add documents to index
- redact pdf c#
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  headline: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  type: TechArticle
- description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  name: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  steps:
  - name: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
    text: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
  - name: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
    text: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
  - name: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
    text: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
  type: HowTo
- questions:
  - answer: Yes—`RedactionEngine` works natively with PDF streams, so you can load
      a PDF, apply redaction objects, and save the result without any format conversion.
    question: Can I redact PDF C# files directly without converting them first?
  - answer: Incremental indexing adds only the new files, keeping the index size stable
      and query latency under 200 ms for typical workloads.
    question: How does adding documents to index affect search speed?
  - answer: Absolutely. Use a Windows Service or Azure Function to call `Index.AddDocument`
      on a timer, feeding newly uploaded files into the index.
    question: Is it possible to schedule automatic re‑indexing?
  - answer: Yes—redaction overwrites the original bytes, making recovery impossible
      even with forensic tools.
    question: Does redaction permanently remove the hidden data?
  - answer: Both .NET Framework 4.6.1+ and .NET Core 3.1+ (including .NET 5/6) are
      officially supported.
    question: What .NET versions are fully supported?
  type: FAQPage
title: 如何在 .NET 中使用 GroupDocs 進行文件遮蔽與搜尋索引優化
type: docs
url: /zh-hant/net/document-management/master-document-redaction-groupdocs-net/
weight: 1
---

# 精通 .NET 中的文件塗抹與搜尋索引管理（使用 GroupDocs）

## 介紹

如果您需要 **how to redact documents** 同時保持文件可搜尋，您已來對地方。本教學將帶您結合 **GroupDocs.Redaction** 與 **GroupDocs.Search**，安全隱藏敏感資料，然後 **add documents to index** 以快速檢索。完成後，您將了解如何 **optimize search performance**、在 C# 中塗抹 PDF 檔案，並建立可隨資料量擴展的穩健索引管線。

## 快速答案
- **How do I redact a PDF in C#?** 使用 `RedactionEngine` 載入檔案、定義塗抹區域，然後呼叫 `Save`。  
- **What class creates a search index?** GroupDocs.Search 的 `Index` 類別負責所有索引操作。  
- **Can I add new files without rebuilding the whole index?** 可以 — 呼叫 `Index.AddDocument` 進行增量更新。  
- **Does redaction affect search results?** 塗抹的內容會從索引中排除，確保搜尋結果乾淨。  
- **Which .NET versions are supported?** 支援 .NET Framework 4.6.1+、.NET Core 3.1+ 以及 .NET 5/6。

## 「how to redact documents」是什麼？

**「How to redact documents」** 指的是以程式方式從檔案中移除或遮蔽機密資訊的過程，使隱藏的資料無法被恢復或顯示。塗抹對於合規、隱私與法律工作流程至關重要，必須防止資料外洩。

## 為何使用 GroupDocs 進行塗抹與搜尋？

GroupDocs 支援 **50+ 種檔案格式**（包括 PDF、DOCX、PPTX 以及各類影像），且能在不將整個檔案載入記憶體的情況下處理上百頁的文件，較通用函式庫可達 **最高 30 % 更快的索引速度**。結合 Redaction + Search 套件讓您 **redact PDF C#** 檔案後即可立即索引乾淨的版本，省去額外前置處理的步驟。

## 前置條件

- **GroupDocs.Search** for .NET (v20.11 或更新版本)  
- **GroupDocs.Redaction** for .NET (v20.10 或更新版本)  
- Visual Studio 2017 或更新版本  
- .NET Framework 4.6.1 或更新版本（或 .NET Core 3.1+）

### 知識前置條件
您應該熟悉基本的 C# 語法、專案參考以及檔案系統操作。

## 設定 GroupDocs.Redaction（.NET）

### 安裝函式庫

**.NET CLI**  
`dotnet add package` 是用於在專案中安裝 NuGet 套件的 .NET CLI 指令。  

```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
`Install-Package` 是 NuGet 套件管理員主控台使用的 PowerShell 指令，用於加入函式庫。  

```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
在 UI 中搜尋 “GroupDocs.Redaction”，然後點擊 **Install** 以下載最新的穩定版。

### 取得授權
- **Free Trial** – 完整功能試用 30 天。  
- **Temporary License** – 15 天延伸評估授權。  
- **Purchase** – 永久正式授權。

#### 基本初始化
`RedactionEngine` 是用於在塗抹後載入、修改與儲存文件的核心類別。  

```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Further configuration and initialization...
```

## 實作指南

我們將解決方案分為三個邏輯部分：建立索引、加入文件（含已塗抹的文件）以及搜尋索引。

### 如何使用 GroupDocs.Search 建立搜尋索引？

`Index` 是 GroupDocs.Search 中代表可搜尋索引的主要類別。您可以透過指向磁碟上的資料夾來載入或建立 `Index` 實例；函式庫會為您管理所有內部檔案。此步驟是 **optimizing search performance** 的基礎，因為良好結構的索引可降低查詢延遲。

```csharp
using GroupDocs.Search;

string indexFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldIndex";
```

**說明：** 這段程式碼定義了用來存放索引檔案的目錄。使用專屬資料夾可將索引資料與來源文件分離。

```csharp
Index index = new Index(indexFolder);
```

**說明：** 建立 `Index` 實例時，若路徑已有索引則會開啟，否則會建立新索引。

### 如何在塗抹後將文件加入索引？

首先，對任何機密段落進行塗抹，然後將乾淨的檔案加入索引。此兩步流程確保只有安全內容可被搜尋。

#### 定義來源資料夾
`documentsFolder` 是原始 PDF 所在的路徑。  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldDocuments";
```

`AddDocument` 是 `Index` 類別的 method，用於將單一文件加入索引。  

```csharp
index.Add(documentsFolder);
```

### 如何在已建立的索引中搜尋？

指定查詢字串、執行搜尋，並遍歷結果。API 會回傳頁碼、摘要與文件識別碼，方便在 UI 中呈現結果。

`SearchResult` 保存查詢回傳的結果，包含符合的文件與摘要。  

```csharp
string query = "Lorem";
```

```csharp
SearchResult result = index.Search(query);
```

## 實務應用

這些功能可解決實務中的問題：

1. **Legal Document Management** – 在索引案件檔案前塗抹客戶姓名，確保隱私，同時律師仍能搜尋案例法。  
2. **Healthcare Records** – 從醫療 PDF 中移除患者識別資訊，然後索引已清理的版本，以快速進行稽核查詢。  
3. **Corporate Compliance** – 自動塗抹財務報表，並立即使乾淨的版本可供內部調查搜尋。

## 效能考量

在處理大量資料時，為了 **optimize search performance**：

- 將索引作業作為背景工作執行，並以批次提交變更。  
- 及時釋放 `Index` 物件，以釋放非受控資源。  
- 監控記憶體使用情況；GroupDocs.Search 以串流方式處理資料，從不將整份文件載入記憶體。  
- 定期安排索引合併，以保持索引緊湊且查詢快速。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **巨型 PDF 的記憶體不足錯誤** | 使用啟用串流模式的 `RedactionEngine` 搭配 `RedactionOptions`。 |
| **搜尋返回已塗抹的詞彙** | 確保在呼叫 `Index.AddDocument` 之前先執行塗抹。 |
| **不支援的檔案格式** | 確認檔案副檔名屬於 50+ 種支援的格式；若不支援，請先轉換為 PDF。 |
| **授權未被識別** | 將授權檔案放置於應用程式根目錄，並在任何 API 使用前呼叫 `License.SetLicense("license.json")`。 |

## 常見問答

**Q: 是否可以直接在 C# 中塗抹 PDF 檔案而無需先轉換？**  
A: 可以 — `RedactionEngine` 原生支援 PDF 串流，您可以載入 PDF、套用塗抹物件，並在不進行任何格式轉換的情況下儲存結果。

**Q: Adding documents to index 如何影響搜尋速度？**  
A: 增量索引僅加入新檔案，使索引大小保持穩定，對於一般工作負載查詢延遲維持在 200 ms 以下。

**Q: 是否可以排程自動重新索引？**  
A: 當然可以。使用 Windows Service 或 Azure Function 於定時器觸發時呼叫 `Index.AddDocument`，將新上傳的檔案加入索引。

**Q: 塗抹是否永久移除隱藏資料？**  
A: 是的 — 塗抹會覆寫原始位元組，即使使用鑑識工具也無法復原。

**Q: 完全支援哪些 .NET 版本？**  
A: 正式支援 .NET Framework 4.6.1+ 以及 .NET Core 3.1+（含 .NET 5/6）。

## 資源
- [文件說明](https://docs.groupdocs.com/search/net/)
- [API 參考](https://reference.groupdocs.com/redaction/net)
- [下載](https://releases.groupdocs.com/search/net/)
- [免費支援](https://forum.groupdocs.com/c/search/10)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

**最後更新：** 2026-07-02  
**測試環境：** GroupDocs.Search 21.2 and GroupDocs.Redaction 21.1 for .NET  
**作者：** GroupDocs

## 相關教學

- [精通 GroupDocs.Redaction .NET：高效索引建立與別名管理以進階文件搜尋](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [如何在 .NET 中使用 GroupDocs.Redaction 依主題索引與搜尋 PDF/Word 文件](/search/net/indexing/index-search-pdf-word-subject-groupdocs-redaction/)
- [精通 GroupDocs Search 與 Redaction 在 .NET 中的應用：進階文件管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)