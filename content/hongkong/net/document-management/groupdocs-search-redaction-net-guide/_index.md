---
date: '2026-04-27'
description: 學習如何在 .NET 中使用 GroupDocs.Search 與 Redaction 進行敏感資料的遮蔽，並了解如何將文件加入索引以搜尋大型文件。
keywords:
- redact sensitive data
- add documents to index
- search large documents
title: GroupDocs.Search 與 .NET 中的資料遮蔽 – 遮蔽敏感資料
type: docs
url: /zh-hant/net/document-management/groupdocs-search-redaction-net-guide/
weight: 1
---

# GroupDocs.Search 與 Redaction 在 .NET 中 – 敏感資料遮蔽

管理大量文件可能令人望而生畏，尤其是當您需要 **遮蔽敏感資料** 同時仍提供快速搜尋功能時。本指南將逐步說明如何設定 GroupDocs.Search 與 GroupDocs.Redaction，展示如何 **將文件加入索引**、執行高效的 **搜尋大型文件** 操作，並確保所有內容符合隱私要求。

## 快速解答
- **What does “redact sensitive data” mean?** 它表示永久移除或遮蔽文件中的機密資訊。  
- **Which libraries do I need?** GroupDocs.Search and GroupDocs.Redaction for .NET (available via NuGet).  
- **Can I index .NET projects automatically?** 是 – 請參閱 “How to index .NET” 章節以獲得逐步指引。  
- **How do I handle huge files?** 使用基於區塊的搜尋，以可管理的方式處理資料。  
- **Is a license required for production?** 生產環境需要有效的 GroupDocs 授權；亦提供免費試用。

## 什麼是遮蔽敏感資料？
遮蔽敏感資料是指永久移除或隱蔽文件中的個人、財務或機密資訊，使其無法被未授權的使用者恢復或檢視。

## 為何將 GroupDocs.Search 與 Redaction 結合？
- **Speed:** 建立可搜尋的索引，於毫秒內返回結果。  
- **Security:** 在文件共享或儲存前套用遮蔽規則。  
- **Scalability:** 區塊搜尋讓您在不耗盡記憶體的情況下處理 TB 級文字。  
- **Compliance:** 符合 GDPR、HIPAA 及其他法規，確保機密資料不外洩。

## 先決條件
- .NET 開發環境（建議使用 Visual Studio）。  
- 基本的 C# 知識。  
- 可使用 NuGet 安裝所需套件。

## 設定 GroupDocs.Redaction for .NET

### 透過 .NET CLI 安裝
```bash
dotnet add package GroupDocs.Redaction
```

### Package Manager 安裝
```powershell
Install-Package GroupDocs.Redaction
```

### NuGet 套件管理員 UI
搜尋 **"GroupDocs.Redaction"** 並安裝最新版本。

### 授權取得步驟
- **Free Trial:** 先使用免費試用以探索功能。  
- **Temporary License:** 申請臨時授權以延長使用。  
- **Purchase:** 考慮購買以供長期生產使用。

### 基本初始化與設定
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## 實作指南

### 如何使用 GroupDocs.Search 索引 .NET 專案
以下我們將實作分解為清晰的編號步驟，讓您輕鬆跟隨。

#### 步驟 1：指定索引資料夾
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*Why?* 定義專用資料夾可保持索引有序，且與原始文件分離。

#### 步驟 2：建立並設定索引
```csharp
Index index = new Index(indexFolder);
```
*Purpose:* 在您指定的位置實例化新的可搜尋索引。

#### 步驟 3：**將文件加入索引**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*Explanation:* 每次呼叫皆會將檔案（或資料夾）加入索引，使其內容可被搜尋。

### 使用區塊搜尋搜尋大型文件
區塊搜尋允許您將龐大檔案切分為較小的片段，以降低記憶體使用量。

#### 步驟 1：定義搜尋查詢
```csharp
string query = "invitation";
```
*Purpose:* 您在所有已索引檔案中尋找的關鍵字。

#### 步驟 2：設定區塊搜尋選項
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*Explanation:* 啟用 `IsChunkSearch` 會指示引擎以區塊方式處理資料。

#### 步驟 3：執行初始搜尋
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*Result:* 顯示包含該關鍵字的文件數量以及總共發現的次數。

#### 步驟 4：繼續處理後續區塊
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*Why this loop?* 確保您從每個區塊取得結果，直至整個資料集處理完畢。

### 如何使用 GroupDocs.Redaction 遮蔽敏感資料
在定位到需要保護的資訊後，套用遮蔽規則。

#### 步驟 1：初始化遮蔽設定
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### 步驟 2：套用遮蔽
使用 `Redactor` 類別（此處未顯示以保持原始程式碼完整）來定義您想遮蔽的模式、文字或影像。  
*Pro tip:* 先在文件副本上測試遮蔽規則，以免意外資料遺失。

## 實務應用
這些功能在多個產業中大放異彩：

1. **Legal Document Management** – 快速搜尋案件檔案，同時遮蔽客戶機密細節。  
2. **Healthcare Data Handling** – 保護患者 PHI，同時讓臨床醫師能找到相關記錄。  
3. **Financial Auditing** – 索引大量交易日誌，並遮蔽帳號或個人識別資訊。

## 效能考量
- **Optimize Indexing:** 僅重新索引變更的檔案，以保持索引新鮮且避免不必要的工作。  
- **Manage Resources:** 根據伺服器 RAM 調整區塊大小 (`options.ChunkSize`)。  
- **Async Operations:** 對於大型批次，使用非同步索引以保持 UI 響應。

## 常見問題

**Q: How do I handle large files efficiently?**  
A: 使用基於區塊的搜尋 (`IsChunkSearch = true`) 以較小的片段處理資料，降低記憶體壓力。

**Q: Can GroupDocs.Redaction work with encrypted documents?**  
A: 可以 – 先解密檔案，套用遮蔽，必要時再重新加密。

**Q: What licensing options are available?**  
A: 免費試用、評估用臨時授權，以及生產環境的完整商業授權。

**Q: How can I troubleshoot index errors?**  
A: 確認索引資料夾路徑正確，確保應用程式具備讀寫權限，並檢查所有文件格式是否受支援。

**Q: Is it possible to customize search queries further?**  
A: 當然可以。您可使用 `SearchOptions` API 結合布林運算子、萬用字元與相近搜尋。

## 資源
- **Documentation:** [GroupDocs Redaction .NET 文件](https://docs.groupdocs.com/search/net/)  
- **API Reference:** [GroupDocs Redaction API 參考](https://reference.groupdocs.com/redaction/net)  
- **Download:** [最新發行版](https://releases.groupdocs.com/search/net/)  
- **Free Support:** [GroupDocs 論壇](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [此處申請](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-04-27  
**測試版本：** GroupDocs.Search 23.9 與 GroupDocs.Redaction 23.9 for .NET  
**作者：** GroupDocs