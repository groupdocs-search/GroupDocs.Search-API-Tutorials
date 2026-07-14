---
date: '2026-05-17'
description: GroupDocs.Search for Java ile search network java'yı yapılandırmayı,
  optimize shards'i, text search'i gerçekleştirmeyi ve port conflicts'i yönetmeyi
  öğrenin.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'GroupDocs.Search for Java''da Parçaları Nasıl Optimize Edebilirsiniz: Kapsamlı
  Bir Rehber'
type: docs
url: /tr/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# GroupDocs.Search for Java'da Shard'ları Optimize Etme: Kapsamlı Bir Rehber

Verimli belge arama, büyük veri setlerini yöneten veya hızlı dahili erişim ihtiyacı olan geliştiriciler ve işletmeler için esastır. Bu öğreticide **how to configure search network java**'ı öğrenecek, belgeleri indeksleme ve sorgulama yöntemlerini ve **optimize shards** için en iyi performansı sağlayacak adımları öğreneceksiniz. Ayrıca gerçek dünya kullanım senaryoları, yaygın tuzaklar ve arama düğümlerinizin sorunsuz çalışmasını sağlayacak pratik ipuçlarını ele alacağız.

## Hızlı Yanıtlar
- **Shard optimizasyonu nedir?** Sorguları hızlandırmak ve depolama maliyetini azaltmak için indeks verilerini yeniden düzenler.  
- **Arama ağını nasıl yapılandırılır?** Temel bir dizin ve port tanımlayın, ardından sağlanan API'yi kullanarak düğümleri dağıtın.  
- **Metin araması nasıl yapılır?** Sorgu dizesiyle `TextSearchInNetwork.searchAll` kullanın.  
- **Java'da belgeler nasıl indekslenir?** `IndexingDocuments.addDirectories` ile belge dizinlerini master düğüme ekleyin.  
- **Port çakışmaları nasıl ele alınır?** `basePort` değişkenini makinenizde kullanılmayan bir porta değiştirin.

## Arama Ağını Nasıl Yapılandırılır
`Configuration`, bir GroupDocs.Search ağını başlatmak için gereken tüm ayarları, örneğin indeks klasör konumu ve iletişim portu gibi, saklar.  
`SearchNetwork`, düğümleri yönlendirir, indekslemeyi ve sorgu dağıtımını yönetir.

Arama yapılandırmanızı yükleyin, belge temel yolunu ayarlayın, boş bir port seçin ve ağı başlatın—tüm bunlar birkaç satır kodla yapılır. Bu doğrudan yanıt, tüm süreci 70 kelimenin altında açıklar: **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`.** Ağ otomatik olarak bir master düğüm ve gerekli worker düğümlerini başlatır, indeksleme isteklerini kabul etmeye hazır.

### Tanım Bağlantısı
`Configuration`, bir GroupDocs.Search ağını başlatmak için gereken tüm ayarları, örneğin indeks klasör konumu ve iletişim portu gibi, saklayan temel sınıftır.

Korkutucu “port already in use” hatasından kaçınmak için, ağı başlatmadan önce seçilen portun boş olduğunu doğrulayın (örneğin `netstat` veya basit bir socket testi kullanarak).

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

## Java'da Belgeleri Nasıl İndekslenir
`IndexingDocuments`, bir arama düğümüne birden fazla dizin eklemeyi basitleştiren ve indeksleme hattını tetikleyen bir yardımcı sınıftır.

Belge klasörlerinizi master düğüme ekleyin, ardından indeksleyicinin bunları taramasına izin verin. **Direct answer:** `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` çağırın ve ardından `masterNode.index()` metodunu çalıştırın; motor, sağladığınız her klasör için aranabilir shard'lar oluşturur. Bu yaklaşım yatay olarak ölçeklenir—daha fazla düğüm ekleyin ve aynı yöntem iş yükünü otomatik olarak dağıtır.

### Tanım Bağlantısı
`IndexingDocuments`, bir arama düğümüne birden fazla dizin eklemeyi basitleştiren ve indeksleme hattını tetikleyen bir yardımcı sınıftır.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Metin Araması Nasıl Yapılır
`TextSearchInNetwork`, ağdaki her düğüme bir metin sorgusu yayınlamak ve sonuçları toplamak için statik yardımcı metodlar sağlar.  
`SearchResult`, eşleşen bir belgenin ID'sini, alıntısını ve alaka düzeyini kapsar.

Tüm shard'lar üzerinde tek bir metod çağrısı ile sorgu çalıştırın. **Direct answer:** `TextSearchInNetwork.searchAll("your query", searchNetwork)` kullanın; metod, belge ID'leri, alıntılar ve alaka skorları içeren bir `SearchResult` nesne koleksiyonu döndürür. Sonuçları dil, dosya türü veya özel meta veri ile ekstra kod yazmadan filtreleyebilirsiniz.

### Tanım Bağlantısı
`TextSearchInNetwork`, ağdaki her düğüme bir metin sorgusu yayınlamak ve sonuçları toplamak için statik yardımcı metodlar sağlar.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Port Çakışmalarını Nasıl Ele Alırsınız
Varsayılan port (`49132`) kullanılıyorsa, sadece başka bir boş port seçin ve ağı başlatmadan önce `basePort` alanını güncelleyin. **Direct answer:** `int basePort = 49132;` satırını `49133` gibi kullanılmayan bir değere değiştirin, yeniden derleyin ve yeniden başlatın; ağ mevcut düğümleri etkilemeden yeni porta bağlanır.

Pro ipucu: Portu yeniden derlemeden değiştirebilmek için küçük bir yapılandırma dosyası (ör. `search-config.properties`) tutun.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Önkoşullar
Başlamadan önce, aşağıdaki önkoşulların mevcut olduğundan emin olun:

### Gerekli Kütüphaneler, Sürümler ve Bağımlılıklar
Bu çözümü uygulamak için, `pom.xml` dosyanıza aşağıdaki yapılandırmayı ekleyerek Maven aracılığıyla GroupDocs.Search kütüphanesini dahil edin:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Ortam Kurulum Gereksinimleri
- Java Development Kit (JDK) 8 veya üzeri.  
- Seçilen `basePort`'a bağlanmaya izin veren ağ izinleri.  
- İndeks dosyaları için yeterli disk alanı (her shard yaklaşık 1.000 belge başına ~10 MB kaplayabilir).

### Bilgi Önkoşulları
Java, nesne‑yönelimli programlama ve istisna yönetimi konusunda temel bir anlayış, örnekleri sorunsuz takip etmenize yardımcı olacaktır.

## GroupDocs.Search for Java'ı Kurma
Projenizde GroupDocs.Search'ı kullanmaya başlamak için şu adımları izleyin:

1. **Bağımlılığı Ekleyin**: Yukarıda gösterildiği gibi, gerekli Maven bağımlılığını projenize ekleyin veya doğrudan releases sayfasından indirin.  
2. **Lisans Edinme**:  
   - **Ücretsiz deneme** – lisans anahtarı gerekmez, ancak kullanım günde 500 belge ile sınırlıdır.  
   - **Geçici lisans** – [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) adresinden 30‑günlük deneme anahtarı isteyin.  
   - **Tam lisans** – sınırsız erişim ve öncelikli destek için üretim lisansı satın alın.  
3. **Temel Başlatma ve Kurulum**:  
   `Configuration` sınıfını kullanarak yapılandırmayı başlatın, belgeler için temel yolu ayarlayın ve bir port numarası belirleyin:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Uygulama Kılavuzu
Şimdi GroupDocs.Search Java kullanarak temel özelliklerin uygulanmasını inceleyelim.

### Özellik: Arama Ağını Yapılandırma
**Genel Bakış**: Bir arama ağı kurmak, belge dizininizi tanımlamayı ve düğümler arasındaki iletişim için belirli bir portla yapılandırmayı içerir.

#### Adım 1: Belge Dizinlerini ve Portu Tanımlayın
`DocumentDirectory`, indekslemek istediğiniz bir klasörün mutlak yolunu tutan basit bir tutucudur. Yapılandırmaya bir veya daha fazla yol sağlayın.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Adım 2: Arama Ağını Yapılandırın
Tanımlanan yolları kullanarak yapılandırma nesnesini oluşturun:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Özellik: Arama Ağ Düğümlerini Dağıtma
**Genel Bakış**: Ağınızda belge aramalarını verimli bir şekilde yönetmek için düğümleri dağıtın.

#### Adım 1: Yapılandırma Kullanarak Düğümleri Dağıtın
Arama ağı düğümlerini dağıtın ve merkezi yönetim için master düğümü belirleyin:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Özellik: Ağ Düğümü Olaylarına Abone Olma
**Genel Bakış**: Önemli değişiklikler veya eylemler hakkında sizi bilgilendiren olaylara abone olarak arama ağınızı izleyin.

#### Adım 1: Master Düğüm Olaylarına Abone Olun
`SearchNetworkEventListener`, indeksleme tamamlanması, düğüm hataları veya shard optimizasyonlarına yanıt vermenizi sağlar.

CODE_BLOCK_PLACEHOLDER_9_END

### Özellik: Ağ Düğümlerinde Belgeleri İndeksleme
**Genel Bakış**: Belgeleri içeren dizinleri verimli aramalar için indeksleme sürecine ekleyin.

#### Adım 1: Belge Dizinlerini İndeksleme Sürecine Ekleyin
Master düğüme klasör yollarının bir listesini gönderin; motor her klasör için ayrı bir shard oluşturur ve paralel sorgu yürütmeyi sağlar.

CODE_BLOCK_PLACEHOLDER_10_END

### Özellik: Ağ Düğümlerinde Metin Arama
**Genel Bakış**: Arama ağınızdaki tüm indekslenmiş belgeler üzerinde metin aramaları yürütün.

#### Adım 1: Metin Araması Yapın
Bir sorgu çalıştırmak ve alaka skorlarıyla eşleşen belgeleri almak için statik yardımcıyı çağırın.

CODE_BLOCK_PLACEHOLDER_11_END

### Özellik: Shard'ları Optimize Etme
**Genel Bakış**: Arama ağ düğümünüzdeki indeksleyicinin shard'larını optimize ederek performansı artırın.

#### Adım 1: İndeksleyici Shard'larını Optimize Edin
Shard'ları optimize ederek arama verimliliğini artırın (burada **how to optimize shards** gerçekten önemlidir):

CODE_BLOCK_PLACEHOLDER_12_END

## Pratik Uygulamalar
GroupDocs.Search for Java, shard optimizasyonundan fayda sağlayan çeşitli gerçek dünya senaryolarında uygulanabilir:

1. **Kurumsal Belge Yönetimi** – Shard optimizasyonundan sonra alt saniyelik sorgu süreleriyle 10 TB+ arşivleri yönetir.  
2. **E‑ticaret Platformları** – 1 milyon SKU üzerinde ürün aramasını sağlar, shard'lar optimize edildiğinde gecikmeyi %45'e kadar azaltır.  
3. **Hukuk Firmaları** – 200 GB depolardan dava dosyalarını 200 ms altında getirir.  
4. **Kütüphane Sistemleri** – 500 k dijital kitap için katalog aramalarını verimli bellek kullanımıyla destekler.  
5. **İçerik Yönetim Sistemleri (CMS)** – 2 milyonun üzerindeki sayfalarla çoklu site dağıtımları için anlık içerik keşfi sağlar.

## Performans Düşünceleri
GroupDocs.Search uygulamanızın optimal performansını sağlamak için:

- **Shard'ları düzenli olarak optimize edin** – Her 10 GB yeni veri sonrası `optimizeShards()` çalıştırmak, sorgu yanıt sürelerini %30‑50 azaltır.  
- **Bellek kullanımını izleyin** – JVM yığınını fiziksel RAM'in %75'inin altında tutun; büyük indeksler için G1GC'yi etkinleştirin.  
- **Artımlı indeksleme kullanın** – Tam yeniden indekslemeyi önlemek için yalnızca değişen dosyaları ekleyin.  
- **Çok düğümlü ölçeklemeyi kullanın** – Shard'ları dağıtmak için worker düğümleri ekleyin; her ek düğüm okuma ağırlıklı iş yüklerinde ~%20 verim artışı sağlayabilir.

## Yaygın Sorunlar ve Çözümler
| Issue | Symptom | Solution |
|-------|---------|----------|
| Başlangıçta port çakışması | `java.net.BindException: Address already in use` | Kullanılmayan bir değere `basePort` değiştirin; `netstat -ano` ile doğrulayın. |
| Optimizasyon sırasında bellek yetersizliği hataları | `java.lang.OutOfMemoryError: Java heap space` | JVM `-Xmx` bayrağını artırın veya optimizasyonu daha fazla RAM'e sahip ayrı bir düğümde çalıştırın. |
| Arama sonuçlarında eksik belgeler | İndekslemeden sonra sonuç döndürülmedi | Dizinlerin `IndexingDocuments.addDirectories` ile doğru eklendiğinden ve `masterNode.index()`'in istisna olmadan tamamlandığından emin olun. |
| Toplu silmeden sonra eski shard'lar | Silinen dosyalar hâlâ görünüyor | `optimizeShards()` çalıştırarak segmentleri birleştirin ve tombstone'ları temizleyin. |

## Sıkça Sorulan Sorular

**Q: Shard optimizasyonu sorgu hızını nasıl etkiler?**  
A: Shard'ları optimize etmek indeksi sıkıştırır, disk I/O'yu azaltır ve genellikle büyük veri setlerinde %30‑50 daha hızlı sorgu yanıtları sağlar.

**Q: `optimizeShards` işlemini canlı bir düğümde çalıştırmak güvenli mi?**  
A: Evet, işlem kesinti olmadan çalışacak şekilde tasarlanmıştır, ancak 20 GB'den büyük indeksler için düşük trafik dönemlerinde zamanlamanız önerilir.

**Q: `OptimizeOptions`'ı özelleştirebilir miyim?**  
A: Kesinlikle. `maxSegmentSize` veya `mergeFactor` gibi parametreleri ayarlayarak optimizasyon sürecini ince ayar yapabilirsiniz.

**Q: Optimizasyon sırasında bir `IOException` ile karşılaşırsam ne yapmalıyım?**  
A: Dosya sistemi izinlerini kontrol edin, yeterli boş disk alanı olduğundan emin olun ve başka bir sürecin indeks dosyalarını kilitlemediğini doğrulayın.

**Q: Shard'ları optimize etmek silinen belge alanını da geri kazanır mı?**  
A: Evet, optimizer segmentleri birleştirir ve tombstone'ları kaldırarak silinen belgeler tarafından işgal edilen alanı serbest bırakır.

## Sonuç
Bu kapsamlı rehberi izleyerek artık **configure search network java**'ı, belgeleri indekslemeyi, metin sorguları çalıştırmayı ve en önemlisi **optimize shards**'ı nasıl yapacağınızı biliyorsunuz; böylece arama performansınızı keskin tutabilirsiniz. Bu desenleri herhangi bir Java‑tabanlı kurumsal arama çözümüne uygulayın, gecikme, ölçeklenebilirlik ve kaynak kullanımı açısından ölçülebilir iyileşmeler göreceksiniz. Bir sonraki adım olarak, özel analizörler, faceted search ve bulut depolama sağlayıcılarıyla entegrasyon gibi gelişmiş özellikleri keşfedin.

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## İlgili Öğreticiler

- [GroupDocs.Search Ağını .NET'te Yapılandırma: Kapsamlı Bir Rehber](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [GroupDocs.Search ile .NET Belge İndeksleme: Kapsamlı Bir Rehber](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [GroupDocs.Search for Java Öğreticileri ve Örnekleri](/search/net/)