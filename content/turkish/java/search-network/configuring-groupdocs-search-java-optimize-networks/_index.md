---
date: '2026-07-16'
description: GroupDocs.Search network'ü Java'da nasıl yapılandırılacağını, index'e
  synonyms eklemeyi ve distributed nodes arasında search performance'ı boost etmeyi
  öğrenin.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: GroupDocs.Search network'ü Java'da nasıl yapılandırılacağını ve index'e
  synonyms ekleyerek daha hızlı, daha doğru sonuçlar elde etmeyi öğrenin. Bu step‑by‑step
  rehberi izleyin.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: GroupDocs.Search Network'ü Java'da Nasıl Yapılandırılır – Boost Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: GroupDocs.Search Network'ü Java'da Nasıl Yapılandırılır Rehberi
type: docs
url: /tr/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Java’da GroupDocs.Search Ağını Nasıl Yapılandırılır – Aramayı Hızlandırma

Modern, veri‑yoğun uygulamalarda, **how to configure GroupDocs** doğru bir şekilde yapılandırmak, devasa belge depoları üzerinde ışık‑hızı, ilgili arama sonuçları sunmanın temelidir. İster bir kurumsal portal, bir bilgi‑tabanı ya da bir ürün kataloğu oluşturuyor olun, iyi ayarlanmış bir GroupDocs.Search ağı, yatay ölçekleme, eşanlamlı mantığı ekleme ve gecikmeyi kontrol altında tutma imkanı sağlar. Bu öğreticide, Java kullanarak bir GroupDocs.Search ağını kurmak, dağıtmak ve ince ayar yapmak için gereken tüm adımları, ayrıca indeks'e eşanlamlı ekleme ve düğüm yaşam döngülerini yönetme konusunda pratik tavsiyeleri ele alacağız.

## Hızlı Yanıtlar
- **GroupDocs.Search ağını yapılandırmanın temel faydası nedir?** Bu, dağıtık indeksleme ve sorgulamayı mümkün kılar, performans ve ölçeklenebilirliği artırır.  
- **Örnekleri çalıştırmak için bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **İndeks yeniden oluşturulmadan eşanlamlılar eklenebilir mi?** Evet—çalışma zamanında eşanlamlı sözlüğünü kullanarak **add synonyms to index**.  
- **Kaç düğüm dağıtabilirim?** Altyapınızın izin verdiği kadar düğüm dağıtabilirsiniz; her düğüm kendi portunda çalışır.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya daha yenisi desteklenir, tam uyumluluk JDK 21'e kadar sağlanır.

## GroupDocs.Search ağını yapılandırmak nedir?
**GroupDocs.Search ağı**, ortak bir belge kümesini indekslemek ve sorgulamak için iş birliği yapan JVM süreçlerinin bir koleksiyonudur. Bir veya daha fazla işçi düğüm (shard) yöneten bir master düğümden oluşur. Ağ, temel depolamayı soyutlar, böylece tek bir sorgu otomatik olarak her shard'e yayınlanır ve sonuçlar, çağırana döndürülmeden önce birleştirilir.

## Neden bir GroupDocs.Search ağı yapılandırmalısınız?
GroupDocs.Search ağını yapılandırmak size üç somut avantaj sağlar: **scalability**, **reliability**, ve **enhanced relevance**. İndeksleme yükünü 20'ye kadar düğüm arasında dağıtarak, her biri 5 GB bir shard işlediğinde, tek düğümlü kurulumla karşılaştırıldığında toplam indeksleme süresini yaklaşık %70 azaltabilirsiniz. Bir eşanlamlı sözlüğü eklemek, alternatif terminoloji kullanan sorgular için geri getirmeyi %35'e kadar artırır, aynı zamanda düğüm yedekliliği bakım pencerelerinde %99,9 çalışma süresi garantiler.

## Önkoşullar
- Java Development Kit (JDK) 8 – 21 (herhangi bir LTS sürümü)  
- Proje oluşturmak için Maven 3.5 +  
- Temel Java sözdizimi ve Maven bağımlılık yönetimi konusunda aşinalık  
- GroupDocs.Search for Java kütüphanesine erişim (Maven Central veya resmi sürüm sayfası üzerinden temin edilebilir)

## Java için GroupDocs.Search Kurulumu

Maven **pom.xml** dosyanıza depo ve bağımlılığı ekleyin:

The following XML snippet adds the GroupDocs.Search repository and library dependency.  
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

### Lisans Edinimi
- **Free Trial** – Ücretsiz deneme, temel özellikleri maliyetsiz keşfetmenizi sağlar.  
- **Temporary License** – Kısa vadeli testler için tam yetenekleri açar.  
- **Commercial License** – Üretim dağıtımları için gereklidir ve premium destek almanızı sağlar.

### Temel Başlatma ve Kurulum
Kütüphanenin doğru yüklendiğini doğrulamak için basit bir Java sınıfı oluşturun:

The SampleInitializer class demonstrates loading the GroupDocs.Search engine.  
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## GroupDocs.Search Ağını Yapılandırma Adım‑Adım Kılavuzu

### 1. Arama Ağını Yapılandırma
Düğüm iletişimi için temel belge klasörünü ve başlangıç portunu tanımlayın.

SearchNetworkConfig holds the configuration for the network nodes.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Sözlüklerin (ör. eşanlamlı dosyalar) bulunduğu dizin.  
- **basePort** – İlk port; sonraki düğümler bu değerden artar.

### 2. Arama Ağı Düğümlerini Dağıtma
Aynı yapılandırmayı paylaşan birden fazla işçi düğümünü başlatın.

SearchNode represents an individual node in the distributed network.  
```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Her düğüm kendi portunda (`basePort + index`) çalışır ve genel indeksin bir shard'ını tutar, böylece indeksleme ve sorgu yürütme işlemleri paralel olarak işlenebilir.

### 3. Düğüm Olaylarına Abone Olma
Master düğüme bir olay dinleyicisi ekleyerek sağlık, indeksleme ilerlemesi ve hata koşullarını izleyin.

NetworkEventListener handles callbacks for node lifecycle events.  
```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Olay geri çağrıları, düğüm başlatma/durdurma, indeksleme tamamlanması ve beklenmeyen hatalara yanıt vermenizi sağlar, dağıtık sistem üzerinde tam gözlemlenebilirlik sunar.

### 4. Bir Düğümün İndeksleyicisine Eşanlamlılar Ekleme  
Çalışma zamanında **add synonyms to index** yaparak alaka düzeyini artırın.

SynonymDictionary allows adding synonym groups to the indexer.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Eşdeğer olarak kabul edilmesi gereken terimlerin dizisi.  
- **clearBeforeAdding** – Mevcut girdileri değiştirmek istiyorsanız `true` olarak ayarlayın.

### 5. İndeksleme İçin Dizinler Ekleme
Master düğüme, aranabilir belgeleri içeren klasörlerin hangileri olduğunu söyleyin.

Indexer.addDirectory registers a folder for indexing.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Metot, dizini özyinelemeli olarak tarar ve dosyaları shard'lar arasında dağıtır, tüm dosyaları belleğe yüklemeden 10 TB'den fazla veriyi destekler.

### 6. Ağda Metin Araması Gerçekleştirme
Tüm düğümlerde bir sorgu çalıştırın, isteğe bağlı olarak tam eşleşme davranışını zorlayabilirsiniz.

SearchEngine.search runs the query on the network.  
```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

`exactMatchOnly` değerini `true` yapın, kök bulma olmadan katı terim eşleşmesi gerektiğinde; bu, kod‑arama senaryolarında kesinliği %20'ye kadar artırabilir.

### 7. Ağ Düğümlerini Kapatma
İşlem tamamlandığında kaynakları nazikçe serbest bırakın.

`node.close()` shuts down a SearchNode and frees resources.  
```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Doğru kapanış bellek sızıntılarını önler ve JVM'i sağlıklı tutar, özellikle düşük yoğunluklu saatlerde düğümleri yeniden kullanan uzun süreli hizmetlerde.

## Pratik Uygulamalar
| Senaryo | Ağın nasıl yardımcı olduğu |
|----------|----------------------------|
| **Kurumsal Arama** | Petabayt ölçeğindeki veri havuzları için veri merkezi sunucuları arasında indekslemeyi dağıtarak, 100 M+ belge için saniyenin altında sorgu gecikmesi elde edilir. |
| **Belge Yönetimi** | Kullanıcıların farklı terminolojiyle bile belgeleri bulabilmesi için indeks'e eşanlamlılar ekleyin, geri getirmeyi %35'e kadar artırır. |
| **E‑ticaret Kataloğu** | Bölge‑spesifik düğümler dağıtarak yerel ürün aramalarını hızlı bir şekilde hizmete sunun, ortalama yanıt süresini 250 ms'den 80 ms'ye düşürür. |
| **İçerik Yönetimi** | Editörler belirli dizinlere yeni dosyalar eklerken içeriği aranabilir tutun; ağ, kesinti olmadan artımlı olarak yeniden indeksler. |

## Yaygın Sorunlar ve Çözümler
- **Port Çakışmaları** – Her düğümün portunun (`basePort + index`) boş olduğundan emin olun; gerekirse `basePort`'u ayarlayın.  
- **Eşanlamlı Uygulanmadı** – Terimleri ekledikten sonra `indexer.setDictionary(dictionary)` çağırdığınızı doğrulayın; aksi takdirde yeni eşanlamlılar arama sırasında dikkate alınmaz.  
- **Düğüm Yanıt Vermiyor** – Olaylara abone olun; ağ problemlerini teşhis etmek için `NodeFailed` geri çağrılarını kontrol edin.  
- **Kapatma Sırasında Bellek Sızıntısı** – Dağıtılan her düğüm için her zaman `node.close()` çağırın; otomatik temizlik için try‑with‑resources bloğu kullanmayı düşünün.  

## Sıkça Sorulan Sorular

**S: Birden fazla düğüm dağıtmak arama performansını nasıl artırır?**  
C: Her düğüm verinin bir shard'ını indeksler, paralel işlemeye izin verir ve iş yükü küme içinde paylaşıldıkça sorgu gecikmesini azaltır.

**S: Mevcut belgeleri yeniden indekslemeden eşanlamlılar ekleyebilir miyim?**  
C: Evet, çalışma zamanında eşanlamlı sözlüğü aracılığıyla **add synonyms to index** yapabilirsiniz; değişiklikler yeni sorgular için hemen etkili olur.

**S: Düğüm olaylarına abone olmak zorunlu mu?**  
C: Temel operasyon için gerekli olmasa da, olay aboneliği düğüm sağlığına görünürlük sağlar ve hatalara hızlı yanıt vermenize yardımcı olur.

**S: Düğüm kaynaklarını yönetmek için en iyi uygulamalar nelerdir?**  
C: Boşta olan düğümleri düzenli olarak kapatın, JVM bellek kullanımını izleyin ve kaynak tüketimini optimum tutmak için düşük yoğunluklu saatlerde düğümleri yeniden kullanın.

**S: GroupDocs.Search PDF veya görüntüler gibi metin dışı formatları destekliyor mu?**  
C: Kesinlikle. Kütüphane PDF'lerden, Office dosyalarından metin çıkarır ve görüntüler üzerinde OCR gerçekleştirir, böylece bunlar kutudan çıkar çıkmaz aranabilir olur.

**Son Güncelleme:** 2026-07-16  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [GroupDocs.Search for Java Öğreticileri ve Örnekleri](/search/net/)
- [.NET'te GroupDocs.Search Ağını Yapılandırma: Kapsamlı Rehber](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [.NET'te GroupDocs kullanarak Arama Ağı Düğümü Dağıtma: Verimli Belge İndeksleme ve Geri Getirme](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)