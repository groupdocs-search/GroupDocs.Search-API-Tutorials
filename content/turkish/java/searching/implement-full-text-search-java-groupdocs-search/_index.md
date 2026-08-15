---
date: '2026-08-15'
description: Java'da GroupDocs.Search ile bir Full text search örneğini öğrenin; belgeleri
  index'e ekleme, boolean query java ve performance optimization konularını kapsar.
keywords:
- full text search example
- add documents to index
- boolean query java
lastmod: '2026-08-15'
og_description: Java'da GroupDocs.Search ile bir Full text search örneğini keşfedin.
  Belgeleri index'e eklemeyi, boolean query java ifadelerini oluşturmayı ve boost
  search performance öğrenin.
og_image_alt: Guide showing how to implement a full text search example in Java with
  GroupDocs.Search
og_title: Java'da GroupDocs.Search kullanarak Full text search örneği
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  headline: Full text search example in Java using GroupDocs.Search
  type: TechArticle
- description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  name: Full text search example in Java using GroupDocs.Search
  steps:
  - name: create an index
    text: The `Index` class is the searchable container that stores indexed documents
      on disk.
  - name: add documents (add documents to index)
    text: You can index everything in a folder or limit to certain extensions using
      a `DocumentFilter`. > **Explanation:** > - `Index` represents the searchable
      database. > - `add()` ingests files; the wildcard `*.*` grabs all files, while
      `DocumentFilter` lets you fine‑tune the **add documents to index** ste
  - name: execute the search
    text: '> **Explanation:** > - `search()` runs the query against the index. > -
      `getDocumentCount()` tells you how many documents matched—useful for quick sanity
      checks.'
  type: HowTo
- questions:
  - answer: It indexes the raw text of every document so you can query any word or
      phrase instantly.
    question: What is full text search example?
  - answer: GroupDocs.Search for Java handles PDF, DOCX, XLSX, PPTX, HTML, TXT, and
      over 50 other file types.
    question: Which library supports multiple formats?
  - answer: Call the `index.add()` method with a folder path or a custom `DocumentFilter`.
    question: How do I add documents to index?
  - answer: Yes—combine terms with AND, OR, NOT for precise results.
    question: Can I run Boolean queries?
  - answer: Use incremental indexing, enable result caching, and disable phonetic
      search unless needed.
    question: How do I improve performance?
  type: FAQPage
tags:
- full text search
- GroupDocs.Search
- Java document indexing
- search performance
title: Java'da GroupDocs.Search kullanarak Full text search örneği
type: docs
url: /tr/java/searching/implement-full-text-search-java-groupdocs-search/
weight: 1
---

# Java ile GroupDocs.Search'te tam metin arama örneği

If you need a **full text search example** that works across PDFs, Word files, spreadsheets, and more, you’ve come to the right place. Manually scanning thousands of documents is a massive bottleneck, but GroupDocs.Search for Java automates indexing and querying with blazing speed. In this tutorial we’ll walk through everything you need to get up and running— from adding documents to index, crafting boolean query java statements, to optimizing search performance for production workloads.

## Hızlı cevaplar
- **Tam metin arama örneği nedir?** It indexes the raw text of every document so you can query any word or phrase instantly.  
- **Hangi kütüphane birden fazla formatı destekler?** GroupDocs.Search for Java handles PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 50 other file types.  
- **Nasıl belgeleri indekse eklerim?** Call the `index.add()` method with a folder path or a custom `DocumentFilter`.  
- **Boolean sorgularını çalıştırabilir miyim?** Yes—combine terms with AND, OR, NOT for precise results.  
- **Performansı nasıl artırabilirim?** Use incremental indexing, enable result caching, and disable phonetic search unless needed.

## Tam metin arama örneği nedir?
A full text search example lets you scan the entire textual content of documents, store it in an efficient index, and retrieve matching records instantly. Unlike filename‑only searches, it looks inside PDFs, Word docs, spreadsheets, and other supported formats, making it ideal for document management systems, support portals, and any application where users need to locate information quickly.

## Neden GroupDocs.Search for Java kullanmalısınız?
GroupDocs.Search for Java provides multi‑format support for over 50 file types, including PDF, DOCX, XLSX, PPTX, HTML and plain text. It scales to millions of files while keeping memory usage low by storing the index on disk. The library includes an advanced query language with built‑in Boolean, fuzzy and phonetic searches, and it integrates with a single Maven dependency, allowing you to start indexing within minutes.

## Önkoşullar
- **Java 11+** (Java 8 works, but Java 11 or later is recommended for better performance).  
- **Maven** for dependency management.  
- A **GroupDocs.Search** license (a free trial key is sufficient for development).  

### Gerekli kütüphaneler ve bağımlılıklar
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

For detailed usage see the [documentation](https://docs.groupdocs.com/search/java/).

### Ortam kurulumu
- Install the JDK (8 or newer) and configure `JAVA_HOME`.  
- Use an IDE such as IntelliJ IDEA or Eclipse for easier debugging.  

### Bilgi önkoşulları
- Basic Java programming concepts.  
- Familiarity with Maven’s `pom.xml` structure.  

## GroupDocs.Search for Java Kurulumu
You can bring in the library via Maven (shown above) or download the JAR manually.

### Doğrudan indirme (manuel kurulum tercih ediyorsanız)
Grab the latest package from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans edinme adımları
1. **Ücretsiz deneme** – Sign up and receive a temporary key.  
2. **Geçici lisans** – Request a longer‑term key for extended testing.  
3. **Satın alma** – Upgrade to a full commercial license when you’re ready for production.

### Temel başlatma ve kurulum
Create an index folder on disk and verify the library loads correctly:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index in the specified directory
        Index index = new Index("C:\\MyIndex");
        
        System.out.println("GroupDocs.Search initialized!");
    }
}
```

> **İpucu:** Sorgu gecikmesini azaltmak için indeks dizinini hızlı bir SSD'de tutun.

## Belgeleri indekse ekleme
**Neden önemli?**: İndekslenmiş içerik olmadan arama sonuçları mümkün değildir. Aşağıda tüm klasörleri nasıl ekleyeceğinizi veya belirli dosya türlerini nasıl filtreleyeceğinizi gösteriyoruz.

### Adım 1: indeks oluşturma
The `Index` class is the searchable container that stores indexed documents on disk.

```java
Index index = new Index("C:\\MyIndex");
```

### Adım 2: belgeleri ekle (belgeleri indekse ekle)
You can index everything in a folder or limit to certain extensions using a `DocumentFilter`.

```java
index.add("C:\\Documents\\*.*"); // Adds all documents from the specified directory
// For specific file types, use:
index.add("C:\\Reports", new DocumentFilter() {
    @Override
    public boolean accept(String fileName) {
        return fileName.endsWith(".pdf") || fileName.endsWith(".docx");
    }
});
```

> **Açıklama:**  
> - `Index` arama yapılabilir veritabanını temsil eder.  
> - `add()` dosyaları alır; `*.*` joker karakteri tüm dosyaları yakalar, `DocumentFilter` ise **belgeleri indekse ekle** adımını ince ayar yapmanıza olanak tanır.

## Arama gerçekleştirme (search documents java)
Now that the index holds data, you can query it.

### Adım 1: sorgu oluşturma
```java
String query = "GroupDocs";
```

### Adım 2: aramayı yürütme
```java
SearchResult result = index.search(query);
System.out.println("Documents found: " + result.getDocumentCount());
```

> **Açıklama:**  
> - `search()` sorguyu indeks üzerinde çalıştırır.  
> - `getDocumentCount()` kaç belgenin eşleştiğini söyler—hızlı doğrulama kontrolleri için faydalıdır.

## Gelişmiş sorgu teknikleri (boolean query java)
For precise control, combine terms with Boolean logic.

### Boolean sorgular
The `BooleanQuery` class lets you build complex expressions using AND, OR, NOT operators.

```java
String booleanQuery = "GroupDocs AND Java";
SearchResult booleanResult = index.search(booleanQuery);
```

### Fonetik aramalar (bulanık eşleşme için isteğe bağlı)
The `PhoneticSearch` feature enables phonetic matching for misspelled terms, but it adds overhead.

```java
index.getSettings().setPhoneticSearch(true);
```

> **Ne zaman kullanılmalı:** Kullanıcılar sık sık terimleri yanlış yazıyorsa fonetik aramayı etkinleştirin; aksi takdirde **arama performansını optimize** etmek için devre dışı bırakın.

## Yaygın sorunlar ve çözümler
| Problem | Neden oluşur | Çözüm |
|---------|----------------|-----|
| **Eksik belgeler** | Yanlış dosya yolu veya yetersiz izinler | Yolu doğrulayın ve okuma izni verin |
| **Yavaş sorgular** | Önbellekleme olmadan büyük indeks veya gereksiz fonetik arama | Önbelleği etkinleştirin, fonetik aramayı devre dışı bırakın ve indeksin bölünmesini düşünün |
| **Bellek dışı hatalar** | İndeks boyutu JVM yığınına aşırı | `-Xmx` değerini artırın veya artımlı indekslemeyi kullanın |

## Pratik uygulamalar
GroupDocs.Search gerçek dünya senaryolarında öne çıkar:

1. **İçerik yönetim sistemleri** – Makaleler, PDF'ler ve medya varlıkları üzerinde anlık tam metin arama sağlar.  
2. **Müşteri destek portalları** – Temsilciler ilgili kılavuzları veya politikaları saniyeler içinde bulabilir.  
3. **Kurumsal belge depoları** – Verileri ayrı bir veritabanına taşımadan sözleşmeler, raporlar ve uyum belgeleri arasında arama yapar.

## Performans değerlendirmeleri
### Arama performansını optimize etme
- **Artımlı indeksleme:** Tüm indeksi yeniden oluşturmak yerine yalnızca değişen dosyaları ekleyin veya güncelleyin.  
- **Önbellekleme:** Sık kullanılan sorgu sonuçlarını bellekte tutun.  
- **Kaynak izleme:** İndeks boyutuna göre JVM yığınını (`-Xmx2g` veya daha yüksek) ayarlayın.

### Kaynak kullanım yönergeleri
- İndeks klasörünü hızlı bir SSD veya NVMe sürücüde saklayın.  
- Toplu indeksleme sırasında CPU ve belleği izleyin; dalgalanmaları önlemek için toplu işlemleri yavaşlatın.

### Java bellek yönetimi için en iyi uygulamalar
- Akışlarla çalışırken `try‑with‑resources` kullanın.  
- Kullanım sonrası büyük nesneleri null yaparak çöp toplama yardımcı olun.

## Sonuç
Artık GroupDocs.Search kullanarak Java'da tam üretim hazır **full text search example**'a sahipsiniz. Kütüphaneyi kurmaktan, **belgeleri indekse ekleme**, **boolean query java** ifadeleri oluşturma, **arama performansını optimize etme**'ye kadar her adım kapsandı.  

### Sonraki adımlar
Explore deeper features such as custom analyzers, synonym dictionaries, and cloud‑storage integration by checking the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/).

---

## Sıkça sorulan sorular

**Q:** GroupDocs.Search hangi dosya formatlarını destekliyor?  
**A:** PDF, DOCX, XLSX, PPTX, HTML, TXT ve birçok görüntü türü dahil olmak üzere 50'den fazla format.

**Q:** Büyük veri setlerini nasıl yönetmeliyim?  
**A:** Bunları birden fazla indekse bölün, artımlı olarak güncelleyin ve gecikmeyi düşük tutmak için sonuç önbelleklemesini etkinleştirin.

**Q:** GroupDocs.Search bulut ortamlarında çalışabilir mi?  
**A:** Evet—indeks klasörünü bağlanmış bir bulut depolamaya (ör. Azure Blob, dosya sistemi sürücüsü üzerinden AWS S3) yönlendirebilirsiniz.

**Q:** GroupDocs.Search diğer kütüphanelere göre avantajları nelerdir?  
**A:** Çoklu format desteği, yerleşik Boolean/fonetik sorgular ve düşük bellek ayak iziyle milyonlarca belge işleyebilen hafif bir Java API'si.

**Q:** Performans sorunlarını nasıl gideririm?  
**A:** İndeks ayarlarını gözden geçirin, gerekmedikçe fonetik aramayı devre dışı bırakın ve indeksleme ve sorgulama sırasında JVM bellek/CPU kullanımını izleyin.

**Son Güncelleme:** 2026-08-15  
**Test Edilen Versiyon:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs  

## Kaynaklar
- **Dokümantasyon:** [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API referansı:** [API Reference Guide](https://reference.groupdocs.com/search/java)  
- **İndirme:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub:** [Source Code on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Destek:** [Forum and Community Support](https://forum.groupdocs.com/c/search/10)  
- **Lisans:** [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)

## İlgili Eğitimler

- [Java tam metin arama nasıl uygulanır: GroupDocs.Search ile indeks dizini oluşturma](/search/java/indexing/groupdocs-search-java-create-index/)
- [GroupDocs.Search for Java ile Belgeleri İndekse Ekleme](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [GroupDocs.Search Java ile Sorgu Performansını İyileştirme: İndeks ve Aramayı Optimize Etme](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)