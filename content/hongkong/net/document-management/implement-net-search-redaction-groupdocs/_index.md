---
date: '2026-06-12'
description: 了解如何在 .NET 中使用 GroupDocs.Search 與 GroupDocs.Redaction 進行文件搜尋與遮蔽，優化搜尋效能並處理索引錯誤。
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: 如何在 .NET 中使用 GroupDocs.Search 與 GroupDocs.Redaction 搜尋與遮蔽文件
type: docs
url: /zh-hant/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# 在 .NET 中使用 GroupDocs.Search 與 GroupDocs.Redaction 進行文件搜尋與遮蔽

在現代企業環境中，**search and redact** 功能對於保護敏感資訊同時讓文件易於搜尋至關重要。本教學將帶領您建立一個結合 GroupDocs.Search 進行快速全文搜尋與 GroupDocs.Redaction 安全移除機密資料的 .NET 解決方案。完成後，您將了解如何設定函式庫、建立自訂文字分段器、執行高效能搜尋，以及安全地套用遮蔽。

## 快速解答
- **什麼是「search and redact」？** 它表示在文件中尋找文字並永久遮蔽。  
- **需要哪些函式庫？** GroupDocs.Search and GroupDocs.Redaction for .NET.  
- **我可以處理多語言內容嗎？** 可以——使用自訂文字分段器正確切分詞彙。  
- **如何提升搜尋速度？** 一次建立索引，重複使用該索引，並啟用 `optimize search performance` 設定。  
- **如果索引失敗該怎麼辦？** 請遵循故障排除章節中的「handle indexing errors」指引。  

## 什麼是「search and redact」？
Search and redact 是在文件集合中定位特定詞彙，然後永久隱蔽或移除這些詞彙，以保護隱私或符合規範要求的過程。它結合了全文搜尋以找出敏感資訊，並使用遮蔽工具在保留文件原始版面配置的同時取代內容。

## 為何同時使用 GroupDocs.Search 與 GroupDocs.Redaction？
GroupDocs.Search 支援 **50+ 檔案格式**，且能在一般伺服器硬體上於一分鐘內索引 **100,000+ 文件**，而 GroupDocs.Redaction 可對 **PDF、DOCX、PPTX 等** 檔案套用遮蔽，且不會改變原始版面配置。將兩者結合即可提供單一解決方案，**優化搜尋效能** 並 **優雅處理索引錯誤**。

## 前置條件
- Visual Studio 2022 或更新版本，支援 .NET 6+。  
- NuGet 套件：**GroupDocs.Search** 與 **GroupDocs.Redaction**（最新穩定版）。  
- 有效的 GroupDocs 授權（試用或購買）。  

### 必要函式庫
- **GroupDocs.Search** – 提供索引、查詢與自訂分段功能。  
- **GroupDocs.Redaction** – 提供文字、影像與中繼資料的遮蔽，支援所有支援的格式。  

### 環境設定需求
確保開發機器對索引將儲存的資料夾具有寫入權限。

### 知識前置條件
- 熟悉 C# 與 .NET 專案結構。  
- 基本了解文件處理概念（非必須但有助）。  

## 如何在 .NET 中安裝 GroupDocs.Redaction？
您可以使用 .NET CLI 或 NuGet 套件管理員將 Redaction 套件加入專案。此指令會下載最新穩定版並註冊於專案檔，使 API 可立即使用。  

```bash
dotnet add package GroupDocs.Redaction
```  

## 如何取得 GroupDocs 授權？
GroupDocs 提供三種授權方案：供評估使用的免費試用、供延長開發測試的臨時授權，以及供正式上線的完整商業授權。試用版功能有限，臨時金鑰可延長評估期間，購買授權則解鎖全部功能並提供優先支援。

## 如何在應用程式中初始化 GroupDocs.Redaction？
`Redaction` 類別是對支援文件套用遮蔽的主要入口。它會載入檔案、準備遮蔽物件，並執行遮蔽程序，返回保留原始版面配置的修改後文件。您亦可設定遮蔽選項，例如顏色、覆蓋層與中繼資料移除，以符合特定合規需求。  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## 如何使用 GroupDocs.Search 建立索引？
`Index` 類別代表儲存在磁碟上的可搜尋儲存庫。它管理索引的建立、更新與查詢，讓您能新增文件、重建索引，並在大型集合中執行快速搜尋。索引資料夾可放於本機或網路儲存，且您可設定壓縮與加密以保護索引資料。  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## 什麼是自訂文字分段器，為何要使用它？
自訂文字分段器決定原始文字如何切分為可搜尋的標記。透過為特定語言或領域客製化分段規則，可提升分詞準確度，進而提升搜尋結果的召回率與相關性。這對於具有複雜詞界的語言（如日文或阿拉伯文）特別有用，因為預設分詞器可能會錯誤切分詞彙。  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## 如何使用自訂分段器執行全文搜尋？
`SearchQuery` 物件封裝使用者的查詢，並與自訂分段器合作定位匹配項目。它支援模糊匹配、片語查詢與加權，返回包含文件 ID、命中位置與相關性分數的結果集。您亦可套用檔案類型或日期範圍等過濾條件，以縮小結果範圍，達到更精確的目標。  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## 找到敏感文字後，如何套用遮蔽？
`Redaction` API 讓您在支援的文件中取代或移除文字、影像與中繼資料。識別出敏感詞彙後，建立遮蔽物件、套用並儲存遮蔽檔案，確保機密資訊永久隱藏。遮蔽選項包括覆蓋黑框、使用自訂顏色，或在保留文件結構的同時移除整個物件。  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## 常見問題與索引錯誤處理方式
- **索引未找到:** 請確認索引路徑存在且應用程式具有讀寫權限。  
- **搜尋無結果:** 重新執行索引程序，並確保自訂分段器已正確註冊。  
- **某些格式的遮蔽失敗:** 確認檔案類型受支援；對於 PDF，請使用最新的 Redaction 版本以處理 PDF 2.0 功能。  

## 實務應用
1. **法律文件管理：** 在合約中搜尋「non‑disclosure」並在外部分享前自動遮蔽相關條款。  
2. **學術研究：** 在手稿中定位未發表的資料，並在同行審查過程中隱藏。  
3. **商業合約：** 批次處理數千份協議，遮蔽個人識別資訊，同時保留法律用語。  

## 如何優化大型文件集合的搜尋效能？
為了最大化效能，請一次索引文件並在後續查詢中重複使用同一索引。啟用平行處理、設定快取，並調整索引設定以降低延遲、提升多核心伺服器的吞吐量。此外，設定 `EnableMemoryMapping` 標誌，使索引以記憶體映射方式載入，從而加速大型資料集的讀取操作。

## 處理大型檔案時，如何管理 .NET 記憶體？
有效的記憶體管理在處理大型文件時至關重要。將 `Index` 與 `Redaction` 物件置於 `using` 陳述式中，以確保即時釋放，並以串流方式處理檔案，避免一次將整個文件載入記憶體。監控效能計數器有助於及早偵測記憶體峰值，讓您調整批次大小或啟用垃圾回收調校。

## 常見問答
**Q: 我可以在 GroupDocs.Search 中使用非文字型中繼資料嗎？**  
A: 可以——中繼資料欄位可與文件內容一起索引，允許類似 “author:JohnDoe” 的搜尋。  

**Q: GroupDocs.Redaction 支援在 Web API 中即時遮蔽嗎？**  
A: 支援；您可以同步呼叫 Redaction API 處理小檔案，或將較大的工作排入佇列以非同步方式處理。  

**Q: 如果索引損毀，我該怎麼辦？**  
A: 刪除損毀的索引資料夾，並使用相同的索引流程重新建置；函式庫會記錄詳細錯誤訊息，協助您找出原因。  

**Q: 是否可以在儲存前預覽遮蔽後的文件？**  
A: 當然可以——呼叫 `redaction.Apply()` 並加上 `preview` 旗標，即可產生供檢視的暫存版本。  

**Q: 官方支援哪些 .NET 版本？**  
A: GroupDocs.Search 與 GroupDocs.Redaction 支援 .NET 6、.NET 5、.NET Core 3.1 以及 .NET Framework 4.6.2 以上版本。  

## 資源
- **文件說明：** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)  
- **API 參考：** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **下載：** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **免費支援：** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權：** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2026-06-12  
**測試環境：** GroupDocs.Search 23.11、GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## 相關教學
- [精通 GroupDocs Search 與 Redaction 在 .NET：進階文件管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [實作 GroupDocs.Search 與 Redaction：在 .NET 中更新與管理文件索引](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [使用 GroupDocs.Redaction 優化 .NET 文件索引：取消、非同步與執行緒](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)