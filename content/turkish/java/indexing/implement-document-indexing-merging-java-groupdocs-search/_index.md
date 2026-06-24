---
date: '2026-05-12'
description: 'Learn java full text search with GroupDocs.Search: add documents to
  index, configure merge options, and cancel merge operation. Ideal for document management
  java solutions.'
keywords:
- java full text search
- document management java
- GroupDocs.Search merging
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: 'Learn java full text search with GroupDocs.Search: add documents to
    index, configure merge options, and cancel merge operation. Ideal for document
    management java solutions.'
  headline: java full text search – add docs & merge with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It tells GroupDocs.Search to scan a folder, extract searchable tokens,
      and store metadata for each file.
    question: What does “add documents to index” mean?
  - answer: Yes—use the `Cancellation` object to abort a merge after a configurable
      timeout.
    question: Can I stop a long merge?
  - answer: A free trial or temporary license works for testing; a commercial license
      unlocks full features.
    question: Do I need a license?
  - answer: JDK 8 or newer.
    question: Which Java version is required?
  - answer: Absolutely—GroupDocs.Search can handle multi‑hundred‑page documents with
      incremental indexing.
    question: Is this suitable for large datasets?
  type: FAQPage
title: java full text search – add docs & merge with GroupDocs.Search
type: docs
url: /tr/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# java tam metin arama – belgeleri ekle ve GroupDocs.Search ile birleştir

## Hızlı Yanıtlar
- **“add documents to index” ne anlama geliyor?** GroupDocs.Search'ün bir klasörü taramasını, aranabilir token'ları çıkarmasını ve her dosya için meta verileri depolamasını sağlar.  
- **Uzun bir birleştirmeyi durdurabilir miyim?** Evet—birleştirmeyi yapılandırılabilir bir zaman aşımından sonra iptal etmek için `Cancellation` nesnesini kullanın.  
- **Bir lisansa ihtiyacım var mı?** Test için ücretsiz deneme veya geçici lisans yeterlidir; ticari lisans tam özellikleri açar.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya daha yeni bir sürüm.  
- **Büyük veri setleri için uygun mu?** Kesinlikle—GroupDocs.Search, artımlı indeksleme ile çok sayıda sayfalı belgeleri işleyebilir.

## GroupDocs.Search'te “add documents to index” nedir?
**Adding documents to an index** bir dosya koleksiyonunu GroupDocs.Search'e beslemek anlamına gelir; böylece kütüphane içeriği analiz eder, token'ları çıkarır ve aranabilir bir veri yapısı oluşturur. Bu süreç, tüm indekslenmiş dosyalar üzerinde ışık hızıyla tam metin sorgularını mümkün kılan kompakt bir temsil oluşturur.

## Neden GroupDocs.Search'i belge yönetimi java için kullanmalısınız?
GroupDocs.Search, **50+ giriş formatı için ölçeklenebilir indeksleme** (PDF, DOCX, XLSX, PPTX, HTML, görüntüler vb.) sunar ve **tüm dosyayı belleğe yüklemeden 2 GB'a kadar belge** işleyebilir. API'si, indeksleme, birleştirme ve iptal üzerinde ayrıntılı kontrol sağlar ve bunu kurumsal düzeyde java tam metin arama çözümleri için birincil tercih yapar.

## Önkoşullar
- **GroupDocs.Search for Java** sürüm 25.4 veya üzeri.  
- Maven (veya manuel JAR indirme).  
- Temel Java bilgisi ve JDK 8+ ortamı.  

## GroupDocs.Search for Java'ı Kurma

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

### Lisans Edinme
- **Free Trial:** Deneme lisansı için GroupDocs web sitesine kaydolun.  
- **Temporary License:** Uzun süreli değerlendirme ihtiyacınız varsa geçici anahtar başvurun.  
- **Commercial License:** Üretim kullanımı için satın alın.

Lisans dosyasını aldıktan sonra, projenize yerleştirin ve kütüphaneyi daha sonra gösterildiği gibi başlatın.

## Uygulama Kılavuzu

### İndekse belge ekleme – İlk İndeksi Oluşturma
**`Index` sınıfını örnekleyerek boş bir indeks yükleyin veya oluşturun; bu sınıf, disk üzerindeki aranabilir bir konteyneri temsil eder.** Bu adım, belgelerinizden üretilecek tüm token'lar için bir depolama konumu hazırlar.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Neden:** Bu adım, indekslenen token'ların kaydedileceği bir depolama konteyneri oluşturur.

#### İndekse belgeleri ekleme
**`index.add` metodunu bir klasör yolu ile çağırın; yöntem her dosyayı tarar, metni çıkarır ve indeks içinde aranabilir meta verileri depolar.** İşlem tek bir geçişte çalışır ve yapılandırılmış `IndexSettings`'e saygı gösterir.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Neden:** Kütüphane her dosyayı okur, metni çıkarır ve `index1` içinde depolar.

### Esnek iş akışları için ikinci bir indeks oluşturma
**Bir başka `Index` nesnesi oluşturun; bu, birleştirmeden önce izole işleme izin veren ayrı bir belge seti tutar.** Bu desen, çok kiracılı senaryolar veya aşamalı indeksleme için faydalıdır.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Neden:** Birden fazla indeks, farklı belge setlerini yönetmenizi ve daha sonra birleştirmenizi sağlar.

### Birleştirme seçeneklerini yapılandırma ve birleştirme işlemini iptal etme
**Bir `MergeOptions` örneği oluşturun, istenen parametreleri ayarlayın ve belirli bir zaman aşımından sonra birleştirmeyi iptal eden bir `Cancellation` token'ı ekleyin.** Bu, büyük birleştirmeler sırasında kaynak kullanımını tam kontrol etmenizi sağlar.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Neden:** `Cancellation`, **birleştirme işlemini iptal** etmenizi otomatik olarak kontrol etmenizi sağlar, kontrol dışı görevleri önler.

### İndeksleri Birleştirme
**`index1.merge(index2, mergeOptions)` çağırın; birincil indeks, token bütünlüğünü koruyarak ikincil indeksin tüm belgelerini absorbe eder.** Birleştirmeden sonra, birleşik bir aranabilir depo elde edersiniz.

```java
index1.merge(index2, options);
```

- **Neden:** Bu çağrıdan sonra, `index1` her iki kaynaktan da tüm belgeleri içerir ve size birleşik bir arama deneyimi sunar.

## Belge Yönetimi Java için Pratik Uygulamalar
- **Legal firms:** Birden fazla ofisten dava dosyalarını tek bir aranabilir indeksde birleştirin.  
- **Financial institutions:** Çeyrek raporlarını hızlı denetim sorguları için birleşik bir depoda birleştirin.  
- **Enterprises:** İnsan kaynakları politikalarını, uyum kılavuzlarını ve iç rehberleri kurumsal çapta arama için birleştirin.

## Performans Düşünceleri
- **Incremental indexing:** Tüm indeksi yeniden oluşturmak yerine yeni dosyaları periyodik olarak ekleyin.  
- **Memory monitoring:** Büyük toplular RAM tüketebilir; dosyaları daha küçük parçalar halinde işleyin veya akış modunu etkinleştirin.  
- **Garbage collection:** Kullanılmayan `Index` nesnelerini hızlıca serbest bırakın, böylece kaynakları boşaltın.  
- **SSD storage:** İndeks dosyalarını SSD'lerde depolamak, birleştirme hızını 2 katına kadar artırabilir.

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| **Yanlış klasör yolu** | Mutlak yolu doğrulayın ve uygulamanın okuma izinlerine sahip olduğundan emin olun. |
| **Yetersiz bellek** | JVM yığın boyutunu (`-Xmx`) artırın veya dosyaları toplu olarak indeksleyin. |
| **İptal tetiklenmedi** | `merge` çağırmadan önce `cancelAfter`'ın ayarlandığından emin olun. |
| **Desteklenmeyen dosya formatı** | Gerekiyorsa GroupDocs'tan ek format eklentileri kurun. |

## Sıkça Sorulan Sorular

**Q:** *Neden tek bir indeks yerine birden fazla indeks oluşturmalıyım?*  
**A:** Ayrı indeksler, veri alanlarını izole etmenizi, farklı güvenlik politikaları uygulamanızı ve sadece gerektiğinde birleştirmenizi sağlar; bu da performans ve organizasyonu artırır.

**Q:** *Bir indeksleme işlemini aynı şekilde birleştirmeyi iptal ettiğim gibi iptal edebilir miyim?*  
**A:** Evet—`add` yöntemiyle `Cancellation` nesnesini kullanarak uzun süren indeksleme görevlerini durdurabilirsiniz.

**Q:** *Çok büyük belge koleksiyonlarıyla optimum performansı nasıl sağlarsınız?*  
**A:** Artımlı indeksleme yapın, JVM belleğini izleyin ve indeksi SSD'lerde depolayın. Bellekteki belgeleri sınırlamak için `BatchSize` ayarını kullanmayı düşünün.

**Q:** *“Erişim reddedildi” hatası alırsam ne yapmalıyım?*  
**A:** Java sürecini çalıştıran kullanıcının klasör izinlerini kontrol edin ve lisans dosyasının okunabilir olduğundan emin olun.

**Q:** *GroupDocs.Search diğer GroupDocs kütüphaneleriyle uyumlu mu?*  
**A:** Kesinlikle—GroupDocs.Viewer, GroupDocs.Conversion ve diğerleriyle entegre ederek tam bir belge çözümü oluşturabilirsiniz.

## Sonuç
Bu kılavuzu izleyerek artık **add documents to index** nasıl yapılır, birleştirme davranışı nasıl yapılandırılır ve gerektiğinde güvenli bir şekilde **cancel merge operation** nasıl iptal edilir, biliyorsunuz—tüm bunlar sağlam bir **java full text search** iş akışı içinde. Daha büyük veri setleriyle deney yapın, özel tokenlaştırıcıları keşfedin veya GroupDocs.Search'ü diğer GroupDocs ürünleriyle birleştirerek kurumsal düzeyde bir çözüm oluşturun.

**Kaynaklar**
- **Dokümantasyon:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Referansı:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **İndirme:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Deposu:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ücretsiz Destek Forumu:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans Başvurusu:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Son Güncelleme:** 2026-05-12  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [GroupDocs.Search kullanarak Java'da Meta Veri İndeksleme ile indeks'e belge ekleme](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [GroupDocs.Search Java'da Belgeleri İndekse Ekle ve Durdurma Kelimelerini Devre Dışı Bırakarak Arama Doğruluğunu Artırma](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
- [Belgeleri İndekse Ekle – GroupDocs.Search Java Eğitimleri](/search/java/document-management/)