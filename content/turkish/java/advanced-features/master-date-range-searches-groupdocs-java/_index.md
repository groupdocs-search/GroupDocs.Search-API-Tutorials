---
date: '2026-03-04'
description: GroupDocs.Search ile özel tarih formatı Java aramaları nasıl uygulanır,
  tarih aralığı sorguları, özel desenler ve performans ipuçları dahil olmak üzere
  öğrenin.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: Özel Tarih Formatı Java | GroupDocs ile Tarih Aralığı Araması
type: docs
url: /tr/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Özel Tarih Biçimi Java | GroupDocs ile Tarih Aralığı Arama

Tarihine göre belge arama, arşiv sistemi, finansal raporlama aracı veya içerik‑yönetim portalı oluştururken sık karşılaşılan bir gereksinimdir. Bu öğreticide **custom date format java** tekniklerini GroupDocs.Search kullanarak öğrenecek, tarih aralığı sorgularını, özel desen tanımlamalarını ve **optimize search performance** ipuçlarını kapsayacaksınız. Sonunda, kullanıcıların kullandıkları formata bakılmaksızın herhangi bir tarih aralığındaki kayıtları getirebileceksiniz.

## Hızlı Yanıtlar
- **İndeksleme için birincil sınıf nedir?** `Index` from the `com.groupdocs.search` package.  
- **Özel bir tarih deseni nasıl tanımlanır?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Metin sorgusuyla arama yapabilir miyim?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Hangi Maven koordinatları gereklidir?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Geliştirme için lisansa ihtiyacım var mı?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## **custom date format java** nedir?
A **custom date format java** tells GroupDocs.Search how to interpret date strings that don’t follow the default ISO pattern (YYYY‑MM‑DD). By defining your own pattern—such as `MM/dd/yyyy` or `dd‑MM‑yyyy`—you enable the engine to recognize dates embedded in documents that use regional or legacy formats.

## Neden tarih aralığı sorguları için GroupDocs.Search kullanmalı?
- **Hız:** Built‑in indexing makes look‑ups O(log n).  
- **Esneklik:** Supports both text‑based and object‑based query creation.  
- **Çoklu biçim desteği:** Handles PDFs, Word, Excel, plain text, and more without extra code.  

## GroupDocs.Search ile **tarihine göre belge arama** nasıl yapılır
Below you’ll find a step‑by‑step guide that walks you through setting up the library, indexing files, and executing both simple and advanced date range searches.

### Önkoşullar
- Java 8 veya daha yeni bir sürüm yüklü.  
- Bağımlılık yönetimi için Maven.  
- GroupDocs.Search lisansına erişim (deneme veya geçici lisans geliştirme için yeterlidir).  

### Java için GroupDocs.Search Kurulumu

#### Maven ile Kurulum
Add the repository and dependency to your `pom.xml`:

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

#### Doğrudan İndirme
Alternatively, you can download the latest version directly from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Temel Başlatma ve Kurulum
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Özellik 1: Tarih Aralığı Arama Sorguları Oluşturma

### Metin Formu Sorgusu Kullanma
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Explanation**: The `daterange` syntax expects dates in `YYYY‑MM‑DD`. It returns all documents whose indexed dates fall within the interval.

### Sorgu Nesnesi Kullanma
For programmatic control and custom parsing, build a `SearchQuery` object:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Explanation**: `createDateRangeQuery` lets you supply `java.util.Date` objects, giving you full flexibility over time zones and locale‑specific handling.

## Özellik 2: **custom date format java** Desenlerini Belirleme

### Özel Tarih Biçimlerini Ayarlama
Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Explanation**: By clearing the default formats and adding a `DateFormat` that uses `/` as the separator, the engine now understands dates written as `MM/dd/yyyy`. This is essential for **search documents by date** in regions that prefer month‑first notation.

## **optimize search performance** İpuçları
- **Index Incrementally**: Add new files to the existing index instead of rebuilding from scratch.  
- **Prune Stale Data**: Periodically remove documents that are no longer needed.  
- **Adjust Memory Settings**: Increase the JVM heap (`-Xmx`) when working with large indexes.  

## Yaygın Sorunlar ve Çözümler
- **Date Parsing Errors**: Verify that the document’s date strings exactly match the custom pattern you defined.  
- **Missing Results**: Ensure the indexed fields contain date metadata; otherwise, the engine cannot match date queries.  
- **Index Access Exceptions**: Confirm that the `indexFolder` path is writable and not locked by another process.  

## Pratik Uygulamalar
1. **Arşiv Sistemleri** – Belirli bir tarihsel dönemden kayıtları getir.  
2. **İçerik Yönetimi** – Avrupa izleyicileri için `dd/MM/yyyy` gibi bölgesel tarih biçimlerini destekle.  
3. **Finansal Yazılım** – İşlemleri mali çeyrek veya yıla göre hızlıca filtrele.  

## Bunun Önemi
Implementing **custom date format java** handling removes the friction of dealing with inconsistent date representations across documents. It enables you to **handle multiple date formats** in a single index, ensuring that end‑users get accurate results no matter how dates were originally recorded.

## Sonraki Adımlar
- `AND`, `OR` ve `NOT` operatörlerini kullanarak daha gelişmiş sorgu kombinasyonlarını keşfet.  
- Ek zaman damgası meta verilerini indekslemeniz gerekiyorsa özel analizörlerle deneme yap.  
- Milyonlarca belge için çözümünüzü ölçeklendirmek amacıyla resmi belgelerdeki performans ayarlama rehberini inceleyin.

## Sıkça Sorulan Sorular

**S: Metin formu ile nesne‑tabanlı tarih sorguları arasındaki fark nedir?**  
C: Metin formu hızlı ve kolaydır ancak varsayılan ISO formatıyla sınırlıdır; nesne‑tabanlı sorgular `Date` nesneleri ve özel formatlar sağlayarak daha fazla esneklik sunar.

**S: Tek bir sorguda birden fazla tarih aralığı arayabilir miyim?**  
C: Evet, `daterange` ifadelerini `AND` veya `OR` gibi mantıksal operatörlerle birleştirerek karmaşık sorgular oluşturabilirsiniz.

**S: Özel tarih biçimleri aramayı yavaşlatır mı?**  
C: Ek ayrıştırma için küçük bir ek yük vardır, ancak tipik iş yükleri için etkisi önemsizdir ve doğruluk kazançlarıyla dengelenir.

**S: GroupDocs.Search büyük ölçekli dağıtımlar için uygun mu?**  
C: Kesinlikle. Doğru indeksleme stratejileri ve JVM ayarlarıyla milyonlarca belgeye ölçeklenebilir.

**S: Daha fazla Java örneği nerede bulunabilir?**  
C: Additional samples and use‑case implementations için [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) adresini inceleyin.

---

**Kaynaklar**

- **Dokümantasyon**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Referansı**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **İndirme**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub Deposu**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ücretsiz Destek Forumu**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Geçici Lisans**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-03-04  
**Test Edilen Versiyon:** GroupDocs.Search Java 25.4  
**Yazar:** GroupDocs  

---