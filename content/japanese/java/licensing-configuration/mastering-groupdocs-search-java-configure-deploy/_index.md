---
date: '2026-05-02'
description: GroupDocs.Search for Java を使用して検索の設定方法とリアルタイム検索更新の有効化方法を学びましょう。ネットワーク設定、ノード展開、インデックス作成に関するステップバイステップガイドです。
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: JavaでGroupDocs.Searchを使用した検索の設定方法 - 構成と展開ガイド
type: docs
url: /ja/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# GroupDocs.Search を使用した Java の検索設定方法

## クイック回答
- **検索ネットワークの主な目的は何ですか？** スケーラビリティと速度のために、インデックス作成とクエリ処理を複数のノードに分散させることです。  
- **必要なライブラリのバージョンは？** GroupDocs.Search for Java v25.4 以上です。  
- **ライセンスは必要ですか？** 評価には無料トライアルで十分ですが、本番環境では商用ライセンスが必要です。  
- **リアルタイム更新はどのように処理されますか？** インデックス変更時に発生するノードイベントを購読することで行われます。  
- **新しいドキュメントフォルダーを動的に追加できますか？** はい—インデクサの `addDirectories` メソッドを使用します。

## GroupDocs のコンテキストで「検索の設定方法」とは何ですか？
検索を設定することは、ドキュメントの所在、ノード間の通信方法、インデックス作成の調整方法を把握した **検索ネットワーク** を構築することを意味します。ネットワークが構成されれば、ダウンタイムなしでノードの追加や削除が可能になり、常に最新の検索結果に継続的にアクセスできます。

## なぜ Java 用 GroupDocs.Search を使用するのか？
- **スケーラビリティ:** 複数のマシンにワークロードを分散します。  
- **リアルタイム更新:** 新しくインデックスされたファイルをネットワーク全体に即座に反映します。  
- **統合の容易さ:** シンプルな Maven 設定と明快な Java API を提供します。  
- **エンタープライズ対応:** 大規模コーパスや複雑なクエリシナリオに対応します。

## 前提条件
- **Java Development Kit (JDK) 8+** がインストールされていること。  
- **Maven** が依存関係管理に使用できること。  
- Java、Maven、検索概念に関する基本的な知識があること。

## GroupDocs.Search for Java の設定

### Maven 依存関係
`pom.xml` にリポジトリと依存関係を追加します:

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

**直接ダウンロード:** ライブラリは [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) からも取得できます。

### ライセンス取得
- **無料トライアル:** すべての機能を試すためのトライアルライセンスを取得します。  
- **一時ライセンス:** 評価期間延長のためにリクエストします。  
- **商用ライセンス:** 本番環境でのデプロイには必要です。

### 基本的な初期化
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Java で検索ネットワークを設定する方法

### 手順 1: 必要なパッケージをインポート
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### 手順 2: ネットワークを構成
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **パラメータ:** `basePath` はドキュメントフォルダーへのパスを指し、`basePort` はノード間通信に使用される TCP ポートです。

## 検索ネットワークノードのデプロイ

### 手順 1: デプロイパッケージをインポート
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### 手順 2: ノードをデプロイ
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **マスターノード:** すべてのノードで検索とインデックス作成を調整します。**マスターノード** の設定（シャード割り当てやヘルスチェックなど）を構成できます。

## リアルタイム検索更新のためのノードイベント購読

### 手順 1: イベントパッケージをインポート
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### 手順 2: マスターノードイベントを購読
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **イベントハンドリング:** ドキュメントが追加、更新、削除されるたびに **リアルタイム検索更新** を有効にします。

## インデックス作成用ディレクトリの追加

### 手順 1: インデクサーパッケージをインポート
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### 手順 2: ドキュメントディレクトリを追加
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **動的インデックス作成:** `addDirectories` メソッドを使用して、ネットワークを再起動せずに **ディレクトリをインデックスに追加** できます。

## インデックス化されたドキュメントの取得

### 手順 1: サーチャーパッケージをインポート
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### 手順 2: ドキュメント情報を取得
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **シャード管理:** ドキュメントをシャードに分散させることで大規模データセットを効率的に処理します。**シャードサイズを最適化**するには、シャード統計を監視し、将来のリリースで `shardSize` 設定を調整します。

## なぜこれがプロジェクトに重要なのか
適切に構成された検索ネットワークはボトルネックを排除し、レイテンシを低減し、ユーザーが常に最新バージョンのドキュメントを閲覧できるようにします。リアルタイム更新や **インデックスにディレクトリを追加** できるダウンタイムなしの機能は、特に法律事務所、研究機関、継続的に変化するドキュメントコレクションを扱う組織にとって価値があります。

## 実用的な活用例
1. **エンタープライズ文書管理:** 数百万のファイルに対して検索を集中化します。  
2. **法律事務所:** ケースファイル、契約書、証拠資料を迅速に検索します。  
3. **学術研究:** ジャーナルや論文をインデックス化し、即座に取得できるようにします。

## パフォーマンス上の考慮点
- **インデックス最適化:** 定期的なインデックスリフレッシュと古いデータの削除をスケジュールします。  
- **メモリ管理:** 特に大きなシャードを扱う際は JVM ヒープを監視します。  
- **スケーラビリティ計画:** コーパスが増加するにつれてノードを追加し、ネットワークが自動的に負荷を均衡させます。  
- **シャードサイズの最適化:** 小さいシャードはクエリ遅延を改善し、大きいシャードはオーバーヘッドを削減します。ハードウェアとクエリパターンに基づいて調整してください。

## よくある問題と解決策
| 問題 | 原因 | 対策 |
|-------|-------|-----|
| ノードが接続できない | ポート競合またはファイアウォール | `basePort` が開いていて他のサービスで使用されていないことを確認してください |
| インデックスが更新されない | イベント購読が欠如している | デプロイ後に `SearchNetworkNodeEvents.subscribe(masterNode)` を呼び出してください |
| メモリ不足エラー | 大量の大きなシャードがロードされている | シャードサイズを減らすか、JVM ヒープ（`-Xmx` フラグ）を増やしてください |

## よくある質問

**Q: ネットワーク稼働中に新しいディレクトリを追加できますか？**  
A: はい—`indexer.addDirectories()` メソッドを使用してください。購読されたイベントがリアルタイムで更新を伝搬します。

**Q: ノードのヘルスをどのように監視しますか？**  
A: 各 `SearchNetworkNode` がステータス API を提供します。お好みの監視ツールと統合してください。

**Q: マスターノードを別のマシンで実行できますか？**  
A: もちろんです。すべてのノードが同じ `basePort` を共有し、ネットワーク上で相互に到達可能であることを確認してください。

**Q: 対応しているファイル形式は何ですか？**  
A: GroupDocs.Search は PDF、Word、Excel、PowerPoint、プレーンテキストなど多数の形式を標準でサポートしています。

**Q: 新しいノードを追加した後にネットワークを再起動する必要がありますか？**  
A: いいえ—ノードは動的に追加・削除でき、マスターノードが自動的にシャードを再バランスします。

## 結論
これで、GroupDocs.Search for Java を使用した **検索の設定方法** が分かりましたので、組織の成長に合わせて高速でスケーラブル、かつ信頼性の高い文書検索ソリューションを構築できます。これらのパターンを適用して、あらゆる業界向けのリアルタイムで分散型の検索体験を実現してください。

---

**最終更新日:** 2026-05-02  
**テスト環境:** GroupDocs.Search for Java 25.4  
**作者:** GroupDocs