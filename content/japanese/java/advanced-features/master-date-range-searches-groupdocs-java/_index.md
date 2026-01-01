---
date: '2025-12-18'
description: GroupDocs.Search を使用したカスタム日付形式の Java 検索の実装方法を学び、日付範囲クエリやカスタムパターン、パフォーマンスのヒントを含める。
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: カスタム日付形式 Java | GroupDocs を使用した日付範囲検索
type: docs
url: /ja/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Custom Date Format Java | GroupDocs を使用した日付範囲検索

日付で文書を検索することは頻繁な要件です—アーカイブシステム、財務レポートツール、またはコンテンツ管理ポータルを構築する場合でも。本チュートリアルでは GroupDocs.Search を使用した **custom date format java** のテクニックを学び、日付範囲クエリ、カスタムパターン定義、そして **optimize search performance** のヒントをカバーします。最後まで読むと、ユーザーが使用する形式に関係なく、任意の日付区間に該当するレコードを取得できるようになります。

## クイック回答
- **インデックス作成の主要クラスは何ですか？** `Index` from the `com.groupdocs.search` package.  
- **カスタム日付パターンはどう定義しますか？** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **テキストクエリで検索できますか？** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **必要な Maven 座標は何ですか？** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **開発にライセンスは必要ですか？** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## **Javaのカスタム日付形式** とは？

**custom date format java** は、デフォルトの ISO パターン (YYYY‑MM‑DD) に従わない日付文字列を GroupDocs.Search がどのように解釈するかを指示します。`MM/dd/yyyy` や `dd‑MM‑yyyy` のように独自のパターンを定義することで、地域固有やレガシー形式の日付が埋め込まれた文書をエンジンが認識できるようになります。

## なぜ GroupDocs.Search を日付範囲クエリに使用するのか？

- **速度:** 組み込みインデックスにより検索は O(log n) で実行されます。  
- **柔軟性:** テキストベースとオブジェクトベースのクエリ作成の両方をサポートします。  
- **マルチフォーマットサポート:** PDF、Word、Excel、プレーンテキストなどを追加コードなしで処理します。

## GroupDocs.Search を使用した **日付で文書を検索** の方法

以下に、ライブラリのセットアップ、ファイルのインデックス作成、シンプルおよび高度な日付範囲検索の実行手順をステップバイステップで示します。

### 前提条件
- Java 8 以上がインストールされていること。  
- 依存関係管理のための Maven。  
- GroupDocs.Search ライセンスへのアクセス（開発にはトライアルまたは一時ライセンスで可）。

### Java 用 GroupDocs.Search の設定

#### Maven を使用したインストール
Add the repository and dependency to your `pom.xml`:

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

#### 直接ダウンロード
あるいは、最新バージョンを直接 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) からダウンロードできます。

#### 基本的な初期化と設定
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## 機能 1: 日付範囲検索クエリの作成

### テキスト形式クエリの使用
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Explanation**: `daterange` 構文は `YYYY‑MM‑DD` 形式の日付を期待します。インデックスされた日付がその区間に入るすべての文書を返します。

### クエリオブジェクトの使用
For programmatic control and custom parsing, build a `SearchQuery` object:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Explanation**: `createDateRangeQuery` は `java.util.Date` オブジェクトを提供でき、タイムゾーンやロケール固有の処理に対して完全な柔軟性を提供します。

## 機能 2: **custom date format java** パターンの指定

### カスタム日付フォーマットの設定
Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Explanation**: デフォルトのフォーマットをクリアし、区切り文字として `/` を使用する `DateFormat` を追加することで、エンジンは `MM/dd/yyyy` 形式の日付を認識できるようになります。これは月が先行する表記を好む地域で **search documents by date** を行う際に不可欠です。

## **optimize search performance** のヒント
- **インデックスを増分で更新**: 既存のインデックスに新しいファイルを追加し、ゼロから再構築しないでください。  
- **古いデータの削除**: 定期的に不要になった文書を削除します。  
- **メモリ設定の調整**: 大規模インデックスを扱う際は JVM ヒープ (`-Xmx`) を増やします。  

## よくある問題と解決策
- **日付パースエラー**: 文書の日付文字列が定義したカスタムパターンと完全に一致しているか確認してください。  
- **結果が出ない**: インデックスされたフィールドに日付メタデータが含まれていることを確認してください。含まれていないと、エンジンは日付クエリにマッチできません。  
- **インデックスアクセス例外**: `indexFolder` パスが書き込み可能で、他のプロセスにロックされていないことを確認してください。

## 実用的な適用例
1. **アーカイブシステム** – 特定の歴史的期間のレコードを取得します。  
2. **コンテンツ管理** – ヨーロッパ向けに `dd/MM/yyyy` などの地域日付フォーマットをサポートします。  
3. **金融ソフトウェア** – 取引を会計四半期や年で迅速にフィルタリングします。

## 結論
これで、GroupDocs.Search を使用した強力な日付範囲検索を構築するための完全な **custom date format java** ツールボックスが手に入りました。これらのパターンを実装し、パフォーマンスを微調整すれば、アプリケーションはあらゆる時間的クエリに対して高速かつ正確な結果を提供します。

## よくある質問

**Q: テキスト形式とオブジェクトベースの日付クエリの違いは何ですか？**  
A: テキスト形式は迅速で簡単ですがデフォルトの ISO 形式に限定されます。オブジェクトベースのクエリは `Date` オブジェクトやカスタムフォーマットを提供でき、柔軟性が向上します。

**Q: 1つのクエリで複数の日付範囲を検索できますか？**  
A: はい、`daterange` 条項を `AND` や `OR` などの論理演算子と組み合わせて複雑なクエリを構築できます。

**Q: カスタム日付フォーマットは検索を遅くしますか？**  
A: 追加のパースによるわずかなオーバーヘッドはありますが、一般的なワークロードでは影響はほとんどなく、精度向上のメリットが上回ります。

**Q: GroupDocs.Search は大規模展開に適していますか？**  
A: はい。適切なインデックス戦略と JVM のチューニングにより、数百万件の文書にスケールします。

**Q: さらに Java の例はどこで見つけられますか？**  
A: 追加のサンプルやユースケース実装は [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) をご覧ください。

---

**Resources**
- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support Forum**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2025-12-18  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs