---
date: '2026-01-11'
description: Aspose.OCR ile GroupDocs for Java OCR indekslemesini nasıl kullanacağınızı
  öğrenin; PDF'ler, görüntüler ve taranmış dosyalar arasında güçlü belge arama yeteneklerini
  etkinleştirir.
keywords:
- Java OCR indexing
- document searchability
- OCR with GroupDocs
title: Aspose ile GroupDocs for Java OCR İndeksleme Nasıl Kullanılır
type: docs
url: /tr/java/ocr-image-search/java-ocr-indexing-aspose-groupdocs-search/
weight: 1
---

# Java OCR Dizinlemesi için GroupDocs'i Aspose ile Nasıl Kullanılır

Bu rehberde **GroupDocs'i nasıl kullanacağınızı** keşfedecek ve Java uygulamalarınıza OCR destekli arama ekleyeceksiniz. GroupDocs.Search ile Aspose.OCR'ı birleştirerek, görüntü tabanlı içeriği aranabilir metne dönüştürebilir ve belge yönetim sistemlerini çok daha kullanışlı hâle getirebilirsiniz. Kurulum, indeksleme, arama ve özel OCR entegrasyonu adımlarını, net adım‑adım örneklerle ele alacağız.

## Hızlı Yanıtlar
- **OCR indekslemesini sağlayan kütüphane nedir?** GroupDocs.Search paired with Aspose.OCR.  
- **Hangi Java sürümü gereklidir?** JDK 8 or higher.  
- **Bir lisansa ihtiyacım var mı?** A free trial is available; a paid license is required for production.  
- **Ayrı ve gömülü görüntüleri aynı anda indeksleyebilir miyim?** Yes, enable both options in `IndexingOptions`.  
- **Çoklu iş parçacığı (multi‑threading) destekleniyor mu?** Yes, you can parallelize indexing for large data sets.

## GroupDocs ile OCR İndekslemesi Nedir?
OCR indekslemesi, görüntülerden (taranmış PDF'ler dahil) metin çıkarır ve saklar içinde bir indeks aranabilir. GroupDocs.Search indeksleme ve sorgu yürütmeyi yönetirken, Aspose.OCR gerçek karakter tanıma işlemlerini gerçekleştirir.

## Java OCR indekslemesi için GroupDocs'i neden kullanmalısınız?
- **Yüksek doğruluk** Aspose'un gelişmiş OCR motoru sayesinde.
- **Sorunsuz Java Bağlantısı** Maven veya doğrudan JAR'lar aracılığıyla.
- **Esnek kurulum** ayrı veya gömülü görüntüler için.
- **Ölçeklenebilir performans** çoklu iş parçacığı ve bellek değişiklikleriyle.

## Önkoşullar
- **GrupDocs.Arama**≥25,4
- **Aspose.OCR** ​​(en son sürüm)
- JDK8+ ve bir IDE (IntelliJ, Eclipse, NetBeans)
- Temel Java bilgisi; Maven faydalı ancak zorunlu değil

## GroupDocs.Search'ü Java için Kurma
### Maven'i Kullanmak
`pom.xml` dosyanıza depoyu ve miktarı ekleyin:

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

### Doğrudan İndirme
Alternatif olarak, GroupDocs.Search'ün Java için en son indirmesi [GroupDocs sürümleri](https://releases.groupdocs.com/search/java/) adresinden indirilir.

### Lisans Alma
- **Ücretsiz Deneme** – tüm özellikler ücretsiz kiralama.
- **Geçici Lisans** – uzatılmış test süresi.
- **Satın Alma** – üretim çıktıları için gereklidir.

### Temel Başlatma ve Kurulum
Bir indeks bileşenlerini birleştirin ve `Index` nesnesini başlatın:

```java
import com.groupdocs.search.Index;
// Specify the directory where the index will be stored.
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
// Create an instance of Index class at the specified location.
Index index = new Index(indexFolder);
```

## OCR İndekslemesi için GroupDocs Nasıl Kullanılır
### Dizin Oluşturma
İlk olarak, indeks aralıklarını muhafaza eden birimler ayarlar:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
Index index = new Index(indexFolder);
```

### OCR İndeksleme Seçeneklerinin Ayarlanması
Ayrı ve gömülü görüntüler için OCR'ı etkinleştirin ve özel bir OCR bağlayıcısı ekleyin:

```java
import com.groupdocs.search.options.IndexingOptions;
IndexingOptions options = new IndexingOptions();
options.getOcrIndexingOptions().setEnabledForSeparateImages(true);
options.getOcrIndexingOptions().setEnabledForEmbeddedImages(true);
// Set a custom OCR connector.
options.getOcrIndexingOptions().setOcrConnector(new OcrConnector());
```

### Belgelerin İndekslenmesi
Kaynak belgelerinizi (PDF'ler, Word dosyaları, görüntüler vb.) indeks'e ekleyin:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder, options);
```

### İndekste Arama
İndekslenmiş içerik üzerinde bir arama sorgusu çalıştırın:

```java
import com.groupdocs.search.results.SearchResult;
String query = "water";
SearchResult result = index.search(query);
```

### OCR Bağlayıcısının Uygulanması
Görüntülerden metin tanımak için Aspose.OCR'ı kullanın. Aşağıda gösterildiği gibi `IOcrConnector` arayüzünü uygulayın:

```java
import com.groupdocs.search.options.IOcrConnector;
import com.groupdocs.search.options.OcrContext;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import com.aspose.ocr.AsposeOCR;

public class OcrConnector implements IOcrConnector {
    @Override
    public final String recognize(OcrContext context) {
        if (null == context.getImageLocation()) {
            throw new RuntimeException("The image type is not supported: " + context.getImageLocation());
        }
        
        BufferedImage image = ImageIO.read(context.getImageLocation().toFile());
        AsposeOCR api = new AsposeOCR();
        String text = api.RecognizePage(image);
        return text;
    }
}
```

## Pratik Uygulamalar
1. **Belge Yönetim Sistemleri** – taranmış görüntüleri içeren belgeleri hızlı bir şekilde toplar.
2. **Arşiv Erişimi** – büyük arşivlerde mevcut olanları bulma.
3. **Hukuki Belge Analizi** – taranmış imzalar veya diyagramlar içeren sözleşme ve delilleri arama.
4. **Tıbbi Kayıt Arama** – hasta formları, laboratuvar sonuçları ve röntgen notlarını indeksleme.

## Performans Düşünceleri
- **İndeks Boyutu** – indeksin hafif kalması için dışarıda gereksiz meta verileri bırakın.
- **Çoklu İş Parçacığı** – indekslemeyi hızlandırmak için büyük partileri paralel işleyin.
- **Bellek Yönetimi** – yüksek verimli ekranlarla çalışırken JVM yığınını izleyin.

## Yaygın Sorunlar ve Çözümler
- **Lisans Hataları** – doğru lisans sürümünün sunulduğu çalışma dizinine yerleştirildiğinden emin olun.
- **Eksik Görüntüler** – görüntü yollarının erişilebilir ve erişilebilir formatlarda (PNG, JPEG, BMP) olduğundan emin olun.
- **Bellek Yetersizliği** – JVM yığınını (`-Xmx`) artırın veya belgeleri daha küçük partilerde işleyin.

## Sıkça Sorulan Sorular
**S: GroupDocs.Search ile lisans çözümleri nasıl çözerim?**
**A:** Tam özellikleri açmak için [GroupDocs web ülkesinde](https://purchase.groupdocs.com/temporary-license/) geçici bir lisans belgesidir.

**S: Büyük belge indekslemesini yönetmenin en iyi yolu nedir?**
**A:** Performansı artırma ve bellek baskısını azaltmak için çoklu iş parçacığı ve toplu işleme kullanın.

**S: GroupDocs.Search içinde OCR özelliklerini daha da özelleştirebilir miyim?**
**A:** Evet, `IndexingOptions` OCR davranışını, dil seçimi ve görüntü ön işleme gibi detayları düzenlemenize izin verir.

**S: GroupDocs.Search sırasında yaygın sorunların çözümleri neler oluyor?**
**A:** Dizin yollarını iki kez kontrol edin, tüm ilişkilerin mevcut olup olmadığını doğrulayın ve eksik dosyaları günlük olarak inceleyin.

**S: Aspose.OCR'ı mevcut Java uygulamasına nasıl entegre edebilirim?**
**A:** Yukarıda gösterildiği gibi `IOcrConnector` tanıtımını modüle edin ve görüntü girişini doğru şekilde yaptığınızdan emin olun.

## Kaynaklar
- [GroupDocs.Arama Belgeleri](https://docs.groupdocs.com/search/java/)
- [API Referansı](https://reference.groupdocs.com/search/java/)

---

**Son Güncelleme:** 2026-01-11
**Edilen Sürümünü Test Edin:** GroupDocs.Search 25.4, Aspose.OCR son sürümü
**Yazar:** GroupDocs