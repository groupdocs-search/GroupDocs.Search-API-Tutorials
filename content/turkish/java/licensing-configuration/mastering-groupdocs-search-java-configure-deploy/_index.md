---
date: '2026-05-02'
description: GroupDocs.Search for Java kullanarak aramayı nasıl yapılandıracağınızı
  ve gerçek zamanlı arama güncellemelerini nasıl etkinleştireceğinizi öğrenin. Ağ
  kurulumu, düğüm dağıtımı ve indeksleme konusunda adım adım rehber.
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: GroupDocs.Search ile Java’da Aramayı Nasıl Yapılandırılır – Konfigürasyon ve
  Dağıtım Kılavuzu
type: docs
url: /tr/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# GroupDocs.Search ile Java'da Aramayı Nasıl Yapılandırılır

Günümüzün hızlı hareket eden dijital dünyasında, **aramayı nasıl yapılandırılır** verimli bir şekilde yapmak bir projenin başarısını belirleyebilir veya bozabilir. Binlerce sözleşme, araştırma makalesi veya iç raporla uğraşıyor olun, iyi tasarlanmış bir **search network** doğru belgeyi saniyeler içinde bulmanızı sağlar. Bu öğretici, bir arama ağını yapılandırma, düğümleri dağıtma ve GroupDocs.Search for Java ile **gerçek zamanlı arama güncellemeleri** etkinleştirme adımlarını size gösterir.

## Hızlı Yanıtlar
- **Arama ağının temel amacı nedir?** İndeksleme ve sorgu işleme görevlerini birden fazla düğüm arasında dağıtarak ölçeklenebilirlik ve hız sağlar.  
- **Hangi kütüphane sürümü gereklidir?** GroupDocs.Search for Java v25.4 veya daha yenisi.  
- **Bir lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme yeterlidir; üretim için ticari lisans gereklidir.  
- **Gerçek zamanlı güncellemeler nasıl yönetilir?** İndeksleme değişikliklerinde tetiklenen düğüm olaylarına abone olarak.  
- **Yeni belge klasörlerini anında ekleyebilir miyim?** Evet—indexer’ın `addDirectories` metodunu kullanın.

## GroupDocs bağlamında “aramayı nasıl yapılandırılır” nedir?
Aramayı yapılandırmak, belgelerinizin nerede bulunduğunu, düğümlerin nasıl iletişim kurduğunu ve indekslemenin nasıl koordine edildiğini bilen bir **search network** kurmak anlamına gelir. Ağ yapılandırıldıktan sonra, kesinti olmadan düğüm ekleyebilir veya kaldırabilirsiniz; bu da sürekli güncel arama sonuçlarına erişimi sağlar.

## Neden Java için GroupDocs.Search kullanmalı?
- **Scalability:** İş yüklerini birden fazla makine arasında dağıtın.  
- **Real‑time updates:** Yeni indekslenen dosyaları ağda anında yansıtın.  
- **Ease of integration:** Basit Maven kurulumu ve net Java API'leri.  
- **Enterprise‑ready:** Büyük veri kümelerini ve karmaşık sorgu senaryolarını yönetir.

## Önkoşullar
- **Java Development Kit (JDK) 8+** yüklü.  
- **Maven** bağımlılık yönetimi için.  
- Java, Maven ve arama kavramlarına temel aşinalık.

## Java için GroupDocs.Search Kurulumu

### Maven Bağımlılığı
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

**Direct Download:** Kütüphaneyi ayrıca [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden edinebilirsiniz.

### Lisans Alımı
- **Free Trial:** Tüm özellikleri keşfetmek için deneme lisansı alın.  
- **Temporary License:** Uzatılmış değerlendirme süresi için talepte bulunun.  
- **Commercial License:** Üretim dağıtımları için gereklidir.

### Temel Başlatma
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Java'da arama ağını nasıl yapılandırılır

### Adım 1: Gerekli Paketleri İçe Aktarın
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Adım 2: Ağı Yapılandırın
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parameters:** `basePath` belge klasörünüzü gösterir; `basePort` düğüm iletişimi için kullanılan TCP portudur.

## Arama Ağı Düğümlerini Dağıtma

### Adım 1: Dağıtım Paketi İçe Aktarın
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Adım 2: Düğümleri Dağıtın
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master Node:** Tüm düğümler arasında aramaları ve indekslemeyi koordine eder. **master node** ayarlarını, örneğin shard tahsisi ve sağlık kontrolleri gibi, **configure master node** yapabilirsiniz.

## Gerçek Zamanlı Arama Güncellemeleri için Düğüm Olaylarına Abone Olma

### Adım 1: Olay Paketi İçe Aktarın
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Adım 2: Master Node Olaylarına Abone Olun
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Event Handling:** Belgeler eklendiğinde, güncellendiğinde veya kaldırıldığında **real time search updates** sağlar.

## İndeksleme İçin Dizin Ekleme

### Adım 1: Indexer Paketi İçe Aktarın
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Adım 2: Belge Dizinlerini Ekleyin
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dynamic Indexing:** Ağ yeniden başlatılmadan anında **add directories to index** yapmak için `addDirectories` metodunu kullanın.

## İndekslenmiş Belgeleri Alma

### Adım 1: Searcher Paketi İçe Aktarın
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Adım 2: Belge Bilgilerini Alın
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Shard Management:** Belgeleri shard'lar arasında dağıtarak büyük veri setlerini verimli bir şekilde yönetir. **optimize shard size** için shard istatistiklerini izleyin ve gelecekteki sürümlerde `shardSize` yapılandırmasını ayarlayın.

## Bunun projeniz için önemi
Doğru yapılandırılmış bir arama ağı darboğazları ortadan kaldırır, gecikmeyi azaltır ve kullanıcıların her zaman belgenin en son sürümünü görmesini sağlar. Gerçek zamanlı güncellemeler ve **add directories to index** yapabilme yeteneği, kesinti olmadan, özellikle hukuk firmaları, araştırma kurumları ve sürekli değişen belge koleksiyonlarıyla çalışan tüm organizasyonlar için değerlidir.

## Pratik Uygulamalar
1. **Enterprise Document Management:** Milyonlarca dosya üzerinde aramayı merkezileştirir.  
2. **Legal Firms:** Dava dosyalarını, sözleşmeleri ve delilleri hızlıca bulur.  
3. **Academic Research:** Dergileri ve makaleleri anında erişim için indeksler.

## Performans Düşünceleri
- **Optimize Indexing:** Düzenli indeks yenilemeleri planlayın ve eski verileri temizleyin.  
- **Memory Management:** Özellikle büyük shard'larla çalışırken JVM yığınını izleyin.  
- **Scalability Planning:** Veri kümeniz büyüdükçe düğüm ekleyin; ağ otomatik olarak yükü dengeler.  
- **Optimize shard size:** Daha küçük shard'lar sorgu gecikmesini iyileştirirken, daha büyük shard'lar yükü azaltır. Donanımınıza ve sorgu desenlerinize göre ayarlayın.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| Düğümler bağlanamıyor | Port çakışması veya güvenlik duvarı | `basePort`'un açık olduğundan ve başka hizmetler tarafından kullanılmadığından emin olun |
| İndeks güncellenmiyor | Olay aboneliği eksik | Dağıtımdan sonra `SearchNetworkNodeEvents.subscribe(masterNode)` çağırın |
| Bellek yetersizliği hataları | Çok fazla büyük shard yüklendi | Shard boyutunu küçültün veya JVM yığınını artırın (`-Xmx` bayrağı). |

## Sıkça Sorulan Sorular

**S: Ağ çalışırken yeni dizinler ekleyebilir miyim?**  
C: Evet—`indexer.addDirectories()` metodunu kullanın; abone olunan olaylar güncellemeleri gerçek zamanlı olarak yayar.

**S: Düğüm sağlığını nasıl izleyebilirim?**  
C: Her `SearchNetworkNode` durum API'leri sağlar; tercih ettiğiniz izleme aracıyla entegre edin.

**S: Master node'u ayrı bir makinede çalıştırmak mümkün mü?**  
C: Kesinlikle. Tüm düğümlerin aynı `basePort`'u paylaştığından ve ağ üzerinden birbirlerine ulaşabildiğinden emin olun.

**S: Hangi dosya formatları destekleniyor?**  
C: GroupDocs.Search, PDF'ler, Word, Excel, PowerPoint, düz metin ve birçok diğer formatı kutudan çıkar çıkmaz destekler.

**S: Yeni bir düğüm ekledikten sonra ağı yeniden başlatmam gerekir mi?**  
C: Hayır—düğümler dinamik olarak eklenip kaldırılabilir; master node shard'ları otomatik olarak yeniden dengeler.

## Sonuç
Artık GroupDocs.Search for Java kullanarak **aramayı nasıl yapılandırılır** bildiğinize göre, kuruluşunuzun büyümesiyle paralel hızlı, ölçeklenebilir ve güvenilir belge arama çözümleri oluşturabilirsiniz. Bu desenleri uygulayarak herhangi bir sektörde gerçek zamanlı, dağıtık arama deneyimleri yaratın.

---

**Son Güncelleme:** 2026-05-02  
**Test Edilen:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs