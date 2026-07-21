---
date: '2026-07-21'
description: 了解如何使用 GroupDocs.Redaction for .NET 進行文件遮蔽，並建立可擴展的搜尋網絡。有效保護機密資訊。
keywords:
- how to redact documents
- how to set scaling
- redact confidential information
lastmod: '2026-07-21'
og_description: 使用 GroupDocs.Redaction for .NET 進行文件遮蔽並建立可擴展的系統。於可擴展的網絡中有效保護機密資訊。
og_image_alt: 'Guide: Redact documents securely using GroupDocs.Redaction .NET with
  scaling network'
og_title: 如何使用 GroupDocs.Redaction .NET – 安全遮蔽指南
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Learn how to redact documents using GroupDocs.Redaction for .NET and
    set up a scalable search network. Secure confidential information efficiently.
  headline: 'How to Redact Documents with GroupDocs.Redaction .NET: Secure Document
    Redaction and Network Setup'
  type: TechArticle
- description: Learn how to redact documents using GroupDocs.Redaction for .NET and
    set up a scalable search network. Secure confidential information efficiently.
  name: 'How to Redact Documents with GroupDocs.Redaction .NET: Secure Document Redaction
    and Network Setup'
  steps:
  - name: Install the NuGet Packages
    text: '**Using .NET CLI:** **Using Package Manager:** Or search for “GroupDocs.Redaction”
      in the NuGet Package Manager UI and install the latest stable release.'
  - name: Acquire and Apply a License
    text: '- **Free Trial** – evaluate all features for 30 days. - **Temporary License**
      – extend testing beyond the trial period. - **Full License** – unlock production‑grade
      performance and support.'
  - name: Initialize the Redactor
    text: '`Redactor` is the core class that represents a single document in memory
      and exposes redaction operations.'
  type: HowTo
- questions:
  - answer: Install the GroupDocs.Redaction NuGet package via .NET CLI or Package
      Manager.
    question: What is the first step?
  - answer: Use the `ConfiguringSearchNetwork.Configure` method to define base paths
      and ports, then spin up slave nodes.
    question: How do I set scaling?
  - answer: Yes—GroupDocs.Redaction supports over 30 file formats, including PDF,
      DOCX, PPTX, and common image types.
    question: Can I redact PDFs and images?
  - answer: A temporary or full license is required for production; a free trial is
      available for evaluation.
    question: What license do I need?
  - answer: Absolutely—both .NET Framework 4.5+ and .NET Core 3.1+ are fully supported.
    question: Is it .NET‑Core compatible?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document security
title: 如何使用 GroupDocs.Redaction .NET 進行文件遮蔽：安全的文件遮蔽與網絡設定
type: docs
url: /zh-hant/net/document-management/mastering-groupdocs-redaction-net-secure-document-redaction/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 進行文件編輯：安全的文件編輯與網絡設置

在當今快速發展的數位世界中，安全地 **如何編輯文件** 是開發人員和 IT 團隊的首要關注。無論您是要保護個人健康記錄、法律合約或內部報告，GroupDocs.Redaction for .NET 為您提供經過實戰驗證的工具組，能在保留檔案其餘內容的同時移除機密資訊。本教學將指導您安裝程式庫、設定可擴展的搜尋網絡，並部署能處理高容量工作負載的編輯節點。

## 快速解答
- **第一步是什麼？** 透過 .NET CLI 或套件管理員安裝 GroupDocs.Redaction NuGet 套件。  
- **如何設定擴展？** 使用 `ConfiguringSearchNetwork.Configure` 方法定義基礎路徑與埠號，然後啟動從屬節點。  
- **我可以編輯 PDF 和圖片嗎？** 可以 — GroupDocs.Redaction 支援超過 30 種檔案格式，包括 PDF、DOCX、PPTX 以及常見的圖片類型。  
- **我需要什麼授權？** 生產環境需要臨時或完整授權；亦提供免費試用供評估。  
- **它相容 .NET‑Core 嗎？** 完全相容 — 支援 .NET Framework 4.5+ 與 .NET Core 3.1+。

## 什麼是文件編輯？
文件編輯是永久移除或遮蔽檔案中敏感內容的過程，使其無法在之後被恢復或檢視。此作業常用於法律、醫療與金融領域，以在公開或與第三方分享文件前保護個人識別資訊、商業機密與機密資料。GroupDocs.Redaction 以程式方式執行此操作，確保符合隱私法規，且不需手動編輯。

## 為何使用 GroupDocs.Redaction for .NET？
GroupDocs.Redaction 支援 **50+ 輸入與輸出格式**，且能在不將整個文件載入記憶體的情況下處理數百頁檔案，與手動編輯工具相比可減少高達 40 % 的 CPU 使用率。程式庫亦內建 OCR 用於掃描圖像，意味著您可以自動編輯圖片內的文字。

## 前置條件
- **必要函式庫**：GroupDocs.Redaction for .NET、GroupDocs.Search.Scaling（相容版本）。  
- **開發環境**：Visual Studio 2022 或任何相容 .NET 的 IDE。  
- **伺服器存取**：至少一台機器（或 VM）用於托管主節點，並需額外機器作為從屬節點。  
- **知識需求**：基本的 C# 與 .NET 概念，熟悉檔案 I/O。

## 如何一步步編輯文件
載入來源檔案、定義編輯區域，並儲存結果 — 只需幾行程式碼即可完成。

只需兩行程式碼即可載入、編輯並儲存 PDF：實例化 `Redactor` 物件、加入 `RedactionArea`，然後呼叫 `Save`。此直接回應模式確保您能在任何現有工作流程中整合編輯功能，且無需大量樣板程式碼。

### 步驟 1：安裝 NuGet 套件
**使用 .NET CLI：**  
```shell
dotnet add package GroupDocs.Redaction
```  

**使用套件管理員：**  
```powershell
Install-Package GroupDocs.Redaction
```  

或在 NuGet 套件管理員 UI 中搜尋 “GroupDocs.Redaction”，並安裝最新的穩定版。

### 步驟 2：取得並套用授權
- **免費試用** – 評估所有功能，期限 30 天。  
- **臨時授權** – 在試用期結束後延長測試。  
- **完整授權** – 解鎖生產等級的效能與支援。

### 步驟 3：初始化 Redactor
`Redactor` 是核心類別，代表記憶體中的單一文件，並提供編輯操作。  
```csharp
using GroupDocs.Redaction;

// Initialize the Redactor
Redactor redactor = new Redactor("your-document-path");
```  

## 如何為搜尋網絡設定擴展？
`ConfiguringSearchNetwork.Configure` 是一個輔助方法，用於以指定的路徑與埠號初始化搜尋網絡環境。它設定來源文件的基礎目錄、指派起始 TCP 埠，並自動將每個節點註冊至叢集。此配置允許多個節點同時處理編輯請求，提升吞吐量，並確保伺服器群組的負載平衡。  
```csharp
   using GroupDocs.Search.Scaling.Configuring;

   string basePath = @"YOUR_DOCUMENT_DIRECTORY";
   int basePort = 49136; // Change if port is busy

   Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
   ```  

- **basePath** – 包含來源文件的根資料夾。  
- **basePort** – 起始 TCP 埠號；每個節點會自動遞增此值。

## 如何部署從屬節點？
`SearchNode.StartSlaveNode` 會啟動次要搜尋節點，並向主節點註冊以處理編輯任務。此方法需要主節點的位址、唯一的節點識別碼，以及可選的逾時設定。啟動後，從屬節點會監聽傳入工作，平行處理文件，並將狀態回報給主節點，提供高可用性與容錯能力。  
```csharp
   using GroupDocs.Search.Scaling;
   using System;

   int sendTimeout = 3000; // Timeout in milliseconds
   int receiveTimeout = 3000;
   int connectTimeout = 3000;
   int retryTimeout = 1000;

   SearchNetworkNode node1 = SearchNetworkNode.CreateSlaveNode(
       1,
       basePath + "Node1\",
       sendTimeout, 
       receiveTimeout, 
       connectTimeout, 
       retryTimeout);
   ```  

- 根據預期的網路延遲調整 `timeout` 參數。  
- 在地理上分散節點，以降低遠端使用者的延遲。

## 常見問題與解決方案
- **埠衝突** – 確認沒有其他服務佔用選定的 `basePort`。可使用 `netstat` 或 Windows 資源監視器來偵測衝突。  
- **檔案存取錯誤** – 確保執行身分對 `basePath` 具有讀寫權限。  
- **大型檔案逾時** – 提高節點的 `timeout` 值，或在編輯前將巨大的 PDF 拆分為較小的片段。

## 常見問答

**Q:** GroupDocs.Redaction for .NET 是什麼？  
**A:** 它是一個 .NET 程式庫，讓開發人員能以程式方式從超過 30 種文件格式中移除或遮蔽敏感資料，同時保留版面配置與中繼資料。

**Q:** 如何使用 GroupDocs.Search.Scaling 設定搜尋網絡？  
**A:** 呼叫 `ConfiguringSearchNetwork.Configure` 並傳入文件目錄與基礎埠號，然後使用 `SearchNode.StartSlaveNode` 啟動從屬節點。

**Q:** 我可以在不同的伺服器上部署節點嗎？  
**A:** 可以 — 每個節點透過 TCP 向主節點註冊，讓您能在任意數量的機器上水平擴展。

**Q:** 設定逾時時常見的陷阱是什麼？  
**A:** 網路延遲或大型檔案可能導致預設逾時值過低；請根據環境中的效能測試進行調整。

**Q:** 我可以在哪裡找到更多關於 GroupDocs.Redaction 的資源？  
**A:** 請參閱以下官方文件、API 參考、最新發行頁面、社群論壇與臨時授權入口。

## 資源

- **文件**: [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/search/net/)
- **API 參考**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **下載**: [Latest Releases](https://releases.groupdocs.com/search/net/)
- **免費支援**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **臨時授權**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)
- 其他連結: [documentation](https://docs.groupdocs.com/search/net/), [API reference](https://reference.groupdocs.com/redaction/net)

---

**最後更新:** 2026-07-21  
**測試環境:** GroupDocs.Redaction 23.9 for .NET, GroupDocs.Search.Scaling 2.4  
**作者:** GroupDocs

## 相關教學

- [精通 .NET 中的文件管理與 GroupDocs.Redaction：授權設定與 HTML 搜尋高亮顯示](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
- [精通 GroupDocs.Redaction .NET：設定與事件處理以實現安全文件管理](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [精通 GroupDocs.Redaction .NET：配置與同步搜尋網絡以達到最佳資料管理](/search/net/search-network/groupdocs-redaction-net-search-network-sync/)