---
date: '2026-07-02'
description: GroupDocs.Search の一時ライセンス取得方法、インデックスにディレクトリを追加し、カスタム文書属性を追加する手順を学びながら、Java
  検索ネットワークノードを管理します。
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: GroupDocs の一時ライセンスを取得 – マスター検索ノード (Java)
type: docs
url: /ja/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# 一時ライセンスの取得 GroupDocs – マスタ検索ノード (Java)

この包括的なガイドでは、**GroupDocs.Search の一時ライセンスを取得**し、マルチノード検索ネットワークを構成し、Java を使用して **インデックスにディレクトリを追加** および **カスタムドキュメント属性を追加** する方法を学びます。エンタープライズ文書管理システムや検索可能な製品カタログを構築する場合でも、これらの手順を習得すれば、制限なくプラットフォームを評価し、検索機能を迅速にスケールできます。

## クイック回答
- **GroupDocs.Search の使用を開始する最初のステップは何ですか？** GroupDocs ポータルから一時ライセンスを取得します。  
- **ライブラリをホストしている Maven リポジトリはどれですか？** `https://releases.groupdocs.com/search/java/`。  
- **インデックスにディレクトリを追加するにはどうすればよいですか？** マスターノードで `addDirectoriesToIndex` ヘルパーを呼び出します。  
- **カスタムドキュメント属性を追加できますか？** はい—ドキュメントキーと属性名を指定して `addAttribute` を呼び出します。  
- **ノードを安全にシャットダウンするには？** `closeNodes` を呼び出してリソースを解放します。

## 一時ライセンスとは何か、なぜ必要なのか
一時ライセンスは、評価制限なしで GroupDocs.Search を評価できるようにします。開発、テスト、概念実証プロジェクトに最適で、フル購入前に製品を試すことができます。ライセンスは限定期間のフル機能アクセスを提供し、パフォーマンスのベンチマーク、統合ポイントのテスト、要件適合性の確認を金銭的コミットメントなしで行えます。

## 前提条件

開始する前に、以下の前提条件が整っていることを確認してください。

### 必要なライブラリと依存関係
GroupDocs.Search for Java を使用するには、必要な Maven 依存関係を含めます:
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
また、最新バージョンは [GroupDocs.Search for Java リリース](https://releases.groupdocs.com/search/java/) から直接ダウンロードできます。

### 環境設定
- 互換性のある JDK（Java 8 以降）がインストールされていることを確認してください。  
- IDE を Maven プロジェクトに対応させて設定してください。

### 知識の前提条件
Java プログラミングの基本的な理解と Maven プロジェクト管理の知識があると役立ちます。これらの概念に不慣れな場合は、入門リソースを参照して始めてください。

## 一時ライセンスの取得方法
一時ライセンスは GroupDocs ポータルにアクセスし、短いリクエストフォームに記入し、受領した `.lic` ファイルをプロジェクトの `resources` フォルダーに配置して取得します。その後、数行のコードでライセンスを初期化します（以下のスニペット参照）。リクエストフォームは公式ページ [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) を使用してください。

## GroupDocs.Search for Java の設定

### インストール情報
プロジェクトで GroupDocs.Search for Java を使用し始めるには、上記の Maven 手順に従うか、公式リリースページから最新バージョンを直接ダウンロードしてください。

#### ライセンス取得手順
1. **無料トライアル** – 何のコミットメントもなく機能を試すことができます。  
2. **一時ライセンス** – テスト用の短期キーを取得します（上記セクション参照）。  
3. **購入** – 本番利用のために、**[GroupDocs 購入ページ](https://purchase.groupdocs.com/)** からフルライセンスを購入してください。

### 基本的な初期化と設定
GroupDocs.Search を使用してプロジェクトを次のように初期化します:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
この初期化手順は、検索ネットワーク内のすべてのコンポーネントがシームレスに機能するために重要です。

## 実装ガイド
それでは、プロセスを管理しやすいセクションに分割し、検索ネットワークノードのデプロイと管理に関する特定の機能に焦点を当てて説明します。

### 機能 1: 設定のセットアップ
**概要:** 検索ネットワークの設定を行うことは、ノードをデプロイする際の最初のステップです。この設定では、ノードデプロイに重要なパスとポートを指定します。

#### 実装手順:
##### 手順 1: ベースパスとポートの定義
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### 手順 2: 検索ネットワークの構成
`configureSearchNetwork` 関数は、ノードをデプロイするために必要な設定オブジェクトを準備します。  
`Configuration` は、インデックスフォルダー、ネットワークポート、ノードロールなどのすべての設定を保持するクラスです。  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **パラメータ:** ベースパスとポートはリソースの場所特定と通信チャネルの確立に使用されます。  
- **戻り値:** デプロイ要件に合わせて構成された `Configuration` オブジェクトです。

### 機能 2: 検索ネットワークのデプロイ
**概要:** ノードをデプロイすることは、さまざまな環境やデータセグメントにわたって検索機能をスケールさせるために不可欠です。

#### 実装手順:
##### 手順 1: ノードのデプロイ
`deploySearchNetwork` 関数は検索ネットワークノードの配列を初期化して返します。  
`SearchNetworkNodes` は、分散検索クラスターに参加する各ノードインスタンスを表します。  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **パラメータ:** ベースパス、ポート、設定はデプロイ環境の決定に使用されます。  
- **戻り値:** 初期化された `SearchNetworkNodes` の配列です。

### 機能 3: ネットワークイベントへのサブスクライブ
**概要:** 検索ネットワークの活動を監視することは、最適なパフォーマンスと信頼性を維持するために重要です。

#### 実装手順:
##### 手順 1: マスターノードイベントへのサブスクライブ
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **目的:** この手順により、検索ネットワーク内の重要なイベントや変更が通知されます。

### 機能 4: ドキュメントのインデックス作成
**概要:** インデックス対象のドキュメントを含むディレクトリを追加することで、ネットワーク全体で効率的なデータ取得が可能になります。

#### ディレクトリをインデックスに追加する方法
`addDirectoriesToIndex` は、マスターノード上でインデックス作成対象のフォルダーパスを登録するヘルパーメソッドです。  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **目的:** 指定されたディレクトリ内のすべてのドキュメントへの迅速なアクセスと検索性を実現します。

### 機能 5: ドキュメントへの属性追加
**概要:** カスタム属性はドキュメントメタデータを強化し、検索をより柔軟かつ情報豊かにします。

#### カスタムドキュメント属性を追加する方法
`addAttribute` は、インデックス内の特定ドキュメントにカスタムメタデータ属性を追加します。  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **パラメータ:** ノード、ドキュメントキー、追加する属性を指定します。  
- **目的:** 追加のメタデータでドキュメントを強化し、検索機能を拡張します。

### 機能 6: インデックス化されたドキュメントの取得
**概要:** インデックス化されたドキュメントを効率的に取得・一覧表示し、データの正確性と完全性を確保します。

#### 実装手順:
##### 手順 1: インデックス化されたドキュメントの取得
```java
getIndexedDocuments(nodes[0]);
```  
- **目的:** 検索ネットワーク内のすべての必要なドキュメントが正常にインデックス化されたことを確認します。

### 機能 7: ネットワークノードのクローズ
**概要:** ノードを適切にクローズすることは、リソース管理とメモリリーク防止に不可欠です。

#### 実装手順:
##### 手順 1: すべてのノードをクローズ
`closeNodes` はすべてのアクティブな検索ノードをシャットダウンし、割り当てられたリソースを解放します。  
```java
closeNodes(nodes);
```  
- **目的:** 各ノードが占有しているリソースを解放し、クリーンなシャットダウンプロセスを保証します。

## GroupDocs.Search で一時ライセンスを使用する理由
一時ライセンスは **30 日間のフル機能アクセス** を提供し、**50,000 件までのインデックス化ドキュメント** をパフォーマンス制限なしでサポートします。これにより、実運用データでインデックス速度、クエリ遅延、スケーラビリティを本番ライセンス購入前にベンチマークできます。また、評価用の透かしが除去され、最終製品の実際の機能を正確に把握できます。

## 一般的なユースケース
1. **エンタープライズ文書管理** – 部門横断で数百万の内部ファイルをインデックスし、瞬時の全文検索を実現します。  
2. **Eコマースプラットフォーム** – 複数の倉庫やサードパーティフィードにまたがる検索可能な製品カタログを構築します。  
3. **法律事務所** – カスタムメタデータでケースファイル、契約書、証拠を整理し、迅速に検索できるようにします。

他システムとの統合例としては、CRM プラットフォーム、コンテンツ管理システム（CMS）、データ分析ツールなどがあり、GroupDocs.Search for Java が提供する堅牢なインデックス・検索機能を活用できます。

## パフォーマンス上の考慮点
GroupDocs.Search for Java を使用する際のパフォーマンス最適化ポイント:
- **設定の最適化** – デプロイ環境に合わせて設定を調整します。  
- **リソース使用状況の監視** – CPU、メモリ、I/O を定期的にチェックし、ボトルネックやメモリリークを防止します。  
- **ベストプラクティスの遵守** – Java のメモリ管理ガイドラインに従い、システムリソースを効率的に活用します。

## よくある質問

**Q: 一時ライセンスの有効期間はどれくらいですか？**  
A: 一時ライセンスは通常 30 日間有効で、製品を十分に評価できる時間が確保されています。

**Q: 再インストールせずに一時ライセンスからフルライセンスへ切り替えられますか？**  
A: はい—一時ライセンスファイルをフルライセンスファイルに置き換え、アプリケーションを再起動するだけです。

**Q: 新しいライセンスを適用した後、ドキュメントを再インデックスする必要がありますか？**  
A: いいえ、インデックスはそのまま保持されます。ライセンスは使用権のみを管理します。

**Q: ノードのクローズを忘れるとどうなりますか？**  
A: リソースが解放されずメモリリークにつながる可能性があります。シャットダウン時は必ず `closeNodes` を呼び出してください。

**Q: 1 つのドキュメントに複数のカスタム属性を追加できますか？**  
A: もちろんです—異なる属性名で `addAttribute` を複数回呼び出せば可能です。

---

**最終更新:** 2026-07-02  
**テスト環境:** GroupDocs.Search for Java 25.4  
**作者:** GroupDocs

## 関連チュートリアル

- [GroupDocs を使用した .NET の検索ネットワークノードのデプロイと効率的な文書インデックス作成と取得](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [ドキュメント管理システム向けに .NET で GroupDocs.Search を使用した検索ネットワークの実装方法](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Aspose.Search ネットワークの構成と .NET 用 GroupDocs.Redaction でのドキュメント属性追加: 包括的ガイド](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)