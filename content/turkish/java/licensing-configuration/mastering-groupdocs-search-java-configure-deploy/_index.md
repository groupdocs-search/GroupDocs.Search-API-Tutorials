---
date: '2026-01-08'
description: GroupDocs.Search for Java kullanarak aramayı nasıl yapılandıracağınızı
  ve gerçek zamanlı arama güncellemelerini nasıl etkinleştireceğinizi öğrenin. Ağ
  kurulumu, düğüm dağıtımı ve indeksleme hakkında adım adım kılavuz.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'Java''da GroupDocs.Search ile Aramayı Nasıl Yapılandırılır: Konfigürasyon
  ve Dağıtım Kılavuzu'
type: docs
url: /tr/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# GroupDocs.Search ile Java'da Arama Nasıl Yapılandırılır

Bugünün hızlı tempolu dijital dünyasında, **aramayı nasıl yapılandırılır** sorusunun verimli bir şekilde yanıtlanması bir projenin başarısını belirleyebilir ya da başarısızlığa sürükleyebilir. Binlerce sözleşme, araştırma makalesi ya da iç raporla uğraşıyor olun, iyi tasarlanmış bir arama ağı doğru belgeyi saniyeler içinde bulmanızı sağlar. Bu öğretici, bir arama ağı yapılandırmayı, düğümleri dağıtmayı ve GroupDocs.Search for Java ile **gerçek zamanlı arama güncellemelerini** etkinleştirmeyi adım adım gösterir.

## Hızlı Yanıtlar
- **Bir arama ağının temel amacı nedir?** İndeksleme ve sorgu işleme görevlerini ölçeklenebilirlik ve hız için birden fazla düğüm arasında dağıtmak.  
- **Hangi kütüphane sürümü gereklidir?** GroupDocs.Search for Java v25.4 veya daha yeni.  
- **Lisans gerekiyor mu?** Değerlendirme için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **Gerçek zamanlı güncellemeler nasıl ele alınır?** İndeksleme değişikliklerinde tetiklenen düğüm olaylarına abone olarak.  
- **Yeni belge klasörlerini anında ekleyebilir miyim?** Evet—indexer’ın `addDirectories` metodunu kullanın.

## GroupDocs bağlamında “aramayı nasıl yapılandırılır” ne anlama gelir?
Aramayı yapılandırmak, belgelerinizin nerede olduğunu, düğümlerin nasıl iletişim kurduğunu ve indekslemenin nasıl koordine edildiğini bilen bir **arama ağı** kurmak demektir. Ağ yapılandırıldıktan sonra, kesinti olmadan düğüm ekleyip çıkarabilir, sürekli güncel arama sonuçlarına erişim sağlayabilirsiniz.

## Neden GroupDocs.Search for Java kullanmalı?
- **Ölçeklenebilirlik:** İş yüklerini birden fazla makine arasında dağıtın.  
- **Gerçek zamanlı güncellemeler:** Yeni indekslenen dosyaları ağda anında yansıtın.  
- **Entegrasyon kolaylığı:** Basit Maven kurulumu ve net Java API'leri.  
- **Kurumsal hazır:** Büyük veri kümelerini ve karmaşık sorgu senaryolarını yönetir.

## Önkoşullar
- **Java Development Kit (JDK) 8+** yüklü.  
- **Maven** bağımlılık yönetimi için.  
- Java, Maven ve arama kavramlarına temel aşinalık.

## GroupDocs.Search for Java Kurulumu

### Maven Bağımlılığı
Add the repository and dependency to your `pom.xml`:

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

**Doğrudan İndirme:** Kütüphaneyi ayrıca [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden edinebilirsiniz.

### Lisans Edinme
- **Ücretsiz Deneme:** Tüm özellikleri keşfetmek için deneme lisansı alın.  
- **Geçici Lisans:** Uzatılmış değerlendirme süreleri için talep edin.  
- **Ticari Lisans:** Üretim dağıtımları için gereklidir.

### Basic Initialization
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Java'da arama ağını nasıl yapılandırılır

### Step 1: Import Required Packages
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Step 2: Configure the Network
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parametreler:** `basePath` belge klasörünüzün yolunu gösterir; `basePort` düğüm iletişimi için kullanılan TCP portudur.

## Arama Ağı Düğümlerinin Dağıtılması

### Step 1: Import Deployment Package
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Step 2: Deploy Nodes
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master Düğüm:** Tüm düğümlerde aramaları ve indekslemeyi koordine eder.

## Gerçek Zamanlı Arama Güncellemeleri için Düğüm Olaylarına Abone Olma

### Step 1: Import Event Package
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Step 2: Subscribe to Master Node Events
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Olay İşleme:** Belgeler eklendiğinde, güncellendiğinde veya kaldırıldığında **gerçek zamanlı arama güncellemelerini** etkinleştirir.

## İndeksleme için Dizinler Eklemek

### Step 1: Import Indexer Package
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Step 2: Add Document Directories
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dinamik İndeksleme:** Gerektiği kadar klasör ekleyin; ağ bunları otomatik olarak indeksleyecek.

## İndekslenmiş Belgeleri Getirme

### Step 1: Import Searcher Package
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Step 2: Retrieve Document Information
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
- **Shard Yönetimi:** Belgeleri shard'lar arasında dağıtarak büyük veri setlerini verimli bir şekilde yönetir.

## Pratik Uygulamalar
1. **Kurumsal Belge Yönetimi:** Milyonlarca dosya üzerinde aramayı merkezileştirir.  
2. **Hukuk Firmaları:** Dava dosyalarını, sözleşmeleri ve delilleri hızlıca bulur.  
3. **Akademik Araştırma:** Dergileri ve makaleleri anında erişim için indeksler.

## Performans Düşünceleri
- **İndekslemeyi Optimize Et:** Düzenli indeks yenilemeleri planla ve eski verileri temizle.  
- **Bellek Yönetimi:** Özellikle büyük shard'larla çalışırken JVM heap'ini izleyin.  
- **Ölçeklenebilirlik Planlaması:** Veri kümeniz büyüdükçe düğüm ekleyin; ağ yükü otomatik dengeler.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| Düğümler bağlanamıyor | Port çakışması veya güvenlik duvarı | `basePort`'un açık olduğundan ve başka hizmetler tarafından kullanılmadığından emin olun |
| İndeks güncellenmiyor | Olay aboneliği eksik | Dağıtımdan sonra `SearchNetworkNodeEvents.subscribe(masterNode)` çağırın |
| Bellek yetersizliği hataları | Çok sayıda büyük shard yüklendi | Shard boyutunu küçültün veya JVM heap'ini artırın (`-Xmx` bayrağı) |

## Sıkça Sorulan Sorular

**S: Ağ çalışırken yeni dizinler ekleyebilir miyim?**  
C: Evet—`indexer.addDirectories()` metodunu kullanın; abone olunan olaylar güncellemeleri gerçek zamanlı olarak yayar.

**S: Düğüm sağlığını nasıl izlerim?**  
C: Her `SearchNetworkNode` durum API'leri sağlar; tercih ettiğiniz izleme aracına entegre edin.

**S: Master düğümü ayrı bir makinede çalıştırmak mümkün mü?**  
C: Kesinlikle. Tüm düğümlerin aynı `basePort`'u paylaştığından ve ağ üzerinden birbirlerine ulaşabildiğinden emin olun.

**S: Hangi dosya formatları destekleniyor?**  
C: GroupDocs.Search, PDF, Word, Excel, PowerPoint, düz metin ve daha birçok formatı kutudan çıkar çıkmaz destekler.

**S: Yeni bir düğüm ekledikten sonra ağı yeniden başlatmam gerekir mi?**  
C: Hayır—düğümler dinamik olarak eklenip çıkarılabilir; master düğüm shard'ları otomatik olarak yeniden dengeler.

## Sonuç
Artık GroupDocs.Search for Java kullanarak **aramayı nasıl yapılandırılır** sorusuna adım adım tam bir anlayışa sahipsiniz; başlangıç kurulumundan gerçek zamanlı güncellemeler ve dağıtık indekslemeye kadar. Bu kalıpları, herhangi bir sektörde hızlı, ölçeklenebilir ve güvenilir belge arama çözümleri oluşturmak için uygulayın.

---

**Son Güncelleme:** 2026-01-08  
**Test Edilen Sürüm:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs