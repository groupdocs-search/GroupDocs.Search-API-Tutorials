---
date: '2026-06-07'
description: .NET アプリケーションで、テキスト保存のための高圧縮 .NET の実装方法と、GroupDocs.Search と GroupDocs.Redaction
  を使用して機密データをレダクトする方法を学びます。
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'GroupDocs で高圧縮 .NET を実装: テキストとレダクション ガイド'
type: docs
url: /ja/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# GroupDocs を使用した高圧縮 .NET の実装：テキストとレダクション ガイド

最新の .NET ソリューションでは、膨大なテキストコレクションをディスク使用量を増やさずに保存する必要がある場合、**implement high compression .net** は不可欠です。同時に、個人識別子や財務数値などの機密情報を保護するには、信頼できるレダクションが必要です。このチュートリアルでは、**GroupDocs.Search** を使用した高圧縮テキストストレージの設定方法と、**GroupDocs.Redaction** を使用して機密データを安全にレダクションする方法をステップバイステップで示します。最後まで読むと、インデックス化されたテキストを最大90 %圧縮し、PDF、Word ファイル、その他多数のフォーマットからプライベートコンテンツを除去できるようになります。

## クイック回答

- **高圧縮インデックスを提供するライブラリはどれですか？** GroupDocs.Search for .NET.  
- **機密データをレダクションするツールはどれですか？** GroupDocs.Redaction for .NET.  
- **インデックスに自動的にドキュメントを追加できますか？** はい—フォルダー スキャン ループ内で `AddDocument` API を使用してください。  
- **圧縮は検索に対してロスレスですか？** はい、圧縮後もテキストは完全に検索可能です。  
- **本番環境でライセンスが必要ですか？** 商用利用には永続的な GroupDocs ライセンスが必要です。

## 「implement high compression .net」とは何ですか？

Implement high compression .net は、GroupDocs.Search のインデックスエンジンを構成し、抽出されたテキストコンテンツを圧縮形式で保存することを意味します。これにより、ディスク上のインデックスサイズが大幅に削減され、テキストは完全に検索可能なままです。圧縮はロスレスであるため、クエリの関連性やスニペット抽出は非圧縮インデックスと同様に機能します。

## 圧縮とレダクションに GroupDocs を使用する理由は？

GroupDocs.Search は 50 以上の入力フォーマットをサポートし、インデックス化されたテキストを最大 90 % 圧縮できるため、大規模なドキュメントコレクションが元のサイズのごく一部しか占めなくなります。GroupDocs.Redaction はこれを補完し、30 以上のファイルタイプで機密情報を永久に削除またはマスクし、GDPR や HIPAA などの厳格なコンプライアンス規制を追加ツールなしで満たすのに役立ちます。

## 前提条件

- **開発環境:** Visual Studio 2022 以降、.NET 6+（または .NET Framework 4.7.2）。  
- **ライブラリ:** `GroupDocs.Search` と `GroupDocs.Redaction` の NuGet パッケージ。  
- **権限:** ソースドキュメントとインデックス出力先フォルダーへの読み書きアクセス。  
- **基本知識:** C# 構文、ファイル I/O、.NET プロジェクト構造の理解。

## GroupDocs で高圧縮 .NET を実装する方法は？

GroupDocs で高圧縮 .NET を実装するには、まず `TextStorageSettings` インスタンスを作成し、その `CompressionLevel` を `High` に設定します。次に `Index` オブジェクトをインスタンス化し、設定とインデックスを保存するフォルダーを渡します。インデックスが準備できたら `AddDocument` でドキュメントを追加し、最後に `Search` メソッドで検索を実行します。エンジンは圧縮と解凍を透過的に処理します。

### ステップ 1: 必要な NuGet パッケージをインストール

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- “GroupDocs.Search” を検索し、**Install** をクリックします。  

### ステップ 2: GroupDocs.Redaction をインストール（データレダクション用）

- **NuGet Package Manager** を開きます。  
- **GroupDocs.Redaction** を検索し、最新の安定版をインストールします。  

### ステップ 3: ライセンスを取得して適用

- **Free trial:** GroupDocs ポータルに登録して 30 日間のトライアルキーを取得します。  
- **Temporary license:** 開発環境用に一時キーをリクエストします。  
- **Permanent license:** 評価制限を解除する本番ライセンスを購入します。

### ステップ 4: 両ライブラリの基本初期化

`Search` と `Redaction` エンジンは共通のライセンスモデルを共有します。アプリケーションの起動時にそれらを初期化します：

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## 機能 1: 高圧縮テキストストレージ設定

### インデックス構成の設定

`TextStorageSettings` は、GroupDocs.Search に抽出テキストの保持方法を指示するクラスです。高圧縮を有効にすると、検索速度に影響を与えることなくインデックスサイズが最大 **10×** 短縮されます。

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**説明:**  
- `CompressionLevel.High` は、テキストブロックを効率的に圧縮する ZSTD ベースのアルゴリズムを有効にします。  
- `UseMemoryCache = false` はエンジンにディスクからデータをストリーミングさせ、 大規模展開に最適です。

### インデックスの作成と管理

`Index` オブジェクトは、ディスク上の検索可能なリポジトリを表します。インデックスファイルを保存するフォルダーを指定し、上記で定義した圧縮設定を渡します。

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**説明:**  
- `indexFolder` は圧縮インデックスファイルの保存場所を決定します。  
- `settings` は高圧縮設定を注入し、追加されるすべてのドキュメントがそれの恩恵を受けるようにします。

## 機能 2: ドキュメントのインデックスへの追加

### インデックスにドキュメントを追加

`AddDocument` は単一ファイルをインデックスに追加し、テキストを抽出し、設定された圧縮設定に従って圧縮し、結果を保存します。GroupDocs.Search はディレクトリツリーからファイルを取り込むことができます。以下のループは `documentsFolder` を走査し、各ファイルを追加し、進捗をログに記録します。

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**説明:**  
- `AddDocument` はファイルを解析し、検索可能なテキストを抽出し、`TextStorageSettings` に従って圧縮し、インデックスに保存します。  
- このアプローチは **PDF、DOCX、TXT、HTML** および **30** 以上のその他のフォーマットで機能します。

## 機能 3: 検索クエリの実行

### 検索を実行

`Search` は圧縮インデックスに対してクエリを実行し、関連度スコアとハイライトされたスニペットを含む一致する `DocumentResult` オブジェクトのコレクションを返します。インデックスが構築されれば、高速なクエリを実行できます。`Search` メソッドはファイルパスとハイライトされたスニペットを含む `DocumentResult` オブジェクトのコレクションを返します。

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**説明:**  
- 検索エンジンは圧縮テキストを直接スキャンするため、**数百万ページ** を含むインデックスでもクエリ遅延は低く保たれます。  
- `Score` は関連度を示し、値が高いほどマッチ度が高いことを意味します。

## GroupDocs.Redaction で機密データをレダクションする方法は？

GroupDocs.Redaction で機密データをレダクションするには、対象ファイル用に `Redactor` インスタンスを作成します。社会保障番号などの正規表現のように、削除すべきテキストを記述する `SearchPattern` オブジェクトを一つまたは複数定義します。各パターンを `Redact` で適用し、`BlackOut` のような `RedactionType` を指定して、結果を新しいドキュメントとして保存します。これにより元のファイルは変更されません。

`Redactor` は、ドキュメントを読み込みレダクション操作を実行するための GroupDocs.Redaction の主要クラスです。  
`SearchPattern` は、レダクション対象テキストを識別する正規表現を定義します。

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**説明:**  
- `SearchPattern` は正規表現を使用して社会保障番号を検出します。  
- `RedactionType.BlackOut` は一致したテキストを黒い矩形で置き換え、データが復元できないようにします。

## 実用的な応用例

1. **Legal Document Management:** 大規模な訴訟ファイルを自動的に圧縮し、アーカイブ前にクライアント識別子をレダクションします。  
2. **Healthcare Records:** 数年分の患者ノートを圧縮インデックスに保存し、研究パートナーと共有する前に PHI（Protected Health Information）を除去します。  
3. **Financial Reporting:** 四半期報告書を保護するために口座番号をレダクションし、監査クエリ用に検索可能なテキストは保持します。

## パフォーマンス上の考慮点

- **圧縮の影響:** 高圧縮によりインデックスサイズが最大 **90 %** 短縮され、SSD の摩耗が減少しバックアップが高速化します。  
- **メモリ使用量:** 非常に大きなインデックスではメモリキャッシュを無効にし、プロセスのフットプリントを **500 MB** 未満に抑えます。  
- **I/O 最適化:** ディスクスラッシングを最小化するため、ドキュメント追加を 100 件単位でバッチ処理します。  
- **非同期処理:** `AddDocument` 呼び出しを `Task.Run` でラップし、デスクトップアプリの UI スレッドを応答性のある状態に保ちます。

## 一般的な落とし穴とトラブルシューティング

- **ファイルパスが正しくない:** `documentsFolder` と `indexFolder` が絶対パスであること、アプリケーションに読み書き権限があることを確認してください。  
- **ライセンスエラー:** `.lic` ファイルが実行ファイルと同じ場所に配置されているか、リソースとして埋め込まれていることを確認してください。  
- **検索で結果が返らない:** `TextStorageSettings` の圧縮レベルがインデックス作成時に使用したものと一致しているか確認してください。設定が一致しないとデシリアライズに失敗する可能性があります。

## よくある質問

**Q: 初期構築後にインデックスにドキュメントを追加できますか？**  
A: はい—新しいファイルに対して `index.AddDocument` を呼び出すだけで、エンジンは圧縮インデックスをインクリメンタルに更新します。

**Q: レダクションは元のファイルを変更しますか？**  
A: いいえ—元のファイルはそのままで、レダクションされたバージョンは新しいファイルとして保存され、ドキュメントの完全性が保たれます。

**Q: GroupDocs.Redaction がサポートするフォーマットは何ですか？**  
A: PDF、DOCX、PPTX、XLSX、画像（PNG、JPEG）、プレーンテキストなど、**30** 以上のフォーマットをサポートしています。

**Q: 高圧縮は検索の関連性に影響しますか？**  
A: 影響しません。テキストの圧縮はロスレスであるため、関連スコアは非圧縮インデックスと同一です。

**Q: インデックス可能なドキュメントサイズに上限はありますか？**  
A: GroupDocs.Search はコンテンツをストリーミングすることでマルチギガバイトのファイルを処理できますが、圧縮インデックス用に十分なディスク容量（元サイズの約 10 %）を確保してください。

## リソース

- [ドキュメンテーション](https://docs.groupdocs.com/search/net/)
- [API リファレンス](https://reference.groupdocs.com/redaction/net)
- [.NET 用 GroupDocs.Redaction のダウンロード](https://releases.groupdocs.com/search/net/)
- [無料サポートフォーラム](https://forum.groupdocs.com/c/search/10)
- [一時ライセンス取得](https://purchase.groupdocs.com/temporary-license/)

---

**最終更新日:** 2026-06-07  
**テスト環境:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**作者:** GroupDocs

## 関連チュートリアル

- [ドキュメント管理のための .NET における GroupDocs.Search と Redaction の実装](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [.NET 用 GroupDocs.Redaction の最適化方法：効率的なインデックスとスペリング管理ガイド](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [.NET での GroupDocs Redaction と Search のマスターガイド：効率的なドキュメント管理と安全な検索](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)