---
date: '2026-01-08'
description: GroupDocs.Search for Java kullanarak aramayı nasıl yapılandıracağınızı
  ve gerçek zamanlı arama güncellemelerini nasıl etkinleştireceğinizi öğrenin. Ağ
  kurulumu, düğüm dağıtımı ve indeksleme hakkında adım adım kılavuz.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'Java''da GroupDocs.Search ile Aramayı Nasıl Yapılandırılır - Konfigürasyon
  ve Dağıtım Kılavuzu'
type: docs
url: /tr/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# GroupDocs.Search ile Java'da Arama Nasıl Yapılır?

Bugünün hızlı tempolu dijital dünyasında, **aramayı nasıl yapılandırılır** başarılı bir şekilde yanıtlanması bir seçeneği seçmeyir ya da başarısızlığa sürüklenebilir. Kişisel sözleşme, araştırma makalesi ya da iç raporla hazırlanır olun, iyi hazırlanmış bir arama ağı doğru belgeyi saniyeler içinde bulmanızı sağlar. Bu öğretici, bir arama ağı işlemleriniyı, düğümleri dağıtmayı ve GroupDocs.Search for Java ile **gerçek zamanlı arama güncellemelerini** etkinleştirmeyi adım adım gösterir.

## Hızlı Yanıtlar
- **Bir arama ağının temel amacı nedir?**İndeksleme ve sorgu işlemeli ölçeklenebilirlik ve hız için birden fazla düğüm arasında dağıtmak.
- **Hangi üye sürümü gereklidir?**GroupDocs.SearchforJavav25.4veya daha yeni.
- **Lisans gerekiyor mu?**Değerlendirme için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.
- **Gerçek zamanlı güncellemeler nasıl ele alınır?**İndeksleme çalıştırmade tetiklenen düğüm hatalarıa abone olarak.
- **Yeni belge klasörlerini anında tamamlayabilir miyim?**Evet—indexer'ın `addDirectories` yöntemini kullanın.

## GroupDocs uzantıları “aramayı nasıl yapılandırılır” ne anlama gelir?
Aramayı karşılaştırın, belgelerinizin nerede olduğunu, düğümlerin nasıl iletişim kurduğunu ve indekslemenin nasıl koordine edildiğini bilen bir **arama ağı** kalibrasyonu demektir. Ağ yapılandırıldıktan sonra, kesilmeden düğümleri birleştirin, sürekli güncel arama yaparak erişim sağlayabilirsiniz.

## Neden GroupDocs.Search for Java kullanılmıyor?
- **Ölçekilebilirlik:** İş yüklerini birden fazla makine arasında dağıtın.
- **Gerçek zamanlı güncellemeler:** Yeni indekslenen dosyalar ağda anında yansıtın.
- **Entegrasyon kolaylığı:** Basit Maven kurulumu ve net Java API'leri.
- **Kurumsal hazır:** Büyük veri kümelerini ve karmaşık sorgu senaryolarını yönetir.

## Önkoşullar
- **Java Development Kit (JDK)8+** Yüklü.
- **Maven** ilişkileri yönetimi için.
- Java, Maven ve arama kavramlarına ilişkin temel bilgi sahibi olma.

## GroupDocs.Java Kurulumunu Arayın

### Maven Bağımlılığı
Depoyu ve bağımlılığı `pom.xml`nize ekleyin:

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

**Doğrudan İndirme:** Kütüphaneyi ayrıca [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/) adresinden edinebilirsiniz.

### Lisans Edinme
- **Ücretsiz Deneme:** Tüm özellikleri ayırmak için deneme lisansı alın.
- **Geçici Lisans:** Uzatılmış değerlendirme koşulları için talep edin.
- **Ticari Lisans:** Üretim kaynakları için gereklidir.

### Temel Başlatma
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Java'da arama ağı nasıl yapılandırılır

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
- **Parametreler:** `basePath` belge klasörünüzün yolunu gösterir; `basePort` düğüm iletişimi için kullanılan TCP portudur.

## Arama Ağı Düğümlerinin Dağıtılması

### 1. Adım: Dağıtım Paketini İçe Aktarın

```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Adım 2: Düğümleri Dağıtın
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master Düğüm:** Tüm düğümlerde aramaları ve indekslemeyi koordine eder.

## Gerçek Zamanlı Arama Güncellemeleri için Düğüm Olaylarına Abone Olma

### Adım 1: Etkinlik Paketini İçe Aktarın
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Adım 2: Ana Düğüm Etkinliklerine abone olun
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Olay İşleme:** Belgeler eklendiğinde, güncellendiğinde veya kaldırıldığında **gerçek zamanlı arama güncellemelerini** etkinleştirir.

## İndeksleme için Dizinler Eklemek

### Adım 1: Dizin Oluşturucu Paketini İçe Aktarın
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Adım 2: Belge Dizinlerini Ekleyin
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dinamik İndeksleme:** Gerektiği kadar klasör ekleyin; ağ bunları otomatik olarak indeksleyecek.

## İndekslenmiş Belgeleri Getirme

### Adım 1: Arama Paketini İçe Aktarın
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
- **Shard Yönetimi:** Belgeleri Shard'lar arasında dağıtarak büyük veri setlerini verimli bir şekilde yönetir.

## Pratik Uygulamalar
1. **Kurumsal Belge Yönetimi:** Milyonlarca dosya üzerinde aramayı merkezileştirir.
2. **Hukuk Firmaları:** Davacıların, sözleşmeleri ve delilleri hızlı bir şekilde bulur.
3. **Akademik Araştırma:** Dergileri ve makaleleri anlık erişim için indeksler.

## Performans Düşünceleri
- **İndekslemeyi Optimize Et:** Düzenli indeks değiştirmeleri planla ve eski veriler silinir.
- **Bellek Yönetimi:** Özellikle büyük parçalarla çalışırken JVM yığın'ını izleyin.
- **Ölçekilebilirlik Planlaması:** Veri kümeniz genişledikçe düğüm ekleyin; ağ yükü otomatik dengeler.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|----------|----------|-----|
| Düğümler bağlanamıyor | Bağlantı noktası çakışması veya güvenlik duvarı | `basePort`un açık olduğundan ve diğer hizmetlerin kullanılmadığından emin olun |
| İndeks güncellenmiyor | Olay aboneliği eksik | Dağıtımdan sonra `SearchNetworkNodeEvents.subscribe(masterNode)` çağrısının |
| Bellek uzatma hataları | Çok sayıda büyük parça yüklendi | Parça değişimi küçültün veya JVM yığınını artırın (`-Xmx` bayrağı) |

## Sıkça Sorulan Sorular

**S: Ağ çalışırken yeni dizinler olabilir mi?**
C: Evet—`indexer.addDirectories()` yöntemini kullanın; abone olunan olaylar güncellemeleri gerçek zamanlı olarak yayın.

**S: Düğüm bilgisayarlarınızı nasıl çalıştırırım?**
C: Her `SearchNetworkNode` durum API'leri sağlar; Tercih ettiğiniz izleme aracına entegre edin.

**S: Master düğümü ayrı bir makinede çalıştırmak mümkün mü?**
C: elbette. Tüm düğümlerin aynı `basePort`'u paylaştığından ve ağ üzerinden birbirlerine ulaşabildiğinden emin olun.

**S: Hangi dosya formatları destekleniyor?**
C: GroupDocs.Search, PDF, Word, Excel, PowerPoint, düz metin ve daha birçok formatı kutudan çıkarılamaz.

**S: Yeni bir düğüm ekledikten sonra ağı yeniden başlatmam gerekir mi?**
C: Hayır—düğümler dinamik olarak eklenip gelmiyor; master düğüm shard'ları otomatik olarak yeniden dengeler.

## Sonuç
Artık GroupDocs.Search for Java kullanarak **aramayı nasıl yapılandırılır** sorusuna adım adım tam bir anlayışa ulaşmak; Başlangıç ​​kurulumundan gerçek zamanlı güncellemeler ve dağıtım indekslemeye kadar. Bu yazılımlar, herhangi bir sonuç hızlı, ölçeklenebilir ve güvenilir belge arama kalıp çözümleri oluşturmak için modüle edilebilir.

---

**Son Güncelleme:** 2026-01-08
**Test Edilen Sürüm:** GroupDocs.Search for Java25.4
**Yazar:** GroupDocs