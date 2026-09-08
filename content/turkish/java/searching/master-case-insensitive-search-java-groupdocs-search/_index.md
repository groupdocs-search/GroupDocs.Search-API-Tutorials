---
date: '2026-07-31'
description: GroupDocs.Search ile bir indekse belge ekleyerek Java'da case insensitive
  search uygulamayı, indeksleme sırasında karakter değiştirme kullanarak metni normalize
  etmeyi öğrenin.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Case insensitive search java, belgeleri bir indekse eklemenizi ve
  harf durumunu düşünmeden sorgulamanızı sağlar. Bu kılavuz, GroupDocs.Search'in indeksleme
  sırasında metni hızlı ve güvenilir sonuçlar için nasıl normalize ettiğini gösterir.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Case Insensitive Search Java – GroupDocs ile Belgeleri İndekse Ekleyin
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Java'da Case‑Insensitive Search için Belgeleri İndekse Ekleyin
type: docs
url: /tr/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Java'da Büyük/Küçük Harfe Duyarsız Arama için Belgeleri Diziye Ekle

Kullanıcıların nasıl yazdıklarından bağımsız olarak güvenilir bir şekilde bilgi bulabilen **case insensitive search java**'a ihtiyacınız olduğunda, metni normalleştirerek belgeleri bir dizine eklemek anahtardır. Bu öğreticide, GroupDocs.Search for Java'ı yapılandırarak indekslediğiniz her belgenin indeksleme sırasında otomatik olarak küçük harfe (veya başka bir şekilde) dönüştürülmesini sağlayacağız, böylece ek sorgu zamanı mantığına ihtiyaç duymadan büyük/küçük harfe duyarsız sonuçlar garantilenir.

## Hızlı Yanıtlar
- **“add documents to index” ne anlama geliyor?** Bu, kaynak dosyaların daha sonra sorgulanabilmesi için aranabilir bir veri yapısına yüklenmesi anlamına gelir.  
- **Karakter değiştirmeyi neden kullanmalıyım?** Bu, her karakteri (genellikle küçük harfe) normalleştirir, böylece aramalar otomatik olarak büyük/küçük harf farkını görmez.  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme yeterlidir; üretim dağıtımları için tam lisans gereklidir.  
- **Hangi Java sürümü gerekiyor?** Java 8 veya daha yenisi; kütüphane optimum performans için Java 11+ hedeflemektedir.  
- **Gerektiğinde büyük/küçük harfe duyarlı aramaya geçebilir miyim?** Evet—arama seçenekleri, sorgu başına büyük/küçük harf duyarlılığını değiştirmenize izin verir.

## GroupDocs.Search'te “add documents to index” ne anlama geliyor?
Kaynak dosyalarınızı (PDF, DOCX, TXT vb.) aranabilir bir dizine yükleyin, böylece motor bunları hızlıca getirebilir. Belgeleri bir dizine eklemek, her dosyayı ayrıştırır, düz metni çıkarır ve hızlı aramalar sağlayan optimize edilmiş bir veri yapısında saklar.

## İndeksleme sırasında karakter değiştirmeyi neden etkinleştirmelisiniz?
Karakter değiştirme, her karakteri önceden tanımlanmış bir eşdeğere (genellikle küçük harfe) dönüştürür, indeks oluşturulurken. Bu, büyük/küçük harf, aksan veya yerel sembollerdeki farklılıkların arama sonuçlarını etkilememesini sağlar. Metni indeksleme sırasında normalleştirerek, motor sorguları tutarlı bir token kümesiyle eşleştirebilir ve her aramada ek işlem yapmadan hızlı, güvenilir büyük/küçük harfe duyarsız davranış sunar.

## Önkoşullar
- **GroupDocs.Search for Java** sürüm 25.4 veya yenisi (kütüphane 30'dan fazla dosya formatını destekler ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri indeksleyebilir).  
- **Java Development Kit (JDK)** 8 veya üzeri yüklü olmalıdır.  
- **Maven**'e temel aşinalık (veya JAR'ları manuel ekleme yeteneği).

## GroupDocs.Search for Java'ı Kurma

### Maven Kurulumu
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Maven kullanmak istemiyorsanız, resmi siteden en son JAR'ı alın: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Alımı
- **Free Trial** – denemeye başlamak için bir deneme lisansı indirin.  
- **Temporary License** – GroupDocs portalından uzatılmış bir test lisansı talep edin.  
- **Full License** – yayına hazır olduğunuzda bir üretim lisansı satın alın.

### Temel Başlatma (Dizini Oluşturma)
The following snippet creates an index folder and enables character replacements:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Uygulama Rehberi

### Dizin Ayarlarında Karakter Değiştirmeyi Etkinleştirme
Bu özelliği etkinleştirmek, motorun indeksleme sırasında karakterleri değiştirmesini sağlar; bu, büyük/küçük harfe duyarsız davranışın temel adımıdır.

#### Adım 1: `IndexSettings`'i Yapılandırma
`IndexSettings`, dizinin metni nasıl saklayıp işlediğini kontrol eden yapılandırma nesnesidir. `useCharacterReplacements` özelliğini **true** olarak ayarlayarak otomatik küçük harfe dönüştürmeyi (veya sağladığınız herhangi bir özel eşlemeyi) etkinleştirirsiniz.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Karakter Değiştirmeleri Yapılandırma
Her karakteri onun küçük harf karşılığına (veya ihtiyacınız olan herhangi bir özel eşlemeye) eşleyin.

#### Adım 2: Değiştirme Çiftlerini Tanımlama ve Ekleme
Değiştirme sözlüğü `'A' → 'a'`, `'É' → 'e'` gibi çiftleri tutar. Bu çiftleri indekslemeden önce eklemek, her tokenın normalleştirilmesini sağlar.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Belgeleri İndeksleme
Dizin hazır olduğuna göre, herhangi bir klasörden **add documents to index** yapabilirsiniz.

#### Adım 3: İndeksleme İçin Belgeleri Ekleme
GroupDocs.Search hedef dizini tarar, her desteklenen dosya tipinden metni çıkarır, değiştirme haritasını uygular ve tokenları dizin depolamasına yazar.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Büyük/Küçük Harfe Duyarlı Arama Yap (İsteğe Bağlı)

#### Adım 4: Büyük/Küçük Harfe Duyarlı Aramaları Gerçekleştirme
`SearchOptions`, sorgu davranışını yapılandırır; örneğin büyük/küçük harf duyarlılığını değiştirmek, aramaların nasıl gerçekleştirileceği üzerinde ayrıntılı kontrol sağlar.  
`SearchOptions.setUseCaseSensitiveSearch(true)` motoru belirli bir sorgu sırasında büyük ve küçük harf karakterlerini ayrı olarak ele almaya zorlar, varsayılan büyük/küçük harfe duyarsız davranışı geçersiz kılar.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Pratik Uygulamalar
1. **Pazarlama Kampanyaları** – Ürün adlarını normalleştirerek satış ekiplerinin varlıkları büyük/küçük harf endişesi olmadan bulmasını sağlar.  
2. **Müşteri Desteği** – Kullanıcı “login” ya da “Login” yazsa da doğru makaleyi döndüren yardım masası arama kutularını güçlendirir.  
3. **E‑ticaret Katalogları** – Alışveriş yapanların ürün başlıklarını nasıl yazarlarsa yazsınlar bulmasını sağlayarak dönüşüm oranlarını artırır.

## Performans Düşünceleri
- **Kaynak Dosyaları Düzenleyin** – Düzenli bir klasör hiyerarşisi, **add documents to index** adımında tarama süresini azaltır.  
- **Belleği İzleyin** – Büyük veri kümelerini indekslemek önemli RAM tüketebilir; dosyaları 500 – 1 000 öğe gruplarında işlemek yığın kullanımını kontrol altında tutar.  
- **Asenkron İndeksleme** – Destekleniyorsa, indekslemeyi arka plan iş parçacığında çalıştırarak UI'nin yanıt vermesini sağlayın ve kullanıcı işlemlerini engellemekten kaçının.

## Yaygın Sorunlar ve Sorun Giderme
| Semptom | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Bilinen bir terim için sonuç dönmüyor | Karakter değiştirmeleri etkinleştirilmemiş | `settings.setUseCharacterReplacements(true)` ayarlandığını ve değiştirme haritasının gerekli karakterleri içerdiğini doğrulayın. |
| İndeksleme sırasında bellek yetersizliği hatası | Aynı anda çok fazla büyük dosya indeksleniyor | Daha küçük partilerde indeksleyin veya JVM yığınını artırın (`-Xmx4g`). |
| Arama beklenmedik şekilde büyük/küçük harfe duyarlı sonuçlar döndürüyor | `SearchOptions.setUseCaseSensitiveSearch(true)` ayarlanmış | Varsayılan büyük/küçük harfe duyarsız davranış için kaldırın veya `false` olarak ayarlayın. |
| Dizin yükleme süresi beklentileri aşıyor | Verimsiz klasör düzeni veya SSD kullanılmıyor | Dosyaları yeniden düzenleyin, kullanılmayan belgeleri temizleyin ve dizini hızlı bir SSD'de depolayın. |
| Özel karakterler yok sayılıyor | Değiştirme haritasında Unicode girişleri eksik | “é”, “ß”, “ø” gibi karakterler için istenen eşlemeleri ekleyin. |

## Sık Sorulan Sorular

**Q: İndeksleme sırasında özel karakterleri (ör. “é”, “ß”) nasıl yönetebilirim?**  
A: Bu karakterleri değiştirme haritanıza ekleyin, ASCII eşdeğerlerine eşleyin veya arama gereksinimlerine göre değiştirmeden bırakın.

**Q: Karakter değiştirmeyi belirli bir dile sınırlayabilir miyim?**  
A: Evet. Sözlüğe eklemeden önce yalnızca hedef dilin karakterlerini içeren özel bir değiştirme dizisi oluşturun.

**Q: Dizinin yüklenmesi uzun sürerse ne yapmalıyım?**  
A: Klasör yapısını optimize edin, gereksiz dosyaları kaldırın ve dizini yüksek hızlı bir SSD'de depolayın. Artımlı indeksleme de yükleme süresini azaltır.

**Q: İndeksleme sonrası karakter değiştirmeleri geri alınabilir mi?**  
A: Hayır. Değiştirmeler indekslenmiş veriye yerleşiktir; değiştirmek için dizini yeni ayarlarla yeniden oluşturmanız gerekir.

**Q: Daha ayrıntılı API belgelerini nerede bulabilirim?**  
A: Resmi dokümantasyon ve API referansı kapsamlı detaylar sunar (aşağıdaki Kaynaklara bakın).

## Kaynaklar
- [Dokümantasyon](https://docs.groupdocs.com/search/java/)
- [API Referansı](https://reference.groupdocs.com/search/java)
- [GroupDocs.Search İndir](https://releases.groupdocs.com/search/java/)
- [GitHub Deposu](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Ücretsiz Destek Forum](https://forum.groupdocs.com/c/search/10)
- [Geçici Lisans Bilgileri](https://purchase.groupdocs.com/temporary-license/) 

---

**Son Güncelleme:** 2026-07-31  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs  

## İlgili Öğreticiler

- [GroupDocs.Search Java'da Karakter Değiştirme: Metin Aramasını ve İndekslemeyi Geliştiren Kapsamlı Rehber](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Belgeleri Diziye Ekle: GroupDocs ile Büyük/Küçük Harfe Duyarlı Java Araması](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [GroupDocs.Search for Java ile Belgeleri Diziye Nasıl Eklenir](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)