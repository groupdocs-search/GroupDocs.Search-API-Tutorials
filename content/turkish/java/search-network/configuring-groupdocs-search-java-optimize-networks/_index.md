---
date: '2026-01-16'
description: Java'da GroupDocs Search ağını nasıl yapılandıracağınızı ve geliştirilmiş
  arama verimliliği için indekse eşanlamlı kelimeler eklemeyi öğrenin.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Java'da GroupDocs.Search Ağını Yapılandır – Aramayı Hızlandır
type: docs
url: /tr/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# GroupDocs.Search Ağını Java’da Yapılandırma – Aramayı Hızlandırma

Günümüzün veri odaklı uygulamalarında **configure groupdocs search network**, büyük belge koleksiyonları üzerinde hızlı ve doğru sonuçlar sunmanın ana adımıdır. İster kurumsal çapta bir arama portalı oluşturuyor olun, ister mevcut bir çözümü genişletiyor olun, iyi yapılandırılmış bir GroupDocs.Search ağı, yatay ölçekleme, eşanlamlı destek ekleme ve gecikmeyi düşük tutma imkanı sağlar. Bu öğreticide, Java kullanarak bir GroupDocs.Search ağını nasıl kuracağınızı, dağıtacağınızı ve ince ayar yapacağınızı, ayrıca indeks'e eşanlamlı ekleme ve düğüm yaşam döngülerini yönetme konusunda pratik ipuçlarını öğreneceksiniz.

## Hızlı Yanıtlar
- **GroupDocs.Search ağını yapılandırmanın temel faydası nedir?** Dağıtık indeksleme ve sorgulamayı mümkün kılar, performans ve ölçeklenebilirliği artırır.  
- **Örnekleri çalıştırmak için lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme yeterlidir; üretim için ticari lisans gereklidir.  
- **İndeksi yeniden oluşturmak zorunda kalmadan eşanlamlılar eklenebilir mi?** Evet—çalışma zamanında eşanlamlı sözlüğünü kullanarak **add synonyms to index**.  
- **Kaç düğüm dağıtabilirim?** Altyapınızın izin verdiği kadar düğüm dağıtabilirsiniz; her düğüm kendi portunda çalışır.  

## GroupDocs.Search ağını yapılandırmak ne demektir?
GroupDocs.Search ağını yapılandırmak, birden fazla JVM örneğinin indeksleme ve arama üzerinde iş birliği yapmasını sağlayan klasör yapısını, portları ve düğüm ayarlarını tanımlamak anlamına gelir. Bu yapılandırma, çalışanları (shard'ları) koordine eden bir master‑node oluşturur ve sorguların tüm veri kümesi üzerinde yürütülmesini sağlar.

## Neden GroupDocs.Search ağı yapılandırılmalı?
- **Scalability** – İndeksleme yükünü birkaç makine arasında dağıtın.  
- **Reliability** – Düğümler, kesinti olmadan eklenebilir veya kaldırılabilir.  
- **Search relevance** – Daha zengin sonuçlar için indeks'e eşanlamlı ekleyin.  
- **Performance** – Paralel sorgu yürütme yanıt süresini azaltır.  

## Önkoşullar
- Java Development Kit (JDK) 8 veya daha yeni  
- Projeyi derlemek için Maven  
- Java sözdizimi hakkında temel bilgi  
- GroupDocs.Search for Java kütüphanesine erişim (Maven üzerinden veya resmi sürüm sayfasından indirilir)  

## GroupDocs.Search for Java'ı Kurma

Maven **pom.xml** dosyanıza depo ve bağımlılığı ekleyin:

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

### Lisans Edinme
- **Free Trial** – Ücretsiz olarak temel özellikleri keşfedin.  
- **Temporary License** – Kısa vadeli testler için tam yetenekleri açın.  
- **Commercial License** – Üretim dağıtımları için gereklidir.  

### Temel Başlatma ve Kurulum
Kütüphanenin doğru yüklendiğini doğrulamak için basit bir Java sınıfı oluşturun:

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

## GroupDocs.Search Ağını Yapılandırmak İçin Adım‑Adım Kılavuz

### 1. Arama Ağını Yapılandırma
Düğüm iletişimi için temel belge klasörünü ve başlangıç portunu tanımlayın.

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

- **basePath** – Sözlüklerin (ör. eşanlamlı dosyaları) bulunduğu yer.  
- **basePort** – İlk port; sonraki düğümler bu değerden artar.  

### 2. Arama Ağı Düğümlerini Dağıtma
Aynı yapılandırmayı paylaşan birden fazla worker düğümü başlatın.

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

Her düğüm kendi portunda (basePort + index) çalışır ve genel indeksin bir shard'ını tutar.

### 3. Düğüm Olaylarına Abone Olma
Master node'a bir olay dinleyicisi ekleyerek sağlık, indeksleme ilerlemesi ve hata durumlarını izleyin.

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

Olay geri çağrıları, düğüm başlatma/durdurma, indeksleme tamamlanması ve beklenmeyen hatalara yanıt vermenizi sağlar.

### 4. Bir Düğümün Indexer'ına Eşanlamlılar Ekleme  
Çalışma zamanında **add synonyms to index** yaparak alaka düzeyini artırın.

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
Master node'a hangi klasörlerin aranabilir belgeler içerdiğini belirtin.

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

Metot, dizini özyinelemeli tarar ve dosyaları shard'lar arasında dağıtır.

### 6. Ağda Metin Araması Yapma
Tüm düğümlerde bir sorgu çalıştırın, isteğe bağlı olarak tam eşleşme davranışını zorlayabilirsiniz.

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

Kök bulma olmadan katı terim eşleşmesi gerektiğinde `exactMatchOnly` değerini `true` olarak değiştirin.

### 7. Ağ Düğümlerini Kapatma
İşlem tamamlandığında kaynakları nazikçe serbest bırakın.

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

Doğru kapatma bellek sızıntılarını önler ve JVM'in sağlıklı kalmasını sağlar.

## Pratik Uygulamalar
| Senaryo | Ağın nasıl yardımcı olduğu |
|----------|-----------------------------|
| **Enterprise Search** | Petabayt ölçeğindeki korpuslar için veri merkezi sunucuları arasında indekslemeyi dağıtın. |
| **Document Management** | Kullanıcıların farklı terminolojiyle bile belgeleri bulabilmesi için indeks'e eşanlamlı ekleyin. |
| **E‑commerce Catalog** | Yerel ürün aramalarını hızlı bir şekilde sunmak için bölgeye özgü düğümler dağıtın. |
| **Content Management** | Editörler belirli dizinlere yeni dosyalar eklerken içeriği aranabilir tutun. |

## Yaygın Sorunlar ve Çözümler
- **Port Conflicts** – Her düğümün portunun (basePort + index) boş olduğundan emin olun; gerekirse `basePort` değerini ayarlayın.  
- **Synonym Not Applied** – Terimleri ekledikten sonra `indexer.setDictionary(dictionary)` çağrısını yaptığınızı doğrulayın.  
- **Node Not Responding** – Olaylara abone olun; ağ problemlerini teşhis etmek için `NodeFailed` geri çağrılarını kontrol edin.  
- **Memory Leak on Close** – Dağıtılan her düğüm için her zaman `node.close()` çağırın.  

## Sıkça Sorulan Sorular

**S: Birden fazla düğüm dağıtmak arama performansını nasıl artırır?**  
C: Her düğüm verinin bir shard'ını indeksler, paralel işleme olanak tanır ve iş yükü paylaşıldıkça sorgu gecikmesini azaltır.

**S: Mevcut belgeleri yeniden indekslemeden eşanlamlı ekleyebilir miyim?**  
C: Evet, çalışma zamanında eşanlamlı sözlüğü aracılığıyla **add synonyms to index** yapabilirsiniz; değişiklikler yeni sorgular için hemen geçerli olur.

**S: Düğüm olaylarına abone olmak zorunlu mu?**  
C: Temel operasyon için gerekli olmasa da, olay aboneliği düğüm sağlığına görünürlük sağlar ve hatalara hızlı yanıt vermenize yardımcı olur.

**S: Düğüm kaynaklarını yönetmek için en iyi uygulamalar nelerdir?**  
C: Boşta kalan düğümleri düzenli olarak kapatın, JVM bellek kullanımını izleyin ve kaynak tüketimini optimal tutmak için düşük yoğunluklu saatlerde düğümleri yeniden başlatın.

**S: GroupDocs.Search PDF'ler veya görüntüler gibi metin dışı formatları destekliyor mu?**  
C: Kesinlikle. Kütüphane PDF'lerden, Office dosyalarından metin çıkarır ve hatta görüntülerde OCR gerçekleştirerek bunları kutudan çıkar çıkmaz aranabilir hâle getirir.

---

**Son Güncelleme:** 2026-01-16  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs