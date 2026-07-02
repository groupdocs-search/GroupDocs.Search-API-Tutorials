---
date: '2026-01-16'
description: JavaでGroupDocs検索ネットワークを構成し、検索効率向上のためにインデックスに同義語を追加する方法を学びましょう。
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: JavaでGroupDocs.Searchネットワークを構成する – 検索をブースト
type: docs
url: /ja/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# JavaでGroupDocs.Searchネットワークを設定する – Boost Search

今日のデータ駆動型アプリケーションでは、**configure groupdocs search network** が大量のドキュメントコレクションに対して高速かつ正確な結果を提供するための重要なステップです。エンタープライズ規模の検索ポータルを構築する場合でも、既存ソリューションを拡張する場合でも、適切に構成された GroupDocs.Search ネットワークにより、水平スケーリング、同義語サポートの追加、レイテンシの低減が可能になります。このチュートリアルでは、Java を使用して GroupDocs.Search ネットワークをセットアップ、デプロイ、微調整する方法と、インデックスに同義語を追加しノードのライフサイクルを管理する実践的なヒントを学びます。

## よくある質問
- **GroupDocs.Search ネットワークを構成する主なメリットは何ですか？**分散インデックス作成とクエリ実行が可能になり、パフォーマンスとスケーラビリティが向上します。
- **サンプルを実行するにはライセンスが必要ですか？**開発環境では無料トライアル版で十分ですが、本番環境では商用ライセンスが必要です。
- **インデックスを再構築せずに同義語を追加できますか？**はい。実行時に同義語辞書を使用して、**インデックスに同義語を追加**できます。
- **ノードはいくつまでデプロイできますか？**インフラストラクチャの許容範囲内で、必要な数のノードをデプロイできます。各ノードは独自のポートで動作します。

## GroupDocs.Search ネットワークを構成するとは？

GroupDocs.Search ネットワークを構成するとは、複数の JVM インスタンスが連携してインデックス作成と検索を実行できるように、フォルダ構造、ポート、ノード設定を定義することです。この設定により、ワーカー (シャード) を調整し、クエリがデータセット全体で実行されるようにするマスターノードが作成されます。

## GroupDocs.Search ネットワークを構成する理由

- **スケーラビリティ** – インデックス作成負荷を複数のマシンに分散します。
- **信頼性** – ダウンタイムなしでノードを追加または削除できます。
- **検索関連性** – インデックスに同義語を追加することで、より豊富な検索結果が得られます。
- **パフォーマンス** – 並列クエリ実行により、応答時間を短縮します。

## 前提条件
- Java Development Kit (JDK) 8 以降
- プロジェクトのビルドには Maven を使用します
- Java 構文の基本的な知識
- GroupDocs.Search for Java ライブラリへのアクセス (Maven または公式リリース ページからダウンロード)

## GroupDocs.Search for Java のセットアップ

Maven の **pom.xml** にリポジトリと依存関係を追加します。

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

または、[GroupDocs.Javaリリース検索](https://releases.groupdocs.com/search/java/)から最新バージョンを直接ダウンロードしてください。

### ライセンスの取得
- **無料トライアル** – コア機能を無料で試用できます。
- **一時ライセンス** – 短期テスト用にすべての機能を利用できます。
- **商用ライセンス** – 本番環境へのデプロイには必須です。

### 基本的な初期化とセットアップ
ライブラリが正しくロードされることを確認するために、簡単なJavaクラスを作成してください。

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## GroupDocs.Searchネットワークの設定手順

### 1. 検索ネットワークの設定
ノード間の通信に使用するベースドキュメントフォルダと開始ポートを定義します。

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – 辞書（例：同義語ファイル）が格納されている場所。
- **basePort** – 最初のポート番号。以降のノードはこの値からインクリメントされます。

### 2. 検索ネットワークノードのデプロイ
同じ構成を共有する複数のワーカーノードを起動します。

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

各ノードはそれぞれ固有のポート（basePort+index）で動作し、全体インデックスのシャードを保持します。

### 3. ノードイベントの購読
マスターノードにイベントリスナーをアタッチすることで、ノードの状態、インデックス作成の進捗状況、およびエラー状態を監視できます。

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

イベントコールバックを使用すると、ノードの起動/停止、インデックス作成の完了、予期しないエラーなどに対応できます。

### 4. ノードのインデクサーへの同義語の追加
実行時にインデックスに同義語を追加することで、関連性を高めることができます。

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – 同等のものとして扱うべき用語の配列。

- **clearBeforeAdding** – 既存のエントリを置き換える場合は `true` に設定してください。

### 5. インデックス作成用ディレクトリの追加
マスターノードに、検索対象とするドキュメントが含まれているフォルダを指定します。

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

このメソッドはディレクトリを再帰的にスキャンし、ファイルをシャード全体に分散します。

### 6. ネットワーク内でのテキスト検索
すべてのノードに対してクエリを実行し、必要に応じて完全一致動作を強制します。

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

ステミングなしで厳密な用語一致が必要な場合は、`exactMatchOnly` を `true` に切り替えてください。

### 7. ネットワークノードの終了
処理が完了したら、リソースを適切に解放します。

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

適切なシャットダウンはメモリリークを防ぎ、JVMを健全な状態に保ちます。

## 実践的な応用例
| シナリオ | ネットワークの活用方法 |

|----------|-----------------------|

| **エンタープライズ検索** | ペタバイト規模のコーパスに対して、データセンターのサーバー間でインデックス作成を分散します。 |
| **ドキュメント管理** | インデックスに同義語を追加することで、ユーザーは用語が異なるドキュメントでも検索できるようになります。 |
| **Eコマースカタログ** | 地域固有のノードをデプロイすることで、ローカライズされた製品検索を迅速に提供します。 |
| **コンテンツ管理** | 編集者が特定のディレクトリに新しいファイルを追加している間も、コンテンツの検索可能性を維持します。 |

## よくある問題と解決策
- **ポートの競合** – 各ノードのポート（basePort+index）が空いていることを確認し、必要に応じて`basePort`を調整してください。
- **同義語が適用されていません** – 用語を追加した後、`indexer.setDictionary(dictionary)` を呼び出したことを確認してください。
- **ノードが応答していません** – イベントを購読し、`NodeFailed` コールバックを探してネットワークの問題を診断してください。
- **クローズ時のメモリリーク** – デプロイされたすべてのノードで、必ず `node.close()` を呼び出してください。

## よくある質問

**Q: 複数のノードをデプロイすると、検索パフォーマンスはどのように向上しますか？** 
A: 各ノードはデータのシャードをインデックス化するため、ワークロードが共有され、並列処理が可能になり、クエリのレイテンシが削減されます。

**Q: 既存のドキュメントを再インデックス化せずに同義語を追加できますか？** 
A: はい、実行時に同義語辞書を使用してインデックスに同義語を追加できます。変更は新しいクエリに即座に反映されます。


**Q: ノードイベントの購読は必須ですか？** 
A: 基本的な操作には必須ではありませんが、イベントを購読することでノードの状態を把握し、障害発生時に迅速に対応できます。

**Q: ノードリソース管理のベストプラクティスは何ですか？** 
A: アイドル状態のノードを定期的にシャットダウンし、JVMメモリ使用量を監視し、リソース消費を最適化するために、ピーク時以外の時間帯にノードを再起動してください。

**Q: GroupDocs.SearchはPDFや画像などの非テキスト形式をサポートしていますか？** 
A: はい、もちろんです。このライブラリはPDFやOfficeファイルからテキストを抽出し、画像に対してもOCR処理を実行するため、すぐに検索可能です。

---

**最終更新日:** 2026年1月16日
**テスト環境:** GroupDocs.Search 25.4 (Java版)
**作成者:** GroupDocs