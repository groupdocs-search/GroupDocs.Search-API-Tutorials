---
date: '2025-12-19'
description: GroupDocs.Search を使用して Java でドキュメントをインデックスに追加し、チャンクベースの検索を有効にする方法を学び、大規模なドキュメントセットのパフォーマンスを向上させましょう。
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Javaでチャンクベース検索を使用してドキュメントをインデックスに追加する
type: docs
url: /ja/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Javaでチャンクベース検索を使用してインデックスにドキュメントを追加する

今日のデータ駆動型の世界では、**インデックスにドキュメントを追加**することを迅速に行い、その後チャンクベースの検索を実行できることが、大量のファイルコレクションを扱うあらゆるアプリケーションにとって不可欠です。法的契約書、カスタマーサポートのアーカイブ、膨大な研究ライブラリなど、どのようなシナリオでも、本チュートリアルでは GroupDocs.Search for Java を設定し、ドキュメントを効率的にインデックス化し、サイズの小さなチャンクで関連情報を取得する方法を詳しく解説します。

## 学べること
- 指定フォルダーに検索インデックスを作成する方法。  
- 複数の場所から **インデックスにドキュメントを追加**する手順。  
- チャンクベース検索を有効にする検索オプションの設定方法。  
- 初回および以降のチャンクベース検索の実行方法。  
- チャンクベースドキュメント検索が有効に機能する実践シナリオ。

## クイック回答
- **最初のステップは何ですか？** 検索インデックスフォルダーを作成します。  
- **多数のファイルを含めるには？** 各ドキュメントフォルダーに対して `index.add()` を使用します。  
- **どのオプションがチャンク検索を有効にしますか？** `options.setChunkSearch(true)`。  
- **最初のチャンクの後も検索を続けられますか？** はい、トークンを渡して `index.searchNext()` を呼び出します。  
- **ライセンスは必要ですか？** 開発用には無料トライアルまたは一時ライセンスで十分ですが、本番環境ではフルライセンスが必要です。

## 前提条件
このガイドを実行するには、以下を確認してください。

- **必須ライブラリ**：GroupDocs.Search for Java 25.4 以降。  
- **環境設定**：互換性のある Java Development Kit (JDK) がインストールされていること。  
- **知識の前提**：基本的な Java プログラミングと Maven の知識。

## GroupDocs.Search for Java のセットアップ
まず、Maven を使用してプロジェクトに GroupDocs.Search を統合します。

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
GroupDocs.Search を試す方法:

- **無料トライアル** – コア機能を制約なくテストできます。  
- **一時ライセンス** – 開発期間中の拡張アクセスが可能です。  
- **購入** – 本番環境でのフルライセンス。

### 基本的な初期化と設定
検索可能データを格納するフォルダーにインデックスを作成します。

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

## インデックスにドキュメントを追加する方法
インデックスが作成されたら、次の論理的ステップは **インデックスにドキュメントを追加** し、ファイルが保存されている場所から取り込むことです。

### 1. インデックスの作成
**概要**: 検索インデックス用のディレクトリーを設定します。

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. インデックスにドキュメントを追加
**概要**: 複数のソースフォルダーからファイルを取り込みます。

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

### 3. チャンク検索用の検索オプション設定
オプションオブジェクトを調整してチャンクベース検索を有効にします。

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. 初回チャンクベース検索の実行
チャンク対応オプションを使用して最初のクエリを実行します。

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. チャンクベース検索の継続
検索が完了するまで残りのチャンクを反復処理します。

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## なぜチャンクベース検索を使うのか？
チャンクベース検索は、巨大なドキュメントコレクションを管理しやすいサイズに分割し、メモリ負荷を軽減しながら応答時間を短縮します。特に次のようなケースで有効です。

1. **法務チーム** が何千もの契約書から特定の条項を探し出す必要がある場合。  
2. **カスタマーサポートポータル** が関連するナレッジベース記事を瞬時に提示する必要がある場合。  
3. **研究者** が膨大なデータセットを、ファイル全体をメモリにロードせずに検索したい場合。

## パフォーマンス上の考慮点
- **メモリ管理** – 大規模インデックス用に十分なヒープ領域（`-Xmx`）を割り当てます。  
- **リソース監視** – インデックス作成および検索時の CPU 使用率に注意します。  
- **インデックスの保守** – 定期的にインデックスを再構築またはクリーンアップし、古いデータを除去します。

## よくある落とし穴とトラブルシューティング
| 問題 | 発生理由 | 対策 |
|------|----------|------|
| `OutOfMemoryError` がインデックス作成中に発生 | ヒープサイズが不足 | JVM ヒープを増やす（例：`-Xmx2g` 以上） |
| 結果が返ってこない | チャンクトークンが処理されていない | `while` ループが `getNextChunkSearchToken()` が `null` になるまで実行されていることを確認 |
| 検索が遅い | インデックスが最適化されていない | バルク追加後に `index.optimize()` を実行 |

## FAQ（よくある質問）

**Q: チャンクベース検索とは何ですか？**  
A: データセットを小さなピースに分割し、ドキュメント全体をメモリにロードせずに大規模データに対して効率的にクエリを実行できる検索方式です。

**Q: 新しいファイルでインデックスを更新するには？**  
A: 新規ドキュメントへのパスを指定して `index.add()` を呼び出すだけで、インデックスに自動的に取り込まれます。

**Q: GroupDocs.Search はさまざまなファイル形式に対応していますか？**  
A: はい、PDF、DOCX、XLSX、PPTX など多数の一般的なフォーマットをサポートしています。

**Q: 主なパフォーマンスボトルネックは何ですか？**  
A: メモリ制約と最適化されていないインデックスが最も一般的です。十分なヒープを確保し、定期的にインデックスを最適化してください。

**Q: 詳細なドキュメントはどこで確認できますか？**  
A: 公式の [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) で、深掘りガイドや API リファレンスが提供されています。

## リソース
- **ドキュメント**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API リファレンス**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **ダウンロード**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **無料サポート**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **一時ライセンス取得**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最終更新日:** 2025-12-19  
**テスト環境:** GroupDocs.Search 25.4 for Java  
**作成者:** GroupDocs  

---