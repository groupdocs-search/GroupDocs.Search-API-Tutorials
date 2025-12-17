---
date: '2025-12-16'
description: Java'da arama indeksi oluşturmayı ve GroupDocs.Search kullanarak katmanlı
  ve karmaşık aramaları uygulamayı öğrenin, arama performansını ve kullanıcı deneyimini
  artırın.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Java ile Arama Dizini Oluşturma – Facetli ve Karmaşık Aramalar
type: docs
url: /tr/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Java’da Arama Dizini Oluşturma – Faceted ve Karmaşık Aramalar

Java’da güçlü bir **search experience** (arama deneyimi) uygulamak göz korkutucu olabilir, özellikle büyük belge koleksiyonlarını yöneten **create search index Java** projelerine ihtiyaç duyduğunuzda. Neyse ki, **GroupDocs.Search for Java** birkaç satır kodla faceted ve karmaşık sorgular oluşturmanıza olanak tanıyan zengin bir API sunar. Bu öğreticide kütüphaneyi nasıl kuracağınızı, **create a search index Java** (arama dizini oluşturma) işlemini, belgeleri eklemeyi ve hem basit faceted aramaları hem de sofistike çok‑kriterli sorguları nasıl çalıştıracağınızı keşfedeceksiniz.

## Hızlı Yanıtlar
- **Faceted arama nedir?** Önceden tanımlanmış kategorilere (ör. dosya türü, tarih) göre sonuçları filtrelemenin bir yolu.  
- **Java’da arama dizini nasıl oluşturulur?** Bir klasöre işaret eden bir `Index` nesnesi başlatın ve belgeleri ekleyin.  
- **Birden fazla kriteri birleştirebilir miyim?** Evet—nesne‑tabanlı sorgular veya metin sorgusunda Boolean operatörleri kullanın.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme çalışır; ticari lisans sınırlamaları kaldırır.  
- **Hangi IDE en iyisi?** Herhangi bir Java IDE (IntelliJ IDEA, Eclipse, NetBeans) sorunsuz çalışır.

## “create search index java” nedir?
Java’da bir arama dizini oluşturmak, belge meta verilerini ve içeriğini depolayan, kullanıcı sorgularına göre hızlı geri getirme sağlayan bir aranabilir veri yapısı inşa etmek anlamına gelir. GroupDocs.Search ile dizin diskte bulunur, artımlı olarak güncellenebilir ve faceting ve karmaşık Boolean mantığı gibi gelişmiş özellikleri destekler.

## Faceted ve karmaşık sorgular için neden GroupDocs.Search kullanılmalı?
- **Out‑of‑the‑box faceting** – dosya adı, boyut veya özel meta veri gibi alanlara göre filtreleme.  
- **Rich query language** – AND/OR/NOT operatörlerini kullanarak metin, ifade ve alan sorgularını karıştırma.  
- **Scalable performance** – milyonlarca belgeyi indekslerken arama gecikmesini düşük tutar.  
- **Pure Java** – yerel bağımlılık yoktur, JDK 8+ çalışan herhangi bir platformda çalışır.

## Ön Koşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- **JDK 8 veya daha yeni bir sürüm** IDE’nizde yüklü ve yapılandırılmış.  
- **Maven** (veya Gradle) bağımlılık yönetimi için.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Java OOP kavramları ve Maven proje yapısı hakkında temel bilgi.

## GroupDocs.Search for Java Kurulumu

### Maven Kurulumu
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

### Doğrudan İndirme
Alternatif olarak, resmi sürüm sayfasından en son JAR dosyasını indirin:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Lisans Edinimi
Tam işlevselliği açmak için:

1. **Free trial** – geliştirme ve test için mükemmeldir.  
2. **Temporary evaluation license** – deneme sınırlamalarını uzatır.  
3. **Commercial license** – üretim kullanımında tüm kısıtlamaları kaldırır.

### Temel Başlatma ve Kurulum
Aşağıdaki kod parçacığı, `Index` sınıfını örnekleyerek **create a search index Java** (arama dizini oluşturma) işlemini nasıl yapacağınızı gösterir:

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

Dizin hazır olduğunda, gerçek dünya faceted ve karmaşık sorgularına geçebiliriz.

## create search index java – Basit Faceted Arama

Faceted arama, son kullanıcıların önceden tanımlanmış kategorilerden (facets) değerler seçerek sonuçları daraltmasını sağlar. Aşağıda adım adım bir rehber bulunmaktadır.

### Adım 1: Bir Dizin Oluşturun
İlk olarak, `Index`i dizin dosyalarının saklanacağı bir klasöre yönlendirin.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Adım 2: Belgeleri Dizi̇ne Ekleyin
GroupDocs.Search’e kaynak belgelerinizin nerede olduğunu söyleyin. Desteklenen tüm dosya türleri (PDF, DOCX, TXT, vb.) otomatik olarak indekslenecektir.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Adım 3: İçerik Alanında Metin Sorgusuyla Arama Yapın
Hızlı bir metin sorgusu `content` alanına göre filtreler. `content: Pellentesque` sözdizimi, gövde metninde *Pellentesque* kelimesini içeren belgelerle sonuçları sınırlar.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Adım 4: Nesne Sorgusu Kullanarak Arama Yapın
Nesne‑tabanlı sorgular size ayrıntılı kontrol sağlar. Burada bir kelime sorgusu oluşturup, bir alan sorgusuna sarar ve yürütürüz.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## create search index java – Karmaşık Sorgu Araması

Karmaşık sorgular birden fazla alan, Boolean operatörleri ve ifade aramalarını birleştirir. Bu, e‑ticaret filtreleri veya hukuki belge araştırmaları gibi senaryolar için idealdir.

### Adım 1: Karmaşık Sorgular İçin Bir Dizin Oluşturun
Aynı klasör yapısını yeniden kullanın; dizini hem basit hem de karmaşık senaryolar arasında paylaşabilirsiniz.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Adım 2: Metin Sorgusuyla Arama Yapın
Aşağıdaki sorgu, *lorem* **ve** *ipsum* adlı dosyaları **veya** iki tam ifadeden birini içeren içeriği arar.

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

### Adım 3: Nesne Sorgusu ile Arama Yapın
Nesne‑tabanlı yapı, metinsel sorguyu yansıtır ancak tip güvenliği ve IDE desteği sağlar.

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

## Faceted ve Karmaşık Aramaların Pratik Uygulamaları

| Senaryo | Faceting Nasıl Yardımcı Olur | Örnek Sorgu |
|----------|-------------------|---------------|
| **E‑ticaret kataloğu** | Kategori, fiyat, marka göre filtreleme | `category: Electronics AND price:[100 TO 500]` |
| **Hukuki belge deposu** | Dava numarası, yargı bölgesi göre daraltma | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Araştırma arşivleri** | Yazar, yayın yılı, anahtar kelimeleri birleştirme | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Kurumsal intranet** | Dosya türü ve departmana göre arama | `filetype: pdf AND department: HR` |

## Yaygın Tuzaklar ve Sorun Giderme
- **Boş sonuçlar** – Belgelerin başarıyla eklendiğini doğrulayın (`index.getDocumentCount()` yardımcı olabilir).  
- **Eski dizin** – Dosyaları ekledikten veya sildikten sonra, dizinin senkronize kalması için `index.update()` çağırın.  
- **Yanlış alan adları** – Yazım hatalarını önlemek için `CommonFieldNames` sabitlerini (`Content`, `FileName`, vb.) kullanın.  
- **Performans darboğazları** – Büyük koleksiyonlar için `index.setCacheSize()` etkinleştirmeyi veya dizin klasörü için ayrı bir SSD kullanmayı düşünün.

## Sıkça Sorulan Sorular

**Q: GroupDocs.Search'ı Spring Boot ile kullanabilir miyim?**  
A: Kesinlikle. Maven bağımlılığını ekleyin, dizini bir Spring bean olarak yapılandırın ve gerektiği yerde enjekte edin.

**Q: Kütüphane özel meta veri alanlarını destekliyor mu?**  
A: Evet – indeksleme sırasında kullanıcı tanımlı alanlar ekleyebilir ve ardından bunlar üzerinde faceting yapabilirsiniz.

**Q: Dizin ne kadar büyüyebilir?**  
A: Dizin disk tabanlıdır ve milyonlarca belgeyi işleyebilir; yeterli depolama alanı sağladığınızdan ve önbellek ayarlarını izlediğinizden emin olun.

**Q: Sonuçları alaka düzeyine göre sıralamanın bir yolu var mı?**  
A: GroupDocs.Search otomatik olarak eşleşmeleri puanlar; puanı `SearchResult.getDocument(i).getScore()` ile alabilirsiniz.

**Q: Şifreli PDF'leri indekslersem ne olur?**  
A: Belgeyi eklerken şifreyi sağlayın: `index.add(filePath, password)`.

## Sonuç

Artık GroupDocs.Search ile **create a search index Java** (arama dizini oluşturma) konusunda rahat hissetmelisiniz, belgeleri ekleyebilir ve hem basit faceted sorgular hem de sofistike Boolean aramaları oluşturabilirsiniz. Bu yetenekler, e‑ticaret platformlarından kurumsal bilgi tabanlarına kadar geniş bir uygulama yelpazesinde hızlı, doğru ve kullanıcı dostu arama deneyimleri sunmanızı sağlar.

Bir sonraki adıma hazır mısınız? **GroupDocs.Search**'in **highlighting**, **suggestions** ve **real‑time indexing** gibi gelişmiş özelliklerini keşfederek uygulamanızın arama gücünü daha da artırın.

---

**Son Güncelleme:** 2025-12-16  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs