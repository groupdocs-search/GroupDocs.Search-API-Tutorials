---
date: '2025-12-16'
description: GroupDocs.Search for Java kullanarak tarih aralığı araması ve faceted
  search gibi diğer gelişmiş arama özelliklerini, hata yönetimi ve performans optimizasyonu
  dahil olmak üzere nasıl gerçekleştireceğinizi öğrenin.
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: 'GroupDocs.Search Java: Tarih Aralığı Araması ve Gelişmiş Özellikler'
type: docs
url: /tr/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

# GroupDocs.Search Java'ı Ustalıkla Kullanma: Tarih Aralığı Araması ve Gelişmiş Özellikler

Bugünün veri odaklı uygulamalarında **date range search**, belgeleri zaman dilimlerine göre filtrelemenizi sağlayan temel bir yetenektir ve alaka düzeyini ve hızı büyük ölçüde artırır. Uyumluluk portalı, e‑ticaret kataloğu veya içerik yönetim sistemi geliştiriyor olun, tarih aralığı aramasını diğer güçlü sorgu türleriyle birlikte ustalaşmak, çözümünüzü hem esnek hem de sağlam kılar. Bu kılavuz, hata yönetimini, tam sorgu türleri yelpazesini ve performans ipuçlarını, kopyalayıp yapıştırabileceğiniz gerçek Java kodlarıyla birlikte adım adım gösterir.

## Hızlı Yanıtlar
- **Tarih aralığı araması nedir?** Belirli bir başlangıç‑bitiş aralığı içinde yer alan tarihleri içeren belgeleri filtreleme.  
- **Hangi kütüphane bunu sağlar?** GroupDocs.Search for Java.  
- **Lisans gerekir mi?** Geliştirme için ücretsiz deneme çalışır; ticari kullanım için bir üretim lisansı gereklidir.  
- **Diğer sorgularla birleştirilebilir mi?** Evet—tarih aralıklarını boolean, faceted veya regex sorgularıyla karıştırabilirsiniz.  
- **Büyük veri setlerinde hızlı mı?** Doğru indekslendiğinde, aramalar milyonlarca kayıt üzerinde bile saniyenin altında sürede çalışır.

## Tarih aralığı araması nedir?
Date range search, “2023‑01‑01 ~~ 2023‑12‑31” gibi iki sınır arasında kalan tarihleri içeren belgeleri bulmanızı sağlar. Raporlar, denetim günlükleri ve zaman‑temelli filtrelemenin önemli olduğu her senaryo için vazgeçilmezdir.

## Neden GroupDocs.Search for Java kullanmalı?
GroupDocs.Search, basit, wildcard, faceted, numeric, date range, regex, boolean ve phrase gibi birçok sorgu türü için birleşik bir API sunar—bu sayede birden fazla kütüphane ile uğraşmadan gelişmiş arama deneyimleri oluşturabilirsiniz. Olay‑tabanlı hata yönetimi ise indeksleme hattınızı dayanıklı tutar.

## Önkoşullar
- **GroupDocs.Search Java library** (v25.4 veya daha yeni).  
- **Java Development Kit (JDK)** projenizle uyumlu.  
- Bağımlılık yönetimi için Maven (veya manuel indirme).  

### Gerekli Kütüphaneler ve Ortam Kurulumu
`pom.xml` dosyanıza GroupDocs deposunu ve bağımlılığı ekleyin:

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

### Alternatif Kurulum
Doğrudan indirmeler için [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresini ziyaret edin.

### Lisanslama ve İlk Kurulum
Ücretsiz deneme veya geçici bir lisansla başlayın:

- Detaylar için [GroupDocs License Options](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin.

Şimdi aranabilir verilerinizi tutacak indeks klasörünü oluşturalım.

## GroupDocs.Search for Java'yı Kurma

### Temel Başlatma
Diskte bir klasöre işaret eden bir `Index` nesnesi oluşturun:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

Artık tüm arama işlemlerine bir geçiş noktanız var.

## Uygulama Kılavuzu

### Özellik 1: İndekslemede Hata Yönetimi
#### İndeksleme hatalarını nasıl yakalarım (Java)

```java
import com.groupdocs.search.events.*;

index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
    @Override
    public void invoke(Object sender, IndexErrorEventArgs args) {
        System.out.println(args.getMessage()); // Output the error message
    }
});

// Add documents to the index
index.add("YOUR_DOCUMENT_DIRECTORY");
```

*Önemi*: `ErrorOccurred` olayını dinleyerek sorunları kaydedebilir, başarısız dosyaları yeniden deneyebilir veya tüm süreci çökertmeden kullanıcıları uyarabilirsiniz.

### Özellik 2: Basit Arama Sorgusu
#### Basit arama nedir?

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*Sonuç*: **volutpat** terimini içeren her belgeyi döndürür.

### Özellik 3: Wildcard Arama Sorgusu
#### Wildcard arama nasıl çalışır?

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*Sonuç*: **affect** ve **effect** kelimelerini eşleştirir, `?` yer tutucusunun gücünü gösterir.

### Özellik 4: Faceted Arama Sorgusu
#### Faceted arama Java nasıl yapılır?

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*Sonuç*: **Content** alanına sınırlama getirir; kategori veya yazar gibi meta verilerle filtreleme için idealdir.

### Özellik 5: Sayısal Aralık Arama Sorgusu
#### Sayısal aralıklar nasıl aranır?

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*Sonuç*: Sayısal değerlerin 2000 ile 3000 arasında olduğu belgeleri getirir.

### Özellik 6: Tarih Aralığı Arama Sorgusu
#### Tarih aralığı araması nasıl yürütülür?

```java
import com.groupdocs.search.options.*;
import java.util.*;

String query = "daterange(2000-01-01 ~~ 2001-06-15)";
SearchOptions options = new SearchOptions();

options.getDateFormats().clear();
DateFormatElement[] elements = {
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

SearchResult result = index.search(query, options);
```

*Açıklama*: `SearchOptions` özelleştirilerek motorun **MM/DD/YYYY** formatındaki tarihleri tanıması sağlanır, ardından 1 Ocak 2000 ile 15 Haziran 2001 arasındaki tüm kayıtlar alınır.

### Özellik 7: Düzenli İfade Arama Sorgusu
#### Regex arama Java nasıl çalıştırılır?

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*Sonuç*: Üç veya daha fazla aynı karakterden oluşan dizileri bulur (ör. “aaa”, “111”).

### Özellik 8: Boolean Arama Sorgusu
#### Boolean arama Java ile koşullar nasıl birleştirilir?

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*Sonuç*: **justo** içeren belgeleri döndürür ancak aynı zamanda **3456** içerenleri hariç tutar.

### Özellik 9: Karmaşık Boolean Arama Sorgusu
#### Gelişmiş boolean sorguları nasıl hazırlanır?

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*Sonuç*: “English” benzeri dosya adlarını (1‑3 karakter varyasyonuna izin vererek) **veya** hem **3456** hem **consequat** içeren içerikleri arar.

### Özellik 10: Phrase Arama Sorgusu
#### Tam ifadeler nasıl aranır?

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*Sonuç*: **ipsum dolor sit amet** tam ifadesini içeren belgeleri getirir.

## Pratik Uygulamalar
1. **E‑commerce Platforms** – Faceted search Java’yı kullanarak ürünleri beden, renk ve marka göre filtreleyin.  
2. **Content Management Systems** – Boolean search Java’yı phrase search ile birleştirerek gelişmiş editöryal araçlar sağlayın.  
3. **Data Analysis Tools** – Tarih aralığı aramasını kullanarak zaman‑temelli raporlar ve panolar oluşturun.

## Yaygın Sorunlar ve Çözümler
- **Tarih aralığı aramasında sonuç yok** – Belgelerinizdeki tarih formatının eklediğiniz özel `DateFormat` ile eşleştiğinden emin olun.  
- **Regex sorguları çok fazla sonuç veriyor** – Deseni iyileştirin veya ek alan niteleyicileriyle arama kapsamını sınırlayın.  
- **İndeksleme hataları yakalanmıyor** – Olay işleyicisinin `index.add(...)` çağrısından **önce** ekli olduğundan emin olun.

## Sıkça Sorulan Sorular

**S: Tarih aralığı aramasını diğer sorgu türleriyle karıştırabilir miyim?**  
C: Kesinlikle. Tek bir sorgu dizesinde tarih aralığı koşulunu boolean operatörleri, faceted filtreler veya regex desenleriyle birleştirebilirsiniz.

**S: Tarih formatlarını değiştirdikten sonra indeksi yeniden oluşturmalı mıyım?**  
C: Evet. İndeks tokenleştirilmiş terimleri saklar; sadece `SearchOptions` güncellemek mevcut veriyi yeniden tokenlemez. Formatları değiştirdikten sonra belgeleri yeniden indeksleyin.

**S: GroupDocs.Search büyük indekslerle nasıl başa çıkar?**  
C: Artımlı indeksleme ve disk‑üzerinde depolama kullanır, böylece bellek tüketimini düşük tutarak milyonlarca belgeye ölçeklenebilir.

**S: Wildcard karakter sayısında bir sınırlama var mı?**  
C: Wildcard’lar verimli işlenir, ancak çok sayıda ön ek wildcard (`*term`) performansı düşürebilir. Önek veya sonek wildcard’ları tercih edin.

**S: Üretim ortamı için hangi lisans modeli önerilir?**  
C: GroupDocs’tan kalıcı veya abonelik lisansı, güncellemeler, destek ve deneme sınırlamaları olmadan dağıtım yapma imkanı sağlar.

## Sonuç
**date range search** ve GroupDocs.Search for Java’nın sunduğu tam gelişmiş sorgu türleri yelpazesini ustalaşarak son derece duyarlı, özellik‑zengin arama deneyimleri oluşturabilirsiniz. Sağlam hata yönetimi uygulayın, indeksinizi ince ayar yapın ve sorguları birleştirerek neredeyse her geri getirme senaryosunu karşılayın. Bugün denemeye başlayın ve uygulamanızın veri‑erişim yeteneklerini bir üst seviyeye taşıyın.

---

**Son Güncelleme:** 2025-12-16  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 (Java)  
**Yazar:** GroupDocs