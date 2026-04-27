---
date: '2026-04-27'
description: 學習如何使用 GroupDocs.Redaction .NET 來遮蔽敏感資訊，同時管理文件搜尋器並在文件中突出顯示文字。
keywords:
- redact sensitive information
- automate document review
- highlight text in documents
title: 使用 GroupDocs.Redaction .NET 進行敏感資訊遮蔽 – 查找器管理與突出顯示
type: docs
url: /zh-hant/net/document-management/groupdocs-redaction-net-finder-management-guide/
weight: 1
---

# 使用 GroupDocs.Redaction .NET 進行敏感資訊遮蔽 – 查找器管理與突顯

在文件中管理與突顯文字可能相當具挑戰性，尤其是處理敏感資訊時。透過 GroupDocs.Redaction .NET 強大的查找器管理與突顯功能，您可以**有效遮蔽敏感資訊**。  

本指南將逐步說明從設定 SDK、加入、移除與刷新查找器，到突顯已找到的字詞，使其在審閱時更為顯眼。

## 快速解答
- **什麼是「遮蔽敏感資訊」？** 從文件中移除或隱蔽機密資料（例如社會安全號碼、姓名），使其能安全共享。  
- **哪個函式庫可協助自動化文件審查？** GroupDocs.Redaction .NET 提供內建查找器，可自動定位並遮蔽資料。  
- **我需要授權嗎？** 是，必須擁有開發或正式授權；亦提供試用金鑰供評估使用。  
- **在遮蔽時能同時突顯文字嗎？** 當然可以——突顯已找到的字詞讓審閱者確認將被遮蔽的內容。  
- **支援哪些 .NET 版本？** 完全支援 .NET Framework 4.6+ 與 .NET Core/5/6+。

## 什麼是「遮蔽敏感資訊」？
遮蔽敏感資訊是指以程式方式在檔案內定位機密資料，並將其移除或套用視覺遮罩，使資料無法被讀取。此程序對於合規、隱私與安全文件共享至關重要。

## 為何使用 GroupDocs.Redaction 自動化文件審查？
自動化文件審查可節省大量手動時間，減少人為錯誤，並確保在大量文件集上保持一致的合規性。透過查找器，您可以掃描信用卡號、日期或自訂詞彙等模式，然後一次性套用遮蔽或突顯。

## 前置條件

- **.NET Framework** 4.6+ **或** **.NET Core/5/6** 已安裝。  
- Visual Studio（任何近期版本）用於開發。  
- 具備基本的 C# 知識及面向物件概念的熟悉度。  

### 設定 GroupDocs.Redaction for .NET

將函式庫加入專案，使用以下任一指令：

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

您也可以在 NuGet 套件管理員 UI 中搜尋 **GroupDocs.Redaction**，並安裝最新的穩定版。

若需取得授權，請前往 [GroupDocs Redaction Purchase](https://purchase.groupdocs.com/)，下載後依照啟用步驟完成授權。

以下為初始化遮蔽器的最小範例：

```csharp
using GroupDocs.Redaction;

// Basic initialization of the redactor with a document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("your-document-path", settings);
```

## 實作指南

以下我們將實作分成多個邏輯區段，直接對應您將使用的核心功能，以**遮蔽敏感資訊**與**在文件中突顯文字**為目標。

### 字元查找器管理

管理字元查找器可讓您在執行期間控制要搜尋的模式。

#### 新增查找器
```csharp
public void Add(IFinder finder)
{
    // Adds a new finder to the list of active finders.
    finders.Add(finder);
}
```
*目的*：註冊 `IFinder` 實作，使遮蔽器能定位特定字元或字串。

#### 移除查找器
```csharp
public void Remove(IFinder finder)
{
    // Mark a finder for removal.
    toRemove.Add(finder);
}
```
*目的*：在安全修改集合之前延遲移除，以防止列舉錯誤。

### 片語與詞彙初始化

片語與詞彙查找器讓您搜尋多字詞表達或單一關鍵字。

#### 初始化詞彙與片語
```csharp
public SuperFinder(string[] terms, string[][] phrases)
{
    // Initialize term finders and add them to the list.
    if (terms != null)
    {
        foreach (var term in terms)
        {
            var finder = new SeparateWordFinder(this, term);
            finders.Add(finder);
        }
    }

    // Initialize phrase finders and add them to the list.
    if (phrases != null)
    {
        foreach (var phrase in phrases)
        {
            var finder = new PhraseFirstWordFinder(this, phrase);
            finders.Add(finder);
        }
    }
}
```
*目的*：為 redactor 填充簡單的詞彙查找器與更複雜的片語查找器，實現強大的搜尋功能。

### 查找器刷新

刷新確保每個查找器重新開始，這在新增或移除查找器後尤為重要。

```csharp
public void Flush()
{
    // Reset each finder's state.
    foreach (var finder in finders)
    {
        finder.Flush();
    }
}
```
*目的*：清除快取狀態，使後續搜尋保持準確。

### 已找到字詞管理

有效處理已找到的字詞可提升效能，特別是在大型文件中。

#### 新增已找到的字詞
```csharp
public LinkedListNode<FoundWord> AddFoundWord(FoundWord foundWord)
{
    // Add a found word to the list.
    var node = foundWords.AddFirst(foundWord);
    return node;
}
```
*目的*：在鏈結串列的頭部插入新的 `FoundWord`，實現 O(1) 插入。

#### 移除已找到的字詞
```csharp
public void RemoveFoundWords(List<LinkedListNode<FoundWord>> words)
{
    // Remove specified words from the list.
    foreach (var node in words)
    {
        foundWords.Remove(node);
    }
}
```
*目的*：批次移除詞彙，減少迭代開銷。

### 突顯已找到的字詞

突顯有助於審閱者快速辨識將被遮蔽的內容。

```csharp
public void HighlightFoundWords()
{
    // Iterate through each found word and highlight it.
    while (foundWords.Count > 0)
    {
        var foundWord = foundWords.First.Value;
        foundWords.RemoveFirst();
        foundWord.Highlight();
    }
}
```
*目的*：對每個 `FoundWord` 套用視覺突顯，然後從處理佇列中移除。

## 實務應用

1. **敏感資訊遮蔽** – 自動隱藏法律合約中的個人資料，如姓名、身分證號或信用卡號碼。  
2. **自動化文件審查** – 突顯關鍵條款或詞彙，讓審查者聚焦於高影響區段。  
3. **內容管理系統** – 在出版工作流程中動態管理與突顯內容變更。

## 效能考量

- **最小化查找器變動**：僅加入必要的查找器；不必要的新增/移除循環會增加負擔。  
- **明智使用 `LinkedList`**：提供 O(1) 的插入/刪除，適合大型結果集。  
- **定期呼叫 `Flush()`**：在長時間批次作業中保持記憶體使用可預測。

## 結論

遵循本指南後，您已掌握如何使用 GroupDocs.Redaction .NET **遮蔽敏感資訊**與**在文件中突顯文字**。一步步設定查找器、管理其生命週期並套用突顯，為建構安全、 自動化的文件處理管線奠定了堅實基礎。

## 常見問題

**Q: 如何安裝 GroupDocs.Redaction？**  
A: 使用 .NET CLI (`dotnet add package GroupDocs.Redaction`) 或套件管理員主控台 (`Install-Package GroupDocs.Redaction`)。

**Q: 刷新查找器的目的為何？**  
A: 刷新會重設內部狀態，確保後續搜尋從乾淨的環境開始，返回準確結果。

**Q: 可以在 .NET Core 上使用 GroupDocs.Redaction 嗎？**  
A: 可以，函式庫同時支援 .NET Framework 與 .NET Core（含 .NET 5/6）。

**Q: 如何有效管理多個已找到的字詞？**  
A: 將它們存於 `LinkedList`，並使用批次移除方法，以保持操作快速且記憶體友好。

**Q: 常見的實務案例有哪些？**  
A: 用於合規的自動遮蔽、與 CMS 平台整合以動態突顯，及加速法律文件審查等。

## 資源

- [GroupDocs Redaction 文件說明](https://docs.groupdocs.com/search/net/)
- [API 參考](https://reference.groupdocs.com/redaction/net)
- [下載最新版本](https://releases.groupdocs.com/redaction/net)

---

**最後更新：** 2026-04-27  
**測試版本：** GroupDocs.Redaction 5.0（撰寫時的最新版本）  
**作者：** GroupDocs