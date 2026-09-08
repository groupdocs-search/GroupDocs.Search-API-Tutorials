---
date: '2026-07-26'
description: GroupDocs.Search Java'yı belgeleri hızlı bir şekilde aramak ve HTML previews
  içinde terimleri vurgulamak için uygulayın. Setup, indexing, fuzzy search ve result
  highlighting hakkında bilgi edinin.
keywords:
- implement groupdocs search java
- how to search documents java
- groupdocs search java highlighting
lastmod: '2026-07-26'
og_description: GroupDocs.Search Java'yı belgeleri hızlı bir şekilde aramak ve HTML
  previews içinde terimleri vurgulamak için uygulayın. Setup, indexing, fuzzy search
  ve result highlighting hakkında bilgi edinin.
og_image_alt: 'Guide: Implement GroupDocs.Search Java for document search and term
  highlighting'
og_title: Document Search için GroupDocs.Search Java'yı Uygulayın
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Implement GroupDocs.Search Java to search documents java quickly and
    highlight terms in HTML previews. Learn setup, indexing, fuzzy search, and result
    highlighting.
  headline: Implement GroupDocs.Search Java for Document Search
  type: TechArticle
- description: Implement GroupDocs.Search Java to search documents java quickly and
    highlight terms in HTML previews. Learn setup, indexing, fuzzy search, and result
    highlighting.
  name: Implement GroupDocs.Search Java for Document Search
  steps:
  - name: Create an Index
    text: 'The `Index` class is the top‑level object that stores searchable metadata
      on disk. Creating it points to a folder where all index files will reside:'
  - name: Configure Search Options (Enable fuzzy search)
    text: '`SearchOptions` lets you fine‑tune query behavior. Setting `FuzzySearch`
      to `true` enables approximate matching, which is useful for handling typos or
      OCR errors:'
  - name: Execute the Search
    text: '`Index.search` runs the query against the prepared index and returns a
      `SearchResult` collection containing matched documents and term occurrences:
      The `SearchResult` object contains the list of documents that match the query
      and their relevance scores.'
  - name: Extract Occurrences
    text: 'Each `SearchResult` item provides `getOccurrences()` which returns the
      exact positions of the query terms inside the source file, allowing you to build
      analytics dashboards or detailed reports:'
  - name: Set Up Index with High Compression
    text: 'High compression reduces storage by **up to 70 %** while keeping query
      speed within milliseconds. Adjust the `CompressionLevel` property before indexing:'
  - name: Perform Search and Highlight Results
    text: 'After executing the search, call `highlight()` on the `SearchResult` object
      to produce an HTML file that highlights every occurrence of the query term.
      The `highlight()` method generates an HTML preview with matched terms wrapped
      in `<mark>` tags:'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java SDK that indexes and searches text across more
      than 50 document formats, offering fuzzy matching and result highlighting.
    question: What is GroupDocs.Search?
  - answer: It tolerates a configurable number of character differences, allowing
      matches on misspelled words or OCR errors.
    question: How does fuzzy search work?
  - answer: Yes, a free trial is available, but a full license is required for production
      deployments.
    question: Can I use GroupDocs.Search without a license?
  - answer: PDF, DOCX, XLSX, PPTX, TXT, and many more—see the official docs for the
      complete list.
    question: What file formats are supported?
  - answer: Serve the generated HTML file directly or embed its content into a page
      using an `<iframe>` or server‑side rendering.
    question: How do I display highlighted results in a web application?
  type: FAQPage
tags:
- implement groupdocs search java
- search documents java
- groupdocs search
- java document indexing
- highlight search terms
title: Document Search için GroupDocs.Search Java'yı Uygulayın
type: docs
url: /tr/java/searching/implement-groupdocs-search-java-document-search/
weight: 1
---

# GroupDocs.Search Java'yı Belge Araması için Uygulama

Günümüzün veri odaklı ortamında, **implement groupdocs search java** hızlı ve güvenilir tam metin araması gerektiren PDF'ler, Word dosyaları, elektronik tablolar ve daha fazlası üzerinde hayati öneme sahiptir. İster bir hukuk‑sözleşme deposu, ister akademik araştırma portalı, ister müşteri‑destek bilgi tabanı oluşturuyor olun, bu öğretici SDK'yı kurmaktan, bir indeks oluşturmaktan, bulanık sorgular çalıştırmaktan ve vurgulanan arama terimleriyle HTML üretmekten—tüm bunları Java ile—size rehberlik eder.

## Hızlı Cevaplar
- **Hangi kütüphane groupdocs search java'yı uygulamaya yardımcı olur?** GroupDocs.Search for Java.  
- **Sonuçlarda java arama terimlerini vurgulayabilir miyim?** Evet—oluşturulan HTML, eşleşmeleri otomatik olarak `<mark>` etiketleriyle sarabilir.  
- **Üretim için lisansa ihtiyacım var mı?** Ücretsiz deneme mevcuttur; ticari kullanım için tam lisans gereklidir.  
- **Hangi IDE en iyisi?** Herhangi bir Java IDE—IntelliJ IDEA, Eclipse veya VS Code.  
- **Maven destekleniyor mu?** Kesinlikle—depolar ve bağımlılıkları `pom.xml` dosyanıza ekleyin.

## GroupDocs.Search for Java Nedir?

`GroupDocs.Search` bir Java SDK'sıdır ve **50+ belge formatı** (PDF, DOCX, XLSX, PPTX, TXT, vb.) üzerinde metni indeksler ve arar, tüm dosyayı belleğe yüklemeden. Bulanık eşleşme, Boolean operatörleri, ifade sorguları ve yerleşik sonuç vurgulama sunar, bu da aranabilir belge depoları için hazır bir çözümdür.

## GroupDocs.Search ile Java Belge Araması Neden Kullanılır?

İndeksli aramalarla 10 k belge için sonuçları 10 ms'den kısa sürede döndürerek hız sağlar, bulanık arama, Boolean mantığı, ifade sorguları ve eşanlamlı genişletme ile esneklik sunar, eşleşmeleri otomatik olarak işaretleyen HTML önizlemeleri oluşturarak vurgulama yapar ve çok sayfalı dosyaları aşırı bellek tüketimi olmadan işleyebilen, yerel, bulut veya hibrit ortamda çalışarak ölçeklenebilirlik sağlar.

## Önkoşullar
- Java Development Kit (JDK) 8 ve üzeri.  
- Maven (veya manuel JAR yönetimi).  
- IntelliJ IDEA, Eclipse veya VS Code gibi bir IDE.  
- Java proje yapısı ve Maven hakkında temel bilgi.

## GroupDocs.Search for Java'ı Kurma

### Maven ile Kurulum
GroupDocs deposunu ve Search bağımlılığını `pom.xml` dosyanıza ekleyin:

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
Maven kullanmak istemiyorsanız, resmi sürüm sayfasından en son JAR dosyasını indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Lisans Edinme Adımları
- **Free Trial:** Özellikleri keşfetmek için ücretsiz deneme ile başlayın.  
- **Temporary License:** [GroupDocs' official site](https://purchase.groupdocs.com/temporary-license) üzerinden edinin.  
- **Purchase:** Sınırsız üretim kullanımı için tam lisans satın alın.

### Temel Başlatma ve Kurulum
`Index` sınıfı, disk üzerinde saklanan aranabilir bir indeksi temsil eden çekirdek bileşendir. Bir indeks klasörü oluşturduktan sonra, belgeleri eklemek, silmek veya sorgulamak için `Index` nesnesini örnekleyebilirsiniz:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
Index index = new Index(indexFolder);
```

## Java Belge Arama – Özellik 1: Arama Sonucu Bilgilerini Çıkarma

Bu özellik, bir sorgu çalıştırmayı, eşleşen belgeleri almayı ve her terim için ayrıntılı oluşum verilerini elde etmeyi açıklar. Adımları izleyerek analiz panoları oluşturabilir veya arama sonuçlarından ayrıntılı raporlar üretebilirsiniz.

### Adım 1: Bir İndeks Oluşturun
`Index` sınıfı, disk üzerinde aranabilir meta verileri depolayan üst‑seviye nesnedir. Oluşturmak, tüm indeks dosyalarının bulunacağı bir klasöre işaret eder:

```java
String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/ObtainSearchResultInformation";
Index index = new Index(indexFolder);
index.add(documentFolder);
```

### Adım 2: Arama Seçeneklerini Yapılandırın (Bulanık aramayı etkinleştir)
`SearchOptions` sorgu davranışını ince ayarlamanızı sağlar. `FuzzySearch` özelliğini `true` olarak ayarlamak, tipografi hataları veya OCR hataları gibi durumlarda yaklaşık eşleşmeyi etkinleştirir:

```java
SearchOptions options = new SearchOptions();
options.getFuzzySearch().setEnabled(true);
options.getFuzzySearch().setFuzzyAlgorithm(new TableDiscreteFunction(3));
```

### Adım 3: Aramayı Gerçekleştirin
`Index.search` hazırlanan indeks üzerinde sorguyu çalıştırır ve eşleşen belgeler ile terim oluşumlarını içeren bir `SearchResult` koleksiyonu döndürür:

```java
String query = "favourable OR \"ipsum dolor\"";
SearchResult result = index.search(query, options);
```

`SearchResult` nesnesi, sorguya uyan belgelerin listesini ve ilgili skorlarını içerir.

### Adım 4: Oluşumları Çıkarın
Her `SearchResult` öğesi, kaynak dosya içinde sorgu terimlerinin tam konumlarını döndüren `getOccurrences()` metodunu sağlar; bu sayede analiz panoları veya ayrıntılı raporlar oluşturabilirsiniz:

```java
for (int i = 0; i < result.getDocumentCount(); i++) {
    FoundDocument document = result.getFoundDocument(i);
    for (FoundDocumentField field : document.getFoundFields()) {
        if (field.getTerms() != null) {
            for (String term : field.getTerms()) {
                int occurrences = field.getTermsOccurrences()[field.getTerms().indexOf(term)];
                System.out.println("Term: " + term + ", Occurrences: " + occurrences);
            }
        }
        if (field.getTermSequences() != null) {
            for (String[] terms : field.getTermSequences()) {
                int occurrences = field.getTermSequencesOccurrences()[ArrayUtils.indexOf(field.getTermSequences(), terms)];
                StringBuilder sequence = new StringBuilder();
                for (String term : terms) {
                    sequence.append(term).append(" ");
                }
                System.out.println("Phrase: " + sequence.toString() + ", Occurrences: " + occurrences);
            }
        }
    }
}
```

## Özellik 2: Java Belgelerinde Arama Terimlerini Vurgulama

Her eşleşmenin `<mark>` etiketiyle sarıldığı bir HTML önizlemesi oluşturun, böylece son‑kullanıcılar anında görsel ipuçları alır.

### Adım 1: Yüksek Sıkıştırmalı İndeks Kurun
Yüksek sıkıştırma, **%70'e kadar** depolama alanı tasarrufu sağlar ve sorgu hızını milisaniyeler içinde tutar. İndekslemeden önce `CompressionLevel` özelliğini ayarlayın:

```java
String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/HighlightSearchResults";
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Adım 2: Aramayı Gerçekleştir ve Sonuçları Vurgula
Aramayı yürüttükten sonra, `SearchResult` nesnesinde `highlight()` metodunu çağırarak sorgu teriminin her oluşumunu vurgulayan bir HTML dosyası üretin. `highlight()` metodu, eşleşen terimleri `<mark>` etiketleriyle saran bir HTML önizlemesi oluşturur:

```java
SearchResult result = index.search("solicitude");
if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    index.highlight(document, highlighter);
}
```

## Pratik Uygulamalar
1. **Legal Document Review** – Binlerce sözleşme içinde belirli maddeleri saniyeler içinde bulun.  
2. **Academic Research** – Araştırma makalelerinden literatür incelemeleri için anahtar ifadeleri çıkarın.  
3. **Customer Support** – E‑posta arşivlerinde tekrarlayan sorunları belirleyerek SSS sayfalarını iyileştirin.  
4. **Content Management** – Makale ve bloglarda SEO anahtar kelimelerini hızlı editöryel kontrol için vurgulayın.

## Performans Düşünceleri
- **Compression:** Yüksek sıkıştırma depolamayı azaltır ancak CPU kullanımını artırabilir; tipik iş yükünüzle benchmark yapın.  
- **Memory Management:** JVM yığınını kontrol altında tutmak için belgeleri 500 – 1 000 dosya grupları halinde indeksleyin.  
- **Index Refresh:** Arama sonuçlarının güncel kalmasını sağlamak için değişen dosyaları her gece yeniden indeksleyin.

## Sonuç
Bu kılavuz, **implement groupdocs search java** nasıl yapılacağını, ayrıntılı sonuç bilgilerini nasıl çıkarılacağını ve **highlight search terms java** nasıl HTML önizlemelerinde vurgulanacağını gösterdi. Bu adımları izleyerek herhangi bir belge deposu için hızlı, kullanıcı‑dostu arama deneyimleri sunabilirsiniz.

### Sonraki Adımlar
- Vurgulanan HTML'yi bir `<iframe>` veya sunucu‑tarafı render kullanarak web UI'nıza yerleştirin.  
- `SynonymSearch` veya `WildcardSearch` gibi ek `SearchOptions` seçenekleriyle deneyler yapın.  
- Özel puanlama, sonuç sayfalama ve çok‑dilli destek için GroupDocs.Search API referansına göz atın.

## Sıkça Sorulan Sorular

**S: GroupDocs.Search nedir?**  
C: GroupDocs.Search, 50'den fazla belge formatı üzerinde metni indeksleyen ve arayan bir Java SDK'sıdır; bulanık eşleşme ve sonuç vurgulama sunar.

**S: Bulanık arama nasıl çalışır?**  
C: Belirli bir karakter farkı sayısını toleranslı tutar, böylece yanlış yazılmış kelimeler veya OCR hataları üzerinde eşleşmeler sağlar.

**S: GroupDocs.Search'ı lisans olmadan kullanabilir miyim?**  
C: Evet, ücretsiz bir deneme mevcuttur, ancak üretim ortamları için tam lisans gereklidir.

**S: Hangi dosya formatları destekleniyor?**  
C: PDF, DOCX, XLSX, PPTX, TXT ve daha fazlası—tam liste için resmi dokümantasyona bakın.

**S: Vurgulanan sonuçları bir web uygulamasında nasıl gösteririm?**  
C: Oluşturulan HTML dosyasını doğrudan sunabilir veya içeriğini bir `<iframe>` veya sunucu‑tarafı render kullanarak bir sayfaya gömebilirsiniz.

---

**Last Updated:** 2026-07-26  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs

## İlgili Öğreticiler

- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Search Result Highlighting Java Tutorial with GroupDocs.Search](/search/java/highlighting/)
- [Mastering GroupDocs.Search Java: Fuzzy Search & Document Indexing Guide](/search/java/searching/groupdocs-search-java-fuzzy-document-indexing/)