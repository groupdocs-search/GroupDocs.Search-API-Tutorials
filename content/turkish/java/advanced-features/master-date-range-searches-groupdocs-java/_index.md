---
date: '2025-12-18'
description: GroupDocs.Search ile Java aramalarında özel tarih formatı uygulamayı,
  tarih aralığı sorgularını, özel desenleri ve performans ipuçlarını öğrenin.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'Özel Tarih Formatı Java | GroupDocs ile Tarih Aralığı Arama'
type: docs
url: /tr/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Custom Date Format Java | GroupDocs ile Tarih Aralığı Arama

Tarih bazlı belge arama, arşiv sistemi, finansal raporlama aracı veya içerik‑yönetim portalı oluşturuyor olsanız da sık bir gereksinimdir. Bu öğreticide GroupDocs.Search kullanarak **custom date format java** tekniklerini öğrenecek, tarih aralığı sorgularını, özel desen tanımlamalarını ve **optimize search performance** ipuçlarını kapsayacaksınız. Sonunda, kullanıcıların kullandıkları formata bakılmaksızın herhangi bir tarih aralığındaki kayıtları alabilmelerini sağlayacaksınız.

## Hızlı Yanıtlar
- **İndeksleme için birincil sınıf nedir?** `Index` from the `com.groupdocs.search` package.  
- **Özel bir tarih deseni nasıl tanımlanır?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Metin sorgusuyla arama yapabilir miyim?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Hangi Maven koordinatları gereklidir?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Geliştirme için lisansa ihtiyacım var mı?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## **custom date format java** nedir?
Bir **custom date format java**, GroupDocs.Search'e varsayılan ISO desenini (YYYY‑MM‑DD) takip etmeyen tarih dizelerini nasıl yorumlayacağını söyler. Kendi deseninizi tanımlayarak—örneğin `MM/dd/yyyy` veya `dd‑MM‑yyyy`—motorun bölgesel veya eski formatları kullanan belgelerdeki tarihleri tanımasını sağlarsınız.

## Tarih aralığı sorguları için neden GroupDocs.Search kullanmalı?
- **Speed:** Built‑in indexing makes look‑ups O(log n).  
- **Flexibility:** Supports both text‑based and object‑based query creation.  
- **Multi‑format support:** Handles PDFs, Word, Excel, plain text, and more without extra code.  

## GroupDocs.Search ile **search documents by date** nasıl yapılır
Aşağıda, kütüphaneyi kurma, dosyaları indeksleme ve hem basit hem de gelişmiş tarih aralığı aramaları yürütme adımlarını içeren adım‑adım bir kılavuz bulacaksınız.

### Önkoşullar
- Java 8 veya daha yeni bir sürüm yüklü.  
- Bağımlılık yönetimi için Maven.  
- Geliştirme için çalışan bir GroupDocs.Search lisansına (deneme veya geçici) erişim.  

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
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

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

**Açıklama**: The `daterange` syntax expects dates in `YYYY‑MM‑DD`. It returns all documents whose indexed dates fall within the interval.

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

**Açıklama**: `createDateRangeQuery` lets you supply `java.util.Date` objects, giving you full flexibility over time zones and locale‑specific handling.

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

**Açıklama**: By clearing the default formats and adding a `DateFormat` that uses `/` as the separator, the engine now understands dates written as `MM/dd/yyyy`. This is essential for **search documents by date** in regions that prefer month‑first notation.

## **optimize search performance** için İpuçları
- **Index Incrementally**: Add new files to the existing index instead of rebuilding from scratch.  
- **Prune Stale Data**: Periodically remove documents that are no longer needed.  
- **Adjust Memory Settings**: Increase the JVM heap (`-Xmx`) when working with large indexes.  

## Yaygın Sorunlar ve Çözümler
- **Date Parsing Errors**: Verify that the document’s date strings exactly match the custom pattern you defined.  
- **Missing Results**: Ensure the indexed fields contain date metadata; otherwise, the engine cannot match date queries.  
- **Index Access Exceptions**: Confirm that the `indexFolder` path is writable and not locked by another process.  

## Pratik Uygulamalar
1. **Archival Systems** – Retrieve records from a specific historical period.  
2. **Content Management** – Support regional date formats like `dd/MM/yyyy` for European audiences.  
3. **Financial Software** – Filter transactions by fiscal quarter or year quickly.  

## Sonuç
Artık GroupDocs.Search ile güçlü tarih‑aralığı aramaları oluşturmak için eksiksiz bir **custom date format java** araç kutusuna sahipsiniz. Bu desenleri uygulayın, performansı ince ayarlayın ve uygulamanız her türlü zaman sorgusu için hızlı, doğru sonuçlar sunacaktır.

## Sıkça Sorulan Sorular

**Q: Metin formu ile nesne‑tabanlı tarih sorguları arasındaki fark nedir?**  
A: Text form is quick and easy but limited to the default ISO format; object‑based queries let you supply `Date` objects and custom formats for greater flexibility.

**Q: Tek bir sorguda birden fazla tarih aralığını arayabilir miyim?**  
A: Yes, combine `daterange` clauses with logical operators like `AND` or `OR` to build complex queries.

**Q: Özel tarih formatları aramayı yavaşlatır mı?**  
A: There is a minor overhead for additional parsing, but the impact is negligible for typical workloads and is outweighed by the accuracy gains.

**Q: GroupDocs.Search büyük ölçekli dağıtımlar için uygun mu?**  
A: Absolutely. With proper indexing strategies and JVM tuning, it scales to millions of documents.

**Q: Daha fazla Java örneği nerede bulunabilir?**  
A: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) for additional samples and use‑case implementations.

---

**Kaynaklar**

- **Dokümantasyon**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Referansı**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **İndirme**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub Deposu**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Ücretsiz Destek Forumu**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Geçici Lisans**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

**Son Güncelleme:** 2025-12-18  
**Test Edilen Versiyon:** GroupDocs.Search Java 25.4  
**Yazar:** GroupDocs