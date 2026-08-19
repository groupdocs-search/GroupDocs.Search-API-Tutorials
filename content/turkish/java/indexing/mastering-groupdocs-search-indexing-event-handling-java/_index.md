---
date: '2026-03-15'
description: GroupDocs.Search for Java kullanarak Java’da indeksleme olaylarını nasıl
  yöneteceğinizi öğrenin; kurulum, olay aboneliği ve en iyi uygulamaları kapsar.
keywords:
- GroupDocs.Search for Java
- indexing event handling
- Java indexing events
title: GroupDocs.Search ile Java’da indeksleme olaylarını nasıl yönetilir
type: docs
url: /tr/java/indexing/mastering-groupdocs-search-indexing-event-handling-java/
weight: 1
---

 translation.

# Java ile GroupDocs.Search'te indeksleme olaylarını nasıl yönetilir

Modern uygulamalarda, **indeksleme olaylarını yönetmek** arama indekslerinin güvenilir ve yanıt verebilir olmasını sağlamak için çok önemlidir. GroupDocs.Search for Java, indeksleme yaşam döngüsünün her aşamasına — ilerleme güncellemeleri, hatalar veya tamamlama bildirimleri — yanıt vermenizi sağlayan güçlü bir olay‑tabanlı API sunar. Bu rehberde kütüphaneyi kurmayı, en faydalı olaylara abone olmayı ve bu teknikleri gerçek‑dünya belge yönetimi senaryolarında uygulamayı adım adım göstereceğiz.

**Öğrenecekleriniz**
- GroupDocs.Search for Java’yı kurma ve yapılandırma.
- İşlem tamamlanması, hatalar, ilerleme değişiklikleri gibi temel olaylara abone olma.
- Olay yönetimini belge yönetim sistemlerine entegre etmek için pratik ipuçları.
- İndeksleme olaylarını yönetmenin güvenilirliği ve kullanıcı deneyimini nasıl büyük ölçüde artırdığını gösteren gerçek‑dünya kullanım örnekleri.

Arama güvenilirliğinizi artırmaya hazır mısınız? Hadi başlayalım!

## Hızlı Yanıtlar
- **İndeksleme olaylarını yönetmenin ana faydası nedir?** İndeksleme ilerlemesini, günlüklerini ve sorunlarını gerçek zamanlı olarak izleyip yanıt vermenizi sağlar.  
- **Bu yeteneği sağlayan kütüphane hangisidir?** GroupDocs.Search for Java.  
- **Denemek için lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme veya geçici lisans mevcuttur.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya üzeri.  
- **İndekslemeyi asenkron çalıştırabilir miyim?** Evet—ana iş parçacığını engellememek için asenkron API’yı kullanın.  

## İndeksleme olaylarını yönetmek ne anlama geliyor?
İndeksleme olaylarını yönetmek, GroupDocs.Search indeksleme sırasında yükselttiği geri çağrılara (callback) özel mantık eklemek anlamına gelir. Bu geri çağrılar (veya olaylar), işlem türü, zaman damgaları, hata mesajları ve ilerleme yüzdeleri gibi detaylara erişim sağlar; böylece bilgileri günlükleyebilir, UI bileşenlerini güncelleyebilir veya alt süreçleri otomatik olarak tetikleyebilirsiniz.

## Neden GroupDocs.Search for Java olay yönetimini kullanmalı?
- **Gerçek zamanlı görünürlük:** İndeksleme ne zaman başladığını, ilerlediğini veya başarısız olduğunu anında öğrenin.  
- **Artan güvenilirlik:** Kullanıcıları etkilemeden önce hataları yakalayıp günlükleyin.  
- **Daha iyi kullanıcı deneyimi:** Uygulamanızda ilerleme çubukları veya bildirimler gösterin.  
- **Otomasyon:** Önbellek yenileme veya analiz gibi indeksleme sonrası görevleri otomatik başlatın.

## Önkoşullar
- **Gerekli Kütüphaneler** – Projenize GroupDocs.Search ekleyin (aşağıdaki Maven koduna bakın).  
- **Ortam** – JDK 8+, IntelliJ IDEA veya Eclipse.  
- **Temel bilgi** – Java ve olay‑tabanlı programlamaya aşina olmak faydalıdır, ancak adımlar ayrıntılı olarak açıklanmıştır.

### Gerekli Kütüphaneler
GroupDocs.Search bağımlılığını ekleyin. Maven kullananlar için aşağıdaki yapılandırmayı ekleyin:

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

Doğrudan indirme için [GroupDocs.Search for Java releases page](https://releases.groupdocs.com/search/java/) adresini ziyaret edin.

### Ortam Kurulumu
- JDK 8 veya daha yeni bir sürüm.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.

### Bilgi Önkoşulları
Java programlama ve olay‑tabanlı tasarım hakkında temel bir anlayış faydalı olacaktır, ancak zorunlu değildir; her adım sade bir dille açıklanmıştır.

## GroupDocs.Search for Java’yı Kurma

### Kurulum Bilgileri
#### Maven Kurulumu
`pom.xml` dosyanıza aşağıdaki girdileri ekleyin:

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

#### Doğrudan İndirme
Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Lisans Edinme
GroupDocs.Search’i etkili bir şekilde kullanmak için:
- **Ücretsiz Deneme** – Özellikleri keşfetmek üzere ücretsiz deneme ile başlayın.  
- **Geçici Lisans** – Sınırlama olmadan değerlendirme için geçici bir lisans alın.  
- **Satın Alma** – Araç üretim ihtiyaçlarınızı karşılıyorsa satın almayı düşünün.

### Temel Başlatma ve Kurulum
Bir indeksin nasıl başlatılacağını ve kurulacağını gösteren örnek:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.events.EventHandler;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/YourIndex";

// Creating an index in a specific folder
Index index = new Index(indexFolder);
```

## Uygulama Kılavuzu
Aşağıda **indeksleme olaylarını yönetirken** en sık karşılaşacağınız olayları adım adım inceliyoruz.

### ÖZELLİK: OperationFinishedEvent
#### Genel Bakış
`OperationFinishedEvent`, bir indeksleme işlemi tamamlandığında tetiklenir; sonucu günlükleyebilir veya başka bir süreci başlatabilirsiniz.

#### Uygulama Adımları
**Adım 1: İndeksi Oluşturun**

```java
import com.groupdocs.search.Index;
import java.text.SimpleDateFormat;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/UsingEvents\\OperationFinishedEvent";
Index index = new Index(indexFolder);
```

**Adım 2: Olayı Abone Olun**  
Konsola yararlı bilgiler yazdıran bir işleyici ekleyin:

```java
index.getEvents().OperationFinished.add(new EventHandler<com.groupdocs.search.events.OperationFinishedEventArgs>() {
    @Override
    public void invoke(Object sender, com.groupdocs.search.events.OperationFinishedEventArgs args) {
        SimpleDateFormat df = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
        System.out.println("Operation finished: " + args.getOperationType());
        System.out.println("Message: " + args.getMessage());
        System.out.println("Index folder: " + args.getIndexFolder());
        System.out.println("Time: " + df.format(args.getTime()));
    }
});
```

**Adım 3: Belgeleri İndeksleyin**

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

### ÖZELLİK: ErrorOccurredEvent
*Aynı desen uygulanır – indeksi oluşturun, `ErrorOccurred` olayına abone olun ve ardından indekslemeyi başlatın. Olay, günlükleyebileceğiniz veya izleme sistemlerine aktarabileceğiniz hata detaylarını sağlar.*

### ÖZELLİK: OperationProgressChangedEvent
*Bu olayı periyodik ilerleme yüzdelerini almak için kullanın. UI bileşenlerini güncelleyin veya denetim amaçlı ilerlemeyi bir günlük dosyasına yazın.*

*(`PasswordRequestedEvent`, `FileProcessingStartedEvent` vb. diğer olaylar için aynı yapıyı, her birini ayrı bir alt bölüme yerleştirerek devam ettirin.)*

## Pratik Uygulamalar
Bu olay‑yönetimi yetenekleri birçok gerçek‑dünya senaryosunda öne çıkar:

1. **Belge Yönetim Sistemleri** – İndeksleme durumunu otomatik olarak günlükleyin ve hataları yönetin; böylece kullanıcı deneyimini iyileştirin.  
2. **İçerik Portalları** – Canlı indeksleme ilerlemesini göstererek kullanıcıların aramanın ne zaman hazır olacağını bilmelerini sağlayın.  
3. **Güvenli Depolar** – Olay geri çağrıları aracılığıyla korumalı dosyalar için şifre istemlerini sorunsuz bir şekilde yönetin.  
4. **Analitik Boru Hatları** – Yeni belgeler indekslendiğinde hemen alt süreç analitik işlerini tetikleyin.

## Performans Düşünceleri
Büyük belge koleksiyonlarını yönetirken:

- UI’nın yanıt vermesini sağlamak için asenkron indekslemeyi tercih edin.  
- Bellek kullanımını izleyin ve indeksleme sonrası kaynakları serbest bırakın.  
- `IndexSettings` içinde `FileFilter` kullanarak gereksiz dosya türlerini dışarıda bırakın.  

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|-------|----------|
| **Çıktı klasöründe izin reddedildi** | İşlem yazma iznine sahip değil. | Dizin yazılabilir olduğundan emin olun veya JVM’yi uygun izinlerle çalıştırın. |
| **İlerleme olayları tetiklenmiyor** | Olay aboneliği eksik ya da indeksleme başladıktan sonra eklendi. | Olayları **index.add(...)** çağrısından **önce** abone olun. |
| **Şifre korumalı dosyalar hata veriyor** | Şifre işleyicisi tanımlı değil. | `PasswordRequestedEvent`’i uygulayın ve şifreyi programatik olarak sağlayın. |
| **Büyük partilerde bellek tükeniyor** | Tüm belgeler aynı anda belleğe yükleniyor. | Asenkron API’yı kullanın ve belgeleri daha küçük partiler halinde işleyin. |

## Sık Sorulan Sorular

**S: İndeksleme hatalarını etkili bir şekilde nasıl yönetirim?**  
C: `ErrorOccurredEvent`’e abone olun ve hata detaylarını günlükleyin veya yöneticileri uyarın.

**S: Hangi dosyaların indeksleneceğini özelleştirebilir miyim?**  
C: Evet—`IndexSettings` içinde `FileFilter` seçeneğini kullanarak dahil etme veya hariç tutma desenleri belirleyebilirsiniz.

**S: Büyük bir belge seti için gerçek‑zamanlı ilerleme güncellemelerine ihtiyacım var; ne yapmalıyım?**  
C: `OperationProgressChangedEvent`’i kullanarak periyodik ilerleme yüzdelerini alın ve UI’nızı buna göre güncelleyin.

**S: Şifre korumalı belgeleri manuel giriş olmadan indeksleyebilir miyim?**  
C: Evet—şifre isteği olayını yakalayarak şifreyi programatik olarak sağlayabilirsiniz.

**S: GroupDocs.Search asenkron indekslemeyi yerleşik olarak destekliyor mu?**  
C: Kesinlikle. Asenkron API metodlarını kullanarak indekslemeyi ayrı bir iş parçacığında başlatın ve uygulamanızın yanıt verebilir kalmasını sağlayın.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Referansı**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **İndirme**: [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search for Java Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ücretsiz Destek**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

Bir sonraki adıma geçmeye hazır mısınız? Tam API’yı keşfedin, ek olayları deneyin ve bu desenleri kendi belge‑odaklı uygulamalarınıza entegre edin.

---

**Son Güncelleme:** 2026-03-15  
**Test Edilen Sürüm:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs