---
date: '2025-12-26'
description: GroupDocs.Search for Java ile aranabilir bir indeks oluşturmayı, arama
  için dosyalar eklemeyi ve düğüme dizinler eklemeyi öğrenin.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Aranabilir Dizin Oluşturma Java – GroupDocs.Search for Java'ı Dağıt
type: docs
url: /tr/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Java’da Aranabilir İndeks Oluşturma – GroupDocs.Search for Java’yı Dağıtma

Günümüz veri odaklı dünyasında, **creating a searchable index java** uygulamaları büyük belge koleksiyonlarını verimli bir şekilde işlemek zorundadır. İster kurumsal düzeyde bir arama hizmeti, ister daha küçük bir proje inşa ediyor olun, iyi yapılandırılmış bir arama ağı, geri getirme hızını ve alaka düzeyini büyük ölçüde artırabilir. Bu rehberde **GroupDocs.Search for Java** kurulum sürecinin tamamını, aramaya dosya eklemekten düğüme dizin eklemeye kadar adım adım göstereceğiz, böylece belgelerinizi hemen indekslemeye başlayabilirsiniz.

## Hızlı Yanıtlar
- **GroupDocs.Search'ün temel amacı nedir?** Dağıtık bir ağda belgeleri indekslemek ve aramak için ölçeklenebilir, Java‑tabanlı bir motor sağlar.  
- **Hangi sürümü kullanmalıyım?** En son kararlı sürüm (ör. 25.4) yeni projeler için önerilir.  
- **Bir lisansa ihtiyacım var mı?** 30 günlük ücretsiz deneme mevcuttur; üretim kullanımı için kalıcı bir lisans gereklidir.  
- **Hem dosyaları hem de tüm dizinleri ekleyebilir miyim?** Evet – içeriği almak için `addFiles` ve `addDirectories` yardımcılarını kullanın.  
- **Hangi Java sürümü gereklidir?** Bağımlılık yönetimi için Maven ile Java 8 veya üzeri.

## “create searchable index java” nedir?
Java’da aranabilir bir indeks oluşturmak, terimleri içeren belgelere eşleyen bir veri yapısı inşa etmek anlamına gelir ve hızlı tam metin sorgularını mümkün kılar. GroupDocs.Search ağır işleri soyutlayarak, belgeleri beslemeye ve arama davranışını ayarlamaya odaklanmanızı sağlar.

## Neden GroupDocs.Search for Java Kullanmalı?
- **Scalable network architecture** – İndeksleme iş yükünü paylaşan birden fazla düğüm dağıtın.  
- **Rich document format support** – PDF'ler, Word, Excel, PowerPoint, görüntüler ve daha fazlası.  
- **Event‑driven updates** – Düğüm olaylarına abone olarak indeksi gerçek zamanlı taze tutun.  
- **Simple Maven integration** – `pom.xml` dosyasına birkaç satır ekleyin ve indekslemeye başlayın.

## Önkoşullar
- **JDK 8+** geliştirme makinenize kurulu.  
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

> **Pro tip:** Resmi sürüm sayfasını kontrol ederek sürüm numarasını güncel tutun.

JAR dosyasını doğrudan resmi siteden de indirebilirsiniz: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinimi
- **Free Trial:** 30 günlük değerlendirme.  
- **Temporary License:** Uzun süreli test için isteyin.  
- **Purchase:** Üretim dağıtımları için gereklidir.

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
Aşağıda, **add files to search** ve **add directories to node** için ihtiyaç duyacağınız temel özellikleri, aynı zamanda ölçeklenebilir bir ağ dağıtarak açıklıyoruz.

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

- **`basePath`** – İndeks verilerinin kalıcı olarak saklanacağı dizin.  
- **`basePort`** – Başlangıç portu; her düğüm bu değerden artar.

### Özellik 2 – Arama Ağı Düğümlerinin Dağıtılması
Düğümleri dağıtmak, indeksleme iş yükünü birden fazla makine veya süreç arasında dağıtır.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Her `SearchNetworkNode` kendi indeksleme hizmetini çalıştırır ve yatay olarak ölçeklenen bir **create searchable index java** oluşturmanıza olanak tanır.

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

Olayları dinleyerek, yeni dosyalar geldiğinde otomatik olarak yeniden indekslemeyi tetikleyebilirsiniz.

### Özellik 4 – Ağ Düğümüne Dizin Ekleme
Bu yardımcıyı **add directories to node** için kullanın, desteklenen tüm belgeleri özyinelemeli olarak toplayın.

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
İnce ayar kontrolüne ihtiyacınız olduğunda, **add files to search** tek tek ekleyin:

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

## Yaygın Sorunlar ve Çözümler
| Sorun | Sebep | Çözüm |
|-------|--------|-----|
| **Arama sonuçlarında belge görünmüyor** | İndeks taahhüt edilmedi | `node.getIndexer().commit()` metodunu dosyalar eklendikten sonra çağırın. |
| **Port çakışma hatası** | `basePort`'u başka bir hizmet kullanıyor | Farklı bir `basePort` seçin veya boş portları doğrulayın. |
| **Desteklenmeyen dosya formatı** | Kütüphane ayrıştırıcıya sahip değil | Dosya uzantısının desteklendiğinden emin olun veya özel bir çıkarıcı ekleyin. |

## Sıkça Sorulan Sorular

**S: GroupDocs.Search'ü bulut‑tabanlı bir Java uygulamasında kullanabilir miyim?**  
C: Evet. Kütüphane herhangi bir Java çalışma zamanı ile çalışır ve `basePath`'i ağ‑bağlı bir klasöre veya yerel olarak bağlanmış bulut depolamaya yönlendirebilirsiniz.

**S: Bir dosya değiştiğinde indeksi nasıl güncellerim?**  
C: Düğüm olaylarına abone olun (bkz. Özellik 3) ve değiştirilmiş yollar için `addFiles` veya `addDirectories` metodunu tekrar çağırın.

**S: Dağıtabileceğim düğüm sayısına bir sınırlama var mı?**  
C: Pratikte, sınır donanımınız ve ağ bant genişliğinizle belirlenir. API'nin kendisi kesin bir üst sınır koymaz.

**S: Yeni dosyalar ekledikten sonra düğümleri yeniden başlatmam gerekiyor mu?**  
C: Hayır. Dosya eklemek indekslemeyi otomatik tetikler; işlemi ertelediyseniz sadece taahhüt etmeniz gerekir.

**S: Hangi belge formatları kutudan çıkar çıkmaz desteklenir?**  
C: PDF'ler, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML ve birçok görüntü türü. Tam liste için resmi belgelere bakın.

---

**Son Güncelleme:** 2025-12-26  
**Test Edilen Sürüm:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs