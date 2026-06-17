---
date: '2026-02-21'
description: GroupDocs.Search for Java kullanarak bir Java dosya uzantısı filtresinin
  nasıl uygulanacağını, mantıksal operatörler, oluşturma/değiştirme tarihleri ve yol
  filtrelerini kapsayacak şekilde öğrenin.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: GroupDocs.Search ile Java dosya uzantısı filtresi – Rehber
type: docs
url: /tr/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Search ile java file extension filter'ı ustalıkla kullanma

Artan bir belge deposunu yönetmek hızla bunaltıcı hâle gelebilir, özellikle yalnızca belirli dosya türlerini indekslemeniz gerektiğinde. **The java file extension filter** GroupDocs.Search'e hangi uzantıların dahil edileceğini veya hariç tutulacağını tam olarak söylemenizi sağlar ve indeksleme hattı üzerinde hassas kontrol sunar. Bu rehberde GroupDocs.Search for Java kurulumunu adım adım gösteriyor ve dosya uzantısı filtrelemesini mantıksal AND, OR ve NOT operatörleriyle, ayrıca tarih aralığı ve yol filtreleriyle nasıl birleştireceğinizi anlatacağız.

## Hızlı Yanıtlar
- **What is the java file extension filter?** İndeksleme sırasında GroupDocs.Search'e hangi dosya uzantılarının dahil edileceğini veya hariç tutulacağını söyleyen bir yapılandırmadır.  
- **Which library provides this feature?** GroupDocs.Search for Java.  
- **Do I need a license?** Değerlendirme için ücretsiz deneme çalışır; üretim için tam lisans gereklidir.  
- **Can I combine filters?** Evet – uzantı, tarih, boyut ve yol filtrelerini AND, OR, NOT mantığıyla zincirleyebilirsiniz.  
- **Is it Maven‑compatible?** Kesinlikle – GroupDocs.Search bağımlılığını `pom.xml` dosyanıza ekleyin.

## java file extension filter nedir?
Bir **java file extension filter**, her dosyanın uzantısını indeksleme motoruna gönderilmeden önce değerlendiren bir kural setidir. `.txt`, `.pdf` veya `.epub` gibi uzantılar belirleyerek **include files by extension** veya **exclude files by extension** yapabilir ve indeksinizi odaklı, arama sonuçlarınızı ilgili tutabilirsiniz.

## GroupDocs.Search ile file‑extension filtering neden kullanılmalı?
- **Performance:** İstenmeyen dosyaları atlamak I/O'yu azaltır ve indekslemeyi hızlandırır.  
- **Storage savings:** Yalnızca ilgili belgeler indeks içinde saklanır, disk kullanımını azaltır.  
- **Compliance:** Gizli veya desteklenmeyen dosya türlerinin yanlışlıkla indekslenmesini önler.  
- **Flexibility:** Belirli dönemlerde oluşturulan veya değiştirilen dosyaları hedeflemek için **date range filter java** özellikleriyle birleştirin.

## Önkoşullar

Başlamadan önce, aşağıdakilere sahip olduğunuzdan emin olun:

### Gerekli Kütüphaneler ve Bağımlılıklar
- **GroupDocs.Search for Java**: Versiyon 25.4 veya üzeri  
- **Java Development Kit (JDK)**: Uyumluluk sağlayan sürüm yüklü  

### Ortam Kurulumu
- Entegre Geliştirme Ortamı (IDE): IntelliJ IDEA, Eclipse veya Maven‑compatible herhangi bir IDE.

### Bilgi Önkoşulları
- Temel Java programlama  
- Java'da dosya I/O'ya aşinalık  
- Düzenli ifadeler ve tarih‑zaman işleme konularının anlaşılması  

## GroupDocs.Search for Java Kurulumu
GroupDocs.Search'i kullanmaya başlamak için projenize bağımlılık olarak eklemeniz gerekir.

### Maven Yapılandırması
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

### Doğrudan İndirme
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Lisans Edinme
1. **Free Trial** – özellikleri ücretsiz keşfedin.  
2. **Temporary License** – sınırlı bir süre tam işlevsellik elde edin.  
3. **Purchase** – üretim kullanımı için kalıcı bir lisans edinin.  

### Temel Başlatma ve Kurulum
Kütüphane eklendikten sonra, indeksleme ortamınızı başlatın:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Uygulama Kılavuzu
Aşağıda her filtre türüne derinlemesine bakacağız, **neden önemli olduğunu** açıklayacağız ve projenize kopyalayabileceğiniz adım adım kodları sunacağız.

### Dosya Uzantısı Filtreleme
İndeksleme sırasında dosyaları uzantılarına göre filtreleyin. Bu, yalnızca e‑kitapları (`.fb2`, `.epub`) ve düz metin dosyalarını (`.txt`) işlemek istediğinizde mükemmeldir.

#### Genel Bakış
`DocumentFilter.createFileExtension` kullanarak uzantıları beyaz listeye ekleyin.

#### Uygulama Adımları
1. **Create Filter**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal NOT Filtre
Arama senaryonuzda ihtiyaç duyulmadığında web sayfaları ve PDF'ler gibi belirli uzantıları hariç tutun.

#### Uygulama Adımları
1. **Create Exclusion Filter**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to Index Settings**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add Documents**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal AND Filtre
Birden fazla koşulu—oluşturma tarihi, uzantı ve dosya boyutu—birleştirerek **tüm kriterleri karşılayan dosyalar** indekslenir.

#### Genel Bakış
`DocumentFilter.createAnd` birden çok filtreyi tek bir kurala birleştirir.

#### Uygulama Adımları
1. **Define Filters**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine Filters**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index Documents**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal OR Filtre
Belirtilen koşullardan **herhangi birini** karşılayan dosyaları dahil edin—küçük metin dosyalarını ve daha büyük metin dışı dosyaları yakalamak istediğinizde faydalıdır.

#### Uygulama Adımları
1. **Define Filters**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine Filters with Logical Conditions**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR Filter**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Oluşturma Zamanı Filtreleri
Belirli bir dönemde oluşturulan dosyaları hedefleyin—klasik bir **date range filter java** senaryosu.

#### Uygulama Adımları
1. **Define Date Range Filter**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index Documents**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Değiştirme Zamanı Filtreleri
Belirli bir kesim tarihinden sonra değiştirilmiş dosyaları hariç tutun.

#### Uygulama Adımları
1. **Define Filter**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index Documents**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Dosya Yolu Filtreleme
İndekslemeyi belirli klasörlerde bulunan veya bir desenle eşleşen dosyalarla sınırlayın—belirli bir dizin hiyerarşisinde **include files by extension** için idealdir.

#### Uygulama Adımları
1. **Define File Path Filter**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Yaygın Tuzaklar ve İpuçları

- **Never mix absolute and relative paths** aynı filtre yapılandırmasında – beklenmeyen hariç tutmalara yol açabilir.  
- **Reset the `IndexSettings`** filtre setlerini değiştirirken; aksi takdirde önceki filtreler kalabilir.  
- **Combine a length upper bound with an extension filter** büyük koleksiyonlarda bellek kullanımını düşük tutmak için.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) bir dosyanın neden reddedildiğini görmek için.  

## Sıkça Sorulan Sorular

**Q: İndeks oluşturulduktan sonra filtre kriterlerini değiştirebilir miyim?**  
A: Evet. Yeni bir `DocumentFilter` ile indeksi yeniden oluşturun veya güncellenmiş ayarlarla artımlı indekslemeyi kullanın.

**Q: java file extension filter sıkıştırılmış arşivlerde (ör. ZIP) çalışır mı?**  
A: GroupDocs.Search desteklenen arşiv formatlarını indeksleyebilir, ancak uzantı filtresi arşivin kendisine uygulanır, iç dosyalara değil. Daha derin kontrol için iç içe filtreler kullanın.

**Q: Belirli bir dosyanın neden dışlandığını nasıl hata ayıklayabilirim?**  
A: Kütüphanenin kaydını etkinleştirin (`LoggingOptions.setEnabled(true)`) ve logu inceleyin – hangi filtrenin her dosyayı reddettiğini raporlar.

**Q: java file extension filter'ı özel regex filtreleriyle birleştirmek mümkün mü?**  
A: Kesinlikle. Bir regex filtresini `DocumentFilter.createAnd()` içinde uzantı filtresiyle birlikte sarabilirsiniz.

**Q: Birçok filtre eklemenin performans üzerindeki etkisi nedir?**  
A: Her filtre indeksleme sırasında hafif bir ek yük getirir, ancak indekslenen veri azalması genellikle maliyeti aşar. Optimal dengeyi bulmak için temsilci bir örnekle test edin.

---

**Son Güncelleme:** 2026-02-21  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs