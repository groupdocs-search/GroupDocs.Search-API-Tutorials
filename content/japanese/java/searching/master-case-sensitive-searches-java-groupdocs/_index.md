---
date: '2026-02-06'
description: GroupDocs.Search を使用して Java でドキュメントをインデックスに追加し、ケースセンシティブ検索を有効にする方法を学び、アプリケーションの精度を向上させましょう。
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: インデックスにドキュメントを追加：GroupDocs を使用した大文字小文字を区別する Java 検索
type: docs
url: /ja/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# インデックスにドキュメントを追加: GroupDocs を使用した Java の大文字小文字検索のマスター

大量のドキュメントコレクションから目的の情報を取得することは、現代アプリケーションの重要な要件です。このガイドでは、GroupDocs.Search for Java を使用して **インデックスにドキュメントを追加** し、 **大文字小文字を区別した検索** を実行する方法を学びます。法務文書リポジトリ、eコマースカタログ、コンテンツ管理システムなど、正確な検索結果はユーザーの満足度とデータの信頼性を高めます。

## Quick Answers
- **検索を開始するための最初のステップは何ですか？** `index.add(...)` でインデックスにドキュメントを追加します。  
- **大文字小文字検索を有効にするには？** `options.setUseCaseSensitiveSearch(true)` を設定します。  
- **複数ディレクトリを横断して検索できますか？** はい – 追加したいフォルダーごとに `index.add()` を呼び出します。  
- **オブジェクトで検索するメソッドはどれですか？** `SearchQuery.createWordQuery(...)` を使用します。  
- **テスト用にライセンスは必要ですか？** 試用目的の一時ライセンスが利用可能です。

## “インデックスにドキュメントを追加” とは何ですか？
インデックスにドキュメントを追加するとは、PDF、Word、プレーンテキストなどのソースファイルを GroupDocs.Search に取り込み、検索可能なデータ構造を構築することです。インデックス化が完了すると、エンジンは高速なクエリ（大文字小文字を区別したものも含む）を実行できます。

## Java で大文字小文字検索を有効にする理由
- **正確な語句一致** – 「Apple」（企業）と「apple」（果物）を区別できます。  
- **規制遵守** – 業界によっては正確なフレーズ一致が求められます。  
- **関連性の向上** – 技術文書や法務文書など、ケースセンシティブな結果が期待されるシナリオで有用です。

## 前提条件
- JDK（Java 17 以上推奨）  
- 依存関係管理のための Maven  
- IntelliJ IDEA または Eclipse などの IDE  
- Java プログラミングの基本的な知識  

## GroupDocs.Search for Java のセットアップ
まず、`pom.xml` に GroupDocs リポジトリと依存関係を追加します。

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

あるいは、[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) から最新バージョンを直接ダウンロードできます。

### ライセンス
トライアルを開始するには、GroupDocs のサイトで一時ライセンスを取得してください。これにより、機能制限なしで全ての機能をテストできます。

## インデックスにドキュメントを追加 – テキストクエリ検索

### 手順 1: インデックスを作成し、ドキュメントを追加
インデックスファイルを保存するフォルダーを作成し、検索対象となるドキュメントが格納されたソースディレクトリを追加します。

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **プロのコツ:** `index.add()` を複数回呼び出すことで、**単一インデックス内で複数ディレクトリを検索** できます。

### 手順 2: 大文字小文字検索を有効化
検索オプションで文字ケースを考慮するよう設定します。

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 手順 3: 大文字小文字を区別したテキストクエリを実行
「Advantages」と「advantages」を区別するクエリを実行します。

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

このループは、正確にケースが一致した語句を含む各ドキュメントのフルパスを出力します。

## インデックスにドキュメントを追加 – オブジェクトクエリ検索

オブジェクトクエリは、複数の条件を組み合わせる必要がある場合に柔軟性を提供します。

### 手順 1: 2 番目のインデックスを初期化（任意）
オブジェクトベースの検索を別管理したい場合は、別のインデックスフォルダーを作成します。

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### 手順 2: 大文字小文字オプションを再利用
同じ `SearchOptions` インスタンスをオブジェクトクエリでも使用できます。

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 手順 3: オブジェクトクエリを構築して実行
ワードクエリオブジェクトを作成し、検索エンジンに渡します。

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

`createWordQuery` を使用すると、後でフレーズ、ワイルドカード、ブールクエリと組み合わせて、より複雑なシナリオを構築できます。

## 実用的な活用例
- **法務文書管理:** 大文字小文字が重要な条文や判例を正確に取得。  
- **eコマースプラットフォーム:** 「PRO‑X」 と 「pro‑x」 のような SKU を区別。  
- **コンテンツ管理システム (CMS):** 著者が正確な見出しやタグを検索できるように。

## パフォーマンス上の考慮点
- **インデックスを常に最新に保つ** – 新規ファイルの追加や既存ファイルの変更時に再インデックス化します。  
- **メモリ使用量を監視** – 大規模コーパスではインクリメンタルインデックスと適切な JVM ヒープサイズが有効です。  
- **Java のガベージコレクタを活用** – `Index` オブジェクトは不要になったら解放します。

## よくある問題と解決策
| Issue | Solution |
|-------|----------|
| `useCaseSensitiveSearch` が無視されているように見える | 最新の GroupDocs.Search バージョンを使用し、オプション変更後にインデックスを再構築したことを確認してください。 |
| 既知の語句で結果が返ってこない | 語句のケースが完全に一致しているか、ドキュメントがインデックスに正しく追加されたかを確認してください。 |
| 多数のフォルダーを検索すると遅くなる | 各フォルダーを個別に `index.add()` で追加し、データセットが非常に大きい場合はインデックスをシャードに分割することを検討してください。 |

## Frequently Asked Questions

**Q:** GroupDocs.Search で大規模データセットを扱うには？  
**A:** インデックスのパーティショニング、JVM メモリ設定の調整、定期的なインデックス圧縮を行い、パフォーマンスを最適化します。

**Q:** 複数ディレクトリを同時に検索できますか？  
**A:** はい – 追加したいディレクトリごとに `index.add()` を呼び出し、結合されたインデックスに対して単一クエリを実行します。

**Q:** 大文字小文字検索設定時の一般的な落とし穴は？  
**A:** `useCaseSensitiveSearch` を有効にした後にインデックスを再構築し忘れる、またはクエリ文字列のケースが誤っていることです。

**Q:** 検索エラーのトラブルシューティング方法は？  
**A:** GroupDocs.Search が生成するログファイルでスタックトレースを確認し、すべての Maven 依存関係が正しく解決されているかをチェックしてください。

**Q:** GroupDocs.Search はリアルタイムアプリケーションに適していますか？  
**A:** インデックス戦略（インクリメンタル更新とインメモリキャッシュ）を適切に構成すれば、ほぼリアルタイムの検索結果を提供できます。

## Resources
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [Java API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Support Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Last Updated:** 2026-02-06  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs