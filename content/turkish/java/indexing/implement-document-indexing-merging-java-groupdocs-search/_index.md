---
date: '2026-01-03'
description: GroupDocs.Search kullanarak Java'da belgeleri indekse eklemeyi ve birleştirme
  işlemini iptal etmeyi öğrenin. Belge yönetimi Java için kapsamlı bir rehber.
keywords:
- document indexing in Java
- merging documents with GroupDocs
- GroupDocs.Search Java tutorial
title: Java'da GroupDocs.Search ile belgeleri indekse ekle ve birleştir
type: docs
url: /tr/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# Java'da GroupDocs.Search kullanarak indeks'e belge ekleme ve birleştirme

Bugünün hızlı tempolu dijital ortam, **indekse belge ekleme** yöntemini verimli bir şekilde öğrenmek, herhangi bir **document management java** çözümü için hayati öneme sahiptir. Sözleşmeler, faturalar veya iç raporlar gibi belgelerle çalışıyor olun, iyi yapılandırılmış bir indeks, bilgileri milisaniyeler içinde almanızı sağlar. Bu öğretici, indeks oluşturma, belge ekleme, birleştirme seçeneklerini yapılandırma ve gerekirse **birleştirme işlemini iptal et** adımlarını GroupDocs.Search for Java ile size gösterir.

## Hızlı Yanıtlar
- **“indekse belge ekleme” ne anlama geliyor?** GroupDocs.Search'e bir klasörü taramasını ve her dosya için aranabilir meta verileri depolamasını söyler.  
- **Uzun bir birleştirmeyi durdurabilir miyim?** Evet—`Cancellation` nesnesini kullanarak zaman aşımından sonra **birleştirme işlemini iptal et**.  
- **Bir lisansa ihtiyacım var mı?** Test için ücretsiz deneme veya geçici lisans yeterlidir; ticari lisans tam özellikleri açar.  
- **Hangi Java sürümü gerekiyor?** JDK 8 veya daha yenisi.  
- **Büyük veri setleri için uygun mu?** Kesinlikle—sadece belleği izleyin ve artımlı indekslemeyi kullanın.  

## GroupDocs.Search'te “indekse belge ekleme” nedir?
Bir indeks'e belge eklemek, dosya koleksiyonunu GroupDocs.Search'e beslemek anlamına gelir; böylece kütüphane içeriği analiz eder, token'ları çıkarır ve aranabilir bir veri yapısı oluşturur. İndeksleme tamamlandığında, tüm belgeler üzerinde hızlı tam metin aramaları yapabilirsiniz.

## Neden GroupDocs.Search'i document management java için kullanmalısınız?
- **Scalable indexing** – Performansı düşürmeden binlerce dosyayı yönetir.  
- **Rich API** – indeksleme, birleştirme ve iptal işlemleri üzerinde ayrıntılı kontrol sağlar.  
- **Cross‑format support** – kutudan çıkar çıkmaz PDF, Word, Excel ve birçok diğer formatla çalışır.  

## Önkoşullar
- **GroupDocs.Search for Java** sürüm 25.4 veya üzeri.  
- Maven (veya manuel JAR indirme).  
- Temel Java bilgisi ve JDK 8+ ortamı.  

## GroupDocs.Search for Java Kurulumu

### Maven Kurulumu
Bağımlılıkları Maven ile yönetiyorsanız, depo ve bağımlılığı `pom.xml` dosyanıza ekleyin:

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
Alternatif olarak, resmi siteden en son JAR'ı indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinimi
- **Free Trial:** GroupDocs web sitesinde deneme lisansı için kaydolun.  
- **Temporary License:** Uzun süreli değerlendirme için geçici bir anahtar talep edin.  
- **Commercial License:** Üretim kullanımı için satın alın.

Lisans dosyasına sahip olduktan sonra, dosyayı projenize yerleştirin ve kütüphaneyi daha sonra gösterildiği gibi başlatın.

## Uygulama Kılavuzu

### Belgeleri indekse ekleme – İlk İndeksin Oluşturulması
İlk olarak, aranabilir verilerinizi tutacak boş bir indeks oluşturun.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Why:** Bu adım, indekslenen token'ların kaydedileceği bir depolama konteyneri oluşturur.

#### Belgeleri indekse ekleme
Şimdi GroupDocs.Search'e bir klasörü taramasını ve **indekse belge ekle** söyleyin.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Why:** Kütüphane her dosyayı okur, metni çıkarır ve `index1` içinde depolar.

### Esnek iş akışları için ikinci bir indeks oluşturma
Bazen ayrı indekslere ihtiyaç duyarsınız—örneğin, bir müşterinin verilerini izole etmek için.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Why:** Birden fazla indeks, farklı belge setlerini yönetmenizi ve daha sonra birleştirmenizi sağlar.

### Birleştirme seçeneklerini yapılandırma ve birleştirme işlemini iptal etme
Birleştirmeden önce, süreci ince ayar yapabilir ve çok uzun sürerse durdurabilirsiniz.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Why:** `Cancellation` size **birleştirme işlemini iptal et** kontrolünü otomatik olarak verir, kontrol dışı görevleri önler.

### İndeksleri birleştirme
Son olarak, ikincil indeksi birincil indeksle birleştirin.

```java
index1.merge(index2, options);
```

- **Why:** Bu çağrıdan sonra, `index1` her iki kaynaktan da tüm belgeleri içerir ve size birleşik bir arama deneyimi sunar.

## Document Management Java için Pratik Uygulamalar
- **Legal firms:** Birden fazla ofisten dava dosyalarını birleştirin.  
- **Financial institutions:** Çeyrek raporları tek bir aranabilir depoya birleştirin.  
- **Enterprises:** HR, uyumluluk ve politika belgelerini kurumsal çapta arama için birleştirin.

## Performans Düşünceleri
- **Incremental indexing:** Tüm indeksi yeniden oluşturmak yerine yeni dosyaları periyodik olarak ekleyin.  
- **Memory monitoring:** Büyük toplular RAM tüketebilir; daha küçük parçalar halinde işlemeyi düşünün.  
- **Garbage collection:** Kullanılmayan `Index` nesnelerini hızlıca serbest bırakın.

## Yaygın Sorunlar ve Çözümler

| Issue | Solution |
|-------|----------|
| **Yanlış klasör yolu** | Mutlak yolu doğrulayın ve uygulamanın okuma izinlerine sahip olduğundan emin olun. |
| **Yetersiz bellek** | JVM yığın boyutunu (`-Xmx`) artırın veya dosyaları toplu olarak indeksleyin. |
| **İptal tetiklenmedi** | `merge` çağrılmadan önce `cancelAfter` ayarlandığından emin olun. |
| **Desteklenmeyen dosya formatı** | Gerekirse GroupDocs'tan ek format eklentileri kurun. |

## Sıkça Sorulan Sorular

**Q:** *Neden tek bir indeks yerine birden fazla indeks oluşturmalıyım?*  
**A:** Ayrı indeksler veri alanlarını izole etmenizi, farklı güvenlik politikaları uygulamanızı ve yalnızca gerektiğinde birleştirmenizi sağlar; bu da performans ve organizasyonu artırır.

**Q:** *Bir indeksleme işlemini, birleştirmeyi iptal ettiğim gibi iptal edebilir miyim?*  
**A:** Evet—`add` yöntemiyle `Cancellation` nesnesini kullanarak uzun süren indeksleme görevlerini durdurabilirsiniz.

**Q:** *Çok büyük belge koleksiyonlarıyla optimum performansı nasıl sağlarsınız?*  
**A:** Artımlı indeksleme yapın, JVM belleğini izleyin ve indeks dizini için SSD depolama kullanmayı düşünün.

**Q:** *“Erişim reddedildi” hatası alırsam ne yapmalıyım?*  
**A:** Java sürecini çalıştıran kullanıcının klasör izinlerini kontrol edin ve lisans dosyasının okunabilir olduğundan emin olun.

**Q:** *GroupDocs.Search diğer GroupDocs kütüphaneleriyle uyumlu mu?*  
**A:** Kesinlikle—tam bir belge çözümü için GroupDocs.Viewer, GroupDocs.Conversion vb. ile entegre edebilirsiniz.

## Sonuç
Bu kılavuzu izleyerek artık **indekse belge ekleme**, birleştirme davranışını yapılandırma ve gerektiğinde güvenli bir şekilde **birleştirme işlemini iptal et** konularını biliyorsunuz—hepsi sağlam bir **document management java** iş akışı içinde. Daha büyük veri setleriyle deney yapın, özel tokenleştiricileri keşfedin veya GroupDocs.Search'ı diğer GroupDocs ürünleriyle birleştirerek gerçek bir kurumsal çözüm oluşturun.

---

**Last Updated:** 2026-01-03  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

## Kaynaklar
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License Application:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)