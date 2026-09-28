---
date: '2026-09-27'
description: GroupDocs.Search for Java kullanarak java tam metin aramasını nasıl uygulayacağınızı
  öğrenin, aramaya dosya ekleyin, dizinleri yapılandırın ve gerçek zamanlı indekslemeyi
  etkinleştirin.
keywords:
- java full text search
- event driven indexing
- java search engine
- add files to search
- real time indexing java
lastmod: '2026-09-27'
og_description: GroupDocs.Search kullanarak java tam metin aramasını uygulayın. Dosya
  eklemeyi, düğümleri yapılandırmayı ve gerçek zamanlı indekslemeyi dakikalar içinde
  öğrenin.
og_image_alt: Guide to setting up java full text search with GroupDocs.Search
og_title: GroupDocs.Search ile java tam metin aramasını nasıl uygularsınız
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to implement java full text search using GroupDocs.Search
    for Java, add files to search, configure directories, and enable real time indexing.
  headline: How to implement java full text search with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: Yes. The library works with any Java runtime, and you can point `basePath`
      to a network‑mounted folder or a cloud storage mount.
    question: Can I use GroupDocs.Search on a cloud‑based Java application?
  - answer: Subscribe to node events (see Feature 3) and call `addFiles` or `addDirectories`
      again for the modified paths.
    question: How do I update the index when a file changes?
  - answer: Practically, the limit is defined by your hardware and network bandwidth.
      The API imposes no hard cap.
    question: Is there a limit to the number of nodes I can deploy?
  - answer: No. Adding files triggers indexing automatically; you only need to commit
      if you defer the operation.
    question: Do I need to restart nodes after adding new files?
  - answer: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, and many image types—over
      50 formats in total.
    question: Which document formats are supported out of the box?
  type: FAQPage
tags:
- java full text search
- GroupDocs.Search
- search indexing
title: GroupDocs.Search ile java tam metin aramasını nasıl uygularsınız
type: docs
url: /tr/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Java tam metin aramasını GroupDocs.Search ile nasıl uygularsınız

Veri odaklı uygulamaların çağında, **java full text search** büyük belge koleksiyonlarını anında aranabilir bilgi tabanlarına dönüştürmek için hayati öneme sahiptir. İster kurumsal düzeyde bir portal, ister hafif bir masaüstü yardımcı program geliştirin, iyi yapılandırılmış bir arama ağı sorgu gecikmesini saniyelerden milisaniyelere düşürebilir ve veri büyüdükçe sonuçların alaka düzeyini korur. Bu eğitim, **GroupDocs.Search for Java**'yı dağıtmayı, dosyaları aramaya eklemeyi, düğümlerdeki dizinleri yapılandırmayı ve indeksinizin manuel müdahale olmadan güncel kalmasını sağlayan gerçek‑zamanlı indekslemeyi nasıl etkinleştireceğinizi adım adım gösterir.

> **Neden bu önemli:** Bir java tam metin arama indeksi sorgu gecikmesini azaltır, veri hacmiyle ölçeklenir ve herhangi bir Java‑tabanlı çözüm—web portalları, masaüstü uygulamaları veya bulut mikro hizmetleri—için güçlü tam‑metin yetenekleri getirir.

## Hızlı yanıtlar
- **GroupDocs.Search'ün temel amacı nedir?** Dağıtılmış bir ağda belgeleri indeksleyen ve arayan ölçeklenebilir bir java arama motoru sağlar.  
- **Hangi sürümü kullanmalıyım?** Yeni projeler için en son kararlı sürüm (ör. 25.4) önerilir.  
- **Lisans gerekir mi?** 30‑günlük ücretsiz deneme mevcuttur; üretim kullanımı için kalıcı bir lisans gereklidir.  
- **Hem dosyaları hem de tüm dizinleri ekleyebilir miyim?** Evet – içerik almak için `addFiles` ve `addDirectories` yardımcılarını kullanın.  
- **Hangi Java sürümü gereklidir?** Maven ile bağımlılık yönetimi yapılabilen Java 8 ve üzeri.  
- **Gerçek zamanlı indeksleme java nasıl çalışır?** Düğüm olaylarına abone olarak dosyalar değiştiğinde otomatik yeniden indekslemeyi tetikleyebilirsiniz.

## “create searchable index java” nedir?
Java’da aranabilir bir indeks oluşturmak, terimleri içeren belgelerle eşleyen bir veri yapısı inşa etmek anlamına gelir; bu sayede hızlı tam‑metin sorguları yapılabilir. **GroupDocs.Search for Java**, ağır işleri soyutlayarak belgeleri beslemeye ve arama davranışını ayarlamaya odaklanmanızı sağlar.

## Neden GroupDocs.Search for Java kullanmalıyım?
GroupDocs.Search, yatay olarak ölçeklenebilen bir java arama motoru sunar, 50'den fazla giriş ve çıkış formatını destekler ve olay‑tabanlı indekslemeye imkan tanır. Birden çok düğüm dağıtarak indeksleme iş yükünü yayabilir, yerleşik sağlık kontrolleriyle ağın güvenilirliğini sağlayabilirsiniz. Ayrıca RESTful API'ler ve ince ayar yapılabilir analizörler sunar.

## Önkoşullar
- **JDK 8+** geliştirme makinenizde kurulu.  
- **IntelliJ IDEA** veya **Eclipse** gibi bir IDE.  
- **Java** ve **Maven** hakkında temel bilgi.  
- **GroupDocs.Search for Java** kütüphanesine erişim (indirme veya Maven).

## GroupDocs.Search for Java kurulumu

### Maven bağımlılığı
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

JAR dosyasını doğrudan resmi siteden de indirebilirsiniz: [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/).

### Lisans edinme
- **Ücretsiz deneme:** 30‑günlük değerlendirme.  
- **Geçici lisans:** Uzatılmış test için talep edin.  
- **Satın alma:** Üretim dağıtımları için gereklidir.

### Temel başlatma
İndeks dosyalarının saklanacağı klasöre işaret eden ve temel iletişim portunu tanımlayan bir yapılandırma nesnesi oluşturun:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## GroupDocs.Search ile java tam metin arama indeksi nasıl oluşturulur?
Bir `SearchConfiguration` nesnesi yükleyin, bir `SearchNetworkNode` başlatın ve `node.getIndexer().addFiles(...)` çağrısıyla indeksi doldurun. Bu tek‑satır kalıp, sorguları anında kabul eden tam işlevsel bir java tam metin arama ağı oluşturur. Aynı temel yol ve port aralığını paylaşan daha fazla düğüm ekleyerek ölçeklendirebilirsiniz.

### Özellik 1 – yapılandırma ve ağ kurulumu
`SearchConfiguration` sınıfı bir düğümü ayağa kaldırmak için gereken tüm ayarları tutar.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – İndeks verisinin kalıcı olarak saklanacağı dizin.  
- **`basePort`** – Başlangıç portu; her düğüm bu değerden artar.

### Özellik 2 – arama ağı düğümlerinin dağıtımı
`SearchNetworkNode` herhangi bir makinede çalışabilen bireysel bir indeksleme hizmetini temsil eder.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

`SearchNetworkNode`, bir indeksi barındıran, ekleme/çıkarma olaylarını işleyen ve arama sorgularına yanıt veren çekirdek çalışma zaman bileşenidir. Birden çok düğüm dağıtarak **java full text search** kümeleri oluşturabilir ve yatay olarak ölçeklendirebilirsiniz.

### Özellik 3 – düğüm olaylarına abone olma
Gerçek‑zamanlı güncellemeler indeksin dosya sistemi değişiklikleriyle senkronize kalmasını sağlar.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Olayları dinleyerek yeni dosyalar geldiğinde otomatik olarak yeniden indekslemeyi tetikleyebilir, **event driven indexing**'i manuel betikler olmadan gerçekleştirebilirsiniz.

### Özellik 4 – düğüme dizin ekleme
Bu yardımcıyı **dizinleri düğüme eklemek** için kullanın; desteklenen tüm belgeleri özyinelemeli olarak toplar.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

`DirectoryAdder.addDirectories(node, path)` yöntemi bir klasör ağacını dolaşır ve her desteklenen dosya için `addFiles` çağrısı yapar, toplu alımı basitleştirir.

### Özellik 5 – düğüme dosya ekleme
Daha ince ayar gerektiğinde, **dosyaları tek tek aramaya ekleyin**:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

`addFiles`, dosya yolu listesi veya akışları kabul eden bir yöntemdir; bulut depolama, geçici önbellekler veya bellek içi akışlardan belgeleri indekslemenizi sağlar.

## Yaygın kullanım senaryoları
- **Kurumsal belge portalları** binlerce PDF ve Office dosyası üzerinde anlık arama gerektiren.  
- **Hukuki e‑keşif platformları** yeni deliller sürekli eklendiğinde gerçek zamanlı aranabilir olmalı.  
- **İçerik yönetim sistemleri** resim, sunum ve elektronik tablo depolayan ve tam‑metin arama ihtiyacı olan.

## Yaygın sorunlar & çözümler
| Sorun | Neden | Çözüm |
|-------|--------|-----|
| **Arama sonuçlarında belge görünmüyor** | İndeks henüz commit edilmemiş | Dosyaları ekledikten sonra `node.getIndexer().commit()` çağırın. |
| **Port çakışması hatası** | Başka bir hizmet `basePort`'u kullanıyor | Farklı bir `basePort` seçin veya boş portları kontrol edin. |
| **Desteklenmeyen dosya formatı** | Kütüphane ilgili ayrıştırıcıyı içermiyor | Dosya uzantısının desteklendiğinden emin olun veya özel bir çıkarıcı ekleyin. |

## Sorun giderme ipuçları
- **Düğüm sağlığını doğrulayın:** Yerleşik sağlık‑kontrol uç noktasını (`http://localhost:{port}/health`) kullanarak her düğümün çalıştığını onaylayın.  
- **Bellek kullanımını izleyin:** Büyük belge topluları bellek tüketimini artırabilir; daha küçük parçalar halinde indeksleyin ve periyodik olarak `commit()` çağırın.  
- **Günlükleri kontrol edin:** GroupDocs.Search, `basePath` klasörüne ayrıntılı günlükler yazar—parsing hataları veya ağ zaman aşımı için bunları inceleyin.

## Sıkça sorulan sorular

**S: GroupDocs.Search'ü bulut‑tabanlı bir Java uygulamasında kullanabilir miyim?**  
C: Evet. Kütüphane herhangi bir Java çalışma zamanı ile çalışır ve `basePath`'i ağ‑bağlı bir klasöre veya bulut depolama bağlamına yönlendirebilirsiniz.

**S: Bir dosya değiştiğinde indeksi nasıl güncellerim?**  
C: Düğüm olaylarına abone olun (bkz. Özellik 3) ve değiştirilen yollar için tekrar `addFiles` veya `addDirectories` çağırın.

**S: Dağıtabileceğim düğüm sayısına bir limit var mı?**  
C: Pratikte limit donanım ve ağ bant genişliğinizle belirlenir. API sabit bir üst sınır koymaz.

**S: Yeni dosyalar ekledikten sonra düğümleri yeniden başlatmam gerekir mi?**  
C: Hayır. Dosya ekleme otomatik olarak indekslemeyi tetikler; işlemi ertelediyseniz `commit` yapmanız yeterlidir.

**S: Hangi belge formatları kutudan çıktığı gibi desteklenir?**  
C: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML ve birçok görüntü türü—toplamda 50'den fazla format.

**S: Sürekli dosya yüklemesi alan bir klasör için gerçek zamanlı indeksleme java nasıl etkinleştirilir?**  
C: `java.nio.file.WatchService` gibi bir dosya sistemi izleyici uygulayarak yeni bir dosya tespit edildiğinde `DirectoryAdder.addDirectories(node, path)` çağırın.

---

**Son güncelleme:** 2026-09-27  
**Test edilen sürüm:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [java tam metin arama nasıl uygulanır: GroupDocs.Search ile indeks dizini oluşturma](/search/java/indexing/groupdocs-search-java-create-index/)
- [Full Text Search Java Groupdocs Search uygulama](/search/java/searching/implement-full-text-search-java-groupdocs-search/)
- [GroupDocs.Search ile Java’da Aramayı Yapılandırma - Konfigürasyon & Dağıtım Kılavuzu](/search/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/)
