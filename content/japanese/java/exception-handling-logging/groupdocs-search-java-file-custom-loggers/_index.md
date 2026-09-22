---
date: '2026-09-21'
description: GroupDocs.Search for Javaでloggerを作成し、max log sizeを設定し、console loggerを使用する方法を学びます。
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: GroupDocs.Search for Javaでloggerを作成し、max log sizeを設定し、console loggerを使用する方法を学びます。ステップバイステップの手順とベストプラクティスのヒントをご覧ください。
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: GroupDocs.Searchでloggerを作成し、log sizeを制限する方法
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: GroupDocs.Search for Javaでloggerを作成し、log sizeを制限する方法
type: docs
url: /ja/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search for Java でロガーを作成し、ログファイルサイズを制限する方法

このチュートリアルでは、GroupDocs.Search 用の **ロガーの作成方法** の実装、最大ログファイルサイズの設定、ファイルベースとコンソールロギングの切り替えについて説明します。適切なログ管理により、大規模なインデックス作成ジョブでディスクがいっぱいになるのを防ぎ、トラブルシューティングが改善され、開発時に即時のフィードバックが得られます。Maven の設定から始め、ロガーの構成を順に解説し、ロガーの動作を示すシンプルな検索クエリで締めくくります。

## クイック回答
- **「ログファイルサイズの制限」とは何ですか？** ログファイルの最大サイズを上限として設定し、ディスク上での無制限な増大を防ぎます。  
- **どのロガーがログファイルサイズを制限できますか？** 組み込みの `FileLogger` が最大サイズパラメータを受け取ります。  
- **コンソールロガー（java）をどう使いますか？** `ConsoleLogger` をインスタンス化し、`IndexSettings` に設定します。  
- **GroupDocs.Search のライセンスは必要ですか？** 評価にはトライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **最初のステップは何ですか？** Maven プロジェクトに GroupDocs.Search の依存関係を追加します。  

## ログファイルサイズの制限とは何ですか？
**ログファイルサイズの制限** 設定は、ファイルが定義された閾値（例: 4 MB）に達したらロガーが新しいエントリの書き込みを停止するよう指示します。上限に達すると、ロガーはさらにメッセージを破棄するか、新しいファイルにローテーションし、ディスク使用量を予測可能に保ちます。

## GroupDocs.Search でファイルおよびカスタムロガーを使用する理由
ファイルロガーとカスタムロガーは、監査性、デバッグの洞察、柔軟性を提供します。本番環境では、ファイルログがすべてのインデックス作成および検索操作の永続的な記録を提供し、開発時にはコンソールログが即時のフィードバックを提供します。これらのログは、チームがパフォーマンスを監視し、エラーを追跡し、詳細なアクティビティ履歴を保持することでコンプライアンス要件を満たすのに役立ちます。

## 前提条件
- GroupDocs.Search for Java ≥ 25.4。  
- JDK 8 以上、IntelliJ IDEA や Eclipse などの IDE。  
- Maven と Java プログラミングの基本的な知識。  

## GroupDocs.Search for Java の設定

以下のいずれかの方法でライブラリをプロジェクトに追加します。

**Maven 設定:**  

```text
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
```

**直接ダウンロード:**  
公式サイトから最新の JAR をダウンロードします: [GroupDocs.Search for Java のリリース](https://releases.groupdocs.com/search/java/)。

### ライセンス取得
トライアルを取得するか、[ライセンスページ](https://purchase.groupdocs.com/temporary-license/) でライセンスを購入してください。

## GroupDocs.Search 用カスタムロガーの作成方法
カスタムロガーの作成は簡単です。GroupDocs.Search は `ILogger` インターフェイスに依存しているためです。このインターフェイスを実装するか、提供されている `FileLogger` や `ConsoleLogger` を拡張することで、リモート転送やログローテーションなどの追加動作を注入できます。また、ネットワーク接続のオープンなどの初期化ロジックを追加し、ロガーのシャットダウンメソッドでリソースを確実にクローズすることも可能です。このアプローチにより、ELK や Splunk などの監視プラットフォームと統合できます。

### 定義アンカー
`ILogger` は GroupDocs.Search のコアロギング契約であり、その `log(Level, String)` メソッドを実装したクラスはロガーとなります。

### 例のアプローチ（コードブロックなし）
1. `ILogger` を実装するクラスを作成します。  
2. `log` メソッドをオーバーライドし、メッセージを選択した宛先（ファイル、データベース、HTTP エンドポイント）に書き込みます。  
3. インデックス設定で `settings.setLogger(new YourCustomLogger())` を呼び出します。  

## File Logger でログファイルサイズを制限する方法
`FileLogger` クラスはログエントリをディスク上のファイルに書き込み、最大サイズの引数を受け取ります。サイズ上限を指定することで、ロガーは自動的に新しいエントリの追加を停止するか、閾値に達したときに新しいファイルを作成し、ディスクの無制限な増大を防ぎます。この動作により、ロギングがインデックス作成のパフォーマンスに影響を与えず、イベントの簡潔な記録が保持されます。

### 定義アンカー
`FileLogger` は組み込みロガーで、メッセージをテキストファイルに永続化し、設定可能な最大ファイルサイズをサポートします。

### 手順ガイド
1️⃣ **必要なパッケージをインポート**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **File Logger を使用したインデックス設定の構成**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **インデックスを作成またはロード**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **インデックスにドキュメントを追加**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **検索クエリを実行**  
```text
```java
SearchResult result = index.search(query);
```
```

**重要ポイント:** `FileLogger` コンストラクタの第2引数（`4.0`）は、メガバイト単位で **最大ログサイズを設定** し、**ログファイルサイズの制限** 要件に直接対応します。

## コンソールロガー（java）の使用方法
ログイベントを即座に確認したい場合、`ConsoleLogger` は各メッセージを `System.out` に書き込みます。このロガーは軽量でスレッドセーフであり、開発やデバッグセッションに適しています。ファイル I/O を必要とせず、インデックス作成の進行状況、検索クエリ、エラー状態に対して即時のフィードバックを提供し、反復テストを高速化できます。

### 定義アンカー
`ConsoleLogger` は標準コンソールストリームにログエントリを出力する軽量ロガーで、デバッグセッションに最適です。

### 設定手順
1️⃣ **コンソールロガーをインポート**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Console Logger を使用したインデックス設定の構成**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **インデックスを作成またはロード**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **ドキュメントを追加し、検索を実行**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**ヒント:** コンソールロガーは開発時に最適で、各ログエントリを即座に出力し、インデックス作成と検索が期待通りに動作することを確認できます。

## 実用的な適用例
1. **ドキュメント管理システム:** インデックスされたすべてのドキュメントの監査トレイルを保持し、コンプライアンス要件を満たします。  
2. **エンタープライズ検索エンジン:** クエリのパフォーマンスとエラー率をリアルタイムで監視し、迅速な SLA コンプライアンスチェックを可能にします。  
3. **法務・コンプライアンスソフトウェア:** 規制報告のために検索語句とタイムスタンプを記録し、ログは規定の保存期間まで保持します。  

## パフォーマンス上の考慮点
- **ログサイズ:** **最大ログサイズを設定** することで、JVM のガベージコレクタを遅くする可能性のある過剰なディスク使用を回避できます。  
- **非同期ロギング:** 高スループットシナリオでは、ロガーを非同期キューでラップし、I/O をインデックススレッドから切り離します（本ガイドの範囲外の実装）。  
- **メモリ管理:** 必要なくなった大きな `Index` オブジェクトは `index.close()` で解放し、JVM のフットプリントを低く保ちます。  

## よくある問題と解決策
- **ログパスにアクセスできない:** ディレクトリが存在し、JVM を実行しているユーザーアカウントに書き込み権限があることを確認してください。  
- **ロガーが動作しない:** `Index` オブジェクトを作成する *前に* `settings.setLogger(...)` を呼び出していることを確認してください。そうでなければデフォルトロガーが使用されます。  
- **コンソール出力がない:** アプリケーションを `System.out` を表示するターミナルで実行し、ロギングフレームワーク（例: SLF4J）が出力をインターセプトしていないことを確認してください。  

## よくある質問

**Q: `FileLogger` の第2パラメータは何を制御しますか？**  
A: ログファイルの最大サイズ（メガバイト）を設定し、**最大ログサイズを設定** して無制限な増大を防ぎます。

**Q: ファイルロガーとコンソールロガーを組み合わせられますか？**  
A: はい。各 `log` 呼び出しを `FileLogger` と `ConsoleLogger` の両方に転送するカスタムロガーを作成し、その複合ロガーを `IndexSettings` に登録します。

**Q: 初期作成後にインデックスにドキュメントを追加するには？**  
A: 任意のタイミングで `index.add(pathToNewDocs)` を呼び出せば、設定されたロガーが自動的に追加を記録します。

**Q: `ConsoleLogger` はスレッドセーフですか？**  
A: `System.out` に直接書き込むため、JVM が内部で同期し、一般的なマルチスレッド使用ケースで安全です。

**Q: ログファイルサイズを制限すると、保存される情報量に影響しますか？**  
A: サイズ上限に達すると、新しいエントリは破棄されるか、実装に応じてロガーが新しいファイルにローテーションします。

## リソース
- [ドキュメント](https://docs.groupdocs.com/search/java/)
- [API リファレンス](https://reference.groupdocs.com/search/java/)

---

**最終更新日:** 2026-09-21  
**テスト環境:** GroupDocs.Search for Java 25.4  
**作者:** GroupDocs  

---

## 関連チュートリアル

- [ロギング実装方法 - GroupDocs.Search Java の例外処理とロギングチュートリアル](/search/java/exception-handling-logging/)
- [Java で非同期ロギングを実装 - GroupDocs.Search カスタムロガーガイド](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Search Index の作成 Java – GroupDocs.Search チュートリアル](/search/java/indexing/)