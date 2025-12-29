---
date: '2025-12-29'
description: GroupDocs.Search for Java'in gelişmiş indeksleme özelliklerini kullanarak
  arama performansını nasıl optimize edeceğinizi öğrenin; iptal, asenkron işlemler,
  çok iş parçacıklı çalışma ve meta veri özelleştirmeyi içeren.
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

# GroupDocs.Search for Java'da Gelişmiş Dizinleme Teknikleriyle Arama Performansını Optimize Etme

Bugünün hızlı tempolu dijital ortamında **arama performansını optimize etmek**, kullanıcılara anlık sonuçlar sunmak için hayati öneme sahiptir. İster özel bir arama motoru oluşturuyor olun, ister mevcut bir belge yönetim sistemini geliştiriyor olun, doğru dizinleme stratejisi gecikmeyi ve kaynak tüketimini büyük ölçüde azaltabilir. Bu öğreticide, GroupDocs.Search for Java’nın en güçlü özelliklerini—iptal, eşzamanlı olmayan dizinleme, çoklu iş parçacığı ve meta veri özelleştirme—adım adım inceleyeceğiz, böylece **add documents index** işlemini daha hızlı ve verimli bir şekilde gerçekleştirebileceksiniz.

**What You’ll Learn**

- Belirli bir süreden sonra bir dizinleme işlemini iptal etme
- Eşzamanlı olmayan dizinleme işlemlerini yürütme ve durum değişikliklerini işleme
- Daha hızlı dizinleme için çoklu iş parçacığını yapılandırma
- Meta veri dizinleme seçeneklerini özelleştirme

Kodlara dalmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım.

## Prerequisites

- **GroupDocs.Search Library** – sürüm 25.4 veya üzeri.  
- **Java Development Environment** – JDK 8 veya üzeri önerilir.  
- Java ve dizinleme kavramına temel aşinalık.

### Setting Up GroupDocs.Search for Java

#### Maven Installation

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
- **What does cancellation do?** Belirli bir süreden sonra dizinlemeyi durdurur ve kaynakları serbest bırakır.  
- **Can I index documents asynchronously?** Evet – `options.setAsync(true)` ayarlayın.  
- **How many threads can I use?** Pozitif bir tam sayı; çoğu sunucu için tipik değer 2‑4’tür.  
- **Is metadata indexing optional?** Kesinlikle – alan bazında etkinleştirebilir veya ince ayar yapabilirsiniz.  
- **Do I need a license for these features?** Deneme sürümü test için yeterlidir; üretim ortamı için tam lisans gereklidir.

## What Is “Optimize Search Performance” in This Context?

Arama performansını optimize etmek, dizinleme sürecini CPU, bellek ve zamanı doğru oranda tüketecek şekilde yapılandırmak ve en alakalı sonuçları anında sunmak demektir. İptal, eşzamanlı olmayan yürütme, iş parçacığı ve meta veri yönetimini kontrol ederek, **add documents index** ve sorgulara yanıt verme hızını doğrudan etkilersiniz.

## Why Use Advanced Indexing Features?

- **Reduced latency** – Eşzamanlı olmayan ve çok iş parçacıklı dizinleme, uygulamanızın yanıt vermesini sağlar.  
- **Better resource management** – İptal, kaynak tüketimini kontrol altında tutar.  
- **Tailored search relevance** – Meta veri seçenekleri, en önemli bilgileri ön plana çıkarmanıza olanak tanır.  

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

**Overview** – Birden çok CPU çekirdeğini kullanarak dizinleme hızını artırın.

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

**Overview** – Hangi belge meta verilerinin dizinleneceğini ve nasıl saklanacağını ince ayar yapın.

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

1. **Document Management Systems** – Büyük toplu işlemler arka planda yürütülürken UI’nın yanıt vermesini sağlamak için eşzamanlı olmayan dizinleme kullanın.  
2. **Content Search Engines** – Yoğun trafik zamanlarında uzun süren işleri engellemek için iptal özelliğini uygulayın.  
3. **Large‑Scale Ingestion Pipelines** – **add documents index** işlemini ölçekli şekilde gerçekleştirmek ve işleme süresini büyük ölçüde kısaltmak için çok iş parçacıklı dizinlemeyi kullanın.

## Performance Considerations

- **Thread Management** – CPU kullanımını izleyin; çok fazla iş parçacığı bağlam geçişi overhead’ine yol açabilir.  
- **Memory Footprint** – `setMaxBytesToIndexField` gibi meta veri limitleri, bellek kullanımını öngörülebilir tutar.  
- **Garbage Collection** – Büyük veri kümelerini dizinlerken uygun JVM bayraklarını (`-Xmx`, `-XX:+UseG1GC`) kullanın.

## Common Issues and Solutions

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Indexing never finishes | Cancellation set too low | Increase `cancelAfter` value or remove cancellation for long jobs |
| No status updates in async mode | Event handler not attached correctly | Ensure `index.getEvents().StatusChanged.add(...)` is called before `index.add` |
| Out‑of‑memory errors | Too many threads or high metadata limits | Reduce `options.setThreads` and lower metadata field limits |
| Missing metadata in results | Metadata indexing disabled | Verify `options.getMetadataIndexingOptions()` is configured and not set to ignore fields |

## Frequently Asked Questions

**Q: How do I obtain a temporary license for GroupDocs.Search?**  
A: Visit [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/).

**Q: Can I cancel an indexing operation midway through?**  
A: Yes – use the cancellation property with `cancelAfter()` or call `Cancellation.cancel()` programmatically.

**Q: What are some use cases for asynchronous indexing?**  
A: Real‑time document retrieval, background batch processing, and UI‑responsive applications benefit from async indexing.

**Q: Is it safe to increase the thread count on a shared server?**  
A: Increase gradually and monitor CPU load; on heavily shared environments, keep the thread count modest (2‑4).

**Q: How does metadata indexing affect search relevance?**  
A: Properly indexed metadata (author, creation date, tags) can be weighted higher in queries, improving result accuracy.

## Conclusion

GroupDocs.Search for Java’nın bu gelişmiş özelliklerini benimseyerek, çeşitli senaryolarda **optimize search performance** elde edebilirsiniz—hızlı belge alımından ince ayarlı meta veri kontrolüne kadar. Farklı yapılandırmalarla deney yapın, kaynak kullanımını izleyin ve ayarları iş yükünüze göre özelleştirerek en iyi sonuçları alın.

---

**Last Updated:** 2025-12-29  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---