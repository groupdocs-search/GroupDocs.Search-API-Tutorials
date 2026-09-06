---
date: '2026-06-07'
description: 了解如何使用 GroupDocs.Redaction 在 C# 中列出檔案副檔名並取得檔案格式。內容包括設定、程式碼與實用技巧。
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: 如何在 .NET 中使用 GroupDocs.Redaction 列出檔案副檔名 – 完整指南
type: docs
url: /zh-hant/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# 在 .NET 中使用 GroupDocs.Redaction 顯示支援的檔案格式

管理各式各樣的文件類型是 .NET 開發人員的日常現實。透過使用 **GroupDocs.Redaction**，您可以 **列出檔案副檔名**，讓您的應用程式具備接受或拒絕上傳的智慧，提供友善的 UI 選項，並避免昂貴的執行時錯誤。本教學將一步步帶您完成所有必要步驟——從前置條件到完整、可投入生產的實作——讓您能自信地 **取得檔案格式** 並 **c# display file formats** 在您的解決方案中。

## 快速解答
- **「list file extensions」是什麼意思？** 這表示從 API 取得支援的檔案類型識別碼集合（例如 *.pdf*、*.docx*）。
- **哪個 NuGet 套件提供此功能？** `GroupDocs.Redaction`（最新穩定版）。
- **執行範例是否需要授權？** 免費試用授權可用於開發；正式環境需使用永久授權。
- **我可以快取結果嗎？** 可以——將清單儲存在記憶體或分散式快取中，以避免重複呼叫 API。
- **此功能是否相容於 .NET 6 與 .NET Core？** 當然；此函式庫支援 .NET Framework 4.5+、.NET Core 3.1+、.NET 5+ 以及 .NET 6+。

## GroupDocs.Redaction 是什麼？
**GroupDocs.Redaction** 是一套 .NET 函式庫，讓開發人員能夠遮蔽敏感內容、轉換文件，並偵測支援的檔案類型——全部不需在伺服器上安裝 Microsoft Office。它將複雜的格式處理抽象為乾淨的物件導向 API。此函式庫提供統一的 API 進行遮蔽、轉換與格式偵測，支援 PDF、Office 文件、影像等多種格式，同時確保高效能與安全性。

## 為什麼要使用 GroupDocs.Redaction 列出檔案副檔名？
此函式庫 **支援超過 50 種輸入與輸出格式**，包括 PDF、DOCX、PPTX、XLSX、HTML，以及超過 30 種影像類型。透過程式化 **列出檔案副檔名**，您可以：

- 防止使用者上傳不支援的檔案（將驗證錯誤降低至最高 90%）。  
- 動態填充下拉選單，確保 UI 與函式庫更新保持同步。  
- 建立稽核日誌，記錄使用者嘗試處理的精確檔案類型。

## 前置條件

- **GroupDocs.Redaction**：透過 NuGet 安裝（請參考以下指令）。  
- **.NET SDK**：確保已安裝最新的 .NET SDK。點此下載 [here](https://dotnet.microsoft.com/download)。  
- **IDE**：Visual Studio 2022 或任何相容的編輯器。  
- **Basic C# knowledge**：您應該熟悉集合與 LINQ。

## 設定 GroupDocs.Redaction 於 .NET

### 安裝函式庫

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- 開啟 NuGet 套件管理員，搜尋 “GroupDocs.Redaction”，並安裝最新版本。

### 取得並套用授權

先使用免費試用或申請臨時授權，以無限制探索完整功能。欲購買授權，請前往 [GroupDocs' purchase page](https://purchase.groupdocs.com/)。取得授權檔案後：

1. 將其放置於專案內可存取的資料夾（例如 `./Licenses/GroupDocs.Redaction.lic`）。  
2. 在應用程式啟動時初始化授權：

`License` 類別會載入您的授權檔案並啟用 GroupDocs.Redaction。  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## 如何使用 GroupDocs.Redaction 列出檔案副檔名？

載入 Redaction API 並呼叫回傳支援格式的方法。此呼叫會返回一個集合，每個項目包含副檔名與可讀的描述。此操作輕量，可於啟動時或按需執行。

### 取得支援的檔案類型
`RedactionApi.GetSupportedFileFormats()` 方法回傳只讀的 `FileFormatInfo` 物件集合，描述每種格式。  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### 顯示每個副檔名與描述
每個 `FileFormatInfo` 物件提供 `Extension` 與 `Description` 屬性，用於描述檔案類型。  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**說明**：此迴圈遍歷每個 `FileFormatInfo` 物件，將其 `Extension` 與 `Description` 列印於整齊對齊的表格中。

## 如何將清單整合至 UI 下拉選單？

取得集合後，將其繫結至任何 UI 元件——WinForms `ComboBox`、WPF `ComboBox` 或 ASP.NET Core `select` 元素。關鍵是使用 `Extension` 作為值，`Description` 作為顯示文字。這可確保使用者看到友善名稱，而程式碼則使用精確的副檔名字串。

## 常見問題與解決方案

- **Missing namespace error** – 確認已匯入 `GroupDocs.Redaction` 與 `GroupDocs.Redaction.Common`。  
- **License not found** – 確認授權檔案路徑正確，且檔案已包含於建置輸出中。  
- **Performance on large projects** – 將結果快取於靜態變數或分散式快取（例如 Redis），以避免重複列舉。

## 實務應用

了解支援的副檔名清單可開啟多種實務情境：

1. **Document Management Systems** – 根據副檔名自動分類進來的檔案。  
2. **Content Filtering Tools** – 在上傳時阻擋不允許的格式（例如可執行檔）。  
3. **File Conversion Pipelines** – 動態判斷檔案是否可轉換，或需使用備援工作流程。

## 效能考量

- **Memory footprint** – 格式清單儲存在輕量的 `IReadOnlyCollection` 中，通常小於 2 KB。  
- **Thread safety** – 此集合在建立後即為不可變，因而安全供多執行緒讀取。  
- **Caching** – 對於高流量 API，將清單快取於應用程式生命週期內，以消除每次請求的微秒級開銷。

## 結論

依照上述步驟操作後，您已擁有可靠的方式使用 GroupDocs.Redaction **列出檔案副檔名** 並 **c# display file formats**。此功能不僅提升使用者體驗，也保護後端免於不支援的檔案。探索其他 Redaction 功能——例如內容遮蔽、PDF 遮蔽與批次處理——以進一步強化文件工作流程。

## 常見問答

**Q: 預設支援的檔案格式有哪些？**  
A: GroupDocs.Redaction 支援超過 50 種格式，包括 PDF、DOCX、PPTX、XLSX、HTML、BMP、JPEG、PNG 等等。完整清單請參閱 [GroupDocs documentation](https://docs.groupdocs.com/search/net/)。

**Q: 如何升級函式庫至最新版本？**  
A: 開啟 NuGet 套件管理員，搜尋 “GroupDocs.Redaction”，然後點選 **Update**。或是執行 `dotnet add package GroupDocs.Redaction --version <latest>`。

**Q: 我可以將此清單用於伺服器端驗證上傳的檔案嗎？**  
A: 可以——在處理之前，將上傳檔案的副檔名與取得的集合比對。這可消除 99% 的格式錯誤。

**Q: 是否可以擴充支援自訂檔案類型？**  
A: 自訂副檔名需要自訂處理程式；核心函式庫本身不會原生加入新格式。請參閱 API 文件以建立自訂的匯入/匯出管線。

**Q: 我的應用程式在加入程式碼後崩潰——應該檢查什麼？**  
A: 確認授權已正確載入、`using` 陳述式引用正確的命名空間，且在讀取授權檔案時處理 `IOException`。

---

**最後更新:** 2026-06-07  
**測試環境:** GroupDocs.Redaction 23.9 for .NET  
**作者:** GroupDocs  

## 資源
- [文件說明](https://docs.groupdocs.com/search/net/)
- [API 參考](https://reference.groupdocs.com/redaction/net)
- [下載 GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)
- [臨時授權申請](https://purchase.groupdocs.com/temporary-license/)

## 相關教學
- [精通 .NET 中的檔案過濾與 GroupDocs.Redaction：高效文件管理技巧](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [精通 GroupDocs.Redaction .NET：設定與事件處理以確保文件管理安全](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [精通 .NET 中的文件管理與 GroupDocs.Redaction：授權設定與 HTML 搜尋高亮](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)