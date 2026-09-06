---
date: '2026-06-12'
description: 了解如何使用 GroupDocs.Search 與 GroupDocs.Redaction 在 .NET 中建立搜尋索引並對 PDF 進行塗抹。說明設定、部署、索引以及進階搜尋的操作。
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: 使用 GroupDocs Search 與 Redaction 建立 .NET 搜尋索引 – 全面指南
type: docs
url: /zh-hant/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# 建立搜尋索引 .NET 與 GroupDocs Search 及 Redaction – 完整指南

在當今的數位環境中，**建立搜尋索引 .NET** 解決方案能快速定位資訊並保護敏感資料，是任何組織的首要任務。本教學將帶領您設定可擴展的 GroupDocs.Search 網路、部署節點、建立文件索引，並使用 GroupDocs.Redaction **對 PDF 套用遮蔽**，全部於 .NET 環境中完成。

## 快速回答
- **建立搜尋索引 .NET 的第一步是什麼？** 定義基礎路徑與埠號，然後部署網路節點。  
- **如何使用 GroupDocs 對 PDF 套用遮蔽？** 初始化 `Redactor` 實例，載入 PDF，並以所需的模式呼叫 `Redact`。  
- **我可以在多台機器上執行搜尋網路嗎？** 可以——在不同伺服器上部署節點，讓主節點協調索引與查詢。  
- **生產環境需要授權嗎？** 生產環境必須擁有有效的 GroupDocs 授權；亦可取得暫時的試用授權以進行評估。  
- **支援哪些 .NET 版本？** 完全支援 .NET Framework 4.7.2+、.NET Core 3.1+ 以及 .NET 5/6/7。

## 什麼是「建立搜尋索引 .NET」？
*建立搜尋索引 .NET* 指的是使用 .NET 函式庫建構可搜尋的文件中繼資料與內容儲存庫，該函式庫會擷取文字、斷詞，並將其存放於最佳化的索引結構中。此機制可在分散式節點間即時回應查詢，支援多種檔案格式，並在企業應用中提供可擴展、高效能的文件檢索。

## 為何同時使用 GroupDocs Search 與 Redaction？
GroupDocs.Search 支援 **超過 50 種檔案格式**——包括 DOCX、PDF、PPTX 與 HTML，且能在不將整個檔案載入記憶體的情況下索引數百頁的文件。結合 GroupDocs.Redaction，後者可在每頁低於 200 ms 的時間內 **對 PDF 套用遮蔽**，為您提供安全且高效能的文件管理流程。

## 前置條件

### 必要的函式庫與相依性
要跟隨本教學，請安裝以下套件：
- **GroupDocs.Search** for .NET
- **GroupDocs.Redaction** for .NET  

您可以使用以下任一方式安裝所需函式庫：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜尋「GroupDocs.Search」與「GroupDocs.Redaction」並安裝最新版本。

### 環境設定需求
- .NET Framework 4.7.2 或更新版本（或 .NET Core 3.1+）
- Visual Studio IDE（Community、Professional 或 Enterprise）

### 知識前置條件
- 基本的 C# 程式設計
- 物件導向概念
- 熟悉網路配置與文件管理系統

## 設定 GroupDocs.Redaction 於 .NET

### 安裝資訊
要在應用程式中整合遮蔽功能，請先加入 GroupDocs.Redaction 函式庫：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜尋「GroupDocs.Redaction」並安裝。

### 取得授權
要開始使用免費試用或暫時授權，請依照以下步驟：
- 前往 [GroupDocs 網站](https://purchase.groupdocs.com/temporary-license/) 申請暫時授權。  
- 若需購買，請前往其 [價格頁面](https://groupdocs.com/pricing)。

取得授權檔案後，於應用程式設定中套用：

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### 基本初始化
要為基本操作初始化 GroupDocs.Redaction，請使用以下程式碼片段：

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## 實作指南

### 設定配置

#### 概觀
此功能使用基礎路徑與埠號設定搜尋網路，構成文件管理系統的基礎。

#### 定義錨點
`SearchNetworkDeployment` 是負責協調網路中搜尋節點部署的類別。

#### 步驟 1：定義基礎路徑與埠號  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### 步驟 2：設定網路
使用 `Configure` 方法，以指定的路徑與埠號設定搜尋網路：

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### 網路節點部署

#### 概觀
在已設定的搜尋網路中部署節點，以進行分散式文件搜尋。

#### 定義錨點
`SearchNetworkNode` 代表可與主節點通訊的單一可搜尋節點。

#### 步驟 1：初始化部署  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### 主節點事件訂閱

#### 概觀
訂閱主節點的事件，以有效監控與管理網路運作。

#### 定義錨點
`SearchNetworkNodeEvents` 提供索引、查詢執行與錯誤處理的回呼。

#### 步驟 1：識別主節點
將第一個節點選為主節點：

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### 步驟 2：訂閱事件
使用以下方式訂閱事件：

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### 文件索引

#### 概觀
為了有效的搜尋操作，請對文件建立索引。此步驟對於確保網路能快速取得所需資料至關重要。

#### 定義錨點
`SearchIndex` 是儲存每個已索引檔案之可搜尋標記與中繼資料的核心物件。

#### 步驟 1：將目錄加入索引
指定包含文件的目錄：

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### 搜尋功能 – 基本使用

#### 概觀
在網路中的節點執行基本搜尋操作。

#### 直接答案
在主節點呼叫 `SearchNetwork.Query("your term")` 以即時取得符合的文件。此方法會回傳包含檔案路徑與相關性分數的 `SearchResult` 物件集合。  
`SearchNetwork.Query` 為在整個網路執行搜尋查詢並回傳符合結果的方法。

#### 步驟 1：定義搜尋參數  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### 進階搜尋功能

#### 概觀
使用可自訂參數的進階搜尋技術，以獲得更精確的結果。

#### 直接答案
實作一個方法，建立 `SearchOptions` 物件，設定 `UseFuzzySearch`、`Highlight` 與 `PageSize` 屬性，然後傳遞給 `SearchNetwork.QueryAdvanced`。此方式會產生分頁、突顯且啟用模糊匹配的結果。  
`SearchNetwork.QueryAdvanced` 為執行具模糊匹配與分頁等進階選項查詢的方法。

#### 步驟 1：實作進階搜尋方法  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### 對 PDF 檔案套用遮蔽

#### 概觀
在 PDF 內容儲存或分享前，透過遮蔽保護敏感資訊。

#### 直接答案
建立 `Redactor` 實例，載入目標 PDF，定義 `RedactionPattern`（例如 SSN 正規表達式），呼叫 `redactor.Apply(pattern)`，最後儲存已遮蔽的文件。此流程確保個人資料被永久移除。

#### 定義錨點
`Redactor` 是 GroupDocs.Redaction 中處理文件並套用遮蔽規則的主要類別。

#### 範例工作流程（無新程式碼區塊）  
1. 使用您的授權初始化 `Redactor`。  
2. 使用 `redactor.Load("sample.pdf")` 載入 PDF。  
3. `RedactionPattern` 代表指定要遮蔽之文字或模式的規則。可定義如 `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")` 的模式。  
4. 執行 `redactor.Apply(pattern)`。  
5. 使用 `redactor.Save("sample_redacted.pdf")` 儲存輸出。

### 實務應用

#### 真實案例
1. **法律文件管理** – 高效搜尋合約並自動遮蔽客戶識別資訊。  
2. **醫療紀錄** – 定位患者筆記，同時確保符合 HIPAA 規範的 PHI 遮蔽。  
3. **企業合規** – 掃描內部通訊以偵測禁用詞彙，並在歸檔前進行遮蔽。

## 結論 
本指南提供了 **建立搜尋索引 .NET** 解決方案的完整路徑，具備可擴展、快速索引與透過遮蔽保護資料的能力。透過設定節點、索引文件、運用進階搜尋功能與套用遮蔽，開發人員能顯著提升文件管理工作流程，同時遵守嚴格的安全標準。

## 常見問題

**Q: 如何在 .NET 使用 GroupDocs 設置分散式搜尋網路？**  
A: 定義基礎路徑與埠號，然後呼叫 `SearchNetworkDeployment.Deploy()` 以在多台機器上啟動主節點與工作節點。

**Q: 我能在 GroupDocs 中使用多個參數執行進階搜尋嗎？**  
A: 可以——使用 `SearchOptions` 在單一查詢中結合模糊匹配、萬用字元支援與結果突顯。

**Q: 能否在主節點監控網路活動？**  
A: 完全可以——訂閱 `SearchNetworkNodeEvents`（如 `IndexingCompleted` 與 `QueryExecuted`）以取得即時資訊。

**Q: 如何使用 GroupDocs 對 PDF 檔案套用遮蔽？**  
A: 初始化 `Redactor`，載入 PDF，定義 `RedactionPattern` 物件（正規表達式或文字字串），呼叫 `Apply`，最後儲存已清理的文件。

**Q: 在網路環境中提升搜尋效能的最簡方法是什麼？**  
A: 在查詢前完整索引文件集，分散節點以利用平行處理，並調整 `SearchOptions` 以支援快取與分頁。

---

**最後更新：** 2026-06-12  
**測試環境：** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**作者：** GroupDocs

## 相關教學

- [掌握 .NET 文件索引與 GroupDocs.Search&#58; 完整指南](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [掌握文件索引與 GroupDocs.Redaction .NET 進階搜尋查詢](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [精通 GroupDocs Search 與 Redaction 在 .NET&#58; 進階文件管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)