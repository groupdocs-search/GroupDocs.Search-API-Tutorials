---
date: '2026-05-17'
description: Ölçeklenebilir bir GroupDocs.Search Java ağı için temel port groupdocs'i
  yapılandırmayı, alma hızını optimize etmeyi ve çok düğümlü sistemler kurmayı öğrenin.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: Java Search Network'te temel port GroupDocs.Search'i yapılandırma
type: docs
url: /tr/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Java Arama Ağı'nda temel port groupdocs yapılandırması

Modern, veri‑ağır uygulamalarda **configure base port groupdocs** hızlı ve güvenilir bir arama altyapısı oluşturmanın ilk adımıdır. Binlerce PDF'yi indeksliyor ya da birkaç sunucuya yayılıyorsanız, benzersiz portlar ve dizinler atamak düğüm‑düğüm çakışmalarını önler ve kümenin sağlıklı kalmasını sağlar. Bu öğretici, önkoşulları, kurulumu ve GroupDocs.Search for Java kullanarak tam bir çok‑düğümlü yapılandırmayı adım adım gösterir, böylece bugün gerçekten ölçeklenebilir bir arama ağı başlatabilirsiniz.

## Hızlı Yanıtlar
- **Birincil amaç nedir?** Her arama düğümü için benzersiz portlar ve temel dizinler atayarak çakışmaları ortadan kaldırmak.  
- **Bir lisansa ihtiyacım var mı?** Evet – üretim dağıtımları için bir deneme veya tam lisans gereklidir.  
- **Hangi Java sürümü destekleniyor?** Java 8 veya üstü (Java 11+ önerilir).  
- **Bunu bulut sunucularında çalıştırabilir miyim?** Kesinlikle – sadece seçtiğiniz portları bulut güvenlik gruplarınızda açın.  
- **Kaç düğüm ekleyebilirim?** Sabit bir limit yok; sadece donanım ve ağ kapasitesiyle sınırlısınız.

## “configure base port groupdocs” nedir?

**Configure base port groupdocs**, her arama düğümünün kullanacağı başlangıç TCP portunu atama ve sonraki düğümler için bu portu artırma sürecidir. Bu basit adım, korkutucu “port already in use” hatalarını ortadan kaldırır ve temiz, yatay‑ölçeklenebilir bir arama kümesi için temel oluşturur, her düğümün ayrı bir uç nokta üzerinden iletişim kurmasını sağlar.

## Ölçeklenebilir bir ağ için GroupDocs.Search'i neden kullanmalısınız?

GroupDocs.Search **high‑performance indexing** (standart 8‑çekirdek sunucuda 50 GB/dk'ye kadar) sunar ve PDF, DOCX, PPTX ve HTML dahil **50+ file formats** destekler. Modüler mimarisi, indeksleyicileri, arayıcıları, shard'ları ve extractor'ları düğümler arasında karıştırmanıza izin verir, donanım ekledikçe doğrusal ölçeklenebilirlik sağlar. Kütüphane ayrıca, tipik iş yükleri için sorgu gecikmesini 200 ms altında tutarken disk kullanımını %70’e kadar azaltan yerleşik sıkıştırma seçenekleri sunar.

## Önkoşullar
- **Java Development Kit (JDK)** 8 veya daha yeni (Java 11+ daha iyi çöp toplama için önerilir).  
- **IDE** (IntelliJ IDEA veya Eclipse gibi).  
- **GroupDocs.Search for Java** kütüphanesi (sürüm 25.4 veya üzeri) Maven ile ya da manuel indirme yoluyla kurulu.  
- Temel ağ bilgisi (TCP portları, localhost vs. uzak hostlar).  
- Geçerli bir **GroupDocs.Search** lisansı (deneme veya tam).

## GroupDocs.Search for Java'ı Kurma

### Kurulum Talimatları

**Maven Setup:**

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

**Direct Download:**

Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Lisans Edinme

- **Free Trial** – hemen test etmeye başlayın.  
- **Temporary License** – [Temporary License](https://purchase.groupdocs.com/temporary-license) adresinden uzatılmış bir deneme alın.  
- **Full Purchase** – üretim dağıtımları için gereklidir.

### Temel Başlatma ve Kurulum

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Uygulama Kılavuzu

### Temel port groupdocs nasıl yapılandırılır?

Temel portu yapılandırmak için ağ yapılandırma dosyasını düzenleyin veya programatik olarak `basePort` özelliğini 49100 gibi yüksek, kullanılmamış bir değere ayarlayın. Her sonraki düğüm için port numarasını bir artırın (veya sabit bir offset ekleyin) böylece her düğüm kendi ayrı TCP uç noktasına bağlanır, port‑çakışma hatalarını ortadan kaldırır ve güvenlik duvarı kurallarını basitleştirir.

#### Temel Yolları Ayarlama

Kod yazmadan önce tutarlı bir klasör düzeni belirleyin. Örneğin, indeksleyiciler (`Indexer0`), arayıcılar (`Searcher0`) ve extractor'lar (`Extractor0`) için ayrı dizinler oluşturun. Bu yapı, her düğümün dosyalarını hızlıca çözümlemesini sağlar.

- **Neden**: Öngörülebilir bir dizin hiyerarşisi, düğümler farklı makinelerde başlatıldığında “file not found” hatalarını önler.

#### Temel Portu Yapılandırma

Ortak hizmetlerle (HTTP 80, SSH 22 vb.) çakışmayı önlemek için yüksek bir başlangıç portu seçin. Eklediğiniz her yeni düğüm için port numarasını artırın.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Neden**: Yüksek bir portta (ör. 49100) başlamak, mevcut hizmetlerle çakışma olasılığını azaltır ve güvenlik duvarı kuralı oluşturmayı basitleştirir.

#### Ana Bilgisayar Adresini Tanımlama

Geliştirme sırasında `localhost` sorunsuz çalışır. Üretimde, uzak düğümlerin birbirine ulaşabilmesi için sunucunun IP adresi veya DNS adıyla değiştirin.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Neden**: Gerçek bir host adresi kullanmak, bulut ya da yerel veri merkezi kümeleri için kritik olan makine‑arası iletişimi etkinleştirir.

#### Ağ Yapılandırması Oluşturma

`NetworkConfig` sınıfı, temel port, host ve isteğe bağlı SSL ayarları gibi tüm ağ seçeneklerini tek bir nesnede birleştirir; bu nesne arama motoru tarafından tüketilir.

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Neden**: Bu seçeneklerin merkezileştirilmesi, yapılandırmanın yeniden kullanılabilir olmasını ve birçok düğümde bakımını kolaylaştırır.

#### Düğümler Ekleme

`SearchNode`, indeksleme veya arama gibi belirli bir işlevi yerine getiren GroupDocs.Search kümesindeki bireysel bir düğümü temsil eder. Her rol (indexer, searcher, extractor) için bir `SearchNode` örneği oluşturun ve `SearchEngine` ile kaydedin. Sorumlulukları düğümler arasında dağıtmak paralelliği ve hata toleransını artırır.

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Neden**: Çalışmayı özel düğümlere bölmek, rekabeti azaltır ve her makinenin tek bir göreve odaklanmasını sağlayarak toplam verimliliği artırır.

#### Yapılandırmayı Tamamlama

Tüm düğümleri ekledikten sonra `engine.start()` çağrısıyla ağı başlatın. Motor, her düğümü otomatik olarak atanmış portuna bağlar ve bağlantıyı doğrular.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Yaygın Sorunlar ve Çözümler

- **Port Çakışmaları** – Her yeni düğüm için `basePort` değerini her zaman artırın. Açık portları `netstat` veya işletim sisteminizin ağ izleyicisiyle doğrulayın.  
- **Eksik Dizinler** – Her klasörün (`Indexer0`, `Searcher0`, vb.) mevcut olduğundan ve Java sürecinin okuma/yazma izinlerine sahip olduğundan emin olun.  
- **Ağ Erişilebilirliği** – Çok makineli bir ortama geçerken `127.0.0.1` adresini gerçek host IP'siyle değiştirin ve seçilen portları güvenlik duvarlarında açın.  

## Pratik Uygulamalar

| Senaryo | Temel port groupdocs yapılandırmanın faydası |
|----------|--------------------------------------------|
| Kurumsal Belge Yönetimi | Bölümler arasında kesintisiz ölçeklendirme |
| Büyük CMS Platformları | İndeks dağıtıldığı için içerik alma daha hızlı |
| Hukuki Dava Yönetimi | PDF'lerin paralel çıkarılması arama gecikmesini azaltır |

## Performans Düşünceleri

- **CPU/Belleği İzleme** – Thread kullanımını izlemek için Java’nın JMX’ini veya bir profil oluşturma aracını kullanın.  
- **Sıkıştırmayı Ayarlama** – `Compression.High` disk alanını tasarruf eder ancak CPU yükü ekleyebilir; ideal dengeyi bulmak için `High` ve `Normal` ikisini de test edin.  
- **Düzenli Güncellemeler** – Yeni GroupDocs.Search sürümleri genellikle performans yamaları içerir; kütüphaneyi güncel tutun.

## Sonuç

Artık **configure base port groupdocs** nasıl yapılacağını ve GroupDocs.Search for Java kullanarak çok‑düğümlü bir arama ağı nasıl kurulacağını öğrendiniz. Ek düğümlerle deney yapın, indeks ayarlarını ince ayarlayın ve ağı mevcut uygulamalarınıza entegre ederek gerçekten ölçeklenebilir bir arama çözümü elde edin.

## Sık Sorulan Sorular

**Q: Dizinlemede durdurma kelimelerinin devre dışı bırakılmasının amacı nedir?**  
A: Durdurma kelimelerinin devre dışı bırakılması, özel alanlarda kritik olabilecek yaygın terimleri koruyarak arama doğruluğunu artırabilir.

**Q: Birden fazla düğüm eklerken port çakışmalarını nasıl yönetirim?**  
A: Yüksek bir `basePort` (ör. 49100) ile başlayın ve her sonraki düğüm için artırın, böylece her düğümün benzersiz bir TCP uç noktası olur.

**Q: Bu kurulumu bulut‑tabanlı uygulamalar için kullanabilir miyim?**  
A: Evet—seçtiğiniz portların bulut güvenlik gruplarınızda açık olduğundan emin olun ve `127.0.0.1` adresini uygun genel veya özel IP ile değiştirin.

**Q: NormalIndex ile diğer indeks türleri arasındaki fark nedir?**  
A: `NormalIndex`, hız ve bellek kullanımı arasında dengeli bir ödün sunarken, özel indeksler (ör. `FastIndex`) belirli performans senaryolarına yöneliktir.

**Q: Ekleyebileceğim düğüm sayısına bir limit var mı?**  
A: Teknik olarak hayır; limit, donanım kaynaklarınız ve ağ bant genişliğiniz tarafından belirlenir.

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## İlgili Eğitimler

- [GroupDocs.Search ve Redaction Kullanarak .NET Arama Ağı Nasıl Yapılandırılır](/search/net/search-network/configure-net-search-network-groupdocs/)
- [.NET için Belge Yönetim Sistemlerinde GroupDocs.Search ile Arama Ağı Nasıl Uygulanır](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [.NET'te Verimli Belge Dizinleme ve Geri Getirme İçin GroupDocs Kullanarak Arama Ağı Düğümü Nasıl Dağıtılır](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)