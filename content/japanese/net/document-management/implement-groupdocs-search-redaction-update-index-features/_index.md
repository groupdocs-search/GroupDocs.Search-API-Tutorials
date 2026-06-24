---
date: '2026-06-07'
description: GroupDocs.Search と Redaction for .NET を使用してインデックスを効率的に更新し、ドキュメント管理システムを強化する方法を学びましょう。
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: GroupDocs.Search と Redaction (.NET) を使用したインデックスの更新方法
type: docs
url: /ja/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# GroupDocs.Search と Redaction (.NET) を使用したインデックスの更新方法

## クイック回答
- **「インデックスの更新方法」とは何か？** 既存の検索インデックスを変更し、新規または変更されたドキュメントが再構築せずに検索可能になるプロセスです。  
- **必要なライブラリは？** GroupDocs.Search と GroupDocs.Redaction for .NET（どちらも NuGet で入手可能）。  
- **ライセンスは必要か？** テスト用の無料トライアルで動作します。製品版ライセンスでフル機能が利用可能です。  
- **.NET Core で実行できるか？** はい、.NET Framework 4.5+、.NET Core 3.1+、および .NET 5/6+ をサポートしています。  
- **期待できるパフォーマンスは？** 1 GB のインデックスを 2 スレッドで更新すると、典型的な 4 コアサーバーで 1 分未満で完了します。

## 「インデックスの更新方法」とは何か？
**インデックスの更新方法** は、インデックス全体を再作成するのではなく、既存の検索インデックスに増分変更を適用する手法を指します。このアプローチによりダウンタイムが削減され、CPU 使用率が抑えられ、ドキュメントの追加・編集・削除に伴って検索結果が常に最新の状態に保たれます。

## インデックス更新に GroupDocs.Search と Redaction を使用する理由
GroupDocs.Search は **50 以上のファイル形式**（PDF、DOCX、XLSX、PPTX、HTML、画像など）をサポートし、数百ページに及ぶドキュメントでもメモリに全体を読み込まずに処理できます。GroupDocs.Redaction と組み合わせることで、インデックス作成前に機密データを自動的に除去またはマスクでき、コンプライアンスを保ちつつ検索の関連性を維持できます。

## 前提条件

- **GroupDocs.Search** – NuGet でインストール。  
- **GroupDocs.Redaction for .NET** – 赤字処理機能に必要。  
- Visual Studio（または任意の .NET IDE）と .NET 6+ がインストールされていること。  
- 基本的な C# の知識とインデックス概念の理解。

### 必要なライブラリとバージョン
- **GroupDocs.Search** – NuGet から入手できる最新の安定版。  
- **GroupDocs.Redaction for .NET** – NuGet から入手できる最新の安定版。

### 環境設定要件
- .NET SDK がインストールされた Windows または Linux マシン。  
- インデックスファイルを格納するフォルダーへのアクセス権。

### 知識の前提条件
- ドキュメントインデックスと検索の基本を理解していること。  
- エンタープライズシステムにおけるドキュメントライフサイクル管理への認識。

## GroupDocs.Redaction for .NET の設定

### パッケージのインストール

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- “GroupDocs.Redaction” を検索し、最新バージョンをインストールします。

### ライセンス取得手順
1. **Free Trial** – すべての機能を試すためにトライアルから開始します。  
2. **Temporary License** – 長期テスト用に一時キーをリクエストします。  
3. **Purchase** – 本番環境向けにフルライセンスを取得します。

### 基本的な初期化と設定
`Redactor` はドキュメントに赤字ルールを適用するコアクラスです。  
使用開始には Redaction 名前空間を参照し、`Redactor` インスタンスを作成します。

```csharp
using GroupDocs.Redaction;
```

これでインデックスにドキュメントを投入する前に赤字ルールを適用できるようになります。

## 実装ガイド

このセクションでは、インデックス化されたドキュメントの更新とインデックスのバージョン管理という 2 つの主要機能を取り上げます。

### GroupDocs.Search を使用したインデックスの更新方法

`Index` はディスク上に保存された検索可能コレクションを表します。  
`UpdateOptions` は増分更新の方法（例：スレッド数）を構成します。  
`UpdateDocument` は単一ドキュメントの変更を適用し、`Commit` は保留中のすべての更新を確定します。

**直接的な回答（40‑70語）：**  
インデックスフォルダーを指す `Index` オブジェクトを作成し、`UpdateOptions` でスレッド数を指定します。変更された各ファイルに対して `UpdateDocument` を呼び出し、最後に `Commit` を実行して変更を永続化します。この増分方式により、フルリビルドなしで変更部分だけが更新され、インデックスが常に最新の状態に保たれます。

#### 機能 1: インデックス化されたドキュメントの更新

##### 概要
インデックス化されたドキュメントを更新することで、ドキュメントが編集または置換された際にも検索結果が最新の内容を反映します。

##### 手順 1: インデックスの作成  
`Index` クラスはディスク上の検索可能コレクションを表す最上位オブジェクトです。

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### 手順 2: インデックスにドキュメントを追加  
ディレクトリからファイルを追加すると、ライブラリが自動的に検索可能テキストを抽出します。

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### 手順 3: 検索と更新  
クエリを実行し、ソースファイルを変更した後、インデックス作成時と同じ `UpdateOptions` を使用して `UpdateDocument` を呼び出します。

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Why This Works:** `Threads = 2` を設定すると、更新処理が 2 つの CPU コアを利用し、クアッドコアマシンでは処理時間が約半分に短縮されます。

### インデックスのバージョン管理方法？

`IndexUpdater` は古いインデックス形式をライブラリがサポートする最新バージョンへアップグレードするユーティリティクラスです。

**直接的な回答（40‑70語）：**  
既存インデックスへのパスで `IndexUpdater` をインスタンス化し、`CanUpdateVersion()` で互換性を確認します。必要に応じて `UpdateVersion()` を実行し、アップグレード後に新フォーマットでインデックスを再ロードして検索を行い、すべてが正常に機能することを確認します。これにより、ライブラリのリリース間でシームレスに移行できます。

#### 機能 2: インデックスのバージョン管理

##### 概要
バージョン管理により、ライブラリのアップグレード後も古いインデックスが検索可能なまま保たれます。

##### 手順 1: 互換性の確認  
`IndexUpdater` は現在のインデックスが最新フォーマットにアップグレード可能かどうかをチェックします。

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### 手順 2: 読み込みと検索  
アップグレード後、リフレッシュされたインデックスをロードし、クエリを実行して整合性を検証します。

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Why This Works:** `CanUpdateVersion` ガードにより、インデックススキーマの不一致によるランタイム例外が防止され、安全なアップグレードパスが提供されます。

## 実用的な応用例

**インデックスの更新方法** が重要になる実世界シナリオ：

1. **Legal Document Management** – 契約書の改訂後に迅速に再インデックス化し、機密条項を赤字処理で除去します。  
2. **Corporate Archives** – 数百万ファイルを再処理せずに、履歴データを検索可能に保ちます。  
3. **Content Management Systems (CMS)** – 執筆者が新記事を公開するたびに、検索インデックスへ増分更新をプッシュします。

## パフォーマンス考慮事項

- **Threading Options:** `UpdateOptions.Threads` を CPU コア数に合わせて調整します。スレッド数を増やすとスループットは向上しますが、メモリ使用量も増加します。  
- **Resource Usage:** RAM を監視してください。ライブラリはファイルをストリーミング処理するため、500 ページの PDF でもメモリスパイクは最小限です。  
- **Best Practices:** 定期的な増分更新をスケジュールし、不要になったインデックスバージョンをクリーンアップして最適なパフォーマンスを維持します。

## よくある問題と解決策

| **Issue** | **Cause** | **Solution** |
|-----------|-----------|--------------|
| **インデックスが見つかりません** | フォルダー パスが誤っている | `Index` コンストラクタが正しいディレクトリを指しているか確認してください。 |
| **バージョン不一致エラー** | 古いインデックスを新しいライブラリで使用している | 通常のインデックス作成前に `IndexUpdater` フローを実行してください。 |
| **赤字が適用されていません** | インデックス作成後に赤字ルールをロードした | ドキュメントをインデックスに追加する **前に** 赤字処理を適用してください。 |

## よくある質問

**Q:** `UpdateDocument` と `Rebuild` の違いは何ですか？  
**A:** `UpdateDocument` は変更されたファイルのみを更新し、`Rebuild` はインデックス全体を最初から作り直すため、時間とリソースの消費が大きくなります。

**Q:** 複数のドキュメントを並列で更新できますか？  
**A:** はい、`UpdateOptions.Threads` に使用したいコア数を設定すれば、ライブラリが内部で並列処理を行います。

**Q:** GroupDocs.Search は暗号化された PDF をサポートしていますか？  
**A:** もちろんです。ドキュメント読み込み時に `SearchOptions.Password` でパスワードを指定してください。

**Q:** インデックス作成前に赤字が正しく適用されたかどうかはどう確認しますか？  
**A:** `Redactor.Apply()` を呼び出し、出力ファイルのサイズを確認します。サイズが減少していれば赤字が成功した可能性が高いです。

**Q:** 正式にサポートされている .NET バージョンは？  
**A:** .NET Framework 4.5+、.NET Core 3.1+、.NET 5、.NET 6+ を公式にサポートしています。

## 結論

このガイドに従えば、GroupDocs.Search と GroupDocs.Redaction for .NET を組み合わせて **インデックスの更新方法** を実装し、インデックスのバージョン互換性も確保できます。手順通りに進めることで、検索レイヤーを高速・正確かつデータプライバシー規制に準拠した状態で維持できます。

**次のステップ:**  
- ハードウェアに最適な `Threads` 設定を試行し、ベストバランスを見つけます。  
- インデックス作成前に高度な赤字パターン（例：正規表現ベースの SSN 削除）を検討します。  
- インデックス更新処理を CI/CD パイプラインに組み込み、ドキュメント管理を完全自動化します。

---

**最終更新日:** 2026-06-07  
**テスト環境:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**作者:** GroupDocs  

## リソース
- [ドキュメント](https://docs.groupdocs.com/search/net/)
- [API リファレンス](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction のダウンロード](https://releases.groupdocs.com/search/net/)
- [無料サポートフォーラム](https://forum.groupdocs.com/c/search/10)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)

## 関連チュートリアル

- [Mastering GroupDocs.Redaction .NET: Efficient Index Creation and Alias Management for Advanced Document Search](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implement Synonym Search with GroupDocs.Redaction .NET for Enhanced Document Management](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Mastering GroupDocs Search and Redaction in .NET: Advanced Document Management](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)