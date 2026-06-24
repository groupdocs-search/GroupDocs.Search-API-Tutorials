---
date: '2026-04-02'
description: .NET 用 GroupDocs.Redaction でファイル拡張子でフィルタリングし、txt ファイルのみを検索する方法を学び、文書管理の効率を向上させましょう。
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: .NETでGroupDocs.Redactionを使用してファイル拡張子でフィルタリングする
type: docs
url: /ja/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# .NETでGroupDocs.Redactionを使用したファイル拡張子でのフィルタリング

大量のファイルコレクションを検索するのは圧倒されがちです。特に特定のファイルタイプの結果だけが必要な場合はなおさらです。このチュートリアルでは、GroupDocs.Redaction for .NET を使用して **ファイル拡張子でフィルタリングする方法** を紹介します。これにより、txt ファイルや任意の拡張子のみを検索できます。ファイルタイプとパスベースのフィルタの設定方法を順に説明するので、必要なドキュメントをすぐに見つけられます。

## クイック回答
- **「ファイル拡張子でフィルタリングする」機能は何をするのですか？** 指定されたファイル拡張子（例: *.txt）に一致するドキュメントに検索を限定します。  
- **なぜ GroupDocs.Redaction を使用するのですか？** 高速で統合が容易な組み込みフィルタリング API を提供します。  
- **ライセンスは必要ですか？** テストには無料トライアルで動作しますが、本番環境では有料ライセンスが必要です。  
- **サポートされている .NET バージョンは？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6+。  
- **ファイルタイプとパスフィルタを組み合わせられますか？** はい。複数のフィルタを適用して、非常に精密な検索が可能です。

## 学べること
- テキストファイルのみを検索対象とする **ファイル拡張子でフィルタリング** 方法。  
- 特定のフォルダーや命名パターンに結果を絞り込む **ファイルパスフィルタ** の設定方法。  
- インデックスを高速かつメモリ効率良く保つためのヒント。

## 前提条件
始める前に、以下が揃っていることを確認してください：

- **GroupDocs.Redaction Library** がインストールされ、.NET プロジェクトと互換性があること。  
- Visual Studio や VS Code などの開発環境。  
- 基本的な C# の知識と .NET プロジェクト構造への理解。

## .NET 用 GroupDocs.Redaction の設定
まず、プロジェクトにライブラリを追加します。

**.NET CLI の使用:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager の使用:**  
```bash
Install-Package GroupDocs.Redaction
```

または NuGet パッケージマネージャー UI で “GroupDocs.Redaction” を検索し、最新バージョンをインストールします。

### ライセンス取得
無料トライアルで開始するか、一時ライセンスをリクエストできます。長期プロジェクトの場合は、公式サイトからライセンスを購入してください。

### 基本初期化
パッケージをインストールしたら、ドキュメントへの参照を保持するインデックスを作成します。

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## 実装ガイド

### 機能 1: テキストドキュメント (.txt) のフィルタ設定

#### テキストドキュメントのファイル拡張子でフィルタリングする方法

1. **インデックスとドキュメントフォルダーを定義**  
   ソースファイルが存在するパスを設定します：

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **インデックスを作成**  
   ソースフォルダーからすべてのファイルをインデックスにロードします：

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **ファイル拡張子フィルタで検索オプションを構成**  
   エンジンに *.txt ファイルのみを対象とするよう指示します：

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **検索を実行**  
   クエリを実行します。フィルタによりテキスト以外のファイルは無視されます：

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explanation*: `Search` メソッドはフィルタを満たす一致を返し、ノイズを大幅に削減しパフォーマンスを向上させます。

### 機能 2: ファイルパスフィルタ

#### なぜファイルパスフィルタを使用するのか？

検索を特定の部門フォルダーや命名規則を共有するファイル群に限定したい場合があります。パスフィルタはまさにそれを実現します。

1. **インデックスとドキュメントフォルダーを定義**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **インデックスを作成**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **パスベースの正規表現で検索オプションを構成**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   この正規表現は、フルパスに “Lorem” という単語が含まれるファイルにマッチし、特定のサブフォルダーを対象にできます。

4. **パスベースの検索を実行**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## 実用的な応用例
- **Legal Document Management** – プレーンテキストファイルとして保存された関連契約書を迅速に検索します。  
- **Academic Research** – 特定のプロジェクトフォルダーに属する *.txt 形式の研究ノートのみを取得します。  
- **Corporate Reporting** – 部門パス（例: `/Finance/2025/`）で内部レポートをフィルタリングします。

## パフォーマンス上の考慮点
- 必要なドキュメントタイプだけをインデックス化します。不要なファイルはインデックスサイズと検索時間を増加させます。  
- 新規または変更されたファイルに対して `index.Add()` を呼び出すスケジュールジョブでインデックスを最新の状態に保ちます。  
- シンプルな正規表現を使用してください。過度に複雑なパターンは検索エンジンを遅くします。  
- `Index` オブジェクトは不要になったら必ず破棄してメモリを解放します。

## 結論
これで、GroupDocs.Redaction for .NET を使用して **ファイル拡張子でフィルタリング** と **ファイルパスフィルタ** を適用する方法が分かりました。これらの手法により、大規模なドキュメントコレクションを細かく制御でき、検索がより高速かつ関連性の高いものになります。次は、複数のフィルタを組み合わせたり、検索機能を大規模なアプリケーションワークフローに統合したりしてみてください。

## FAQ セクション

**Q1: テキストファイル以外のドキュメントもフィルタリングできますか？**  
A1: はい、GroupDocs.Redaction は多数のフォーマットをサポートしています。`CreateFileExtension` の引数を目的の拡張子（例: ".pdf"）に変更してください。

**Q2: 検索インデックスを定期的に更新するには？**  
A2: バックグラウンドサービスや cron ジョブをスケジュールし、更新したいディレクトリで `index.Add()` を実行します。

**Q3: ファイルパスでフィルタリングするとパフォーマンスに影響がありますか？**  
A3: 適切に最適化された正規表現は影響が最小限ですが、常に自分のデータセットでベンチマークしてください。

**Q4: 複数のフィルタを組み合わせて、より細かい検索ができますか？**  
A4: もちろんです。フィルタをチェーンしたり、複合フィルタを作成してファイルタイプとパスの両方を同時に対象にできます。

**Q5: GroupDocs.Redaction に関するリソースはどこで見つけられますか？**  
A5: 詳細なガイドや API リファレンスは、公式ドキュメント [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) をご覧ください。

## よくある質問

**Q: `SearchDocumentFilter` は暗号化ファイルでも機能しますか？**  
A: フィルタはファイルメタデータ上で動作するため、インデックス作成時に必要な復号クレデンシャルを提供すれば、暗号化ファイルもインデックス化されます。

**Q: パスフィルタで正規表現の代わりにワイルドカードを使用できますか？**  
A: 現在 API は正規表現が必須ですが、シンプルなワイルドカード（例: `.*`）をシミュレートできます。

**Q: インデックスがどの程度のサイズになるとシャーディングを検討すべきですか？**  
A: 数百ギガバイト規模のインデックスは、複数の論理インデックスに分割すると効果的です。コレクションが大きくなるにつれてパフォーマンスをテストしてください。

**Q: インデックスからドキュメントを削除する組み込みメソッドはありますか？**  
A: はい。`index.Delete(documentId)` または `index.DeleteAll()` を呼び出して古いエントリを管理できます。

**Q: 完全なドキュメントを読み込む前に検索結果をプレビューする方法はありますか？**  
A: `SearchResult` オブジェクトにはスニペット情報が含まれており、ファイル全体を開かずに UI に表示できます。

## リソース
- **Documentation**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最終更新日:** 2026-04-02  
**テスト環境:** GroupDocs.Redaction 23.12 for .NET  
**作者:** GroupDocs