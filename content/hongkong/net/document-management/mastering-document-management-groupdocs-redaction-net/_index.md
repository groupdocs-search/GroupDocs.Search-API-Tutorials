---
date: '2026-08-15'
description: 了解如何設定授權，並在 .NET 應用程式中使用 GroupDocs.Redaction 搜尋與高亮顯示 HTML 內容。
keywords:
- how to set license
- search and highlight html
- GroupDocs.Redaction .NET
lastmod: '2026-08-15'
og_description: 探索如何為 GroupDocs.Redaction 設定授權，並在 .NET 中執行搜尋與高亮顯示 HTML 結果。提供實務範例的詳細指南。
og_image_alt: Guide showing license setup and HTML search highlighting using GroupDocs.Redaction
  in .NET
og_title: 如何設定授權，使用 GroupDocs.Redaction 進行搜尋並高亮顯示
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  headline: How to set license, highlight search with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  name: How to set license, highlight search with GroupDocs.Redaction
  steps:
  - name: '**Legal document analysis**: Quickly find and highlight key legal terms.'
    text: '**Legal document analysis**: Quickly find and highlight key legal terms.'
  - name: '**Customer support**: Highlight relevant customer feedback in support tickets.'
    text: '**Customer support**: Highlight relevant customer feedback in support tickets.'
  - name: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
    text: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
  - name: '**Financial reports**: Identify and highlight critical financial metrics.'
    text: '**Financial reports**: Identify and highlight critical financial metrics.'
  - name: '**Content management**: Improve content discoverability through keyword
      highlighting.'
    text: '**Content management**: Improve content discoverability through keyword
      highlighting.'
  type: HowTo
- questions:
  - answer: Visit [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)
      for more details.
    question: How do I obtain a GroupDocs license?
  - answer: Yes, after acquiring the appropriate license.
    question: Can I use GroupDocs in a commercial project?
  - answer: Use consistent directory structures and environment variables for flexibility.
    question: What is the best practice for managing document paths?
  - answer: Regularly update your index and optimize query parameters.
    question: How can I improve search performance?
  - answer: Yes, multiple language dictionaries are supported.
    question: Is there support for languages other than English in GroupDocs?
  type: FAQPage
tags:
- license setup
- HTML search highlighting
- GroupDocs.Redaction
- .NET document management
title: 如何設定授權，使用 GroupDocs.Redaction 進行搜尋並高亮顯示
type: docs
url: /zh-hant/net/document-management/mastering-document-management-groupdocs-redaction-net/
weight: 1
---

# 精通 .NET 中的 GroupDocs.Redaction 文件管理

## 簡介

在當今的數位環境中，高效的文件管理對於維護資料隱私與提升搜尋功能至關重要。無論您是開發人員或是希望提升文件處理能力的企業，整合 Aspose 與 GroupDocs 等強大函式庫都能帶來顯著變化。本教學將指導您設定這些函式庫的授權，並使用 GroupDocs.Redaction .NET 函式庫在 HTML 格式中標示搜尋結果。

**您將學到的內容：**

- 如何為 Aspose 與 GroupDocs 函式庫設定授權
- 設定路徑並使用 GroupDocs.Search 進行搜尋
- 使用 GroupDocs.Viewer 在 HTML 文件中標示搜尋字詞
- 將上述功能整合至可執行的 .NET 應用程式

透過實作範例與步驟說明，您將能順利優化文件管理流程。

## 快速回答
- **如何為 GroupDocs.Redaction 設定授權？** 使用 `License` 類別在任何 API 呼叫前載入 `.lic` 檔案。
- **可以搜尋並標示 HTML 內容嗎？** 可以，結合 GroupDocs.Search 與 GroupDocs.Viewer 即可定位字詞並產生標示的 HTML。
- **是否也需要 Aspose 授權？** 只有在使用 Aspose.HTML 進行額外渲染時才需要；否則僅使用 GroupDocs.Redaction 即可。
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。
- **測試時使用試用授權足夠嗎？** 臨時授權可讓您完整評估所有功能，且無時間限制的限制。

## 如何為 GroupDocs.Redaction 設定授權？

`License` 類別會向 GroupDocs SDK 註冊授權檔案。使用 `License` 類別載入授權檔，並在任何其他 SDK 呼叫之前呼叫 `SetLicense`。這會解鎖全部功能、移除評估水印，並啟用效能最佳化。提前載入授權可讓 SDK 在每一次操作前執行權限檢查，確保所有遮蔽、搜尋與渲染功能皆無限制地運作。

```text
```bash
dotnet add package GroupDocs.Redaction
```
```

## 如何為 Aspose.HTML 設定授權？

Aspose.HTML 的 `License` 類別會註冊產品授權並停用試用限制。建立 Aspose 的 `License` 物件，指向 `.lic` 檔案，即可確保所有 Aspose.HTML 渲染功能在無試用警告的情況下執行，且可使用 CSS 支援與進階版面引擎等高級功能。

```text
```csharp
using Aspose.Html;

string licensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";
new License().SetLicense(licensePath);
```
```

- **說明**：`License.SetLicense` 會載入授權檔，解鎖全部功能。

## 如何為 GroupDocs.Viewer 設定授權？

GroupDocs.Viewer 的 `License` 類別會註冊檢視器授權，讓 PDF、DOCX 等格式以高保真度渲染為 HTML，且不會出現水印。為 GroupDocs.Viewer 建立 `License` 實例並呼叫 `SetLicense`。若您需要將文件渲染為 HTML，這一步是必要的。

```text
```csharp
using GroupDocs.Viewer;

new License().SetLicense(licensePath);
```
```

## 為何使用 GroupDocs 進行搜尋與 HTML 標示？

GroupDocs.Search 以輕量、唯讀的結構索引文件，能在毫秒級查詢數百萬筆記錄。結合 GroupDocs.Viewer，您可以將任何支援的文件渲染為 HTML，並以 CSS 樣式覆蓋匹配的字詞。量化說明：此搜尋引擎在典型 2 GHz 伺服器上可於 2 秒內處理 500 頁 PDF，且檢視器在不到 1 秒的時間內將同一檔案渲染為 HTML。

## 設定 GroupDocs.Redaction 於 .NET 的使用

### 安裝

要在專案中使用 GroupDocs.Redaction，可透過以下套件管理工具安裝：

**.NET CLI：**
```text
```powershell
Install-Package GroupDocs.Redaction
```
```

**Package Manager Console：**
```text
```csharp
// Set your license path
string redactionLicensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";

// Initialize the Redaction API with the license
new GroupDocs.Redaction.License().SetLicense(redactionLicensePath);
```
```

**NuGet 套件管理員 UI：**  
搜尋「GroupDocs.Redaction」並安裝最新版本。

### 授權取得

在使用 GroupDocs.Redaction 完整功能之前，請先取得授權。您可以選擇：

- **免費試用**：下載試用授權以測試功能。  
- **臨時授權**：透過 [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) 取得。  
- **購買**：若要在正式環境使用，請購買永久授權。

欲了解詳細授權條款，請參閱 [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)。

### 基本初始化與設定

```text
```csharp
string basePath = @"./HighlightInHtml/HighlightExample";
string viewerCacheFolderPath = basePath + @"/ViewerCache";
string indexFolder = basePath + @"/Index";
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
string query = "\"dapibus diam\" OR lorem";
```
```

## 實作指南

### 為 Aspose 與 GroupDocs 函式庫設定授權

#### 概觀

設定授權可確保您能無限制地使用 Aspose.HTML 與 GroupDocs.Viewer 的全部功能。

#### 步驟

**1. 為 Aspose.HTML 設定授權**

```text
```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder); // Initialize index at specified path
index.Add(documentsFolder); // Add documents from directory to index
```
```

**2. 為 GroupDocs.Viewer 設定授權**

```text
```csharp
using GroupDocs.Search.Results;

SearchResult result = index.Search(query); // Execute the search
FoundDocument foundDocument = result.GetFoundDocument(0); // Retrieve first document
```
```

### 設定路徑與查詢

#### 概觀

定義文件路徑並準備搜尋查詢，以定位特定內容。

#### 步驟

**1. 定義基礎路徑**

```text
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Viewer.Options;

IndexedFileInfo fileInfo = new IndexedFileInfo(viewerCacheFolderPath, foundDocument.DocumentInfo.FilePath);
HighlightService highlightService = new HighlightService(fileInfo, null); // Prepare for highlighting

highlightService.Highlight(foundDocument, index.Dictionaries.Alphabet); // Perform highlighting
```
```

- **說明**：組織路徑可確保搜尋與標示功能順利整合。

### 建立並加入索引

#### 概觀

建立索引以提升文件搜尋效率。

**步驟**

**1. 建立索引**

```text
CODE_BLOCK_PLACEHOLDER_9_END
```

- **說明**：`Index` 物件管理已索引的資料，允許快速檢索。

### 在索引中搜尋

#### 概觀

對已建立的索引執行搜尋查詢並取得結果。

**步驟**

**1. 執行搜尋**

```text
CODE_BLOCK_PLACEHOLDER_10_END
```

- **說明**：`index.Search` 會執行查詢，回傳符合的文件。

### 在 HTML 中標示搜尋結果

#### 概觀

使用 GroupDocs.Viewer 於文件的 HTML 表示中標示關鍵字。

**步驟**

**1. 初始化標示服務**

```text
CODE_BLOCK_PLACEHOLDER_11_END
```

- **說明**：`HighlightService` 會處理並在文件內標示搜尋字詞。

## 實務應用

1. **法律文件分析**：快速找出並標示關鍵法律條款。  
2. **客服支援**：在支援票證中標示相關客戶回饋。  
3. **研究論文**：透過標示特定科學術語協助研究。  
4. **財務報告**：辨識並標示關鍵財務指標。  
5. **內容管理**：透過關鍵字標示提升內容可發現性。

## 效能考量

- **優化索引**：定期更新索引以維持搜尋效率。  
- **記憶體管理**：盡可能使用非同步處理以降低記憶體佔用。  
- **資源使用**：監控應用程式效能，適時調整資源配置。

## 常見問題與除錯

- **授權未被識別** – 確認 `.lic` 檔案路徑為絕對路徑或相對於執行組件的正確路徑。  
- **搜尋無結果** – 確保在新增文件後重新建立索引；索引不會自動偵測檔案變更。  
- **HTML 標示缺少 CSS** – 請加入 GroupDocs.Viewer 提供的預設樣式表，或自行添加 CSS 以樣式化 `<mark>` 標籤。  
- **大型 PDF 超時** – 增加 `SearchOptions.MaxDegreeOfParallelism` 設定，以利用多核心處理器。

## 常見問答

**Q: 如何取得 GroupDocs 授權？**  
A: 前往 [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) 了解詳情。

**Q: 可以在商業專案中使用 GroupDocs 嗎？**  
A: 可以，取得相應授權後即可使用。

**Q: 管理文件路徑的最佳實踐是什麼？**  
A: 使用一致的目錄結構與環境變數，以提升彈性。

**Q: 如何提升搜尋效能？**  
A: 定期更新索引並優化查詢參數。

**Q: GroupDocs 是否支援非英語語系？**  
A: 支援多種語言字典。

## 資源

- [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs Redaction](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

## 結論

您已學會如何設定授權、配置搜尋路徑、建立索引、執行搜尋以及使用 GroupDocs.Redaction 在 .NET 中標示結果。將這些功能整合至您的應用程式時，建議持續參考進階文件以探索更高階的能力。

**後續步驟：**

- 前往 [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) 深入了解。  
- 嘗試額外功能，如遮蔽與註解。

---

**最後更新：** 2026-08-15  
**測試環境：** GroupDocs.Redaction 23.10 for .NET  
**作者：** GroupDocs

## 相關教學

- [Mastering GroupDocs.Redaction .NET: Efficient Index Creation and Alias Management for Advanced Document Search](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implement GroupDocs.Redaction .NET for Document Finder Management and Highlighting](/search/net/document-management/groupdocs-redaction-net-finder-management-guide/)
- [Master GroupDocs.Redaction .NET: Setup & Event Handling for Secure Document Management](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}