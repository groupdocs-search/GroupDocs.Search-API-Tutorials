---
date: '2025-12-20'
description: 學習如何在 Java 中使用 GroupDocs.Search 建立詞形提供者。產生單數與複數形式，以供搜尋、文字分析等用途。
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: 使用 GroupDocs.Search API 在 Java 中建立 Word 表單提供者
type: docs
url: /zh-hant/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# 在 Java 中使用 GroupDocs.Search API 建立詞形提供程式

將單數詞轉換為複數詞—或相反—在構建具備語言感知的應用程式時是一個常見的挑戰。在本指南中，您將使用 GroupDocs.Search Java API **建立詞形提供程式**，讓您的搜尋引擎或文字分析工具能自動理解並匹配不同的詞彙變形。

無論您是開發搜尋引擎、內容管理系統，或任何處理自然語言的 Java 應用程式，掌握詞形產生都能讓結果更精確、使用者更滿意。讓我們先了解開始前的前置條件。

## 快速答案
- **詞形提供程式的功能是什麼？** 它會產生給定詞彙的替代形式（單數、複數等），使搜尋能匹配所有變體。  
- **需要哪個函式庫？** GroupDocs.Search for Java（版本 25.4 或更新）。  
- **是否需要授權？** 免費試用可用於評估；正式上線需購買永久授權。  
- **支援的 Java 版本為何？** JDK 8 或以上。  
- **需要多少行程式碼？** 簡易提供程式大約 30 行。

## 「建立詞形提供程式」功能是什麼？
**建立詞形提供程式** 元件是一個自訂類別，實作 `IWordFormsProvider` 介面。它接收一個詞彙，並根據您定義的規則回傳可能的形態陣列——單數、複數或其他語言變化。這讓搜尋索引能將「cat」與「cats」視為等價，提升召回率而不犧牲精確度。

## 為何使用 GroupDocs.Search 產生詞形？
- **內建可擴充性：** 您可以直接將自訂提供程式插入索引流程。  
- **效能最佳化：** 此函式庫能有效處理大型索引，且可快取結果以提升速度。  
- **跨語言支援：** 雖然本教學以 Java 為例，相同概念亦適用於 .NET 與其他平台。

## 前置條件

在實作 **建立詞形提供程式** 之前，請確保您已具備：

- **Maven** 已安裝，且機器上配置 JDK 8 或更新版本。  
- 具備 Java 開發與 Maven `pom.xml` 設定的基本認識。  
- 取得 GroupDocs.Search Java 函式庫（版本 25.4 或以上）。

## 為 Java 設定 GroupDocs.Search

### Maven 設定

將儲存庫與相依性加入 `pom.xml` 檔案，請完全照下列範例操作：

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

亦可從官方發行頁面下載最新 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權步驟

若要無限制使用 GroupDocs.Search：

1. **免費試用：** 註冊試用以探索核心功能。  
2. **臨時授權：** 申請臨時金鑰以延長測試。  
3. **購買：** 取得商業授權以在正式環境無限制使用。

### 基本初始化與設定

以下程式碼片段示範如何建立索引——這是加入文件與詞形邏輯的起點：

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

以下步驟說明如何 **建立詞形提供程式**，以處理簡單的單數↔複數轉換。

### 實作 SimpleWordFormsProvider

#### 概觀

我們的自訂提供程式將：

- 移除結尾的 “es” 或 “s” 以推測單數形態。  
- 將結尾的 “y” 變為 “is” 以產生複數形態（例如 “city” → “citis”）。  
- 附加 “s” 與 “es” 以產生基本的複數候選。

#### 步驟 1 – 建立類別骨架

先定義一個實作 `IWordFormsProvider` 的類別。請保持 import 陳述式不變：

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### 步驟 2 – 實作 `getWordForms`

加入建立可能形態清單的方法。此區塊包含核心邏輯，日後可擴充以支援更複雜規則。

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

- **單數化：** 偵測常見的複數後綴 (`es`, `s`) 並移除，以近似原始詞根。  
- **複數化：** 處理以 `y` 結尾的名詞，將其換成 `is`，此簡單規則適用於許多英文字。  
- **後綴附加：** 加上 `s` 與 `es`，以涵蓋先前檢查未捕捉的規則複數形態。

#### 疑難排解技巧

- **大小寫敏感度：** 此方法使用 `toLowerCase()` 進行比較，確保 “Cats” 與 “cats” 行為一致。  
- **邊緣情況：** 長度小於後綴的詞彙會被忽略，以避免回傳空字串。  
- **效能：** 對於大型詞彙表，建議將結果快取於 `ConcurrentHashMap` 中。

## 實務應用

實作 **建立詞形提供程式** 可提升多種真實情境的效能：

1. **搜尋引擎：** 使用者輸入 “mouse” 時，也應能找到包含 “mice” 的文件。提供程式可產生此類不規則形態。  
2. **文字分析工具：** 當所有詞形變體皆被辨識時，情感或實體抽取的可靠度提升。  
3. **內容管理系統：** 自動標籤產生可納入複數同義詞，提升 SEO 與內部連結。

## 效能考量

將提供程式嵌入正式系統時，請留意以下建議：

- **快取常用詞形：** 將結果存於記憶體，避免重複計算相同詞彙。  
- **監控 JVM 堆積：** 大型索引可能增加記憶體壓力，請適當調整 `-Xmx`。  
- **使用高效集合：** 小規模集合可用 `ArrayList`，但若有數千種詞形，建議使用 `HashSet` 以快速去除重複。

**最佳實踐**

- 保持函式庫為最新版本，以獲得效能修補。  
- 以實際查詢負載對提供程式進行效能分析，及早發現瓶頸。

## 結論

您現在已學會如何使用 GroupDocs.Search for Java **建立詞形提供程式**。這個輕量級元件能顯著提升搜尋結果的相關性與語言分析的準確度，適用於各種應用場景。

**下一步：**  
- 嘗試更複雜的語言規則（不規則複數、詞幹提取）。  
- 將提供程式整合至索引流程，測量召回率提升。  
- 探索 GroupDocs.Search 其他功能，如同義詞字典與自訂分析器。

**行動呼籲：** 立即將 `SimpleWordFormsProvider` 加入您的專案，體驗它為搜尋體驗帶來的提升！

## 常見問題

**1. What is GroupDocs.Search for Java?**  
它是一套功能強大的函式庫，提供全文搜尋、索引與語言特性——包括可插入自訂詞形提供程式的能力。

**2. How does the SimpleWordFormsProvider work?**  
它透過簡單的後綴規則（移除 “s/es”、將 “y” 轉為 “is”、以及附加 “s/es”）產生替代形態。

**3. Can I customize the word form generation rules?**  
當然可以。修改 `getWordForms` 方法，即可加入不規則形態、特定語系規則，或與外部字典整合。

**4. What are some common applications for this feature?**  
搜尋引擎、文字分析管線與 CMS 平台皆可藉由辨識單複數變體獲益。

**5. Do I need a commercial license for production use?**  
是的——雖然試用版可讓您探索 API，正式使用仍需購買授權以解除使用限制並取得支援。

---

**最後更新：** 2025-12-20  
**測試環境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs