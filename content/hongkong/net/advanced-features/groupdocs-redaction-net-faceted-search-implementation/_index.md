---
date: '2026-04-02'
description: 學習如何使用 GroupDocs.Search 和 GroupDocs.Redaction 在 .NET 中建立 GroupDocs 搜尋索引並將文件加入索引，同時實作分面搜尋。
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: 使用 Redaction .NET 分面搜尋建立 GroupDocs 搜尋索引
type: docs
url: /zh-hant/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# 使用 Redaction .NET 分面搜尋建立 GroupDocs 搜尋索引

在現代應用程式中，**使用 GroupDocs 建立搜尋索引**對於快速、精確的文件檢索至關重要。無論您處理的是法律合約、產品目錄或大型知識庫，完善的索引都能讓您**將文件加入索引**，並在數秒內執行強大的分面搜尋。本教學將帶您完整了解整個流程——從設定 GroupDocs.Redaction 到構建簡單與複雜的分面查詢——讓您在 .NET 專案中提供即時的搜尋體驗。

## 快速解答
- **主要目的為何？** 使用 GroupDocs 建立搜尋索引並啟用分面搜尋。  
- **需要哪些函式庫？** GroupDocs.Redaction 與 GroupDocs.Search（適用於 .NET）。  
- **如何將文件加入索引？** 在初始化索引後使用 `index.Add(documentsFolder)`。  
- **能執行複雜查詢嗎？** 可以，將物件查詢與邏輯運算子結合以進行進階篩選。  
- **是否需要授權？** 開發階段可使用免費試用版，正式上線則需商業授權。

## 什麼是分面搜尋，為何要與 GroupDocs 結合使用？
分面搜尋允許使用者同時套用多個篩選條件（如類別、日期或作者）來細化結果。結合 **GroupDocs.Redaction** 後，您可取得符合遮蔽規則的安全可搜尋內容，十分適合合規性要求嚴格的環境。

## 先決條件

### 所需函式庫、版本與相依性
- **GroupDocs.Redaction .NET** – 最新穩定版。  
- **GroupDocs.Search .NET** – 與 Redaction 緊密合作以進行索引。

### 環境設定需求
- **IDE**：Visual Studio 2019 或更新版本。  
- **Framework**：.NET Core 3.1、.NET 5 或 .NET 6。  
- **OS 相容性**：Windows、Linux、macOS。

### 知識先備條件
具備基本的 C# 技能與對分面搜尋概念的高層次了解會有幫助，但本步驟指南對新手亦相當友善。

## 設定 GroupDocs.Redaction（適用於 .NET）

### 安裝資訊
您可以使用以下任一方法加入 GroupDocs.Redaction 套件：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- 搜尋 "GroupDocs.Redaction" 並安裝最新版本。

### 取得授權步驟
若要解鎖全部功能，請先使用免費試用版或取得永久授權：

1. 前往 [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) 了解授權方案。  
2. 按照畫面指示取得您的試用或購買授權檔案。

### 基本初始化與設定
套件安裝完成後，於應用程式中初始化 Redactor：

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## 如何建立 GroupDocs 搜尋索引

以下我們將實作分為兩個部分：**簡易分面搜尋** 與 **複雜查詢**。每個部分皆示範如何**建立 GroupDocs 搜尋索引**、加入文件以及執行查詢。

### 功能 1：簡易分面搜尋

**概述**  
分面搜尋允許使用者透過選取多個條件來縮小結果。本節示範使用 GroupDocs.Search 的簡單方法。

#### 步驟 1：定義索引與文件資料夾
設定索引所在的資料夾路徑以及原始文件所在的資料夾路徑。

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### 步驟 2：建立索引
在先前定義的資料夾中初始化搜尋索引。

```csharp
Index index = new Index(indexFolder);
```

#### 步驟 3：將文件加入索引
載入文件，使其可被搜尋。

```csharp
index.Add(documentsFolder);
```

#### 步驟 4：執行文字查詢搜尋
對 **content** 欄位執行基本文字查詢。

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### 步驟 5：執行物件查詢搜尋
使用物件導向查詢以取得更細緻的控制。

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### 功能 2：複雜查詢

**概述**  
當需要結合多個篩選條件（例如檔名模式與片語匹配）時，您可以使用邏輯運算子構建複雜查詢。

#### 步驟 1：定義索引與文件資料夾
在更進階的情境中重複使用相同的資料夾結構。

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### 步驟 2：建立索引並加入文件
（請參考簡易範例的步驟 2‑3；操作相同。）

#### 步驟 3：執行文字查詢搜尋
執行結合檔名與內容條件的複合文字查詢。

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### 步驟 4：建構並執行物件查詢
以程式方式構建相同的邏輯。

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

持續結合片語、範圍與布林運算子，以符合您的精確業務規則。

## 實務應用

1. **電子商務平台** – 依類別、價格與評分篩選商品。  
2. **文件管理系統** – 依作者、日期或機密等級搜尋合約。  
3. **內容入口網站** – 讓讀者依標籤、主題與發佈日期深入搜尋。

## 效能考量

- **索引刷新**：定期重新索引新檔或已更新的檔案，以維持搜尋速度。  
- **記憶體管理**：使用完畢後釋放 `Index` 物件，特別是處理大型資料集時。  
- **非同步索引**：使用 `Task.Run` 或背景服務，避免在大量索引時造成 UI 卡頓。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **找不到索引** | 確認 `indexFolder` 路徑，並確保該資料夾具有寫入權限。 |
| **未返回結果** | 確認您查詢的欄位（例如 `Content`、`Filename`）已被索引。 |
| **記憶體不足錯誤** | 將文件分批處理，並考慮增大 .NET GC 堆大小。 |

## 常見問答

**Q: 什麼是分面搜尋？**  
A: 分面搜尋允許使用者使用多個獨立的篩選條件（如類別、日期或作者）來細化結果。

**Q: 如何使用 GroupDocs.Search 處理大型資料集？**  
A: 使用增量索引、批次處理與非同步操作，以降低記憶體使用並提升效能。

**Q: 能將 GroupDocs 功能整合到現有的 .NET 應用程式嗎？**  
A: 可以，這些函式庫設計為可無縫整合至任何 .NET 專案。

**Q: 分面搜尋常見的問題是什麼？**  
A: 複雜的查詢語法以及確保所有相關欄位已被索引是常見挑戰；透過適當的測試與索引維護可減輕這些問題。

**Q: 如何取得 GroupDocs 的臨時授權？**  
A: 前往 [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) 申請試用授權，以在評估期間解鎖全部功能。

## 資源
- **文件**： [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API 參考**： [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**最後更新：** 2026-04-02  
**測試環境：** GroupDocs.Redaction 23.12 for .NET、GroupDocs.Search 23.12 for .NET  
**作者：** GroupDocs