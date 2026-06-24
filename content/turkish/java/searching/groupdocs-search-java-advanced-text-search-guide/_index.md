---
date: '2026-05-22'
description: GroupDocs.Search Java ile Java bulanık aramayı öğrenin, belgeleri dizine
  ekleyin, gelişmiş metin aramayı etkinleştirin ve birden fazla dosya türünü verimli
  bir şekilde yönetin.
keywords:
- java fuzzy search
- advanced text search java
- search file types java
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn java fuzzy search with GroupDocs.Search Java, add documents to
    index, enable advanced text search, and handle multiple file types efficiently.
  headline: 'Java Fuzzy Search: Add Documents to Index with GroupDocs.Search'
  type: TechArticle
- description: Learn java fuzzy search with GroupDocs.Search Java, add documents to
    index, enable advanced text search, and handle multiple file types efficiently.
  name: 'Java Fuzzy Search: Add Documents to Index with GroupDocs.Search'
  steps:
  - name: '**Free Trial** – explore the API without cost.'
    text: '**Free Trial** – explore the API without cost.'
  - name: '**Temporary License** – extend the trial period for deeper testing.'
    text: '**Temporary License** – extend the trial period for deeper testing.'
  - name: '**Purchase** – obtain a commercial license for production use.'
    text: '**Purchase** – obtain a commercial license for production use.'
  - name: '**Corporate Document Management** – Quickly locate policies, contracts,
      or HR manuals across thousands of files.'
    text: '**Corporate Document Management** – Quickly locate policies, contracts,
      or HR manuals across thousands of files.'
  - name: '**Legal Research** – Find precedent cases even when the exact phrasing
      differs, thanks to word‑form search.'
    text: '**Legal Research** – Find precedent cases even when the exact phrasing
      differs, thanks to word‑form search.'
  - name: '**E‑commerce Catalogs** – Allow shoppers to search product descriptions
      using varied terminology, improving conversion rates.'
    text: '**E‑commerce Catalogs** – Allow shoppers to search product descriptions
      using varied terminology, improving conversion rates.'
  type: HowTo
- questions:
  - answer: It means loading source files into a searchable data structure that GroupDocs.Search
      can query.
    question: What does “add documents to index” mean?
  - answer: GroupDocs.Search for Java 25.4 (or newer) includes all features demonstrated
      here.
    question: Which library version is required?
  - answer: A free trial works for development; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—enable `setUseWordFormsSearch(true)` in `SearchOptions`.
    question: Can I search different word forms?
  - answer: No, you can also download the JAR directly (see the Direct Download link).
    question: Is Maven the only way to install?
  type: FAQPage
title: 'Java Bulanık Arama: GroupDocs.Search ile Belgeleri Dizin''e Ekleyin'
type: docs
url: /tr/java/searching/groupdocs-search-java-advanced-text-search-guide/
weight: 1
---

# Java Fuzzy Search: Dizin'e Belge Ekleme - GroupDocs.Search

## Hızlı Yanıtlar
- **add documents to index** ne anlama geliyor? Bu, kaynak dosyaların GroupDocs.Search'in sorgulayabileceği bir aranabilir veri yapısına yüklenmesi anlamına gelir.  
- **Hangi kütüphane sürümü gereklidir?** GroupDocs.Search for Java 25.4 (veya daha yeni) burada gösterilen tüm özellikleri içerir.  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme çalışır; üretim kullanımı için ticari lisans gereklidir.  
- **Farklı kelime biçimlerini arayabilir miyim?** Evet—`SearchOptions` içinde `setUseWordFormsSearch(true)` etkinleştirin.  
- **Maven kurulumun tek yolu mu?** Hayır, JAR'ı doğrudan da indirebilirsiniz (Doğrudan İndirme bağlantısına bakın).

## “add documents to index” nedir?
Belge ekleme, kaynak dosyaları taramayı, aranabilir metni çıkarmayı ve bu bilgiyi hızlı arama sağlayan yapılandırılmış bir formata kaydetmeyi ifade eder. GroupDocs.Search, birçok dosya türünü kutudan çıkar çıkmaz işler, böylece iş mantığınıza odaklanırsınız, ayrıştırma ile uğraşmazsınız. Oluşturulan dizin, disk üzerinde ya da bellek içinde saklanabilir; böylece her sorgu çalıştırıldığında orijinal dosyalar yeniden okunmaz ve hızlı geri getirme sağlanır.

## Neden gelişmiş metin arama Java tekniklerini kullanmalı?
Dizininizi bir kez yükleyin ve ardından dosyaları yeniden işleme gerektirmeden bulanık, büyük/küçük harf duyarsız veya yakınlık sorguları çalıştırın. Bu tekniklerin etkinleştirilmesi, gerçek dünyadaki testlerde geri getirme oranını %30’a kadar artırır; kullanıcılar tam kelime ya da yazım hatası yaptıklarında bile ilgili sonuçları bulabilir.

## Önkoşullar
- **Gerekli Kütüphaneler**: GroupDocs.Search for Java 25.4.  
- **Ortam Kurulumu**: Java JDK 8 veya daha yeni, Maven (veya manuel JAR yönetimi).  
- **Bilgi Önkoşulları**: Temel Java programlama ve Maven bağımlılık yönetimi.

## GroupDocs.Search for Java Kurulumu
Kod yazmaya başlamadan önce, kütüphanenin projenizde mevcut olduğundan emin olun.

### Maven Kurulumu
`pom.xml` dosyası, bağımlılıkların bildirildiği Maven proje tanımlayıcısıdır.

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
Maven kullanmak istemiyorsanız, resmi sayfadan en yeni JAR'ı indirebilirsiniz: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

Detaylı kullanım talimatları için [GroupDocs Documentation](https://docs.groupdocs.com/search/java/) sayfasına bakın.

### Lisans Edinme Adımları
1. **Ücretsiz Deneme** – API'yi ücretsiz keşfedin.  
2. **Geçici Lisans** – daha derin testler için deneme süresini uzatın.  
3. **Satın Alma** – üretim kullanımı için ticari lisans edinin.

## Java'da Desteklenen Arama Dosya Türleri
GroupDocs.Search **50+ giriş ve çıkış formatını** destekler—DOCX, PDF, PPTX, XLSX, TXT, HTML ve yaygın görüntü türleri dahil—bu sayede işletmenizin kullandığı neredeyse her belgeyi dizine ekleyebilirsiniz.

## Adım‑Adım Uygulama Kılavuzu

### 1. Bir Dizin Oluşturun ve Yapılandırın
`Index` sınıfı, disk üzerinde saklanan aranabilir bir deponun en üst düzey nesnesidir.

#### Genel Bakış
Dizin dosyalarını tutacak bir klasör oluşturacağız.

#### Code
```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/SearchForDifferentWordForms";
Index index = new Index(indexFolder);
```

*Explanation*: `Index` yapıcısı, tüm dizin verilerinin kalıcı olarak saklanacağı bir klasöre işaret eder. `YOUR_DOCUMENT_DIRECTORY` ifadesini makinenizdeki gerçek yol ile değiştirin.

### 2. Belgeleri Dizin'e Nasıl Eklenir
`add` metodu, bir klasörü özyinelemeli olarak tarar, metni çıkarır ve dizine kaydeder.

#### Genel Bakış
GroupDocs.Search belirtilen dizini tarar ve bulduğu her desteklenen dosya türünü indeksler.

#### Code
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
index.add(documentsFolder);
```

*Explanation*: Yolun doğru olduğundan ve uygulamanın okuma izinlerine sahip olduğundan emin olun. Metod, bellek kullanımını düşük tutmak için dosyaları toplu işleyerek çalışır.

### 3. Kelime Biçimleri için Arama Seçeneklerini Yapılandırma
`SearchOptions` sorguların nasıl işlendiğini kontrol eden parametreleri tutar.

#### Genel Bakış
`SearchOptions` içinde word‑form (bulanık) aramayı etkinleştireceğiz.

#### Code
```java
import com.groupdocs.search.SearchOptions;

SearchOptions options = new SearchOptions();
options.setUseWordFormsSearch(true); // Enables search for different grammatical variations of words.
```

*Explanation*: `setUseWordFormsSearch(true)` ayarı, motorun “wish”, “wished” ve “wishes” gibi bilinen çekim biçimlerini sorguya eklemesini sağlar, böylece geri getirme artar.

### 4. Aramayı Gerçekleştirme
`SearchResult` eşleşen belgelerin listesini ve alıntı snippet'lerini içerir.

#### Genel Bakış
“wished” kelimesi için arama yapacak ve eşleşen belgeleri getireceğiz.

#### Code
```java
import com.groupdocs.search.SearchResult;

String query = "wished";
SearchResult result = index.search(query, options);
```

*Explanation*: `search` metodu, tanımladığımız seçeneklerle indekslenmiş içeriğe sorguyu çalıştırır. Dönen `SearchResult` her bir eşleşme için belge referansları ve vurgulanmış snippet'ler sunar.

## Yaygın Sorunlar ve Sorun Giderme
- **Yanlış yollar** – `indexFolder` ve `documentsFolder`'ı yazım hataları ve doğru erişim izinleri için iki kez kontrol edin.  
- **Desteklenmeyen dosya formatları** – Belgelerinizin GroupDocs.Search dokümantasyonunda listelenen 50+ format arasında olduğundan emin olun.  
- **Performans yavaşlığı** – Büyük veri kümeleri için, dizini toplu olarak oluşturun, JVM yığın kullanımını izleyin ve dizini SSD depolama üzerinde tutun.

## Pratik Uygulamalar
1. **Kurumsal Belge Yönetimi** – Binlerce dosya arasında politikaları, sözleşmeleri veya İK kılavuzlarını hızlıca bulun.  
2. **Hukuki Araştırma** – Kelime biçimi araması sayesinde tam ifadeler farklı olsa bile emsal davaları bulun.  
3. **E‑ticaret Katalogları** – Alışveriş yapanların ürün açıklamalarını farklı terimlerle aramasına izin verin, dönüşüm oranlarını artırın.

## Performans İpuçları
- Yeni belgeler eklendiğinde veya mevcut belgeler değiştiğinde yalnızca yeniden dizin oluşturun.  
- Büyük dizinler için yeterli yığın belleği ayırmak amacıyla Java’nın `-Xmx` bayrağını kullanın (örnek: `-Xmx4g`).  
- Periyodik olarak `index.optimize()` (varsa) çağırarak dizin dosyalarını sıkıştırın ve disk I/O'yu azaltın.

## Sonuç
Artık **add documents to index** işlemini, java fuzzy search'i etkinleştirmeyi ve GroupDocs.Search for Java'ı ince ayar yapmayı biliyorsunuz. Bu teknikler, herhangi bir belge koleksiyonunda duyarlı, özellik‑zengin arama deneyimleri oluşturmanızı sağlar.

### Sonraki Adımlar
- Bulanık eşleştirme ve özel sıralama ile deney yapın.  
- Arama modülünü ön‑uç tüketimi için bir REST API'ye entegre edin.  
- Dil‑spesifik analizörleri yapılandırarak çok‑dilli desteği keşfedin.

## Sıkça Sorulan Sorular

**Q1: GroupDocs.Search hangi formatları destekliyor?**  
A1: DOCX, PDF, PPTX, XLSX, TXT, HTML ve yaygın görüntü türleri dahil 50+ formatı destekler. Tam liste için resmi dokümantasyona bakın.

**Q2: Dizini yeni belgelerle nasıl güncellerim?**  
A2: `index.add(newDocumentsFolder)` metodunu tekrar çağırın; kütüphane yalnızca yeni veya değişmiş dosyaları ekler, mevcut girişleri dokunulmaz bırakır.

**Q3: Arama sorgularını daha da özelleştirebilir miyim?**  
A3: Evet—`SearchOptions` bulanık arama, büyük/küçük harf duyarlılığı, sonuç sayfalama ve özel sıralama algoritmaları için seçenekler sunar.

**Q4: Aramalarım yavaş—ne yapabilirim?**  
A4: Dizini hızlı SSD depolama üzerinde tutun, JVM yığın boyutunu (`-Xmx`) artırın ve gereksiz büyük dosyaları indekslemekten kaçının. Ayrıca, yalnızca gerektiğinde kelime‑biçim aramasını etkinleştirin.

**Q5: Topluluktan nereden yardım alabilirim?**  
A5: Resmi destek forumunu kullanın: [GroupDocs Support Forum](https://forum.groupdocs.com/c/search/10).

**Son Güncelleme:** 2026-05-22  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs  

## İlgili Öğreticiler

- [GroupDocs.Search Java - Tarih Aralığı Arama ve Gelişmiş Özellikler](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Java'da GroupDocs.Search Kullanarak Eş Anlamlı Kelimeler Nasıl Eklenir – Kapsamlı Rehber](/search/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/)
- [Java'da Parça‑Tabanlı Arama ile Belgeleri Dizin'e Ekleme](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)