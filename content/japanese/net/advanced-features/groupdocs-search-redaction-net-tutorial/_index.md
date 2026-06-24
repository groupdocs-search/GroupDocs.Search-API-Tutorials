---
date: '2026-04-04'
description: GroupDocs.Search を使用して法的文書の検索とインデックス管理を学び、.NET で GroupDocs.Redaction
  を利用して医療記録のレダクションを統合します。
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: GroupDocs Search & Redaction for .NET で法的文書を検索
type: docs
url: /ja/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# GroupDocs Search と Redaction を使用した .NET での法的文書検索

今日のデータ駆動型環境では、**法的文書の検索** を迅速かつ安全に行うことが、あらゆる組織にとって重要な要件です。契約書、裁判所への提出書類、コンプライアンスレポートを扱う場合でも、GroupDocs.Search は高速でスケーラブルなインデックスを提供し、GroupDocs.Redaction は機密情報が隠されたままになることを保証します。このチュートリアルでは、検索可能なインデックスの設定、複数フォルダーからのドキュメント追加、そしてレダクションの構成方法を説明し、医療記録やその他の機密ファイルを安全に検索できるようにします。

## クイック回答
- **GroupDocs.Search は何をしますか？** さまざまなドキュメント形式に対して、全文検索可能なインデックスを作成します。  
- **検索前に情報をレダクトできますか？** はい。GroupDocs.Redaction を使用して機密データをマスクまたは削除します。  
- **インデックスにドキュメントを追加するには？** 追加したい各フォルダーに対して `index.Add("folderPath")` を呼び出します。  
- **サポートされているファイルタイプは何ですか？** PDF、DOCX、PPTX、TXT など多数の形式がサポートされています。  
- **本番環境でライセンスが必要ですか？** 一時的なトライアルは利用可能ですが、商用利用には永続ライセンスが必要です。

## 前提条件
このチュートリアルを進めるには、以下がインストールされていることを確認してください：
- .NET Core SDK (3.1 以上) がインストールされていること。  
- Visual Studio Code、Visual Studio、または .NET をサポートするその他の IDE。  
- C# プログラミングの基本的な知識があること。

### ライセンス取得
両方のライブラリの無料トライアルから始めることができます。長期利用の場合は、一時ライセンスを取得するか、[GroupDocs のウェブサイト](https://purchase.groupdocs.com/temporary-license/) から購入することをご検討ください。

## 必要なパッケージのインストール

**GroupDocs.Search のインストール:**  
**.NET CLI** を使用して、次を実行します:
```bash
dotnet add package GroupDocs.Search
```
または、Visual Studio のパッケージ マネージャ コンソールを使用します:
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction のインストール:**  
- .NET CLI を使用:
```bash
dotnet add package GroupDocs.Redaction
```
- または、パッケージ マネージャーを使用:
```powershell
Install-Package GroupDocs.Redaction
```

GUI を好む場合は、NuGet パッケージ マネージャ UI を開き、"GroupDocs.Redaction" を検索してインストールしてください。

## レダクタ設定の構成
レダクションを開始する前に、レダクタの動作を調整したい場合があります（例：レダクションの色を設定したり、カスタムパターンを定義したり）。以下のスニペットは基本的な初期化を示しています。

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **プロのコツ:** `redactorSettings` を組織のコンプライアンス ポリシーに合わせて調整します（例：テキストを黒いボックスに置き換える、レダクション前に OCR を適用する、など）。

## 実装ガイド

### 法的文書を検索する方法は？
検索可能なインデックスを作成することは、法的文書を高速に取得するための基盤です。GroupDocs.Search を使用すると、任意のフォルダーを指定してインデックスを構築し、数千のファイルに対して複雑なクエリを実行できます。

### インデックスにドキュメントを追加する方法
ドキュメントの追加は簡単です。ライブラリにファイルが格納されたディレクトリを指定するだけです。複数のフォルダーを追加できるため、法的コーパスが異なる場所に分散している場合に便利です。

#### インデックスの作成と管理
**概要:**  
インデックスの作成は、効率的なドキュメント検索操作への第一歩です。GroupDocs.Search を使用すると、任意のディレクトリに検索可能なインデックスを作成でき、ドキュメントの迅速な取得が可能になります。

##### 手順 1: インデックスの作成
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*説明:* `Index` は指定されたディレクトリに検索インデックスを初期化します。パスがプロジェクトのフォルダー構造を反映していることを確認してください。

##### 手順 2: インデックスへのドキュメント追加
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*説明:* `Add` メソッドは指定されたフォルダーをスキャンし、サポートされているすべてのドキュメントをインデックスに含めます。契約書、ケースファイル、医療記録など、複数のソースから **インデックスにドキュメントを追加** する際に使用します。

### インデックス作成レポートの取得と表示
**概要:**  
インデックス作成レポートは、処理されたドキュメント数、総語句数、ストレージサイズなどの情報を提供し、パフォーマンス調整に不可欠な指標となります。

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*説明:* `GetIndexingReports` はインデックス作成プロセスの詳細を示すレポートの配列を返し、パフォーマンスの監視と最適化に役立ちます。

## 実用的な活用例
1. **法的文書管理:** ケースファイルのインデックス作成を自動化し、法令、ブリーフ、判決を瞬時に取得できるようにします。  
2. **医療記録システム:** GroupDocs.Redaction を使用して PHI をマスクし、プライバシーを保護しながら患者記録を検索します。  
3. **企業 HR ポータル:** 検索可能な従業員ファイルとレダクションを組み合わせて、個人データを保護します。

## パフォーマンス上の考慮点
- **インデックスサイズの最適化:** 定期的に古いエントリを削除し、インデックスを再構築して軽量に保ちます。  
- **メモリ管理:** .NET のガベージコレクタを活用し、`Index` オブジェクトは不要になったら破棄します。  
- **スケーラビリティのベストプラクティス:** インデックスは高速 SSD に保存し、大規模コーパスは複数のインデックスに分割することを検討してください。

## よくある質問

**Q: GroupDocs.Search の主な用途は何ですか？**  
A: 大規模なドキュメントコレクションから検索可能なインデックスを作成し、法的および医療ファイルの高速取得を実現するのに最適です。

**Q: GroupDocs.Redaction はどのようにデータプライバシーを確保しますか？**  
A: インデックス作成や共有前に機密情報を永久に削除またはマスクするレダクションパターンを定義できます。

**Q: これらのライブラリをクラウド環境で使用できますか？**  
A: はい。適切なライセンスさえあれば、Azure、AWS、または任意のコンテナ化された .NET デプロイメントで両方のライブラリが動作します。

**Q: GroupDocs.Search がサポートするファイル形式は何ですか？**  
A: PDF、Word、Excel、PowerPoint、TXT、HTML など多数のエンタープライズ形式がサポートされています。

**Q: インデックス作成エラーをトラブルシュートするには？**  
A: フォルダーパスを確認し、ファイル権限をチェックし、`IndexingReport` のコンソール出力で特定のエラーコードを確認してください。

## リソース
- **ドキュメント:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API リファレンス:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **ダウンロード:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **無料サポート:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **一時ライセンス:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**最終更新日:** 2026-04-04  
**テスト環境:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**作者:** GroupDocs