---
date: '2026-02-21'
description: GroupDocs.Search kullanarak Java'da yazım düzeltmeyi nasıl etkinleştireceğinizi,
  belgeleri indekse eklemeyi ve daha iyi arama doğruluğu için maksimum hata sayısını
  ayarlamayı öğrenin.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: GroupDocs.Search ile Java’da Yazım Denetimini Nasıl Etkinleştirirsiniz
type: docs
url: /tr/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

Son Güncelleme:"; "Tested With:" => "Test Edilen Versiyon:"; "Author:" => "Yazar:". Keep dates.

Now produce final markdown.

Check for any missed shortcodes: none.

Make sure no extra spaces.

Proceed to final.# Java'da GroupDocs.Search Kullanarak Yazım Denetimini Etkinleştirme

Doğru arama sonuçları, modern bir uygulama için çok önemlidir. Bu öğreticide GroupDocs.Search ile Java'da **yazım denetimini nasıl etkinleştireceğinizi** öğrenecek, böylece kullanıcılar sorguları hatalı yazsa bile doğru sonuçları alacak. Bir indeks oluşturma, **indekse belge ekleme**, yazım seçeneklerini yapılandırma ve hataları otomatik olarak düzelten bir arama yürütme adımlarını göstereceğiz.

## Hızlı Yanıtlar
- **“Yazım denetimini nasıl etkinleştiririz” ne anlama geliyor?** Arama sırasında kullanıcı yazım hatalarını düzelten yerleşik yazım denetleyiciyi etkinleştirir.  
- **Bu özelliği hangi kütüphane sağlar?** Java için GroupDocs.Search.  
- **Lisans gerekir mi?** Değerlendirme için ücretsiz deneme lisansı yeterlidir; üretim için tam lisans gereklidir.  
- **Toleransı kontrol edebilir miyim?** Evet – kaç tane yazım hatasına izin verileceğini tanımlamak için `setMaxMistakeCount` kullanın.  
- **Büyük indeksler için uygun mu?** Kesinlikle – motor yüksek performanslı indeksleme ve arama için optimize edilmiştir.

## GroupDocs.Search'te “yazım denetimini nasıl etkinleştiririz” nedir?
Yazım denetimini etkinleştirmek, sorgu hatalar içerdiğinde arama motorunun en yakın doğru terimleri aramasını sağlar. Bu özellik, yanlış yazılmış girişlerde bile ilgili sonuçlar döndürerek kullanıcı deneyimini büyük ölçüde iyileştirir.

## Java uygulamalarında yazım denetimini neden etkinleştirmelisiniz?
- **Kullanıcı memnuniyetini artırır** – kullanıcıların mükemmel yazması gerekmez.  
- **Hemen çıkma oranlarını azaltır** – daha doğru sonuçlar ziyaretçileri meşgul tutar.  
- **Çeşitli alanlarda çalışır** – kütüphane kataloglarından e‑ticaret ürün aramalarına kadar.

## Önkoşullar
- Java Development Kit (JDK) yüklü.  
- Temel Java ve Maven bilgisi.  
- İndeksleme kavramları hakkında anlayış.  
- GroupDocs.Search deneme veya lisanslı anahtarı.

### Java için GroupDocs.Search Kurulumu
Maven projenize kütüphaneyi entegre edin.

**Maven Kurulumu**  
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

**Doğrudan İndirme**  
Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Lisans Edinme
Değerlendirme için ücretsiz bir deneme lisansı edinin. Üretim kullanımı için tam lisans satın alın veya resmi siteden geçici bir anahtar isteyin.

## İndekse Belgeleri Nasıl Eklenir
İndeks oluşturmak, arama özellikli herhangi bir uygulamanın temelidir. Aşağıda bir klasörden **indekse belge ekleyen** minimal bir örnek bulunmaktadır.

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

*İpucu:* Yolların doğru olduğundan ve uygulamanın indeks klasörüne yazma iznine sahip olduğundan emin olun.

## Yazım Düzeltmeyi Nasıl Yapılandırırsınız (set max mistake count)
Yazım denetleyiciyi etkinleştirerek ve hata toleransını ayarlayarak ince ayar yapabilirsiniz.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

*`setMaxMistakeCount` neden önemlidir:* Motorun kaç tane yazım hatasını tolere edeceğini tanımlar. Bu değeri, alanınızdaki tipik hata kalıplarına göre ayarlayın.

## Yazım Düzeltmeli Arama Nasıl Yapılır
İndeks hazır ve yazım seçenekleri yapılandırıldıktan sonra hatalı olabilecek bir sorgu çalıştırın.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

`search()` çağrısı, düzeltilmiş terimleri ve en ilgili belgeleri içeren bir `SearchResult` döndürür.

## Pratik Uygulamalar
1. **Kütüphane Sistemleri:** Yanlış yazılmış kitap başlıklarını veya yazar adlarını düzeltir.  
2. **E‑ticaret Platformları:** Ürün aramalarındaki kullanıcı hatalarını düzelterek dönüşümleri artırır.  
3. **İçerik Yönetim Sistemleri:** Editör personeli için makale bulmayı iyileştirir.

## Performans Düşünceleri
- **İndeksi güncel tutun** – yeni veya değişen dosyaları düzenli olarak yeniden indeksleyin.  
- **JVM bellek ayarlarını ayarlayın** – büyük indeksler için yeterli yığın tahsis edin.  
- **Kaynak kullanımını izleyin** – gerekirse çöp toplama bayraklarını ayarlayın.

## Yaygın Sorunlar ve Sorun Giderme
| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| Yazım denetimi etkinleştirildikten sonra sonuç gelmiyor | İndeks klasör yolu yanlış veya boş | `indexFolder` geçerli bir indekse işaret ettiğinden ve `index.add()` başarılı olduğundan emin olun |
| Yazım denetleyici belirgin hataları düzeltmiyor | `setMaxMistakeCount` çok düşük ayarlanmış | Daha toleranslı düzeltme için sayıyı 2 veya 3'e artırın |
| Büyük belge setlerinde uygulama çöküyor | Yetersiz JVM yığını | `-Xmx` seçeneğini artırın (ör. `-Xmx4g`) |

## Sıkça Sorulan Sorular

**S: GroupDocs.Search nedir?**  
C: Hızlı indeksleme, gelişmiş arama özellikleri ve yerleşik yazım düzeltmesi sağlayan bir Java kütüphanesidir.

**S: GroupDocs.Search için lisansı nasıl alırım?**  
C: Ücretsiz deneme indirmek veya tam lisans satın almak için resmi siteyi ziyaret edin.

**S: GroupDocs.Search'ı diğer Java çerçeveleriyle entegre edebilir miyim?**  
C: Evet, Spring, Jakarta EE ve herhangi bir standart Java uygulamasıyla çalışır.

**S: İndeks kurarken yaygın sorunlar nelerdir?**  
C: Yanlış klasör yolları, yetersiz dosya izinleri veya `pom.xml` içinde eksik bağımlılıklar.

**S: Yazım düzeltmesi arama sonuçlarını nasıl iyileştirir?**  
C: Yanlış yazılmış sorguları otomatik olarak en yakın doğru terimlere yeniden yazar, daha ilgili sonuçlar döndürür.

## Ek Kaynaklar
- [Dokümantasyon](https://docs.groupdocs.com/search/java/)
- [API Referansı](https://reference.groupdocs.com/search/java)
- [İndirme](https://releases.groupdocs.com/search/java/)
- [GitHub Deposu](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/search/10)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-02-21  
**Test Edilen Versiyon:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs