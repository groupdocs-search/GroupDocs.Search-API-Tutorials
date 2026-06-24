---
date: '2026-05-17'
description: GroupDocs Maven bağımlılığını nasıl ekleyeceğinizi, Java search network'ü
  nasıl kuracağınızı ve hızlı, ölçeklenebilir belge geri getirme için dizinlere klasör
  eklemeyi öğrenin.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Search Network için GroupDocs Maven Bağımlılığını Nasıl Eklenir
type: docs
url: /tr/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# GroupDocs Maven Bağımlılığını Arama Ağı İçin Nasıl Eklenir

Bu kapsamlı rehberde **groupdocs Maven bağımlılığını nasıl ekleyeceğinizi**, GroupDocs.Search kullanarak sağlam bir Java arama ağı yapılandırmayı ve parçalarınızı senkronize tutmayı öğreneceksiniz. Hukuki özetler, finansal tablolar veya akademik makaleler indeksleseniz de, aşağıdaki adımlar arama yapılabilir indeksler oluşturmanıza, sorgu yükünü düğümler arasında dağıtmanıza ve veri tutarlılığını minimum çabayla korumanıza yardımcı olacak.

## Hızlı Yanıtlar
- **GroupDocs Maven bağımlılığı nedir?** Java projeleri için GroupDocs.Search kütüphanesini paketleyen bir Maven artefaktıdır.  
- **Arama ağı neden kullanılır?** İndeksleme ve sorgu yükünü birden çok düğüm arasında dağıtarak hız ve güvenilirliği artırır.  
- **Dizinlere klasör nasıl eklenir?** Master düğümde `IndexingDocuments.addDirectories` metodunu kullanın.  
- **Parçalar nasıl senkronize edilir?** Her düğümün `Indexer` nesnesinde `SynchronizeOptions` çağırın.  
- **Lisans gerekli mi?** Evet, üretim kullanımı için bir deneme veya ticari lisans gereklidir.

## GroupDocs Maven Bağımlılığı Nedir?

`GroupDocs Maven bağımlılığı`, Java projeleri için GroupDocs.Search kütüphanesini paketleyen bir Maven artefaktıdır.  
Arama yapılabilir indeksler oluşturmak, ağ düğümlerini yönetmek ve hızlı sorgular çalıştırmak için gereken tüm sınıfları sağlar; Maven de geçişli bağımlılıkları otomatik olarak çözer, böylece `pom.xml` dosyanıza birkaç satır ekleyerek kullanıma hazır bir arama motoru elde edersiniz.

## GroupDocs Maven Bağımlılığı Nasıl Eklenir

Depo ve bağımlılık girdilerini `pom.xml` dosyanıza ekleyin, ardından `mvn clean install` komutunu çalıştırın; Maven `groupdocs-search` JAR dosyasını ve gerekli kütüphaneleri indirir, API projenizde kullanılabilir hâle gelir. Derleme başarılı olduğunda `com.groupdocs.search` sınıflarını hemen kullanmaya başlayabilirsiniz.

### Maven Yapılandırması

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

> **İpucu:** Resmi sürüm sayfasını kontrol ederek sürüm numarasını güncel tutun.

JAR dosyasını doğrudan resmi siteden de indirebilirsiniz: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Neden Arama Ağı Kullanılır?

Bir arama ağı, indeksi ayrı düğümlerde bulunan parçalar (shard) halinde bölerek yatay ölçeklenebilirlik sağlar. GroupDocs.Search **50+ giriş formatını** destekler ve **yüzlerce sayfalık belgeleri** belleğe tamamını yüklemeden işleyebilir; veri hacmi arttıkça bile alt saniyelik sorgu yanıtları sunar.

## Ön Koşullar

- **JDK** (11 veya üzeri) yüklü olmalı.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Temel Java bilgisi, Maven tecrübesi ve ağ düğümü kavramlarına aşinalık.  
- Geçerli bir GroupDocs.Search lisansı (ücretsiz deneme veya ticari).

## Temel Başlatma ve Kurulum

Bir indeks klasörü oluşturun:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Bu basit adım, sonraki ağ yapılandırması için ortamı hazırlar.

## Uygulama Kılavuzu

### Özellik 1: Arama Ağı Yapılandırması

#### Genel Bakış

Arama ağını yapılandırmak, düğümlerin iletişim kuracağı dosya yollarını ve portları ayarlar.

##### Yolları ve Portları Ayarlama

Configuration sınıfı, arama kümesi için ağ yollarını, portları ve diğer ayarları tutar.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
`configuration` nesnesi artık arama ağınız için gerekli tüm ayarları içeriyor.

### Özellik 2: Arama Ağı Düğümlerinin Dağıtımı

#### Genel Bakış

Düğümleri dağıtarak iş yükünü ağınızda paylaştırın. Master düğüm işlemleri ve olayları yönetir.

##### Dağıtım Kodu

SearchNetworkNode, master veya worker olarak görev alabilen bir arama ağı düğümünü temsil eder.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Özellik 3: Arama Ağı Düğüm Olaylarına Abone Olma

#### Genel Bakış

Olayları dinlemek, ağınızdaki değişiklikleri veya güncellemeleri dinamik olarak ele almanızı sağlar.

##### Abonelik Uygulaması

SearchNetworkNodeEvents, düğüm yaşam döngüsü ve indeksleme eylemleri için olay kancaları sunar.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Özellik 4: Dizinlere Klasör Ekleme

#### Genel Bakış

Klasör eklemek, belgelerinizin aranabilir hâle gelmesini sağlayan temel adımdır.

##### Belge Ekleme

`IndexingDocuments.addDirectories` klasör yollarını işleme alınacak indekse ekler.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Özellik 5: Arama Ağı Düğümünde Parçaları Senkronize Etme

#### Genel Bakış

Senkronizasyon, tüm parçalar arasında veri tutarlılığını sağlar.

##### Senkronizasyon Kodu

`SynchronizeOptions` parçaların düğümler arasında nasıl senkronize edileceğini yapılandırır.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Özellik 6: Arama Ağı Düğümlerini Kapatma

#### Genel Bakış

Düğümleri düzgün bir şekilde kapatmak kaynakları serbest bırakır ve bellek sızıntılarını önler.

##### Düğüm Kapatma

`close()` kaynakları serbest bırakır ve arama ağı düğümünü kapatır.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Pratik Uygulamalar

1. **Hukuki Belge Yönetimi** – Dava dosyalarını ve içtihatları hızlıca bulun.  
2. **Finansal Kayıt Tutma** – Beyanlar ve denetim izlerini saniyeler içinde erişin.  
3. **Akademik Araştırma** – Binlerce makale arasında ilgili atıfları arayın.

## Performans Düşünceleri

- **Sorguları Optimize Et** – Yanıt süresini azaltmak için özlü sorgular yazın.  
- **Bellek Yönetimi** – JVM yığın kullanımını izleyin; büyük indeksler için GC ayarlarını gözden geçirin.  
- **Ölçekleme Stratejisi** – Veri hacmi ve sorgu yüküne göre düğüm sayısını orantılı olarak artırın.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|----------|
| Düğümler bağlanamıyor | Port çakışması | `basePort` değerini kullanılmayan bir porta değiştirin |
| İndeks güncellenmiyor | Olay aboneliği eksik | `SearchNetworkNodeEvents.subscribe(masterNode)` çağrısının yapıldığından emin olun |
| Yüksek gecikme | Yetersiz parça sayısı | Düğüm sayısını artırın ve belge dağılımını dengeleyin |

## Sıkça Sorulan Sorular

**S: GroupDocs.Search kullanmanın temel faydası nedir?**  
C: Büyük belge setlerinde hızlı, ölçeklenebilir arama yetenekleri sunar ve minimum yapılandırma gerektirir.

**S: Arama ağında düğüm yapılandırmalarını özelleştirebilir miyim?**  
C: Evet, `Configuration` nesnesi üzerinden özel yollar, portlar ve diğer seçenekleri ayarlayabilirsiniz.

**S: Ağ çalışırken dizinlere klasör nasıl eklenir?**  
C: Yeni klasörleri indekslemek istediğinizde `IndexingDocuments.addDirectories(masterNode, "path")` metodunu çağırın.

**S: Yeni bir düğüm ağa katıldığında parçalar nasıl senkronize edilir?**  
C: Yukarıda gösterilen `synchronizeShards` metodunu yeni eklenen düğümde çalıştırın.

**S: Geliştirme için lisans gerekiyor mu?**  
C: Test için ücretsiz deneme lisansı yeterlidir; üretim için ticari lisans gereklidir.

## Sonuç

Bu rehberi izleyerek **groupdocs Maven bağımlılığını nasıl ekleyeceğinizi**, çoklu düğüm arama ağı yapılandırmayı, dizin klasörleri eklemeyi ve parçaları senkronize etmeyi öğrendiniz. Bu adımlar, organizasyonunuzun ihtiyaçlarıyla büyüyebilen yüksek performanslı bir belge arama çözümünün temelini oluşturur.

---

**Son Güncelleme:** 2026-05-17  
**Test Edilen Sürüm:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [GroupDocs.Search for Java Eğitimleri ve Örnekleri](/search/net/)
- [GroupDocs.Search Ağını .NET'te Yapılandırma: Kapsamlı Rehber](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [GroupDocs.Search ile .NET'te Belge Yönetim Sistemleri İçin Arama Ağı Nasıl Uygulanır](/search/net/search-network/implement-search-network-groupdocs-dotnet/)