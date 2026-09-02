---
date: '2026-09-02'
description: GroupDocs.Search kullanarak search index java oluşturmayı ve yazım düzeltmesini
  etkinleştirmeyi öğrenin. Belgeleri eklemek, max mistake count yapılandırmak ve arama
  doğruluğunu artırmak için adım adım talimatları izleyin.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: GroupDocs.Search kullanarak search index java oluşturmayı ve yazım
  düzeltmesini etkinleştirmeyi öğrenin. Belgeleri eklemek, max mistake count yapılandırmak
  ve arama doğruluğunu artırmak için adım adım talimatları izleyin.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: search index java oluşturma ve yazım denetimini etkinleştirme
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: search index java oluşturma ve yazım denetimini etkinleştirme
type: docs
url: /tr/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Java’da arama dizini oluşturma ve yazım denetimini etkinleştirme

Modern Java uygulamalarında doğru arama sonuçları sunmak vazgeçilmez bir özelliktir. Bu öğreticide **how to create search index java** ve GroupDocs.Search ile yazım düzeltmeyi nasıl etkinleştireceğinizi gösteriyoruz; böylece kullanıcılar sorgularını yanlış yazsalar bile ilgili sonuçları alır. Kütüphaneyi nasıl kuracağınızı, belgeleri nasıl ekleyeceğinizi, maksimum hata sayısını nasıl yapılandıracağınızı ve yazım hatalarına toleranslı bir arama nasıl yapacağınızı göreceksiniz — ekstra bir konfigürasyon kodu satırı yazmadan.

## Hızlı Yanıtlar
- **“enable spelling” ne yapar?** Arama sırasında yanlış yazılmış terimleri en yakın doğru formlara yeniden yazarak yerleşik yazım denetleyiciyi etkinleştirir.  
- **Bu özelliği hangi kütüphane sağlar?** GroupDocs.Search for Java.  
- **Bir lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme çalışır; üretim kullanımı için tam lisans gereklidir.  
- **Toleransı kontrol edebilir miyim?** Evet – sorgu başına kaç yazım hatasına izin verileceğini tanımlamak için `setMaxMistakeCount` kullanın.  
- **Büyük dizinler için uygun mu?** Kesinlikle – motor, tipik sunucu donanımında sorgu gecikmesini 100 ms’nin altında tutarak milyonlarca kayıttan oluşan dizinleri yönetir.

## GroupDocs.Search Nedir?
GroupDocs.Search, yerleşik yazım düzeltme dahil hızlı tam metin indeksleme ve gelişmiş arama özellikleri sunan bir Java kütüphanesidir. 50’den fazla giriş formatını destekler ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri işleyebilir.

## Java uygulamalarında yazım düzeltmeyi neden etkinleştirmelisiniz?
- **Kullanıcı memnuniyetini artırır** – ziyaretçiler eksik yazım olsa bile doğru sonuçlar alır.  
- **Hemen çıkma oranlarını azaltır** – doğru sonuçlar kullanıcıların daha uzun süre etkileşimde kalmasını sağlar.  
- **Çeşitli alanlarda çalışır** – kütüphane kataloglarından e-ticaret ürün aramalarına kadar, yazım düzeltme her yerde alaka düzeyini artırır.

## Önkoşullar
- Java Development Kit (JDK) yüklü.  
- Temel Java ve Maven bilgisi.  
- İndeksleme kavramları hakkında anlayış.  
- Bir GroupDocs.Search deneme veya lisans anahtarı.

### GroupDocs.Search for Java Kurulumu
Kütüphaneyi Maven projenize entegre edin.

**Maven kurulumu**  
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

**Doğrudan indirme**  
Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Lisans edinme
Değerlendirme için ücretsiz deneme lisansı alın. Üretim kullanımı için tam lisans satın alın veya resmi siteden geçici bir anahtar talep edin.

## Java’da bir arama dizini nasıl oluşturulur?
`SearchIndex`, diskte depolanan aranabilir bir dizini temsil eden birincil sınıftır.  
Diskte bir klasöre işaret eden bir `SearchIndex` örneği oluşturun, ardından kaynak dizinden belgeleri ekleyin. Motor, hızlı aramaları sağlayan ters bir indeks oluşturur. Her dosya için `index.add()` çağırabilirsiniz; kütüphane dosya türüne göre metni otomatik olarak çıkarır.

## Yazım düzeltmeyi nasıl etkinleştiririm?
`getSpellingOptions()` indeks için yazım yapılandırma nesnesini döndürür ve yazım denetimi özelliklerini etkinleştirmenize veya ayarlamanıza olanak tanır.  
Yazım denetimini etkinleştirmek için `index.getSpellingOptions().setEnabled(true)` çağırın. Bu, motorun sorgu terimlerini analiz etmesini ve uyumsuzluk tespit edildiğinde düzeltilmiş alternatifler önermesini sağlar. Özellik, kütüphanenin desteklediği tüm indekslenmiş diller için kutudan çıkar çıkmaz çalışır.

## max mistake count ayarı nedir?
`setMaxMistakeCount`, yazım denetleyicisinin bir terim başına tolerans göstereceği maksimum karakter düzenlemesini yapılandırır.  
`setMaxMistakeCount(int)`, bir terim başına tolerans gösterecek maksimum karakter düzenlemesini (eklemeler, silmeler, değişiklikler) tanımlar. **2** olarak ayarlamak, motorun yaygın iki karakterli yazım hatalarını düzeltmesine izin verirken, alakasız sonuçlar döndürebilecek aşırı agresif düzeltmelerden kaçınır.

## Yazım‑düzeltmeli bir arama nasıl yapılır
`search()` indeks üzerinde bir sorgu çalıştırır ve eşleşmeleri ile düzeltilmiş terimleri içeren bir `SearchResult` nesnesi döndürür.  
`search()` metodunu kullanarak bir arama sorgusu çalıştırın. Sorgu yanlış yazılmış kelimeler içeriyorsa, motor düzeltilmiş terimleri ve en ilgili belgelerin bir listesini içeren bir `SearchResult` döndürür. Kullanıcıya şeffaflık sağlamak için hem orijinal sorguyu hem de düzeltilmiş versiyonu gösterebilirsiniz.  
`SearchResult`, eşleşen belgelerin listesini ve sorgu düzeltmeleri hakkında bilgileri tutar.

## Pratik uygulamalar
1. **Kütüphane sistemleri** – yanlış yazılmış kitap başlıklarını veya yazar adlarını otomatik olarak düzeltir.  
2. **E‑ticaret platformları** – dönüşüm oranlarını artırmak için ürün adı yazım hatalarını düzeltir.  
3. **İçerik yönetimi** – editörlerin eksik anahtar kelimelerle bile makaleleri bulmasına yardımcı olur.

## Performans değerlendirmeleri
- **İndeksi güncel tutun** – yeni veya değişen dosyaları düzenli olarak yeniden indeksleyin.  
- **JVM bellek ayarlarını ayarlayın** – büyük indeksler için yeterli yığın ayırın (ör. `-Xmx4g`).  
- **Kaynak kullanımını izleyin** – toplu indeksleme sırasında duraklamalar fark ederseniz çöp toplama bayraklarını ayarlayın.

## Yaygın sorunlar ve sorun giderme
| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|------|
| Yazım denetimi etkinleştirildikten sonra sonuç gelmiyor | İndeks klasör yolu yanlış veya boş | `indexFolder`'ın geçerli bir indekse işaret ettiğini ve `index.add()`'ın başarılı olduğunu doğrulayın |
| Yazım denetleyicisi bariz hataları düzeltmiyor | `setMaxMistakeCount` çok düşük ayarlanmış | Daha toleranslı düzeltme için sayıyı 2 veya 3 olarak artırın |
| Uygulama büyük belge setlerinde çöküyor | Yetersiz JVM yığını | `-Xmx` seçeneğini artırın (ör. `-Xmx4g`) |

## Sıkça Sorulan Sorular

**S: GroupDocs.Search nedir?**  
**C:** GroupDocs.Search, hızlı indeksleme, gelişmiş sorgu yetenekleri ve herhangi bir Java uygulaması için yerleşik yazım düzeltme sağlayan bir Java kütüphanesidir.

**S: GroupDocs.Search için lisansı nasıl elde ederim?**  
**C:** Resmi siteyi ziyaret ederek ücretsiz deneme indirebilir veya tam lisans satın alabilirsiniz; kısa vadeli test için geçici bir anahtar da mevcuttur.

**S: GroupDocs.Search'i diğer Java çerçeveleriyle entegre edebilir miyim?**  
**C:** Evet, Spring, Jakarta EE ve herhangi bir standart Java uygulamasıyla sorunsuz çalışır.

**S: Bir indeks kurarken yaygın sorunlar nelerdir?**  
**C:** Yanlış klasör yolları, eksik dosya izinleri veya eksik Maven bağımlılıkları tipik sorunlardır.

**S: Yazım düzeltme arama sonuçlarını nasıl iyileştirir?**  
**C:** Yanlış yazılmış sorguları otomatik olarak en yakın doğru terimlere yeniden yazar, daha ilgili sonuçlar döndürür ve kullanıcı hayal kırıklığını azaltır.

## Ek kaynaklar
- [Dokümantasyon](https://docs.groupdocs.com/search/java/)
- [API Referansı](https://reference.groupdocs.com/search/java)
- [İndirme](https://releases.groupdocs.com/search/java/)
- [GitHub Deposu](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/search/10)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-09-02  
**Test Edilen Versiyon:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs

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

## İlgili Öğreticiler

- [Java için GroupDocs.Search API'si Kullanarak Belge İndeksi Oluşturma ve Belge Ekleme](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Java Dil İşleme – GroupDocs.Search ile Eş Anlamlı Sözlük Oluşturma](/search/java/dictionaries-language-processing/)
- [Aramada Durdurma Kelimeleri: GroupDocs.Search Java ile Dizin'e Belge Ekleme](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)