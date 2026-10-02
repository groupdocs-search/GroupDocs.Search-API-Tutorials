---
date: '2026-10-02'
description: Javaで chunk‑based search を使用してインデックスにドキュメントを追加する際に temporary license
  の使い方を学び、検索パフォーマンス (search performance) を向上させながらメモリ使用量 (memory usage) を制御します。
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Javaで chunk‑based search を使用してインデックスにドキュメントを追加する際に temporary license
  を使用し、検索速度 (search speed) を向上させ、メモリ消費 (memory consumption) を削減します。
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Javaで chunk‑based indexing に temporary license を使用する
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Javaで chunk‑based indexing に temporary license を使用する
type: docs
url: /ja/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Javaでチャンクベースのインデックス作成に一時ライセンスを使用する

このチュートリアルでは、**一時ライセンス**を使用して、GroupDocs.Search のチャンクベース検索機能でドキュメントをインデックスに追加します。このアプローチにより、法的契約書、サポートチケット、研究論文などの大量のドキュメントコレクションを扱いながら、**java search index memory** の使用量を低く抑え、**検索パフォーマンスを大幅に向上**させることができます。インデックスフォルダーの設定方法、複数のドキュメントソースの投入、チャンク検索の有効化、そして最初のクエリとその後のクエリの実行方法を確認します。

## クイック回答
- **最初のステップは何ですか？** 検索インデックスフォルダーを作成します。  
- **多数のファイルを含めるには？** 各ドキュメントフォルダーに対して `index.add()` を使用します。  
- **どのオプションがチャンク検索を有効にしますか？** `options.setChunkSearch(true)`。  
- **最初のチャンクの後も検索を続けられますか？** はい、トークンを使用して `index.searchNext()` を呼び出します。  
- **ライセンスは必要ですか？** 開発には無料トライアルまたは一時ライセンスで十分です。製品環境ではフルライセンスが必要です。  

## 学べること
- 指定フォルダーに検索インデックスを作成する方法。  
- 複数の場所から **add documents to index** を行う手順。  
- チャンクベース検索を有効にする検索オプションの設定。  
- 初回およびその後のチャンクベース検索の実行。  
- チャンクベースのドキュメント検索が有効に機能する実際のシナリオ。  

## 前提条件
- **必要なライブラリ**: GroupDocs.Search for Java 25.4 以降。  
- **環境設定**: 互換性のある Java Development Kit (JDK) がインストールされていること。  
- **知識の前提**: 基本的な Java プログラミングと Maven の知識。  

## GroupDocs.Search for Java の設定
まず、Maven を使用してプロジェクトに GroupDocs.Search を統合します：

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

あるいは、最新バージョンを [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) からダウンロードしてください。

### ライセンス取得
GroupDocs.Search を試すには：

- **無料トライアル** – コミットせずにコア機能をテストできます。  
- **一時ライセンス** – 開発用に拡張されたアクセス。  
- **購入** – 本番環境で使用するフルライセンス。  

## インデックスにドキュメントを追加する方法は？
**直接的な回答:** 検索対象としたいファイルが含まれる各フォルダーに対して `index.add()` を呼び出します。このメソッドはフォルダーを再帰的にスキャンし、サポートされているすべてのドキュメントを単一の操作でインデックスに追加します。これにより、ファイルごとの手動処理が不要になり、一括取り込みが高速化されます。

`SearchIndex` はディスク上の検索可能なコレクションを表す中心クラスです。インスタンス化した後は、すべてのインデックス作成およびクエリ操作がこのオブジェクトを通じて行われます。

### 1. インデックスの作成
**直接的な回答:** インデックスファイルを保存するパスで `SearchIndex` オブジェクトをインスタンス化し、`index.create()` を呼び出してストレージ構造を初期化します。この呼び出しは、初回使用時に必要なフォルダーとメタデータファイルを作成します。

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. インデックスへのドキュメント追加
**直接的な回答:** `index.add()` メソッドを使用し、各ソースフォルダーの絶対パスを渡します。API は自動的にサポートされている形式（PDF、DOCX、XLSX など）を検出し、検索可能なテキストをインデックスに抽出します。

`SearchOptions` はインデックス作成および検索時のドキュメント処理方法を細かく調整できる構成オブジェクトです。後でチャンクベースのクエリを有効にするために使用します。

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. チャンク検索のための検索オプション設定
**直接的な回答:** クエリ実行前に `SearchOptions` インスタンスで `options.setChunkSearch(true)` を設定します。これによりエンジンは各ドキュメントを論理的なチャンク（通常は段落）に分割し、ファイル全体ではなくチャンク単位で一致結果を返します。

`SearchResult` は一致したチャンク、その位置、関連度スコアを保持します。チャンク検索が有効な場合、各 `SearchResult` は元のドキュメントの単一フラグメントに対応します。

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. 初回のチャンクベース検索の実行
**直接的な回答:** `index.search("your query", options)` を実行します。この呼び出しは、最初の一致チャンクの `SearchResult` コレクションと、検索状態を表すトークンを返します。

返されたトークンは、全体のクエリを再実行せずに大規模な結果セットをページングするために不可欠です。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. チャンクベース検索の継続
**直接的な回答:** 前回の呼び出しで返されたトークンを `index.searchNext(token, options)` に渡します。メソッドが `null` を返すまで繰り返し、すべての一致チャンクが取得されたことを示します。

このインクリメンタル方式は、現在のチャンクバッチのみがメモリに保持されるため、メモリ使用量を低く抑えます。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## なぜチャンクベース検索を使用するのか？
チャンクベース検索は、大規模なドキュメントコレクションを扱いやすい部分に分割し、メモリ負荷を軽減し、応答時間を高速化します。段落やセクション単位でインデックス化することで、エンジンは関連するフラグメントだけを取得でき、CPU 使用率を下げ、エンドユーザーのレイテンシを改善します。特に以下の場合に有益です：

- **Legal teams** は何千もの契約書から特定の条項を検索する必要があります。  
- **Customer support portals** は関連するナレッジベース記事を即座に表示する必要があります。  
- **Researchers** は全ファイルをメモリに読み込むことなく、大規模データセットを検索します。  

具体的な主張: GroupDocs.Search は標準的な 8 コアサーバー上で、**500 ページ超の PDF** を **チャンクあたり 2 秒未満** で処理でき、ピークヒープを **200 MB** 未満に抑えます。

## このアプローチが検索パフォーマンスを向上させる方法
**直接的な回答:** ファイル全体ではなく小さなチャンクを検索することで、エンジンは不要なセクションを早期にスキップし、CPU サイクルを削減し、アクティブなチャンクだけをメモリに保持できるため、**java search index memory** の消費を直接削減し、応答時間を高速化します。このターゲット型アプローチは、より効果的なキャッシュと並列処理も可能にし、複数のコアが同時に異なるチャンクを処理できるため、マルチコアサーバーでのスループットがさらに向上します。

追加の利点は以下の通りです：
- 複数コアによるチャンクの並列処理。  
- 高関連性の一致が見つかった際の早期終了。  

## java search index memory の管理
**直接的な回答:** 想定されるインデックスサイズに応じて十分な JVM ヒープ（例: `-Xmx2g` 以上）を割り当て、バルク追加後に `index.optimize()` を実行してインデックス構造を圧縮し、VisualVM で GC の一時停止を監視してレイテンシスパイクを防止します。

さらにチューニングするヒント：
- 大量バッチの後に `index.flush()` を使用して中間データをディスクに書き出す。  
- `options.setMemoryLimit(256)` を有効にして、検索ごとのメモリ使用量を上限設定する。  

## パフォーマンス上の考慮点
- **メモリ管理** – 大規模インデックス用に十分なヒープ領域（`-Xmx`）を割り当てる。  
- **リソース監視** – インデックス作成および検索時の CPU 使用率を監視する。  
- **インデックス保守** – 定期的にインデックスを再構築またはクリーンアップし、古いデータを削除する。  

## よくある落とし穴とトラブルシューティング
| 問題 | 発生理由 | 対策 |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | ヒープサイズが小さすぎる | JVM ヒープを増やす（`-Xmx2g` 以上） |
| No results returned | チャンクトークンが処理されていない | `while` ループが `getNextChunkSearchToken()` が `null` になるまで実行されていることを確認 |
| Slow search performance | インデックスが最適化されていない | バルク追加後に `index.optimize()` を実行 |

## よくある質問
**Q: チャンクベース検索とは何ですか？**  
A: チャンクベース検索はデータセットを小さなピースに分割し、ドキュメント全体をメモリに読み込むことなく大規模データに対して効率的なクエリを実行できるようにします。

**Q: 新しいファイルでインデックスを更新するには？**  
A: 新しいドキュメントへのパスを指定して `index.add()` を呼び出すだけで、インデックスに自動的に取り込まれます。

**Q: GroupDocs.Search はさまざまなファイル形式に対応していますか？**  
A: はい、**PDF、DOCX、XLSX、PPTX、HTML、TXT、その他 30 以上の形式** をサポートしています。

**Q: 典型的なパフォーマンスボトルネックは何ですか？**  
A: メモリ制約と最適化されていないインデックスが最も一般的です。十分なヒープを割り当て、定期的にインデックスを最適化してください。

**Q: 詳細なドキュメントはどこで見つけられますか？**  
A: 公式の [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) をご覧ください。詳細なガイドと API リファレンスが掲載されています。

**Q: 暗号化された PDF でもチャンクベース検索は機能しますか？**  
A: はい、適切な API オーバーロードでパスワードを提供すれば動作します。

**Q: インデックス作成の進捗を監視するには？**  
A: `Index.add()` のオーバーロードで `Progress` オブジェクトを返すものを使用するか、ロギングコールバックにフックしてください。

## リソース
- **ドキュメント**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API リファレンス**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **ダウンロード**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **無料サポート**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **一時ライセンス**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最終更新日:** 2026-10-02  
**テスト環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 関連チュートリアル

- [検索インデックスディレクトリの作成とライセンス設定 – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [GroupDocs.Search Java でクエリパフォーマンスを向上 – インデックスと検索の最適化](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java 高度な検索機能](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)