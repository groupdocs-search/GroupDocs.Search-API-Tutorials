---
date: '2026-02-21'
description: GroupDocs.Search を使用して Java でスペル補正を有効にし、インデックスにドキュメントを追加し、検索精度向上のために最大ミス数を設定する方法を学びましょう。
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: GroupDocs.Search を使用して Java でスペリングを有効にする方法
type: docs
url: /ja/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

Docs (no translation).

Now ensure we preserve markdown formatting: headings, bold, lists, tables.

Check for any shortcodes: none besides placeholders.

Now produce final content.

# JavaでGroupDocs.Searchを使用してスペリングを有効にする方法

正確な検索結果は、現代のアプリケーションにとって不可欠です。このチュートリアルでは、GroupDocs.Searchを使用してJavaで**スペリングを有効にする**方法を学び、ユーザーがクエリを誤入力しても正しい結果が得られるようにします。インデックスの作成、**インデックスへのドキュメント追加**、スペリングオプションの設定、そして自動的に誤りを修正する検索の実行手順を順に説明します。

## クイック回答
- **「スペリングを有効にする」とは何ですか？** 組み込みのスペルチェッカーを有効にし、検索時にユーザーのタイプミスを修正します。  
- **どのライブラリがこの機能を提供しますか？** GroupDocs.Search for Java。  
- **ライセンスは必要ですか？** 評価には無料トライアルライセンスで動作しますが、本番環境ではフルライセンスが必要です。  
- **許容度を制御できますか？** はい – `setMaxMistakeCount` を使用して許容できるタイプミスの数を定義します。  
- **大規模インデックスに適していますか？** もちろんです – エンジンは高性能なインデックス作成と検索に最適化されています。

## GroupDocs.Searchで「スペリングを有効にする」とは何ですか？
スペリングを有効にすると、クエリにエラーが含まれている場合に検索エンジンが最も近い正しい語句を探すようになります。この機能は、誤字入力でも関連性の高い結果を返すことでユーザー体験を大幅に向上させます。

## Javaアプリケーションでスペリング補正を有効にする理由は？
- **ユーザー満足度の向上** – ユーザーは完璧に入力する必要がありません。  
- **直帰率の低減** – より正確な結果で訪問者のエンゲージメントが向上します。  
- **さまざまなドメインで利用可能** – 図書館カタログから e コマースの製品検索まで。

## 前提条件
- Java Development Kit (JDK) がインストールされていること。  
- 基本的な Java と Maven の知識。  
- インデックス概念の理解。  
- GroupDocs.Search のトライアルまたはライセンスキー。

### GroupDocs.Search for Java のセットアップ
ライブラリを Maven プロジェクトに統合します。

**Maven 設定**  
リポジトリと依存関係を `pom.xml` ファイルに追加します:

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

**直接ダウンロード**  
あるいは、最新バージョンを [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) からダウンロードしてください。

### ライセンス取得
評価用に無料トライアルライセンスを取得します。本番利用の場合は、フルライセンスを購入するか、公式サイトから一時キーをリクエストしてください。

## インデックスへのドキュメント追加方法
インデックスの作成は、検索対応アプリケーションの基盤です。以下はフォルダーから **インデックスにドキュメントを追加** する最小例です。

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

*ヒント:* パスが正しいこと、アプリケーションがインデックスフォルダーへの書き込み権限を持っていることを確認してください。

## スペリング補正の設定方法（set max mistake count）
スペルチェッカーを有効にし、エラー許容度を設定することで細かく調整できます。

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

*`setMaxMistakeCount` が重要な理由:* エンジンが許容するタイプミスの数を定義します。ドメイン固有のエラーパターンに応じてこの値を調整してください。

## スペリング補正検索の実行方法
インデックスが準備でき、スペリングオプションが設定されたら、誤りを含む可能性のあるクエリを実行します。

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

`search()` 呼び出しは、修正された語句と最も関連性の高いドキュメントを含む `SearchResult` を返します。

## 実用的な活用例
1. **図書館システム:** 誤字の書名や著者名を修正します。  
2. **E コマースプラットフォーム:** 製品検索でのユーザーのタイプミスを修正し、コンバージョンを向上させます。  
3. **コンテンツ管理システム:** 編集スタッフのために記事検索を改善します。

## パフォーマンス上の考慮点
- **インデックスを最新に保つ** – 新規または変更されたファイルを定期的に再インデックスします。  
- **JVM メモリ設定の調整** – 大規模インデックス用に十分なヒープを割り当てます。  
- **リソース使用状況の監視** – 必要に応じてガベージコレクタのフラグを調整します。

## よくある問題とトラブルシューティング
| 症状 | 想定原因 | 対策 |
|---------|--------------|-----|
| スペリングを有効にした後に結果が返らない | インデックスフォルダーのパスが間違っているか空です | `indexFolder` が有効なインデックスを指していること、`index.add()` が成功したことを確認してください |
| スペルチェッカーが明らかなタイプミスを修正しない | `setMaxMistakeCount` が低すぎる | 許容度を高めるためにカウントを 2 または 3 に増やしてください |
| 大量のドキュメントセットでアプリケーションがクラッシュする | JVM ヒープが不足している | `-Xmx` オプションを増やす（例: `-Xmx4g`） |

## よくある質問

**Q: GroupDocs.Search とは何ですか？**  
A: 高速インデックス作成、高度な検索機能、組み込みのスペリング補正を提供する Java ライブラリです。

**Q: GroupDocs.Search のライセンスはどう取得しますか？**  
A: 公式サイトで無料トライアルをダウンロードするか、フルライセンスを購入してください。

**Q: GroupDocs.Search を他の Java フレームワークと統合できますか？**  
A: はい、Spring、Jakarta EE、その他標準的な Java アプリケーションで動作します。

**Q: インデックス設定時の一般的な問題は何ですか？**  
A: フォルダー パスの誤り、ファイル権限不足、`pom.xml` の依存関係が欠如していることなどです。

**Q: スペル補正は検索結果をどのように改善しますか？**  
A: 誤字クエリを最も近い正しい語句に自動的に書き換え、より関連性の高いヒットを返します。

## 追加リソース
- [ドキュメント](https://docs.groupdocs.com/search/java/)
- [API リファレンス](https://reference.groupdocs.com/search/java)
- [ダウンロード](https://releases.groupdocs.com/search/java/)
- [GitHub リポジトリ](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [無料サポートフォーラム](https://forum.groupdocs.com/c/search/10)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)

---

**最終更新日:** 2026-02-21  
**テスト環境:** GroupDocs.Search 25.4  
**作者:** GroupDocs