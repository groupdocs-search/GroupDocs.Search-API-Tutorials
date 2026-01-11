---
date: '2026-01-11'
description: 學習如何使用 GroupDocs.Search for Java 建立自訂搜尋索引，設定常規與混合字元，以實現進階 OCR 與影像搜尋。
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: 建立自訂搜尋索引與字元辨識 – GroupDocs.Search Java
type: docs
url: /zh-hant/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# 使用 GroupDocs.Search for Java 建立具字符辨識的自訂搜尋索引

在現代文件密集的應用程式中，**建立自訂搜尋索引** 能夠理解文字中的細微差異——例如連字符、底線或語言特有符號——對於快速且精確的檢索至關重要。本教學將帶您設定 **GroupDocs.Search for Java** 的字符辨識，涵蓋一般字符（字母、數字、底線）與混合字符（例如連字符）。完成後，您將能夠打造符合 OCR 或影像搜尋情境的精確索引。

## 快速解答
- **「建立自訂搜尋索引」是什麼意思？** 意指將索引設定為將特定符號視為字母或混合字符，而非直接忽略。  
- **使用哪個函式庫？** GroupDocs.Search for Java（撰寫時為 v25.4）。  
- **需要授權嗎？** 開發階段可使用免費試用版；正式上線須購買授權。  
- **可以同時索引 PDF 與影像嗎？** 可以——只要正確設定，GroupDocs.Search 會對影像與 PDF 執行 OCR。  
- **必須使用 Maven 嗎？** Maven 為建議的相依管理方式，亦可使用 Gradle 或手動 JAR。

## 什麼是自訂搜尋索引？
自訂搜尋索引讓您定義搜尋引擎如何解讀字符。預設情況下，許多符號會被忽略，這可能導致找不到如案件編號 (`ABC-123`) 或程式碼片段 (`my_variable`) 等關鍵字。調整字母字典即可完全掌控引擎將哪些字符視為可搜尋的文字。

## 為什麼要設定一般字符與混合字符？
- **一般字符**（字母、數字、底線）會被視為獨立的詞彙，有助於精確匹配搜尋。  
- **混合字符**（連字符、斜線）會連接詞彙；將其設定為混合字符可避免不必要的詞彙切割，對法律條文、產品代碼或原始碼索引尤為重要。

## 前置條件
- 已安裝 **JDK 8** 或更新版本。  
- 已安裝 **Maven** 以管理相依。  
- 取得 **GroupDocs.Search for Java** 函式庫（可透過 Maven 或官方網站下載）。

### 必要的函式庫與相依
將以下儲存庫與相依項目加入 `pom.xml`（如範例所示）。此 XML 區塊必須保持原樣。

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

您也可以從 [GroupDocs.Search for Java 版本發布頁面](https://releases.groupdocs.com/search/java/) 下載最新的 JAR。

### 授權取得
- **免費試用** – 適合早期實驗。  
- **臨時授權** – 方便較長的開發週期。  
- **正式授權** – 商業部署時必須使用。

從官方入口取得授權：[GroupDocs](https://purchase.groupdocs.com/temporary-license/)。

### 基本初始化
以下程式碼片段示範建立空索引的最小需求。請保持原樣，我們稍後會在此基礎上擴充。

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
在 *前置條件* 章節中提供的 Maven 設定即為全部需求。加入後執行 `mvn clean install` 下載相應的二進位檔。

### 環境設定需求
- 確認 **索引資料夾** 與 **文件資料夾** 已存在於磁碟上。  
- 使用絕對路徑或在 IDE 中正確設定相對路徑的解析。

## 實作指南

以下說明兩項不同功能：**一般字符** 與 **混合字符**。每項功能的流程相同——設定路徑、建立索引、設定字符字典，最後將文件加入索引。

### 功能 1 – 一般字符

#### 概觀
一般字符會被視為獨立的詞彙。當您希望數字、字母與底線能夠精確搜尋時，此設定最為理想。

#### 步驟實作

**1️⃣ 設定路徑**  
定義索引要儲存的位置以及來源文件所在的資料夾。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ 建立並設定索引**  
實例化索引並清除先前的字母設定。

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ 定義一般字符**  
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

**4️⃣ 索引文件**  
將來源資料夾中的所有檔案加入新建立的索引。

```java
index.add(documentFolder);
```

### 功能 2 – 混合字符

#### 概觀
混合字符（例如連字符）常用於連接兩個詞彙。將其標記為 *混合* 後，索引時會保留相鄰詞彙的完整性。

#### 步驟實作

**1️⃣ 設定路徑**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ 建立並設定索引**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ 定義混合字符**  
此處告訴字典將連字符視為混合字符。

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ 索引文件**  

```java
index.add(documentFolder);
```

## 實務應用

### 用例 1 – 法律文件管理
法律文件常包含如 `2023-AB-456` 的案件編號。透過設定底線與連字符，可在搜尋時取得完整匹配，而不會被切割。

### 用例 2 – 原始碼倉庫
開發者需要搜尋包含底線 (`my_variable`) 與連字符 (`my-function`) 的程式碼片段。自訂字符辨識確保搜尋引擎正確處理這些符號。

### 用例 3 – 多語言資料集
處理使用額外字母表的語言時，可將一般字符集擴充至相應的 Unicode 範圍，確保跨語言搜尋的準確性。

## 效能考量

- **資源管理** – 留意堆積記憶體使用量；大型索引建議使用增量提交。  
- **垃圾回收** – 完成後釋放 `Index` 物件，以讓 JVM 回收記憶體。  
- **索引最佳化** – 定期呼叫 `index.optimize()`（若有提供）以壓縮索引並提升查詢速度。

## 結論

您現在已掌握如何使用 GroupDocs.Search for Java **建立自訂搜尋索引**，並分別設定一般字符與混合字符。這種細緻的控制讓您能夠打造具 OCR 感知、高效能的搜尋解決方案，適用於法律、開發或多語言環境。

**後續步驟**  
- 嘗試為非拉丁字母加入額外的 Unicode 範圍。  
- 結合字符設定與 GroupDocs.Search 的其他功能，如詞幹分析或同義詞。  
- 將索引整合至 REST API，為前端應用提供搜尋服務。

## 常見問題

**Q:** *`CharacterType.Letter` 的用途是什麼？*  
**A:** 它告訴索引將提供的字符視為一般字母，於索引時會被獨立切分為詞彙。

**Q:** *我可以在同一個索引中同時使用一般字符與混合字符嗎？*  
**A:** 可以——只要分別呼叫 `setRange` 設定兩種型別，字典會同時處理這兩種配置。

**Q:** *變更字母表後需要重新建立索引嗎？*  
**A:** 必須。字符字典的變更會影響切詞方式，必須重新索引文件才能套用新規則。

**Q:** *自訂字符的數量有限制嗎？*  
**A:** 函式庫支援完整的 Unicode 範圍；若加入過多字符可能會影響效能，建議僅加入實際需要的字符。

**Q:** *這會如何影響 OCR 的準確度？*  
**A:** 透過讓索引的字符集與 OCR 輸出保持一致，可減少偽陰性，提升整體搜尋相關性。

---

**最後更新：** 2026-01-11  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

---