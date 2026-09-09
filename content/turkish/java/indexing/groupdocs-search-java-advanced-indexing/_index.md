---
date: '2026-08-15'
description: GroupDocs.Search for Java'ın advanced indexing özelliklerini kullanarak
  arama gecikmesini nasıl iyileştireceğinizi öğrenin; cancellation, async operations,
  multithreading ve metadata customization dahil.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: GroupDocs.Search for Java ile cancellation, asynchronous indexing,
  multithreading ve metadata customization kullanarak arama gecikmesini iyileştirin.
  Performansı artırın ve kaynak kullanımını azaltın.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: GroupDocs'ta advanced indexing ile arama gecikmesini iyileştirin
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: GroupDocs'ta advanced indexing ile arama gecikmesini iyileştirin
type: docs
url: /tr/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Gelişmiş indeksleme ile arama gecikmesini iyileştirin

Bugünün hızlı tempolu dijital ortamında, **arama gecikmesini iyileştirmek** kullanıcıya anlık sonuçlar sunmak için gereklidir. İster özel bir arama motoru oluşturuyor olun ister mevcut bir belge yönetim sistemini geliştiriyor olun, doğru indeksleme stratejisi gecikmeyi büyük ölçüde azaltabilir, kaynak tüketimini düşürebilir ve **arama gecikmesini iyileştirebilir**. Bu öğreticide, GroupDocs.Search for Java'nın en güçlü özelliklerini—iptal, eşzamanlı olmayan indeksleme, çok iş parçacıklı çalışma ve meta veri özelleştirme—gözden geçireceğiz, böylece **belgeleri indekse ekleyin** daha hızlı ve daha verimli bir şekilde.

**Neler öğreneceksiniz**

- Belirli bir süreden sonra bir indeksleme işlemini iptal etme  
- Eşzamanlı olmayan indeksleme işlemlerini gerçekleştirme ve durum değişikliklerini işleme  
- Daha hızlı indeksleme için çok iş parçacıklı yapılandırma  
- Meta veri indeksleme seçeneklerini **arama meta verilerini özelleştirmek** için özelleştirme  

Kodun içine dalmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım.

## Hızlı cevaplar
- **İptal ne işe yarar?** Belirli bir zaman aşımından sonra indekslemeyi durdurur, CPU ve belleği diğer görevler için serbest bırakır.  
- **Belgeleri eşzamanlı olmayan şekilde indeksleyebilir miyim?** Evet – bunu `options.setAsync(true)` ile etkinleştirin.  
- **Kaç iş parçacığı kullanabilirim?** Pozitif bir tam sayı; çoğu sunucu için tipik olarak 2‑4 iş parçacığı.  
- **Meta veri indeksleme isteğe bağlı mı?** Kesinlikle – her alan için etkinleştirebilir veya ince ayar yapabilirsiniz.  
- **Bu özellikler için lisansa ihtiyacım var mı?** Test için bir deneme sürümü çalışır; üretim için tam lisans gereklidir.

## Önkoşullar

- **GroupDocs.Search kütüphanesi** – sürüm 25.4 ve üzeri.  
- **Java Geliştirme Ortamı** – JDK 8 ve üzeri önerilir.  
- Java ve indeksleme kavramına temel aşinalık.

### GroupDocs.Search for Java'ı Kurma

#### Maven kurulumu

`pom.xml` dosyanıza depo ve bağımlılığı ekleyin:

`pom.xml` yapılandırması, Maven'e hangi GroupDocs.Search artefaktlarını indirmesi ve projenize dahil etmesi gerektiğini söyler.

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

Alternatif olarak, en son JAR dosyasını [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

**Lisans edinme** – Tam özellik setini açmak için ücretsiz bir deneme ile başlayın veya geçici bir lisans isteyin.

### Temel başlatma ve kurulum

`SearchIndex` sınıfı, diskte veya bellekte depolanan aranabilir bir indeksi temsil eden giriş noktasıdır.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Bu bağlamda “arama performansını optimize etme” nedir?

Arama performansını optimize etmek, indeksleme sürecini doğru miktarda CPU, bellek ve zaman tüketecek şekilde yapılandırmak ve en alakalı sonuçları anında sunmak anlamına gelir. İptal, async yürütme, iş parçacığı ve meta veri işleme kontrol edilerek, motorun **belgeleri indekse ekleyebilir** ve sorgulara yanıt vermesi doğrudan etkilenir.

## Neden gelişmiş indeksleme özelliklerini kullanmalısınız?

Eşzamanlı olmayan ve çok iş parçacıklı indeksleme, uygulamanızın yanıt vermesini sağlar, iptal ise kontrolsüz süreçleri önler. İnce ayarlı meta veri seçenekleri en önemli bilgileri ortaya çıkarmanıza olanak tanır ve bu doğrudan son kullanıcılar için **arama gecikmesini iyileştirir**. Ayrıca bu özellikler CPU dalgalanmalarını azaltır, bellek baskısını düşürür ve büyük belge hacimlerini işlerken daha sorunsuz ölçeklendirme sağlar.

## Gelişmiş indeksleme ile arama gecikmesini nasıl iyileştirirsiniz?

`SearchIndex` örneğinizi yükleyin, `IndexingOptions`'ı iptal, async ve iş parçacığı ayarlarıyla yapılandırın, ardından `index.add(document)` çağrısını yapın — bu kombinasyon tipik iş yüklerinde toplam indeksleme süresini %60’a kadar azaltır ve uzun süren görevlerin diğer işlemleri engellemesini önler. Ayrıca meta veri indeksleme limitlerini ayarlayabilir ve performans bütçeleri içinde kalmasını sağlamak için durum‑değiştirme olaylarıyla ilerlemeyi izleyebilirsiniz.

## Uygulama rehberi

### İptal özelliği

**Genel Bakış** – Kaynakların aşırı tüketilmesini önlemek için belirli bir süreden sonra indekslemeyi iptal edin.

#### Adım 1: ortamı kurun

İndeks klasörünüze işaret eden bir `SearchIndex` örneği oluşturun.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Adım 2: iptal ile indeksleme seçenekleri oluşturun

`IndexingOptions`, indeksleme motorunun nasıl davranacağını belirlemenizi sağlar.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Ana noktalar**

- `setCancellation()` özelliği etkinleştirir.  
- `cancelAfter(int milliseconds)` zaman aşımını tanımlar (bu örnekte 3 saniye).

### Eşzamanlı olmayan (asenkron) özelliği

**Genel Bakış** – İndekslemeyi arka plan iş parçacığında çalıştırın ve durum değişikliklerini dinleyin.

#### Adım 1: ortamı kurun

İndeksi örnekleyin ve belge koleksiyonunu hazırlayın.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Adım 2: durum‑değiştirme olayına abone olun

`StatusChanged` olayı, indeksleme işinin durumlar arasında geçiş yaptığını size bildirir.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Adım 3: asenkron seçenekleri yapılandırın

Çağrının hemen döndürülmesi ve işlemenin arka planda devam etmesi için async modunu etkinleştirin.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### İş parçacığı özelliği

**Genel Bakış** – Birden fazla CPU çekirdeğinden yararlanarak indekslemeyi hızlandırın.

#### Adım 1: ortamı kurun

İndeksi hazırlayın ve JVM'nin yeterli yığın belleğine sahip olduğundan emin olun.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Adım 2: çok iş parçacıklı çalışmayı yapılandırın

İşçi iş parçacığı sayısını ayarlayın; her iş parçacığı belgelerin bir alt kümesini işler.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Meta veri indeksleme seçenekleri özelliği

**Genel Bakış** – Hangi belge meta verisinin indeksleneceğini ve nasıl saklanacağını ince ayar yapın.

#### Adım 1: ortamı kurun

Yazar, başlık ve özel etiketler gibi meta veri alanları içeren bir belge yükleyin.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Adım 2: meta veri seçeneklerini yapılandırın

`MetadataIndexingOptions`, bireysel meta veri alanlarını etkinleştirmenize veya devre dışı bırakmanıza ve boyut limitlerini tanımlamanıza olanak tanır.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Pratik uygulamalar

1. **Belge yönetim sistemleri** – Büyük toplu işlemler arka planda işlenirken UI'nın yanıt vermesini sağlamak için asenkron indeksleme kullanın.  
2. **İçerik arama motorları** – Yoğun trafik sırasında uzun süren işlerin sunucu kaynaklarını tüketmesini önlemek için iptal uygulayın.  
3. **Büyük ölçekli alma hatları** – **belgeleri indekse ekleyin** için çok iş parçacıklı çalışmayı kullanarak işleme süresini büyük ölçüde kısaltın.  

## Performans değerlendirmeleri

- **İş parçacığı yönetimi** – CPU kullanımını izleyin; çok fazla iş parçacığı bağlam geçişi yüküne neden olabilir.  
- **Bellek ayak izi** – Meta veri limitleri (ör. `setMaxBytesToIndexField`) bellek kullanımını öngörülebilir tutar.  
- **Çöp toplama** – Büyük veri kümelerini indekslerken uygun JVM bayraklarını (`-Xmx`, `-XX:+UseG1GC`) kullanın.  

## Yaygın sorunlar ve çözümler

| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| İndeksleme hiç bitmiyor | İptal çok düşük ayarlandı | `cancelAfter` değerini artırın veya uzun işler için iptali kaldırın |
| Asenkron modda durum güncellemeleri yok | Olay işleyicisi doğru bağlanmadı | `index.getEvents().StatusChanged.add(...)` çağrısının `index.add`'den önce yapıldığından emin olun |
| Bellek yetersiz hataları | Çok fazla iş parçacığı veya yüksek meta veri limitleri | `options.setThreads` değerini azaltın ve meta veri alan limitlerini düşürün |
| Sonuçlarda meta veri eksik | Meta veri indeksleme devre dışı | `options.getMetadataIndexingOptions()` yapılandırıldığını ve alanları yok saymadığını doğrulayın |

## Sıkça sorulan sorular

**Q: GroupDocs.Search için geçici bir lisans nasıl alabilirim?**  
A: [GroupDocs geçici lisans sayfasını](https://purchase.groupdocs.com/temporary-license/) ziyaret edin ve ekrandaki talimatları izleyin.

**Q: Bir indeksleme işlemini ortasında iptal edebilir miyim?**  
A: Evet – `cancelAfter()` ile iptal özelliğini kullanın veya programlı olarak `Cancellation.cancel()` çağırın.

**Q: Asenkron indeksleme için bazı kullanım senaryoları nelerdir?**  
A: Gerçek zamanlı belge alma, arka plan toplu işleme ve UI‑yanıt veren uygulamalar asenkron indekslemeden faydalanır.

**Q: Paylaşılan bir sunucuda iş parçacığı sayısını artırmak güvenli mi?**  
A: Yavaş yavaş artırın ve CPU yükünü izleyin; yoğun paylaşımlı ortamlarda iş parçacığı sayısını makul tutun (2‑4).

**Q: Meta veri indeksleme arama alaka düzeyini nasıl etkiler?**  
A: Doğru indekslenmiş meta veriler (yazar, oluşturma tarihi, etiketler) sorgularda daha yüksek ağırlık alabilir, sonuç doğruluğunu artırır.

## Sonuç

GroupDocs.Search for Java'nın bu gelişmiş özelliklerini benimseyerek, **arama gecikmesini iyileştirecek** çeşitli senaryolarda—hızlı belge alımından ince ayarlı meta veri kontrolüne kadar—kullanabilirsiniz. Farklı yapılandırmalarla deney yapın, kaynak kullanımını izleyin ve en iyi sonuçları elde etmek için ayarları özel iş yükünüze göre özelleştirin.

---

**Son Güncelleme:** 2026-08-15  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [GroupDocs.Search Java ile Sorgu Performansını İyileştirme: İndeks ve Aramayı Optimize Et](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs.Search kullanarak Java'da Meta Veri İndeksleme ile belgelere indeks ekleme](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [GroupDocs.Search for Java'da Birden Çok Takma Ad Eklemek ve Belgeleri İndekse Eklemek](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)