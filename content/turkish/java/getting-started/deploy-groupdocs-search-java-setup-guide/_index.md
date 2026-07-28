---
date: '2026-02-27'
description: Java için GroupDocs.Search ile aranabilir bir indeks oluşturmayı, aramaya
  dosyalar eklemeyi, düğüme dizinler eklemeyi ve gerçek zamanlı indekslemeyi etkinleştirmeyi
  öğrenin.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Aranabilir Dizin Oluşturma Java – GroupDocs.Search for Java'ı Dağıt
type: docs
url: /tr/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Java’da Aranabilir İndeks Oluşturma – GroupDocs.Search for Java’yı Dağıtın

Günümüzün veri odaklı dünyasında, **creating a searchable index java** uygulamaları büyük belge koleksiyonlarını verimli bir şekilde yönetmek zorundadır. İster kurumsal düzeyde bir arama servisi ister daha küçük bir proje inşa ediyor olun, iyi yapılandırılmış bir arama ağı, geri getirme hızını ve alaka düzeyini büyük ölçüde artırabilir. Bu rehberde **GroupDocs.Search for Java** kurulum sürecinin tamamını, aramaya dosya eklemekten düğüme dizin eklemeye kadar adım adım anlatacağız, böylece belgelerinizi hemen indekslemeye başlayabilirsiniz.

> **Neden Önemli:** Aranabilir bir indeks, sorgu gecikmesini saniyelerden milisaniyelere düşürür, veri artışınızla ölçeklenir ve herhangi bir Java‑tabanlı çözüme güçlü tam‑metin yetenekleri eklemenizi sağlar—ister bir web portalı, ister bir masaüstü uygulaması, ister bir bulut mikroservisi olsun.

## Hızlı Yanıtlar
- **GroupDocs.Search'ün temel amacı nedir?** Dağıtık bir ağda belgeleri indekslemek ve aramak için ölçeklenebilir, Java‑tabanlı bir motor sağlar.  
- **Hangi sürümü kullanmalıyım?** En son kararlı sürüm (ör. 25.4), yeni projeler için önerilir.  
- **Lisans gerekir mi?** 30‑günlük ücretsiz deneme mevcuttur; üretim kullanımı için kalıcı bir lisans gereklidir.  
- **Hem dosyalar hem de tüm dizinler ekleyebilir miyim?** Evet – içeriği almak için `addFiles` ve `addDirectories` yardımcılarını kullanın.  
- **Hangi Java sürümü gereklidir?** Bağımlılık yönetimi için Maven ile Java 8 ve üzeri.  
- **Gerçek zamanlı indeksleme java nasıl çalışır?** Düğüm olaylarına abone olarak dosyalar değiştikçe otomatik yeniden indekslemeyi tetikleyebilirsiniz.

## “create searchable index java” nedir?
Java’da aranabilir bir indeks oluşturmak, terimleri içeren belgelere eşleyen bir veri yapısı inşa etmek anlamına gelir ve hızlı tam‑metin sorgularını mümkün kılar. GroupDocs.Search ağır işleri soyutlayarak, belgeleri beslemeye ve arama davranışını ayarlamaya odaklanmanızı sağlar.

## Neden GroupDocs.Search for Java Kullanmalı?
- **Ölçeklenebilir ağ mimarisi** – İndeksleme iş yükünü paylaşan birden fazla düğüm dağıtın.  
- **Zengin belge formatı desteği** – PDF'ler, Word, Excel, PowerPoint, görüntüler ve daha fazlası.  
- **Olay‑tabanlı güncellemeler** – Düğüm olaylarına abone olarak indeksi gerçek zamanlı taze tutun.  
- **Basit Maven entegrasyonu** – `pom.xml` dosyasına birkaç satır ekleyin ve indekslemeye başlayın.

## GroupDocs.Search ile gerçek zamanlı indeksleme java
GroupDocs.Search, bir dosya eklendiğinde, güncellendiğinde veya kaldırıldığında olaylar tetikler. Bu olayları işleyerek `addFiles` veya `addDirectories` metodlarını otomatik olarak çağırabilir, indeksin manuel müdahale olmadan senkronize kalmasını sağlayabilirsiniz. Bu yaklaşım, belge yönetim sistemleri, içerik portalları ve verilerin sık sık değiştiği tüm uygulamalar için idealdir.

## Önkoşullar
- **JDK 8+** geliştirme makinenizde kurulu olmalı.  
- **IntelliJ IDEA** veya **Eclipse** gibi bir IDE.  
- **Java** ve **Maven** hakkında temel bilgi.  
- **GroupDocs.Search for Java** kütüphanesine erişim (indirme veya Maven).

## GroupDocs.Search for Java Kurulumu

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

> **Pro ipucu:** Resmi sürüm sayfasını kontrol ederek sürüm numarasını güncel tutun.

JAR dosyasını doğrudan resmi siteden de indirebilirsiniz: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinme
- **Ücretsiz Deneme:** 30‑günlük değerlendirme.  
- **Geçici Lisans:** Uzatılmış test için talep edin.  
- **Satın Alma:** Üretim dağıtımları için gereklidir.

### Temel Başlatma
İndeks dosyalarının saklanacağı bir klasöre işaret eden ve temel iletişim portunu tanımlayan bir yapılandırma nesnesi oluşturun:

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

## GroupDocs.Search ile searchable index java nasıl oluşturulur?
Aşağıda, **add files to search** ve **add directories to node** işlemleri için ihtiyaç duyacağınız temel özellikleri, aynı zamanda ölçeklenebilir bir ağ dağıtarak açıklıyoruz.

### Özellik 1 – Yapılandırma ve Ağ Kurulumu
Arama ağını yapılandırmak, aranabilir bir indeks oluşturmanın ilk adımıdır.

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
- **`basePort`** – Başlangıç portu; her düğüm bu değerden itibaren artar.

### Özellik 2 – Arama Ağ Düğümlerini Dağıtma
Düğümlerin dağıtılması, indeksleme iş yükünü birden fazla makine veya süreç arasında dağıtır.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Her `SearchNetworkNode` kendi indeksleme hizmetini çalıştırır ve yatay olarak ölçeklenen bir **create searchable index java** oluşturmanızı sağlar.

### Özellik 3 – Düğüm Olaylarına Abone Olma
Gerçek zamanlı güncellemeler, indeksi dosya sistemi değişiklikleriyle senkronize tutar.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Olayları dinleyerek yeni dosyalar geldiğinde otomatik olarak yeniden indekslemeyi tetikleyebilirsiniz.

### Özellik 4 – Ağ Düğümüne Dizin Ekleme
Bu yardımcıyı **add directories to node** için kullanın; desteklenen tüm belgeleri yinelemeli olarak toplar.

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

### Özellik 5 – Ağ Düğümüne Dosya Ekleme
İnce ayar kontrolüne ihtiyaç duyduğunuzda, **add files to search** işlemini tek tek yapın:

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

Bu yöntem, akışlardan, bulut depolamadan veya geçici konumlardan gelen dosyaları indeksleme esnekliği sağlar.

## Yaygın Kullanım Senaryoları
- **Kurumsal belge portalları** binlerce PDF ve Office dosyası üzerinde anlık arama ihtiyacı duyan.  
- **Hukuki e‑keşif platformları** yeni kanıtların sürekli eklendiği ve gerçek zamanlı aranabilir olması gereken.  
- **İçerik yönetim sistemleri** görüntüler, sunumlar ve elektronik tablolar depolayan ve tam‑metin arama gerektiren.

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|--------|-----|
| **Arama sonuçlarında belge görünmüyor** | İndeks commit edilmemiş | Dosyalar eklendikten sonra `node.getIndexer().commit()` çağırın. |
| **Port çakışma hatası** | Başka bir hizmet `basePort` kullanıyor | Farklı bir `basePort` seçin veya boş portları kontrol edin. |
| **Desteklenmeyen dosya formatı** | Kütüphanede ayrıştırıcı yok | Dosya uzantısının desteklendiğinden emin olun veya özel bir çıkarıcı ekleyin. |

## Sorun Giderme İpuçları
- **Düğüm sağlığını doğrulayın:** Her düğümün çalıştığını onaylamak için yerleşik sağlık kontrolü uç noktasını (`http://localhost:{port}/health`) kullanın.  
- **Bellek kullanımını izleyin:** Büyük belge topluları bellek kullanımını artırabilir; daha küçük parçalar halinde indekslemeyi ve periyodik olarak `commit()` çağırmayı düşünün.  
- **Kayıtları kontrol edin:** GroupDocs.Search, `basePath` klasörüne ayrıntılı günlükler yazar—parçalama hataları veya ağ zaman aşımı için inceleyin.

## Sıkça Sorulan Sorular

**S: GroupDocs.Search'ü bulut‑tabanlı bir Java uygulamasında kullanabilir miyim?**  
C: Evet. Kütüphane herhangi bir Java çalışma zamanı ile çalışır ve `basePath`'i ağ‑bağlı bir klasöre veya yerel olarak bağlanmış bulut depolamaya yönlendirebilirsiniz.

**S: Bir dosya değiştiğinde indeksi nasıl güncellerim?**  
C: Düğüm olaylarına abone olun (bkz. Özellik 3) ve değiştirilen yollar için `addFiles` veya `addDirectories` tekrar çağırın.

**S: Dağıtabileceğim düğüm sayısında bir sınırlama var mı?**  
C: Pratikte, limit donanımınız ve ağ bant genişliğinizle belirlenir. API'nin kendisi kesin bir üst sınır koymaz.

**S: Yeni dosyalar ekledikten sonra düğümleri yeniden başlatmam gerekir mi?**  
C: Hayır. Dosya eklemek otomatik olarak indekslemeyi tetikler; işlemi ertelediyseniz sadece commit etmeniz gerekir.

**S: Hangi belge formatları kutudan çıkar çıkmaz desteklenir?**  
C: PDF'ler, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML ve birçok görüntü türü. Tam liste için resmi belgelere bakın.

**S: Sürekli dosya yükleyen bir klasör için gerçek zamanlı indeksleme java'yı nasıl etkinleştirebilirim?**  
C: Yeni bir dosya algılandığında `DirectoryAdder.addDirectories(node, path)` çağıran bir dosya sistemi izleyicisi (ör. `java.nio.file.WatchService`) uygulayın.

---

**Son Güncelleme:** 2026-02-27  
**Test Edilen Sürüm:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs