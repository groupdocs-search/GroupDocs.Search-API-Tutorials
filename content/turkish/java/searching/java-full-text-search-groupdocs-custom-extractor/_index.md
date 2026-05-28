---
date: '2026-02-03'
description: GroupDocs.Search kullanarak Java’da tam metin arama için bir log dosyası
  çıkarıcı nasıl oluşturulur öğrenin. Belgeleri indekse ekleyin, arama performansını
  optimize edin ve büyük log dosyalarını verimli bir şekilde yönetin.
keywords:
- full-text search Java GroupDocs
- custom text extractor Java
- GroupDocs.Search indexing
title: 'Java''da Tam Metin Aramayı Ustalaşın: GroupDocs ile Log Dosyası Çıkarıcısı
  Uygulayın'
type: docs
url: /tr/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Java'da Tam Metin Aramayı Öğrenin: Uygulayın

Tam‑metin arama şekilde geri getirmek isteyen uygulamalar için vazgeçilmezdir.landır özel bir çıkarıcı oluşturacağınızı, **belgeleri indekse ekleyeceğinizi** ve **büyük log dosyalarını ararken** arama performansını **optimize edeceğinizi** keşfedeceksiniz.

## Öğrenecekleriniz
- GroupDocs.Search for Java'yı kurma ve yapılandırma.  
- Özelleştirilk.  
- **Log dosyası çıkarıcısının** öne çıktığı gerçek dünya senaryasa log.

## Hızlı Yanıtlar
- **Log dosyası çıkarıcısı nedir? okuyup indeksleyeceğini belirten özel bir bileşen.  
- **Neden GroupDocs.Search kullanılmalı?** Hazır indeksleme, otomatik yeniden indeksleme ve güçlü sorgulama yetenekleri sunar.  
- **eme ya da tam lisans gereklidir.  
- **Diğer dosyakste  
ıları ve otomatik yeniden indeksleme ile bellek kullanımını sınırlayın.

## Ön Koşullar

Uygulamaya başlamadan önce aşağıdakilerin mevcut olduğundan emin olun:

### Gerekli Kütüphaneler
Projenize bağımlılık olarak ekleyerek doğru GroupDocs.Search for Java sürümünü kullandığınızdan emin olun. Maven ile nasıl ayarlanacağını aşağıda bulabilirsiniz:

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

Alternatif olarak, en yeni sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Ortam Kurulumu
- JDK 8 veya üzeri.  
- Java programlama ve dosya işleme kavramlarına aşinalık.

### Lisans Edinme
GroupDocs.Search özelliklerini keşfetmek için ücretsiz bir deneme lisansı indirin. Uzun vadeli kullanım için tam lisans satın almayı ya da [GroupDocs'un web sitesinden](https://purchase.groupdocs.com/temporary-license/) geçici bir lisans talep etmeyi düşünün.

## GroupDocs.Search for Java'ı Kurma

GroupDocs aşağıdaki:

1.ildiği gibi `pom.xml` dosyanıza Maven yapılandırmasını doğru eklediğinizden emin olun.  
2. **Lisans Başlatma**:  
   ```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

KurizBir **log dosyası çıkarıcısı**, GroupDocs.Search'ün ham log dosyalarını (genellikle `.log`) okuyup içeriklerini aranabilir metne dönüştürmesini sağlayan bir kod parçasıdır. Kendi çıkarıcınızı sağlayarak, ayrıştırma kuralları, gürültü filtreleme ve arama senaryonuza uygun yalnızca gerekli bilgileri çıkarma üzerinde tam kontrol elde edersiniz.

## Log Dosyası Çıkarıcısı Oluşturma

GroupDocs.Search, özel metin çıkarıcılarıyla belirli dosya türlerine yönelik indeksler oluşturmanıza izin verir. İşte adım adım kılavuz:

### Adım 1: Özel Çıkarıcıyı Tanımlama
`TextExtractorBase` sınıfını genişılarını bildirir ve çıkarma mantığını içerir.

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

**Önemli noktalar**  
- `getFileExtensions()` GroupDocs.Search'ün için kullanextractText filtreleyebilir veya **büyük log dosyalarını arama** ihtiyacıcıyla İndeks Ayarlarını Yapılandırma
Çıkarıcıyı indeks konfigürasyonuna ekmesi için otomatik‑yeniden‑indekslemeyi etkinleştirin.

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

### Adım 3: Belgeleri İndekse Ekleyin
İndeks artık log dosyalarını nasıl ele alacağını bildiğine göre, **belgeleri indekse ekleyin** diğer dosya türleri gibi.

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

### Adım 4: İndeksi Arayın
Düz metin sorgularıyla arama yapın. Özel çıkarıcı, log içeriğinin aranabilir olmasını sağlar.

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

## Arama Performansını Optimize Etme İpuçları

- **Artımlı İndeksleme** – Tüm klasörü yeniden indekslemek yerine yalnızca yeni ya da değişen log dosyalarını ekleyin.  
- **Bellek Yönetimi** – `autoReindex` bayrağını kullanarak bellek kullanımını düşük tutun.lerini – Devasa log arşivlerinde sonuç kullanın.

## Pratik Uygulamalar

GroupDocs.Search çeşitli senaryolarda kullanılabilir, örneğin:

- **Log Yönetimi** – Gigabaytlarca log verisi içinde hata mesajlarını, kullanıcıli zaman damgalarını hızeleri birik Analizi** – Anahtar edin.

## Performans Düşünceleri

GroupDocs.Search kullanırken şu en iyi uygulamaları aklınızda tutun:

- Daha hızlı okumaumlarını hızlı SSD depolama üzerinde tutun.  
- JVM heap ayrı bir süreçte çalıştırmayı değerlendirin.  
- Otomatik‑yeniden‑indekslemeyi (gösterildiği gibi) etkinleştirerek indeksi manuel müdahale olmadan güncel tutun.

## Sonuç

Artık bir **log dosyası çıkarıcısı** oluşturmuş, **belgeleri indekse eklemeyi** öğrenmiş ve büyük log arşivleri için **arama performansını optimize etme** yollarını keşfetmiş oldunuz. Bu güçlü kombinasyon, Java uygulamalarınızın herhangi bir belge türü üzerinde hızlı ve doğru tam‑metin arama sağlamasını mümkün kılar.

Daha derinlemesine keşif için resmi [GroupDocs documentation](https://docs.groupdocs.com/search/java/) sayfasına göz atın veya benzersiz kullanım senaryonuza uygun farklı çıkarıcı implementasyonlarıyla deneyler yapın.

## SSS Bölümü
1. **GroupDocs.Search ile hangi dosya türlerini indeksleyebilirim?**  
   - PDF, Word belgeleri, elektronik tablolar ve özel formatlar dahil olmak üzere çeşitli dosya türlerini, metin çıkarıcıları aracılığıyla indeksleyebilirsiniz.  
2. **Büyük belge koleksiyonlarını verimli bir şekilde nasıl yönetirim?**  
   - Artımlı güncellemeler veya indeks bölümlendirme gibi uygun indeksleme stratejileri kullanarak kaynakları etkili bir şekilde yönetin.  
3. **GroupDocs.Search başka sistemlerle entegre edilebilir mi?**  
   - Evet, API'ler aracılığıyla mevcut Java uygulamaları ve servislerine entegre edilerek sorunsuz tam‑metin arama yetenekleri sağlar.  
4. **Geçici lisans nedir ve nasıl temin ederim?**  
   - Geçici lisans, değerlendirme amaçlı sınırlama olmadan yazılımı kullanmanıza olanak tanır. [GroupDocs'un web sitesinden](https://purchase.groupdocs.com/temporary-license/) başvurabilirsiniz.

## Sıkça Sorulan Sorular

**S: Log dosyası çıkarıcısı varsayılan çıkarıcıdan nasıl farklıdır?**  
C: Varsayılan çıkarıcı yaygın formatları (PDF, DOCX vb.) işler. Özel bir log dosyası çıkarıcısı, düz‑metin log girişlerinin nasıl ayrıştırılacağını ve indeksleneceğini tam olarak tanımlamanızı sağlar.

**S: Sıkıştırılmış log arşivlerini (ör. .zip) indeksleyebilir miyim?**  
C: Evet, arşivden dosyaları çıkartıp indeksleme işlemine gönderen bir ön‑işleme adımı ekleyerek bunu yapabilirsiniz.

**S: Sürekli üretilen loglarla indeksin güncel kalmasını nasıl sağlamak en iyi yoldur?**  
C: Otomatik‑yeniden‑indekslemeyi etkinleştirin ve log dizinini izleyen bir arka plan işi planlayarak yeni bir dosya ortaya çıktığında `index.add(newLogFile)` çağrısını yapın.

**S: Tek bir log dosyasının indekslenebileceği bir boyut sınırı var mı?**  
C: Pratik olarak sınır, mevcut bellek miktarıyla belirlenir. Çok büyük logları indekslemeden önce daha küçük parçalara bölmek önerilir.

**S: GroupDocs.Search bulanık veya joker karakterli aramaları destekliyor mu?**  
C: Evet, arama API'si bulanık eşleşme, joker karakterler ve yakınlık sorguları gibi seçenekleri içerir ve sonuçların alaka düzeyini artırır.

---

**Son Güncelleme:** 2026-02-03  
**Test Edilen Sürüm:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs