---
date: '2026-01-11'
description: 學習如何使用 GroupDocs for Java OCR 索引結合 Aspose.OCR，為 PDF、圖像及掃描檔案提供強大的文件搜尋功能。
keywords:
- Java OCR indexing
- document searchability
- OCR with GroupDocs
title: 如何使用 GroupDocs for Java 進行 OCR 索引與 Aspose
type: docs
url: /zh-hant/java/ocr-image-search/java-ocr-indexing-aspose-groupdocs-search/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 進行 OCR 索引（搭配 Aspose）

在本指南中，您將了解 **如何使用 GroupDocs** 為您的 Java 應用程式加入 OCR 驅動的搜尋功能。結合 GroupDocs.Search 與 Aspose.OCR，您可以將基於影像的內容轉換為可搜尋的文字，讓文件管理系統的效用大幅提升。我們將逐步說明設定、索引、搜尋以及自訂 OCR 整合的完整流程，並提供清晰的範例程式碼。

## 快速答覆
- **哪個函式庫提供 OCR 索引功能？** GroupDocs.Search 搭配 Aspose.OCR。  
- **需要哪個 Java 版本？** JDK 8 或以上。  
- **需要授權嗎？** 提供免費試用版；正式上線需購買授權。  
- **可以同時索引獨立與嵌入式影像嗎？** 可以，於 `IndexingOptions` 中啟用兩者。  
- **支援多執行緒嗎？** 支援，您可以為大量資料集平行化索引程序。

## 什麼是使用 GroupDocs 的 OCR 索引？
OCR 索引會從影像（包括掃描的 PDF）中擷取文字，並將其儲存於可搜尋的索引中。GroupDocs.Search 負責索引與查詢執行，而 Aspose.OCR 則執行實際的字元辨識。

## 為什麼要使用 GroupDocs 進行 Java OCR 索引？
- **高精度**：得益於 Aspose 先進的 OCR 引擎。  
- **無縫 Java 整合**：可透過 Maven 或直接使用 JAR 檔。  
- **彈性設定**：支援獨立或嵌入式影像。  
- **可擴充效能**：支援多執行緒與記憶體最佳化。

## 前置條件
- **GroupDocs.Search** ≥ 25.4  
- **Aspose.OCR**（最新版本）  
- JDK 8+ 以及 IDE（IntelliJ、Eclipse、NetBeans）  
- 基本的 Java 知識；Maven 有助於管理相依性，但非必須

## 設定 GroupDocs.Search for Java
### 使用 Maven
將儲存庫與相依性加入 `pom.xml`：

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
或是從 [GroupDocs releases](https://releases.groupdocs.com/search/java/) 下載最新的 GroupDocs.Search for Java 版本。

### 取得授權
- **免費試用** – 無償探索全部功能。  
- **臨時授權** – 延長測試期間。  
- **購買授權** – 正式上線時必須取得。

### 基本初始化與設定
建立索引資料夾並初始化 `Index` 物件：

```java
import com.groupdocs.search.Index;
// Specify the directory where the index will be stored.
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
// Create an instance of Index class at the specified location.
Index index = new Index(indexFolder);
```

## 如何使用 GroupDocs 進行 OCR 索引
### 建立索引
首先，設定用來存放索引檔案的資料夾：

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
Index index = new Index(indexFolder);
```

### 設定 OCR 索引選項
啟用對獨立與嵌入式影像的 OCR，並插入自訂 OCR 連接器：

```java
import com.groupdocs.search.options.IndexingOptions;
IndexingOptions options = new IndexingOptions();
options.getOcrIndexingOptions().setEnabledForSeparateImages(true);
options.getOcrIndexingOptions().setEnabledForEmbeddedImages(true);
// Set a custom OCR connector.
options.getOcrIndexingOptions().setOcrConnector(new OcrConnector());
```

### 索引文件
將來源文件（PDF、Word、影像等）加入索引：

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder, options);
```

### 在索引中搜尋
對已索引的內容執行搜尋查詢：

```java
import com.groupdocs.search.results.SearchResult;
String query = "water";
SearchResult result = index.search(query);
```

### 實作 OCR 連接器
使用 Aspose.OCR 進行影像文字辨識。依照下例實作 `IOcrConnector` 介面：

```java
import com.groupdocs.search.options.IOcrConnector;
import com.groupdocs.search.options.OcrContext;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import com.aspose.ocr.AsposeOCR;

public class OcrConnector implements IOcrConnector {
    @Override
    public final String recognize(OcrContext context) {
        if (null == context.getImageLocation()) {
            throw new RuntimeException("The image type is not supported: " + context.getImageLocation());
        }
        
        BufferedImage image = ImageIO.read(context.getImageLocation().toFile());
        AsposeOCR api = new AsposeOCR();
        String text = api.RecognizePage(image);
        return text;
    }
}
```

## 實務應用
1. **文件管理系統** – 快速取得含掃描影像的文件。  
2. **檔案庫檢索** – 在龐大檔案庫中定位歷史紀錄。  
3. **法律文件分析** – 搜尋包含掃描簽名或圖表的合約與證據。  
4. **醫療紀錄搜尋** – 索引患者表單、檢驗結果與 X 光註解。

## 效能考量
- **索引大小** – 排除不必要的中繼資料以保持索引精簡。  
- **多執行緒** – 以平行方式處理大批次資料，加速索引速度。  
- **記憶體管理** – 處理高解析度影像時，需監控 JVM 堆積使用情形。

## 常見問題與解決方案
- **授權錯誤** – 確認正確的授權檔已放置於應用程式的工作目錄。  
- **影像遺失** – 檢查影像路徑是否可存取，且格式支援 (PNG、JPEG、BMP)。  
- **記憶體不足** – 增加 JVM 堆積 (`-Xmx`) 或將文件分批處理。

## 常見問答
**Q: 如何解決 GroupDocs.Search 的授權問題？**  
A: 從 [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) 取得臨時授權，以解鎖全部功能。

**Q: 大量文件索引的最佳做法是什麼？**  
A: 使用多執行緒與批次處理，可提升效能並減少記憶體壓力。

**Q: 能否在 GroupDocs.Search 中進一步自訂 OCR 設定？**  
A: 可以，`IndexingOptions` 允許微調 OCR 行為，例如語言選擇與影像前處理。

**Q: 使用 GroupDocs.Search 時常見的除錯技巧有哪些？**  
A: 再次確認目錄路徑、確保所有相依性已正確加入，並檢查日誌輸出是否有遺失檔案的訊息。

**Q: 如何將 Aspose.OCR 整合至現有的 Java 應用程式？**  
A: 如上所示實作 `IOcrConnector` 介面，並確保正確處理影像輸入。

## 參考資源
- [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**最後更新：** 2026-01-11  
**測試環境：** GroupDocs.Search 25.4、Aspose.OCR 最新版  
**作者：** GroupDocs