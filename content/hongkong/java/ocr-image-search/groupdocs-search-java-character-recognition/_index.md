---
date: '2026-03-17'
description: 學習如何使用 GroupDocs.Search for Java 建立索引、設定一般與混合字元，並優化對法律案件編號與 OCR 圖片的搜尋。
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: 如何在 Java 中使用字元辨識建立索引
type: docs
url: /zh-hant/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# 如何使用 GroupDocs.Search for Java 建立具字符辨識的索引

在現代以文件為主的應用程式中，**how to create index** 必須能夠顧及文字的細節——例如連字符、底線或特定語言的符號，才能確保快速且精確的檢索。本教學將逐步說明如何在 **GroupDocs.Search for Java** 中設定字符辨識，涵蓋一般字符（字母、數字、底線）與混合字符（例如連字符）。完成後，您將能夠自訂索引，以符合 OCR 或影像搜尋情境的精確需求，無論是索引法律案件編號、原始碼庫或多語言 PDF。

## 快速回答
- **「create custom search index」是什麼意思？** 這表示將索引設定為將特定符號視為字母或混合字符，而不是忽略它們。  
- **使用哪個函式庫？** GroupDocs.Search for Java (v25.4 at the time of writing)。  
- **我需要授權嗎？** 免費試用可用於開發；商業環境需付費授權。  
- **我可以同時索引 PDF 與影像嗎？** 可以——GroupDocs.Search 在正確設定下支援影像與 PDF 的 OCR。  
- **需要 Maven 嗎？** Maven 是建議的相依性管理方式，但也可使用 Gradle 或手動 JAR。

## 什麼是自訂搜尋索引？
自訂搜尋索引允許您定義搜尋引擎如何解讀字符。預設情況下，許多符號會被忽略，可能導致如案件編號 (`2023-AB-456`) 或程式碼片段 (`my_variable`) 等匹配失敗。調整字母表字典即可完整掌控引擎將哪些字符視為可搜尋的文字。

## 為什麼要為法律案件編號設定一般與混合字符？
- **Regular characters**（字母、數字、底線）會被獨立切分，讓識別碼的精確匹配成為可能。  
- **Blended characters**（連字符、斜線）會將相關的詞彙保持在一起，避免案件編號、產品代碼或檔案路徑被不必要地切分。  
- 此設定透過減少詞彙碎片化並提升 OCR 產生內容的相關性，**optimizes search index** 效能。

## 前置條件
- **JDK 8** 或更新版本已安裝。  
- **Maven** 用於相依性管理。  
- 取得 **GroupDocs.Search for Java** 函式庫（可透過 Maven 或官方網站下載）。

### 必要的函式庫與相依性
將儲存庫與相依性條目加入您的 `pom.xml`（如下所示）。XML 區塊必須保持不變。

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

您也可以從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR。

### 取得授權
- **Free Trial** – 適合早期試驗。  
- **Temporary License** – 適用於較長的開發週期。  
- **Production License** – 商業部署必須取得。

從官方入口取得授權：[GroupDocs](https://purchase.groupdocs.com/temporary-license/)。

### 基本初始化
以下程式碼片段展示建立空白索引所需的最小程式碼。請保持原樣，我們稍後會在此基礎上擴充。

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## 設定 GroupDocs.Search for Java

### 透過 Maven 安裝
在 *Prerequisites* 章節中的 Maven 設定即為全部需求。加入後，執行 `mvn clean install` 以下載二進位檔。

### 環境設定需求
- 確認 **index folder** 與 **document folder** 已在磁碟上存在。  
- 使用絕對路徑或在 IDE 中正確設定相對路徑。

## 實作指南

以下說明兩個不同的功能：**regular characters** 與 **blended characters**。每個功能遵循相同的步驟——定義路徑、建立索引、設定字符字典，最後索引文件。

### 功能 1 – Regular Characters

#### 概述
Regular characters 會被視為獨立的詞彙。當您希望數字、字母與底線能夠精確搜尋時，此方式最為理想。

#### 步驟實作

**1️⃣ Set Up Paths**  
定義索引儲存位置以及來源文件所在的路徑。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
建立索引實例並清除任何先前的字母表設定。

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
建立包含數字、拉丁字母與底線的字符陣列。

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index Documents**  
將來源資料夾中的所有檔案加入新設定的索引。

```java
index.add(documentFolder);
```

### 功能 2 – Blended Characters

#### 概述
Blended characters（如連字符）常用於連接兩個詞彙。將其標記為 *blended* 可指示引擎在索引時將相鄰的詞彙保持在一起。

#### 步驟實作

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
在此我們告訴字典將連字符視為 blended character。

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## 實務應用

### 使用案例 1 – 法律文件管理
法律文件常包含如 `2023-AB-456` 的案件編號。透過設定底線與連字符，搜尋可返回完整匹配而不會切分識別碼，協助您有效 **search legal case numbers**。

### 使用案例 2 – 原始碼庫
開發者需要搜尋包含底線（`my_variable`）與連字符（`my-function`）的程式碼片段。自訂字符辨識可確保搜尋引擎尊重這些符號。

### 使用案例 3 – 多語言資料集
處理使用額外字母表的語言時，您可以 **extend Unicode character set** 以納入這些範圍，確保跨語言搜尋結果的準確性。

### 使用案例 4 – 索引 PDF 影像
若要索引掃描的 PDF 或影像檔案，OCR 輸出常包含混合字符。正確設定 regular 與 blended characters 可 **optimizes search index** 於影像內容的效能。

## 效能考量
- **Resource Management** – 監控堆積記憶體使用情況；大型索引可受益於增量提交。  
- **Garbage Collection** – 完成後釋放 `Index` 物件，讓 JVM 回收記憶體。  
- **Index Optimization** – 定期呼叫 `index.optimize()`（若支援）以壓縮索引並提升查詢速度。

## 結論
您現在已了解如何使用 GroupDocs.Search for Java **how to create index**，將 regular 與 blended characters 區分開來。此精細的控制讓您能構建具 OCR 感知、高效能的搜尋解決方案，適用於法律、開發或多語言環境。

### 往後步驟
- 嘗試為非拉丁字母加入更多 Unicode 範圍。  
- 將字符設定與其他 GroupDocs.Search 功能（如詞幹分析或同義詞）結合。  
- 將索引整合至 REST API，向前端應用程式提供搜尋功能。

## 常見問題

**Q:** *`CharacterType.Letter` 的用途是什麼？*  
**A:** 它告訴索引將提供的字符視為 regular letters，於索引時會被獨立切分。

**Q:** *我可以在同一個索引中混合 regular 與 blended characters 嗎？*  
**A:** 可以——只需對每種型別呼叫 `setRange`，字典會同時處理兩種設定。

**Q:** *變更字母表後需要重新建立索引嗎？*  
**A:** 必須。字符字典的變更會影響切分方式，必須重新索引文件以套用新規則。

**Q:** *我可以定義的自訂字符數量有上限嗎？*  
**A:** 函式庫支援完整 Unicode 範圍；若加入過多字符可能影響效能，建議僅定義實際需要的字符。

**Q:** *這對 OCR 的準確度有何影響？*  
**A:** 透過使索引的字符集與 OCR 引擎的輸出保持一致，可減少偽陰性並提升整體搜尋相關性。

---

**最後更新:** 2026-03-17  
**測試環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs