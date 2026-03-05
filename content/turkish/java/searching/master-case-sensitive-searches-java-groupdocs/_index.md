---
date: '2026-02-06'
description: GroupDocs.Search kullanarak Java'da belgeleri indekse eklemeyi ve büyük/küçük
  harfe duyarlı aramayı etkinleştirmeyi öğrenin, uygulamanızın doğruluğunu artırın.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Belgeleri indekse ekle: GroupDocs ile büyük/küçük harf duyarlı Java araması'
type: docs
url: /tr/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Dizin'e belge ekleme: Java'da GroupDocs ile Büyük/Küçük Harfe Duyarlı Aramaları Ustalıkla Kullanma

Büyük bir belge koleksiyonundan doğru bilgiyi elde etmek, modern uygulamaların temel gereksinimlerinden biridir. Bu rehberde **belge ekleme** ve **büyük/küçük harfe duyarlı aramaları** GroupDocs.Search for Java kullanarak nasıl yapacağınızı öğreneceksiniz. İster bir hukuk belgesi deposu, bir e‑ticaret kataloğu ya da bir içerik yönetim sistemi oluşturuyor olun, kesin arama sonuçları kullanıcıları mutlu eder ve verinizin güvenilirliğini artırır.

## Hızlı Yanıtlar
- **Aramaya başlamak için temel adım nedir?** `index.add(...)` ile bir dizine belge ekleyin.  
- **Büyük/küçük harfe duyarlı arama nasıl etkinleştirilir?** `options.setUseCaseSensitiveSearch(true)` ayarlayın.  
- **Birden fazla klasörde arama yapabilir miyim?** Evet – dahil etmek istediğiniz her klasör için `index.add()` çağırın.  
- **Nesnelerle arama yapmamı sağlayan yöntem hangisidir?** `SearchQuery.createWordQuery(...)` kullanın.  
- **Test için lisansa ihtiyacım var mı?** Deneme amaçlı geçici bir lisans mevcuttur.

## “Dizin'e belge ekleme” ne anlama geliyor?
Belge ekleme, kaynak dosyalarınızı (PDF, Word belgeleri, düz metin vb.) GroupDocs.Search’e besleyerek arama yapılabilir bir veri yapısı oluşturması demektir. Dizin oluşturulduktan sonra motor, büyük/küçük harfe duyarlı sorgular da dahil olmak üzere hızlı sorgular çalıştırabilir.

## Java’da büyük/küçük harfe duyarlı arama neden etkinleştirilmeli?
- **Tam terim eşleşmesi** – “Apple” (şirket) ile “apple” (meyve) arasını ayırır.  
- **Düzenleyici uyumluluk** – bazı sektörler tam ifade eşleşmesi gerektirir.  
- **Gelişmiş alaka düzeyi** – kullanıcılar teknik veya hukuki bağlamlarda büyük/küçük harfe duyarlı sonuçlar bekler.

## Önkoşullar
- JDK (Java 17 veya daha yeni sürüm önerilir)  
- Bağımlılık yönetimi için Maven  
- IntelliJ IDEA veya Eclipse gibi bir IDE  
- Java programlamaya temel aşinalık  

## GroupDocs.Search for Java Kurulumu
İlk olarak, GroupDocs deposunu ve bağımlılığı `pom.xml` dosyanıza ekleyin:

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

Alternatif olarak, en yeni sürümü doğrudan [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Lisanslama
Deneme sürümüyle başlamak için GroupDocs sitesinden geçici bir lisans edinin. Bu, tüm özellikleri sınırlama olmadan test etmenizi sağlar.

## Dizin'e belge ekleme – Metin Sorgusu Arama

### Adım 1: Bir Dizin Oluşturun ve Belgelerinizi Ekleyin
Dizin dosyalarının saklanacağı bir klasör oluşturun, ardından aramak istediğiniz belgeleri içeren kaynak klasörü ekleyin.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **İpucu:** Tek bir dizinde **birden fazla klasörde arama** yapmak için `index.add()` metodunu birden çok kez çağırabilirsiniz.

### Adım 2: Büyük/küçük harfe duyarlı aramayı etkinleştirin
Arama seçeneklerini harf duyarlılığını koruyacak şekilde yapılandırın.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Adım 3: Büyük/küçük harfe duyarlı bir metin sorgusu çalıştırın
“Advantages” ile “advantages” arasını ayıran bir sorgu yürütün.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Döngü, tam olarak büyük/küçük harfe uyan terimi içeren her belgenin tam yolunu yazdırır.

## Dizin'e belge ekleme – Nesne Sorgusu Arama

Nesne sorguları, özellikle birden fazla kriteri birleştirmeniz gerektiğinde daha fazla esneklik sağlar.

### Adım 1: İkinci bir dizin başlatın (isteğe bağlı)
Nesne‑tabanlı aramaları ayrı tutmak isterseniz, başka bir dizin klasörü oluşturun.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Adım 2: Büyük/küçük harfe duyarlı seçeneği yeniden kullanın
Aynı `SearchOptions` örneği nesne sorguları için de çalışır.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Adım 3: Bir nesne sorgusu oluşturun ve çalıştırın
Bir kelime sorgusu nesnesi oluşturun ve arama motoruna gönderin.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

`createWordQuery` kullanmak, daha sonra ifadeler, joker karakterler veya Boolean sorgularla birleştirerek daha karmaşık senaryolar oluşturmanıza olanak tanır.

## Pratik Uygulamalar
- **Hukuki Belge Yönetimi:** Büyük/küçük harf duyarlılığının önemli olduğu durum‑özel kanun maddelerini geri getirin.  
- **E‑ticaret Platformları:** “PRO‑X” ile “pro‑x” gibi ürün SKU’larını ayırın.  
- **İçerik Yönetim Sistemleri (CMS):** Yazarların tam başlıkları veya etiketleri bulmasını sağlayın.

## Performans Düşünceleri
- **Dizini güncel tutun** – yeni dosyalar eklendiğinde veya mevcut dosyalar değiştiğinde yeniden indeksleyin.  
- **Bellek kullanımını izleyin** – büyük veri kümeleri, artımlı indeksleme ve uygun JVM yığın boyutu ile fayda sağlar.  
- **Java’nın çöp toplayıcısını kullanın** – `Index` nesnelerini artık ihtiyaç duyulmadığında serbest bırakın.

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| `useCaseSensitiveSearch` göz ardı ediliyor gibi görünüyor | En yeni GroupDocs.Search sürümünü kullandığınızdan ve seçeneği değiştirdikten sonra dizinin yeniden oluşturulduğundan emin olun. |
| Bilinen bir terim için sonuç gelmiyor | Terimin büyük/küçük harfinin tam olarak eşleştiğini ve belgenin dizine başarıyla eklendiğini kontrol edin. |
| Çok sayıda klasör aramak yavaşlıyor | Her klasörü ayrı ayrı `index.add()` ile ekleyin ve çok büyük veri setleri için dizini parçalar (shard) halinde bölmeyi düşünün. |

## Sıkça Sorulan Sorular

**S:** GroupDocs.Search ile büyük veri setlerini nasıl yönetebilirim?  
**C:** Dizin bölümlendirmesini kullanın, JVM bellek ayarlarını optimize edin ve performansı korumak için periyodik olarak dizini sıkıştırın.

**S:** Aynı anda birden fazla klasörde arama yapabilir miyim?  
**C:** Evet – dahil etmek istediğiniz her klasör için `index.add()` çağırın, ardından birleşik dizin üzerinde tek bir sorgu çalıştırın.

**S:** Büyük/küçük harfe duyarlı aramaları ayarlarken sık karşılaşılan tuzaklar nelerdir?  
**C:** `useCaseSensitiveSearch` etkinleştirildikten sonra dizinin yeniden oluşturulmasını unutmak veya sorgu dizesinde yanlış harf kullanmak.

**S:** Arama hatalarını nasıl gideririm?  
**C:** GroupDocs.Search tarafından oluşturulan log dosyalarını inceleyin, yığın izlerini (stack trace) kontrol edin ve tüm Maven bağımlılıklarının doğru çözüldüğünden emin olun.

**S:** GroupDocs.Search gerçek‑zaman uygulamaları için uygun mu?  
**C:** Doğru indeksleme stratejileri (artımlı güncellemeler ve bellek içi önbellekleme) ile neredeyse gerçek‑zaman arama sonuçları sağlayabilir.

## Kaynaklar
- **Dokümantasyon:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Referansı:** [Java API Reference](https://reference.groupdocs.com/search/java)  
- **İndirme:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Deposu:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Destek Forumu:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Son Güncelleme:** 2026-02-06  
**Test Edilen Versiyon:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs  

---