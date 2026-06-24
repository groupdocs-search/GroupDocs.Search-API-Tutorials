---
date: '2026-04-05'
description: 學習如何使用 GroupDocs.Search 與 GroupDocs.Redaction 建立 .NET 搜尋索引、將文件加入索引，以及在查詢時轉義特殊字元。
keywords:
- create search index .net
- add documents to index
- escape special characters query
title: 使用 GroupDocs Redaction 與 Search 建立 .NET 搜尋索引
type: docs
url: /zh-hant/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/
weight: 1
---

# 精通 GroupDocs Redaction 與 Search 在 .NET 中的應用：高效文件管理與安全搜尋

管理大量文件集合很快會變得難以應付，尤其是當您需要 **create search index .NET** 解決方案，同時保護敏感資訊時。無論是建置法律檔案庫、醫療紀錄系統，或是電商目錄，**GroupDocs.Redaction** 與 **GroupDocs.Search for .NET** 的組合都能提供安全且高效的索引、搜尋與遮蔽功能。

## 快速解答
- **「create search index .NET」是什麼意思？** 它指的是在磁碟上建立可搜尋的資料結構，讓您的 .NET 應用程式能快速定位文件。  
- **哪個函式庫負責遮蔽？** GroupDocs.Redaction 會從文件中移除或遮蔽敏感資料。  
- **如何將文件加入索引？** 使用 `index.Add(yourFolderPath)` 以自動匯入檔案。  
- **查詢時需要轉義特殊字元嗎？** 需要——請轉義 `&`、`|`、`(`、`)` 等字元，以避免解析錯誤。  
- **此方法適用於大型資料集嗎？** 絕對可以；索引具備可擴充性，且可增量更新。

## 什麼是「create search index .NET」？
在 .NET 中建立搜尋索引是指構建一個永久性的結構，將詞彙映射到出現該詞彙的文件。此索引可在不每次查詢時掃描所有檔案的情況下，實現快速的全文搜尋。

## 為何結合 GroupDocs.Search 與 GroupDocs.Redaction？
- **安全第一：** 在顯示搜尋結果前先遮蔽個人資料。  
- **效能：** 搜尋索引已優化以提升速度，而遮蔽僅在需要時於原始檔案上執行。  
- **彈性：** 兩個函式庫皆內建支援多種檔案格式（PDF、DOCX、影像等）。

## 先決條件
- **GroupDocs.Search** 版本 21.8 以上  
- **GroupDocs.Redaction** for .NET（相容版本）  
- .NET Core SDK 3.1 或更新版本  
- 包含欲索引文件的資料夾  

## 設定 GroupDocs.Redaction for .NET
### 安裝
```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

### 取得授權
1. **Free Trial** – 測試核心功能。  
2. **Temporary License** – 延長試用限制。  
3. **Full License** – 解鎖可投入生產的功能。

### 基本初始化
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the file path of the document
Redactor redactor = new Redactor("path/to/document.pdf");
```

## 如何建立 search index .NET
以下是逐步說明，展示如何 **create search index .NET** 專案、設定特殊字元處理，並準備查詢。

### 步驟 1：建立索引
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchForSpecialCharacters";

// Create an index at the specified path. The second parameter 'true' allows overwriting existing indexes.
Index index = new Index(indexFolder, true);
```
*此行會建立實體索引資料夾，並為文件匯入做好準備。*

### 步驟 2：設定字元類型
```csharp
// Configure character types for '&' as a letter and '-' as a separator within the alphabet dictionary of the index.
index.Dictionaries.Alphabet.SetRange(new char[] { '&' }, CharacterType.Letter);
index.Dictionaries.Alphabet.SetRange(new char[] { '-' }, CharacterType.Separator);
```
*自訂字元處理可確保諸如「rock&roll‑music」的查詢能正確解析。*

### 步驟 3：將文件加入索引
```csharp
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index.
index.Add(documentsFolder);
```
*此處我們以批次方式 **add documents to index**，使所有支援的檔案皆可搜尋。*

### 步驟 4：在查詢中定義並轉義特殊字元
```csharp
using System.Text;

string word = "rock&roll-music";
StringBuilder result = new StringBuilder();

// Replace separators with space characters in the query string.
for (int i = 0; i < word.Length; i++)
{
    char character = word[i];
    CharacterType characterType = index.Dictionaries.Alphabet.GetCharacterType(character);
    if (characterType == CharacterType.Separator)
    {
        result.Append(' ');
    }
    else
    {
        result.Append(character);
    }
}

// Escape special characters.
const string specialCharacters = "():\"&|!^~*?\\";
for (int i = result.Length - 1; i >= 0; i--)
{
    char c = result[i];
    if (specialCharacters.Contains(c.ToString()))
    {
        result.Insert(i, '\\');
    }
}

string query = result.ToString();
if (query.Contains(" "))
{
    query = "\"" + query + "\"";
}
```
*此區塊的 **escape special characters query** 邏輯確保搜尋引擎能正確解析輸入。*

### 步驟 5：執行搜尋查詢
```csharp
// Perform the search using the prepared query string.
SearchResult searchResult = index.Search(query);
```
*`SearchResult` 物件現在包含所有符合的文件，可進一步處理或顯示。*

## 實務應用
1. **Legal Document Management** – 在數千份合約中定位條款，同時遮蔽個人資料。  
2. **Medical Records Search** – 快速搜尋患者筆記，然後在分享前遮蔽 PHI。  
3. **E‑commerce Catalogs** – 透過自訂分詞處理 SKU 代碼與品牌名稱，提供強大的商品搜尋功能。

## 效能考量
- **Index Refresh:** 當檔案變更時重新執行 `index.Add()` 或使用增量更新。  
- **Memory Management:** 完成後釋放 `Index` 物件，特別是在高負載服務中。  
- **Async Operations:** 將搜尋呼叫包裹在 `Task.Run` 中，以實現非阻塞的 UI 或 API 回應。

## 常見問題與解決方案
| 問題 | 解決方案 |
|------|----------|
| 查詢含有 `&` 或 `-` 的詞彙時未返回結果 | 確保如 **步驟 2** 所示配置字元類型。 |
| 大型 PDF 造成高記憶體使用 | 啟用串流模式 (`index.Options.UseStreaming = true`) 並以批次方式處理結果。 |
| 遮蔽未套用於搜尋的片段 | 先遮蔽原始檔案，然後重新建立索引以反映已清理的內容。 |

## 常見問答

**Q: 如何自訂搜尋索引中的字元處理？**  
A: 使用 `index.Dictionaries.Alphabet.SetRange()` 將字元標記為字母、分隔符或標點符號。

**Q: 我可以索引多種文件格式嗎？**  
A: 可以——GroupDocs.Search 支援 PDF、Word、Excel、PowerPoint、影像等多種格式。

**Q: 在搜尋查詢中應如何處理特殊字元？**  
A: 請遵循 **Define and Escape Special Characters in Query** 步驟，將分隔符替換為空格，並在保留符號前加上反斜線 (`\`)。

**Q: 搜尋時會自動執行遮蔽嗎？**  
A: 遮蔽是獨立的步驟；您可以先遮蔽文件再重新建立索引，或在檢索後對結果進行遮蔽。

**Q: 我應該多久重建或更新一次索引？**  
A: 每當來源檔案變更時即更新索引；大多數環境中，每晚進行增量重建效果良好。

## 結論
您現在擁有一份完整、可投入生產的 **create search index .NET** 專案指南，結合強大的遮蔽功能。透過設定字元處理、安全轉義查詢字串，並定期更新索引，您即可為任何文件密集型應用提供快速且安全的搜尋體驗。

---

**最後更新：** 2026-04-05  
**測試環境：** GroupDocs.Search 21.8+、GroupDocs.Redaction 最新版  
**作者：** GroupDocs