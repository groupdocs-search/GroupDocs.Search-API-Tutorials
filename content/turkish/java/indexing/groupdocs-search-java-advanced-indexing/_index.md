---
date: '2026-03-01'
description: GroupDocs.Search for Java'in gelişmiş indeksleme özelliklerini, iptal,
  eşzamanlı olmayan işlemler, çok iş parçacıklı çalışma ve meta veri özelleştirmesi
  dahil olmak üzere kullanarak arama performansını nasıl optimize edeceğinizi ve arama
  gecikmesini nasıl iyileştireceğinizi öğrenin.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: GroupDocs.Search for Java'da Gelişmiş Dizinleme Teknikleriyle Arama Performansını
  Optimize Edin
type: docs
url: /tr/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Gelişmiş Dizinleme Teknikleriyle GroupDocs.Search for Java'da Arama Performansını Optimize Etme

Günümüzün hızlı tempolu dijital ortamında, **optimize search performance** kullanıcılarına anında sonuç sunmak için hayati öneme sahiptir. İster özel bir arama motoru oluşturuyor olun, ister mevcut bir belge yönetim sistemini geliştiriyor olun, doğru dizinleme stratejisi gecikmeyi büyük ölçüde azaltabilir, kaynak tüketimini düşürebilir ve **improve search latency** tüm sistemde iyileştirebilir. Bu öğreticide GroupDocs.Search for Java'nın en güçlü özelliklerini—cancellation, asynchronous indexing, multi‑threading ve metadata customization—adım adım inceleyeceğiz, böylece **add documents index** daha hızlı ve verimli bir şekilde yapabilirsiniz.

**Neler Öğreneceksiniz**

- Belirli bir süreden sonra bir dizinleme işlemini iptal etmeyi
- Asenkron dizinleme işlemlerini gerçekleştirmeyi ve durum değişikliklerini yönetmeyi
- Daha hızlı dizinleme için çoklu iş parçacığını yapılandırmayı
- Metadata dizinleme seçeneklerini özelleştirmeyi

Kodlara dalmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım.

## Prerequisites

- **GroupDocs.Search Library** – sürüm 25.4 ve üzeri.  
- **Java Development Environment** – JDK 8 ve üzeri önerilir.  
- Java ve dizinleme kavramına temel aşinalık.

### Setting Up GroupDocs.Search for Java

#### Maven Installation

Add the repository and dependency to your `pom.xml` file:

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

#### Direct Download

Alternatif olarak, en son JAR dosyasını [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

**License Acquisition** – Tam özellik setini açmak için ücretsiz deneme sürümüyle başlayın veya geçici bir lisans isteyin.

### Basic Initialization and Setup

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

## Quick Answers
- **What does cancellation do?** Dizinlemeyi belirli bir süreden sonra durdurarak kaynakları serbest bırakır.  
- **Can I index documents asynchronously?** Evet – `options.setAsync(true)` ayarlayın.  
- **How many threads can I use?** Pozitif bir tam sayı; çoğu sunucu için tipik değerler 2‑4'tür.  
- **Is metadata indexing optional?** Kesinlikle – alan bazında etkinleştirebilir veya ince ayar yapabilirsiniz.  
- **Do I need a license for these features?** Test için bir deneme yeterli; üretim için tam lisans gereklidir.

## “Optimize Search Performance” Bu Bağlamda Ne Anlama Geliyor?

Arama performansını optimize etmek, dizinleme sürecini CPU, bellek ve zamanı doğru oranda tüketecek şekilde yapılandırmak ve en alakalı sonuçları anında sunmak demektir. İptal, asenkron yürütme, çoklu iş parçacığı ve metadata yönetimini kontrol ederek motorun **add documents index** hızını ve sorgulara yanıt süresini doğrudan etkilersiniz.

## Neden Gelişmiş Dizinleme Özelliklerini Kullanmalısınız?

- **Reduced latency** – Asenkron ve çok iş parçacıklı dizinleme uygulamanızın yanıt vermesini sağlar.  
- **Better resource management** – İptal, kontrolsüz süreçlerin önüne geçer.  
- **Tailored search relevance** – Metadata seçenekleri en önemli bilgileri öne çıkarmanıza olanak tanır.  

## Gelişmiş Dizinleme ile arama gecikmesini nasıl iyileştirirsiniz?

**improve search latency** ihtiyacınız olduğunda, keşfedeceğimiz özellikleri birleştirin: uzun süren işleri iptal edin, dizinlemeyi arka planda çalıştırın ve işi birden çok CPU çekirdeğine dağıtın. Bu çok yönlü yaklaşım genellikle en büyük hız artışını sağlar.

## Implementation Guide

### Cancellation Property

**Overview** – Kaynak aşırı tüketimini önlemek için belirli bir süreden sonra dizinlemeyi iptal edin.

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Create Indexing Options with Cancellation

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

**Key Points**

- `setCancellation()` özelliği etkinleştirir.  
- `cancelAfter(int milliseconds)` zaman aşımını tanımlar (bu örnekte 3 saniye).

### Asynchronous Property

**Overview** – Dizinlemeyi arka plan iş parçacığında çalıştırın ve durum değişikliklerini dinleyin.

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Subscribe to Status Changed Event

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

#### Step 3: Configure Asynchronous Options

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Threads Property

**Overview** – Birden çok CPU çekirdeğini kullanarak dizinlemeyi hızlandırın.

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Multi‑threading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metadata Indexing Options Property

**Overview** – Hangi belge metadata'sının dizinleneceğini ve nasıl saklanacağını ince ayar yapın.

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Metadata Options

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

## Practical Applications

1. **Document Management Systems** – Büyük toplu işlemler arka planda yürütülürken UI'nun yanıt vermesini sağlamak için asenkron dizinleme kullanın.  
2. **Content Search Engines** – Yoğun trafik sırasında uzun süren işlerin sunucu kaynaklarını tüketmesini önlemek için iptal uygulayın.  
3. **Large‑Scale Ingestion Pipelines** – **add documents index** işlemini ölçekli şekilde gerçekleştirmek ve işleme süresini dramatik şekilde kısaltmak için çok iş parçacıklı dizinleme kullanın.

## Performance Considerations

- **Thread Management** – CPU kullanımını izleyin; çok fazla iş parçacığı bağlam geçişi yükü oluşturabilir.  
- **Memory Footprint** – `setMaxBytesToIndexField` gibi metadata limitleri bellek kullanımını öngörülebilir tutar.  
- **Garbage Collection** – Büyük veri kümeleri dizinlenirken uygun JVM bayraklarını (`-Xmx`, `-XX:+UseG1GC`) kullanın.

## Common Issues and Solutions

| Semptom | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Dizinleme hiç bitmiyor | İptal süresi çok düşük ayarlandı | `cancelAfter` değerini artırın veya uzun işler için iptali kaldırın |
| Asenkron modda durum güncellemeleri yok | Olay işleyicisi doğru bağlanmadı | `index.getEvents().StatusChanged.add(...)` çağrısının `index.add`'den önce yapıldığından emin olun |
| Bellek yetersizliği hataları | Çok fazla iş parçacığı veya yüksek metadata limitleri | `options.setThreads` değerini azaltın ve metadata alan limitlerini düşürün |
| Sonuçlarda metadata eksik | Metadata dizinleme devre dışı | `options.getMetadataIndexingOptions()` yapılandırıldığını ve alanları yok sayacak şekilde ayarlanmadığını doğrulayın |

## Frequently Asked Questions

**S: GroupDocs.Search için geçici bir lisans nasıl alınır?**  
C: [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin.

**S: Bir dizinleme işlemini ortasında iptal edebilir miyim?**  
C: Evet – `cancelAfter()` ile iptal özelliğini kullanın veya programmatically `Cancellation.cancel()` çağırın.

**S: Asenkron dizinleme için hangi kullanım senaryoları vardır?**  
C: Gerçek zamanlı belge erişimi, arka plan toplu işleme ve UI yanıt verebilirliğinin kritik olduğu uygulamalar asenkron dizinlemeden faydalanır.

**S: Paylaşımlı bir sunucuda iş parçacığı sayısını artırmak güvenli mi?**  
C: Yavaş yavaş artırın ve CPU yükünü izleyin; yoğun paylaşımlı ortamlarda iş parçacığı sayısını mütevazı tutun (2‑4).

**S: Metadata dizinleme arama alaka düzeyini nasıl etkiler?**  
C: Doğru dizinlenmiş metadata (yazar, oluşturma tarihi, etiketler) sorgularda daha yüksek ağırlık alabilir, bu da sonuç doğruluğunu artırır.

## Conclusion

GroupDocs.Search for Java'nın bu gelişmiş özelliklerini benimseyerek **optimize search performance**'ı çeşitli senaryolarda—hızlı belge alımı, ince ayarlı metadata kontrolü gibi—optimize edebilirsiniz. Farklı yapılandırmalarla deney yapın, kaynak kullanımını izleyin ve ayarları iş yükünüze göre özelleştirerek en iyi sonuçları elde edin.

---

**Last Updated:** 2026-03-01  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs