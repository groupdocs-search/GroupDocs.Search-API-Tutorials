---
date: '2026-08-10'
description: GroupDocs.Search for Java kullanarak belgeleri nasıl index edeceğinizi
  ve belgeleri indexe eklemeyi öğrenin. text ve object sorgularıyla güçlü search apps
  oluşturun.
keywords:
- how to index documents
- create search index
- index pdf files
- search word documents
- update search index
lastmod: '2026-08-10'
og_description: 'GroupDocs.Search for Java ile belgeleri nasıl index edeceğinizi öğrenin.
  Adım adım rehber: bir search index oluşturma, PDFs, Word, Excel dosyalarını ekleme
  ve fast queries çalıştırma.'
og_image_alt: Code example showing Java indexing with GroupDocs.Search
og_title: GroupDocs.Search for Java ile belgeleri index etme – Hızlı search guide
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  headline: How to index documents with GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  name: How to index documents with GroupDocs.Search for Java
  steps:
  - name: '**Free trial** – explore the library without cost.'
    text: '**Free trial** – explore the library without cost.'
  - name: '**Temporary license** – request a short‑term key for extended evaluation.'
    text: '**Temporary license** – request a short‑term key for extended evaluation.'
  - name: '**Purchase** – obtain a full license for production use.'
    text: '**Purchase** – obtain a full license for production use.'
  - name: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
    text: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
  - name: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
    text: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
  - name: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
    text: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
  type: HowTo
- questions:
  - answer: Call `index.add("NEW_DOCUMENT_PATH")` again; the library merges the new
      entries without recreating the whole index.
    question: How do I update an existing index with new documents?
  - answer: Yes, it supports 30+ formats—including PDF, DOCX, XLSX, PPTX, TXT, and
      HTML—so you can index virtually any business document.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Java 8+ runtime, at least 2 GB RAM for modest collections (larger sets
      benefit from 4 GB+), and read/write access to the index folder.
    question: What are the system requirements for using GroupDocs.Search?
  - answer: Keep the index up‑to‑date, profile your queries, and review JVM memory
      settings. Reducing the number of indexed fields or using object queries can
      also speed up execution.
    question: How can I troubleshoot search performance issues?
  - answer: Yes, you can enable synonym dictionaries and fuzzy search via the `SearchOptions`
      class to broaden matching without sacrificing relevance. The `SearchOptions`
      class configures advanced search behavior such as synonyms and fuzzy matching.
    question: Is there support for synonyms or fuzzy matching?
  type: FAQPage
tags:
- document indexing
- GroupDocs.Search
- Java search library
- search API
- indexing tutorial
title: GroupDocs.Search for Java ile belgeleri index etme
type: docs
url: /tr/java/searching/master-document-search-groupdocs-java/
weight: 1
---

# GroupDocs.Search for Java ile belgeleri nasıl indeksleyebilirsiniz

Günümüzün veri odaklı dünyasında, **belgeleri nasıl indeksleyebilirsiniz** verimli bir şekilde büyük dosya koleksiyonlarıyla çalışan her Java geliştiricisi için kritik bir beceridir. İster yasal sözleşmeler, finansal raporlar ya da iç raporlar üzerinde çalışıyor olun, iyi tasarlanmış bir arama indeksi, saatler süren manuel tarama yerine saniyeler içinde tam olarak ihtiyacınız olan bilgiyi bulmanızı sağlar. Bu eğitim, GroupDocs.Search for Java ile bir arama indeksi oluşturmayı, belgeleri eklemeyi ve hem metin‑tabanlı hem de nesne‑tabanlı sorgular çalıştırmayı adım adım gösterir.

## Hızlı cevaplar
- **Belgeleri indekslemek için ilk adım nedir?** `Index` örneği oluşturun ve bu örnek indeks dosyalarının saklanacağı bir klasöre işaret etsin.  
- **Hangi yöntem bir indekse belgeleri ekler?** `index.add("PATH_TO_DOCUMENTS")` metodunu çağırarak bir dizini tarayın ve desteklenen dosyaları içe aktarın.  
- **Sayısal aralıkları arayabilir miyim?** Evet – `"400 ~~ 4000"` gibi bir metin sorgusu kullanın veya `SearchQuery.createNumericRangeQuery` aracılığıyla bir nesne sorgusu yapın. `createNumericRangeQuery` yöntemi bir sayısal aralık sorgu nesnesi oluşturur.  
- **Bir lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme sürümü yeterlidir; ticari bir lisans tam özellik setini açar ve kullanım sınırlamalarını kaldırır.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya üzeri desteklenir.

## GroupDocs.Search ile belgeleri nasıl indeksleyebileceğimiz nedir?
Belgeleri indekslemek, her dosya için aranabilir bir token deposu oluşturur ve motorun her seferinde orijinal dosyaları okumadan eşleşmeleri almasını sağlar. Bu ön işleme adımı, ham içeriği milisaniyeler içinde sorgulanabilen optimize bir indekse dönüştürür. İndeks, terimleri, konumları ve meta verileri saklar ve tüm desteklenen belge türlerinde hızlı ifade ve yakınlık aramaları yapmayı mümkün kılar.

## GroupDocs.Search for Java neden kullanılmalı?
Arama işlemleri genellikle standart 2‑CPU, 8 GB VM üzerinde çalışan 10 000 dosyadan (ortalama 1 KB) oluşan bir koleksiyonda 50 ms'den az sürede tamamlanır. Kütüphane **30+ giriş ve çıkış formatını**—PDF, DOCX, XLSX, PPTX, TXT ve HTML dahil—destekler, böylece ek dönüştürücülere ihtiyaç duymadan neredeyse her iş belgesini indeksleyebilirsiniz. Esnek API'si, düz metin sorgularını, sayısal aralıkları ve karmaşık nesne sorgularını birleştirmenize olanak tanırken, artımlı güncellemeler tüm indeksi yeniden oluşturmak zorunda kalmadan yeni dosyalar eklemenizi sağlar.

## Önkoşullar
- Maven, bağımlılık yönetimi için kurulu olmalı.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Temel Java bilgisi (OOP kavramları, istisna yönetimi).  

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
Ayrıca en son JAR dosyasını [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Lisans edinme adımları
1. **Ücretsiz deneme** – kütüphaneyi maliyetsiz keşfedin.  
2. **Geçici lisans** – genişletilmiş değerlendirme için kısa vadeli bir anahtar isteyin.  
3. **Satın al** – üretim kullanımı için tam lisans edinin.

## Temel başlatma ve kurulum
İndekse **belgeleri eklemek** için, önce indeks dosyalarının saklanacağı klasöre işaret eden bir `Index` nesnesi oluşturmalısınız:

`Index`, diskteki aranabilir bir indeksi temsil eden temel sınıftır.  
```java
import com.groupdocs.search.Index;

// Initialize the index by specifying a directory path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");
```

Bu satır, belgeleri almaya hazır bir indeksi (oluşturur veya açar).

## Uygulama rehberi
### Belgeleri oluşturma ve indeksleme
#### İndekse belgeleri nasıl eklenir
`add` yöntemi bir klasörü tarar ve her dosya için aranabilir verileri depolar. Desteklenen tüm belgeleri özyinelemeli olarak işler, metin ve meta verileri çıkarır ve daha önce belirttiğiniz indeks klasörüne tokenları yazar.

```java
import com.groupdocs.search.Index;

// Initialize an index at the specified path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");

// Add documents from a directory for indexing
index.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Parametreler:** Yol dizesi, indekslemek istediğiniz dosyaları içeren klasöre işaret eder.  
- **Amaç:** Bu adımın ardından indeks, tüm desteklenen belge türlerinden tokenlar içerir ve tüm koleksiyon üzerinde hızlı aramaları mümkün kılar.

## Metin sorgu araması
#### Metin tabanlı sayısal aralık araması nasıl yapılır
Aralık tanımlayan basit bir dize kullanarak arama yapabilirsiniz. Motor, `~~` operatörünü “arasında” olarak yorumlar ve belirtilen sınırlar içindeki sayıları içeren tüm belgeleri döndürür.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define a query for numeric values within a specific range
String query1 = "400 ~~ 4000";

// Execute text-based search on indexed data
SearchResult result1 = index.search(query1);
```

- **Parametreler:** `"400 ~~ 4000"` sorgu dizesi, motoru 400 ile 4000 arasındaki sayıları bulmaya yönlendirir.  
- **Dönüş değeri:** `SearchResult`, eşleşen belgelerin listesini tutar ve eşleşen parçaları vurgular.

## Nesne sorgu araması
#### Sayısal aralıklar için nesne sorgusu nasıl kullanılır
Nesne tabanlı sorgular, arama kriterleri üzerinde programatik kontrol sağlar, birden fazla koşulu birleştirmenize veya çalışma zamanında dinamik olarak sorgular oluşturmanıza olanak tanır.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Create a numeric range query object
SearchQuery query2 = SearchQuery.createNumericRangeQuery(400, 4000);

// Perform search using the query object
SearchResult result2 = index.search(query2);
```

- **Parametreler:** `createNumericRangeQuery`, başlangıç ve bitiş tam sayılarını alır.  
- **Amaç:** Bu yöntem, fatura tutarları, yaşlar veya ürün kodları gibi sayısal alanlara göre sonuçları filtrelemeniz gerektiğinde idealdir.

## Pratik uygulamalar
İşte **belgeleri nasıl indeksleyebilirsiniz** oyunu değiştiren bazı gerçek dünya senaryoları:

1. **Hukuki belge yönetimi** – binlerce sözleşme içinde maddeleri, dava numaralarını veya tarihleri saniyeler içinde bulun.  
2. **Finansal raporlama** – her bir elektronik tabloyu taramadan belirli bir para aralığına giren işlemleri çekin.  
3. **Envanter takibi** – dağıtık bir dosya sisteminde seri numaraları, parti kodları veya SKU aralıklarıyla öğeleri bulun.

GroupDocs.Search'ü veritabanları, bulut depolama veya mesaj kuyruklarıyla entegre etmek, belge iş akışlarını daha da otomatikleştirebilir.

## Performans değerlendirmeleri
- **Düzenli indeks güncellemeleri:** Yeni dosyalar için indeksi taze tutmak amacıyla `index.add` komutunu yeniden çalıştırın.  
- **Kaynak yönetimi:** Yığın kullanımını izleyin; büyük indeksler, ayarlanmış JVM çöp toplama ayarlarından fayda sağlar.  
- **Sorgu optimizasyonu:** Gereksiz taramaları azaltmak ve yanıt süresini iyileştirmek için karmaşık filtrelerde nesne sorgularını kullanın.

## Yaygın sorunlar ve çözümler
| Sorun | Neden oluşur | Çözüm |
|-------|----------------|-----|
| **Arama sonuç vermiyor** | İndeks oluşturulmamış veya klasör yolu yanlış | `index.add`'in doğru dizinde çalıştırıldığını ve indeks klasörünün yazılabilir olduğunu doğrulayın. |
| **İndeksleme sırasında OutOfMemoryError** | Çok büyük dosyalar veya yetersiz yığın | JVM `-Xmx` değerini artırın veya dosyaları daha küçük partiler halinde indeksleyin. |
| **Desteklenmeyen dosya formatı** | Dosya türü GroupDocs.Search tarafından tanınmıyor | Uzantının desteklenen listede (PDF, DOCX, XLSX, PPTX, TXT, HTML, vb.) olduğundan emin olun. |

## Sıkça sorulan sorular
**Q: Mevcut bir indeksi yeni belgelerle nasıl güncellerim?**  
A: `index.add("NEW_DOCUMENT_PATH")` metodunu tekrar çağırın; kütüphane yeni girdileri bütün indeksi yeniden oluşturmadan birleştirir.

**Q: GroupDocs.Search farklı dosya formatlarını işleyebilir mi?**  
A: Evet, PDF, DOCX, XLSX, PPTX, TXT ve HTML dahil 30+ formatı destekler; böylece neredeyse her iş belgesini indeksleyebilirsiniz.

**Q: GroupDocs.Search kullanmak için sistem gereksinimleri nelerdir?**  
A: Java 8+ çalışma zamanı, orta ölçekli koleksiyonlar için en az 2 GB RAM (daha büyük setler 4 GB+ fayda sağlar) ve indeks klasörüne okuma/yazma erişimi.

**Q: Arama performans sorunlarını nasıl gideririm?**  
A: İndeksi güncel tutun, sorgularınızı profilleyin ve JVM bellek ayarlarını gözden geçirin. İndekslenen alan sayısını azaltmak veya nesne sorguları kullanmak da yürütmeyi hızlandırabilir.

**Q: Eşanlamlılar veya bulanık eşleşme desteği var mı?**  
A: Evet, `SearchOptions` sınıfı aracılığıyla eşanlamlı sözlüklerini ve bulanık aramayı etkinleştirebilirsiniz; bu, alaka düzeyini kaybetmeden eşleşmeyi genişletir. `SearchOptions` sınıfı, eşanlamlılar ve bulanık eşleşme gibi gelişmiş arama davranışlarını yapılandırır.

---

**Son Güncelleme:** 2026-08-10  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [GroupDocs.Search kullanarak Java'da Meta Veri İndeksleme ile belgelere nasıl eklenir](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [GroupDocs.Search for Java'da Belgeleri İndekse Eklemek ve Takma Adları Yönetmek](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
- [GroupDocs.Search ile Java'da İndeksi Güncelleme – Kapsamlı Rehber](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)