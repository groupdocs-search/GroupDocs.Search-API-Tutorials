---
date: '2026-10-17'
description: Java'da GroupDocs.Search ile eşanlamlıları nasıl kullanacağınızı öğrenin,
  eşanlamlı sözlüklerini içe aktarın, eşanlamlı gruplarını yönetin ve daha iyi alaka
  düzeyi için arama dizininizi optimize edin.
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: Java'da GroupDocs.Search ile eşanlamlıları nasıl kullanacağınızı öğrenin,
  eşanlamlı sözlüklerini içe aktarın, eşanlamlı gruplarını yönetin ve daha iyi alaka
  düzeyi için arama dizininizi optimize edin.
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: Java'da GroupDocs.Search ile eşanlamlıları nasıl kullanılır
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: Java'da GroupDocs.Search ile eşanlamlıları nasıl kullanılır
type: docs
url: /tr/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da GroupDocs.Search ile eşanlamlıları nasıl kullanılır

Kullanıcılarınızın farklı kelimeler yazsalar bile doğru içeriği bulmasını istiyorsanız, **search with synonyms** cevaptır. Bu rehberde eşanlamlı sözlüğü nasıl oluşturacağınızı, içe ve dışa aktaracağınızı, eşanlamlı gruplarını nasıl yöneteceğinizi ve bu eşanlamlıları kullanarak sorguları otomatik olarak genişleten bir arama nasıl çalıştıracağınızı öğreneceksiniz. Bir CMS, bir e‑ticaret kataloğu veya bir hukuk belge deposu oluşturuyor olun, eşanlamlı desteği eklemek alaka düzeyini ve dönüşüm oranlarını önemli ölçüde artırabilir.

## Hızlı cevaplar
- **Eşanlamlıları eklemenin ilk adımı nedir?** `Index` örneği oluşturun ve `SynonymDictionary` API'si ile çalışın.  
- **Hazır bir eşanlamlı sözlüğü içe aktarabilir miyim?** Evet – dosya konumuyla `importDictionary(path)` çağırın.  
- **Eşanlamlı duyarlı aramayı nasıl etkinleştiririm?** `SearchOptions.setUseSynonymSearch(true)`'ı etkinleştirin.  
- **Çalışma zamanında eşanlamlı grupları düzenlemek mümkün mü?** Kesinlikle – sözlük API'si aracılığıyla grupları temizleyebilir, ekleyebilir veya alabilirsiniz.  
- **İndeksi ölçeklendirirken neyi izlemeliyim?** Kullanılmayan girişleri düzenli olarak temizleyin ve büyük eşanlamlı dosyaları için JVM yığınını ayarlayın.  

## Eşanlamlılarla arama nedir?
**Search with synonyms**, motorun bir kelime veya ifade kümesini birbirinin yerine geçebilecek şekilde ele alması demektir. Bir kullanıcı **“better”** yazdığında, motor aynı eşanlamlı grubunda tanımladığınız **“improve”**, **“enhance”** veya başka herhangi bir terimi de arar, kullanıcı sorgusunu değiştirmeden daha zengin sonuçlar sunar.

## GroupDocs.Search'te eşanlamlı desteği neden etkinleştirilir?
Eşanlamlı desteğini etkinleştirmek, motorun sorguları otomatik olarak eşdeğer terimleri içerecek şekilde genişletmesini sağlar; bu da sonuç alakasını artırır, kullanıcı memnuniyetini yükseltir ve e‑ticaret veya içerik odaklı siteler için dönüşüm oranlarını artırabilir. Ayrıca terim yönetimini merkezileştirir, birden fazla uygulama arasında bakım yükünü azaltır.

## Önkoşullar
- GroupDocs.Search for Java sürümü **25.4** veya daha yeni.  
- Maven desteği olan bir Java IDE (IntelliJ IDEA, Eclipse vb.).  
- Temel Java bilgisi ve Maven proje yapısına aşinalık.

### Gerekli kütüphaneler ve sürümler
- GroupDocs.Search for Java **25.4** veya üzeri.

### Ortam kurulumu
- Tercih ettiğiniz IDE (IntelliJ IDEA, Eclipse vb.).  
- Bağımlılık yönetimi için Maven.

### Bilgi gereksinimleri
- Java'da nesne yönelimli programlama.  
- Temel dosya I/O işlemleri.

## GroupDocs.Search for Java'ı kurma

### Kurulum bilgileri
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

**Direct download** – ayrıca en son JAR dosyasını [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Lisans edinimi
- **Ücretsiz deneme:** Lisans olmadan temel özellikleri test edin.  
- **Geçici lisans:** Değerlendirme sırasında deneme yeteneklerini genişletir.  
- **Satın alma:** Üretim kullanımı ve tam özellik seti için gereklidir.

#### Temel başlatma ve kurulum
Create an `Index` instance, then add documents to be searchable:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## Arama indeksinize eşanlamlıları nasıl eklersiniz

### Özellik 1: bir indeks oluşturma ve indeksleme
The `Index` class represents a searchable collection of documents stored on disk or in memory.  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### Özellik 2: bir kelime için eşanlamlıları alma
`SynonymDictionary` manages synonym groups and provides methods to query synonyms for a term.  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Özellik 3: eşanlamlı grupları alma
`SynonymDictionary.getGroups()` returns a list of all defined synonym groups with their identifiers.  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### Özellik 4: eşanlamlı sözlük girişlerini yönetme
`add(word, synonym)` inserts a new synonym relationship into the dictionary. `clear()` removes all entries, and `remove(word)` deletes a specific term from the dictionary.  

```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### Özellik 5: eşanlamlıları bir dosyaya dışa aktarma
`exportDictionary(path)` writes the current synonym dictionary to a binary .dat file at the specified location.  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### Özellik 6: bir dosyadan eşanlamlıları içe aktarma
`importDictionary(path)` loads a previously exported .dat file into the synonym dictionary.  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### Özellik 7: eşanlamlı desteğiyle arama gerçekleştirme
`SearchOptions` configures query behavior, including whether synonym expansion is enabled. `setUseSynonymSearch(true)` turns on synonym‑aware searching for the upcoming query.  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## Eşanlamlılarla nasıl arama yapılır
`Index`'inizi yükleyin, eşanlamlı aramayı etkinleştirin ve bir sorgu çalıştırın. Motor, oluşturduğunuz veya içe aktardığınız eşanlamlı sözlüğü kullanarak sorguyu otomatik olarak genişletir ve ilgili tüm terimler için eşleşmeler döndürür.

## Eşanlamlı sözlüğü nasıl içe aktarılır
Başka bir ortamda hazırlanmış bir `.dat` dosyanız zaten varsa, sadece `importDictionary(path)` çağırın. Bu, sözlükleri geliştirme, test ve üretim sunucuları arasında senkronize etmek için idealdir.

## Eşanlamlı grupları nasıl yönetilir
Eşanlamlı gruplar, bir dizi terimi tek bir mantıksal varlık olarak ele almanızı sağlar. Grupları ekleme, temizleme veya alma işlemleri, yukarıdaki kod parçacıklarında gösterildiği gibi `SynonymDictionary` API'si aracılığıyla yapılır.

## Arama indeksini nasıl optimize edersiniz
- **Kullanılmayan girişleri düzenli olarak temizleyin:** Toplu güncellemelerden önce `clear()` kullanın.  
- **JVM yığınını ayarlayın:** Büyük sözlükler daha fazla bellek gerektirebilir; `-Xmx` parametresini buna göre artırın.  
- **Kütüphaneyi güncel tutun:** Yeni sürümler performans iyileştirmeleri ve hata düzeltmeleri içerir.

## Pratik uygulamalar
1. **İçerik yönetim sistemleri (CMS):** Kullanıcılar alternatif terminoloji kullansalar bile makaleleri bulur.  
2. **E‑ticaret platformları:** Ürün aramaları “laptop” ve “notebook” gibi eşanlamlılara toleranslı hale gelir.  
3. **Belge depoları:** Hukuki veya tıbbi arşivler, alana özgü eşanlamlı gruplardan faydalanarak profesyoneller için keşfedilebilirliği artırır.

## Performans dikkate alması gerekenler
- **İndeks depolamayı optimize edin:** Eski verileri kaldırmak için periyodik olarak indeksi yeniden oluşturun.  
- **Bellek kullanımını yönetin:** Büyük eşanlamlı dosyaları yüklerken yığın tüketimini izleyin; 500 MB bir sözlük genellikle 64‑bit JVM'de 2 GB yığın gerektirir.  
- **Düzenli güncellemeler:** Hata düzeltmeleri ve hız artışları için en son GroupDocs.Search sürümünü kullanın.

## Yaygın sorunlar ve çözümler

| Sorun | Muhtemel neden | Çözüm |
|-------|----------------|-------|
| Eşanlamlı eşleşmeleri görünmüyor | `setUseSynonymSearch(true)` ayarlanmamış veya sözlük içe aktarılmamış | Seçeneğin etkin olduğundan ve sözlük dosyasının mevcut olduğundan emin olun. |
| İçe aktarım sırasında bellek yetersizliği hataları | Çok büyük `.dat` dosyası JVM yığınını aşıyor | `-Xmx` yığın boyutunu artırın veya daha küçük partiler halinde içe aktarın. |
| Sonuçlarda yinelenen girişler | Aynı terim birden fazla eşanlamlı grubunda yer alıyor | Çakışan grupları `clear()` ardından `addRange()` kullanarak birleştirin. |

## Sıkça Sorulan Sorular

**S: GroupDocs.Search kullanmak için minimum sistem gereksinimi nedir?**  
C: Uyumlu bir JDK (Java 8 veya daha yeni) ile herhangi bir modern işletim sistemi yeterlidir.

**S: Eşanlamlı sözlüğümü ne sıklıkta yenilemeliyim?**  
C: Yeni terminoloji ortaya çıktıkça güncelleyin—temiz bir yenileme için `clear()` ardından `addRange()` kullanın.

**S: GroupDocs.Search'i lisans satın almadan çalıştırabilir miyim?**  
C: Ücretsiz deneme değerlendirme için çalışır, ancak üretim dağıtımları için lisans gereklidir.

**S: Büyük veri setlerini indekslemek için en iyi uygulamalar nelerdir?**  
C: Veriyi mantıksal partilere bölün, yığın kullanımını izleyin ve düzenli indeks bakımı planlayın.

**S: Beklenen eşanlamlı eşleşmeleri göremiyorum—ne kontrol etmeliyim?**  
C: Sözlüğün doğru şekilde içe aktarıldığını, `setUseSynonymSearch(true)`'ın etkin olduğunu ve terimlerin eşanlamlı gruplarında bulunduğunu doğrulayın.

**Kaynaklar**  
- [Dokümantasyon](https://docs.groupdocs.com/search/java/)  
- [API Referansı](https://reference.groupdocs.com/search/java)  
- [GroupDocs.Search for Java'ı İndir](https://releases.groupdocs.com/search/java/)  
- [GitHub Deposu](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/search/10)  
- [Geçici Lisans Alımı](https://purchase.groupdocs.com/temporary-license/) 

---

**Son Güncelleme:** 2026-10-17  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [GroupDocs Search Java İndeksi Oluşturma ve Yönetme](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Java Tam Metin Arama Kütüphanesi – GroupDocs.Search ile İndeksi Optimize Etme](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Java Bulanık Arama: GroupDocs.Search ile Belgeleri İndekse Ekleme](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}