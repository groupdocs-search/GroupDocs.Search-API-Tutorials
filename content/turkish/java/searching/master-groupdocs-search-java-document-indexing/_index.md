---
date: '2026-02-08'
description: Java'da arama sonuçlarını nasıl vurgulayacağınızı ve GroupDocs.Search
  for Java kullanarak senkron ve asenkron indeksleme ile belgeleri nasıl indeksleyeceğinizi
  öğrenin.
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: Vurgulama Arama Sonuçları Java – Senkron ve Asenkron Dizinleme
type: docs
url: /tr/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Java’da Arama Sonuçlarını Vurgulama – Senkron ve Async İndeksleme

Boost your Java applications by **highlighting search results Java** with the powerful GroupDocs.Search library. Whether you’re dealing with a few files or a massive repository, mastering both synchronous and asynchronous indexing lets you deliver fast, accurate results without blocking your application threads.

## Hızlı Yanıtlar
- **“highlight search results Java” ne anlama geliyor?** Arama sonuçlarında eşleşen terimleri görsel ipuçları (ör. HTML `<mark>` etiketleri) ile render etmeyi ifade eder, böylece kullanıcılar sorgunun her belgede nerede göründüğünü görebilir.  
- **Senkron indekslemeyi ne zaman kullanmalıyım?** Yeni eklenen belgelerin anında kullanılabilir olması gereken küçük ve orta ölçekli veri setleri için.  
- **Asenkron indeksleme ne zaman tercih edilir?** Büyük belge koleksiyonlarını işlerken veya uygulamanın yanıt vermeye devam etmesi gereken bir UI iş parçacığında çalışırken.  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme yeterlidir; tam lisans gelişmiş özellikleri açar ve kullanım limitlerini kaldırır.  
- **Hangi Java sürümü destekleniyor?** Java 8 veya üzeri.

## “highlight search results Java” nedir?
Java’da arama sonuçlarını vurgulamak, GroupDocs.Search tarafından döndürülen ham eşleşmeleri alıp eşleşen terimleri HTML (veya başka bir işaretleme dili) içinde sararak bir UI veya web sayfasında görüntülendiğinde öne çıkmasını sağlamaktır. Bu, her bir eşleşmenin bağlamını anında göstererek kullanıcı deneyimini iyileştirir.

## Neden Java için GroupDocs.Search kullanmalı?
GroupDocs.Search, yüksek performanslı, dil bağımsız bir motor sunar ve şunları destekler:
- Gerçek zamanlı indeksleme ve arama
- Büyük iş yükleri için asenkron işleme
- Yerleşik sonuç vurgulama
- Çok dilli ve özel analizör desteği  

Bu yetenekler, içerik yönetim sistemleri, e‑ticaret katalogları ve kurumsal belge depoları için ideal kılar.

## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- **Java Development Kit** (JDK 8 veya daha yeni) yüklü.
- **IntelliJ IDEA** veya **Eclipse** gibi bir IDE.
- İndekslemek istediğiniz belgeleri içeren bir klasör.
- Bağımlılık yönetimi için Maven (veya JAR dosyasını manuel olarak indirebilirsiniz).

### Gerekli Kütüphaneler ve Bağımlılıklar
Maven projenize GroupDocs.Search ekleyin:

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

### Ortam Kurulumu
- **JAVA_HOME**'unuzun uyumlu bir JDK'ye işaret ettiğini doğrulayın.
- IDE'nizde bir proje oluşturun ve yukarıdaki Maven yapılandırmasını ekleyin.
- Örnek metin, PDF veya Word dosyaları içeren bir dizin (ör. `documents/`) hazırlayın.

## GroupDocs.Search for Java Nasıl Kurulur
1. **Kütüphaneyi Kurun** – Yukarıdaki Maven snippet'ini kullanın veya JAR dosyasını [GroupDocs](https://releases.groupdocs.com/search/java/) adresinden indirin.  
2. **Lisans Alın** – Öncelikle bir deneme lisansı alın, ardından üretime geçtiğinizde yükseltin.  
3. **İndeksi Başlatın** – Aşağıdaki snippet, bir indeks klasörü oluşturmayı (veya açmayı) gösterir:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Java’da arama sonuçlarını vurgulama – Senkron İndeksleme
Senkron indeksleme, belgeleri anında işler ve yeni eklenen dosyaların hemen aranabilir olmasını sağlar.

### Adım 1: İndeksi oluşturun ve hata yönetimini ekleyin
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

### Adım 2: Belgeleri ekleyin ve bir arama çalıştırın
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Adım 3: Sonuçları işleyin ve **highlight search results Java**
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

`DocumentHighlighter`, eşleşen terimleri otomatik olarak `<mark>` etiketleri (veya yapılandırdığınız herhangi bir format) ile sarar ve size **highlighted search results** (vurgulanmış arama sonuçları) gösterime hazır hâle getirir.

## Java’da arama sonuçlarını vurgulama – Asenkron İndeksleme
Binlerce dosyayla çalışırken ana iş parçacığını engellemek istenmez. Asenkron indeksleme, motorun arka planda çalışmasını sağlar.

### Adım 1: Olay dinleyicileriyle indeksi kurun
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

### Adım 2: Asenkron modu etkinleştirin ve indekslemeyi başlatın
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

İndeks oluşturulurken uygulamanız diğer istekleri hizmet vermeye devam edebilir. `StatusChanged` olayı `Ready` (Hazır) rapor ettiğinde, güvenle arama yapabilir ve **highlighted search results Java** elde edebilirsiniz.

## **index documents java** Nasıl Yapılır – Pratik İpuçları
- **Batch size**: Büyük koleksiyonlar için klasörü daha küçük partilere bölerek bellek dalgalanmalarını önleyin.  
- **File filters**: `IndexingOptions.setFileExtensions` kullanarak yalnızca ihtiyacınız olan formatları (ör. `.pdf`, `.docx`) dahil edin.  
- **Re‑indexing**: Belgeler değiştiğinde tüm indeksi yeniden oluşturmak yerine `index.update(documentPath)` çağırın.

## Performans Düşünceleri
- **Memory**: Yığın kullanımını izleyin; çok sayıda büyük dosya işliyorsanız `-Xmx` değerini artırın.  
- **CPU**: Asenkron indeksleme iş yükünü dağıtır, ancak hâlâ CPU tüketir—JVisualVM ile izleyin.  
- **Result Highlighting**: Vurgulama küçük bir işlem ek yükü ekler; sonuçları tekrar tekrar göstermeniz gerekiyorsa oluşturulan HTML'i önbelleğe alın.

## Sıkça Sorulan Sorular

**S: Senkron ve asenkron indekslemeyi aynı uygulamada birleştirebilir miyim?**  
C: Evet. Küçük, sık güncellenen setler için senkron indeksleme, toplu ithalatlar veya arka plan görevleri için asenkron indeksleme kullanın.

**S: Vurgulama stilini nasıl özelleştirebilirim?**  
C: Eşleşen terimler etrafına istediğiniz HTML, CSS veya XML etiketlerini yazan özel bir `DocumentHighlighter` uygulaması sağlayın.

**S: GroupDocs.Search varsayılan olarak hangi dosya türlerini destekliyor?**  
C: Metin, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML ve dahili ayrıştırıcıları sayesinde daha birçok format.

**S: Aynı anda birden fazla dilde arama yapmak mümkün mü?**  
C: Kesinlikle. GroupDocs.Search çok‑dilli analizörler içerir; indeks oluştururken uygun `Analyzer`'ı yapılandırmanız yeterlidir.

**S: İndeks klasörünü nasıl güvence altına alabilirim?**  
C: İndeksi korumalı bir dizinde saklayın, uygun dosya sistemi izinlerini ayarlayın ve kütüphanenin güvenlik özellikleriyle indeksi şifrelemeyi düşünün.

---

**Son Güncelleme:** 2026-02-08  
**Test Edilen Sürüm:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs