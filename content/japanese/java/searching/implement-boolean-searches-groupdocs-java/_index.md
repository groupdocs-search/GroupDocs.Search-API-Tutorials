---
date: '2026-07-21'
description: Create Boolean Query Java チュートリアルでは、GroupDocs.Search for Java を使用してブール
  AND、OR、NOT 検索を実装する方法、ドキュメントをインデックスに追加する方法、そしてドキュメント取得をブーストする方法を示します。
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Create Boolean Query Java チュートリアルでは、GroupDocs.Search for Java を使用して
  AND、OR、NOT クエリを構築する手順をステップバイステップで解説し、ドキュメントをインデックスに追加し、取得パフォーマンスを向上させる方法を説明します。
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – GroupDocs.Search でブール検索をマスター
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Javaでブールクエリを作成: GroupDocs.Search for Java でブール検索をマスターする'
type: docs
url: /ja/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Javaでブール検索クエリを作成: GroupDocs.Search for Javaでブール検索をマスターする

大量のドキュメントコレクションを検索することは、干し草の山から針を探すように感じられることがあります。**Create Boolean Query Java** を使用すると、エンジンに正確に必要な条件—*両方* の用語を含むドキュメント、*いずれか* の用語を含むドキュメント、または不要な単語を*除外*するドキュメント—を指示できます。このガイドでは、**GroupDocs.Search for Java** の設定、インデックスへのドキュメント追加、そして **document retrieval java** ワークフローを強化する強力なブールクエリの作成手順を解説します。最後まで読むと、数行のコードだけで Java でブールクエリを作成するクリーンで保守しやすいコードを書けるようになります。

## クイック回答
- **ブール AND クエリとは何ですか？** 指定された*すべて*の用語を含むドキュメントのみを返します。  
- **OR は AND とどう違いますか？** OR は*いずれか*の用語を含むドキュメントに一致し、結果セットを拡大します。  
- **NOT はいつ使用すべきですか？** NOT を使用して、不要な単語を含むドキュメントを除外します。  
- **ライセンスは必要ですか？** 無料トライアルでテストできますが、本番環境では商用ライセンスが必要です。  
- **必要な Java バージョンは？** Java 8+ がサポートされており、JDK 11+ が推奨されます。

## **create boolean query java**とは何ですか？
`create boolean query java` は、GroupDocs.Search API を使用して AND、OR、NOT などの論理演算子を組み合わせた検索クエリを Java で構築することを指します。これらの演算子を組み合わせることで、マッチするドキュメントを正確に制御でき、高度なフィルタリング、関連性調整、複雑な検索シナリオを実現します。

## GroupDocs.Search for Javaを使用する理由は？
- **High performance** 大規模なドキュメントセットでも高速に動作し、標準サーバー上で 500 GB のテキストを 1 分未満でインデックス化・検索できます。  
- **Rich API** テキストベースとオブジェクトベースのクエリの両方をサポートし、アーキテクチャに合わせたスタイルを選択できます。  
- **Built‑in language support** 30 以上の言語に対してステミング、ストップワード、ファジーマッチングを提供します。  
- **Easy integration** Maven または直接 JAR ダウンロードで簡単に統合でき、数行のコードで開始できます。

## 前提条件
開始する前に以下を用意してください：

- **GroupDocs.Search for Java** (v25.4 以降) – 下記のダウンロードリンクをご参照ください。  
- IDE (IntelliJ IDEA、Eclipse など) に JDK 8+ がインストールされ、設定されていること。  
- 基本的な Java の知識と Maven による依存管理。

## GroupDocs.Search for Javaの設定

### Maven設定
リポジトリと依存関係を `pom.xml` に追加します：

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

### 直接ダウンロード
公式サイトから最新の JAR をダウンロードしてください: [GroupDocs.Search for Java リリース](https://releases.groupdocs.com/search/java/)。

### ライセンス取得
まずは無料トライアルライセンスで全機能を試せます。本番環境では商用ライセンスを購入してフル機能を有効化してください。

### 基本的な初期化と設定
インデックスフォルダーを作成し、`Index` オブジェクトをインスタンス化します：

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Javaでブールクエリを作成するには？
`Index` クラスはディスク上に保存された検索可能なドキュメントコレクションを表します。`BooleanQuery` は複数のサブクエリを論理演算子で組み合わせます。`createAndQuery`、`createOrQuery`、`createNotQuery` はそれぞれ AND、OR、NOT のサブクエリを構築します。`Index` インスタンスをロードまたは作成し、ドキュメントを追加した後、`createAndQuery`、`createOrQuery`、`createNotQuery` のいずれかで `BooleanQuery` オブジェクトを構築します。`index.search(query)` を呼び出して一致するドキュメントを取得します。このパターンはシンプルなシナリオでも複雑なシナリオでも機能し、インデックス初期化、ドキュメント追加、クエリ実行の 3 ステップだけで完了します。

## ブール AND 検索

### 概要
AND クエリは結果を絞り込み、複数の条件に一致するドキュメントが必要なときに関連性を向上させます。

### 実装手順

1. **Initialize Index** – これにより AND シナリオ用の **add documents to index** も示されます。

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – プレーン文字列構文を使用します。

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – プログラムでクエリを構築する際に便利です (**search with and java**)。

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## ブール OR 検索

### 概要
OR クエリは、いくつかのキーワードのうち少なくとも 1 つを含むドキュメントを取得したい探索的検索に最適です (**search with or java**)。

### 実装手順

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## ブール NOT 検索

### 概要
NOT クエリは、競合他社のブランド名など、不要な情報を除外して関連性の低いドキュメントを排除するのに役立ちます (**boolean search examples java**)。

### 実装手順

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## 複合ブールクエリ

### 概要
複合クエリは、たとえば「好意的なスポーツ記事だが特定の選手に関する記述は除外する」といった実世界の検索シナリオをモデル化できます。

### 実装手順

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## **java boolean and or** クエリの実用的な応用
- **Document Management Systems** – 「confidential」**AND**「renewal」の両方を含む契約書を検索します。  
- **Legal Research** – **AND**/**OR** を使って判例を絞り込み、**NOT** で古い法令を除外します。  
- **Customer Support** – 「login」**AND**「error」を含み、かつ「resolved」を含まないチケットを取得します。  
- **Content Curation** – ニュースレター用に「cloud」**OR**「serverless」に関するブログ記事を集めます。

## よくある落とし穴とトラブルシューティング
- **Missing Index Refresh** – 新しいドキュメントを追加した後、`index.update()` を呼び出して検索可能にします。  
- **Incorrect Operator Spacing** – GroupDocs.Search は演算子 (`AND`, `OR`, `NOT`) の前後にスペースがあることを期待します。  
- **Case Sensitivity** – クエリはデフォルトで大文字小文字を区別しませんが、カスタムアナライザーが影響する可能性があります。  
- **Large Result Sets** – メモリ過負荷を防ぐためにページネーション (`search(query, 0, 100)`) を使用します。  

## よくある質問

**Q: AND クエリで 2 つ以上の用語を組み合わせることはできますか？**  
A: もちろん可能です。複数の `createWordQuery` オブジェクトを `createAndQuery` でチェーンするか、テキストクエリで `"term1 AND term2 AND term3"` と記述してください。

**Q: GroupDocs.Search はワイルドカードやファジー検索をサポートしていますか？**  
A: はい。`*` を付けてワイルドカード（例: `promot*`）にし、`~` を付けてファジーマッチ（例: `comfort~`）にできます。

**Q: 特定のファイルタイプに検索を限定する方法は？**  
`FileTypeQuery` は PDF や DOCX など特定のファイル形式に検索結果を限定します。  
A: `FileTypeQuery` クラスを使用して PDF、DOCX などに結果を絞り込み、ブールクエリと組み合わせてください。

**Q: インデックス性能を監視する最適な方法は？**  
A: 組み込みロガーを有効にします (`index.getLogger().setLevel(Level.INFO)`)。各 `add` 操作後にタイミング指標を確認してください。

**Q: 特定の用語の関連性を高める方法はありますか？**  
`BoostQuery` は検索クエリ内の指定用語のスコアを上げます。  
A: 重要な単語を `BoostQuery` でラップして、スコアリングアルゴリズムでの重みを増やしてください。

---

**Last Updated:** 2026-07-21  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs

## 関連チュートリアル

- [Boolean Operators Java – Create Search Index & Faceted Search](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java&#58; Efficient Document Search and Index Management](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Mastering GroupDocs.Search Java – Create and Manage a Search Index](/search/java/indexing/groupdocs-search-java-create-index-guide/)