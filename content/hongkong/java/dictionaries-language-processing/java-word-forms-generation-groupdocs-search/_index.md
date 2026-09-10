---
date: '2026-09-02'
description: 如何在 Java 中使用 GroupDocs.Search 生成詞形變化表：學習如何建立自訂詞形變化提供程式，以提升搜尋與文字分析的準確性。
keywords:
- how to generate forms
- GroupDocs.Search Java
- word forms provider
- singular plural Java
lastmod: '2026-09-02'
og_description: 如何在 Java 中使用 GroupDocs.Search 生成詞形變化表：學習如何建立自訂詞形變化提供程式，以提升搜尋與文字分析的準確性。
og_image_alt: Guide showing how to generate forms in Java using GroupDocs.Search
og_title: 如何在 Java 中使用 GroupDocs.Search 生成詞形變化表
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: 'How to generate forms in Java with GroupDocs.Search: learn to create
    a custom word‑forms provider for accurate search and text analysis.'
  headline: How to generate forms in Java with GroupDocs.Search
  type: TechArticle
- description: 'How to generate forms in Java with GroupDocs.Search: learn to create
    a custom word‑forms provider for accurate search and text analysis.'
  name: How to generate forms in Java with GroupDocs.Search
  steps:
  - name: '**Free trial:** Sign up for a trial to explore core features.'
    text: '**Free trial:** Sign up for a trial to explore core features.'
  - name: '**Temporary license:** Request a temporary key for extended testing.'
    text: '**Temporary license:** Request a temporary key for extended testing.'
  - name: '**Purchase:** Obtain a commercial license for unrestricted production use.'
    text: '**Purchase:** Obtain a commercial license for unrestricted production use.'
  - name: '**Search engines:** Users typing “mouse” should also find documents containing
      “mice”. A provider can generate such irregular forms.'
    text: '**Search engines:** Users typing “mouse” should also find documents containing
      “mice”. A provider can generate such irregular forms.'
  - name: '**Text analysis tools:** Sentiment or entity extraction becomes more reliable
      when all word variants are recognised.'
    text: '**Text analysis tools:** Sentiment or entity extraction becomes more reliable
      when all word variants are recognised.'
  - name: '**Content management systems:** Automatic tag generation can include plural
      synonyms, improving SEO and internal linking.'
    text: '**Content management systems:** Automatic tag generation can include plural
      synonyms, improving SEO and internal linking.'
  type: HowTo
- questions:
  - answer: It’s a powerful library that offers full‑text search, indexing, and linguistic
      features—including the ability to plug in custom word‑form providers.
    question: What is GroupDocs.Search for Java?
  - answer: It generates alternative forms by applying simple suffix‑based rules (removing
      “s/es”, converting “y” to “is”, and appending “s/es”).
    question: How does the SimpleWordFormsProvider work?
  - answer: Absolutely. Modify the `getWordForms` method to include irregular forms,
      locale‑specific rules, or integration with external dictionaries.
    question: Can I customize the word form generation rules?
  - answer: Search engines, text‑analysis pipelines, and CMS platforms benefit from
      recognising singular/plural variants.
    question: What are some common applications for this feature?
  - answer: Yes—while a trial lets you explore the API, a purchased license removes
      usage limits and grants support.
    question: Do I need a commercial license for production use?
  type: FAQPage
tags:
- word forms
- GroupDocs.Search
- Java
- search indexing
- text analysis
title: 如何在 Java 中使用 GroupDocs.Search 生成詞形變化表
type: docs
url: /zh-hant/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Search 產生詞形

在本指南中，您將學習 **如何在 Java 中產生詞形**，使用 GroupDocs.Search API。透過建立自訂的字詞形態提供者，您可以讓搜尋或文字分析引擎識別每一個詞彙的變化——無論是「cat」、「cats」、「city」或「citis」。這能大幅提升召回率，同時保持高精確度。

## 快速答覆
- **字詞形態提供者的功能是什麼？** 它會產生給定單字的替代形式（單數、複數等），讓搜尋能匹配所有變體。  
- **需要哪個函式庫？** GroupDocs.Search for Java（版本 25.4 或更新）。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。  
- **支援哪個 Java 版本？** JDK 8 或以上。  
- **需要多少行程式碼？** 簡易提供者實作大約 30 行。

## 什麼是「建立字詞形態提供者」功能？
**建立字詞形態提供者** 是實作 `IWordFormsProvider` 的自訂類別。`IWordFormsProvider` 為介面，定義提供者如何向搜尋引擎提供替代字詞形態。它接受一個單字，並根據您定義的規則回傳可能的形態陣列——單數、複數或其他語言變化。這使得搜尋索引能將「cat」與「cats」視為等價，提升召回率而不犧牲精確度。

## 為何使用 GroupDocs.Search 產生字詞形態？
GroupDocs.Search 提供內建的可擴充性，讓您可直接將自訂提供者插入索引流程。它能處理多達 **1,000 萬文件** 的索引，同時因串流架構將記憶體使用量控制在 **500 MB** 以下，且您可快取結果以達到毫秒以下的查詢速度。

## 先決條件
- **Maven** 已安裝，且機器上配置了 JDK 8 或更新版本。  
- 具備 Java 開發與 Maven `pom.xml` 設定的基本認識。  
- 取得 GroupDocs.Search Java 函式庫（版本 25.4 或以上）。

## 設定 GroupDocs.Search for Java

### Maven 設定
將以下儲存庫與相依性加入您的 `pom.xml` 檔案，完全照下列範例。

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
或者，從官方發佈頁面下載最新的 JAR 檔案：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 取得授權步驟
1. **免費試用：** 註冊試用以探索核心功能。  
2. **臨時授權：** 申請臨時金鑰以進行延長測試。  
3. **購買：** 取得商業授權，以在正式環境無限制使用。

### 基本初始化與設定
以下程式碼片段示範如何建立索引——這是加入文件與字詞形態邏輯的起點：

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

以下說明如何 **建立字詞形態提供者**，以處理簡單的單數轉複數與複數轉單數轉換。

### 實作 SimpleWordFormsProvider

#### 概觀
`SimpleWordFormsProvider` 類別實作 `IWordFormsProvider`。以下說明其目的：

`SimpleWordFormsProvider` 是 `IWordFormsProvider` 的自訂實作，為索引引擎提供單數與複數的變化。

#### 步驟 1 – 建立類別骨架
首先定義一個實作 `IWordFormsProvider` 的類別。請保留 import 陳述式不變：

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### 步驟 2 – 實作 `getWordForms`
加入建立可能形態清單的方法。此區塊包含核心邏輯，您日後可擴充以支援更複雜的規則。

`getWordForms` 接收一個詞彙，回傳包含所有產生變形的 `String[]`。

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
- **單數化：** 偵測常見的複數字尾（`es`、`s`），並將其移除以近似原始詞形。  
- **複數化：** 處理以 `y` 結尾的名詞，將其換成 `is`，此簡單規則適用於許多英文單字。  
- **字尾附加：** 加上 `s` 與 `es`，以涵蓋先前檢查未捕捉到的規則複數形態。

#### 故障排除技巧
- **大小寫敏感度：** 此方法使用 `toLowerCase()` 進行比較，確保「Cats」與「cats」的行為相同。  
- **邊緣情況：** 長度小於字尾長度的單字會被忽略，以避免回傳空字串。  
- **效能：** 面對大型詞彙表時，建議將結果快取於 `ConcurrentHashMap` 中。

## 實務應用

實作 **建立字詞形態提供者** 可提升多種實務情境：

1. **搜尋引擎：** 使用者輸入「mouse」時，也應能找到包含「mice」的文件。提供者可產生此類不規則形態。  
2. **文字分析工具：** 當所有字詞變形皆被識別時，情感或實體抽取的可靠度會提升。  
3. **內容管理系統：** 自動標籤產生可納入複數同義詞，提升 SEO 與內部連結。

## 效能考量

將提供者嵌入正式系統時，請留意以下建議：

- **快取常用形態：** 將結果存於記憶體，以免重複計算相同單字。  
- **監控 JVM 堆積：** 大型索引可能增加記憶體壓力，請適當調整 `-Xmx`。  
- **使用高效集合：** `ArrayList` 適用於小型集合，若有數千種形態，建議使用 `HashSet` 以快速去除重複。

**最佳實踐**
- 保持函式庫為最新版本，以獲得效能修補。  
- 以實際查詢負載對提供者進行效能分析，及早發現瓶頸。

## 結論

您現在已學會如何使用自訂的 `SimpleWordFormsProvider` 搭配 GroupDocs.Search **在 Java 中產生詞形**。此輕量元件能顯著提升搜尋結果的相關性與多種應用中的語言分析準確度。

**後續步驟**  
- 嘗試更進階的語言規則（不規則複數、詞幹提取）。  
- 將提供者整合至索引流程，並衡量召回率提升。  
- 探索其他 GroupDocs.Search 功能，如同義詞字典與自訂分析器。  

**行動呼籲：** 現在就將 `SimpleWordFormsProvider` 加入您的專案，體驗它如何提升搜尋體驗！

## 常見問題

**Q: 什麼是 GroupDocs.Search for Java？**  
A: 它是一套功能強大的函式庫，提供全文搜尋、索引與語言功能——包括可插入自訂字詞形態提供者的能力。

**Q: SimpleWordFormsProvider 如何運作？**  
A: 它透過簡單的字尾規則產生替代形態（移除 “s/es”、將 “y” 轉為 “is”，以及附加 “s/es”）。

**Q: 我可以自訂字詞形態產生規則嗎？**  
A: 當然可以。修改 `getWordForms` 方法，即可加入不規則形態、特定語系規則，或與外部字典整合。

**Q: 此功能的常見應用有哪些？**  
A: 搜尋引擎、文字分析管線與 CMS 平台皆可受惠於識別單數/複數變形。

**Q: 正式環境需要商業授權嗎？**  
A: 需要——雖然試用版可讓您探索 API，購買授權則解除使用限制並提供支援。

---

**最後更新：** 2026-09-02  
**測試環境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs

## 相關教學

- [Java 語言處理 – 使用 GroupDocs.Search 建立同義詞字典](/search/java/dictionaries-language-processing/)
- [如何實作 Java 全文搜尋：使用 GroupDocs.Search 建立索引目錄](/search/java/indexing/groupdocs-search-java-create-index/)
- [如何在 Java 中使用正規表達式搜尋：精通 GroupDocs.Search 進行文字文件分析](/search/java/searching/groupdocs-search-java-regex-tutorial/)