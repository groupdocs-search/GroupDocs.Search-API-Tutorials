---
date: '2026-04-02'
description: 學習如何按檔案副檔名篩選，僅搜尋 txt 檔案，使用 GroupDocs.Redaction for .NET——提升文件管理效率。
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: 在 .NET 中使用 GroupDocs.Redaction 按檔案副檔名篩選
type: docs
url: /zh-hant/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# 使用 GroupDocs.Redaction 在 .NET 中依檔案副檔名過濾

在龐大的檔案集合中搜尋可能令人感到壓力，尤其是當你只需要特定檔案類型的結果時。在本教學中，你將了解 **依檔案副檔名過濾**，讓你只能搜尋 txt 檔或任何你選擇的副檔名。我們將逐步說明如何設定檔案類型與路徑為基礎的過濾條件，讓你快速定位所需的文件。

## 快速解答
- **「依檔案副檔名過濾」是什麼作用？** 它會將搜尋限制在符合指定副檔名的文件（例如 *.txt）。  
- **為什麼要使用 GroupDocs.Redaction？** 它提供內建的過濾 API，快速且易於整合。  
- **我需要授權嗎？** 免費試用可用於測試；正式環境需購買授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6+。  
- **我可以同時結合檔案類型與路徑過濾嗎？** 可以——套用多個過濾條件以達到高度精準的搜尋。  

## 你將學到
- 如何 **依檔案副檔名過濾**，僅搜尋文字檔。  
- 如何設定 **檔案路徑過濾**，將結果限制於特定資料夾或命名模式。  
- 保持索引快速且節省記憶體的技巧。  

## 前置條件

在開始之前，請確保你已具備以下條件：

- **GroupDocs.Redaction Library** 已安裝且與你的 .NET 專案相容。  
- 開發環境，例如 Visual Studio 或 VS Code。  
- 基本的 C# 知識以及對 .NET 專案結構的了解。  

## 設定 GroupDocs.Redaction for .NET

首先，將函式庫加入你的專案。

**使用 .NET CLI：**  
```bash
dotnet add package GroupDocs.Redaction
```

**使用套件管理員：**  
```bash
Install-Package GroupDocs.Redaction
```

或在 NuGet 套件管理員 UI 中搜尋 “GroupDocs.Redaction”，並安裝最新版本。

### 授權取得

你可以先使用免費試用或申請臨時授權。長期專案請從官方網站購買授權。

### 基本初始化

套件安裝完成後，建立一個索引以保存文件的參考：

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## 實作指南

### 功能 1：為文字文件 (.txt) 設定過濾條件

#### 如何為文字文件依檔案副檔名過濾

1. **定義索引與文件資料夾**  
   設定來源檔案所在的路徑：

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **建立索引**  
   將來源資料夾中的所有檔案載入索引：

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **使用檔案副檔名過濾設定搜尋選項**  
   告訴引擎僅考慮 *.txt 檔案：

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **執行搜尋**  
   執行查詢；過濾條件會忽略非文字檔案：

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *說明*：`Search` 方法會回傳符合過濾條件的匹配項目，顯著減少雜訊並提升效能。

### 功能 2：檔案路徑過濾

#### 為什麼使用檔案路徑過濾？

有時你需要將搜尋限制在特定部門資料夾或符合命名慣例的一組檔案。路徑過濾正好能做到這點。

1. **定義索引與文件資料夾**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **建立索引**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **使用基於路徑的正規表達式設定搜尋選項**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   此正規表達式會匹配完整路徑中包含「Lorem」字樣的任何檔案，讓你能針對特定子資料夾。

4. **執行基於路徑的搜尋**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## 實務應用
- **法律文件管理** – 快速定位以純文字檔儲存的相關合約。  
- **學術研究** – 僅提取屬於特定專案資料夾的 *.txt 研究筆記。  
- **企業報告** – 依部門路徑（例如 `/Finance/2025/`）過濾內部報告。  

## 效能考量
- 僅索引實際需要的文件類型；不必要的檔案會增加索引大小與搜尋時間。  
- 使用排程工作呼叫 `index.Add()` 以保持索引即時更新，涵蓋新檔或變更檔案。  
- 使用簡單的正規表達式；過於複雜的模式會拖慢搜尋引擎。  
- 在不再需要時釋放 `Index` 物件，以釋放記憶體。  

## 結論
現在你已了解如何使用 GroupDocs.Redaction for .NET **依檔案副檔名過濾** 以及套用 **檔案路徑過濾**。這些技巧讓你對大型文件集合擁有精細的控制，使搜尋更快且更相關。接下來，可嘗試結合多種過濾條件或將搜尋整合至更大的應用工作流程中。

## 常見問答

**Q1: 我可以過濾非文字檔的文件嗎？**  
A1: 可以，GroupDocs.Redaction 支援多種格式。將 `CreateFileExtension` 的參數改為想要的副檔名（例如 ".pdf"）。

**Q2: 我該如何定期更新搜尋索引？**  
A2: 排程背景服務或 cron 工作，對想保持最新的目錄執行 `index.Add()`。

**Q3: 依檔案路徑過濾會有效能影響嗎？**  
A3: 經過適當優化的正規表達式影響極小，但仍建議使用自己的資料集進行效能測試。

**Q4: 我可以結合多個過濾條件以獲得更精細的搜尋嗎？**  
A4: 當然可以。你可以串接過濾條件或建立複合過濾，以同時針對檔案類型與路徑。

**Q5: 我在哪裡可以找到更多關於 GroupDocs.Redaction 的資源？**  
A5: 前往官方文件 [GroupDocs 文件說明](https://docs.groupdocs.com/search/net/) 取得詳細指南與 API 參考。

## 常見問題

**Q: `SearchDocumentFilter` 能處理加密檔案嗎？**  
A: 此過濾器僅作用於檔案中繼資料，只要在索引時提供必要的解密憑證，加密檔案仍會被索引。

**Q: 我可以使用萬用字元而非正規表達式進行路徑過濾嗎？**  
A: 目前 API 需要正規表達式，但你可以模擬簡單的萬用字元（例如 `.*` 代表任意字元）。

**Q: 索引多大時需要考慮分片？**  
A: 幾百 GB 的索引可能需要拆分為多個邏輯索引；隨著集合增長請測試效能。

**Q: 有內建方法可從索引中移除文件嗎？**  
A: 有——呼叫 `index.Delete(documentId)` 或 `index.DeleteAll()` 以管理過時的條目。

**Q: 有辦法在載入完整文件前預覽搜尋結果嗎？**  
A: `SearchResult` 物件包含摘要資訊，可在 UI 中顯示，而無需開啟整個檔案。

## 資源
- **文件說明**： [GroupDocs 文件說明](https://docs.groupdocs.com/search/net/)  
- **API 參考**： [GroupDocs API 參考](https://reference.groupdocs.com/redaction/net)  
- **下載**： [GroupDocs 下載](https://releases.groupdocs.com/search/net/)  
- **免費支援**： [GroupDocs 論壇](https://forum.groupdocs.com/c/search/10)  
- **臨時授權**： [GroupDocs 臨時授權](https://purchase.groupdocs.com/temporary-license)  

---

**最後更新：** 2026-04-02  
**測試環境：** GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs