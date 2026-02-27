---
date: '2026-01-11'
description: GroupDocs.Search for Java を使用してカスタム検索インデックスを作成し、通常文字とブレンド文字を設定して高度な OCR
  と画像検索を実現する方法を学びましょう。
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: 文字認識を使用したカスタム検索インデックスの作成 – GroupDocs.Search Java
type: docs
url: /ja/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# 文字認識を使用したカスタム検索インデックスの作成（GroupDocs.Search for Java）

現代の文書が大量に扱われるアプリケーションでは、**カスタム検索インデックスの作成**が、ハイフン、アンダースコア、言語固有の記号などテキストのニュアンスを理解できることが、迅速かつ正確な検索に不可欠です。このチュートリアルでは、**GroupDocs.Search for Java** における文字認識の設定方法を、通常文字（文字、数字、アンダースコア）と混合文字（例：ハイフン）の両方をカバーしながら解説します。最後まで読むと、OCR や画像検索シナリオの正確な要件に合わせたインデックスを作成できるようになります。

## クイック回答
- **「create custom search index」とは何ですか？** インデックスを構成し、特定の記号を無視せずに文字または混合文字として扱うことを意味します。  
- **使用されているライブラリはどれですか？** GroupDocs.Search for Java（執筆時点のバージョンは v25.4）。  
- **ライセンスは必要ですか？** 開発には無料トライアルで十分ですが、本番環境では有料ライセンスが必要です。  
- **PDF と画像の両方をインデックスできますか？** はい。適切に構成すれば、GroupDocs.Search は画像と PDF の OCR をサポートします。  
- **Maven は必須ですか？** 依存関係の管理には Maven が推奨されますが、Gradle や手動で JAR を使用することも可能です。  

## カスタム検索インデックスとは？
カスタム検索インデックスを使用すると、検索エンジンが文字をどのように解釈するかを定義できます。デフォルトでは多くの記号が無視されるため、ケース番号（`ABC-123`）やコードスニペット（`my_variable`）などの一致が見逃されることがあります。アルファベット辞書を調整することで、エンジンが検索対象のテキストとして扱うものを完全にコントロールできます。

## なぜ通常文字と混合文字を設定するのか？
- **Regular characters**（文字、数字、アンダースコア）は単独のトークンとして扱われ、完全一致検索が向上します。  
- **Blended characters**（ハイフン、スラッシュ）は単語を結合します。これらを設定することで不要なトークン分割を防ぎ、法的参照、製品コード、ソースコードのインデックス作成に重要です。  

## 前提条件
- **JDK 8** 以上がインストールされていること。  
- **Maven** が依存関係管理に使用できること。  
- **GroupDocs.Search for Java** ライブラリへのアクセス（Maven または公式サイトからダウンロード）。  

### 必要なライブラリと依存関係
`pom.xml` にリポジトリと依存関係のエントリを追加します（以下参照）。XML ブロックは変更せずにそのままにしてください。

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

最新の JAR は [GroupDocs.Search for Java リリース](https://releases.groupdocs.com/search/java/) からもダウンロードできます。

### ライセンス取得
- **Free Trial** – 初期の実験に最適です。  
- **Temporary License** – 長期の開発サイクルに便利です。  
- **Production License** – 商用展開には必須です。  

公式ポータルからライセンスを取得してください: [GroupDocs](https://purchase.groupdocs.com/temporary-license/)。  

### 基本的な初期化
以下のスニペットは空のインデックスを作成するために必要な最小コードを示しています。そのまま保持してください。後でこの上に構築します。

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## GroupDocs.Search for Java の設定

### Maven でのインストール
*Prerequisites* セクションの Maven 設定がすべてです。追加したら `mvn clean install` を実行してバイナリを取得してください。

### 環境設定要件
- **index folder** と **document folder** がディスク上に存在することを確認してください。  
- 絶対パスを使用するか、IDE が相対パスを正しく解決するように設定してください。  

## 実装ガイド
以下では、**regular characters** と **blended characters** の 2 つの機能を順に解説します。各機能は同じパターンに従います—パスを定義し、インデックスを作成し、文字辞書を設定し、最後にドキュメントをインデックスします。

### 機能 1 – 通常文字

#### 概要
通常文字は独立したトークンとして扱われます。数字、文字、アンダースコアをそのまま検索可能にしたい場合に最適です。

#### 手順実装

**1️⃣ Set Up Paths**  
インデックスの保存場所とソースドキュメントの場所を定義します。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
インデックスをインスタンス化し、既存のアルファベット設定をクリアします。

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
数字、ラテン文字、アンダースコアを含む文字配列を作成します。

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index Documents**  
ソースフォルダー内のすべてのファイルを新しく構成したインデックスに追加します。

```java
index.add(documentFolder);
```

### 機能 2 – 混合文字

#### 概要
混合文字（ハイフンなど）はしばしば2つの単語を結びつけます。これらを *blended* とマークすると、インデックス作成時にエンジンは周囲のトークンを一緒に保持します。

#### 手順実装

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
ここでは、ハイフンを混合文字として扱うよう辞書に指示します。

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## 実用的な応用例

### ユースケース 1 – 法務文書管理
法務文書には `2023-AB-456` のようなケース番号が含まれることが多いです。アンダースコアとハイフンを設定することで、識別子が分割されずに正確な一致が検索されます。

### ユースケース 2 – ソースコードリポジトリ
開発者は、アンダースコア（`my_variable`）やハイフン（`my-function`）が意味を持つコードスニペットを検索する必要があります。カスタム文字認識により、検索エンジンがこれらの記号を尊重します。

### ユースケース 3 – 多言語データセット
追加のアルファベットを使用する言語を扱う場合、通常文字セットにそれらの Unicode 範囲を拡張でき、正確な多言語検索結果が保証されます。

## パフォーマンス考慮事項
- **Resource Management** – ヒープ使用量に注意してください。大規模インデックスはインクリメンタルコミットで恩恵を受けます。  
- **Garbage Collection** – 終了時に `Index` オブジェクトを解放し、JVM にメモリ回収させます。  
- **Index Optimization** – 定期的に `index.optimize()`（利用可能な場合）を呼び出してインデックスを圧縮し、クエリ速度を向上させます。  

## 結論
これで、GroupDocs.Search for Java を使用して **custom search index** を作成し、通常文字と混合文字を区別できるようになりました。この細かな制御により、法務、開発、または多言語環境に合わせた OCR 対応の高性能検索ソリューションを構築できます。

**次のステップ**  
- ラテン文字以外のアルファベット用に追加の Unicode 範囲を試してみてください。  
- 文字設定をステミングや同義語など、他の GroupDocs.Search 機能と組み合わせます。  
- インデックスを REST API に統合し、フロントエンドアプリケーションに検索機能を提供します。

## よくある質問

**Q:** *`CharacterType.Letter` の目的は何ですか？*  
**A:** インデックスに対し、提供された文字を通常の文字として扱うよう指示し、インデックス作成時に個別にトークン化されます。

**Q:** *同じインデックスで通常文字と混合文字を混在させられますか？*  
**A:** はい。各タイプに対して `setRange` を呼び出すだけで、辞書は両方の設定を同時に処理します。

**Q:** *アルファベットを変更した後、インデックスを再構築する必要がありますか？*  
**A:** 必要です。文字辞書の変更はトークン化に影響するため、新しいルールを適用するにはドキュメントを再インデックスする必要があります。

**Q:** *定義できるカスタム文字の数に制限はありますか？*  
**A:** ライブラリは Unicode 全域をサポートしていますが、非常に大量の文字を追加するとパフォーマンスが低下する可能性があるため、実際に必要な文字に限定してください。

**Q:** *これが OCR の精度にどのように影響しますか？*  
**A:** インデックスの文字セットを OCR エンジンの出力と合わせることで、偽陰性を減らし、検索の関連性全体を向上させます。

---

**最終更新日:** 2026-01-11  
**テスト環境:** GroupDocs.Search 25.4 for Java  
**作者:** GroupDocs