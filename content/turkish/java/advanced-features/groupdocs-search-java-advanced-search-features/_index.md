---
date: '2026-02-16'
description: GroupDocs.Search for Java kullanarak wildcard arama, tarih aralığı araması
  ve özel tarih formatı gibi özellikleri nasıl uygulayacağınızı, hata yönetimi ve
  performans optimizasyonu dahil olmak üzere öğrenin.
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: GroupDocs.Search ile Java'da Joker Karakter Araması – Gelişmiş Özellikler
type: docs
url: /tr/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

# Wildcard Search Java ile GroupDocs.Search – Gelişmiş Özellikler

Modern, veri‑odaklı uygulamalarda **wildcard search java**, kullanıcıların bir kelimenin sadece bir kısmını bildiklerinde bile bilgi bulmalarını sağlayan en esnek yöntemlerden biridir. Uyumluluk portalı, e‑ticaret kataloğu veya içerik‑yönetim sistemi oluşturuyor olsanız da, wildcard search'ü tarih aralığı, faceted, numeric, regex ve boolean sorgularıyla birleştirmek size gerçekten güçlü bir arama motoru sağlar. Bu öğretici, sizi her gelişmiş özelliğin üzerinden geçirir, indeksleme hatalarının nasıl ele alınacağını gösterir ve performans‑ayar ipuçları sunar — hepsi kopyalanmaya hazır Java kodu ile.

## Quick Answers
- **Wildcard search java nedir?** Bir terimde bir veya birden fazla karakteri eşleştirmek için `?` veya `*` yer tutucularını kullanan bir sorgudur.  
- **Bunu sağlayan kütüphane hangisidir?** GroupDocs.Search for Java.  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü çalışır; ticari kullanım için bir üretim lisansı gereklidir.  
- **Bunu tarih aralığı sorgularıyla birleştirebilir miyim?** Evet—wildcard, tarih aralığı, faceted ve boolean ifadelerini tek bir sorguda karıştırabilirsiniz.  
- **Büyük veri setleri için hızlı mı?** Doğru indekslendiğinde, aramalar milyonlarca belge üzerinde bile saniyenin altında sürede çalışır.  

## What is wildcard search java?
Wildcard search java, bir terimin `?ffect` (*affect* veya *effect* eşleşmesi) veya `prod*` (*product*, *production* vb. eşleşmesi) gibi bir desenle eşleştiği belgeleri bulmanızı sağlar. Yanlış yazımlar, kısmi girişler veya tam ifadenin bilinmediği durumlar için idealdir.

## Why use GroupDocs.Search for Java?
GroupDocs.Search, birçok sorgu türü için birleşik bir API sunar—simple, **wildcard search java**, faceted, numeric, date range, regex, boolean ve phrase—böylece birden fazla kütüphaneyle uğraşmadan gelişmiş arama deneyimleri oluşturabilirsiniz. Olay‑tabanlı hata yönetimi de indeksleme hattınızı dayanıklı tutar.

## Prerequisites
- **GroupDocs.Search Java kütüphanesi** (v25.4 veya daha yeni).  
- **Java Development Kit (JDK)** projenizle uyumlu.  
- Bağımlılık yönetimi için Maven (veya manuel indirme).  

### Required Libraries and Environment Setup
GroupDocs deposunu ve bağımlılığı `pom.xml` dosyanıza ekleyin:

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

### Alternative Setup
Doğrudan indirmeler için, [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresini ziyaret edin.

### Licensing and Initial Setup
Ücretsiz deneme sürümü veya geçici bir lisansla başlayın:

- Detaylar için [GroupDocs License Options](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin.

Şimdi, aranabilir verilerinizi tutacak indeks klasörünü oluşturalım.

## Setting Up GroupDocs.Search for Java

### Basic Initialization
İlk olarak, diskte bir klasöre işaret eden bir `Index` nesnesi oluşturun:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

Artık tüm arama işlemlerine bir geçiş noktanız var.

## Implementation Guide

### Feature 1: Error Handling in Indexing
#### How to capture indexing errors (Java)

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

*Neden önemli*: `ErrorOccurred` olayını dinleyerek, sorunları kaydedebilir, başarısız dosyaları yeniden deneyebilir veya tüm süreci çökertmeden kullanıcılara uyarı gönderebilirsiniz.

### Feature 2: Simple Search Query
#### What is a simple search?

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*Sonuç*: **volutpat** terimini içeren tüm belgeleri döndürür.

### Feature 3: Wildcard Search Query
#### How does wildcard search java work?

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*Sonuç*: **affect** ve **effect** her ikisini de eşleştirir, `?` yer tutucusunun gücünü gösterir.

### Feature 4: Faceted Search Query
#### How to perform faceted search java

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*Sonuç*: Aramayı **Content** alanıyla sınırlar, kategori veya yazar gibi meta verilerle filtreleme için idealdir.

### Feature 5: Numeric Range Search Query
#### How to search numeric ranges

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*Sonuç*: Sayısal değerlerin 2000 ile 3000 arasında olduğu belgeleri getirir.

### Feature 6: Date Range Search Query
#### How to execute date range search (custom date format java)

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

*Açıklama*: `SearchOptions`'ı özelleştirerek, motorun tarihleri **MM/DD/YYYY** biçiminde tanımasını sağlarsınız, ardından 1 Ocak 2000 ile 15 Haziran 2001 arasındaki tüm kayıtları getirirsiniz.

### Feature 7: Regular Expression Search Query
#### How to run regex search java

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*Sonuç*: Üç veya daha fazla aynı karakterden oluşan dizileri bulur (ör. “aaa”, “111”).

### Feature 8: Boolean Search Query
#### How to combine conditions with boolean search java

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*Sonuç*: **justo** içeren belgeleri döndürür ancak aynı zamanda **3456** içerenleri hariç tutar.

### Feature 9: Complex Boolean Search Query
#### How to craft advanced boolean queries

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*Sonuç*: “English” benzeri dosya adlarını (1‑3 karakter varyasyonu izin vererek) **veya** hem **3456** hem de **consequat** içeren içeriği arar.

### Feature 10: Phrase Search Query
#### How to search exact phrases

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*Sonuç*: **ipsum dolor sit amet** tam ifadesini içeren yalnızca belgeleri getirir.

## Practical Applications
1. **E‑ticaret Platformları** – Ürünleri beden, renk ve marka göre filtrelemek için **faceted search java** kullanın.  
2. **İçerik Yönetim Sistemleri** – Gelişmiş editöryal araçları güçlendirmek için **boolean search java** ile phrase search'i birleştirin.  
3. **Veri Analizi Araçları** – Zaman‑bazlı raporlar ve panolar oluşturmak için **date range search** ve **custom date format java**'yu kullanın.  

## Common Issues & Solutions
- **Tarih aralığı aramasında sonuç yok** – Belgelerinizdeki tarih formatının eklediğiniz özel `DateFormat` ile eşleştiğini doğrulayın.  
- **Regex sorguları çok fazla sonuç döndürüyor** – Deseni iyileştirin veya ek alan niteleyicileriyle arama kapsamını sınırlayın.  
- **İndeksleme hataları yakalanmıyor** – Olay işleyicisinin `index.add(...)` çağrılmadan **önce** ekli olduğundan emin olun.  
- **Wildcard arama yavaş görünüyor** – Çok büyük indekslerde baştaki wildcard'ları (`*term`) kullanmaktan kaçının; son ek veya orta ek desenlerini tercih edin.  

## Frequently Asked Questions

**S: Tarih aralığı aramasını diğer sorgu türleriyle karıştırabilir miyim?**  
C: Kesinlikle. Tek bir sorgu dizesinde tarih aralığı koşulunu wildcard, boolean, faceted veya regex desenleriyle birleştirebilirsiniz.

**S: Tarih formatlarını değiştirdikten sonra indeksi yeniden oluşturmalı mıyım?**  
C: Evet. İndeks, tokenleştirilmiş terimleri saklar; sadece `SearchOptions`'ı güncellemek mevcut verileri yeniden tokenleştirmez. Formatları değiştirdikten sonra belgeleri yeniden indeksleyin.

**S: GroupDocs.Search büyük indeksleri nasıl yönetir?**  
C: Artımlı indeksleme ve disk‑üzerinde depolama kullanır, böylece bellek kullanımını düşük tutarak milyonlarca belgeye ölçeklendirebilirsiniz.

**S: Wildcard karakter sayısında bir limit var mı?**  
C: Wildcard'lar verimli işlenir, ancak çok sayıda baştaki wildcard (ör. `*term`) performansı düşürebilir. Ön ek veya son ek wildcard'ları tercih edin.

**S: Üretim için önerilen lisans modeli nedir?**  
C: GroupDocs'tan kalıcı ya da abonelik lisansı, güncellemeler, destek ve deneme sınırlamaları olmadan dağıtım yapma imkanı sağlar.

## Conclusion
**wildcard search java**'yi ve GroupDocs.Search for Java tarafından sunulan gelişmiş sorgu türlerinin tam paketini ustaca kullanarak, son derece yanıt veren, özellik‑zengin arama deneyimleri oluşturabilirsiniz. Sağlam hata yönetimi uygulayın, indeksinizi ince ayar yapın ve sorguları birleştirerek neredeyse her türlü geri getirme senaryosunu karşılayın. Bugün denemeye başlayın ve uygulamanızın veri‑erişim yeteneklerini yükseltin.

---

**Son Güncelleme:** 2026-02-16  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 (Java)  
**Yazar:** GroupDocs