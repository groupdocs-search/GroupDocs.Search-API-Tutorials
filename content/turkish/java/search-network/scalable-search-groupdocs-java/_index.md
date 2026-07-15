---
date: '2026-05-22'
description: GroupDocs.Search for Java kullanarak belgeleri dizine eklemeyi ve ölçeklenebilir
  bir arama ağı oluşturmayı öğrenin. Birden fazla sunucu üzerinde aramayı destekler.
keywords:
- build scalable search network
- add documents to index
- search across multiple servers
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  headline: Build Scalable Search Network – Index Docs with GroupDocs Java
  type: TechArticle
- description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  name: Build Scalable Search Network – Index Docs with GroupDocs Java
  steps:
  - name: Define Base Path and Port
    text: The `SearchNetworkNode` class represents a single node that participates
      in the distributed index.
  - name: Configure the Network
    text: '`NetworkConfiguration` holds the common settings (base path, ports, replication
      factor) that every node reads at startup.'
  - name: Deploy Nodes Using Configuration
    text: '`SearchNetworkNode` instances are started with the same configuration file,
      allowing them to discover each other via the defined base port range.'
  - name: Define Subscription Method
    text: '`NodeEventListener` is an interface you implement to receive callbacks
      for indexing progress, errors, and node health changes.'
  - name: Use Subscription Method
    text: Register your listener with each node so that you get real‑time feedback
      during large batch operations.
  type: HowTo
- questions:
  - answer: Change the `basePort` variable in your configuration code to an available
      port.
    question: How do I handle port conflicts when deploying nodes?
  - answer: Yes, it supports real‑time indexing with appropriate configurations.
    question: Can GroupDocs.Search be used for real‑time indexing?
  - answer: Network connectivity and incorrect path settings are frequent culprits.
      Ensure all paths and ports are correctly configured.
    question: What are some common issues during node deployment?
  - answer: Absolutely. You can call `index.add(...)` on any node, and the network
      will distribute the new workload automatically.
    question: Is it possible to add documents to index after the network is running?
  - answer: A temporary trial license is sufficient for testing; a commercial license
      is required for production use.
    question: Do I need a license for development testing?
  type: FAQPage
title: Ölçeklenebilir Arama Ağı Oluşturun – Belgeleri GroupDocs Java ile Dizinleyin
type: docs
url: /tr/java/search-network/scalable-search-groupdocs-java/
weight: 1
---

# Ölçeklenebilir Arama Ağı Oluşturun – Belgeleri GroupDocs.Java ile Dizinle

Bu öğreticide, GroupDocs.Search for Java ile **belgeleri indekse eklemeyi** ve **ölçeklenebilir bir arama ağı oluşturmayı** öğreneceksiniz. Bir arama ağı yapılandırmayı, düğümleri dağıtmayı ve olayları yönetmeyi adım adım göstereceğiz, böylece uygulamanız birden fazla sunucu üzerinde büyük belge koleksiyonlarını verimli bir şekilde işleyebilir.

## Hızlı Yanıtlar
- **“belgeleri indekse eklemek” ne anlama gelir?** Bu, dosyaları aranabilir bir indekse eklemek anlamına gelir, böylece hızlı bir şekilde sorgulanabilir.  
- **Bu yeteneği sağlayan kütüphane hangisidir?** GroupDocs.Search for Java.  
- **Bir lisansa ihtiyacım var mı?** Geçici bir deneme lisansı mevcuttur; üretim için ticari bir lisans gereklidir.  
- **Yatay olarak ölçeklendirebilir miyim?** Evet—birden fazla SearchNetworkNode örneği dağıtarak.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya daha üstü.

## Belgeleri indekse eklemek nedir?
Kaynak dosyalarınızı (PDF, DOCX, PPTX, vb.) GroupDocs.Search motoruna yükleyin; motor metni çıkarır, terim‑frekans tabloları oluşturur ve bunları bir indeks dosyasında saklar. Oluşan indeks, çok sayfalı koleksiyonlarda bile saniyenin altında anahtar kelime sorgularına olanak tanır.

## Ağ ortamında GroupDocs.Search for Java neden kullanılmalı?
İndeksleme ve arama iş yüklerini birden fazla düğüm arasında dağıtarak, veri kaynağına yakın işleyerek sorgu gecikmesini azaltır ve düğümleri kesintisiz ekleyip kaldırabilirsiniz. Bu mimari, **birden fazla sunucu arasında arama** yapmanıza izin verir ve performansı tutarlı tutar.

## Önkoşullar
- **Java Development Kit (JDK) 8+** yüklü.  
- **Maven** bağımlılık yönetimi için.  
- Java ve Maven proje yapısına temel aşinalık.

### Gerekli Kütüphaneler, Sürümler ve Bağımlılıklar
GroupDocs.Search for Java'ı uygulamak için Maven projenize aşağıdakileri ekleyin:

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

Alternatif olarak, en son sürümü [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz. Sürümleri ayrıca [GroupDocs Search Java sürümleri](https://releases.groupdocs.com/search/java/) adresinde bulabilirsiniz.

### Ortam Kurulum Gereksinimleri
- Sisteminizde JDK 8 veya daha üstü yüklü.  
- Maven yüklü ve Maven projesi kullanıyorsanız yapılandırılmış.

### Bilgi Önkoşulları
- Java programlamaya temel bir anlayış.  
- Maven'de bağımlılık yönetimine aşinalık.

## GroupDocs.Search for Java'ı Kurma
1. **Maven Kurulumu**: Yukarıda gösterildiği gibi `pom.xml` dosyanıza depo ve bağımlılığı ekleyin.  
2. **Doğrudan İndirme**: Alternatif olarak, kütüphaneyi [GroupDocs Search Java sürümleri](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Lisans Edinme
- [GroupDocs web sitesini](https://purchase.groupdocs.com/temporary-license) ziyaret ederek ücretsiz bir deneme veya geçici lisans edinin.  
- Tam erişim ve destek için ticari bir lisans satın almayı düşünün.

### Temel Başlatma
Java uygulamanızda GroupDocs.Search'i başlatın:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index/directory");

        // Add documents to the index
        index.add("path/to/documents");
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## Arama Ağında Belgeleri İndekse Nasıl Eklenir?
Belgelerinizi ağdaki herhangi bir düğüm üzerinden yükleyin; çerçeve indeksleme iş yükünü otomatik olarak dağıtır, yükü dengeler ve paylaşılan indeksi gerçek zamanlı olarak günceller. Her düğüm atanan dosyaları işler, metni çıkarır ve merkezi indekse artımlı değişiklikler yazar, böylece yeni eklenen içerik hemen tüm düğümlerde aranabilir hâle gelir.

### Özellik 1: Arama Ağını Yapılandırma
#### Genel Bakış
Bir arama ağı yapılandırmak, düğümleri arama görevlerini verimli bir şekilde yönetmek ve dağıtmak için ayarlamayı içerir.

##### Adım 1: Temel Yolu ve Bağlantı Noktasını Tanımlama
`SearchNetworkNode` sınıfı, dağıtılmış indekse katılan tek bir düğümü temsil eder.  
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SearchNetworkNodeEvents/";
int basePort = 49140; // Change if necessary due to busy port issues
```

##### Adım 2: Ağı Yapılandırma
`NetworkConfiguration` her düğümün başlangıçta okuduğu ortak ayarları (temel yol, bağlantı noktaları, replikasyon faktörü) tutar.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.scaling.configuring.*;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

### Özellik 2: Arama Ağ Düğümlerini Dağıtma
#### Genel Bakış
Ağınızda arama işlemlerini dağıtmak ve yönetmek için düğümleri dağıtın.

##### Adım 1: Yapılandırma Kullanarak Düğümleri Dağıtma
`SearchNetworkNode` örnekleri aynı yapılandırma dosyasıyla başlatılır, böylece tanımlı temel bağlantı noktası aralığı üzerinden birbirlerini keşfedebilirler.  
```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
```

### Özellik 3: Düğüm Olaylarına Abone Olma
#### Genel Bakış
Düğüm olaylarına abone olmak, arama ağı içindeki çeşitli eylemleri izlemenize ve yanıt vermenize olanak tanır.

##### Adım 1: Abonelik Yöntemini Tanımlama
`NodeEventListener`, indeksleme ilerlemesi, hatalar ve düğüm sağlık değişiklikleri için geri çağrılar almanızı sağlayan bir arayüzdür.  
```java
import com.groupdocs.search.events.*;
import com.groupdocs.search.scaling.events.*;

public static void subscribe(SearchNetworkNode node) {
    // Subscribe to IndexingCompleted event
    node.getEvents().IndexingCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            System.out.println("Indexing completed.");
        }
    });

    // Additional events can be subscribed similarly...
}
```

##### Adım 2: Abonelik Yöntemini Kullanma
Dinleyicinizi her düğümde kaydedin, böylece büyük toplu işlemler sırasında gerçek zamanlı geri bildirim alırsınız.  
```java
SearchNetworkNode masterNode = nodes[0];
subscribe(masterNode);
```

### Düğümleri Kapatma
Bekleyen yazmaları temizlemek ve ağ soketlerini serbest bırakmak için düğümleri her zaman düzgün bir şekilde kapatın.  
```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Pratik Uygulamalar
1. **Kurumsal Arama Çözümleri** – Birden fazla sunucu üzerinde büyük ölçekli belge aramalarını yönetmek için bir arama ağı uygulayın.  
2. **E‑ticaret Platformları** – İndeksleme görevlerini birkaç düğüm arasında dağıtarak ürün arama yeteneklerini artırın.  
3. **İçerik Yönetim Sistemleri (CMS)** – CMS ortamlarında içerik alma ve güncellemelerin performansını iyileştirin.

## Performans Düşünceleri
- Sistem kaynaklarınıza göre düğüm dağıtımını optimize edin.  
- Özellikle büyük veri setleriyle çalışırken bellek sızıntılarını önlemek için bellek kullanımını düzenli olarak izleyin.  
- Daha iyi verimlilik için indeksleme ve arama işlemlerini ince ayarlamak amacıyla yapılandırma ayarlarını kullanın.

## Yaygın Sorunlar ve Çözümler
| Sorun | Tipik Neden | Çözüm |
|-------|-------------|-------|
| Bağlantı noktası çakışmaları | `basePort` zaten kullanımda | `basePort`'u kullanılabilir bir numaraya değiştirin |
| Düğüm erişilemez | Güvenlik duvarı veya ağ kuralları | Gerekli bağlantı noktalarını açın ve bağlantıyı doğrulayın |
| İndeks güncellenmiyor | Yanlış belge yolu | `basePath`'in doğru dizine işaret ettiğini doğrulayın |
| Yüksek bellek kullanımı | Büyük toplu indeksleme | Belgeleri daha küçük partilerde indeksleyin veya yığın (heap) boyutunu artırın |

## Sıkça Sorulan Sorular
**S: Düğümleri dağıtırken bağlantı noktası çakışmalarını nasıl ele alırım?**  
C: Yapılandırma kodunuzdaki `basePort` değişkenini kullanılabilir bir bağlantı noktasına değiştirin.

**S: GroupDocs.Search gerçek zamanlı indeksleme için kullanılabilir mi?**  
C: Evet, uygun yapılandırmalarla gerçek zamanlı indekslemeyi destekler.

**S: Düğüm dağıtımı sırasında bazı yaygın sorunlar nelerdir?**  
C: Ağ bağlantısı ve yanlış yol ayarları sık karşılaşılan sorunlardır. Tüm yolların ve bağlantı noktalarının doğru yapılandırıldığından emin olun.

**S: Ağ çalışırken belgelere indekse eklemek mümkün mü?**  
C: Kesinlikle. Herhangi bir düğümde `index.add(...)` çağrısı yapabilirsiniz; ağ yeni iş yükünü otomatik olarak dağıtacaktır.

**S: Geliştirme testleri için bir lisansa ihtiyacım var mı?**  
C: Test için geçici bir deneme lisansı yeterlidir; üretim kullanımı için ticari bir lisans gereklidir.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs Search Java Dokümantasyonu](https://docs.groupdocs.com/search/java/)  
- **API Referansı**: [GroupDocs API Referansı](https://reference.groupdocs.com/search/java)  
- **İndirme**: [En Son Sürüm](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Deposu](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ücretsiz Destek**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans**: [Geçici Lisans Alın](https://purchase.groupdocs.com/temporary-license)

Bu rehberi izleyerek, GroupDocs.Search for Java kullanarak **belgeleri indekse ekleyebilir** ve sağlam bir **ölçeklenebilir arama ağı oluşturabilir**. Kodlamanın tadını çıkarın!

---

**Son Güncelleme:** 2026-05-22  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler
- [GroupDocs.Search .NET için Arama Ağı Öğreticileri](/search/net/search-network/)
- [GroupDocs.Search ve Redaction Kullanarak .NET Arama Ağı Nasıl Yapılandırılır](/search/net/search-network/configure-net-search-network-groupdocs/)
- [GroupDocs kullanarak .NET'te Etkili Belge İndeksleme ve Geri Getirme için Arama Ağı Düğümü Dağıtma](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)