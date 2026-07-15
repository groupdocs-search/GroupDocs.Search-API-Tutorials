---
date: '2026-06-12'
description: GroupDocs.Search と GroupDocs.Redaction を使用して、.NET で検索インデックスを作成し、PDF に対してレダクションを適用する方法を学びます。セットアップ、デプロイ、インデックス作成、そして高度な検索について解説しています。
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: GroupDocs Search と GroupDocs.Redaction を使用した .NET の検索インデックス作成 – 包括的ガイド
type: docs
url: /ja/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# GroupDocs Search と Redaction を使用した .NET の検索インデックス作成 – 包括的ガイド

今日のデジタル環境では、情報を迅速に検索でき、機密データを保護できる **search index .NET** ソリューションの作成は、あらゆる組織にとって最優先事項です。このチュートリアルでは、スケーラブルな GroupDocs.Search ネットワークの構成、ノードのデプロイ、ドキュメントのインデックス作成、そして GroupDocs.Redaction を使用した **PDF へのレダクション適用** の手順を、.NET 環境内で解説します。

## クイック回答
- **search index .NET を作成する最初のステップは何ですか？** ベースパスとポートを定義し、ネットワークノードをデプロイします。  
- **GroupDocs で PDF にレダクションを適用するにはどうすればよいですか？** `Redactor` インスタンスを初期化し、PDF をロードして、目的のパターンで `Redact` を呼び出します。  
- **検索ネットワークを複数のマシンで実行できますか？** はい。ノードを別々のサーバーにデプロイし、マスターノードがインデックス作成とクエリを調整します。  
- **本番環境で使用するにはライセンスが必要ですか？** 本番環境では有効な GroupDocs ライセンスが必要です。評価用に一時的なトライアルライセンスが利用可能です。  
- **サポートされている .NET バージョンは何ですか？** .NET Framework 4.7.2 以上、.NET Core 3.1 以上、そして .NET 5/6/7 が完全にサポートされています。

## “search index .NET の作成” とは？
*search index .NET の作成* は、.NET ライブラリを使用してドキュメントのメタデータとコンテンツの検索可能なリポジトリを構築することを指します。テキストを抽出し、用語をトークン化し、最適化されたインデックス構造に保存します。これにより、分散ノード間で即時のクエリ応答が可能となり、さまざまなファイル形式をサポートし、エンタープライズアプリケーションでスケーラブルかつ高性能なドキュメント検索が実現します。

## GroupDocs Search と Redaction を組み合わせて使用する理由
GroupDocs.Search は **50 以上のファイル形式**（DOCX、PDF、PPTX、HTML など）をサポートし、ファイル全体をメモリにロードせずに数百ページに及ぶドキュメントをインデックスできます。これに、1 ページあたり 200 ms 未満で **PDF にレダクションを適用** できる GroupDocs.Redaction を組み合わせることで、セキュアで高性能なドキュメント管理パイプラインが実現します。

## 前提条件

### 必要なライブラリと依存関係
このチュートリアルを実行するには、以下のパッケージをインストールしてください。
- .NET 用 **GroupDocs.Search**
- .NET 用 **GroupDocs.Redaction**

必要なライブラリをインストールするには、次のいずれかの方法を使用できます：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
"GroupDocs.Search" と "GroupDocs.Redaction" を検索し、最新バージョンをインストールします。

### 環境設定要件
- .NET Framework 4.7.2 以上（または .NET Core 3.1 以上）
- Visual Studio IDE（Community、Professional、Enterprise のいずれか）

### 知識の前提条件
- 基本的な C# プログラミング
- オブジェクト指向の概念
- ネットワーク構成およびドキュメント管理システムに関する知識

## .NET 用 GroupDocs.Redaction の設定

### インストール情報
アプリケーションにレダクション機能を統合するには、まず GroupDocs.Redaction ライブラリを追加します。

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
"GroupDocs.Redaction" を検索し、インストールします。

### ライセンス取得
無料トライアルまたは一時ライセンスを開始するには、以下の手順に従ってください。
- [GroupDocs のウェブサイト](https://purchase.groupdocs.com/temporary-license/) にアクセスして、一時ライセンスをリクエストします。  
- 購入オプションについては、[価格ページ](https://groupdocs.com/pricing) をご覧ください。

ライセンスファイルを取得したら、アプリケーション設定で適用します：

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```

### 基本的な初期化
基本的な操作のために GroupDocs.Redaction を初期化するには、以下のコードスニペットを使用します：

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```

## 実装ガイド

### 設定構成

#### 概要
この機能は、ベースパスとポート番号を使用して検索ネットワークを構成し、ドキュメント管理システムの基盤を形成します。

#### 定義アンカー
`SearchNetworkDeployment` は、ネットワーク全体の検索ノードのデプロイを調整するクラスです。

#### 手順 1: ベースパスとポートの定義  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### 手順 2: ネットワークの構成
`Configure` メソッドを使用して、指定されたパスとポートで検索ネットワークを設定します：

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```

### ネットワークノードのデプロイ

#### 概要
構成した検索ネットワーク内にノードをデプロイし、分散ドキュメント検索を実現します。

#### 定義アンカー
`SearchNetworkNode` は、マスターノードと通信する個々の検索可能ノードを表します。

#### 手順 1: デプロイの初期化  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```

### マスターノードのイベント購読

#### 概要
マスターノードのイベントを購読して、ネットワーク操作を効果的に監視・管理します。

#### 定義アンカー
`SearchNetworkNodeEvents` は、インデックス作成、クエリ実行、エラーハンドリングのコールバックを提供します。

#### 手順 1: マスターノードの特定
マスターノードとして最初のノードを選択します：

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```

#### 手順 2: イベントの購読
以下のようにイベントを購読します：

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```

### ドキュメントのインデックス作成

#### 概要
効率的な検索操作のためにドキュメントをインデックスします。このステップは、ネットワークが必要なデータを迅速に取得できるようにするために重要です。

#### 定義アンカー
`SearchIndex` は、インデックスされた各ファイルの検索可能トークンとメタデータを格納するコアオブジェクトです。

#### 手順 1: インデックスにディレクトリを追加
ドキュメントが格納されているディレクトリを指定します：

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### 検索機能 – 基本的な使用法

#### 概要
ネットワーク内のノード間で基本的な検索操作を実行します。

#### 直接回答
マスターノードで `SearchNetwork.Query("your term")` を呼び出すと、一致するドキュメントが即座に取得できます。このメソッドは、ファイルパスと関連度スコアを含む `SearchResult` オブジェクトのコレクションを返します。  
`SearchNetwork.Query` は、ネットワーク全体に対して検索クエリを実行し、一致する結果を返すメソッドです。

#### 手順 1: 検索パラメータの定義  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```

### 高度な検索機能

#### 概要
カスタマイズ可能なパラメータを使用した高度な検索手法を活用し、より正確な結果を得ます。

#### 直接回答
`SearchOptions` オブジェクトを作成し、`UseFuzzySearch`、`Highlight`、`PageSize` プロパティを設定してから `SearchNetwork.QueryAdvanced` に渡すメソッドを実装します。これにより、ファジーマッチングが有効なページングされたハイライト結果が得られます。  
`SearchNetwork.QueryAdvanced` は、ファジーマッチングやページングなどの高度なオプションを使用してクエリを実行するメソッドです。

#### 手順 1: 高度な検索メソッドの実装  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```

### PDF ファイルへのレダクション適用

#### 概要
保存または共有する前に PDF コンテンツをレダクションして、機密情報を保護します。

#### 直接回答
`Redactor` インスタンスを作成し、対象の PDF をロードし、`RedactionPattern`（例: SSN の正規表現）を定義して `redactor.Apply(pattern)` を呼び出し、最後にレダクションされたドキュメントを保存します。このプロセスにより、個人データが永久に削除されます。

#### 定義アンカー
`Redactor` は、GroupDocs.Redaction におけるドキュメントを処理し、レダクションルールを適用する主要クラスです。

#### ワークフロー例（新しいコードブロックはなし）
1. ライセンスを使用して `Redactor` を初期化します。  
2. `redactor.Load("sample.pdf")` で PDF をロードします。  
3. `RedactionPattern` は、レダクション対象のテキストまたはパターンを指定するルールを表します。例として `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")` のようにパターンを定義します。  
4. `redactor.Apply(pattern)` を実行します。  
5. `redactor.Save("sample_redacted.pdf")` で出力を保存します。

### 実用的な応用例

#### 実際の使用例
1. **法務文書管理** – 契約書を効率的に検索し、クライアント識別子を自動的にレダクションします。  
2. **医療記録** – 患者ノートを検索し、HIPAA 準拠の PHI レダクションを確保します。  
3. **企業コンプライアンス** – 社内コミュニケーションをスキャンし、禁止用語を検出してアーカイブ前にレダクションします。

## 結論
本ガイドは、**search index .NET** ソリューションをスケールさせ、迅速にインデックスし、レダクションでデータを保護するための包括的な手順を提供します。ノードの構成、ドキュメントのインデックス作成、高度な検索機能の活用、レダクションの適用により、開発者はドキュメント管理ワークフローを大幅に改善し、厳格なセキュリティ基準を維持できます。

## よくある質問

**Q: .NET で GroupDocs を使用して分散検索ネットワークを設定するにはどうすればよいですか？**  
A: ベースパスとポートを定義し、`SearchNetworkDeployment.Deploy()` を呼び出して、マスターとワーカーノードを複数のマシンに展開します。

**Q: GroupDocs で複数のパラメータを使用した高度な検索を実行できますか？**  
A: はい。`SearchOptions` を使用して、ファジーマッチング、ワイルドカードサポート、結果のハイライトを単一のクエリで組み合わせます。

**Q: マスターノードのネットワークアクティビティを監視できますか？**  
A: もちろんです。`IndexingCompleted` や `QueryExecuted` などの `SearchNetworkNodeEvents` を購読して、リアルタイムのインサイトを得られます。

**Q: GroupDocs を使用して PDF ファイルにレダクションを適用するにはどうすればよいですか？**  
A: `Redactor` を初期化し、PDF をロードし、`RedactionPattern` オブジェクト（正規表現または文字列）を定義して `Apply` を呼び出し、サニタイズされたドキュメントを保存します。

**Q: ネットワーク環境で検索パフォーマンスを向上させる最も簡単な方法は何ですか？**  
A: クエリ実行前にドキュメントセット全体をインデックスし、ノードを分散させて並列処理を活用し、`SearchOptions` をキャッシュやページング向けに調整します。

**最終更新日:** 2026-06-12  
**テスト環境:** GroupDocs.Search 23.9 for .NET、GroupDocs.Redaction 23.9 for .NET  
**作者:** GroupDocs

## 関連チュートリアル

- [GroupDocs.Search を使用した .NET ドキュメントインデックスのマスターガイド – 包括的ガイド](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [GroupDocs.Redaction .NET を使用したドキュメントインデックスと高度な検索クエリのマスター](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [.NET での GroupDocs Search と Redaction のマスター – 高度なドキュメント管理](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)