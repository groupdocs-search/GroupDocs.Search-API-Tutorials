---
date: '2026-06-07'
description: 了解如何在 .NET 應用程式中使用 GroupDocs.Search 與 GroupDocs.Redaction，實作高壓縮 .NET
  以儲存文字並遮蔽機密資料。
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 使用 GroupDocs 實作高壓縮 .NET：文字與遮蔽指南
type: docs
url: /zh-hant/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# 實作高壓縮 .NET 與 GroupDocs：文字與遮蔽指南

在現代 .NET 解決方案中，**implement high compression .net** 在需要儲存大量文字集合而不致佔用過多磁碟空間時是必不可少的。同時，保護敏感資訊——例如個人識別碼或財務數字——需要可靠的遮蔽功能。本教學將一步一步示範如何使用 **GroupDocs.Search** 設定高壓縮文字儲存，以及如何使用 **GroupDocs.Redaction** 安全地遮蔽機密資料。完成後，您將能將索引文字壓縮至最高 90 % 並從 PDF、Word 檔案以及其他多種格式中移除私人內容。

## 快速解答
- **什麼函式庫提供高壓縮索引？** GroupDocs.Search for .NET.  
- **哪個工具可遮蔽敏感資料？** GroupDocs.Redaction for .NET.  
- **我可以自動將文件加入索引嗎？** 可以——在資料夾掃描迴圈中使用 `AddDocument` API。  
- **壓縮對搜尋是否無損？** 是的，壓縮後文字仍可完整搜尋。  
- **生產環境是否需要授權？** 商業使用需購買永久 GroupDocs 授權。

## 「implement high compression .net」是什麼？
Implement high compression .net 指的是設定 GroupDocs.Search 索引引擎，以壓縮形式儲存擷取的文字內容。這可大幅減少磁碟上的索引大小，同時保持文字可完整搜尋。壓縮是無損的，查詢相關性與摘要擷取的表現與未壓縮的索引完全相同。

## 為什麼選擇 GroupDocs 進行壓縮與遮蔽？
GroupDocs.Search 支援超過五十種輸入格式，且可將索引文字壓縮至最高九成，讓大型文件集合只佔原始大小的一小部分。GroupDocs.Redaction 透過永久刪除或遮蔽超過三十種檔案類型的敏感資訊，協助您在不需額外工具的情況下符合 GDPR、HIPAA 等嚴格合規規範。

## 前置條件
- **開發環境：** Visual Studio 2022 或更新版本，.NET 6+（或 .NET Framework 4.7.2）。  
- **函式庫：** `GroupDocs.Search` 與 `GroupDocs.Redaction` NuGet 套件。  
- **權限：** 讀寫包含來源文件及索引輸出位置的資料夾的存取權限。  
- **基礎知識：** C# 語法、檔案 I/O 以及 .NET 專案結構的熟悉度。

## 如何使用 GroupDocs 實作高壓縮 .NET？
要使用 GroupDocs 實作高壓縮 .NET，首先建立 `TextStorageSettings` 實例，並將其 `CompressionLevel` 設為 `High`。接著實例化 `Index` 物件，傳入設定與索引將儲存的資料夾。索引準備好後，使用 `AddDocument` 新增文件，最後以 `Search` 方法執行搜尋，整個過程中引擎會自動處理壓縮與解壓縮。

### 步驟 1：安裝必要的 NuGet 套件
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- 搜尋 “GroupDocs.Search” 並點擊 **Install**。  

### 步驟 2：安裝 GroupDocs.Redaction（用於資料遮蔽）
- 開啟 **NuGet Package Manager**。  
- 搜尋 **GroupDocs.Redaction** 並安裝最新的穩定版。  

### 步驟 3：取得並套用授權
- **免費試用：** 在 GroupDocs 入口網站註冊以取得 30 天試用金鑰。  
- **臨時授權：** 申請開發環境的臨時金鑰。  
- **永久授權：** 購買正式授權以移除評估限制。  

### 步驟 4：兩個函式庫的基本初始化
`Search` 與 `Redaction` 引擎共用相同的授權模式。請在應用程式啟動時初始化它們：

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## 功能 1：高壓縮文字儲存設定

### 設定索引配置
`TextStorageSettings` 是告訴 GroupDocs.Search 如何保存擷取文字的類別。啟用高壓縮可在不影響搜尋速度的情況下將索引大小縮減至最高 **10 倍**。

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**說明：**  
- `CompressionLevel.High` 會啟用基於 ZSTD 的演算法，有效壓縮文字區塊。  
- `UseMemoryCache = false` 使引擎從磁碟串流資料，適合大規模部署。

### 建立與管理索引
`Index` 物件代表磁碟上的可搜尋儲存庫。您需要指定索引檔案的儲存資料夾，並傳入上述的壓縮設定。

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**說明：**  
- `indexFolder` 決定壓縮索引檔案的存放位置。  
- `settings` 注入高壓縮設定，確保每個新增文件皆受惠。

## 功能 2：將文件加入索引

### 將文件加入索引
`AddDocument` 會將單一檔案加入索引，擷取其文字、依設定壓縮，並儲存結果。GroupDocs.Search 能從目錄樹中讀取檔案。以下迴圈會遍歷 `documentsFolder`，將每個檔案加入索引並記錄進度。

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**說明：**  
- `AddDocument` 解析檔案，擷取可搜尋文字，依 `TextStorageSettings` 壓縮，並存入索引。  
- 此方式支援 **PDF、DOCX、TXT、HTML** 以及超過 **30** 種其他格式。

## 功能 3：執行搜尋查詢

### 執行搜尋
`Search` 針對壓縮索引執行查詢，回傳符合條件的 `DocumentResult` 物件集合，包含相關性分數與突顯的摘要。索引建好後，即可執行快速查詢。`Search` 方法會回傳包含檔案路徑與突顯摘要的 `DocumentResult` 物件集合。

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**說明：**  
- 搜尋引擎直接掃描壓縮文字，即使索引包含 **數百萬頁**，查詢延遲仍保持低。  
- `Score` 表示相關性，數值越高代表匹配度越好。

## 如何使用 GroupDocs.Redaction 遮蔽機密資料？
使用 GroupDocs.Redaction 遮蔽機密資料的流程是先為目標檔案建立 `Redactor` 實例。定義一或多個 `SearchPattern` 物件，描述要移除的文字，例如社會安全號碼的正規表達式。使用 `Redact` 套用每個模式，並指定 `RedactionType`（如 `BlackOut`），最後將結果儲存為新文件，確保原始檔案保持不變。

`Redactor` 是 GroupDocs.Redaction 中用於載入文件並執行遮蔽操作的主要類別。  
`SearchPattern` 定義用於識別要遮蔽文字的正規表達式。

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**說明：**  
- `SearchPattern` 使用正規表達式定位社會安全號碼。  
- `RedactionType.BlackOut` 以實心黑色矩形取代匹配文字，確保資料無法復原。

## 實務應用
1. **法律文件管理：** 自動壓縮大量案件檔案，並在歸檔前遮蔽客戶識別資訊。  
2. **醫療紀錄：** 將多年患者筆記儲存於壓縮索引，並在與研究夥伴共享前移除 PHI（受保護健康資訊）。  
3. **財務報告：** 透過遮蔽帳號來保護季報，同時保留可搜尋文字以供稽核查詢。

## 效能考量
- **壓縮影響：** 高壓縮可將索引大小縮減至最高 **90 %**，降低 SSD 磨損並加速備份作業。  
- **記憶體使用量：** 對於極大索引，停用記憶體快取以將程式佔用保持在 **500 MB** 以下。  
- **I/O 最佳化：** 將文件批次加入（每批 100 筆）以減少磁碟抖動。  
- **非同步處理：** 將 `AddDocument` 呼叫包裹於 `Task.Run`，確保桌面應用程式的 UI 執行緒保持回應。

## 常見問題與除錯
- **檔案路徑錯誤：** 確認 `documentsFolder` 與 `indexFolder` 為絕對路徑，且應用程式具備讀寫權限。  
- **授權錯誤：** 確保 `.lic` 檔案與可執行檔一起部署或嵌入為資源。  
- **搜尋無結果：** 檢查 `TextStorageSettings` 的壓縮等級是否與索引時使用的相同；設定不符可能導致反序列化失敗。  

## 常見問答

**Q: 我可以在初始建置後再加入文件到索引嗎？**  
A: 可以——只要對新檔案呼叫 `index.AddDocument`，引擎會以增量方式更新壓縮索引。

**Q: 遮蔽會改變原始檔案嗎？**  
A: 不會——原始檔案保持不變，遮蔽後的版本會另存為新檔案，保留文件完整性。

**Q: GroupDocs.Redaction 支援哪些格式？**  
A: 超過 **30** 種格式，包括 PDF、DOCX、PPTX、XLSX、影像（PNG、JPEG）以及純文字。

**Q: 高壓縮會影響搜尋相關性嗎？**  
A: 不會。文字壓縮是無損的，相關性分數與未壓縮的索引相同。

**Q: 索引文件的大小有上限嗎？**  
A: GroupDocs.Search 可透過串流處理多 GB 的檔案；但請確保有足夠的磁碟空間存放壓縮索引（約為原始大小的 10 %）。

## 資源
- [文件說明](https://docs.groupdocs.com/search/net/)
- [API 參考文件](https://reference.groupdocs.com/redaction/net)
- [下載 GroupDocs.Redaction for .NET](https://releases.groupdocs.com/search/net/)
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)
- [取得臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-06-07  
**測試環境：** GroupDocs.Search 23.12 與 GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs

## 相關教學

- [在 .NET 中實作 GroupDocs.Search 與 Redaction 於文件管理](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [如何優化 GroupDocs.Redaction for .NET：高效索引與拼寫管理指南](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [精通 GroupDocs Redaction 與 Search in .NET：高效文件管理與安全搜尋](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)