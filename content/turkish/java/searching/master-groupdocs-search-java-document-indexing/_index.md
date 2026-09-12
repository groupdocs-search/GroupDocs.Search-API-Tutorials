---
date: '2026-09-11'
description: GroupDocs.Search for Java kullanarak Java’da arama sonuçlarını nasıl
  vurgulayacağınızı ve belgeleri nasıl indeksleyeceğinizi, synchronous ve asynchronous
  indexing ile öğrenin.
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: GroupDocs.Search ile Java’da arama sonuçlarını vurgulayın. Java uygulamalarında
  synchronous ve asynchronous indexing, real‑time updates ve sonuç vurgulama hakkında
  bilgi edinin.
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: Java’da arama sonuçlarını vurgulama – Hızlı synchronous & async indexing
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: Java’da arama sonuçlarını vurgulama – Synchronous & async indexing
type: docs
url: /tr/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Java’da Arama Sonuçlarını Vurgulama – Senkron ve Asenkron indeksleme

Bu rehberde GroupDocs.Search kütüphanesini kullanarak **highlight search results Java** nasıl yapılacağını keşfedecek ve Java’da belgeleri senkron ve asenkron olarak nasıl indeksleyeceğinizi adım adım göreceksiniz. Küçük bir masaüstü aracı ya da büyük ölçekli bir kurumsal arama hizmeti oluşturuyor olun, bu teknikler uygulama iş parçacıklarınızı engellemeden anında, görsel olarak net eşleşmeler sunmanızı sağlar.

## Hızlı cevaplar
- **“highlight search results Java” ne anlama geliyor?** Bu, döndürülen snippet'lerdeki her eşleşen terimi işaretleme (ör. `<mark>`) ile sarmak anlamına gelir, böylece kullanıcılar vuruşun bağlamını anında görebilir.
- **Senkron indekslemeyi ne zaman kullanmalıyım?** Belge eklendiği anda aranabilir olması gereken küçük‑orta ölçekli koleksiyonlar için kullanın.
- **Asenkron indeksleme ne zaman tercih edilir?** Büyük toplu işlemler için veya indeks arka planda oluşturulurken UI iş parçacığının yanıt vermeye devam etmesi gerektiğinde seçin.
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü yeterlidir; tam lisans sınırlamaları kaldırır ve gelişmiş özelliklerin kilidini açar.
- **Hangi Java sürümü destekleniyor?** Java 8 veya üzeri.

## “highlight search results Java” nedir?
`highlight search results java` GroupDocs.Search'ten alınan ham eşleşme verilerini alıp her bulunan terimin etrafına görsel ipuçları—genellikle HTML `<mark>` etiketleri—ekleme sürecidir. Bu, sonuç snippet'lerini bir web sayfasında veya Swing bileşeninde anında okunabilir kılar, sorgunun tam olarak nerede göründüğünü göstererek kullanıcı deneyimini iyileştirir.

## Java için GroupDocs.Search neden kullanılmalı?
GroupDocs.Search, **saniyede 5 000 belgeye kadar işleyebilen**, **30+ dosya formatını destekleyen** ve **10 milyon belge koleksiyonunu indeksleyebilen** yüksek performanslı, dil bağımsız bir motor sunar; tüm veri kümesini belleğe yüklemeden çalışır. Yerleşik vurgulama, gerçek zamanlı indeksleme ve çok‑dilli analizörleri, içerik yönetim sistemleri, e‑ticaret katalogları ve kurumsal belge depoları için ideal kılar.

## Önkoşullar
- **Java Development Kit** (JDK 8 veya daha yeni) yüklü ve `JAVA_HOME` doğru şekilde ayarlanmış.  
- **IntelliJ IDEA** veya **Eclipse** gibi bir IDE.  
- `documents/` gibi (örnek) bir klasör, indekslemek istediğiniz dosyaları içerir—düz metin, PDF, DOCX vb.  
- Bağımlılık yönetimi için Maven (veya JAR'ı manuel olarak ekleyebilirsiniz).

### Gerekli kütüphaneler ve bağımlılıklar
Maven `pom.xml` dosyanıza GroupDocs.Search ekleyin:

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

Doğrudan indirme için, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden alın.

### Ortam kurulumu
- `JAVA_HOME`'un uyumlu bir JDK'ya işaret ettiğini doğrulayın.  
- Yeni bir Maven projesi oluşturun ve yukarıdaki snippet'i `<dependencies>` bölümüne yapıştırın.  
- Örnek dosyaları `src/main/resources/documents/` gibi bir dizine yerleştirin.

## GroupDocs.Search for Java Nasıl Kurulur
`Index`, diskte depolanan aranabilir bir koleksiyonu temsil eden temel sınıftır.

Diskteki bir klasöre işaret eden bir `Index` örneği oluşturun, bir lisansınız varsa uygulayın ve isteğe bağlı olarak dil‑spesifik tokenizasyon için bir analizör yapılandırın. Bu hazırlık adımı, motorun indeksi verimli bir şekilde okuyup yazıp aramasını sağlar.

`Index` sınıfı, diskteki aranabilir bir koleksiyonu temsil eden çekirdek bileşendir. Oluşturduktan sonra, tüm indeksleme ve sorgu işlemleri bu nesne üzerinden gerçekleşir.

1. **Kütüphaneyi kurun** – Yukarıdaki Maven snippet'ini kullanın veya JAR'ı [GroupDocs](https://releases.groupdocs.com/search/java/) adresinden indirin.  
2. **Lisans edinin** – Öncelikle bir deneme lisansı alın; dağıtımdan önce üretim anahtarıyla değiştirin.  
3. **İndeksi başlatın** – Aşağıdaki snippet, bir indeks klasörü oluşturmayı (veya açmayı) gösterir:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Java’da Arama Sonuçlarını Vurgulama – Senkron indeksleme
`DocumentHighlighter`, arama sonuçlarından vurgulanan snippet'ler üreten bir yardımcı sınıftır.

İndeksi yükleyin, `index.add(documentPath)` ile belgeleri ekleyin, bir sorgu çalıştırın ve ardından eşleşmeleri `<mark>` etiketleriyle sarmak için `DocumentHighlighter`'ı çağırın. Tüm süreç çağıran iş parçacığında çalışır, böylece belge `add` döndükten hemen sonra kullanıcılar için aranabilir hâle gelir.

### Adım 1: indeksi oluşturun ve hata yönetimi ekleyin
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Adım 2: belgeleri ekleyin ve bir arama çalıştırın
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Adım 3: sonuçları işleyin ve Java’da arama sonuçlarını vurgulayın
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## Java’da Arama Sonuçlarını Vurgulama – Asenkron indeksleme
`IndexingOptions`, indeksleme sürecinin nasıl çalışacağını yapılandırır; senkron veya asenkron mod dahil.

`IndexingOptions`'ı arka plan modunda çalışacak şekilde yapılandırın, `StatusChanged` olaylarına abone olun ve motor dosyaları indekslerken UI'niz diğer istekleri hizmet vermeye devam etsin. Durum `Ready` (Hazır) olduğunda, senkron modda olduğu gibi arama yapabilir ve vurgulanan snippet'ler alabilirsiniz.

`AsyncIndexingListener`, ilerleme güncellemelerini alır; böylece ana iş parçacığını engellemeden bir ilerleme çubuğu gösterebilir veya durumu kaydedebilirsiniz.

### Adım 1: indeks'i olay dinleyicileriyle kurun
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Adım 2: asenkron modu etkinleştirin ve indekslemeyi başlatın
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## Java’da Belgeleri İndeksleme – Pratik İpuçları
`index.update(path)`, belirtilen yoldaki dosyayla indeksteki mevcut bir belgeyi günceller.

Büyük koleksiyonları 1 000–5 000 dosyadan oluşan partilere bölün, gereksiz ayrıştırmayı önlemek için uzantıya göre filtreleyin ve tüm indeksi yeniden oluşturmak yerine değişen dosyalar için `index.update(path)` kullanın. Bu uygulamalar bellek kullanımını düşük tutar ve indeksleme süresini öngörülebilir kılarak tutarlılığı korur.

- **Batch size**: Büyük koleksiyonlar için, bellek dalgalanmalarını önlemek amacıyla klasörü daha küçük partilere bölün.  
- **File filters**: Sadece ihtiyacınız olan formatları (ör. `.pdf`, `.docx`) dahil etmek için `IndexingOptions.setFileExtensions` kullanın.  
- **Re‑indexing**: Bir belge değiştiğinde, indeksi sıfırdan yeniden oluşturmak yerine `index.update(documentPath)` çağırın.

## Performans Düşünceleri
- **Memory**: Yığın kullanımını izleyin; aynı anda birçok büyük dosya işliyorsanız `-Xmx` değerini artırın.  
- **CPU**: Asenkron indeksleme işi iş parçacıkları arasında dağıtır ancak hâlâ CPU tüketir—kullanımı JVisualVM ile izleyin.  
- **Result highlighting**: Vurgulama, sonuç başına yaklaşık 2–5 ms ek bir yük getirir. Aynı snippet'leri tekrar tekrar göstermeniz gerekiyorsa oluşturulan HTML'yi önbelleğe alın.

## Sıkça Sorulan Sorular

**Q: Aynı uygulamada senkron ve asenkron indekslemeyi birleştirebilir miyim?**  
A: Evet. Küçük, sık güncellenen setler için senkron indeksleme, toplu içe aktarmalar veya arka plan işleri için asenkron indeksleme kullanın.

**Q: Vurgulama stilini nasıl özelleştirebilirim?**  
A: Eşleşen terimler etrafında istediğiniz HTML, CSS veya XML etiketlerini yazan özel bir `DocumentHighlighter` uygulaması sağlayın.

**Q: GroupDocs.Search varsayılan olarak hangi dosya türlerini destekliyor?**  
A: Metin, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML ve yerleşik ayrıştırıcılar sayesinde daha birçok format—toplamda 30'dan fazla.

**Q: Aynı anda birden fazla dilde arama yapmak mümkün mü?**  
A: Kesinlikle. GroupDocs.Search çok‑dilli analizörler içerir; indeks oluştururken uygun `Analyzer`'ı yapılandırmanız yeterlidir.

**Q: İndeks klasörünü nasıl güvenli hale getirebilirim?**  
A: İndeksi korumalı bir dizinde saklayın, sıkı dosya sistemi izinleri ayarlayın ve isteğe bağlı olarak kütüphanenin güvenlik özelliklerini kullanarak indeksi şifreleyin.

**Son Güncelleme:** 2026-09-11  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [Java için GroupDocs.Search API'sı Kullanarak Belge İndeksi Oluşturma ve Belgeleri Ekleme](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Java ile index deposu oluşturma: GroupDocs.Search ile Verimli Belge İndeksleme ve Arama](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [Verimli Belge İndeksleme Arama Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)