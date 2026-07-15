---
date: '2026-05-28'
description: GroupDocs.Search for Java kullanarak wildcard patterns ile ifadeyi nasıl
  arayacağınızı öğrenin. search index oluşturma, belge ekleme ve exact phrase ve wildcard
  queries yürütme konularını içerir.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: GroupDocs.Search for Java ile Joker Karakterli İfade Arama
type: docs
url: /tr/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# GroupDocs.Search for Java'da Joker Karakterli İfade Arama

Modern belge‑odaklı uygulamalarda, **ifade arama** hızlı ve doğru bir şekilde yapılması, kullanıcı deneyimi için belirleyici bir faktördür. Bilgi tabanı, e‑ticaret kataloğu ya da uyumluluk‑odaklı bir depo oluşturuyor olun, tam bir ifadeyi—veya esnek bir varyasyonunu—bulabilme yeteneği, kullanıcıların üretkenliğini artırır ve destek maliyetlerini azaltır. Bu öğretici, **GroupDocs.Search for Java** kurulumunu, arama indeksinin oluşturulmasını, belgelerin yüklenmesini ve hem tam‑ifade hem de joker‑karakter destekli sorguların çalıştırılmasını, net, üretim‑hazır kod parçacıklarıyla adım adım gösterir.

## Hızlı Yanıtlar
- **İfade aramalarının temel faydası nedir?** Kelime sırası ve yakınlığının kesin eşleşmesi, yalnızca tam diziyi içeren belgelerin döndürülmesini garanti eder.  
- **Bir ifade içinde joker karakterler kullanılabilir mi?** Evet—joker karakterler, genel sıralamayı korurken kelimeleri atlamanıza veya değiştirmenize izin verir.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme çalışır; üretim dağıtımları için tam lisans gereklidir.  
- **Hangi Maven sürümünü kullanmalıyım?** En son GroupDocs.Search for Java sürümü (örneğin, yazım sırasında 25.4).  
- **Bu yaklaşım büyük belge setleri için uygun mu?** Kesinlikle—GroupDocs.Search, indeks optimize edildiğinde, yüz binlerce belge koleksiyonunu alt saniyelik sorgu gecikmesiyle işleyebilir.

## “ifade arama” nedir?
**Bir ifadeyi aramak, bir belgede belirli bir kelime dizisini aramak anlamına gelir.**  
Bir ifade sorgusu yürüttüğünüzde, motor kelimelerin tam sırayla ve tanımlı yakınlıkta göründüğünü kontrol eder, farklı bağlamda aynı kelimeleri içeren alakasız sonuçları eleyerek. Bu, ifade aramalarını yasal maddeler, ürün kodları veya sıralamanın önemli olduğu herhangi bir metin bulmak için ideal kılar.

## Neden GrupDocs.Search'i İfade ve Joker Karakter Sorguları İçin Kullanmalısınız?
GroupDocs.Search, tipik sunucu donanımında **1 milyon belgeye kadar yüksek verimli indeksleme ve alt saniyelik sorgu yanıt süreleri** sağlar. Sorgu dili, tam ifadeler, basit `*` ve `?` joker karakterler ve sayısal aralıklar (`*2~5`) gibi gelişmiş desenleri destekler. Kütüphane, Maven veya doğrudan JAR indirme yoluyla herhangi bir Java uygulamasıyla bütünleşir ve dış hizmetlere ihtiyaç duymadan Java 8+ üzerinde çalışır.

## Önkoşullar
- Java 8 veya daha yeni (Java 11 LTS önerilir).  
- Maven 3 veya üzeri (bağımlılık yönetimini tercih ediyorsanız).  
- Java proje yapısı ve nesne‑yönelimli kavramlara temel aşinalık.  

## GroupDocs.Search for Java'i Kurma

### Maven Kullanarak
Resmi depoyu ve GroupDocs.Search bağımlılığını `pom.xml` dosyanıza ekleyin:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Doğrudan İndirme
Alternatif olarak, resmi sürüm sayfasından en son JAR'ı indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinme
- **Ücretsiz Deneme:** Hızlı deneyler için ideal; indekslenen veri 100 MB ile sınırlıdır.  
- **Geçici Lisans:** GroupDocs portalından 30‑günlük değerlendirme anahtarı talep edin.  
- **Tam Lisans:** Üretim kullanımı ve sınırsız indeksleme kapasitesi için gereklidir.

## Temel Başlatma ve Kurulum
İndeks dosyalarını tutacak bir klasör oluşturun ve `Index` nesnesini örnekleyin. `Index` sınıfı, disk üzerinde depolanan aranabilir indeksi temsil eder ve belgeleri ekleme, güncelleme ve sorgulama yöntemleri sağlar.

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

Aranabilir hale getirmek istediğiniz belgeleri ekleyin:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## GroupDocs.Search'te Joker Karakterli İfade Arama
Bu bölüm, üç düzeyde ifade aramayı gösterir—tam eşleşme, basit joker karakter ve gelişmiş joker karakter desenleri—bir indeks oluşturmayı, belgeleri eklemeyi ve her sorgu türünü özlü Java kodu ile yürütmeyi. Örnekler, hem metin‑tabanlı sorguları hem de nesne‑tabanlı sorgu oluşturmayı göstererek geliştiricilerin uygulamalarına esnek arama yetenekleri entegre etmelerini sağlar.

### Basit İfade Arama

#### Genel Bakış
Bir kelime dizisinin **tam eşleşmesi** gerektiğinde, örneğin yasal bir madde veya ürün model numarası gibi, bu yaklaşımı kullanın.

#### Doğrudan Cevap
İndeksi yükleyin, `search` metodunu tırnak içinde bir ifadeyle (ör. `"quick brown fox"`) çağırın ve motor yalnızca bu tam diziyi içeren belgeleri, kelime sırasını ve boşlukları koruyarak döndürür. Sorgu, yüz binlerce dosya içeren indekslerde bile milisaniyeler içinde çalışır.

#### Adım 1: Bir İndeks Oluşturun
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Adım 2: Belgeleri İndekse Ekleyin
```java
Index index = new Index(indexFolder);
```

#### Adım 3: Belirli Bir İfadeyi (Metin Formu) Ara
```java
index.add(documentsFolder);
```

#### Adım 4: Nesne‑Tabanlı Sorgular (Tam İfade Ara)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Joker Karakterli İfade Arama

#### Genel Bakış
Joker karakter yer tutucuları (`*` herhangi bir karakter sayısı için, `?` tek bir karakter için) çevredeki sıralamayı korurken **değişken kelimeleri atlamanıza** izin verir.

#### Doğrudan Cevap
Tırnak içinde bir ifadeye joker karakter (`*`) ekleyin—ör. `"quick * fox"`—ve *quick* ile *fox* arasındaki herhangi bir kelimeyi eşleştirin. Motor, joker karakteri sorgu zamanında genişletir, yalnızca desene uyan indekslenmiş terimleri tarar; bu da performansı düz bir ifade sorgusuna benzer tutar.

#### Adım 1: Bir İndeks Oluşturun
*(Basit İfade Arama ile aynı.)*

#### Adım 2: Belgeleri İndekse Ekleyin
*(Basit İfade Arama ile aynı.)*

#### Adım 3: Joker Karakterli Metin Formu Arama
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Adım 4: Joker Karakterli Nesne‑Tabanlı Sorgular (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Gelişmiş Joker Karakter Arama

#### Genel Bakış
Sayısal aralıkları, isteğe bağlı karakterleri ve özel regex‑benzeri desenleri birleştirerek **gelişmiş eşleşme** elde edin; örneğin sürüm numaraları veya ürün kodları gibi.

#### Doğrudan Cevap
İzin verilen kelime mesafesi aralığını tanımlamak için genişletilmiş joker karakter sözdizimini `*min~max` kullanın veya tek bir karakteri eşleştirmek için `?` kullanın. Örneğin, `"error *2~5 code"` ifadesi *error* kelimesini takip eden iki ila beş kelimeyi ve ardından *code* kelimesini bulur. Bu kesinlik, yanlış pozitifleri azaltırken hâlâ esneklik sunar.

#### Adım 1: Bir İndeks Oluşturun
*(Açıklık için tekrarlanmıştır.)*

#### Adım 2: Belgeleri İndekse Ekleyin
*(Açıklık için tekrarlanmıştır.)*

#### Adım 3: Karmaşık Joker Karakter Desenleriyle Metin Formu Arama
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Adım 4: Gelişmiş Joker Karakterli Nesne‑Tabanlı Sorgular
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Pratik Uygulamalar
- **İçerik Yönetim Sistemleri:** Editörler, yüzlerce sayfayı manuel olarak taramadan tam maddeleri veya esnek alıntıları bulabilir.  
- **E‑ticaret Katalogları:** Alıcılar, bir tanımlamayı atlasalar ya da eş anlamlı kelimeler kullansalar bile, joker karakter toleransı sayesinde ürünleri bulabilir.  
- **Hukuk & Uyum:** Sözleşmelerde küçük varyasyonlarla ortaya çıkabilecek sözleşme dilini hızlıca izole edin.  

## Performans Düşünceleri
- **Arama İndeksini Oluşturun** yalnızca kararlı belge seti başına bir kez; tüm sorgular için aynı `Index` örneğini yeniden kullanın.  
- **Belgeleri Artımlı Ekleyin** yeni dosyalar geldiğinde—CPU kullanımını düşük tutmak için tüm indeksi yeniden oluşturmayı önleyin.  
- **Kesin Joker Karakter Desenleri Tasarlayın**; daha geniş desenler (`*`) terim genişlemelerinin sayısını artırır ve CPU yükünü yükseltebilir.  
- **`index.optimize()`** metodunu periyodik olarak (destekleniyorsa) çağırarak indeksi sıkıştırın ve bellek tüketimini kontrol altında tutun.  

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| Joker karakter sorgusu için sonuç dönmüyor | Joker karakter sözdizimini (`*min~max`) doğrulayın ve hedef kelimelerin tanımlı mesafe içinde mevcut olduğundan emin olun. |
| Dosya güncellemelerinden sonra indeks eski hale geliyor | `index.add(updatedFolder)` metodunu veya artımlı güncelleme API'sini kullanarak yalnızca değişen dosyaları yenileyin. |
| Büyük veri setlerinde yüksek bellek tüketimi | JVM yığınını artırın (`-Xmx4g` veya daha yüksek) ve paralel işleme için indeksi birden fazla parçaya bölmeyi düşünün. |

## Sıkça Sorulan Sorular

**S: Joker karakter ile ifade araması arasındaki fark nedir?**  
C: İfade araması tam kelime sırası ve boşluk gerektirirken, joker karakter bu sıradaki kelimeleri değiştirme veya atlama imkanı sunar ve esnek eşleşme sağlar.

**S: Aramalarda sayısal verilerle joker karakter kullanabilir miyim?**  
C: Evet—joker karakter aralık parametreleri (`*min~max`) sayılar ve kelimeler için çalışır, `"version *1~3"` gibi sorgulara olanak tanır.

**S: Çok büyük belge koleksiyonlarıyla nasıl başa çıkmalıyım?**  
C: İndeksi optimize tutun, artımlı güncellemeler yapın ve terim genişlemesini sınırlamak için belirli joker karakter desenleri oluşturun. GroupDocs.Search, standart donanımda sorgu gecikmesini 200 ms altında tutarak 1 milyon belgeyi indeksleyebilir.

**S: GroupDocs.Search gerçek‑zamanlı arama senaryoları için uygun mu?**  
C: Kesinlikle—indeks oluşturulduktan sonra sorgular milisaniyeler içinde çalışır, bu da etkileşimli arama kutuları ve otomatik tamamlama özellikleri için idealdir.

**S: Bu kütüphaneyi mevcut bir Java projesine entegre edebilir miyim?**  
C: Evet. Maven bağımlılığını veya JAR'ı ekleyin, gösterildiği gibi `Index` nesnesini örnekleyin ve mevcut kodu değiştirmeden sorgulamaya hazırsınız.

**Last Updated:** 2026-05-28  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## İlgili Eğitimler

- [Java için Arama İndeksi Oluşturma – GroupDocs.Search Eğitimleri](/search/java/)
- [İndekse Belge Ekleme – GroupDocs.Search Java Eğitimleri](/search/java/document-management/)
- [Arama İndeksi Oluşturma - GroupDocs.Search Java Eğitimleri](/search/java/advanced-features/)