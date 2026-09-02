---
date: '2026-04-02'
description: Java’da indeks deposu oluşturmayı, belgelere indeks eklemeyi, gerçek
  zamanlı indeksleme olaylarını yönetmeyi ve GroupDocs.Search for Java kullanarak
  birden fazla indeks üzerinde arama yapmayı öğrenin.
keywords:
- create index repository java
- add documents to index
- search across multiple indices
title: 'GroupDocs.Search ile Java’da indeks deposu nasıl oluşturulur: Verimli Belge
  İndeksleme ve Arama'
type: docs
url: /tr/java/searching/master-groupdocs-search-java-indexing-search/
weight: 1
---

# GroupDocs.Search ile java indeks deposu oluşturma: Verimli Belge İndeksleme ve Arama

Günümüz dijital ortamında, büyük veri kümelerini verimli bir şekilde yönetmek, dünya çapındaki geliştiricilerin karşılaştığı bir zorluktur. **Bu öğretici, GroupDocs.Search for Java kullanarak java indeks deposu oluşturmayı** gösterir, böylece belgelere indeks ekleyebilir, gerçek zamanlı indeksleme olaylarına yanıt verebilir ve birden çok indeks üzerinde hızlı aramalar yapabilirsiniz. Ortamı kurma, bir indeks deposu oluşturma, olaylara abone olma ve güçlü sorgular yürütme adımlarını net, adım adım kod örnekleriyle ele alacağız.

## Hızlı Yanıtlar
- **İlk adım nedir?** Projenize GroupDocs.Search Maven deposunu ve bağımlılığını ekleyin.  
- **Bir indeks deposu nasıl oluşturulur?** Her klasör için `IndexRepository` örneği oluşturun ve `Index` nesnelerini ekleyin.  
- **İndeksleme ilerlemesini izleyebilir miyim?** Evet—gerçek zamanlı güncellemeler için `OperationProgressChanged` olaylarına abone olun.  
- **Birden çok indeks üzerinde nasıl arama yapılır?** Tüm indeksleri ekledikten sonra `indexRepository.search(query)` çağırın.  
- **Gerekli Java sürümü nedir?** JDK 8 veya üzeri.

## Öğrenecekleriniz
- GroupDocs.Search ile geliştirme ortamınızı kurma ve yapılandırma.  
- **java indeks deposu nasıl oluşturulur** ve birden çok indeksi verimli bir şekilde yönetme.  
- Anlık geri bildirim için **gerçek zamanlı indeksleme olaylarına** abone olma.  
- **Belge ekleme** ve güncel tutma.  
- Tek bir sorgu ile **birden çok indeks üzerinde arama** gerçekleştirme.  
- Pratik uygulamalar ve performans ayarlama ipuçları.

### Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
- **Java Development Kit (JDK)**: Sürüm 8 veya üzeri.  
- **Entegre Geliştirme Ortamı (IDE)**: IntelliJ IDEA veya Eclipse gibi.  
- **Maven**: Bağımlılıkları yönetmek için (isteğe bağlı ancak önerilir).

#### Gerekli Kütüphaneler ve Bağımlılıklar
GroupDocs.Search for Java'ı kullanmak için `pom.xml` dosyanıza aşağıdaki Maven yapılandırmasını ekleyin:

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

Alternatif olarak, en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Lisans Edinimi
Tüm özellikleri sınırsız olarak keşfetmek için ücretsiz deneme lisansı alabilir veya tam lisans satın alabilirsiniz. Lisanslama detayları ve geçici lisanslar için [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin.

## GroupDocs.Search for Java'ı Kurma

GroupDocs.Search'i Java projenizde kullanmaya başlamak için, Maven yüklü olduğundan emin olun (Maven kullanmıyorsanız, kütüphaneyi manuel olarak kurun). Aşağıdaki adımları izleyin:

1. **Depo ve Bağımlılık Ekle**: GroupDocs.Search'i dahil etmek için sağlanan Maven yapılandırmasını kullanın.  
2. **Temel Başlatma**:

```java
import com.groupdocs.search.Index;

// Initialize an index repository instance
IndexRepository indexRepository = new IndexRepository();
```

## java indeks deposu oluşturma ve birden çok indeksi yönetme

İndeksleme için yapılandırılmış bir sistem oluşturmak, verimli belge yönetimi ve aranabilirlik sağlar. Bu numaralı adımları izleyin; her adım kod bloğundan önce kısa bir açıklama içerir, böylece ne olduğunu tam olarak bilirsiniz.

### Adım 1: İndeks ve Belgeler İçin Yolları Tanımlama
```java
String indexFolder1 = "YOUR_DOCUMENT_DIRECTORY\\Index1";
String indexFolder2 = "YOUR_DOCUMENT_DIRECTORY\\Index2";
String documentFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentFolder2 = "YOUR_DOCUMENT_DIRECTORY";
```

### Adım 2: `IndexRepository` Örneği Oluşturma
```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexRepository;

// Initialize the index repository
IndexRepository indexRepository = new IndexRepository();
```

### Adım 3: İndeksleri Oluşturma veya Yükleme ve Depoya Ekleme
```java
// Load or create indices
Index index1 = new Index(indexFolder1);
indexRepository.addToRepository(index1);

Index index2 = new Index(indexFolder2);
indexRepository.addToRepository(index2);
```
Bu yapılandırma, **birden çok indeksi** sorunsuz bir şekilde **yönetmenizi** sağlar.

### Adım 4: **Belge ekleme** – Her İndeksi Doldurma
```java
// Add documents to the first index
index1.add(documentFolder1);

// Add documents to the second index
index2.add(documentFolder2);
```

### Adım 5: Depodaki Tüm İndeksleri Güncelleme
```java
// Synchronize all indices with new document data
indexRepository.update();
```
`update()` çalıştırmak, arama sonuçlarınızın her zaman en son değişiklikleri yansıtmasını sağlar.

## Gerçek zamanlı indeksleme olaylarına abone olma

İndeksleme olaylarını izlemek, uygulama yanıtını artırabilir ve anlık geri bildirim sağlayabilir. İşte bu olaylara nasıl bağlanacağınız.

### Adım 1: İndeks Klasörü İçin Yolları Tanımlama
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\Index";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

### Adım 2: `IndexRepository` Örneği Oluşturma ve Olaylara Abone Olma
```java
import com.groupdocs.search.events.EventHandler;
import com.groupdocs.search.events.OperationProgressEventArgs;

// Initialize the index repository
IndexRepository indexRepository = new IndexRepository();

// Load or create an index
Index index = new Index(indexFolder);
indexRepository.addToRepository(index);

// Subscribe to indexing progress events
indexRepository.getEvents().OperationProgressChanged.add(new EventHandler<OperationProgressEventArgs>() {
    @Override
    public void invoke(Object sender, OperationProgressEventArgs args) {
        System.out.println("Document indexed: " + args.getIndexedDocumentName());
    }
});
```
Bu işleyici, her belge indekslendiğinde bir mesaj yazdırır ve size **gerçek zamanlı indeksleme olayları** sağlar.

### Adım 3: Olayları Tetiklemek İçin Belgeler Ekleme
```java
// Start adding documents to trigger events
index.add(documentFolder);
```

## Birden çok indeks üzerinde arama

Tüm indekslerinizi kapsayan bir arama yürütmek, hızlı bilgi elde etmek için esastır.

### Adım 1: Yolları Tanımlama ve Depoyu Başlatma
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\Index";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Create or load the index repository
IndexRepository indexRepository = new IndexRepository();
indexRepository.addToRepository(new com.groupdocs.search.Index(indexFolder));
```

### Adım 2: Belgeler Ekleme ve Aramayı Gerçekleştirme
```java
new com.groupdocs.search.Index(indexFolder).add(documentFolder);

String query = "decisively";
SearchResult result = indexRepository.search(query);
// Process search results (implement as needed)
```
Bu kurulumla tek bir sorgu dizesi kullanarak **birden çok indeks üzerinde arama** yapabilirsiniz.

## Pratik Uygulamalar
1. **Kurumsal Belge Yönetimi** – Anlık erişim için büyük kurumsal kütüphaneleri indeksleyin.  
2. **Hukuki Dava Geri Getirme Sistemleri** – İlgili dava dosyalarını hızlı bulun.  
3. **Müşteri Desteği** – Belirli anahtar kelimelerle geçmiş biletleri veya e-postaları çekin.  
4. **İçerik Toplama Platformları** – Çeşitli kaynaklardan milyonlarca makaleyi yönetin.

## Performans Hususları
- İndeksi güncel tutmak için düzenli olarak `indexRepository.update()` çalıştırın.  
- Bellek kullanımını izleyin; büyük veri kümeleri ayrı indekslere bölünmeyi gerektirebilir.  
- **Gerçek zamanlı indeksleme olaylarını** kullanarak gereksiz tam yeniden indekslemeyi önleyin.  

## Sonuç
Bu kılavuzu izleyerek GroupDocs.Search ile **java indeks deposu oluşturmayı**, **belge eklemeyi**, **gerçek zamanlı indeksleme olaylarını** dinlemeyi ve hızlı **birden çok indeks üzerinde arama** yapmayı öğrendiniz. Bir sonraki adım olarak, [GroupDocs documentation](https://docs.groupdocs.com/search/java/) adresindeki daha gelişmiş özellikleri keşfedin.

## Sık Sorulan Sorular

**S: GroupDocs.Search'ı diğer Java çerçeveleriyle kullanabilir miyim?**  
E: Evet, Spring Boot, Jakarta EE ve diğer popüler çerçevelerle sorunsuz bir şekilde entegre olur.

**S: Çok büyük belge koleksiyonlarıyla nasıl başa çıkmalıyım?**  
E: Toplu indeksleme kullanın ve verileri birkaç indekse bölmeyi düşünün, ardından yukarıda gösterildiği gibi bunlar arasında arama yapın.

**S: Hangi lisans seçenekleri mevcuttur?**  
E: Ürünü değerlendirmek için ücretsiz deneme lisansı ile başlayın; üretim kullanımı için tam lisans gereklidir.

**S: Arama sonuçlarının alaka sıralamasını özelleştirmek mümkün mü?**  
E: Kesinlikle – `SearchSettings` API'si aracılığıyla sıralama kriterlerini ayarlayabilirsiniz.

**S: İndeksleme hataları için sorun giderme ipuçlarını nerede bulabilirim?**  
E: Ayrıntılı günlük kaydını etkinleştirin ve sorunlu dosyaları belirlemek için `OperationProgressChanged` olaylarına abone olun.

## Kaynaklar
- **Documentation**: [GroupDocs Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs API](https://apireference.groupdocs.com/search/java/)

---

**Last Updated:** 2026-04-02  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---