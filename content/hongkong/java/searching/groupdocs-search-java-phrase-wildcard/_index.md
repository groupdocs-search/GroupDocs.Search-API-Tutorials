---
date: '2026-01-26'
description: 了解如何在 GroupDocs.Search for Java 中使用通配符模式搜尋片語。本指南涵蓋建立搜尋索引、將文件加入索引，以及執行通配符搜尋（Java）。
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: 如何在 GroupDocs.Search Java 中使用通配符搜尋短語
type: docs
url: /zh-hant/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# 如何在 GroupDocs.Search for Java 中使用通配符搜尋片語

在當今快速變化的文件管理領域，**如何搜尋片語**的效率直接影響應用程式的可用性。無論您是在建置內容管理系統、電子商務目錄，或是法律文件庫，能夠定位精確片語或其彈性變體都是關鍵。本教學將逐步說明如何設定 **GroupDocs.Search for Java**、建立搜尋索引、將文件加入索引，並掌握簡單片語搜尋與強大的通配符搜尋 Java 技術。

## 快速回答
- **片語搜尋的主要好處是什麼？** 精確匹配詞序與相近距離。  
- **可以在片語內使用通配符嗎？** 可以，您可以將通配符與精確詞彙結合，以達到彈性匹配。  
- **開發時需要授權嗎？** 免費試用可用於測試；正式上線需購買完整授權。  
- **應該使用哪個 Maven 版本？** 使用最新的 GroupDocs.Search for Java 版本（例如撰寫時的 25.4）。  
- **此方法適用於大型文件集嗎？** 絕對適用，只要保持索引最佳化並使用針對性的通配符模式即可。

## 什麼是「搜尋片語」？
搜尋片語指的是在文件中尋找特定的詞序。加入通配符後，搜尋引擎可以跳過或替換詞彙，讓您在不犧牲相關性的前提下匹配各種變體。

## 為什麼使用 GroupDocs.Search 進行片語與通配符查詢？
- **高效能**：在大型集合上依賴優化的倒排索引。  
- **豐富的查詢語言**：支援精確片語、簡單通配符與進階模式。  
- **易於整合**：透過 Maven 或直接下載即可在任何基於 Java 的應用程式中使用。

## 前置條件
- 已安裝 Java 8 或更新版本。  
- 已安裝 Maven 3 或以上（若使用 Maven 管理相依性）。  
- 具備基本的 Java 語法與專案結構知識。

## 設定 GroupDocs.Search for Java

### 使用 Maven
將以下儲存庫與相依性加入 `pom.xml` 檔案：

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
或是從 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下載最新的 JAR。

### 取得授權
- **免費試用**：適合快速實驗。  
- **臨時授權**：可於 GroupDocs 入口網站申請，以延長測試時間。  
- **正式購買**：建議於正式環境部署時使用。

### 基本初始化與設定
建立索引資料夾並進行初始化：

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

將欲搜尋的文件加入索引：

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## 如何在 GroupDocs.Search 中使用通配符搜尋片語
以下分為三個遞進情境：精確片語搜尋、簡單通配符使用，以及進階通配符模式。

### 簡單片語搜尋

#### 概述
當您需要精確匹配詞序時使用此方式。

##### 步驟 1：建立索引
```java
Index index = new Index(indexFolder);
```

##### 步驟 2：將文件加入索引
```java
index.add(documentsFolder);
```

##### 步驟 3：以文字形式搜尋特定片語
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### 步驟 4：基於物件的查詢（搜尋精確片語）
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### 使用通配符的片語搜尋

#### 概述
通配符佔位符允許在精確詞彙之間跳過可變數量的詞彙。

##### 步驟 1：建立索引
*(Same as the Simple Phrase Search steps.)*

##### 步驟 2：將文件加入索引
*(Same as above.)*

##### 步驟 3：以文字形式使用通配符搜尋
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### 步驟 4：基於物件的通配符查詢（Wildcard Search Java）
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### 進階通配符搜尋

#### 概述
結合數值範圍、可選字元與自訂模式，以實現更精細的匹配。

##### 步驟 1：建立索引
*(Repeated for clarity.)*

##### 步驟 2：將文件加入索引
*(Repeated.)*

##### 步驟 3：以文字形式使用複雜的通配符模式搜尋
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### 步驟 4：基於物件的進階通配符查詢
```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## 實務應用
- **內容管理系統**：協助編輯者快速定位精確條款或彈性摘錄。  
- **電子商務目錄**：即使使用者遺漏詞彙或使用同義詞，也能找到商品。  
- **法律與合規**：迅速找出可能出現細微變化的合約語句。

## 效能考量
- **建立搜尋索引** 只需對每組文件執行一次，之後重複使用。  
- **將文件加入索引** 時可增量更新，避免每次都重建整個索引。  
- 使用 **精確的通配符模式** 可減少不必要的掃描；過於寬鬆的模式會增加 CPU 負載。  
- 定期呼叫 `index.optimize()`（若支援）以降低記憶體使用。

## 常見問題與解決方案
| 問題 | 解決方案 |
|------|----------|
| 通配符查詢未返回結果 | 檢查通配符語法（`*min~~max`）並確認指定距離內確實存在相關詞彙。 |
| 文件更新後索引變舊 | 重新執行 `index.add(updatedFolder)` 或使用增量更新 API。 |
| 大型資料集記憶體消耗過高 | 增加 JVM 堆積大小，並考慮將索引切分為多個分片。 |

## 常見問答

**Q: 通配符與片語搜尋有何不同？**  
A: 片語搜尋要求詞序完全相同，而通配符允許在該序列中替換或跳過詞彙。

**Q: 可以在搜尋中對數值資料使用通配符嗎？**  
A: 可以，通配符的範圍參數同樣適用於數字。

**Q: 如何處理極大型的文件集合？**  
A: 保持索引最佳化，使用增量更新，並盡可能設計具體的通配符模式。

**Q: GroupDocs.Search 適合即時搜尋情境嗎？**  
A: 完全適合——索引建好後，查詢在毫秒級完成，適用於互動式應用。

**Q: 我可以將此函式庫整合到現有的 Java 專案嗎？**  
A: 可以。加入 Maven 相依性或 JAR，依照示範初始化索引，即可開始使用。

---

**最後更新：** 2026-01-26  
**測試環境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs