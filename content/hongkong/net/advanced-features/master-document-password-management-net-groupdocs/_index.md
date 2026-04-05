---
date: '2026-04-05'
description: 學習如何使用 GroupDocs.Redaction 在 .NET 中建立密碼字典，並從字典中移除密碼，以實現安全的文件處理。
keywords:
- create password dictionary .net
- remove password from dictionary
- GroupDocs Redaction password management
title: 使用 GroupDocs Redaction 建立 .NET 密碼字典
type: docs
url: /zh-hant/net/advanced-features/master-document-password-management-net-groupdocs/
weight: 1
---

# 使用 GroupDocs Redaction 建立 .NET 密碼字典

在當今的數位世界中，保護敏感文件至關重要，**您將學習如何使用 GroupDocs.Redaction 建立 .NET 密碼字典**。無論您是保護公司報告的商業專業人士，還是保護個人檔案的個人使用者，強大的密碼字典都能讓您掌控存取權限並簡化安全索引。

**您將學習**
- 如何使用 GroupDocs **建立 .NET 密碼字典**
- 當不再需要時，**從字典中移除密碼** 的技巧
- 使用嵌入式密碼安全索引文件的步驟
- 如何有效搜尋受密碼保護的檔案

## 快速解答
- **什麼是密碼字典？** 一個將檔案路徑映射到其密碼的鍵值儲存。  
- **為什麼使用 GroupDocs.Redaction？** 它在同一個 API 中整合了塗銷與密碼管理。  
- **我需要授權嗎？** 試用版可用於測試；正式環境需購買完整授權。  
- **我可以索引大型資料夾嗎？** 可以——只要確保管理好字典大小。  
- **支援 .NET Core 嗎？** 當然，GroupDocs.Redaction 可在 .NET Core 及更高版本上運作。  

## GroupDocs 中的密碼字典是什麼？
密碼字典是一個簡單的記憶體或磁碟集合，用於將每份文件的位置與其開啟密碼關聯起來。GroupDocs.Search 在索引過程中會讀取此字典，從而自動開啟加密檔案。

## 為什麼要在 .NET 中建立密碼字典？
建立密碼字典可集中管理憑證、減少重複程式碼，並支援批次操作，例如在多個受保護檔案中搜尋，而無需每次手動指定密碼。

## 前置條件
- **函式庫**：`GroupDocs.Search` 與 `GroupDocs.Redaction` NuGet 套件。  
- **環境**：.NET Core 3.1 以上（或 .NET 6/7）。  
- **知識**：基本的 C# 與檔案 I/O 概念。

## 為 .NET 設定 GroupDocs.Redaction

### 安裝套件
**使用 .NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console（Visual Studio）**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet 套件管理員 UI**
- 搜尋「GroupDocs.Redaction」並安裝最新版本。

### 取得授權
- **免費試用：** 使用臨時試用授權以探索功能。  
- **購買：** 若需在試用期後持續使用，請考慮購買完整授權。詳細說明請參閱他們的[購買頁面](https://purchase.groupdocs.com/temporary-license/)。

### 初始化與設定
```csharp
using GroupDocs.Redaction;

// Basic initialization of the Redactor
RedactorSettings settings = new RedactorSettings();
var redactor = new Redactor("path/to/document.pdf", settings);
```

環境已就緒，讓我們深入核心實作。

## 如何在 .NET 中建立密碼字典

### 步驟 1：初始化索引
```csharp
using GroupDocs.Search;
using System.IO;

string indexFolder = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Index");
Index index = new Index(indexFolder);
```
*說明：* 我們建立一個 `Index` 物件，用於保存密碼字典及其他搜尋中繼資料。

### 步驟 2：清除現有密碼（若有）
```csharp
if (index.Dictionaries.DocumentPasswords.Count > 0)
{
    index.Dictionaries.DocumentPasswords.Clear();
}
```
*說明：* 移除過期條目可確保從乾淨的狀態開始，避免意外使用舊密碼。

### 步驟 3：將密碼加入字典
```csharp
string key1 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "English.docx"));
index.Dictionaries.DocumentPasswords.Add(key1, "123456");
```
*說明：* 這會將文件路徑（`key1`）對應到其密碼（`"123456"`）。對每個受保護的檔案重複此步驟。

### 步驟 4：取得並移除密碼
```csharp
if (index.Dictionaries.DocumentPasswords.Contains(key1))
{
    string password = index.Dictionaries.DocumentPasswords.GetPassword(key1);
    index.Dictionaries.DocumentPasswords.Remove(key1);
}
```
*說明：* 您可以在需要時取得已儲存的密碼，並在文件不再需要存取時 **從字典中移除密碼**。

## 如何一次加入多筆密碼至字典
```csharp
string key2 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "English.docx"));
index.Dictionaries.DocumentPasswords.Add(key2, "123456");
string key3 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Lorem ipsum.docx"));
index.Dictionaries.DocumentPasswords.Add(key3, "123456");
```
*說明：* 一次加入多筆條目可讓您批次管理多個檔案的存取權限。

## 如何使用密碼索引文件
```csharp
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
index.Add(documentsFolder);
```
*說明：* `Add` 方法會讀取每個檔案，自動套用字典中的密碼，並建立可搜尋的索引。

## 如何在已索引的受密碼保護文件中搜尋
```csharp
string query = "ipsum OR increasing";
SearchResult result = index.Search(query);
```
*說明：* 索引完成後，您可以對所有文件執行一般搜尋查詢，無論其是否加密。

## 常見問題與解決方案
- **密碼未套用** – 請確認作為字典鍵的檔案路徑與實際檔案位置完全相符（使用 `Path.GetFullPath`）。  
- **大型字典影響效能** – 定期清除未使用的條目，若字典變得非常龐大，可考慮將其持久化至輕量級資料庫。  
- **授權錯誤** – 確保在應用程式啟動時正確引用您的試用或完整授權檔案。

## 常見問答

**Q: 我可以免費使用 GroupDocs.Redaction 嗎？**  
A: 您可以先使用臨時試用授權。若需長期使用，必須購買完整授權。

**Q: 如何有效處理大型文件集？**  
A: 使用高效的索引與記憶體管理方式，以有效處理更大的資料集。

**Q: GroupDocs.Redaction 與所有 .NET 版本相容嗎？**  
A: 是的，它支援最新的 .NET Core 版本。請隨時檢查相容性更新。

**Q: 我可以無縫搜尋受密碼保護的文件嗎？**  
A: 可以，一旦使用密碼完成索引，即可使用 GroupDocs.Search 執行搜尋，毫無問題。

**Q: 設定 GroupDocs.Redaction 時有哪些常見的故障排除技巧？**  
A: 確認您的授權已啟用，且文件目錄的路徑正確指定。請參閱[支援論壇](https://forum.groupdocs.com/)以獲得進一步協助。

## 結論
透過上述步驟，您現在已了解如何 **建立 .NET 密碼字典**，以及在適當時機 **從字典中移除密碼**。此方法可集中憑證處理、提升安全性，並實現對加密檔案的強大搜尋。可進一步探索與雲端儲存或文件管理系統的整合，以擴充您的解決方案。

---

**最後更新：** 2026-04-05  
**測試環境：** GroupDocs.Redaction 23.2 for .NET  
**作者：** GroupDocs