---
date: '2026-09-02'
description: 'Java''da GroupDocs.Search ile formları nasıl oluşturulur: doğru arama
  ve metin analizi için özel bir word‑forms sağlayıcısı oluşturmayı öğrenin.'
keywords:
- how to generate forms
- GroupDocs.Search Java
- word forms provider
- singular plural Java
lastmod: '2026-09-02'
og_description: 'Java''da GroupDocs.Search ile formları nasıl oluşturulur: doğru arama
  ve metin analizi için özel bir word‑forms sağlayıcısı oluşturmayı öğrenin.'
og_image_alt: Guide showing how to generate forms in Java using GroupDocs.Search
og_title: Java'da GroupDocs.Search ile formları nasıl oluşturulur
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: 'How to generate forms in Java with GroupDocs.Search: learn to create
    a custom word‑forms provider for accurate search and text analysis.'
  headline: How to generate forms in Java with GroupDocs.Search
  type: TechArticle
- description: 'How to generate forms in Java with GroupDocs.Search: learn to create
    a custom word‑forms provider for accurate search and text analysis.'
  name: How to generate forms in Java with GroupDocs.Search
  steps:
  - name: '**Free trial:** Sign up for a trial to explore core features.'
    text: '**Free trial:** Sign up for a trial to explore core features.'
  - name: '**Temporary license:** Request a temporary key for extended testing.'
    text: '**Temporary license:** Request a temporary key for extended testing.'
  - name: '**Purchase:** Obtain a commercial license for unrestricted production use.'
    text: '**Purchase:** Obtain a commercial license for unrestricted production use.'
  - name: '**Search engines:** Users typing “mouse” should also find documents containing
      “mice”. A provider can generate such irregular forms.'
    text: '**Search engines:** Users typing “mouse” should also find documents containing
      “mice”. A provider can generate such irregular forms.'
  - name: '**Text analysis tools:** Sentiment or entity extraction becomes more reliable
      when all word variants are recognised.'
    text: '**Text analysis tools:** Sentiment or entity extraction becomes more reliable
      when all word variants are recognised.'
  - name: '**Content management systems:** Automatic tag generation can include plural
      synonyms, improving SEO and internal linking.'
    text: '**Content management systems:** Automatic tag generation can include plural
      synonyms, improving SEO and internal linking.'
  type: HowTo
- questions:
  - answer: It’s a powerful library that offers full‑text search, indexing, and linguistic
      features—including the ability to plug in custom word‑form providers.
    question: What is GroupDocs.Search for Java?
  - answer: It generates alternative forms by applying simple suffix‑based rules (removing
      “s/es”, converting “y” to “is”, and appending “s/es”).
    question: How does the SimpleWordFormsProvider work?
  - answer: Absolutely. Modify the `getWordForms` method to include irregular forms,
      locale‑specific rules, or integration with external dictionaries.
    question: Can I customize the word form generation rules?
  - answer: Search engines, text‑analysis pipelines, and CMS platforms benefit from
      recognising singular/plural variants.
    question: What are some common applications for this feature?
  - answer: Yes—while a trial lets you explore the API, a purchased license removes
      usage limits and grants support.
    question: Do I need a commercial license for production use?
  type: FAQPage
tags:
- word forms
- GroupDocs.Search
- Java
- search indexing
- text analysis
title: Java'da GroupDocs.Search ile formları nasıl oluşturulur
type: docs
url: /tr/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Java'da GroupDocs.Search ile formları nasıl oluşturulur

Bu rehberde GroupDocs.Search API'sını kullanarak **Java'da formları nasıl oluşturacağınızı** öğreneceksiniz. Özel bir kelime‑formları sağlayıcısı oluşturarak arama veya metin‑analizi motorunuzun bir terimin tüm varyasyonlarını tanımasını sağlarsınız—örneğin “cat”, “cats”, “city” veya “citis”. Bu, geri çağırmayı büyük ölçüde artırırken kesinliği yüksek tutar.

## Hızlı cevaplar
- **Bir kelime formları sağlayıcısı ne yapar?** Verilen bir kelimenin alternatif biçimlerini (tekil, çoğul vb.) oluşturur, böylece aramalar tüm varyantlarla eşleşebilir.  
- **Hangi kütüphane gereklidir?** GroupDocs.Search for Java (sürüm 25.4 veya daha yeni).  
- **Lisans gerekiyor mu?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gereklidir.  
- **Hangi Java sürümü destekleniyor?** JDK 8 ve üzeri.  
- **Kaç satır kod gerekir?** Basit bir sağlayıcı uygulaması için yaklaşık 30 satır.

## “Kelime formları oluşturma sağlayıcısı” özelliği nedir?
Bir **kelime formları oluşturma sağlayıcısı**, `IWordFormsProvider` arayüzünü uygulayan özel bir sınıftır. `IWordFormsProvider`, sağlayıcıların arama motoruna alternatif kelime biçimlerini nasıl sunduğunu tanımlayan bir arayüzdür. Bir kelime alır ve tanımladığınız kurallara göre olası biçimlerin bir dizisini döndürür—tekil, çoğul veya diğer dilsel varyasyonlar. Bu, arama indeksinin “cat” ve “cats” gibi kelimeleri eşdeğer olarak ele almasını sağlar, geri çağırmayı artırırken kesinliği feda etmez.

## Kelime‑formları oluşturmak için neden GroupDocs.Search kullanılmalı?
GroupDocs.Search, yerleşik genişletilebilirlik sunar ve kendi sağlayıcınızı doğrudan indeksleme hattına bağlamanıza izin verir. **10 milyon belge**ye kadar indeksleri işleyebilir ve akış mimarisi sayesinde bellek kullanımını **500 MB** altında tutar; ayrıca sonuçları önbelleğe alarak milisaniyenin altında arama süreleri elde edebilirsiniz.

## Önkoşullar
- **Maven** yüklü ve makinenizde JDK 8 veya daha yeni bir sürüm kurulu.  
- Java geliştirme ve Maven’in `pom.xml` yapılandırması hakkında temel bilgi.  
- GroupDocs.Search Java kütüphanesine erişim (sürüm 25.4 veya sonrası).

## Java için GroupDocs.Search Kurulumu

### Maven yapılandırması
`pom.xml` dosyanıza aşağıda gösterildiği gibi depo ve bağımlılığı ekleyin:

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
Alternatif olarak, resmi sürüm sayfasından en son JAR dosyasını indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans edinme adımları
1. **Ücretsiz deneme:** Temel özellikleri keşfetmek için bir deneme kaydı oluşturun.  
2. **Geçici lisans:** Uzatılmış test için geçici bir anahtar isteyin.  
3. **Satın al:** Sınırsız üretim kullanımı için ticari bir lisans edinin.

### Temel başlatma ve kurulum
Aşağıdaki kod parçacığı, belgeler ve kelime‑form mantığı eklemek için başlangıç noktası olan bir indeksin nasıl oluşturulacağını gösterir:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Uygulama rehberi

Aşağıda, basit tekil‑çoğul ve çoğul‑tekil dönüşümleri işleyen **kelime formları sağlayıcısı oluşturma** adımlarını anlatıyoruz.

### SimpleWordFormsProvider'ı Uygulama

#### Genel Bakış
`SimpleWordFormsProvider` sınıfı `IWordFormsProvider` arayüzünü uygular. Tanım açıklaması amacını netleştirir:

`SimpleWordFormsProvider`, indeksleme motoru için tekil‑çoğul varyasyonları sağlayan `IWordFormsProvider` arayüzünün özel bir uygulamasıdır.

#### Adım 1 – sınıf iskeletini oluşturun
`IWordFormsProvider` arayüzünü uygulayan bir sınıf tanımlayarak başlayın. İçe aktarma (import) ifadelerini değiştirmeyin:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Adım 2 – `getWordForms` metodunu uygulayın
Olası biçimlerin listesini oluşturan metodu ekleyin. Bu blok temel mantığı içerir; daha karmaşık kuralları kapsayacak şekilde sonradan genişletebilirsiniz.

`getWordForms` bir terim alır ve oluşturulan tüm varyasyonları içeren bir `String[]` döndürür.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Mantığın açıklaması
- **Tekilleştirme:** Yaygın çoğul eklerini (`es`, `s`) algılar ve temel kelimeyi tahmin etmek için bunları kaldırır.  
- **Çoğullaştırma:** `y` ile biten isimleri `is` ile değiştirerek işler; bu, birçok İngilizce kelime için çalışan basit bir kuraldır.  
- **Ek ekleme:** Önceki kontroller tarafından yakalanmamış olabilecek düzenli çoğul formları kapsamak için `s` ve `es` ekler.

#### Sorun giderme ipuçları
- **Büyük/küçük harf duyarlılığı:** Metod, karşılaştırma için `toLowerCase()` kullanır, böylece “Cats” ve “cats” aynı şekilde davranır.  
- **Köşe durumları:** Ek uzunluğundan kısa kelimeler, boş string döndürmeyi önlemek için yok sayılır.  
- **Performans:** Büyük sözlükler için sonuçları bir `ConcurrentHashMap` içinde önbelleğe almayı düşünün.

## Pratik uygulamalar

**Kelime formları oluşturma sağlayıcısı** uygulamak, çeşitli gerçek‑dünya senaryolarını artırabilir:

1. **Arama motorları:** “mouse” yazan kullanıcılar aynı zamanda “mice” içeren belgeleri de bulmalıdır. Bir sağlayıcı bu tür düzensiz biçimleri oluşturabilir.  
2. **Metin analiz araçları:** Tüm kelime varyantları tanındığında duygu veya varlık çıkarımı daha güvenilir olur.  
3. **İçerik yönetim sistemleri:** Otomatik etiket oluşturma, çoğul eşanlamlıları içerebilir, SEO ve iç bağlantıları iyileştirir.

## Performans değerlendirmeleri

Sağlayıcıyı bir üretim sistemine entegre ettiğinizde, aşağıdaki ipuçlarını aklınızda tutun:

- **Sık kullanılan biçimleri önbellekle:** Aynı kelimeyi tekrar tekrar yeniden hesaplamaktan kaçınmak için sonuçları bellekte saklayın.  
- **JVM yığınını izleyin:** Büyük indeksler bellek baskısını artırabilir; `-Xmx` parametresini buna göre ayarlayın.  
- **Verimli koleksiyonlar kullanın:** `ArrayList` küçük setler için uygundur, ancak binlerce form için `HashSet` kullanarak tekrarları hızlıca ortadan kaldırabilirsiniz.

**En iyi uygulamalar**
- Kütüphaneyi güncel tutarak performans yamalarından yararlanın.  
- Sağlayıcıyı gerçekçi sorgu yükleriyle profilleyerek darboğazları erken tespit edin.

## Sonuç

Artık GroupDocs.Search ile özel bir `SimpleWordFormsProvider` kullanarak **Java'da formları nasıl oluşturacağınızı** öğrendiniz. Bu hafif bileşen, arama sonuçlarının alaka düzeyini ve birçok uygulamada dilsel analiz doğruluğunu büyük ölçüde artırabilir.

**Sonraki adımlar**
- Daha karmaşık dil kuralları (düzensiz çoğullar, kök bulma) ile deneyler yapın.  
- Sağlayıcıyı bir indeksleme hattına entegre edin ve geri çağırma (recall) iyileştirmelerini ölçün.  
- Eşanlamlı sözlükler ve özel analizörler gibi diğer GroupDocs.Search özelliklerini keşfedin.

**Eylem çağrısı:** `SimpleWordFormsProvider`'ı bugün kendi projenize ekleyin ve arama deneyiminizi nasıl zenginleştirdiğini görün!

## SSS bölümü

**Q: GroupDocs.Search for Java nedir?**  
A: Tam metin arama, indeksleme ve dil özellikleri sunan güçlü bir kütüphanedir—özelleştirilmiş kelime‑form sağlayıcılarını bağlama yeteneği dahil.

**Q: SimpleWordFormsProvider nasıl çalışır?**  
A: Basit ek‑tabanlı kurallar (“s/es” kaldırma, “y”yi “is”e çevirme ve “s/es” ekleme) uygulayarak alternatif biçimler oluşturur.

**Q: Kelime formu oluşturma kurallarını özelleştirebilir miyim?**  
A: Kesinlikle. `getWordForms` metodunu düzensiz biçimler, bölge‑spesifik kurallar veya harici sözlüklerle entegrasyon ekleyecek şekilde değiştirin.

**Q: Bu özellik için yaygın uygulamalar nelerdir?**  
A: Arama motorları, metin‑analiz hatları ve CMS platformları tekil/çoğul varyantları tanıyarak fayda sağlar.

**Q: Üretim kullanımı için ticari lisans gerekiyor mu?**  
A: Evet—deneme sürümü API’yı keşfetmenizi sağlarken, satın alınan lisans kullanım sınırlamalarını kaldırır ve destek sunar.

---

**Son güncelleme:** 2026-09-02  
**Test edildi:** GroupDocs.Search 25.4 (Java)  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [Java Dil İşleme – GroupDocs.Search ile Eşanlamlı Sözlük Oluşturma](/search/java/dictionaries-language-processing/)
- [Java tam metin arama nasıl uygulanır: GroupDocs.Search ile indeks dizini oluşturma](/search/java/indexing/groupdocs-search-java-create-index/)
- [Java’da Regex Arama: Metin Belgesi Analizi için GroupDocs.Search Kullanımı](/search/java/searching/groupdocs-search-java-regex-tutorial/)