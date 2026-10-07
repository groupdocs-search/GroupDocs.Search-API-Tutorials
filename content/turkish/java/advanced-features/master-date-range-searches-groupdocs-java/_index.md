---
date: '2026-10-07'
description: GroupDocs ile custom date format java aramalarını nasıl uygulayacağınızı
  öğrenin; date range queries, custom patterns ve performance tips konularını kapsar.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: Custom date format java öğreticisi, GroupDocs.Search for Java'ı nasıl
  yapılandıracağınızı, date range queries çalıştırmayı ve performance artırmayı gösterir.
  Adım adım örnekleri izleyin.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Custom date format java – GroupDocs ile date range search rehberi
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Custom date format java | GroupDocs ile tarih aralığı araması
type: docs
url: /tr/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Özel tarih formatı java | tarih aralığı araması GroupDocs ile

Tarihine göre belge arama, arşiv sistemi, finansal raporlama aracı veya içerik‑yönetim portalı oluşturuyor olsanız da sık karşılaşılan bir gereksinimdir. Bu öğreticide GroupDocs.Search kullanarak **custom date format java** tekniklerini öğrenecek, tarih aralığı sorgularını, özel desen tanımlarını ve **optimize search performance** ipuçlarını kapsayacaksınız. Sonunda, kullanıcıların kullandıkları formata bakılmaksızın herhangi bir tarih aralığındaki kayıtları alabilmelerini sağlayacaksınız.

## Hızlı cevaplar
- **İndeksleme için birincil sınıf nedir?** `Index` from the `com.groupdocs.search` package.  
- **Özel bir tarih deseni nasıl tanımlanır?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Metin sorgusuyla arama yapabilir miyim?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Hangi Maven koordinatları gereklidir?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Geliştirme için lisansa ihtiyacım var mı?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## custom date format java nedir?
Custom date format java, GroupDocs.Search'e varsayılan ISO desenini (YYYY‑MM‑DD) takip etmeyen tarih dizelerini nasıl yorumlayacağını söyler. Kendi deseninizi—örneğin `MM/dd/yyyy` veya `dd‑MM‑yyyy`—tanımlayarak, motorun bölgesel veya eski formatları kullanan belgelerde gömülü tarihleri tanımasını sağlarsınız. Bu yetenek, tarih‑merkezli aramalarda hatırlama ve kesinliği artırarak, heterojen kaynaklar arasında tarihleri tutarlı bir şekilde indekslemenize ve sorgulamanıza olanak tanır.

## Neden tarih aralığı sorguları için GroupDocs.Search kullanmalısınız?
GroupDocs.Search, yüksek hızlı indekslemeyi esnek sorgu oluşturmayla birleştirerek tarih‑aralığı senaryoları için ideal hale getirir. Motor, belirtilen bir aralık içinde tarih içeren belgeleri, bu tarihlerin serbest metin ya da meta veri alanlarında bile bulunması durumunda hızlı bir şekilde bulabilir. Birden çok dosya formatı için yerleşik destek ve özelleştirilebilir tarih ayrıştırıcıları, format‑özel kod yazmadan çeşitli belge koleksiyonlarını yönetmenizi sağlar ve büyük indekslerde alt‑saniyelik yanıt süreleri elde etmenize olanak tanır.

## GroupDocs.Search ile tarihine göre belgeleri nasıl ararsınız
Kütüphaneyi kuracak, örnek bir klasörü indeksleyecek ve ardından hem basit metin‑form sorgularını hem de daha zengin nesne‑tabanlı sorguları çalıştıracaksınız. Süreç, bir `Index` örneği oluşturmak, ihtiyacınız olan özel tarih formatlarını yapılandırmak ve ardından arama API'sini düz bir dize ya da yapılandırılmış bir `SearchQuery` ile çağırmakla başlar. Bu yaklaşım, uygulamanızın gereksinimlerine uygun kontrol seviyesini seçmenizi sağlar.

### Önkoşullar
- Java 8 veya daha yeni bir sürüm yüklü.  
- Bağımlılık yönetimi için Maven.  
- GroupDocs.Search lisansına erişim (deneme veya geçici lisans geliştirme için çalışır).  

### GroupDocs.Search for Java kurulumu

#### Maven ile kurulum
Add the repository and dependency to your `pom.xml`:

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

#### Doğrudan indirme
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Temel başlatma ve kurulum
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** `Index` sınıfı, eklediğiniz her dosya için aranabilir meta verileri depolayan temel kapsayıcıdır ve büyük koleksiyonlarda hızlı aramaları mümkün kılar.

## Özellik 1: tarih aralığı arama sorguları oluşturma

### Metin form sorgusu kullanma
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** İndeksinizi yükleyin, ardından `search("daterange(2022-01-01 ~~ 2022-12-31)")` çağrısını yaparak 1 Ocak 2022 ile 31 Aralık 2022 arasında indekslenmiş tarihleri olan her belgeyi alın. Bu tek‑satırlık sorgu kutudan çıktığı gibi çalışır ve sonuçları alaka düzeyine göre sıralar.

**Explanation:** `daterange` sözdizimi tarihleri `YYYY‑MM‑DD` formatında bekler. Aralık içinde indekslenmiş tarihleri olan tüm belgeleri döndürür.

### Sorgu nesnesi kullanma
Programatik kontrol ve özel ayrıştırma için bir `SearchQuery` nesnesi oluşturun. `SearchQuery` sınıfı, anahtar kelimeler, filtreler ve tarih aralıkları gibi birden çok kriteri birleştirebilen yapılandırılmış bir sorguyu temsil eder.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** `startDate` ve `endDate` `java.util.Date` örnekleri olan `createDateRangeQuery(startDate, endDate)` ile bir `SearchQuery` oluşturun; ardından sorguyu `index.search(query)`'ye geçirerek zaman dilimi farklarını ve yerel takvimleri dikkate alan kesin sonuçlar elde edin.

**Definition anchor:** `SearchQuery` sınıfı tüm arama kriterlerini kapsüller ve tarih aralıklarını anahtar kelime filtreleri, Boolean operatörleri ve artırma kurallarıyla birleştirmenize olanak tanır.

**Explanation:** `createDateRangeQuery`, `java.util.Date` nesneleri sağlamanıza izin verir ve zaman dilimleri ve yerel‑özel işleme konusunda tam esneklik sunar.

## Özellik 2: custom date format java desenlerini belirleme

### Özel tarih formatlarını ayarlama
The `DateFormat` class tells the engine how to split and interpret a date string based on element order and separator characters. Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** Varsayılan formatları `dateFormat.clear()` ile temizleyin, ardından `DateFormatElement` nesnelerinden (ay, gün, yıl) oluşturulan yeni bir `DateFormat` ekleyin ve ayırıcıyı `/` olarak ayarlayın. Bundan sonra motor, indeksleme ve sorgulama sırasında `MM/dd/yyyy` biçiminde yazılmış tarihleri doğru bir şekilde ayrıştıracaktır.

**Definition anchor:** `DateFormat`, GroupDocs.Search'e bir tarih dizesini öğe sırasına ve ayırıcı karakterlere göre nasıl bölüp yorumlayacağını söyleyen bir yapılandırma nesnesidir.

**Explanation:** Varsayılan formatları temizleyip `/` ayırıcıyı kullanan bir `DateFormat` ekleyerek, motor artık `MM/dd/yyyy` biçiminde yazılmış tarihleri anlar. Bu, ay‑öncelikli gösterimi tercih eden bölgelerde **search documents by date** için esastır.

## Arama performansını optimize etme ipuçları
- **Index incrementally:** Yeni dosyaları sıfırdan yeniden oluşturmak yerine mevcut indekse ekleyin; bu, günlük güncellemeler için CPU kullanımını %70'e kadar azaltır.  
- **Prune stale data:** Periyodik olarak artık ihtiyaç duyulmayan belgeleri kaldırın; hafif bir indeks önbellek isabet oranını artırır ve sorgu gecikmesini azaltır.  
- **Adjust memory settings:** 5 GB'den büyük indekslerle çalışırken JVM yığınını (`-Xmx4g` veya daha yüksek) artırarak bellek dışı hatalardan kaçının.  
- **Enable multi‑threaded indexing:** `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` kullanarak belge işleme paralel hale getirin ve indeksleme süresini CPU çekirdek sayısı kadar azaltın.

## Yaygın sorunlar ve çözümler
- **Date parsing errors:** Belgenin tarih dizelerinin tanımladığınız özel desenle tam olarak eşleştiğini doğrulayın; uyumsuz ayırıcılar veya eksik önde gelen sıfırlar hatalara neden olur.  
- **Missing results:** İndekslenen alanların tarih meta verisi içerdiğinden emin olun; bir belge yalnızca serbest metin paragraflarında tarih içeriyorsa, indeksleme sırasında `ExtractDateMetadata` seçeneğini etkinleştirin.  
- **Index access exceptions:** `indexFolder` yolunun yazılabilir ve başka bir işlem tarafından kilitli olmadığını doğrulayın; çakışmaları önlemek için ortam başına (dev, test, prod) ayrı bir klasör kullanın.

## Pratik uygulamalar
1. **Arşiv sistemleri** – Tarihleri manuel olarak normalleştirmeden belirli bir tarihsel dönemden kayıtları alın.  
2. **İçerik yönetimi** – Avrupa kullanıcıları için `dd/MM/yyyy` gibi bölgesel tarih formatlarını destekleyerek kullanıcı memnuniyetini artırın.  
3. **Finansal yazılım** – İşlemleri mali çeyrek veya yıla göre hızlıca filtreleyerek gerçek zamanlı raporlama panolarını etkinleştirin.

## Neden bu önemli
**custom date format java** işleme uygulamak, belgeler arasında tutarsız tarih temsilleriyle uğraşmanın getirdiği zorluğu ortadan kaldırır. Tek bir indeks içinde **handle multiple date formats** yapmanıza olanak tanır ve son kullanıcıların tarihlerin orijinal kaydediliş şekli ne olursa olsun doğru sonuçlar almasını sağlar. Bu esneklik, arama alakasını artırır, ön işleme çabasını azaltır ve tarih‑merkezli uygulamalar için değer‑zamanını kısaltır.

## Sonraki adımlar
- `AND`, `OR` ve `NOT` operatörlerini kullanarak daha gelişmiş sorgu kombinasyonlarını keşfedin.  
- XML etiketlerine gömülü zaman damgaları gibi ek zaman meta verilerini indekslemeniz gerekiyorsa özel analizörlerle deney yapın.  
- Resmi belgelerdeki performans ayarlama kılavuzunu inceleyerek çözümünüzü milyonlarca belge ve çok kiracılı ortamlar için ölçeklendirin.

## Sıkça sorulan sorular

**S: Metin formu ile nesne‑tabanlı tarih sorguları arasındaki fark nedir?**  
C: Metin formu hızlı ve kolaydır ancak varsayılan ISO formatıyla sınırlıdır; nesne‑tabanlı sorgular, daha fazla esneklik için `Date` nesneleri ve özel formatlar sağlamanıza izin verir.

**S: Tek bir sorguda birden fazla tarih aralığını arayabilir miyim?**  
C: Evet, `daterange` ifadelerini `AND` veya `OR` gibi mantıksal operatörlerle birleştirerek karmaşık sorgular oluşturabilirsiniz.

**S: Özel tarih formatları aramayı yavaşlatır mı?**  
C: Ek ayrıştırma için küçük bir ek yük vardır, ancak tipik iş yükleri için etkisi önemsizdir ve doğruluk kazançlarıyla dengelenir.

**S: GroupDocs.Search büyük ölçekli dağıtımlar için uygun mu?**  
C: Kesinlikle. Uygun indeksleme stratejileri ve JVM ayarlamalarıyla, milyonlarca belgeye ölçeklenir ve alt‑saniyelik sorgu yanıt sürelerini korur.

**S: Daha fazla Java örneği nerede bulunabilir?**  
C: Ek örnekler ve kullanım senaryosu uygulamaları için [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) adresini inceleyin.

---

**Kaynaklar**
- **Dokümantasyon:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API referansı:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **İndirme:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub deposu:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **GitHub'ta görüntüle:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ücretsiz destek forumu:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Geçici lisans:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-10-07  
**Test Edilen:** GroupDocs.Search Java 25.4  
**Yazar:** GroupDocs  

## İlgili Öğreticiler
- [Groupdocs Search Java Gelişmiş Arama Özellikleri](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Java Tam Metin Arama Kütüphanesi – GroupDocs.Search ile İndeksi Optimize Et](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [GroupDocs.Search kullanarak Java'da Meta Veri İndeksleme ile belgeleri indekse ekleme](/search/java/indexing/groupdocs-search-java-metadata-indexing/)