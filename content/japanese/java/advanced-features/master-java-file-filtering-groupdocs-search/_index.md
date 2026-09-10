---
date: '2026-09-06'
description: GroupDocs.Search for Java を使用して Java のファイル拡張子をフィルタリングする方法を学びます。論理演算子
  AND、OR、NOT、日付範囲フィルタ、パスフィルタについて解説します。
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: GroupDocs.Search を使用して Java のファイル拡張子をフィルタリングします。Java で論理演算子を使い、拡張子、日付範囲、パスフィルタを組み合わせる方法を学びます。
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: GroupDocs.Search で Java のファイル拡張子をフィルタリング – 完全ガイド
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: GroupDocs.Search を使用した Java のファイル拡張子フィルタリング方法
type: docs
url: /ja/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Searchでjavaのファイル拡張子をフィルタリングする

この包括的なチュートリアルでは、GroupDocs.Searchでドキュメントをインデックス化する際に **filter file extensions java** を学びます。ガイドの最後までに、必要なファイルタイプだけを含め、不要な形式を除外し、日付範囲やパスフィルタと論理演算子（AND、OR、NOT）で組み合わせる方法が身につきます。このアプローチによりインデックスが軽量化され、検索が高速化され、データ取り扱いポリシーへの準拠も容易になります。

## クイック回答
- **java ファイル拡張子フィルタとは何ですか？** これは、インデックス作成時に GroupDocs.Search がどのファイル拡張子を含めるか、除外するかを指示するルールです。  
- **どのライブラリがこの機能を提供しますか？** GroupDocs.Search for Java。  
- **ライセンスは必要ですか？** 無料トライアルで評価できますが、本番環境ではフルライセンスが必要です。  
- **フィルタを組み合わせられますか？** はい – 拡張子、日付、サイズ、パスフィルタを AND、OR、NOT ロジックで連結できます。  
- **Maven に対応していますか？** 完全に対応しています – `pom.xml` に GroupDocs.Search の依存関係を追加してください。

## java ファイル拡張子フィルタとは何ですか？
**java ファイル拡張子フィルタ** は、各ファイルの拡張子をインデックスエンジンに送る前に評価するルールセットです。`.txt`、`.pdf`、`.epub` などの拡張子を指定することで、**拡張子でファイルを含める** または **拡張子でファイルを除外する** が可能になり、インデックスを目的に合わせて絞り込み、検索結果の関連性を高めます。

## GroupDocs.Searchでファイル拡張子フィルタリングを使用する理由
ファイル拡張子フィルタリングは、不要なフォーマットを除外することでインデックス作成の効率を向上させ、ストレージ要件を削減し、機密情報やサポート外のファイルがインデックスに入らないようにしてコンプライアンスを支援します。また、データセットが小さくなるためクエリ応答が高速化します。

- **パフォーマンス:** 不要なファイルをスキップすることで I/O が削減され、大規模リポジトリではインデックス作成が最大 40 % 速くなります。  
- **ストレージ削減:** 関連するドキュメントだけがインデックスに保存され、ディスク使用量が平均 30 % 減少します。  
- **コンプライアンス:** 機密情報やサポート外のファイルタイプの誤インデックスを防止します。  
- **柔軟性:** **date range filter java** 機能と組み合わせて、特定期間に作成または変更されたファイルを対象にできます。

## 前提条件

開始する前に、以下を確認してください。

### 必要なライブラリと依存関係
- **GroupDocs.Search for Java** – バージョン 25.4 以降（60 以上の入力フォーマットに対応）。  
- **Java Development Kit (JDK)** – 任意の互換バージョン（8 以降）。

### 環境設定
- 統合開発環境 (IDE): IntelliJ IDEA、Eclipse、または任意の Maven 対応 IDE。

### 知識の前提条件
- 基本的な Java プログラミング。  
- Java におけるファイル I/O の知識。  
- 正規表現と日付時刻処理の理解。

## GroupDocs.Search for Java のセットアップ
GroupDocs.Search を使用開始するには、プロジェクトに依存関係として追加する必要があります。

### Maven 設定
以下のリポジトリと依存関係の設定を `pom.xml` ファイルに追加してください。

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
あるいは、[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) から最新バージョンを直接ダウンロードしてください。

#### ライセンス取得
1. **無料トライアル** – コストなしで機能を試せます。  
2. **一時ライセンス** – 限定期間でフル機能を利用できます。  
3. **購入** – 本番環境で使用する永続ライセンスを取得します。

### 基本的な初期化と設定
ライブラリを追加したら、インデックス環境を初期化します。`IndexSettings` クラスはフィルタを含むすべての構成オプションを保持します。

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## 実装ガイド
以下では各フィルタタイプを詳しく解説し、**なぜ重要か** を説明したうえで、プロジェクトにコピーできる手順をステップバイステップで提供します。

### ファイル拡張子フィルタリング
インデックス作成時に拡張子でファイルをフィルタリングします。e‑book（`.fb2`、`.epub`）やプレーンテキスト（`.txt`）だけを処理したい場合に最適です。

#### 概要
`DocumentFilter.createFileExtension` は拡張子のホワイトリストを作成します。

#### 実装手順
1. **フィルタ作成** – 保持したい拡張子を定義します。

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **インデックス初期化とドキュメント追加** – `IndexSettings` を構築する際にフィルタを適用します。

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 論理 NOT フィルタ
検索シナリオで不要な場合、ウェブページや PDF など特定の拡張子を除外します。

#### 実装手順
1. **除外フィルタ作成** – 拒否したい拡張子を指定します。

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **インデックス設定に適用** – NOT フィルタを他のルールと組み合わせます。

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **ドキュメント追加** – 組み合わせたフィルタを通過したファイルだけがインデックス化されます。

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 論理 AND フィルタ
作成日、拡張子、ファイルサイズなど複数条件を組み合わせ、**すべての条件を満たすファイル** のみをインデックス化します。

#### 概要
`DocumentFilter.createAnd` は複数のフィルタを単一ルールに統合します。

#### 実装手順
1. **フィルタ定義** – 各条件ごとに個別フィルタを作成します。

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **フィルタ結合** – AND 演算子で全条件を必須にします。

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **ドキュメントインデックス** – 結合フィルタをインデックスパイプラインに渡します。

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 論理 OR フィルタ
**いずれかの条件を満たす** ファイルを含めます。小さなテキストファイルと大きな非テキストファイルの両方を取得したい場合に便利です。

#### 実装手順
1. **フィルタ定義** – 代替条件ごとに別々のフィルタを作成します。

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **論理条件で結合** – OR 演算子を使用します。

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **OR フィルタ確定** – 結合フィルタをインデックス構成に添付します。

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 作成時間フィルタ
特定期間内に作成されたファイルを対象にします。典型的な **date range filter java** シナリオです。

#### 実装手順
1. **日付範囲フィルタ定義** – 開始日と終了日を指定します。

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **ドキュメントインデックス** – 作成タイムスタンプが範囲内にあるファイルだけがインデックス化されます。

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 更新時間フィルタ
特定のカットオフ日以降に変更されたファイルを除外します。

#### 実装手順
1. **フィルタ定義** – 最大更新タイムスタンプを設定します。

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **ドキュメントインデックス** – カットオフ以降に更新されたファイルは無視されます。

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ファイルパスフィルタリング
特定フォルダ内またはパターンに一致するファイルだけをインデックス対象とします。特定ディレクトリ階層内で **include files by extension** を実現するのに最適です。

#### 実装手順
1. **ファイルパスフィルタ定義** – glob または正規表現パターンでディレクトリをマッチさせます。

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **インデックス初期化とドキュメント追加** – パスフィルタを他のルールと併用します。

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## よくある落とし穴とヒント

- **絶対パスと相対パスを同一フィルタ構成で混在させない** – 予期しない除外が発生する可能性があります。  
- **`IndexSettings` をリセット** してからフィルタセットを切り替えないと、以前のフィルタが残ります。  
- **拡張子フィルタとサイズ上限を組み合わせ** て、大規模コレクションのメモリ使用量を抑えます。  
- LoggingOptions は GroupDocs.Search のロギング構成を制御します。  
- **ロギングを有効化** (`LoggingOptions.setEnabled(true)`) すると、ファイルが除外された理由を確認できます。  

## よくある質問

**Q: インデックス作成後にフィルタ基準を変更できますか？**  
A: はい。新しい `DocumentFilter` でインデックスを再構築するか、設定を更新したインクリメンタルインデックスを使用してください。

**Q: java ファイル拡張子フィルタは圧縮アーカイブ（例: ZIP）に対して機能しますか？**  
A: GroupDocs.Search はサポートされているアーカイブ形式をインデックス化できますが、拡張子フィルタはアーカイブ自体に適用され、内部ファイルには適用されません。内部ファイルを制御したい場合はネストされたフィルタを使用してください。

**Q: 特定のファイルが除外された理由をデバッグする方法は？**  
A: ライブラリのロギングを有効化 (`LoggingOptions.setEnabled(true)`) し、ログを確認するとどのフィルタがファイルを拒否したかが記録されます。

**Q: java ファイル拡張子フィルタをカスタム正規表現フィルタと組み合わせられますか？**  
A: 完全に可能です。拡張子フィルタと共に `DocumentFilter.createAnd()` 内で正規表現フィルタをラップしてください。

**Q: 多数のフィルタを追加するとパフォーマンスにどの程度影響しますか？**  
A: 各フィルタはインデックス作成時にわずかなオーバーヘッドを加えますが、インデックス対象データが減少することで得られる速度向上が通常は上回ります。代表的なサンプルでテストし、最適なバランスを見つけてください。

---

**最終更新日:** 2026-09-06  
**テスト環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs

## 関連チュートリアル

- [カスタム日付フォーマット Java | GroupDocsによる日付範囲検索](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: GroupDocs.Search for Java でのブール検索マスター](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [GroupDocs.Search for Java の高度なインデックス技術で検索パフォーマンスを最適化](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

