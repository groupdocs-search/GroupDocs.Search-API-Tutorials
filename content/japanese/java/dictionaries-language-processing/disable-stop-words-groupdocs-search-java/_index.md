---
date: '2026-02-19'
description: GroupDocs.Search for Java を使用して検索時のストップワードを無効にし、ドキュメントをインデックスに追加して、クエリの精度を向上させる方法を学びましょう。
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 検索におけるストップワード：GroupDocs.Search Javaでドキュメントをインデックスに追加
type: docs
url: /ja/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# 検索におけるストップワード: GroupDocs.Search Javaでインデックスにドキュメントを追加

重要な用語（特に一般的なもの）が無視されないように **add documents to index** したい場合は、ここが最適です。このガイドでは GroupDocs.Search for Java を使用して **disable stop words in search** の方法を示します。これにより、すべてのトークン（「on」や「by」や「the」さえも）が検索可能になり、結果が格段に正確になります。

## Quick Answers
- **“add documents to index” とは何ですか？** ソースファイルを検索可能なインデックスにロードし、効率的にクエリできるようにすることです。  
- **なぜストップワードを無効にするのですか？** ドメイン固有で重要な意味を持つ一般的な単語（例: “on”, “the”）を検索に含めるためです。  
- **必要なライブラリのバージョンは？** GroupDocs.Search for Java 25.4 以降。  
- **ライセンスは必要ですか？** 評価用の無料トライアルは利用可能です。製品環境では永続ライセンスが必要です。  
- **Maven プロジェクトで使用できますか？** はい – 下記のリポジトリと依存関係を追加するだけです。

## What are stop words in search and why might you want to disable them?
ストップワードは検索エンジンがクエリの高速化のために自動的に除外する頻出語です。汎用ウェブ検索ではパフォーマンス向上に寄与しますが、法務契約書、e‑コマースカタログ、技術マニュアルなどの専門領域では「on」や「by」や「as」などが実質的な意味を持つため、精度が低下します。ストップワードを無効化すると、すべての単語を重要とみなすことができ、関連ドキュメントが見逃されません。

## How does adding documents to index work in GroupDocs.Search?
ドキュメントを追加すると、ライブラリは各ファイルを読み取り、内容をトークン化し、最適化されたデータ構造（インデックス）にトークンを格納します。インデックス化が完了すれば、エンジンは大規模コレクションでもミリ秒単位で一致するドキュメントを取得できます。

## Prerequisites

- **必須ライブラリ**: GroupDocs.Search for Java 25.4（またはそれ以降）。  
- **開発環境**: IntelliJ IDEA、Eclipse、またはお好みの Java IDE。  
- **基本知識**: Java の構文とインデックス概念に慣れていること。

## Setting Up GroupDocs.Search for Java

### Maven Installation

Maven を使用している場合は、`pom.xml` に以下を追加してください。

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

### Direct Download

あるいは、[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) から最新バージョンをダウンロードします。

#### License Acquisition Steps
- **Free Trial** – すぐにテストを開始できます。  
- **Temporary License** – フル機能を一定期間利用できるキーを取得します。  
- **Purchase** – 本番環境向けに永続ライセンスを取得します。

## Basic Initialization and Setup

インデックスの動作を制御するために `IndexSettings` のインスタンスを作成します。

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## How to disable stop words in search (Java)

組み込みのストップワードフィルタをオフにするには、次の行を使用します。

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parameters*: `setUseStopWords` はブール値を受け取ります。  
*Purpose*: 一般的なストップワードを含むすべての単語がインデックス化され、検索可能になることを保証します。

## How to add documents to index

### Defining the Output Directory

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Specifying the Document Directory

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

これで `YOUR_DOCUMENT_DIRECTORY` 内のすべてのファイルが **add documents to index** され、クエリ実行の準備が整います。

## Performing a Search Query

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

ストップワードが無効化されているため、検索語句 `"on"` も検索対象となり、通常は無視されるマッチが返されます。

## Practical Applications

1. **Enterprise Document Search** – 重要な用語がフィルタリングされないようにします。  
2. **E‑commerce Platforms** – 商品説明のすべての単語をインデックス化し、製品発見を向上させます。  
3. **Legal Research Tools** – 法的文書において、一般的にストップワードとみなされる語句もすべて捕捉します。

## Performance Considerations

- **Optimization Tips**: インデックスは定期的に更新・削除して、検索速度を高く保ちます。  
- **Resource Usage**: JVM ヒープサイズを監視してください。大規模インデックスではガベージコレクション設定の調整が必要になることがあります。  
- **Java Memory Management**: 効率的なデータ構造を使用し、非常に大きなコーパスの場合はオフヒープストレージの導入も検討してください。

## Common Issues and Solutions

| Symptom | Likely Cause | Fix |
|---|---|---|
| No results for common words | `setUseStopWords(true)`（デフォルト） | 上記のように `setUseStopWords(false)` を呼び出す。 |
| Out‑of‑memory errors during indexing | 一度に大量の大きなファイルをインデックス化している | バッチ処理でファイルを分割し、`-Xmx` JVM オプションでヒープを増やす。 |
| Search returns stale data | ドキュメント追加後にインデックスが更新されていない | `index.update()` を呼び出すか、変更されたドキュメントを再追加する。 |

## Frequently Asked Questions

**Q: What are stop words?**  
A: ストップワードは多くの検索エンジンがクエリ高速化のために無視する一般的な語（例: “the”, “is”, “on”）です。無効化すると、すべてのトークンが検索対象になります。

**Q: Why disable stop words in search indexes?**  
A: 正確なフレーズマッチが必要な法務・技術文書などでは、すべての単語が意味を持つため、ストップワードを含める必要があります。

**Q: How does GroupDocs.Search handle large datasets?**  
A: ライブラリは最適化されたデータ構造とインクリメンタルインデックスを使用し、数百万件のドキュメントでもメモリ使用量を抑えます。

**Q: Can I integrate GroupDocs.Search with other Java applications?**  
A: はい。API は Web サービスからデスクトップアプリまで、あらゆる Java ベースのシステムに簡単に組み込めるよう設計されています。

**Q: What should I do if my search results are not accurate?**  
A: インデックスにすべての必要なドキュメントが含まれているか（`add documents to index`）を確認し、必要に応じてストップワードフィルタが無効化されているかをチェックしてください。大幅な変更後はインデックスの再構築も検討してください。

## Additional Resources

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

このガイドに従えば、**add documents to index** と **disable stop words in search** の方法が分かり、Java アプリケーションでより正確な検索結果を提供できるようになります。

---

**Last Updated:** 2026-02-19  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs