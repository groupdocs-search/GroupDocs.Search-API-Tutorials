---
date: 2026-10-17
description: GroupDocs.Search kullanarak fuzzy search java nasıl etkinleştirileceğini
  öğrenin; installation, licensing, configuration ve fuzzy matching ile searchable
  solution oluşturmayı kapsar.
keywords:
- enable fuzzy search java
- GroupDocs.Search Java
- fuzzy matching Java
lastmod: 2026-10-17
og_description: GroupDocs.Search ile fuzzy search java dakikalar içinde etkinleştirin.
  Bu öğretici, installation, licensing, fuzzy matching configuration ve indexing documents
  for robust search adımlarını size gösterir.
og_image_alt: Guide showing how to enable fuzzy search java using GroupDocs.Search
og_title: GroupDocs.Search ile fuzzy search java etkinleştirme – Hızlı rehber
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to enable fuzzy search java using GroupDocs.Search, covering
    installation, licensing, configuration, and building a searchable solution with
    fuzzy matching.
  headline: How to enable fuzzy search java with GroupDocs.Search – Getting started
    tutorial
  type: TechArticle
- description: Learn how to enable fuzzy search java using GroupDocs.Search, covering
    installation, licensing, configuration, and building a searchable solution with
    fuzzy matching.
  name: How to enable fuzzy search java with GroupDocs.Search – Getting started tutorial
  steps:
  - name: add GroupDocs.Search to your project
    text: Add the GroupDocs.Search dependency to your `pom.xml` (Maven) or `build.gradle`
      (Gradle). This makes the library available on the classpath for compilation
      and runtime.
  - name: apply your license
    text: '`License` loads and validates the GroupDocs.Search license file, unlocking
      all premium features such as fuzzy matching. Create a `License` instance and
      point it at the `.lic` file you received from GroupDocs.'
  - name: initialize the index settings
    text: Define a folder on disk where the index files will be stored. You can also
      configure case‑sensitivity, stop‑words, and other indexing options at this stage.
  - name: index your documents
    text: The `Indexer` class reads files, extracts searchable text, and writes the
      data to the index folder. It automatically detects the file type, so you can
      feed a mix of PDFs, DOCX, XLSX, and images without extra code.
  - name: enable fuzzy search in your query
    text: '`SearchOptions` configures parameters for a search operation, such as fuzzy
      matching and filters. When you create a `SearchOptions` object, set its `fuzzySearch`
      flag to `true`. You may also adjust the `fuzzinessLevel` (e.g., `2`) to control
      how tolerant the engine should be.'
  - name: perform a search query
    text: The `search` method executes the query against the index and returns matching
      results. Call the `search` method with the query string and the configured `SearchOptions`.
      The method returns a list of `SearchResult` objects, each containing a document
      path and a relevance score that reflects fuzzy mat
  - name: review results
    text: '`SearchResult` represents a single document match, including its path and
      relevance score. Iterate over the `SearchResult` collection, display file names,
      and optionally highlight matched terms in your UI. Fuzzy matches typically have
      a slightly lower relevance score than exact matches, which you ca'
  type: HowTo
- questions:
  - answer: Yes, the library is platform‑independent and works on any operating system
      that supports Java.
    question: Can I run GroupDocs.Search on a Linux server?
  - answer: Invoke the `Indexer` again with the new files; the SDK merges them into
      the current index automatically.
    question: How do I add new files to an existing index?
  - answer: Yes, set a folder filter in `SearchOptions` before executing the query.
    question: Is it possible to limit search results to a specific folder?
  - answer: The API switches to evaluation mode with limited features; replace the
      temporary key with a permanent license to regain full functionality.
    question: What happens after the temporary license expires?
  - answer: Absolutely—enable the `fuzzySearch` flag in `SearchOptions` to retrieve
      results that contain minor spelling variations.
    question: Does GroupDocs.Search support fuzzy search?
  type: FAQPage
tags:
- fuzzy search
- GroupDocs.Search
- Java search library
- document indexing
title: GroupDocs.Search ile fuzzy search java nasıl etkinleştirilir – Başlangıç öğreticisi
type: docs
url: /tr/java/getting-started/
weight: 1
---

# GroupDocs.Search ile Java'da bulanık aramayı etkinleştirme – Başlangıç öğreticisi

Bu kapsamlı rehberde, GroupDocs.Search kütüphanesini kullanarak **Java'da fuzzy search** öğreneceksiniz. SDK'yı kurma, lisans uygulama, fuzzy eşleşmeyi yapılandırma ve çeşitli belge türlerini indeksleme adımlarını göstereceğiz, böylece kullanıcılarınız yazım hataları yapsalar ya da alternatif terimler kullansalar bile ilgili içeriği bulabilir. Öğreticinin sonunda, 15 dakikadan kısa bir sürede tamamen işlevsel bir arama çözümüne sahip olacaksınız.

## Hızlı cevaplar
- **İlk adım nedir?** Maven `pom.xml` veya Gradle `build.gradle` dosyanıza GroupDocs.Search bağımlılığını ekleyin.  
- **Lisans gerekir mi?** Evet—geçici bir geliştirme lisansı test için çalışır; üretim dağıtımları için kalıcı bir lisans gereklidir.  
- **Hangi IDE en iyisidir?** Maven veya Gradle'ı destekleyen herhangi bir Java IDE (IntelliJ IDEA, Eclipse, VS Code).  
- **PDF, Word ve Excel dosyalarını indeksleyebilir miyim?** Kesinlikle—GroupDocs.Search yerel olarak PDF, DOCX, XLSX, PPTX ve birçok görüntü türü dahil 50'den fazla dosya formatını destekler.  
- **Bulanık aramayı nasıl etkinleştiririm?** Sorguyu çalıştırmadan önce bir `SearchOptions` örneğinde `fuzzySearch` özelliğini `true` olarak ayarlayın.  
- **Tüm kurulum ne kadar sürer?** Yeni bir proje için genellikle 15 dakikadan az.

## GroupDocs.Search'te “fuzzy search'ü etkinleştirme” nedir?
Bulanık aramayı etkinleştirmek, motorun sorgu terimlerini eşleştirirken küçük yazım farklılıklarını, eksik karakterleri veya yer değiştirmiş harfleri tolere etmesini sağlar. Bu özellik, kullanıcı yazım hataları, OCR‑ile oluşturulmuş metinler veya çok dilli içerik gibi senaryolarda keşfedilebilirliği büyük ölçüde artırır; çünkü arama algoritması tam anahtar kelime bulunmasa bile ilgili belgeleri döndürür.

## Neden Java için GroupDocs.Search yapılandırmalı ve fuzzy search'ü etkinleştirmelisiniz?
Az kodla anında, üretime hazır arama yetenekleri elde ederken aynı zamanda daha akıcı bir kullanıcı deneyimi sunarsınız. GroupDocs.Search belgeleri tamamen belleğe yüklemeden indeksler, **50+ giriş ve çıkış formatını** destekler ve uygun donanımda **milyonlarca dosyaya** ölçeklenebilir. Fuzzy search'ü etkinleştirmek, başarısız sorguları **%80**'e kadar azaltan bir tolerans katmanı ekler; böylece hatalı yazılmış kullanıcı girdileri ekstra geliştirme çabası olmadan doğru sonuçlara dönüşür.

## Önkoşullar
- Java Development Kit (JDK) 8 veya daha yeni bir sürüm.  
- Bağımlılık yönetimi için Maven 3 veya Gradle 5.  
- Geçici veya kalıcı bir GroupDocs.Search lisans anahtarı.  

## Adım adım kılavuz

### Adım 1: Projenize GroupDocs.Search ekleyin
GroupDocs.Search bağımlılığını `pom.xml` (Maven) veya `build.gradle` (Gradle) dosyanıza ekleyin. Bu, kütüphanenin derleme ve çalışma zamanı için sınıf yolunda bulunmasını sağlar.

### Adım 2: Lisansınızı uygulayın
`License` sınıfı, GroupDocs.Search lisans dosyasını yükler ve doğrular, fuzzy eşleşme gibi tüm premium özelliklerin kilidini açar. Bir `License` örneği oluşturun ve GroupDocs'tan aldığınız `.lic` dosyasına yönlendirin.

### Adım 3: İndeks ayarlarını başlatın
İndeks dosyalarının saklanacağı bir klasör tanımlayın. Bu aşamada ayrıca büyük/küçük harf duyarlılığı, durdurma kelimeleri ve diğer indeksleme seçeneklerini yapılandırabilirsiniz.

### Adım 4: Belgelerinizi indeksleyin
`Indexer` sınıfı dosyaları okur, aranabilir metni çıkarır ve verileri indeks klasörüne yazar. Dosya tipini otomatik olarak algılar, böylece ek kod yazmadan PDF, DOCX, XLSX ve görüntü karışımını besleyebilirsiniz.

### Adım 5: Sorgunuzda fuzzy search'ü etkinleştirin
`SearchOptions` bir arama işlemi için parametreleri yapılandırır, örneğin fuzzy eşleşme ve filtreler.  
Bir `SearchOptions` nesnesi oluşturduğunuzda, `fuzzySearch` bayrağını `true` olarak ayarlayın. Ayrıca motorun ne kadar toleranslı olacağını kontrol etmek için `fuzzinessLevel` (ör. `2`) değerini ayarlayabilirsiniz.

### Adım 6: Bir arama sorgusu gerçekleştirin
`search` metodu, sorguyu indeks üzerinde çalıştırır ve eşleşen sonuçları döndürür.  
`search` metodunu sorgu dizesi ve yapılandırılmış `SearchOptions` ile çağırın. Metod, her biri belge yolunu ve fuzzy eşleşmeleri yansıtan bir alaka skorunu içeren `SearchResult` nesnelerinin bir listesini döndürür. `SearchResult`, yol ve alaka skoru dahil tek bir belge eşleşmesini temsil eder.

### Adım 7: Sonuçları gözden geçirin
`SearchResult`, yol ve alaka skoru dahil tek bir belge eşleşmesini temsil eder.  
`SearchResult` koleksiyonunu döngüyle gezerek dosya adlarını gösterin ve isteğe bağlı olarak UI'nizde eşleşen terimleri vurgulayın. Fuzzy eşleşmeler genellikle tam eşleşmelere göre biraz daha düşük bir alaka skoruna sahiptir; bu skoru sonuçları sıralamak için kullanabilirsiniz.

## Yaygın sorunlar ve çözümler
- **Lisans tanınmıyor** – Lisans dosyası yolunun doğru olduğundan ve dosyanın kullandığınız GroupDocs.Search sürümüyle eşleştiğinden emin olun.  
- **Eksik belge formatları** – Daha az yaygın dosya tiplerini desteklemek için isteğe bağlı `groupdocs-conversion` eklentisini kurun.  
- **Fuzzy search sonuç döndürmüyor** – `fuzzySearch` bayrağının `true` olduğundan ve sorgu uzunluğunun minimum karakter gereksinimini (genellikle üç karakter) karşıladığından emin olun.  
- **Performans darboğazları** – Artımlı indeksleme kullanın ve okuma/yazma hızını artırmak için indeks klasörünü bir SSD'de tutun.  

## Sıkça sorulan sorular

**S: GroupDocs.Search'ı bir Linux sunucusunda çalıştırabilir miyim?**  
C: Evet, kütüphane platform bağımsızdır ve Java destekleyen herhangi bir işletim sisteminde çalışır.

**S: Mevcut bir indekse yeni dosyalar nasıl eklenir?**  
C: `Indexer`'ı yeni dosyalarla tekrar çağırın; SDK bunları mevcut indekse otomatik olarak birleştirir.

**S: Arama sonuçlarını belirli bir klasörle sınırlamak mümkün mü?**  
C: Evet, sorguyu çalıştırmadan önce `SearchOptions` içinde bir klasör filtresi ayarlayın.

**S: Geçici lisans süresi dolduğunda ne olur?**  
C: API, sınırlı özelliklere sahip değerlendirme moduna geçer; tam işlevselliği geri kazanmak için geçici anahtarı kalıcı bir lisansla değiştirin.

**S: GroupDocs.Search fuzzy search'ü destekliyor mu?**  
C: Kesinlikle—küçük yazım farklılıkları içeren sonuçları almak için `SearchOptions` içinde `fuzzySearch` bayrağını etkinleştirin.

**S: Fuzzy search'ü tarih aralıkları gibi diğer filtrelerle birleştirebilir miyim?**  
C: Evet, fuzzy eşleşmeyi aktif tutarken `SearchOptions`'a ek filtreler ekleyebilirsiniz.

## Ek kaynaklar

### Mevcut öğreticiler

### [GroupDocs.Search'ı Java için dağıtın: Kapsamlı Kurulum Kılavuzu](./deploy-groupdocs-search-java-setup-guide/)
Bu adım adım kılavuzla GroupDocs.Search'ı Java için nasıl dağıtacağınızı ve yapılandıracağınızı öğrenin. Projelerinizde belge indeksleme ve arama yeteneklerini geliştirin.

### Faydalı bağlantılar
- [GroupDocs.Search for Java Belgeleri](https://docs.groupdocs.com/search/java/)
- [GroupDocs.Search for Java API Referansı](https://reference.groupdocs.com/search/java/)
- [GroupDocs.Search for Java'ı İndir](https://releases.groupdocs.com/search/java/)
- [GroupDocs.Search Forumu](https://forum.groupdocs.com/c/search)
- [Ücretsiz Destek](https://forum.groupdocs.com/)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-10-17  
**Test Edilen:** GroupDocs.Search 23.12 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [Java Lisansını Ayarla – GroupDocs.Search Java Konfigürasyon Kılavuzu](/search/java/licensing-configuration/)
- [Java Fuzzy Search: Belgeleri GroupDocs.Search ile İndekse Ekle](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)
- [Java Groupdocs Search Yazım Düzeltme Öğreticisi](/search/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/)