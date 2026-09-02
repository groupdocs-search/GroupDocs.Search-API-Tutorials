---
date: '2026-04-02'
description: .NETでGroupDocs.SearchとGroupDocs.Redactionを使用し、検索インデックス（GroupDocs）を作成してドキュメントをインデックスに追加しながら、ファセット検索を実装する方法を学びましょう。
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: レダクション付きGroupDocsで検索インデックスを作成する .NET ファセット検索
type: docs
url: /ja/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Redaction .NET ファセット検索で GroupDocs の検索インデックスを作成する

最新のアプリケーションでは、**GroupDocs を使用した検索インデックスの作成**は、迅速かつ正確なドキュメント検索に不可欠です。法的契約書、製品カタログ、または大規模なナレッジベースを扱う場合でも、適切に構築されたインデックスにより、**インデックスにドキュメントを追加**し、数秒で強力なファセット検索を実行できます。本チュートリアルでは、GroupDocs.Redaction の設定からシンプルおよび複雑なファセットクエリの作成まで、プロセス全体を順を追って説明します。これにより、.NET プロジェクトで応答性の高い検索体験を提供できます。

## クイック回答
- **主な目的は何ですか？** GroupDocs を使用して検索インデックスを作成し、ファセット検索を有効にすることです。  
- **必要なライブラリは何ですか？** GroupDocs.Redaction と GroupDocs.Search for .NET。  
- **インデックスにドキュメントを追加するにはどうすればよいですか？** インデックスを初期化した後、`index.Add(documentsFolder)` を使用します。  
- **複雑なクエリを実行できますか？** はい、オブジェクトクエリを論理演算子と組み合わせて高度なフィルタリングが可能です。  
- **ライセンスは必要ですか？** 開発には無料トライアルで動作しますが、本番環境では商用ライセンスが必要です。

## ファセット検索とは何か、そして GroupDocs と併用する理由
ファセット検索は、カテゴリ、日付、著者など、複数のフィルタを同時に適用して結果を絞り込むことができます。**GroupDocs.Redaction** と組み合わせることで、赤字規則を遵守した安全で検索可能なコンテンツが得られ、コンプライアンスが重視される環境に最適です。

## 前提条件

### 必要なライブラリ、バージョン、依存関係
- **GroupDocs.Redaction .NET** – 最新の安定版リリースです。  
- **GroupDocs.Search .NET** – インデックス作成のために Redaction と連携して動作します。

### 環境設定要件
- **IDE**: Visual Studio 2019 以降。  
- **Framework**: .NET Core 3.1、.NET 5、または .NET 6。  
- **OS Compatibility**: Windows、Linux、macOS。

### 知識の前提条件
基本的な C# スキルとファセット検索概念の高レベルな理解が役立ちますが、ステップバイステップのガイドは初心者にも優しいです。

## .NET 用 GroupDocs.Redaction の設定

### インストール情報
以下のいずれかの方法で GroupDocs.Redaction パッケージを追加できます。

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- 「GroupDocs.Redaction」を検索し、最新バージョンをインストールします。

### ライセンス取得手順
すべての機能を有効にするには、無料トライアルから開始するか、永続ライセンスを取得してください。

1. ライセンスオプションを確認するには、[GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) にアクセスしてください。  
2. 画面の指示に従って、トライアルまたは購入したライセンスファイルを受け取ります。

### 基本的な初期化と設定
パッケージがインストールされたら、アプリケーションで Redactor を初期化します。

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## GroupDocs の検索インデックスの作成方法

以下では実装を 2 つのパートに分けて説明します：**Simple Faceted Search** と **Complex Query**。各パートでは、**GroupDocs の検索インデックスを作成**し、ドキュメントを追加し、クエリを実行する方法を示します。

### 機能 1: シンプルなファセット検索

**概要**  
ファセット検索は、複数の条件を選択して結果を絞り込むことができます。このセクションでは、GroupDocs.Search を使用したシンプルなアプローチを示します。

#### ステップ 1: インデックスとドキュメント フォルダーを定義する
インデックスが保存されるフォルダーと、ソースドキュメントが存在するフォルダーのパスを設定します。

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### ステップ 2: インデックスを作成する
定義したフォルダーに検索インデックスを初期化します。

```csharp
Index index = new Index(indexFolder);
```

#### ステップ 3: インデックスにドキュメントを追加する
ドキュメントをロードして検索可能にします。

```csharp
index.Add(documentsFolder);
```

#### ステップ 4: テキストクエリ検索を実行する
**content** フィールドに対して基本的なテキストクエリを実行します。

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### ステップ 5: オブジェクトクエリ検索を実行する
より細かい制御のためにオブジェクト指向クエリを使用します。

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### 機能 2: 複雑なクエリ

**概要**  
ファイル名パターンやフレーズ一致など、複数のフィルタを組み合わせる必要がある場合、論理演算子を使用して複雑なクエリを構築できます。

#### ステップ 1: インデックスとドキュメント フォルダーを定義する
より高度なシナリオのために、同じフォルダー構造を再利用します。

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### ステップ 2: インデックスを作成し、ドキュメントを追加する
(シンプル例のステップ 2‑3 を参照してください。変更はありません。)

#### ステップ 3: テキストクエリ検索を実行する
ファイル名とコンテンツの条件を組み合わせた複合テキストクエリを実行します。

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### ステップ 4: オブジェクトクエリを構築して実行する
同じロジックをプログラムで構築します。

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

フレーズ、範囲、ブール演算子を組み合わせて、正確なビジネスルールに合致させてください。

## 実用的な応用例

1. **E‑Commerce Platforms** – カテゴリ、価格、評価で製品をフィルタリングします。  
2. **Document Management Systems** – 著者、日付、機密レベルで契約書を検索します。  
3. **Content Portals** – タグ、トピック、公開日で読者が絞り込めるようにします。

## パフォーマンス上の考慮点

- **Index Refresh**: 新規または更新されたファイルを定期的に再インデックスし、検索を高速に保ちます。  
- **Memory Management**: 使用後は `Index` オブジェクトを破棄します。特に大規模データセットでは重要です。  
- **Asynchronous Indexing**: 重いインデックス作成中に UI がフリーズしないよう、`Task.Run` やバックグラウンドサービスを使用します。

## 一般的な問題と解決策

| 問題 | 解決策 |
|-------|----------|
| **インデックスが見つかりません** | `indexFolder` のパスを確認し、フォルダーに書き込み権限があることを確認してください。 |
| **結果が返されません** | クエリ対象のフィールド（例: `Content`、`Filename`）がインデックスされているか確認してください。 |
| **メモリ不足エラー** | ドキュメントをバッチ処理し、.NET の GC ヒープサイズの増加を検討してください。 |

## よくある質問

**Q: ファセット検索とは何ですか？**  
A: ファセット検索は、カテゴリ、日付、著者など、複数の独立したフィルタを使用して結果を絞り込むことができます。

**Q: GroupDocs.Search で大規模データセットを扱うにはどうすればよいですか？**  
A: 増分インデックス作成、バッチ処理、非同期操作を使用して、メモリ使用量を抑え、パフォーマンスを高く保ちます。

**Q: 既存の .NET アプリケーションに GroupDocs の機能を統合できますか？**  
A: はい、これらのライブラリは任意の .NET プロジェクトへのシームレスな統合を想定して設計されています。

**Q: ファセット検索で一般的な問題は何ですか？**  
A: 複雑なクエリ構文や、すべての関連フィールドがインデックスされていることを確認することが典型的な課題です。適切なテストとインデックスのメンテナンスでこれらを軽減できます。

**Q: GroupDocs の一時ライセンスを取得するには？**  
A: 評価期間中にフル機能を解放するトライアルライセンスを申請するには、[GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) にアクセスしてください。

## リソース
- **ドキュメント**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API リファレンス**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**最終更新日:** 2026-04-02  
**テスト環境:** GroupDocs.Redaction 23.12 for .NET、GroupDocs.Search 23.12 for .NET  
**作者:** GroupDocs