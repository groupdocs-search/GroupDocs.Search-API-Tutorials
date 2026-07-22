---
date: '2026-02-24'
description: GroupDocs.Search for Javaでカスタムロガーの作成方法、最大ログサイズの設定方法、コンソールまたはファイルロガーの構成方法を学びましょう。
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: GroupDocs.Search Javaでカスタムロガーを作成し、ログファイルサイズを制限する方法
type: docs
url: /ja/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

 Java 25.4"

"**Author:** GroupDocs" translate: "**作者:** GroupDocs"

Then final "---"? Already there.

Make sure to keep markdown formatting.

Now produce final content.# GroupDocs.Search Java ロガーでログファイルサイズを制限する

このガイドでは、**カスタムロガー**の実装を作成し、GroupDocs.Search for Java を使用しながら **ログファイルサイズを制限**する方法を学びます。ログの増大を制御することは大規模なドキュメントインデックス作成において重要で、組み込みロガーを使用すると **set max log size**、**roll over log file**、または **use console logger** に切り替えて即時フィードバックを得ることができます。Maven の設定から検索クエリの実行まで、完全なセットアップを順に見ていき、ロガーが有効な状態で **add documents index** する方法を確認しましょう。

## クイック回答
- **“limit log file size” とは何ですか？** ログファイルの最大サイズを上限設定し、ディスク上での無制限な増大を防ぎます。  
- **どのロガーがログファイルサイズを制限できますか？** 組み込みの `FileLogger` は max‑size パラメータを受け取ります。  
- **console logger java はどう使いますか？** `ConsoleLogger` をインスタンス化し、`IndexSettings` に設定します。  
- **GroupDocs.Search のライセンスは必要ですか？** 評価にはトライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **最初のステップは何ですか？** Maven プロジェクトに GroupDocs.Search の依存関係を追加します。  

## ログファイルサイズを制限するとは？
ログファイルサイズを制限するとは、ロガーを設定してファイルが事前に定義されたしきい値（例: 4 MB）に達したら、これ以上サイズが増えないかロールオーバーさせることを意味します。これにより、アプリケーションのストレージ使用量が予測可能になり、パフォーマンス低下を防げます。

## GroupDocs.Search でファイルロガーとカスタムロガーを使用する理由
- **監査性:** インデックス作成と検索イベントの永続的な記録を保持します。  
- **デバッグ:** 簡潔なログを確認することで問題を迅速に特定できます。  
- **柔軟性:** 永続的なファイルログと即時のコンソール出力（`use console logger`）のどちらかを選択できます。  

## 前提条件
- **GroupDocs.Search for Java** ≥ 25.4。  
- JDK 8 以上、IDE（IntelliJ IDEA、Eclipse など）。  
- 基本的な Java と Maven の知識。  

## GroupDocs.Search for Java の設定

以下のいずれかの方法でライブラリをプロジェクトに追加します。

**Maven 設定:**

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

**Direct Download:**  公式サイトから最新の JAR をダウンロードしてください: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### ライセンス取得
トライアルを取得するか、[ライセンスページ](https://purchase.groupdocs.com/temporary-license/) からライセンスを購入してください。

## GroupDocs.Search 用カスタムロガーの作成方法
GroupDocs.Search は `ILogger` インターフェイスの任意の実装をプラグインできるようにしています。`FileLogger` または `ConsoleLogger` を拡張することで、ログファイルのロールオーバーやリモート監視サービスへのメッセージ転送などの追加動作を実装できます。この柔軟性により、多くのチームが運用要件に合わせた **custom logger** ソリューションを **create custom logger** しています。

## File Logger でログファイルサイズを制限する方法
以下は、**configure file logger** して指定したサイズを超えないようにログファイルを設定する手順です。

### 1️⃣ 必要なパッケージのインポート
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ File Logger を使用した Index Settings の設定
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ インデックスの作成またはロード
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ インデックスへのドキュメント追加
```java
index.add(documentsFolder);
```

### 5️⃣ 検索クエリの実行
```java
SearchResult result = index.search(query);
```

**重要ポイント:** `FileLogger` コンストラクタの第2引数（`4.0`）はメガバイト単位で **set max log size** を定義し、**limit log file size** の要件に直接対応します。

## console logger java の使用方法
ターミナルで即時フィードバックが欲しい場合は、ファイルロガーをコンソールロガーに置き換えてください。

### 1️⃣ Console Logger のインポート
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Console Logger を使用した Index Settings の設定
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ インデックスの作成またはロード
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ ドキュメントの追加と検索の実行
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**ヒント:** コンソールロガーは開発時に最適です。各ログエントリを即座に出力し、インデックス作成と検索が期待通りに動作することを確認できます。

## 実用的な適用例
1. **Document Management Systems:** インデックスされたすべてのドキュメントの監査トレイルを保持します。  
2. **Enterprise Search Engines:** クエリのパフォーマンスとエラー率をリアルタイムで監視します。  
3. **Legal & Compliance Software:** 規制報告のために検索語句を記録します。  

## パフォーマンス上の考慮点
- **ログサイズ:** **set max log size** により、アプリケーションを遅くする可能性のある過剰なディスク使用を回避できます。  
- **非同期ロギング:** スループットを上げる必要がある場合は、ロガーを非同期キューでラップすることを検討してください（このガイドの範囲外）。  
- **メモリ管理:** `Index` オブジェクトが不要になったら解放し、JVM のフットプリントを低く保ちます。  

## よくある問題と解決策
- **ログパスにアクセスできない:** ディレクトリが存在し、アプリケーションに書き込み権限があることを確認してください。  
- **ロガーが作動しない:** `Index` オブジェクトを作成する *前に* `settings.setLogger(...)` を呼び出していることを確認してください。  
- **コンソール出力がない:** `System.out` が表示されるターミナルでアプリケーションを実行していることを確認してください。  

## よくある質問

**Q: `FileLogger` の第2パラメータは何を制御しますか？**  
A: ログファイルの最大サイズ（メガバイト単位）を設定し、**set max log size** が可能になります。

**Q: ファイルロガーとコンソールロガーを組み合わせられますか？**  
A: はい、メッセージを両方の宛先に転送するカスタムロガーを作成すれば可能です。

**Q: 初期作成後にインデックスにドキュメントを追加するには？**  
A: 任意のタイミングで `index.add(pathToNewDocs)` を呼び出せば、ロガーが操作を記録します。

**Q: `ConsoleLogger` はスレッドセーフですか？**  
A: `System.out` に直接書き込むため、JVM が同期化しており、ほとんどのユースケースで安全です。

**Q: ログファイルサイズを制限すると、保存される情報量に影響しますか？**  
A: サイズ上限に達すると、新しいエントリが破棄されるか、ロガー実装に応じてファイルが **roll over log file** される可能性があります。

## リソース
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](httpshttps://reference.groupdocs.com/search/java/)

---

**最終更新日:** 2026-02-24  
**テスト環境:** GroupDocs.Search for Java 25.4  
**作者:** GroupDocs  

---