---
date: '2026-08-26'
description: Boolean operators Java'ın hızlı bir arama indeksi oluşturmanıza, Java
  içerik araması yapmanıza ve GroupDocs.Search ile faceted queries çalıştırmanıza
  nasıl olanak sağladığını öğrenin.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Boolean operators Java'ın hızlı bir arama indeksi oluşturmanıza, Java
  içerik araması yapmanıza ve GroupDocs.Search ile faceted queries yürütmenize nasıl
  olanak sağladığını öğrenin.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – arama indeksi oluşturun ve faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – arama indeksi oluşturun & faceted search
type: docs
url: /tr/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean operators Java – arama indeksi oluşturma ve faceted arama

Java'da güçlü bir **search experience** uygulamak göz korkutucu olabilir, özellikle faceted ve karmaşık sorgular için **boolean operators Java** destekleyen **create a search index Java** yapmanız gerektiğinde. Bu öğreticide **GroupDocs.Search for Java**'ı kurmayı, bir indeks oluşturmayı, belgeler eklemeyi ve hem basit faceted aramaları hem de Boolean mantığını kullanan gelişmiş çok‑kriterli sorguları nasıl oluşturacağınızı adım adım göstereceğiz. Sonunda **content search Java**, **filename search Java** ve hatta **update index Java** işlemlerini nasıl kullanarak verilerinizi güncel tutacağınızı anlayacaksınız.

## Hızlı cevaplar
- **Faceted arama nedir?** Dosya türü veya tarih gibi önceden tanımlanmış kategorilere göre sonuçları filtrelemenin bir yoludur.  
- **Java'da bir arama indeksi nasıl oluştururum?** Bir klasöre işaret eden bir `Index` nesnesi başlatın ve belgeleri ekleyin.  
- **Birden fazla kriteri boolean operatörleriyle birleştirebilir miyim?** Evet—nesne‑tabanlı sorgular veya metin sorgusundaki Boolean operatörlerini kullanın.  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme çalışır; ticari lisans limitleri kaldırır.  
- **Hangi IDE en iyisi?** IntelliJ IDEA, Eclipse, NetBeans gibi herhangi bir Java IDE yeterlidir.

## “create search index java” nedir?

Java'da bir arama indeksi oluşturmak, belge metni ve meta verileri depolayan, sorgular aracılığıyla eşleşen belgelerin anında alınmasını sağlayan disk‑tabanlı bir yapı inşa etmek anlamına gelir. İndeks, terimleri belge tanımlayıcılarına eşler, hızlı aramaları destekler ve dosyalar değiştikçe artımlı olarak güncellenebilir, böylece güçlü arama özelliklerinin temelini oluşturur.

## Faceted ve karmaşık sorgular için GroupDocs.Search neden kullanılmalı?

GroupDocs.Search for Java, faceting, Boolean sorgu desteği ve yüksek performanslı indeksleme sunar; tipik sunucu donanımında sorgu gecikmesini 200 ms altında tutarak 10 milyon belgeye kadar işleyebilir. Kutudan çıkar çıkmaz alan filtreleri, zengin sorgu dili ve saf Java uyumluluğu sağlar, bu da kurumsal ölçekli arama senaryoları için idealdir.

## Önkoşullar

- **JDK 8 veya daha yeni** IDE'nizde kurulu ve yapılandırılmış.  
- **Maven** (veya Gradle) bağımlılık yönetimi için.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Java OOP kavramları ve Maven proje yapısı hakkında temel bilgi.

## GroupDocs.Search for Java kurulumu

### Maven kurulumu
`pom.xml` dosyanıza depo ve bağımlılığı ekleyin:

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

### Doğrudan indirme
Alternatif olarak, resmi sürüm sayfasından en son JAR'ı indirin:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Lisans edinme
Tam işlevselliği açmak için:

1. **Ücretsiz deneme** – geliştirme ve test için mükemmeldir.  
2. **Geçici değerlendirme lisansı** – deneme limitlerini genişletir.  
3. **Ticari lisans** – üretim kullanımında tüm kısıtlamaları kaldırır.

### Temel başlatma ve kurulum
`Index` sınıfı, disk üzerinde depolanan aranabilir bir indeksi temsil eden temel bileşendir. Aşağıdaki kod parçacığı, `Index` sınıfını örnekleyerek **create a search index Java** nasıl yapılacağını gösterir:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## boolean operators java nasıl kullanılır – Basit faceted arama

İndeksinizi yükleyin, belgeler ekleyin ve bir alan sorgusu çalıştırın; iki‑adımlı desen, facet sayımlarını ve filtrelenmiş sonuçları tek bir çağrıda almanızı sağlar. Bu yaklaşım, kullanıcıların dosya türü, yazar veya özel meta veri gibi kategorilere göre sonuçları daraltmalarına sezgisel bir yol sunar.

### Adım 1: Bir indeks oluşturun
İlk olarak, `Index`i indeks dosyalarının saklanacağı bir klasöre yönlendirin.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Adım 2: Belgeleri indekse ekleyin
GroupDocs.Search'e kaynak belgelerinizin nerede olduğunu söyleyin. Desteklenen tüm dosya türleri (PDF, DOCX, TXT vb.) otomatik olarak indekslenecektir.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Adım 3: İçerik alanında metin sorgusuyla arama yapın
Hızlı bir metin sorgusu `content` alanına göre filtre uygular. `content: Pellentesque` sözdizimi, gövde metninde *Pellentesque* kelimesini içeren belgelerle sonuçları sınırlar.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Adım 4: Nesne sorgusuyla arama yapın
Nesne‑tabanlı sorgular size ayrıntılı kontrol sağlar. Burada bir kelime sorgusu oluşturur, bir alan sorgusuna sarar ve yürütürüz.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## boolean operators java nasıl kullanılır – Karmaşık sorgu araması

Karmaşık bir sorgu yürütmek için birden fazla alan koşulunu AND/OR/NOT operatörleriyle birleştirin ve isteğe bağlı olarak ifade aramaları ekleyin. Her koşulu alan sorguları ile belirtebilir, Boolean operatörleriyle iç içe geçirebilir ve artırma (boosting) ile alaka düzeyini kontrol edebilirsiniz; böylece tüm gerekli kriterleri karşılayan en alakalı belgeleri alırsınız.

### Adım 1: Karmaşık sorgular için bir indeks oluşturun
Aynı klasör yapısını yeniden kullanın; indeksi hem basit hem de karmaşık senaryolar arasında paylaşabilirsiniz.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Adım 2: Metin sorgusuyla arama yapın
Aşağıdaki sorgu, *lorem* **ve** *ipsum* **veya** iki tam ifadeden birini içeren içerikle dosyaları arar.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Adım 3: Nesne sorgusuyla arama yapın
Nesne‑tabanlı yapı, metinsel sorguya benzer ancak tip güvenliği ve IDE desteği sağlar.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Faceted ve karmaşık aramaların pratik uygulamaları

| Senaryo | Faceting nasıl yardımcı olur | Örnek sorgu |
|----------|-------------------|---------------|
| **E‑ticaret kataloğu** | Kategori, fiyat, marka ile filtreleme | `category: Electronics AND price:[100 TO 500]` |
| **Hukuki belge deposu** | Dava numarası, yargı bölgesi ile daraltma | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Araştırma arşivleri** | Yazar, yayın yılı, anahtar kelimeleri birleştirme | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Kurumsal intranet** | Dosya türü ve departmana göre arama | `filetype: pdf AND department: HR` |

Bu örnekler, **boolean operators java** ve **filename search java** tekniklerini ustaca kullanmanın veri‑yoğun uygulamalar için ne kadar büyük bir fark yarattığını gösterir.

## Yaygın tuzaklar ve sorun giderme

`SearchResult` nesnesi, bir sorguya uyan belgeleri içerir ve alaka puanlarına ve vurgulanan parçalara erişim sağlar.  
`CommonFieldNames` sınıfı, API genelinde kullanılan `Content` ve `FileName` gibi standart alan adlarını tanımlar.

- **Boş sonuçlar** – Belgelerin başarıyla eklendiğini doğrulayın (`index.getDocumentCount()` yardımcı olabilir).  
- **Eski indeks** – Dosyaları ekledikten veya sildikten sonra `index.update()` çağırarak **update index java** yapın ve indeksi senkronize tutun.  
- **Yanlış alan adları** – `CommonFieldNames` sabitlerini (`Content`, `FileName` vb.) kullanarak yazım hatalarından kaçının.  
- **Performans darboğazları** – Büyük koleksiyonlar için `index.setCacheSize()` etkinleştirmeyi veya indeks klasörü için ayrı bir SSD kullanmayı düşünün.  
- **Vurgulama eksik** – **highlight search results java** için eşleşen parçaları `SearchResult.getFragments()` ile alın (burada gösterilmemiştir ancak API'de mevcuttur).  

## Sıkça sorulan sorular

**S: GroupDocs.Search'i Spring Boot ile kullanabilir miyim?**  
C: Kesinlikle. Maven bağımlılığını ekleyin, indeksi bir Spring bean olarak yapılandırın ve arama yeteneklerine ihtiyaç duyduğunuz her yerde enjekte edin.

**S: Kütüphane özel meta veri alanlarını destekliyor mu?**  
C: Evet – indeksleme sırasında kullanıcı tanımlı alanlar ekleyebilir ve ardından bunlar üzerinde faceting yapabilirsiniz.

**S: İndeks ne kadar büyüyebilir?**  
C: Disk‑tabanlı indeks 10 milyon belgeye kadar dayanabilir; yeterli depolama sağladığınızdan ve önbellek ayarlarını izlediğinizden emin olun.

**S: Sonuçları alaka düzeyine göre sıralamanın bir yolu var mı?**  
C: GroupDocs.Search eşleşmeleri otomatik olarak puanlar; puanı `SearchResult.getDocument(i).getScore()` ile alabilirsiniz.

**S: Şifreli PDF'leri indekslersem ne olur?**  
C: Belgeyi eklerken şifreyi sağlayın: `index.add(filePath, password)`.

## Sonuç

Artık GroupDocs.Search ile **create a search index Java** oluşturma, belgeler ekleme ve hem basit faceted sorgular hem de **boolean operators java** kullanan gelişmiş Boolean aramaları yapma konusunda rahat hissetmelisiniz. Bu yetenekler, e‑ticaret platformlarından kurumsal bilgi tabanlarına kadar geniş bir uygulama yelpazesinde hızlı, doğru ve kullanıcı‑dostu arama deneyimleri sunmanızı sağlar.

Bir sonraki adıma hazır mısınız? **GroupDocs.Search**'in **highlighting**, **suggestions** ve **real‑time indexing** gibi gelişmiş özelliklerini keşfederek uygulamanızın arama gücünü daha da artırın.

---

**Last Updated:** 2026-08-26  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## İlgili Öğreticiler

- [Wildcard Search Java with GroupDocs.Search – Gelişmiş Özellikler](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [GroupDocs.Search ile Index Java Güncelleme – Kapsamlı Rehber](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Java tam metin araması nasıl uygulanır: GroupDocs.Search ile indeks dizini oluşturma](/search/java/indexing/groupdocs-search-java-create-index/)