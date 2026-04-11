---
date: '2026-04-11'
description: 了解如何在 .NET 應用程式中使用 GroupDocs Search 與 Redaction 管理同義詞，包括匯入同義詞字典及提升搜尋功能。
keywords:
- how to manage synonyms
- import synonym dictionary
- GroupDocs Search .NET
title: 如何在 .NET 中使用 GroupDocs Search 管理同義詞
type: docs
url: /zh-hant/net/dictionaries-language-processing/master-synonym-management-dotnet-groupdocs-search-redaction/
weight: 1
---

# 精通 .NET 中的同義詞管理與 GroupDocs Search 及 Redaction

提升應用程式理解不同字詞變化的能力，首先要有效地 **如何管理同義詞**。無論您需要更智慧的搜尋結果或精確的內容遮蔽，本指南將帶您使用 .NET 版 GroupDocs.Search 搭配 GroupDocs.Redaction。完成後，您將能建立、匯出、匯入及查詢同義詞字典，並了解這些功能在實際情境中的應用。

## 快速解答
- **“如何管理同義詞”是什麼意思？** 它是建立、更新及使用同義詞字典的過程，使搜尋能返回字詞變化的結果。  
- **哪個函式庫提供同義詞支援？** GroupDocs.Search for .NET 提供內建的同義詞字典。  
- **我可以匯入同義詞字典嗎？** 可以 – 使用 `ImportDictionary` 方法載入先前匯出的檔案。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買完整授權。  
- **Redaction 相容嗎？** 絕對相容 – 您可以將以搜尋為基礎的同義詞處理與 GroupDocs.Redaction 結合，以安全地處理文件。

## 什麼是同義詞管理？
同義詞管理是定義具有相同意義的詞彙群組的做法（例如 “buy”、 “purchase”、 “acquire”）。當使用者搜尋某個詞彙時，搜尋引擎會自動將查詢擴展至其同義詞，提供更完整的結果。

## 為何使用 GroupDocs Search 進行同義詞管理？
- **內建字典 API** – 無需自行建立資料結構。  
- **與 GroupDocs.Redaction 無縫整合**，讓您可根據同義詞擴展的查詢進行內容遮蔽。  
- **效能最佳化** 的索引與搜尋，即使面對大型同義詞集合亦能順暢。

## 前置條件
- **GroupDocs.Search** 與 **GroupDocs.Redaction** NuGet 套件。  
- .NET 開發環境（Visual Studio、VS Code 或 .NET CLI）。  
- 基本的 C# 知識，特別是檔案處理與集合相關。

## 設定 .NET 版 GroupDocs Redaction
### 安裝資訊
使用以下任一方法將必要的函式庫加入您的專案：

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**  
搜尋 *GroupDocs.Redaction* 並安裝最新版本。

### 取得授權步驟
1. **免費試用** – 在未使用授權金鑰的情況下探索核心功能。  
2. **臨時授權** – 取得時間限制的金鑰以進行延長測試。  
3. **完整授權** – 購買以在正式環境中無限制使用。

**基本初始化**
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a file path and apply basic configurations
Redactor redactor = new Redactor("sample.docx");
redactor.Apply(new ExactPhraseRedaction("Sensitive Info", new ReplacementOptions("[REDACTED]")));
```

## 實作指南
讓我們逐步說明在您的 .NET 專案中 **如何管理同義詞** 所需的每個步驟。

### 建立與管理索引
#### 概觀
建立索引是任何同義詞操作的基礎。您將 `Index` 類別指向資料夾，然後加入可供搜尋的文件。

**步驟**
- **初始化索引**  
  ```csharp
  using GroupDocs.Search;

  // Specify paths according to your environment
  string indexPath = @"YOUR_DOCUMENT_DIRECTORY/ManagingDictionaries/SynonymDictionary/Index";
  Index index = new Index(indexPath);
  ```

- **加入文件**  
  ```csharp
  string documentsPath = @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";
  index.Add(documentsPath);
  ```

### 取得單字的同義詞
#### 概觀
您可以取得特定詞彙的所有同義詞，這對顯示建議或除錯字典很有幫助。

**步驟**
```csharp
string[] synonyms = index.Dictionaries.SynonymDictionary.GetSynonyms("make");
```

```csharp
foreach (string synonym in synonyms)
{
    Console.WriteLine(synonym);
}
```

### 取得同義詞群組
#### 概觀
群組讓您看到相關詞彙聚集在一起，有助於語意分析。

**步驟**
```csharp
string[][] synonymGroups = index.Dictionaries.SynonymDictionary.GetSynonymGroups("make");
```

```csharp
foreach (string[] group in synonymGroups)
{
    Console.WriteLine(string.Join(", ", group));
}
```

### 清除與新增同義詞至字典
#### 概觀
動態應用程式常需要在不重新建構整個索引的情況下刷新同義詞清單。

**步驟**
```csharp
if (index.Dictionaries.SynonymDictionary.Count > 0)
{
    index.Dictionaries.SynonymDictionary.Clear();
}
```

```csharp
string[][] newSynonymGroups = new string[][
    { "achieve", "accomplish", "attain", "reach" },
    { "accept", "take", "have" }
];

index.Dictionaries.SynonymDictionary.AddRange(newSynonymGroups);
```

### 匯出與匯入同義詞字典
#### 概觀
匯出可讓您備份或分享同義詞資料；匯入則可在之後還原或載入共享的字典。

**步驟**
```csharp
string fileName = @"YOUR_DOCUMENT_DIRECTORY/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.Dictionaries.SynonymDictionary.ExportDictionary(fileName);
```

```csharp
index.Dictionaries.SynonymDictionary.ImportDictionary(fileName);
```

### 在索引中執行同義詞搜尋
#### 概觀
在搜尋查詢期間啟用同義詞擴展，讓使用者即使使用不同措辭也能找到相關文件。

**步驟**
```csharp
string query = "better";
SearchOptions options = new SearchOptions() { UseSynonymSearch = true };
```

```csharp
SearchResult result = index.Search(query, options);

// Display results (implementation-dependent)
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```

## 實務應用
- **法律文件管理** – 使用同義的法律術語來定位合約。  
- **內容推薦引擎** – 基於同義詞擴展的查詢推薦文章。  
- **客戶支援系統** – 即使用語不同，也能將工單與知識庫文章匹配。  
- **電子商務平台** – 透過辨識如 “sofa” 與 “couch” 等同義詞提升商品搜尋。

## 效能考量
- **索引策略** – 以增量方式重建或更新索引，以保持同義詞資料新鮮。  
- **資源使用** – 載入大型同義詞字典時監控記憶體；及時釋放 `Index` 物件。  
- **執行緒安全** – 未經適當同步，避免在多執行緒間共享單一 `Index` 實例。

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| 同義詞未返回結果 | 同義詞字典未載入或 `UseSynonymSearch` 設為 `false` | 確保 `SearchOptions.UseSynonymSearch = true` 且字典已正確匯入。 |
| 重新匯入後出現重複項目 | 匯入前未先清除 | 在 `ImportDictionary` 前呼叫 `index.Dictionaries.SynonymDictionary.Clear()`。 |
| 記憶體使用量過高 | 將非常大的同義詞檔案載入記憶體 | 將同義詞拆分為多個較小的字典或按需載入。 |

## 常見問答

**Q: 更新同義詞字典後，我該如何匯入？**  
A: 在可選擇先清除現有字典後，使用 `index.Dictionaries.SynonymDictionary.ImportDictionary(filePath)`。

**Q: 我可以將同義詞搜尋與片語搜尋結合嗎？**  
A: 可以 – 在 `SearchOptions` 中同時啟用 `UseSynonymSearch` 與 `UsePhraseSearch` 以取得結合行為。

**Q: 更改同義詞後需要重新建構索引嗎？**  
A: 不需要，同義詞變更會儲存在字典中，並立即對新搜尋生效。

**Q: 能否以人類可讀的格式匯出同義詞？**  
A: `ExportDictionary` 方法會寫入二進位檔案；您可以將其反序列化，或保留平行的 JSON/YAML 檔案以供閱讀。

**Q: Redaction 會遵循同義詞擴展的查詢嗎？**  
A: 絕對會 – 您可以先執行同義詞搜尋，然後將結果文件清單傳遞給 `GroupDocs.Redaction` 以進行安全處理。

---
**最後更新：** 2026-04-11  
**測試環境：** GroupDocs.Search 23.11 for .NET, GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs