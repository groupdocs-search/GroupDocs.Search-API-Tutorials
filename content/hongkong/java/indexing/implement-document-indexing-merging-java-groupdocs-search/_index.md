---
date: '2026-01-03'
description: 學習如何在 Java 中使用 GroupDocs.Search 將文件新增至索引並取消合併操作。完整的文件管理 Java 指南。
keywords:
- document indexing in Java
- merging documents with GroupDocs
- GroupDocs.Search Java tutorial
title: 在 Java 中使用 GroupDocs.Search 將文件加入索引並合併
type: docs
url: /zh-hant/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# 在 Java 中使用 GroupDocs.Search 添加文件至索引並合併

在當今快速發展的數位環境中，學習**如何有效地將文件添加至索引**對任何**文件管理 java**解決方案都至關重要。無論您處理合約、發票或內部報告，良好結構的索引都能讓您在毫秒內檢索資訊。本教學將指導您建立索引、添加文件、設定合併選項，甚至在需要時**取消合併操作**——全部使用 GroupDocs.Search for Java。

## 快速解答
- **「add documents to index」是什麼意思？** 它會指示 GroupDocs.Search 掃描資料夾，並為每個檔案儲存可搜尋的中繼資料。  
- **我可以停止長時間的合併嗎？** 可以——使用 `Cancellation` 物件在逾時後**取消合併操作**。  
- **我需要授權嗎？** 免費試用或臨時授權可用於測試；商業授權則解鎖全部功能。  
- **需要哪個 Java 版本？** JDK 8 或更新版本。  
- **這適用於大型資料集嗎？** 絕對適用——只需監控記憶體並使用增量索引。

## 在 GroupDocs.Search 中「add documents to index」是什麼？
將文件添加至索引是指將一組檔案輸入至 GroupDocs.Search，讓程式庫能分析其內容、擷取標記，並建立可搜尋的資料結構。完成索引後，您即可對所有文件執行快速的全文搜尋。

## 為何在 document management java 中使用 GroupDocs.Search？
- **可擴充的索引** – 能處理數千個檔案而不降低效能。  
- **豐富的 API** – 提供對索引、合併與取消的精細控制。  
- **跨格式支援** – 開箱即支援 PDF、Word、Excel 以及許多其他格式。

## 前置條件
- **GroupDocs.Search for Java** 版本 25.4 或更新。  
- Maven（或手動下載 JAR）。  
- 基本的 Java 知識與 JDK 8+ 環境。

## 設定 GroupDocs.Search for Java

### Maven 安裝
如果您使用 Maven 管理相依性，請將以下儲存庫與相依性加入您的 `pom.xml`：

```xml
<repositories>
    <repository>
        <id>repository.groupdocs.com</id>
        <name>GroupDocs Repository</name>
        <url>https://releases.groupdocs.com/search/java/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-search</artifactId>
        <version>25.4</version>
    </dependency>
</dependencies>
```

### 直接下載
或者，從官方網站下載最新的 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權
- **免費試用：** 在 GroupDocs 網站註冊以取得試用授權。  
- **臨時授權：** 如需延長評估，可申請臨時金鑰。  
- **商業授權：** 購買以供正式營運使用。

取得授權檔案後，將其放置於專案中，並依下文示範初始化程式庫。

## 實作指南

### 如何添加文件至索引 – 建立第一個索引
首先，建立一個空的索引，用於保存可搜尋的資料。

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **原因：** 此步驟會設定一個儲存容器，用於保存已索引的標記。

#### 添加文件至索引
現在指示 GroupDocs.Search 掃描資料夾並**添加文件至索引**。

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **原因：** 程式庫會讀取每個檔案，擷取文字，並將其儲存於 `index1`。

### 建立第二個索引以支援彈性工作流程
有時您需要分開的索引，例如用於隔離客戶的資料。

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **原因：** 多個索引讓您管理不同的文件集合，之後再將它們合併。

### 如何設定合併選項並取消合併操作
在合併之前，您可以微調流程，甚至在執行時間過長時停止它。

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **原因：** `Cancellation` 讓您能自動**取消合併操作**，防止任務失控。

### 合併索引
最後，將次要索引合併至主要索引。

```java
index1.merge(index2, options);
```

- **原因：** 呼叫此方法後，`index1` 會包含兩個來源的所有文件，提供統一的搜尋體驗。

## Document Management Java 的實務應用
- **法律事務所：** 整合多個辦公室的案件檔案。  
- **金融機構：** 將季報合併至單一可搜尋的儲存庫。  
- **企業：** 結合人力資源、合規與政策文件，以供全企業搜尋。

## 效能考量
- **增量索引：** 定期添加新檔案，而非重建整個索引。  
- **記憶體監控：** 大批次可能佔用大量 RAM；建議分批處理。  
- **垃圾回收：** 及時釋放未使用的 `Index` 物件以釋放資源。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **資料夾路徑不正確** | 確認絕對路徑，並確保應用程式具有讀取權限。 |
| **記憶體不足** | 增加 JVM 堆積大小（`-Xmx`）或分批索引檔案。 |
| **取消未觸發** | 在呼叫 `merge` 前確保已設定 `cancelAfter`。 |
| **不支援的檔案格式** | 如有需要，從 GroupDocs 安裝額外的格式插件。 |

## 常見問答

**Q:** *為什麼我要建立多個索引而不是單一索引？*  
A: 分離的索引讓您能隔離資料領域、套用不同的安全政策，並在需要時才合併，從而提升效能與組織性。

**Q:** *我可以像取消合併一樣取消索引作業嗎？*  
A: 可以——使用 `Cancellation` 物件搭配 `add` 方法來停止長時間執行的索引任務。

**Q:** *如何確保在非常大的文件集合下仍保持最佳效能？*  
A: 執行增量索引、監控 JVM 記憶體，並考慮使用 SSD 儲存索引目錄。

**Q:** *如果收到「存取被拒」錯誤，我該怎麼辦？*  
A: 檢查執行 Java 程序之使用者的資料夾權限，並確保授權檔案可讀取。

**Q:** *GroupDocs.Search 能與其他 GroupDocs 函式庫相容嗎？*  
A: 當然可以——您可以將其與 GroupDocs.Viewer、GroupDocs.Conversion 等整合，打造完整的文件解決方案。

## 結論
透過本指南，您現在已了解如何**添加文件至索引**、設定合併行為，並在需要時安全地**取消合併操作**——全部在強大的**document management java**工作流程中。可嘗試更大的資料集、探索自訂分詞器，或將 GroupDocs.Search 與其他 GroupDocs 產品結合，打造真正的企業級解決方案。

**資源**
- **文件說明：** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API 參考：** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **下載：** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub 倉庫：** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **免費支援論壇：** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **臨時授權申請：** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-01-03  
**測試版本：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  
