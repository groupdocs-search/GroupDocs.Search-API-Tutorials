---
date: '2026-08-05'
description: GroupDocs.Search kullanarak Java'da full-text search için bir log file
  extractor oluşturmayı öğrenin. Belgeleri index'e ekleyin, arama performansını optimize
  edin ve büyük log dosyalarını verimli bir şekilde yönetin.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Full text search java tutorial, GroupDocs.Search kullanarak bir custom
  log file extractor oluşturmayı, belgeleri index'e eklemeyi ve massive log archives
  için arama performansını optimise etmeyi gösterir.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Full text search java: log file extractor ile GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Full text search java: log file extractor ile GroupDocs'
type: docs
url: /tr/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Tam metin arama java: GroupDocs ile günlük dosyası çıkarıcı

Full‑text search java, büyük belge koleksiyonları içinde bilgiyi hızlıca bulması gereken her sistem için temel bir bileşendir. Bu öğreticide GroupDocs.Search'ı nasıl yapılandıracağınızı, özel bir günlük dosyası çıkarıcı oluşturacağınızı, belgeleri indekse ekleyeceğinizi ve gigabaytlarca günlük verisiyle çalışırken arama performansını nasıl optimize edeceğinizi öğreneceksiniz.

## Öğrenecekleriniz
- GroupDocs.Search for Java'yı kurun ve yapılandırın.  
- İhtiyacınıza göre düz metin günlüklerini ayrıştıran bir **log file extractor** uygulayın.  
- PDF'ler, DOCX ve diğer formatların yanı sıra **belgeleri indekse ekleyin**.  
- Gerçek dünya senaryoları, bir **log file extractor**'ın ölçülebilir değer kattığı durumlar.  
- Çok gigabaytlık günlük arşivleri için **optimise search performance** konusunda kanıtlanmış ipuçları.

## Hızlı cevaplar
- **Log file extractor nedir?** GroupDocs.Search'a düz metin günlük dosyalarını nasıl okuyup indeksleyeceğini söyleyen özel bir bileşen.  
- **Neden GroupDocs.Search kullanmalı?** 50+ formatın indekslenmesini destekler, otomatik yeniden indeksleme sağlar ve 2 GB RAM altında 10 GB'a kadar indeksleri yönetir.  
- **Lisans gerekir mi?** Evet – kütüphaneyi etkinleştirmek için bir deneme veya tam lisans gereklidir.  
- **Diğer dosya türlerini aynı anda indeksleyebilir miyim?** Kesinlikle; aynı indeks içinde PDF'leri, DOCX'i ve özel günlük dosyalarını karıştırabilirsiniz.  
- **Performansı nasıl artırabilirim?** Artımlı indeksleme kullanın, `IndexSettings`'i ayarlayın ve `autoReindex` bayrağını etkinleştirin.

## Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

### Gerekli kütüphaneler
`pom.xml` dosyanıza GroupDocs.Search Maven bağımlılığını ekleyin. Projenizin Java seviyesine uygun en son sürümü kullanın.

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

Alternatif olarak, en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Ortam kurulumu
- JDK 8 veya üzeri.  
- Java programlaması ve temel dosya işleme kavramlarına aşinalık.

### Lisans edinimi
GroupDocs.Search özelliklerini keşfetmek için önce ücretsiz bir deneme lisansı indirin. Üretim kullanımı için tam bir lisans satın alın veya [GroupDocs'un web sitesinden](https://purchase.groupdocs.com/temporary-license/) geçici bir lisans isteyin.

## GroupDocs.Search for Java'ı Kurma

Başlamak için kütüphaneyi başlatın ve lisans dosyanızı uygulayın:

1. **Maven kurulumu** – önceki adımdaki bağımlılığın mevcut olduğunu doğrulayın.  
2. **Lisans başlatma** – diğer API çağrılarından önce lisans dosyasını yükleyin.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

Ortam hazır olduğunda, özel **log file extractor**'ı oluşturmaya geçebilirsiniz.

## Log file extractor nedir?

Log file extractor, GroupDocs.Search'a ham günlük dosyalarını (genellikle `.log`) nasıl okuyacağını ve içeriklerini aranabilir metne dönüştüreceğini söyleyen bir kod parçasıdır. Kendi çıkarıcınızı sağlayarak ayrıştırma kuralları, gürültü filtreleme ve arama senaryonuz için önemli olan bilgileri çıkarmak üzerinde tam kontrol elde edersiniz.

## Log file extractor oluşturma

GroupDocs.Search, herhangi bir dosya türü için özel metin çıkarıcıları eklemenize olanak tanır. Günlük dosyaları için bir tane oluşturmak için aşağıdaki adımları izleyin.

### Adım 1: özel çıkarıcıyı tanımlayın
`TextExtractorBase`, özel bir çıkarıcı oluşturmak için genişlettiğiniz soyut temel sınıftır. Çıkarıcının desteklediği dosya uzantılarını bildirir ve temel çıkarma mantığını içerir.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Anahtar noktalar**  
- `getFileExtensions()` çıkarıcıyı `.log` dosyaları için kaydeder.  
- `extractText` zaman damgalarını kaldırabileceğiniz, hata ayıklama satırlarını filtreleyebileceğiniz veya **search large log files** için gerekli ön işleme uygulayabileceğiniz yerdir.

### Adım 2: çıkarıcıyla indeks ayarlarını yapılandırın
Çıkarıcınızı `IndexSettings`'e ekleyin ve `autoReindex`'i etkinleştirin, böylece yeni günlükler manuel müdahale olmadan otomatik olarak indekslenir.

`IndexSettings`, bellek limitleri ve özel çıkarıcılar gibi indeks davranışını yapılandırır.  
`autoReindex`, kaynak dosyalar değiştiğinde indeksi otomatik olarak günceller.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### Adım 3: belgeleri indekse ekleyin
Artık indeks günlük dosyalarını tanıdığından, **add documents to index** işlemini diğer desteklenen formatlar gibi gerçekleştirebilirsiniz.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### Adım 4: indeksi arayın
Düz metin sorguları yapın. Özel çıkarıcı, her günlük kaydının aranabilir olmasını garanti eder.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Arama performansını optimize etme ipuçları

- **Incremental indexing** – tüm indeksi yeniden oluşturmak yerine yalnızca yeni veya değişen günlük dosyalarını ekleyin.  
- **Memory management** – `autoReindex` bayrağı, ara verileri diske yazarak RAM kullanımını düşük tutar.  
- **Index settings** – `setMaxMemoryUsage`'i sunucunuzun kapasitesine göre ayarlayın; tipik bir ayar 10 GB indeks için 1 GB'dir.  
- **Query optimisation** – büyük günlük arşivlerinde arama yaparken sonuçları daraltmak için ifade sorguları, joker karakterler veya filtreler kullanın.

## Pratik uygulamalar

GroupDocs.Search birçok gerçek dünya senaryosunda uygulanabilir, örneğin:

- **Log management** – gigabaytlarca günlük verisi içinde saniyeler içinde hata mesajlarını, kullanıcı eylemlerini veya belirli zaman damgalarını bulun.  
- **Document retrieval systems** – PDF'ler, Word belgeleri, elektronik tablolar ve özel günlük dosyalarını içeren tek bir aranabilir depo tutun.  
- **Content analysis** – anahtar kelime sıklığı raporları çalıştırın veya akış halindeki günlük verilerinde anormallikleri tespit edin.

## Performans değerlendirmeleri

GroupDocs.Search'ı ölçekli bir şekilde dağıtırken aşağıdaki en iyi uygulamaları aklınızda tutun:

- İndeksleri hızlı SSD'lerde depolayarak okuma/yazma gecikmesini en aza indirin.  
- JVM yığın kullanımını izleyin; bellek darboğazı oluşturursa büyük indeksleri ayrı bir sürece aktarmayı düşünün.  
- `autoReindex`'i (gösterildiği gibi) etkinleştirerek indeksi manuel yeniden oluşturma olmadan güncel tutun.

## Sonuç

Şimdiye kadar bir **log file extractor** oluşturmuş, **add documents to index** nasıl yapılacağını öğrenmiş ve büyük günlük arşivleri için **optimise search performance** yollarını keşfetmiş oldunuz. Bu kombinasyon, Java uygulamalarınızın herhangi bir belge türü üzerinde hızlı ve doğru tam metin arama sağlamasına olanak tanır.

Daha derin bir keşif için resmi [GroupDocs documentation](https://docs.groupdocs.com/search/java/) adresine bakın veya benzersiz kullanım durumunuza uygun farklı çıkarıcı uygulamalarıyla deney yapın.

## SSS bölümü
1. **GroupDocs.Search ile hangi dosya türlerini indeksleyebilirim?**  
   - PDF'ler, Word belgeleri, elektronik tablolar ve birçok diğer formatı, ayrıca metin çıkarıcılarıyla özel günlük dosyalarını indeksleyebilirsiniz.  
2. **Büyük belge koleksiyonlarını verimli bir şekilde nasıl yönetirim?**  
   - Artımlı güncellemeler kullanın, indeksleri bölümlere ayırın ve `IndexSettings`'i kaynakları etkili yönetmek için ayarlayın.  
3. **GroupDocs.Search başka sistemlerle entegre edilebilir mi?**  
   - Evet, mevcut hizmetlere, mikro‑servislere veya web uygulamalarına gömülebilen temiz bir Java API'si sunar.  
4. **Geçici lisans nedir ve nasıl temin ederim?**  
   - Geçici lisans, süresiz değerlendirme için tam işlevsellik sağlar. [GroupDocs'un web sitesinden](https://purchase.groupdocs.com/temporary-license/) başvurun.

## Sıkça Sorulan Sorular

**S: Log file extractor varsayılan çıkarıcıdan nasıl farklıdır?**  
C: Varsayılan çıkarıcı yaygın formatları (PDF, DOCX, vb.) işler. Özel bir log file extractor, düz metin günlük girişlerinin nasıl ayrıştırılacağını ve indeksleneceğini tam olarak tanımlamanıza olanak tanır.

**S: Sıkıştırılmış günlük arşivlerini (ör. .zip) indeksleyebilir miyim?**  
C: Evet, arşivden dosyaları çıkartan bir ön‑işleme adımı ekleyerek indekslemeden önce besleyebilirsiniz.

**S: Sürekli üretilen günlüklerle indeksin güncel kalmasını sağlamak için en iyi yol nedir?**  
C: `autoReindex`'i etkinleştirin ve yeni bir dosya ortaya çıktığında `index.add(newLogFile)` çağıran bir arka plan izleyicisi zamanlayın.

**S: İndekslenebilecek tek bir günlük dosyasının boyutu için bir limit var mı?**  
C: Pratikte, limit mevcut bellekle sınırlıdır. Çok büyük günlükleri indekslemeden önce daha küçük parçalara bölmek önerilir.

**S: GroupDocs.Search bulanık veya joker karakter aramaları destekliyor mu?**  
C: Evet, arama API'si sonuç alaka düzeyini artırmak için bulanık eşleşme, joker karakterler ve yakınlık sorgularını içerir.

**Son Güncelleme:** 2026-08-05  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [Java Tam Metin Arama: GroupDocs.Search ile İndeks Oluşturma](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [GroupDocs.Search for Java ile Belgeleri İndekse Ekleme](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [GroupDocs.Search Java ile Sorgu Performansını İyileştirme: İndeksi ve Aramayı Optimize Etme](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)