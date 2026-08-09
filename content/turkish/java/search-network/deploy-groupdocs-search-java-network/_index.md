---
date: '2026-06-27'
description: GroupDocs.Search for Java kullanarak dağıtık aramayı nasıl yapılandıracağınızı
  ve güçlü bir arama ağı nasıl dağıtacağınızı öğrenin; performans ve ölçeklenebilirliği
  artırın.
keywords:
- configure distributed search
- add documents to index
- GroupDocs.Search Java network
schemas:
- author: GroupDocs
  dateModified: '2026-06-27'
  description: Learn how to configure distributed search and deploy a powerful search
    network using GroupDocs.Search for Java, improving performance and scalability.
  headline: Configure Distributed Search with GroupDocs.Search Java Network
  type: TechArticle
- description: Learn how to configure distributed search and deploy a powerful search
    network using GroupDocs.Search for Java, improving performance and scalability.
  name: Configure Distributed Search with GroupDocs.Search Java Network
  steps:
  - name: '**Large‑Scale Enterprise Systems** – Index millions of contracts, policies,
      and reports while maintaining sub‑second query responses.'
    text: '**Large‑Scale Enterprise Systems** – Index millions of contracts, policies,
      and reports while maintaining sub‑second query responses.'
  - name: '**Content Management Platforms** – Serve thousands of concurrent users
      searching across multimedia assets without bottlenecks.'
    text: '**Content Management Platforms** – Serve thousands of concurrent users
      searching across multimedia assets without bottlenecks.'
  - name: '**E‑commerce Websites** – Accelerate product searches and faceted navigation
      on catalogs containing millions of SKUs.'
    text: '**E‑commerce Websites** – Accelerate product searches and faceted navigation
      on catalogs containing millions of SKUs.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search for Java is a high‑performance library that indexes and
      searches text across more than 50 document formats, providing fast, scalable
      full‑text search for Java applications.
    question: What is GroupDocs.Search for Java?
  - answer: Visit the [GroupDocs's licensing page](https://purchase.groupdocs.com/temporary-license/)
      to request a free trial or purchase a full license for production use.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes, you can **add documents to index** at any time using the `IndexManager.addDocument()`
      method; the changes propagate automatically across the cluster. **IndexManager.addDocument()**
      adds a new document to the index and propagates it across the network.
    question: Can I add new documents after the network is deployed?
  - answer: Typical issues include mismatched base paths, port conflicts, and insufficient
      file‑system permissions. Double‑check each node’s configuration and ensure all
      directories are accessible.
    question: What are common pitfalls when configuring nodes?
  - answer: Absolutely. GroupDocs.Search offers real‑time indexing APIs that immediately
      make newly added documents searchable across all nodes without downtime.
    question: Does the network support real‑time indexing?
  type: FAQPage
title: GroupDocs.Search Java Ağı ile Dağıtık Aramayı Yapılandırın
type: docs
url: /tr/java/search-network/deploy-groupdocs-search-java-network/
weight: 1
---

# GroupDocs.Search Java Ağı ile Dağıtık Aramayı Yapılandırma

Günümüzün veri odaklı dünyasında, **dağıtık aramayı yapılandırma** büyük belge koleksiyonlarını yönetmek ve yanıt sürelerini düşük tutmak için gereklidir. Bu öğretici, sağlam bir GroupDocs.Search for Java ağı kurmanızı adım adım gösterir, **birden fazla düğümde aramayı dağıtmayı**, **belgeleri indekse eklemeyi** ve **güvenilir iletişim için TCP ayarlarını yapılandırmayı** anlatır. Sonunda, üretime hazır ölçeklenebilir bir arama çözümüne sahip olacak ve bu mimarinin tek düğümlü kurulumdan neden daha iyi performans gösterdiğini net bir şekilde anlayacaksınız.

## Hızlı Yanıtlar
- **Dağıtık aramayı yapılandırma nedir?** Bu, birden fazla bağımsız arama düğümünü birbirine bağlayarak topluca indeksleme ve sorgulara yanıt verme sürecidir; daha yüksek verim ve hata toleransı sağlar.  
- **Kaç düğüm önerilir?** Genellikle 3‑5 düğüm, çoğu kurumsal iş yükü için performans ve hata toleransı arasında iyi bir denge sağlar.  
- **Lisans gerekiyor mu?** Evet – GroupDocs.Search'in üretim kullanımında geçici veya tam lisans gereklidir.  
- **Hangi portları kullanmalıyım?** Sunucularınızda boş olan portları seçin; örnek 49136‑49139 aralığını kullanıyor, ancak herhangi bir açık aralık çalışır.  
- **Dağıtım sonrası yeni belgeler ekleyebilir miyim?** Kesinlikle – **belgeleri indekse ekleyebilirsiniz** ağ yeniden başlatılmadan istediğiniz zaman.

## Dağıtık aramayı yapılandırma nedir?
Dağıtık bir arama mimarisini yapılandırmak, birden fazla bağımsız arama düğümünü birbirine bağlayarak indeksleme işini paylaşmalarını ve sorgulara topluca yanıt vermelerini sağlar. Bu, tek bir makinenin yükünü azaltır, hem verimi hem de güvenilirliği artırır ve hata toleransı için yerleşik yedeklilik sağlar.

## Neden GroupDocs.Search for Java kullanmalı?
GroupDocs.Search for Java, **yüksek performanslı indeksleme** (modern donanımlarda 1 GB/s'ye kadar) ve **ölçeklenebilir mimari** sunar; 10+ düğümden oluşan kümeleri destekler. Yerel olarak **50+ belge formatını** anlar—PDF, DOCX, XLSX, PPTX ve e‑posta dosyaları dahil—bu sayede ek dönüştürücülere ihtiyaç duymadan neredeyse tüm iş içeriklerini indeksleyebilirsiniz. Dahili `TcpSettings` sınıfı, gecikme, verim ve keep‑alive aralıklarını ince ayar yapmanıza olanak tanır; veri merkezi sınırları arasında bile düğümler arası güvenilir iletişimi sağlar. **TcpSettings**, düğümler arasındaki düşük seviyeli TCP iletişim parametrelerini yapılandırır.

## Önkoşullar

### Gerekli Kütüphaneler ve Bağımlılıklar
**GroupDocs.Search for Java** sürüm 25.4 veya üzeri gerekir. Geliştirme ortamınızda Java yüklü olduğundan emin olun.

### Ortam Kurulum Gereksinimleri
- Java Development Kit (JDK) 11 veya daha yeni bir sürüm.  
- IntelliJ IDEA veya Eclipse gibi bir IDE, proje yönetimini kolaylaştırır.

### Bilgi Önkoşulları
Temel Java programlama becerileri ve ağ yapılandırması hakkında genel bir anlayış, adımları sorunsuz takip etmenize yardımcı olacaktır.

## GroupDocs.Search for Java'ı Kurma
Başlamak için, projenize GroupDocs.Search for Java ekleyin. Bunu Maven aracılığıyla ya da kütüphaneyi doğrudan indirerek yapabilirsiniz.

**Maven Kurulumu**  
`pom.xml` dosyanıza aşağıdaki depo ve bağımlılık yapılandırmasını ekleyin:

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

**Doğrudan İndirme**  
Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Lisans Edinme
GroupDocs.Search'i tam olarak kullanmak için geçici bir lisans alabilir veya satın alabilirsiniz. Ücretsiz deneme veya tam lisans edinme hakkında daha fazla bilgi için [GroupDocs'in lisans sayfasını](https://purchase.groupdocs.com/temporary-license/) ziyaret edin. Aynı amaçla [GroupDocs lisans sayfasını](https://purchase.groupdocs.com/temporary-license/) da kullanabilirsiniz.

### Temel Başlatma ve Kurulum
Java uygulamanızda GroupDocs.Search'i başlatalım:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        // Add documents to the index
        index.add("YOUR_DOCUMENT_DIRECTORY");
    }
}
```

## Uygulama Kılavuzu
Bu bölümde, GroupDocs.Search for Java kullanarak bir arama ağı yapılandırma ve dağıtma sürecini adım adım göstereceğiz.

### GroupDocs.Search ile dağıtık aramayı nasıl yapılandırılır?
Ağ yapılandırmasını yükleyin, temel yolları tanımlayın ve sadece birkaç kod satırıyla TCP parametrelerini ayarlayın. Bu doğrudan‑cevap modeli, ayrıntılı açıklamalara geçmeden önce temel adımları gösterir.

İlk olarak, bir `SearchNetworkConfig` nesnesi oluşturun, ortak bir temel dizin belirleyin ve her düğüm için ayrı bir TCP portu atayın. **SearchNetworkConfig**, dağıtık arama kümesi için temel dizin ve düğüm portları gibi ayarları tanımlar. Ardından, soket zaman aşımı, tampon boyutu ve keep‑alive davranışını kontrol eden `TcpSettings` sınıfını örnekleyin. Son olarak, kümeyi başlatmak için `NetworkManager.deploy(config)` metodunu çağırın. **NetworkManager**, küme içindeki arama düğümlerinin dağıtımını ve yönetimini gerçekleştirir.

#### Ağın Yapılandırılması
`TcpSettings` sınıfı, düğümler arasındaki tüm TCP‑seviyesi iletişimin yapılandırma merkezi görevi görür. Bağlantı zaman aşımını, okuma/yazma tampon boyutlarını ve Nagle algoritmasının kullanılmasını ayarlamanıza olanak tanır.

```java
Configuration configuration = ConfiguringSearchNetwork.configure("YOUR_DOCUMENT_DIRECTORY", 49136);
```

#### Düğümleri Dağıtma
Her düğümü, benzersiz kimliğini ve önceden tanımlanmış yapılandırmasını sağlayarak dağıtın. Dağıtım rutini, düğümü otomatik olarak kümeye kaydeder, dinleme soketini açar ve arka plan indeksleme iş parçacıklarını başlatır.

```java
public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
    // Define timeouts for sending and receiving data over the network.
    int sendTimeout = 3000;
    int receiveTimeout = 3000;

    // Create and start three nodes that can run on separate servers or together.
    SearchNetworkNode node1 = new SearchNetworkNode(
        1,
        basePath + "Node1",
        new TcpSettings(basePort + 1, sendTimeout, receiveTimeout)
    );
    node1.start();

    SearchNetworkNode node2 = new SearchNetworkNode(
        2,
        basePath + "Node2",
        new TcpSettings(basePort + 2, sendTimeout, receiveTimeout)
    );
    node2.start();

    SearchNetworkNode node3 = new SearchNetworkNode(
        3,
        basePath + "Node3",
        new TcpSettings(basePort + 3, sendTimeout, receiveTimeout)
    );
    node3.start();

    // Create and configure the main configuration node.
    SearchNetworkNode node0 = new SearchNetworkNode(
        0,
        basePath + "Node0",
        new TcpSettings(basePort, sendTimeout, receiveTimeout),
        new ConsoleLogger(),
        configuration
    );

    // Add an event handler to notify when the configuration is complete.
    node0.getEvents().ConfigurationCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            // Event handling logic here (e.g., logging)
        }
    });

    // Configure all nodes in the network using the main configuration node.
    node0.configureAllNodes();

    // Start the search network by launching all configured nodes.
    node0.start();

    // Return an array of all deployed nodes.
    return new SearchNetworkNode[] {node0, node1, node2, node3};
}
```

## Yaygın Sorunlar ve Çözümler
- **Dizin Erişim Hataları** – Her düğümün temel dizininin mevcut olduğundan ve Java işleminin okuma/yazma izinlerine sahip olduğundan emin olun.  
- **Port Çakışmaları** – Seçilen portların (ör. 49136‑49139) başka hizmetler tarafından kullanılmadığını doğrulayın; kontrol etmek için `netstat -an` komutunu çalıştırabilirsiniz.  
- **Yavaş Ağlarda Zaman Aşımı** – Yüksek gecikmeli ortamlarda sık sık bağlantı kesintileri yaşıyorsanız `TcpSettings.setConnectionTimeout()` değerini artırın.  
- **İndeks Bozulması** – İndeks klasörünü düzenli olarak yedekleyin ve bozulmuş parçaları otomatik olarak yeniden oluşturmak için `NetworkManager.enableAutoRecovery()`'ı etkinleştirin.

## Pratik Uygulamalar
Dağıtık bir arama ağı dağıtmak çeşitli senaryolarda faydalı olabilir:

1. **Büyük Ölçekli Kurumsal Sistemler** – Milyonlarca sözleşme, politika ve raporu indeksleyerek yarım saniyeden kısa sorgu yanıtları sağlar.  
2. **İçerik Yönetim Platformları** – Multimedya varlıkları üzerinde arama yapan binlerce eşzamanlı kullanıcıya darboğaz olmadan hizmet verir.  
3. **E‑ticaret Web Siteleri** – Milyonlarca SKU içeren kataloglarda ürün aramalarını ve katmanlı gezinmeyi hızlandırır.

## Performans Düşünceleri
**dağıtık aramayı yapılandırma** ortamınızın verimli çalışmasını sağlamak için:

- **İndeks Boyutu Yönetimi** – GroupDocs.Search, 100 GB'yi aşan indeksleri yönetebilir; ancak disk I/O'yu izleyin ve büyük koleksiyonları birden fazla düğümde parçalamayı düşünün.  
- **Kaynak Ayarı** – İş yükünüze göre Java bellek ayarlarını (`-Xmx8g -Xms4g`) uygulayın ve yüksek verimli ağlar için `TcpSettings.setReadBufferSize()`'ı ayarlayın.  
- **Sağlık İzleme** – Yerleşik `NetworkHealthMonitor`'ı kullanarak her düğümde CPU, bellek ve ağ gecikmesini izleyin ve tanımladığınız eşikler için uyarılar ayarlayın.

## Sonuç
Bu öğreticiyi izleyerek **dağıtık aramayı yapılandırma** ve ölçeklenebilir bir GroupDocs.Search Java ağı dağıtma konusunda bilgi edindiniz. Bu çözüm, özellikle büyük ve heterojen belge koleksiyonlarıyla çalışırken uygulamanızın arama özelliklerinin hızını ve güvenilirliğini büyük ölçüde artırabilir.

### Sonraki Adımlar
Özel analizörler, eşanlamlı kelime yönetimi ve gerçek‑zamanlı indeksleme gibi gelişmiş yetenekleri keşfederek arama deneyiminizi daha da iyileştirin. Ayrıca ağı bir RESTful API katmanı ile bütünleştirerek arama işlevselliğini dış istemcilere açabilirsiniz.

### Eylem Çağrısı
Bu sağlam çözümü bugün projelerinizde uygulamaya başlayın ve performans artışını ilk elden gözlemleyin!

## Sıkça Sorulan Sorular

**S: GroupDocs.Search for Java nedir?**  
C: GroupDocs.Search for Java, 50'den fazla belge formatı üzerinde metin indeksleyip arama yapabilen yüksek performanslı bir kütüphanedir; Java uygulamaları için hızlı, ölçeklenebilir tam metin arama sağlar.

**S: GroupDocs.Search için geçici lisans nasıl alınır?**  
C: Ücretsiz deneme veya üretim kullanımı için tam lisans talep etmek üzere [GroupDocs'in lisans sayfasını](https://purchase.groupdocs.com/temporary-license/) ziyaret edin.

**S: Ağ dağıtıldıktan sonra yeni belgeler ekleyebilir miyim?**  
C: Evet, `IndexManager.addDocument()` metodunu kullanarak **belgeleri indekse ekleyebilirsiniz**; değişiklikler otomatik olarak küme içinde yayılır. **IndexManager.addDocument()** yeni bir belgeyi indekse ekler ve ağ üzerinden dağıtır.

**S: Düğümleri yapılandırırken yaygın tuzaklar nelerdir?**  
C: Tipik sorunlar arasında uyumsuz temel yollar, port çakışmaları ve yetersiz dosya sistemi izinleri bulunur. Her düğümün yapılandırmasını iki kez kontrol edin ve tüm dizinlerin erişilebilir olduğundan emin olun.

**S: Ağ gerçek‑zamanlı indekslemeyi destekliyor mu?**  
C: Kesinlikle. GroupDocs.Search, yeni eklenen belgelerin tüm düğümlerde kesintisiz olarak aranabilir olmasını sağlayan gerçek‑zamanlı indeksleme API'leri sunar.

**Son Güncelleme:** 2026-06-27  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## İlgili Öğreticiler

- [GroupDocs.Search for Java Öğreticileri ve Örnekleri](/search/net/)
- [.NET'te GroupDocs kullanarak Verimli Belge İndeksleme ve Geri Getirme için Bir Arama Ağı Düğümü Dağıtma](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [GroupDocs.Search .NET için Arama Performans Optimizasyonu Öğreticileri](/search/net/performance-optimization/)