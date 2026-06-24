---
date: '2026-04-04'
description: 學習如何使用 GroupDocs.Search 搜尋法律文件及管理索引，並在 .NET 中使用 GroupDocs.Redaction 整合醫療記錄的遮蔽功能。
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: 使用 GroupDocs Search & Redaction for .NET 搜尋法律文件
type: docs
url: /zh-hant/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# 在 .NET 中使用 GroupDocs Search 與 Redaction 搜尋法律文件

在今天的資料驅動環境中，**搜尋法律文件**快速且安全是任何組織的關鍵需求。無論您在處理合約、法院文件或合規報告，GroupDocs.Search 為您提供快速、可擴展的索引，而 GroupDocs.Redaction 則確保敏感資訊保持隱蔽。本教學將指導您設定可搜尋的索引、從多個資料夾加入文件，以及設定遮蔽，以便安全搜尋醫療記錄和其他機密檔案。

## 快速解答
- **GroupDocs.Search 的功能是什麼？** 它會為各種文件格式建立全文可搜尋的索引。  
- **我可以在搜尋前先遮蔽資訊嗎？** 可以 – 使用 GroupDocs.Redaction 來遮蔽或移除敏感資料。  
- **如何將文件加入索引？** 呼叫 `index.Add("folderPath")` 以加入每個資料夾。  
- **支援哪些檔案類型？** PDF、DOCX、PPTX、TXT 等多種格式。  
- **生產環境是否需要授權？** 可使用臨時試用版；商業使用需購買永久授權。

## 前置條件
請確保您已具備以下條件以跟隨本教學：
- .NET Core SDK（3.1 或更新版本）已安裝。  
- Visual Studio Code、Visual Studio，或其他支援 .NET 的 IDE。  
- 具備基本的 C# 程式開發知識。

### 取得授權
您可以先使用兩個函式庫的免費試用版。若需長期使用，請考慮取得臨時授權或從 [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) 購買授權。

## 安裝必要套件

**GroupDocs.Search 安裝：**  
使用 **.NET CLI**，執行：
```bash
dotnet add package GroupDocs.Search
```
或者，在 Visual Studio 中使用套件管理員主控台：
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction 安裝：**  
- 使用 .NET CLI：
```bash
dotnet add package GroupDocs.Redaction
```
- 或使用套件管理員：
```powershell
Install-Package GroupDocs.Redaction
```

若偏好圖形介面，請前往 NuGet 套件管理員 UI，搜尋 "GroupDocs.Redaction" 進行安裝。

## 設定 Redactor 參數
在開始遮蔽之前，您可能想微調 Redactor 行為（例如設定遮蔽顏色或自訂模式）。以下程式碼片段展示了基本的初始化：

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **專業提示：** 調整 `redactorSettings` 以符合貴組織的合規政策（例如以黑框取代文字、在遮蔽前套用 OCR 等）。

## 實作指南

### 如何搜尋法律文件？
建立可搜尋的索引是快速檢索法律文件的基礎。GroupDocs.Search 允許您指向任意資料夾、建立索引，並對成千上萬的檔案執行複雜查詢。

### 如何將文件加入索引
加入文件相當簡單——只需將函式庫指向保存檔案的目錄。您可以加入多個資料夾，當法律文檔散佈於不同位置時非常方便。

#### 建立與管理索引
**概述：**  
建立索引是高效文件搜尋作業的第一步。GroupDocs.Search 允許您在任意目錄建立可搜尋的索引，實現文件的快速檢索。

##### 步驟 1：建立索引
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*說明：* `Index` 會在指定目錄初始化搜尋索引。請確保路徑符合您專案的資料夾結構。

##### 步驟 2：將文件加入索引
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*說明：* `Add` 方法會掃描給定的資料夾，將所有支援的文件納入索引。可用於從多個來源（如合約、案件檔案或醫療記錄）**將文件加入索引**。

### 取得與顯示索引報告
**概述：**  
索引報告可讓您了解處理的文件數量、總詞彙數以及儲存空間大小——這些都是效能調校的關鍵指標。

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*說明：* `GetIndexingReports` 會回傳一個報告陣列，詳細說明索引過程，協助您監控與優化效能。

## 實務應用
1. **法律文件管理：** 自動為案件檔案建立索引，以即時檢索法規、簡報與判決。  
2. **醫療記錄系統：** 使用 GroupDocs.Redaction 遮蔽個人健康資訊（PHI），在保護隱私的同時搜尋患者記錄。  
3. **企業人力資源門戶：** 結合可搜尋的員工檔案與遮蔽功能，以保護個人資料。

## 效能考量
- **優化索引大小：** 定期清除過時條目並重新建立索引，以保持精簡。  
- **記憶體管理：** 利用 .NET 的垃圾回收機制；在不再需要時釋放 `Index` 物件。  
- **可擴充性最佳實踐：** 將索引存放於高速 SSD，並考慮將大型文庫分割至多個索引。

## 常見問題

**Q: GroupDocs.Search 的主要用途是什麼？**  
A: 它非常適合從大型文件集合建立可搜尋的索引，實現法律與醫療檔案的快速檢索。

**Q: GroupDocs.Redaction 如何確保資料隱私？**  
A: 它允許您定義遮蔽模式，於文件被索引或分享前永久移除或遮蔽敏感資訊。

**Q: 我可以在雲端環境使用這些函式庫嗎？**  
A: 可以——兩個函式庫皆可在 Azure、AWS 或任何具備適當授權的容器化 .NET 部署中使用。

**Q: GroupDocs.Search 支援哪些檔案格式？**  
A: PDF、Word、Excel、PowerPoint、TXT、HTML 等多種企業格式。

**Q: 如何排除索引錯誤？**  
A: 核對資料夾路徑、檢查檔案權限，並檢視 `IndexingReport` 的主控台輸出以取得具體錯誤代碼。

## 資源
- **文件說明：** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API 參考：** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **下載：** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **免費支援：** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權：** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2026-04-04  
**測試版本：** GroupDocs.Search 23.12、GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs