---
date: '2026-01-24'
description: GroupDocs.Search Java kullanarak ölçeklenebilir arama ağları için temel
  port grupdosyasını nasıl yapılandıracağınızı, alma hızını nasıl optimize edeceğinizi
  ve çok düğümlü sistemleri nasıl kuracağınızı öğrenin.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Java Search Network'te temel port groupdocs'i yapılandır
type: docs
url: /tr/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Java Arama Ağı'nda temel port groupdocs yapılandırması

Modern, veri‑ağır uygulamalarda **temel port groupdocs yapılandırması**, hızlı ve güvenilir bir arama altyapısı oluşturmanın temel adımını oluşturur. Binlerce PDF ile çalışıyor olun ya da birden çok sunucuya ölçeklendiriyor olun, doğru port ve yol ayarları her düğümün diğerleriyle çatışma olmadan iletişim kurmasını sağlar. Bu öğretici, ön koşullardan tam çok‑düğüm yapılandırmasına kadar her detayı adım adım anlatır—böylece GroupDocs.Search for Java ile ölçeklenebilir bir arama ağına güvenle başlayabilirsinizümü destekiuplarınızda portların açık olduğundan emin olun.
- **Kaç düğüm ekleyebilirim?** Katı bir limit yok; donanım ve ağınız izin verdiği sürece istediğiniz kadar ekleyebilirsiniz.

## “temel port groupdocs yapılandırması” nedir?
**Temel port groupdocs yapılandırması** yaptığınızda, her düğümün kullanacağı bir başlangıç TCP portu (ve sonraki düğümler için artan bir değer) atarsınız. Bu basit kullanım## Neden herhangi bir Java uygulamasıyla, yerel ya da bulut ortamında çalışır.
- **Güçlü lisanslama** – deneme seçenekleri, tam geçiş yapmadan önce test etmenizi sağlar.

## Ön Koşullar
- **Java Development Kit (JDK)** 8 veya daha yeni bir sürüm.
- **IDE** – IntelliJ IDEA veya Eclipse gibi.
- **GroupDocs.Search for Java** kütüphanesi (sürüm 25.4 veya üzeri), Maven ile ya da manuel indirme yoluyla kurulmuş.
- Temel ağ bilgisi (TCP portları, localhost vs. uzak hostlar).

## GroupDocs.Search for Java Kurulumu

### Kurulum Talimatları

**Maven Ayarı:**

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

**Doğrudan İndirme:**

Alternatif olarak, en son sürümü [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Lisans Alımı

- **Ücretsiz Deneme** – hemen test etmeye başlayın.
- **Geçici Lisans** – [Geçici Lisans](https://purchase.groupdocs.com/temporary-license) adresinden uzatılmış bir deneme alın.
- **Tam Satın Alma** – üretim dağıtımları için gereklidir.

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

### temel port groupdocs nasıl yapılandırılır

#### Temel Yolların Ayarlanması

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Neden**: Tutarlı bir dizin yapısı, her düğümün indeks, shard veya çıkarıcı dosyalarını belirsizlik olmadan bulmasını sağlar.

#### Temel Portun Yapılandırılması

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Neden**: Yüksek bir port numarası (ör. 49100) başlatmak, yaygın hizmetlerle çakışma olasılığını azaltır. Her ek düğüm için portu artırın.

#### Host Adresinin Tanımlanması

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Neden**: `localhost` geliştirme için idealdir; üretimde sunucunuzun IP’si ya da DNS adı ile değiştirin.

#### Ağ Yapılandırmasının Oluşturulması

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

- **Neden**: Bu seçenekler hız ve depolama verimliliği arasında denge kurar, size hafif ama güçlü bir arama indeksi sunar.

#### Düğümlerin Eklenmesi

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

- **Neden**: Görevlerin düğümler arasında bölünmesi (indeksleme vsılması

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Yaygın Sorunlar & Çözümler

- **Port Çakışmaları** – Her yeni düğüm için `basePort` değerini mutlaka artırın. `netstat` ya da işletim sisteminizin port izleyicisiyle doğrulayın.
- **Eksik Dizinler** – Referans verilen her klasörün (`Indexer0`, `Searcher0` vb.) mevcut olduğundan ve Java sürecinin okuma/yazma izinlerine sahip olduğundan Platformlarıirme- **CPU/Memory İzleme** – Java’nın JMX’i veya bir profil aracıyla iş parçacığı kullanımını izleyin.
- **Sıkıştırmayı Ayarlama** – `Compression.High` disk alanını tasarruf ettirir ancak CPU yükü ekleyebilir; `High` ve `Normal` ikisini de test edin.
- **Düzenli Güncellemeler** – Yeni GroupDocs.Search sürümleri genellikle performans yamaları içerir.

## Sonuç

Artık **temel port groupdocs yapılandırması** yapmayı ve GroupDocs.Search for Java ile çok‑düğümlü bir arama ağı kurmayı öğrendiniz. Ek düğümler ekleyerek, indeks ayarlarını ince ayar yaparak ve ağı mevcut uygulamalarınıza entegre ederek gerçekten ölçeklenebilir bir arama çözümü elde edebilirsiniz.

## Sıkça Sorulan Sorular

**S: İndekslemede stop word’lerin devre dışı bırakılmasının amacı nedir?**  
C: Stop word’leri devre dışı bırakmak, özel alanlarda kritik olabilecek yaygın terimleri tutarak arama doğruluğunu artırabilir.

**S: Birden fazla düğüm eklerken port çakışmalarını nasıl yönetirim?**  
C: Yüksek bir `basePort` (ör. 49100) ile başlayın ve her sonraki düğüm için artırın; böylece her düğümün benzersiz bir TCP uç noktası olur.

**S: Bu yapılandırmayı bulut‑tabanlı uygulamalar için kullanabilir miyim?**  
C: Evet—seçtiğiniz portların bulut güvenlik gruplarınızda açık olduğundan emin olun ve `127.0.0.1` yerine uygun genel ya da özel IP’yi kullanın.

**S: NormalIndex ile diğer indeks tipleri arasındaki fark nedir?**  
C: `NormalIndex`, hız ve bellek kullanımı arasında dengeli bir tercih sunarken, özel indeksler (ör. `FastIndex`) belirli performans senaryolarına yöneliktir.

**S: Ekleyebileceğim düğüm sayısında bir limit var mı?**  
C: Teknik olarak hayır; limit donanım kaynaklarınız ve ağ bant genişliğiniz tarafından belirlenir.

---

**Son Güncelleme:** 2026-01-24  
**Test Edilen Versiyon:** GroupDocs.Search Java 25.4  
**Y