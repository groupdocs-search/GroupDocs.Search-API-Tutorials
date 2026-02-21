---
date: '2026-02-21'
description: 學習如何在 Java 中使用 GroupDocs.Search API 產生單複數形態。建立自訂詞形提供程式，以提升搜尋與文字分析的精準度。
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: 在 Java 中使用 GroupDocs.Search 產生單複數形式
type: docs
url: /zh-hant/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

 answer.# 在 Java 中使用 GroupDocs.Search 產生單數與複數形式

如果您需要在 Java 中**產生單數與複數形式**，自訂字形提供者是讓您的搜尋或文字分析引擎理解每個詞彙變化的關鍵。在本教學中，我們將帶您一步步使用 GroupDocs.Search Java API 建立此類提供者，讓您的應用程式能自動匹配「cat」、「cats」、「city」以及「citis」而無需額外工作。

## 快速解答
- **字形提供者的功能是什麼？** 它會為給定的詞產生替代形式（單數、複數等），使搜尋能匹配所有變體。  
- **需要哪個函式庫？** GroupDocs.Search for Java（版本 25.4 或更新）。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。  
- **支援哪個 Java 版本？** JDK 8 或更高版本。  
- **需要多少行程式碼？** 簡易提供者實作大約 30 行。

## 「Create Word Forms Provider」功能是什麼？
**create word forms provider** 元件是一個自訂類別，實作 `IWordFormsProvider` 介面。它接收一個詞彙並根據您定義的規則回傳可能的形式陣列——單數、複數或其他語言變化。這讓搜尋索引能將「cat」與「cats」視為等價，提高召回率而不犧牲精確度。

## 為何使用 GroupDocs.Search 產生字形變化？
- **內建可擴充性：** 可直接將自訂提供者插入索引流程。  
- **效能最佳化：** 能有效處理大型索引，且可快取結果以提升速度。  
- **跨語言支援：** 相關概念同樣適用於 .NET 及其他平台。

## 前置條件
在實作 **create word forms provider** 之前，請確保您已具備以下條件：

- **Maven** 已安裝，且機器上已設定 JDK 8 或更新版本。  
- 具備 Java 開發與 Maven `pom.xml` 設定的基本知識。  
- 可取得 GroupDocs.Search Java 函式庫（版本 25.4 或以上）。

## 設定 GroupDocs.Search for Java

### Maven 設定

將以下儲存庫與相依性加入您的 `pom.xml` 檔案，完全照以下示範。

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

或者，從官方發佈頁面下載最新的 JAR 檔案：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 取得授權步驟
1. **免費試用：** 註冊試用以探索核心功能。  
2. **臨時授權：** 申請臨時金鑰以延長測試時間。  
3. **購買：** 取得商業授權以在正式環境無限制使用。

### 基本初始化與設定

以下程式碼示範如何建立索引——這是加入文件與字形邏輯的起點：

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## 實作指南

以下說明如何一步步建立 **create word forms provider**，以處理簡單的單數到複數及複數到單數轉換。

### 實作 SimpleWordFormsProvider

#### 概觀
我們的自訂提供者將會：

- 移除結尾的 “es” 或 “s” 以推測單數形式。  
- 將結尾的 “y” 變為 “is” 以產生複數形式（例如 “city” → “citis”）。  
- 附加 “s” 與 “es” 以產生基本的複數候選。

#### 步驟 1 – 建立類別骨架
首先定義一個實作 `IWordFormsProvider` 的類別。請保持 import 陳述式不變：

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### 步驟 2 – 實作 `getWordForms`
加入建構可能形式清單的方法。此區塊包含核心邏輯，您之後可擴充以支援更複雜的規則。

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### 邏輯說明
- **單數化：** 偵測常見的複數字尾（`es`、`s`），並移除以近似原始詞根。  
- **複數化：** 處理以 `y` 結尾的名詞，將其換成 `is`，這是一個適用於許多英文單詞的簡易規則。  
- **字尾附加：** 加上 `s` 與 `es`，以涵蓋先前檢查未捕捉到的規則複數形式。

#### 疑難排解提示
- **大小寫敏感度：** 此方法使用 `toLowerCase()` 進行比較，確保 “Cats” 與 “cats” 行為相同。  
- **邊緣情況：** 長度小於字尾長度的詞會被忽略，以避免回傳空字串。  
- **效能：** 對於大型詞彙表，建議將結果快取於 `ConcurrentHashMap` 中。

## 實務應用

實作 **create word forms provider** 可提升多種實務情境：

1. **搜尋引擎：** 使用者輸入 “mouse” 時，也應能找到包含 “mice” 的文件。提供者可產生此類不規則變形。  
2. **文字分析工具：** 當所有詞彙變形皆被辨識時，情感或實體抽取的可靠性會提升。  
3. **內容管理系統：** 自動標籤產生可納入複數同義詞，提升 SEO 與內部連結。

## 效能考量

將提供者嵌入正式系統時，請留意以下建議：

- **快取常用形式：** 將結果儲存於記憶體，以避免重複計算相同詞彙。  
- **監控 JVM 堆積：** 大型索引可能增加記憶體壓力，請相應調整 `-Xmx`。  
- **使用高效集合：** `ArrayList` 適用於小集合，若有上千種形式，建議使用 `HashSet` 以快速去除重複。

**最佳實踐**
- 保持函式庫為最新版本，以獲得效能修補。  
- 以實際查詢負載對提供者進行效能分析，及早發現瓶頸。

## 結論

現在您已學會如何使用 GroupDocs.Search 的自訂 `SimpleWordFormsProvider` 在 Java 中**產生單數與複數形式**。此輕量元件能顯著提升搜尋結果的相關性與多種應用中的語言分析精確度。

**下一步：**  
- 嘗試更複雜的語言規則（不規則複數、詞幹提取）。  
- 將提供者整合至索引流程，並衡量召回率提升。  
- 探索其他 GroupDocs.Search 功能，如同義詞字典與自訂分析器。

**行動呼籲：** 立即將 `SimpleWordFormsProvider` 加入您的專案，體驗它如何提升搜尋體驗！

## 常見問題集

**1. 什麼是 GroupDocs.Search for Java？**  
它是一套強大的函式庫，提供全文搜尋、索引與語言功能——包括可插入自訂字形提供者的能力。

**2. SimpleWordFormsProvider 如何運作？**  
它透過簡單的字尾規則產生替代形式（移除 “s/es”、將 “y” 轉為 “is”、以及附加 “s/es”）。

**3. 我可以自訂字形產生規則嗎？**  
當然可以。修改 `getWordForms` 方法，即可加入不規則形式、特定語系規則，或與外部字典整合。

**4. 此功能的常見應用有哪些？**  
搜尋引擎、文字分析管線與 CMS 平台皆可受益於辨識單數/複數變形。

**5. 正式環境是否需要商業授權？**  
是的——雖然試用版可讓您探索 API，正式使用仍需購買授權以解除使用限制並取得支援。

---
**最後更新：** 2026-02-21  
**測試環境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs  
---