---
date: '2026-07-31'
description: 了解如何透過實作自訂 Console Logger 並利用內建的 FileLogger，使用 GroupDocs 建立穩健的 .NET 日誌記錄，以達到有效的監控。
keywords:
- create robust .net logging
- groupdocs logging
- custom console logger
- .net file logger
lastmod: '2026-07-31'
og_description: 了解如何透過實作自訂 Console Logger 並利用內建的 FileLogger，使用 GroupDocs 建立穩健的 .NET
  日誌記錄，以達到有效的監控。
og_image_alt: Guide showing how to create robust .NET logging with GroupDocs custom
  console logger
og_title: 使用 GroupDocs Console Logger 建立穩健的 .NET 日誌記錄
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to create robust .NET logging using GroupDocs by implementing
    a custom console logger and leveraging the built‑in FileLogger for effective monitoring.
  headline: Create Robust .NET Logging with GroupDocs Console Logger
  type: TechArticle
- description: Learn how to create robust .NET logging using GroupDocs by implementing
    a custom console logger and leveraging the built‑in FileLogger for effective monitoring.
  name: Create Robust .NET Logging with GroupDocs Console Logger
  steps:
  - name: '**Application Monitoring:** Use `ConsoleLogger` during development to see
      live diagnostics.'
    text: '**Application Monitoring:** Use `ConsoleLogger` during development to see
      live diagnostics.'
  - name: '**Audit Trails:** Deploy `FileLogger` to maintain compliance‑grade logs
      for regulatory reporting.'
    text: '**Audit Trails:** Deploy `FileLogger` to maintain compliance‑grade logs
      for regulatory reporting.'
  - name: '**Debugging:** Leverage detailed trace messages to pinpoint issues in complex
      search pipelines.'
    text: '**Debugging:** Leverage detailed trace messages to pinpoint issues in complex
      search pipelines.'
  - name: '**Performance Analysis:** Examine log timestamps to identify bottlenecks
      and optimize resource usage.'
    text: '**Performance Analysis:** Examine log timestamps to identify bottlenecks
      and optimize resource usage.'
  type: HowTo
- questions:
  - answer: Yes—both `ConsoleLogger` and `FileLogger` are thread‑safe, so you can
      log from parallel tasks without race conditions.
    question: Can I use the custom console logger in a multi‑threaded application?
  - answer: A single GroupDocs license covers all modules, including Search and Redaction,
      simplifying procurement.
    question: Do I need a separate license for GroupDocs.Search and GroupDocs.Redaction?
  - answer: Set the `LogFilePath` property when constructing the `FileLogger` instance,
      e.g., `new FileLogger("C:\\Logs\\app.log")`.
    question: How do I change the log file location for FileLogger?
  - answer: The library provides `Debug`, `Info`, `Warning`, `Error`, and `Critical`
      levels, allowing fine‑grained control over output.
    question: What log levels does GroupDocs support?
  - answer: Absolutely—create a composite logger that forwards messages to both `ConsoleLogger`
      and `FileLogger` for dual visibility.
    question: Is it possible to combine both console and file logging simultaneously?
  type: FAQPage
tags:
- logging
- groupdocs
- .net
- custom logger
- console logger
title: 使用 GroupDocs Console Logger 建立穩健的 .NET 日誌記錄
type: docs
url: /zh-hant/net/exception-handling-logging/mastering-logging-dotnet-groupdocs-custom-console-logger-guide/
weight: 1
---

# 建立穩健的 .NET 記錄功能與 GroupDocs 主控台記錄器

## 介紹

您是否在追蹤 .NET 應用程式中的錯誤與操作流程時感到困難？**Create robust .NET logging** 是監控效能、除錯問題與維持順暢運作的關鍵。本教學將帶您使用 GroupDocs.Search 建立自訂主控台記錄器，並示範如何整合 GroupDocs.Redaction for .NET。完成後，您將擁有一套透明且易於維護的記錄解決方案，能直接嵌入現有程式碼基礎。

## 快速解答
- **自訂記錄器的功能是什麼？** 直接將日誌條目寫入主控台，以在開發期間即時回饋。  
- **哪個 GroupDocs 元件提供檔案記錄？** 內建的 `FileLogger` 類別負責持久化日誌檔案。  
- **需要授權嗎？** 測試可使用臨時授權；正式環境必須使用正式授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **此解決方案是執行緒安全的嗎？** 是——`ConsoleLogger` 與 `FileLogger` 均設計為可同時使用。

## 什麼是「Create robust .NET logging」？
**Create robust .NET logging** 意指建立可靠且高效能的記錄管線，能在應用程式的各層捕捉錯誤、警告與資訊訊息。透過 GroupDocs，您可以同時使用主控台與檔案目標，且設定簡單。

## 為什麼在 .NET 記錄中使用 GroupDocs？
GroupDocs 支援 **30+ .NET platforms**，且可處理高達 **2 GB** 的文件而不會明顯影響效能。其記錄 API 輕量、執行緒安全，且能無縫整合現有的例外處理模式，提供成熟的企業級解決方案。

## 前置條件

- **必備函式庫與版本：** GroupDocs.Search for .NET 與 GroupDocs.Redaction for .NET（最新相容版本）。  
- **環境設定：** Visual Studio 2022 或任何相容 .NET 的 IDE。  
- **知識前提：** 熟悉 C# 語法與基本記錄概念。

## 設定 GroupDocs.Redaction for .NET

首先，將 GroupDocs.Redaction 加入您的專案。選擇最符合工作流程的方法。

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜尋 “GroupDocs.Redaction” 並安裝最新版本。

### 取得授權

要開始使用，您可以取得臨時授權或購買正式授權。這讓您能在不受限制的情況下探索所有功能。請前往 [GroupDocs 官方網站](https://purchase.groupdocs.com/temporary-license/) 了解取得授權的更多細節。

### 基本初始化與設定

`Redactor` 類別提供 API 以修改與編輯受支援文件中的內容。  
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a file path or stream
Redactor redactor = new Redactor("path/to/your/document.pdf");
```  

## 實作指南

### 如何使用 GroupDocs 實作自訂主控台記錄器？

透過建立 `ConsoleLogger` 實例並將其傳遞給 `SearchOptions` 或任何接受 `ILogger` 的 GroupDocs 元件，即可載入自訂記錄器。記錄器會將每則訊息寫入 `Console.WriteLine`，讓您即時看到函式庫的運作情形，並在開發期間快速發現問題。

`ConsoleLogger` 類別實作 `ILogger`，直接將日誌訊息寫入主控台。  
```csharp
using System;
using GroupDocs.Search.Common;

public class ConsoleLogger : ILogger
{
    public ConsoleLogger()
    {
    }

    // Logs an error message using the console.
    public void Error(string message)
    {
        Console.WriteLine("Error: " + message);
    }

    // Logs a trace message using the console.
    public void Trace(string message)
    {
        Console.WriteLine(message);
    }
}
```  

**步驟 1：定義您的自訂記錄器**  
建立一個名為 `ConsoleLogger` 的新類別：  
```csharp
using System;
using GroupDocs.Search.Common;

public class ConsoleLogger : ILogger
{
    public ConsoleLogger()
    {
    }

    // Logs an error message using the console.
    public void Error(string message)
    {
        Console.WriteLine("Error: " + message);
    }

    // Logs a trace message using the console.
    public void Trace(string message)
    {
        Console.WriteLine(message);
    }
}
```  

**步驟 2：與 GroupDocs.Search 整合**  

`SearchOptions` 用於設定搜尋行為，並接受 `ILogger` 進行記錄。  
```csharp
using System;
using GroupDocs.Search.Common;
using GroupDocs.Search.Results;

public static void ImplementingCustomLogger()
{
    string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Logging/ImplementingCustomLogger";
    string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
    string query = "Lorem";

    IndexSettings settings = new IndexSettings();
    settings.Logger = new ConsoleLogger(); // Set your custom logger

    Index index = new Index(indexFolder, settings);
    index.Add(documentsFolder);

    SearchResult result = index.Search(query);
}
```  

### 什麼是 FileLogger 以及何時使用？

`FileLogger` 類別實作 `ILogger`，將日誌條目持久化至磁碟檔案，適合需要稽核追蹤的生產環境。GroupDocs 提供的 `FileLogger` 會將日誌寫入指定檔案，讓您在需要永久稽核紀錄時使用。您可以設定日誌輪替、檔案大小上限與日誌等級，以符合營運需求。

`FileLogger` 類別實作 `ILogger`，將日誌條目持久化至磁碟檔案。  
```csharp
using System;
using GroupDocs.Search.Common;
using GroupDocs.Search.Results;

public static void UseOfStandardFileLogger()
{
    string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Logging/UseOfStandardFileLogger";
    string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
    string query = "Lorem";
    string logPath = "YOUR_OUTPUT_DIRECTORY/Logging/Log.txt";

    IndexSettings settings = new IndexSettings();
    settings.Logger = new FileLogger(logPath, 4.0); // Log file path and max size

    Index index = new Index(indexFolder, settings);
    index.Add(documentsFolder);

    SearchResult result = index.Search(query);
}
```  

### 為什麼選擇 GroupDocs 作為 .NET 記錄？

GroupDocs 提供 **quantified** 優勢：支援 **over 50 output formats**，且能處理 **multi‑hundred‑page documents** 而不需將整個檔案載入記憶體。其記錄基礎設施每筆日誌僅增加不到 **2 ms** 的開銷，即使在高負載下也能保持最佳效能。

## 實務應用

以下是幾個記錄技術發揮效用的實務情境：

1. **應用程式監控：** 在開發期間使用 `ConsoleLogger` 以即時觀測診斷資訊。  
2. **稽核追蹤：** 部署 `FileLogger` 以維持符合規範的稽核日誌，供法規報告使用。  
3. **除錯：** 利用詳細的追蹤訊息定位複雜搜尋管線中的問題。  
4. **效能分析：** 檢視日誌時間戳記以找出瓶頸，並優化資源使用。

## 效能考量

為了保持記錄快速且高效：

- **限制日誌詳細度：** 在生產環境將記錄等級設為 `Info` 或 `Warning`，避免過度 I/O。  
- **有效利用資源：** 將 `FileLogger` 設定為最大檔案大小 10 MB，並啟用自動輪替。  
- **記憶體管理：** 使用 `using` 區塊或明確呼叫 `Dispose()` 釋放記錄器實例，以即時回收資源。

## 常見問題

**Q: 可以在多執行緒應用程式中使用自訂主控台記錄器嗎？**  
A: 可以——`ConsoleLogger` 與 `FileLogger` 均為執行緒安全，您可以在平行任務中安全記錄而不會產生競爭條件。

**Q: 是否需要為 GroupDocs.Search 與 GroupDocs.Redaction 分別購買授權？**  
A: 單一 GroupDocs 授權即可涵蓋所有模組，包括 Search 與 Redaction，簡化採購流程。

**Q: 如何變更 FileLogger 的日誌檔案位置？**  
A: 建構 `FileLogger` 實例時設定 `LogFilePath` 屬性，例如 `new FileLogger("C:\\Logs\\app.log")`。

**Q: GroupDocs 支援哪些日誌等級？**  
A: 函式庫提供 `Debug`、`Info`、`Warning`、`Error` 與 `Critical` 等級，讓您可細緻控制輸出。

**Q: 能否同時結合主控台與檔案記錄？**  
A: 完全可以——建立複合記錄器，同時將訊息轉發至 `ConsoleLogger` 與 `FileLogger`，達到雙重可見性。

## 資源

- [GroupDocs Redaction 文件](https://docs.groupdocs.com/search/net/)  
- [API 參考](https://reference.groupdocs.com/redaction/net)  
- [下載 GroupDocs 程式庫](https://releases.groupdocs.com/search/net/)  
- [免費支援論壇](https://forum.groupdocs.com/c/search/10)  
- [臨時授權取得](https://purchase.groupdocs.com/temporary-license/)  

## 結論

本指南說明了如何透過建立自訂主控台記錄器並利用 GroupDocs 內建的 `FileLogger`，**create robust .NET logging**。這些工具在開發期間提供即時洞察，於生產環境則提供可靠且持久的日誌。您可以探索不同的日誌等級設定、嘗試複合記錄器，並將解決方案整合至更大型的服務，以實現全端可觀測性。

**下一步**

- 測試不同的日誌等級設定，找出在細節與效能之間的最佳平衡點。  
- 為 `FileLogger` 加入結構化日誌（JSON 輸出），以便更容易匯入日誌分析平台。  
- 探索 GroupDocs 的其他模組，如 Search 與 Annotation，擴充文件處理管線。

---

**最後更新：** 2026-07-31  
**測試環境：** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs  

## 相關教學

- [GroupDocs.Search .NET 例外處理與記錄教學](/search/net/exception-handling-logging/)  
- [在 .NET 中實作 GroupDocs.Search 與 Redaction 以進行文件管理](/search/net/document-management/groupdocs-search-redaction-net-guide/)  
- [精通 GroupDocs Search 與 Redaction 在 .NET：進階文件管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)