---
date: '2025-12-26'
description: GroupDocs.Search for Java を使用して、ドキュメント内のテキストを検索しハイライトする方法を学びましょう。全文書およびフラグメントのハイライト手法を探求します。
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: GroupDocs.Search for Javaでテキストを検索しハイライトする
type: docs
url: /ja/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# GroupDocs.Search for Java を使用したドキュメント内のテキスト検索とハイライト

今日のデジタル時代において、膨大なドキュメントコレクションに対する **search and highlight text** は一般的な要件です。法務レビューツール、学術研究ポータル、カスタマーサポートダッシュボードのいずれを構築する場合でも、キー用語を瞬時に検索し強調表示できることは、ユーザビリティを大幅に向上させます。この包括的ガイドでは、GroupDocs.Search for Java を使用した **search and highlight text** の実装方法を紹介します—全文書のハイライトと、コンテキストに焦点を当てたフラグメントレベルのハイライトの両方をカバーします。

## クイック回答
- **“search and highlight text” とは何ですか？** ドキュメント内でクエリ語句を検索し、視覚的に強調表示（例：背景色）することを指します。  
- **どのライブラリがこの機能を提供しますか？** GroupDocs.Search for Java。  
- **ライセンスは必要ですか？** 無料トライアルで評価できますが、本番環境ではフルライセンスが必要です。  
- **ハイライト色はカスタマイズできますか？** はい—任意の RGB 色を `HighlightOptions` で設定できます。  
- **フラグメントハイライトはサポートされていますか？** もちろんです。マッチ前後の語句数を指定して簡潔なスニペットを作成できます。

## Search and Highlight Text とは？
Search and highlight text は、指定されたクエリに対してドキュメントインデックスをスキャンし、一致するドキュメントを取得した後、ドキュメント出力（HTML、PDF など）内のクエリ語句のすべての出現箇所にマークを付けるプロセスです。この視覚的な手がかりにより、エンドユーザーは関連情報を瞬時に見つけることができます。

## なぜ GroupDocs.Search for Java を使用するのか？
- **High‑performance indexing** with configurable compression.  
- **Rich highlighting API** that works on whole documents and on custom fragments.  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT, and more).  
- **Easy Maven integration** and clear Java‑centric API.

## 前提条件
- Java Development Kit (JDK) 8 or newer.  
- Maven for dependency management.  
- IntelliJ IDEA や Eclipse などの IDE。  
- Java 文法に関する基本的な知識。

## GroupDocs.Search for Java のセットアップ

Add the GroupDocs repository and dependency to your `pom.xml`:

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

You can also download the latest JAR directly from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### ライセンス取得
Start with a free trial or obtain a temporary license for evaluation. For production deployments, purchase a full license to unlock all features.

## 実装ガイド

The implementation is split into two practical sections: **highlighting in entire documents** and **highlighting in fragments**. Both sections include the essential steps for **how to highlight Java** documents using GroupDocs.Search.

### インデックス設定の構成
Before indexing, configure the storage to use high compression—this reduces disk usage while preserving search speed.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### 全文書のハイライト

#### 手順 1: インデックスの作成とデータの投入
Create an index folder and add all source files you want to search.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### 手順 2: 検索の実行とハイライトの適用
Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted matches.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Key options explained**
- **Compression** – high compression saves storage.  
- **HighlightColor** – set any RGB value to match your UI palette.  
- **UseInlineStyles** – `false` generates clean HTML that can be styled globally with CSS.

### フラグメントのハイライト

#### 手順 1: インデックス作成と検索（上記と同様）
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### 手順 2: フラグメントコンテキストの定義とハイライト
Specify how many terms before and after the match should appear in each fragment.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### 手順 3: ハイライトされたフラグメントの取得と書き出し
Collect the generated fragments and write them to an HTML file.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## 実用的な活用例
1. **Legal Document Review** – instantly highlight statutes, clauses, or case references.  
2. **Academic Research** – surface key terminology across dozens of PDFs and Word files.  
3. **Customer Support** – pinpoint order numbers or error codes within ticket histories.

## パフォーマンス考慮事項
- **Index Size** – high compression (`Compression.High`) reduces disk footprint.  
- **Fragment Context** – larger `termsBefore/After` values increase accuracy but may affect speed.  
- **Memory Management** – monitor JVM heap when indexing large corpora; consider incremental indexing for very large sets.

## よくある問題と解決策
- **Indexing Errors** – verify file paths and ensure the application has read/write permissions.  
- **No Highlights Appear** – confirm that `UseInlineStyles` matches your output format (HTML vs. PDF).  
- **Color Not Applied** – make sure the RGB values are within 0‑255 range and that the HTML viewer supports the style.

## よくある質問

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: It offers fast, scalable indexing, customizable highlighting, and support for many document formats.

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: Expose the search and highlight methods via Spring Boot controllers, returning HTML or JSON payloads.

**Q: Does the library handle password‑protected files?**  
A: Yes—provide the password when adding the document to the index.

**Q: Can I customize the highlight markup beyond color?**  
A: Absolutely; you can inject CSS classes via `HighlightOptions` or modify the HTML after generation.

**Q: What version was tested for this guide?**  
A: The code was validated against GroupDocs.Search 25.4.

---

**最終更新日:** 2025-12-26  
**テスト環境:** GroupDocs.Search 25.4  
**作成者:** GroupDocs