---
date: '2026-02-06'
description: GroupDocs.Search for Java kullanarak belgeleri nasıl indeksleyeceğinizi
  ve indekslere belge ekleyeceğinizi öğrenin. Metin ve nesne sorgularıyla güçlü arama
  uygulamaları oluşturun.
keywords:
- GroupDocs.Search Java
- document indexing in Java
- Java document search
title: GroupDocs.Search for Java ile Belgeleri Nasıl Dizinlersiniz
type: docs
url: /tr/java/searching/master-document-search-groupdocs-java/
weight: 1
---

# Java için GroupDocs.Search ile Belgeleri Dizinleme

Günümüzün veri odaklı dünyasında, **belgeleri nasıl dizinleyebileceğinizi** verimli bir şekilde yapmak, büyük dosya koleksiyonlarıyla çalışan her Java geliştiricisi için kritik bir beceridir. İster yasal sözleşmeler, finansal tablolar ya da iç raporlarla çalışıyor olun, doğru bilgiyi hızlı bir şekilde bulabilmek saatlerce manuel çalışmayı tasarruf ettirebilir. Bu öğreticide GroupDocs.Search kütüphanesini kullanarak **belgeleri nasıl dizinleyebileceğinizi** öğrenecek, ardından oluşturulan dizin üzerinde hem metin tabanlı hem de nesne tabanlı sorgular gerçekleştireceksiniz. Hadi başlayalım!

## Hızlı Yanıtlar
- **Belgeleri dizinlemek için ilk adım nedir?** Dizinin saklanacağı bir klasöre işaret eden bir `Index` nesnesi başlatın.  
- **Hangi yöntem dizine belgeleri ekler?** `index.add("PATH_TO_DOCUMENTS")` kullanın.  
- **Sayısal aralıkları arayabilir miyim?** Evet, `"400 ~~ 4000"` gibi bir metin sorgusu ya da `SearchQuery.createNumericRangeQuery` aracılığıyla bir nesne sorgusu ile.  
- **Lisans gerekiyor mu?** Ücretsiz bir deneme mevcuttur; ticari bir lisans tam özellikleri açar.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya üzeri.

## GroupDocs.Search ile “belgeleri nasıl dizinleyebileceğiniz” nedir?
Belgeleri dizinlemek, bir klasördeki dosyaların içeriğini taramak ve aranabilir tokenları ayrı bir dizin klasöründe depolamak anlamına gelir. Bu ön işleme adımı, daha sonra yıldırım hızıyla arama yapmayı sağlar, çünkü kütüphane her seferinde ham dosyalar yerine hazırlanmış dizini arar.

## Neden Java için GroupDocs.Search kullanmalı?
- **Performans:** Binlerce dosyada bile aramalar milisaniyeler içinde gerçekleşir.  
- **Format desteği:** PDF, Word, Excel, PowerPoint ve daha birçok formatı işler.  
- **Esneklik:** Düz metin sorgularını, sayısal aralıkları ve karmaşık nesne sorgularını destekler.  
- **Ölçeklenebilirlik:** Sıfırdan yeniden oluşturmak zorunda kalmadan yeni belgeler ekleyerek dizini kolayca güncelleyebilirsiniz.

## Önkoşullar
- Bağımlılık yönetimi için Maven yüklü olmalı.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Temel Java bilgisi (OOP kavramları, istisna yönetimi).  

## Java için GroupDocs.Search Kurulumu
### Maven Kurulumu
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

### Doğrudan İndirme
Ayrıca en son JAR dosyasını [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Lisans Edinme Adımları
1. **Ücretsiz Deneme** – kütüphaneyi ücretsiz olarak keşfedin.  
2. **Geçici Lisans** – genişletilmiş değerlendirme için kısa vadeli bir anahtar isteyin.  
3. **Satın Alma** – üretim kullanımı için tam lisans edinin.

## Temel Başlatma ve Kurulum
**Dizine belge ekleme** için önce dizin dosyalarının saklanacağı klasöre işaret eden bir `Index` nesnesi oluşturursunuz:

```java
import com.groupdocs.search.Index;

// Initialize the index by specifying a directory path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");
```

Bu satır, belgeleri almaya hazır bir dizin oluşturur (veya açar).

## Uygulama Kılavuzu
### Belgeleri Oluşturma ve Dizinleme
#### Dizine belge ekleme
`add` yöntemi bir klasörü tarar ve her dosya için aranabilir verileri depolar.

```java
import com.groupdocs.search.Index;

// Initialize an index at the specified path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");

// Add documents from a directory for indexing
index.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Parametreler:** Yol dizesi, dizinlemek istediğiniz dosyaları içeren klasöre işaret eder.  
- **Amaç:** Bu adımın ardından dizin, tüm desteklenen belge türlerinden tokenları içerir ve hızlı aramaları mümkün kılar.

### Metin Sorgusu Arama
#### Metin tabanlı sayısal aralık araması nasıl yapılır
Bir aralık tanımlayan basit bir dizeyle arama yapabilirsiniz.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define a query for numeric values within a specific range
String query1 = "400 ~~ 4000";

// Execute text-based search on indexed data
SearchResult result1 = index.search(query1);
```

- **Parametreler:** `"400 ~~ 4000"` sorgu dizesi, motorun 400 ile 4000 arasındaki sayıları bulmasını söyler.  
- **Dönüş Değeri:** `SearchResult`, eşleşen belgelerin listesini ve vurgulamaları tutar.

### Nesne Sorgusu Arama
#### Sayısal aralıklar için nesne sorgusu nasıl kullanılır
Nesne tabanlı sorgular, arama kriterleri üzerinde programatik kontrol sağlar.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Create a numeric range query object
SearchQuery query2 = SearchQuery.createNumericRangeQuery(400, 4000);

// Perform search using the query object
SearchResult result2 = index.search(query2);
```

- **Parametreler:** `createNumericRangeQuery`, başlangıç ve bitiş tam sayılarını alır.  
- **Amaç:** Bu yöntem, birden fazla koşulu birleştirmeniz veya sorguları dinamik olarak oluşturmanız gerektiğinde idealdir.

## Pratik Uygulamalar
İşte **belgeleri nasıl dizinleyeceğinizin** oyun değiştirici olduğu bazı gerçek dünya senaryoları:

1. **Hukuki Belge Yönetimi** – binlerce sözleşme içinde maddeleri, dava numaralarını veya tarihleri bulun.  
2. **Finansal Raporlama** – belirli bir para aralığına düşen işlemleri çekin.  
3. **Envanter Takibi** – seri numaraları, parti kodları veya SKU aralıklarıyla öğeleri bulun.

GroupDocs.Search'ü veritabanları, bulut depolama veya mesaj kuyruğu sistemleriyle entegre etmek, belge iş akışlarını daha da otomatikleştirebilir.

## Performans Düşünceleri
- **Düzenli Dizin Güncellemeleri:** Yeni dosyalar için `index.add` komutunu yeniden çalıştırarak dizini güncel tutun.  
- **Kaynak Yönetimi:** Yığın kullanımını izleyin; büyük dizinler ayarlanmış JVM çöp toplama ayarlarından faydalanır.  
- **Sorgu Optimizasyonu:** Gereksiz taramaları azaltmak için karmaşık filtrelerde nesne sorgularını kullanın.

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Arama sonuç döndürmüyor** | Dizin oluşturulmamış veya klasör yolu yanlış | `index.add`'in doğru dizinde çalıştırıldığını ve dizin klasörünün yazılabilir olduğunu doğrulayın. |
| **Dizinleme sırasında OutOfMemoryError** | Çok büyük dosyalar veya yetersiz yığın | JVM `-Xmx` değerini artırın veya dosyaları daha küçük partiler halinde dizinleyin. |
| **Desteklenmeyen dosya formatı** | Dosya türü GroupDocs.Search tarafından tanınmıyor | Dosya uzantısının desteklenen listede (PDF, DOCX, XLSX, vb.) olduğundan emin olun. |

## Sıkça Sorulan Sorular
**Q:** Mevcut bir dizini yeni belgelerle nasıl güncellerim?  
**A:** `index.add("NEW_DOCUMENT_PATH")`'i tekrar çağırın; kütüphane tüm dizini yeniden oluşturmadan yeni girişleri birleştirir.

**Q:** GroupDocs.Search farklı dosya formatlarını işleyebilir mi?  
**A:** Evet, PDF, Word, Excel, PowerPoint, düz metin ve birçok diğer yaygın formatı destekler.

**Q:** GroupDocs.Search kullanmak için sistem gereksinimleri nelerdir?  
**A:** Java 8+ çalışma zamanı, yeterli RAM (orta ölçekli koleksiyonlar için en az 2 GB), ve dizin klasörüne okuma/yazma erişimi.

**Q:** Arama performans sorunlarını nasıl gideririm?  
**A:** Dizinin güncel olduğundan emin olun, sorgularınızı profilleyin ve JVM bellek ayarlarını gözden geçirin. Dizinlenen alan sayısını azaltmak da hızı artırabilir.

**Q:** Eşanlamlılar veya bulanık eşleşme ile arama yapmanın bir yolu var mı?  
**A:** Evet, GroupDocs.Search eşanlamlı sözlükleri ve `SearchOptions` sınıfı aracılığıyla etkinleştirilebilen bulanık arama seçenekleri sunar.

## Sonuç
Artık Java için GroupDocs.Search kullanarak **belgeleri nasıl dizinleyeceğiniz**, **belgeleri dizine nasıl ekleyeceğiniz** ve hem metin tabanlı hem de nesne tabanlı sorguları nasıl çalıştıracağınız konusunda sağlam bir anlayışa sahipsiniz. Bu teknikleri entegre ederek, Java uygulamalarınız herhangi bir belge deposunda hızlı ve doğru arama deneyimleri sunacaktır.

Bir sonraki adıma hazır mısınız? Facetli aramayı, eşanlamlı yönetimini keşfedin veya dizini bir REST API ile entegre ederek arama yeteneklerini diğer hizmetlere sunun.

---

**Son Güncelleme:** 2026-02-06  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs