---
date: '2026-04-21'
description: GroupDocs.Redaction for .NET を使用してファイルをフィルタリングする方法を学びます。作成日、ファイルサイズ、更新日でのフィルタリングや、NOT
  フィルタの適用方法も含まれます。
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: .NET 用 GroupDocs.Redaction でファイルをフィルタリングする方法
type: docs
url: /ja/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# GroupDocs.Redaction for .NET を使用したファイルのフィルタリング方法

今日の急速に変化するデジタル環境では、**ファイルのフィルタリング方法** を効率的に行うことが生産性を左右します。拡張子、作成日、サイズ、または更新日でドキュメントを分離する必要がある場合、堅実なフィルタリング戦略は時間を節約し、ストレージコストを削減し、検索インデックスを整頓された状態に保ちます。このチュートリアルでは、GroupDocs.Redaction for .NET を使用した実践的な例を通じて、一般的なビジネスニーズに合わせたファイルのフィルタリング方法を詳しく解説します。

## クイック回答
- **どのライブラリが必要ですか？** GroupDocs.Redaction for .NET (NuGet でインストール)。  
- **作成日でフィルタリングできますか？** はい – `CreateCreationTimeRange` を使用します。  
- **特定のタイプを除外するには？** `DocumentFilter.CreateNot` を使用して NOT フィルタを適用します。  
- **ファイルサイズのフィルタリングはサポートされていますか？** 完全にサポートされており、`CreateFileLengthRange` または上限/下限を指定できます。  
- **ライセンスは必要ですか？** 本番環境で使用するには、トライアルまたはフルライセンスが必要です。

## GroupDocs.Redaction におけるファイルフィルタリングとは？

ファイルフィルタリングは、拡張子、日付、パスパターン、サイズなどのメタデータに基づいて、インデックスエンジンに含めるドキュメントや除外するドキュメントを指示できる機能です。正確な `DocumentFilter` ルールを定義することで、インデックスを軽量に保ち、検索を高速に行えます。

## なぜ GroupDocs.Redaction for .NET を使用するのか？

- **組み込みのフィルタヘルパー** – カスタムのファイルシステムコードを書く必要がありません。  
- **論理演算子** – AND、OR、NOT を使用して複数の条件を組み合わせられます。  
- **パフォーマンス最適化** – フィルタはインデックス作成時に適用され、後からではありません。  
- **クロスプラットフォーム** – .NET Framework、.NET Core、.NET 5/6+ で動作します。

## 前提条件
- .NET Framework 4.6 以上または .NET Core 3.1 以上がインストールされていること。  
- Visual Studio またはお好みの C# IDE。  
- 基本的な C# の知識。

### 必要なライブラリとセットアップ
好みの方法で NuGet パッケージをインストールします：

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **プロのコツ:** インストール後、ライセンスファイルをプロジェクトのルートに追加し、Redactor または Index オブジェクトを作成する前に `License.SetLicense("license-file-path")` を呼び出します。

## GroupDocs.Redaction for .NET の設定

まず、操作対象のドキュメントを指す `Redactor` インスタンスを作成します：

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **なぜ重要か:** Redactor を初期化することで、ライブラリが後続のワークフローでフィルタや赤字ルールを適用できる状態になることが保証されます。

## 拡張子でファイルをフィルタリングする方法

ファイル拡張子でフィルタリングすることは、ドキュメントセットを絞り込む最も一般的な方法です。以下では FB2、EPUB、TXT ファイルのみを保持します。

### 拡張子でフィルタリング

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 不要なタイプを除外するために NOT フィルタを適用する方法

**NOT フィルタ** ロジックを適用する必要がある場合（例: HTML と PDF ファイルを除外する）、`CreateNot` を使用します。

### HTM、HTML、PDF ファイルを除外

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 作成日でファイルをフィルタリングする方法

**作成日でフィルタリング** する必要がある場合、開始と終了の `DateTime` を指定します。

### 作成日範囲でフィルタリング

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 更新日でファイルをフィルタリングする方法

作成日と同様に、特定の時点以前に更新されたファイルに結果を限定できます。

### 更新日でフィルタリング

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 正規表現を使用してパスでファイルをフィルタリングする方法

フォルダー構造が命名規則に従っている場合、正規表現で特定のパスを対象にできます。

### ファイルパスパターンでフィルタリング

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## サイズでファイルをフィルタリングする方法

帯域幅やストレージの制限に対処する際、ドキュメントサイズの管理は重要です。

### ファイルサイズでフィルタリング (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## AND で複数条件を組み合わせる方法

複数の条件を同時に使用して **ファイルをフィルタリング** する必要がある場合、`CreateAnd` で組み合わせます。

### 論理 AND の例

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## OR で複数条件を組み合わせる方法

いずれかのルールが適合すればよい場合は `CreateOr` を使用します。

### 論理 OR の例

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## よくある問題と解決策
- **フィルタが適用されない:** `Index` インスタンスを作成する **前に** `settings.DocumentFilter` を設定していることを確認してください。  
- **予期しないファイルが表示される:** ファイル拡張子に先頭のドット（`.txt`）が含まれているか再確認してください。  
- **パフォーマンス低下:** フィルタを AND で組み合わせ、インデックスパイプラインの初期段階でスキャンするファイル数を減らします。  
- **正規表現エラー:** パスパターン内の特殊文字をエスケープするか、`RegexOptions.IgnoreCase` を使用して大文字小文字を区別しないマッチにします。

## よくある質問

**Q: NOT フィルタと AND フィルタを組み合わせることはできますか？**  
A: はい。まず NOT フィルタを作成し（`DocumentFilter.CreateNot`）、それを `DocumentFilter.CreateAnd` の引数の一つとして組み込みます。

**Q: 10 MB より大きいファイルをフィルタリングするには？**  
A: `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` を使用して、そのサイズを超えるファイルのみを含めます。

**Q: 作成日と更新日を同時にフィルタリングすることは可能ですか？**  
A: もちろん可能です。各フィルタを個別に作成し、`CreateAnd` で組み合わせます。

**Q: これらのフィルタはクラウドストレージのパスでも機能しますか？**  
A: フィルタはローカルファイルシステム上で動作します。クラウドソースの場合、まずファイルを一時フォルダーにダウンロードし、同じフィルタを適用してください。

**Q: フィルタを変更すると再インデックスが必要ですか？**  
A: はい。フィルタは `index.Add` を呼び出したときに評価されます。フィルタを変更した場合、新しい条件を反映させるためにインデックスを再構築する必要があります。

## 結論

GroupDocs.Redaction for .NET を使用した **ファイルのフィルタリング方法** を習得すれば、拡張子、作成日、更新日、ファイルサイズ、または NOT ロジックを用いたフィルタリングに関わらず、ドキュメント管理を効率化し、インデックスのパフォーマンスを保ち、真に重要なコンテンツに集中できます。論理演算子を試してビジネスルールに合わせたフィルタリングをカスタマイズすれば、速度とストレージ効率の即時向上が実感できるでしょう。

---

**最終更新日:** 2026-04-21  
**テスト環境:** GroupDocs.Redaction 24.11 for .NET  
**作者:** GroupDocs