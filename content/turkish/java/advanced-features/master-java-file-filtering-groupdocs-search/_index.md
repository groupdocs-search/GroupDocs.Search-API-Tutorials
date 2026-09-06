---
date: '2026-09-06'
description: GroupDocs.Search for Java kullanarak Java dosya uzantılarını nasıl filtreleyeceğinizi
  öğrenin; mantıksal AND, OR, NOT operatörleri, tarih aralığı filtreleri ve yol filtrelerini
  kapsar.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: GroupDocs.Search kullanarak Java dosya uzantılarını filtreleyin. Java'da
  mantıksal operatörlerle uzantı, tarih aralığı ve yol filtrelerini birleştirmeyi
  öğrenin.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: GroupDocs.Search ile Java dosya uzantılarını filtreleme – Tam Kılavuz
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: GroupDocs.Search ile Java dosya uzantılarını nasıl filtre ederim
type: docs
url: /tr/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Search ile java dosya uzantılarını filtreleme

Bu kapsamlı öğreticide, GroupDocs.Search ile belgeleri indekslerken **filter file extensions java** nasıl yapılacağını öğreneceksiniz. Kılavuzun sonunda yalnızca ihtiyacınız olan dosya türlerini dahil edebilecek, istenmeyen formatları hariç tutabilecek ve bu kuralları tarih aralığı ve yol filtreleriyle mantıksal AND, OR ve NOT operatörleri kullanarak birleştirebileceksiniz. Bu yaklaşım indeksinizi hafif tutar, aramaları hızlandırır ve veri işleme politikalarına uyum sağlamanıza yardımcı olur.

## Hızlı yanıtlar
- **Java dosya uzantı filtresi nedir?** Bu, GroupDocs.Search'e indeksleme sırasında hangi dosya uzantılarını dahil edeceğini veya hariç tutacağını belirten bir kuraldır.  
- **Bu özelliği hangi kütüphane sağlar?** GroupDocs.Search for Java.  
- **Bir lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme çalışır; üretim için tam lisans gereklidir.  
- **Filtreleri birleştirebilir miyim?** Evet – uzantı, tarih, boyut ve yol filtrelerini AND, OR, NOT mantığıyla zincirleyebilirsiniz.  
- **Maven ile uyumlu mu?** Kesinlikle – GroupDocs.Search bağımlılığını `pom.xml` dosyanıza ekleyin.

## Java dosya uzantı filtresi nedir?
Bir **java file extension filter**, her dosyanın uzantısını indeksleme motoruna gönderilmeden önce değerlendiren bir kural kümesidir. `.txt`, `.pdf` veya `.epub` gibi uzantıları belirterek **include files by extension** veya **exclude files by extension** yapabilir ve indeksinizin odaklanmış ve arama sonuçlarınızın ilgili olmasını sağlayabilirsiniz.

## GroupDocs.Search ile dosya uzantısı filtrelemeyi neden kullanmalısınız?
Dosya uzantısı filtreleme, alakasız formatları hariç tutarak indeksleme verimliliğini artırır, depolama gereksinimlerini azaltır ve istenmeyen içeriğin indekse girmesini önleyerek uyumluluk kurallarına uymaya yardımcı olur. Ayrıca, arama motoru daha küçük ve daha ilgili bir veri kümesini işlediği için sorgu yanıtları daha hızlı olur.

- **Performance:** İstenmeyen dosyaların atlanması I/O'yu azaltır ve büyük depolarda indekslemeyi %40'a kadar hızlandırır.  
- **Storage savings:** Yalnızca ilgili belgeler indeksde saklanır, ortalama %30 disk kullanımını düşürür.  
- **Compliance:** Gizli veya desteklenmeyen dosya türlerinin yanlışlıkla indekslenmesini önler.  
- **Flexibility:** **date range filter java** özellikleriyle birleştirerek belirli dönemlerde oluşturulan veya değiştirilen dosyaları hedefleyebilirsiniz.

## Önkoşullar

Başlamadan önce, aşağıdakilere sahip olduğunuzdan emin olun:

### Gerekli kütüphaneler ve bağımlılıklar
- **GroupDocs.Search for Java** – sürüm 25.4 veya daha yeni (60+ giriş formatını destekler).  
- **Java Development Kit (JDK)** – uyumlu herhangi bir sürüm (8 veya daha yeni).

### Ortam kurulumu
- Entegre Geliştirme Ortamı (IDE): IntelliJ IDEA, Eclipse veya herhangi bir Maven‑uyumlu IDE.

### Bilgi önkoşulları
- Temel Java programlama.  
- Java'da dosya I/O konusuna aşinalık.  
- Düzenli ifadeler ve tarih‑zaman işleme anlayışı.

## GroupDocs.Search for Java Kurulumu
GroupDocs.Search'i kullanmaya başlamak için, projenize bir bağımlılık olarak eklemeniz gerekir.

### Maven yapılandırması
`pom.xml` dosyanıza aşağıdaki depo ve bağımlılık yapılandırmasını ekleyin:

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

### Doğrudan indirme
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Lisans edinme
1. **Free trial** – özellikleri ücretsiz olarak keşfedin.  
2. **Temporary license** – sınırlı bir süre için tam işlevsellik elde edin.  
3. **Purchase** – üretim kullanımı için kalıcı bir lisans edinin.

### Temel başlatma ve yapılandırma
Kütüphane eklendikten sonra, indeksleme ortamınızı başlatın. `IndexSettings` sınıfı, filtreler dahil tüm yapılandırma seçeneklerini tutar.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Uygulama rehberi
Aşağıda her filtre türüne derinlemesine bakacağız, **neden önemli olduğunu** açıklayacağız ve projenize kopyalayabileceğiniz adım adım talimatlar sunacağız.

### Dosya uzantısı filtreleme
İndeksleme sırasında dosyaları uzantılarına göre filtreleyin. Bu, yalnızca e‑kitapları (`.fb2`, `.epub`) ve düz metin dosyalarını (`.txt`) işlemek istediğinizde mükemmeldir.

#### Genel Bakış
`DocumentFilter.createFileExtension` uzantıların bir beyaz listesini oluşturur.

#### Uygulama adımları
1. **Create filter** – tutmak istediğiniz uzantıları tanımlayın.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – `IndexSettings` oluştururken filtreyi uygulayın.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal NOT filtresi
Arama senaryonuz için gerekli olmadığında, web sayfaları ve PDF'ler gibi belirli uzantıları hariç tutun.

#### Uygulama adımları
1. **Create exclusion filter** – reddedeceğiniz uzantıları belirtin.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – NOT filtresini diğer kurallarla birleştirin.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – yalnızca birleşik filtreyi geçen dosyalar indekslenir.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal AND filtresi
Birden fazla koşulu—oluşturma tarihi, uzantı ve dosya boyutu—birleştirerek **tüm kriterleri karşılayan dosyalar** indekslenir.

#### Genel Bakış
`DocumentFilter.createAnd` birden fazla filtreyi tek bir kurala birleştirir.

#### Uygulama adımları
1. **Define filters** – her koşul için ayrı filtreler oluşturun.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – tüm koşulları gerektirmek için AND operatörünü kullanın.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – birleşik filtreyi indeksleme boru hattına gönderin.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal OR filtresi
Belirtilen koşullardan **herhangi birini** karşılayan dosyaları dahil edin—küçük metin dosyalarını ve daha büyük metin dışı dosyaları yakalamak istediğinizde faydalıdır.

#### Uygulama adımları
1. **Define filters** – her alternatif koşul için ayrı filtreler oluşturun.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – OR operatörünü kullanın.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – birleşik filtreyi indeks yapılandırmasına ekleyin.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Oluşturma zamanı filtreleri
Belirli bir dönemde oluşturulan dosyaları hedefleyin—klasik bir **date range filter java** senaryosu.

#### Uygulama adımları
1. **Define date‑range filter** – başlangıç ve bitiş tarihlerini belirtin.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – yalnızca oluşturma zaman damgaları aralık içinde olan dosyalar indekslenir.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Değiştirme zamanı filtreleri
Belirli bir kesim tarihinden sonra değiştirilmiş dosyaları hariç tutun.

#### Uygulama adımları
1. **Define filter** – maksimum değiştirme zaman damgasını ayarlayın.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – kesim tarihinden daha yeni dosyalar göz ardı edilir.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Dosya yolu filtreleme
İndekslemeyi belirli klasörlerde bulunan veya bir desene uyan dosyalarla sınırlayın—belirli bir dizin hiyerarşisinde **include files by extension** için idealdir.

#### Uygulama adımları
1. **Define file‑path filter** – dizinleri eşleştirmek için glob veya regex desenleri kullanın.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – yol filtresini diğer kurallarla birlikte uygulayın.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Yaygın tuzaklar ve ipuçları

- **Never mix absolute and relative paths** aynı filtre yapılandırmasında karıştırmayın – beklenmeyen hariç tutmalara yol açabilir.  
- **Reset the `IndexSettings`** filtre setlerini değiştirirken; aksi takdirde önceki filtreler kalabilir.  
- **Combine a length upper bound with an extension filter** büyük koleksiyonlar için bellek kullanımını düşük tutmak amacıyla bir uzunluk üst sınırıyla uzantı filtresini birleştirin.  
- LoggingOptions, GroupDocs.Search için günlükleme yapılandırmasını kontrol eder.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) bir dosyanın neden reddedildiğini görmek için.

## Sıkça Sorulan Sorular

**S: İndeks oluşturulduktan sonra filtre kriterlerini değiştirebilir miyim?**  
C: Evet. Yeni bir `DocumentFilter` ile indeksi yeniden oluşturun veya güncellenmiş ayarlarla artımlı indeksleme kullanın.

**S: java file extension filter sıkıştırılmış arşivlerde (ör. ZIP) çalışır mı?**  
C: GroupDocs.Search desteklenen arşiv formatlarını indeksleyebilir, ancak uzantı filtresi arşivin kendisine uygulanır, iç dosyalara değil. Daha derin kontrol için iç içe filtreler kullanın.

**S: Belirli bir dosyanın neden dışlandığını nasıl hata ayıklayabilirim?**  
C: Kütüphanenin günlüklemesini etkinleştirin (`LoggingOptions.setEnabled(true)`) ve logu inceleyin – hangi filtrenin her dosyayı reddettiğini rapor eder.

**S: java file extension filter'ı özel regex filtreleriyle birleştirmek mümkün mü?**  
C: Kesinlikle. Bir regex filtresini `DocumentFilter.createAnd()` içinde uzantı filtresiyle birlikte kullanabilirsiniz.

**S: Çok sayıda filtre eklemenin performans üzerindeki etkisi nedir?**  
C: Her filtre indeksleme sırasında modest bir ek yük getirir, ancak indekslenen verinin azalması genellikle maliyeti aşar. Optimal dengeyi bulmak için temsilci bir örnekle test edin.

---

**Son Güncelleme:** 2026-09-06  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [Özel Tarih Formatı Java | GroupDocs ile Tarih Aralığı Araması](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: GroupDocs.Search for Java ile Boolean Aramaları](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [GroupDocs.Search for Java'da Gelişmiş İndeksleme Teknikleriyle Arama Performansını Optimize Et](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}