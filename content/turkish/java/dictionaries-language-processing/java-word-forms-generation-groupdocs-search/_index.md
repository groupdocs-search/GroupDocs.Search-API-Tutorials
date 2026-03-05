---
date: '2026-02-21'
description: Java'da GroupDocs.Search API'sini kullanarak tekil-çoğul formları nasıl
  oluşturacağınızı öğrenin. Doğru arama ve metin analizi için özel bir kelime formu
  sağlayıcısı oluşturun.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Java'da GroupDocs.Search ile Tekil ve Çoğul Formlar Oluşturun
type: docs
url: /tr/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Java'da Tekil Çoğul Formları Oluşturma – GroupDocs.Search ile

Java'da **Java'da tekil çoğul formları oluşturma** gerekiyorsa, özel bir kelime‑formları sağlayıcısı, arama veya metin‑analiz motorunuzun bir terimin tüm varyasyonlarını anlamasını sağlayan anahtardır. Bu öğreticide, GroupDocs.Search Java API'si ile böyle bir sağlayıcı oluşturmayı adım adım göstereceğiz, böylece uygulamanız “cat”, “cats”, “city” ve “citis” gibi kelimeleri ekstra çaba harcamadan otomatik olarak eşleştirebilir.

## Hızlı Yanıtlar
- **Bir kelime formları sağlayıcısı ne yapar?** Belirli bir kelimenin alternatif formlarını (tekil, çoğul vb.) üretir, böylece aramalar tüm varyantları eşleştirebilir.  
- **Hangi kütüphane gereklidir?** GroupDocs.Search for Java (sürüm 25.4 veya daha yeni).  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gerekir.  
- **Hangi Java sürümü destekleniyor?** JDK 8 ve üzeri.  
- **Kaç satır kod gerekir?** Basit bir sağlayıcı uygulaması için yaklaşık 30 satır.

## “Create Word Forms Provider” özelliği nedir?
Bir **create word forms provider** bileşeni, `IWordFormsProvider` arayüzünü uygulayan özel bir sınıftır. Bir kelime alır ve tanımladığınız kurallara göre olası formların bir dizisini döndürür—tekil, çoğul veya diğer dilsel varyasyonlar. Bu, arama indeksinin “cat” ve “cats” gibi kelimeleri eşdeğer olarak ele almasını sağlar, kesinliği kaybetmeden geri getirmeyi (recall) artırır.

## Kelime‑formu oluşturma için neden GroupDocs.Search kullanmalı?
- **Yerleşik genişletilebilirlik:** Kendi sağlayıcınızı doğrudan indeksleme hattına bağlayın.  
- **Performans‑optimizasyonu:** Büyük indeksleri verimli bir şekilde işler ve ek hız için sonuçları önbelleğe alabilirsiniz.  
- **Çapraz‑dil desteği:** Kavramlar .NET ve diğer platformlarda da geçerlidir.

## Önkoşullar
**create word forms provider** uygulamaya koymadan önce, şunların olduğundan emin olun:
- **Maven** kurulu ve makinenizde JDK 8 veya daha yeni bir sürüm ayarlanmış.  
- Java geliştirme ve Maven'in `pom.xml` yapılandırması konusunda temel bilgi.  
- GroupDocs.Search Java kütüphanesine erişim (sürüm 25.4 veya sonrası).

## GroupDocs.Search for Java'ı Kurma

### Maven Yapılandırması
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

### Doğrudan İndirme
Alternatif olarak, resmi sürüm sayfasından en son JAR dosyasını indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinme Adımları
1. **Ücretsiz Deneme:** Temel özellikleri keşfetmek için bir deneme hesabı oluşturun.  
2. **Geçici Lisans:** Uzun süreli test için geçici bir anahtar isteyin.  
3. **Satın Alma:** Sınırsız üretim kullanımı için ticari bir lisans edinin.

### Temel Başlatma ve Kurulum
Aşağıdaki kod parçacığı, belge eklemek ve kelime‑form mantığını uygulamak için başlangıç noktası olan bir indeksin nasıl oluşturulacağını gösterir:

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

## Uygulama Kılavuzu

Aşağıda, basit tekil‑çoğul ve çoğul‑tekil dönüşümleri yöneten bir **create word forms provider** oluşturma adımlarını anlatıyoruz.

### SimpleWordFormsProvider'ı Uygulama

#### Genel Bakış
Özel sağlayıcımız şunları yapacak:
- Sonundaki “es” veya “s” karakterlerini kaldırarak tekil form tahmin edecek.  
- Sonundaki “y” harfini “is” ile değiştirerek çoğul form oluşturacak (örnek: “city” → “citis”).  
- Temel çoğul adaylarını oluşturmak için “s” ve “es” ekleyecek.

#### Adım 1 – Sınıf İskeletini Oluşturma
`IWordFormsProvider` arayüzünü uygulayan bir sınıf tanımlayarak başlayın. İçe aktarma (import) ifadelerini değiştirmeyin:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Adım 2 – `getWordForms` Metodunu Uygulama
Olası formların listesini oluşturan metodu ekleyin. Bu blok temel mantığı içerir; daha karmaşık kuralları kapsayacak şekilde sonradan genişletebilirsiniz.

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

#### Mantığın Açıklaması
- **Tekilleştirme:** Yaygın çoğul eklerini (`es`, `s`) algılar ve temel kelimeyi tahmin etmek için kaldırır.  
- **Çoğullaştırma:** `y` ile biten isimleri `is` ile değiştirir, birçok İngilizce kelime için işe yarayan basit bir kural.  
- **Ek Ekleme:** Önceki kontrollerle yakalanamayan düzenli çoğul formları kapsamak için `s` ve `es` ekler.

#### Sorun Giderme İpuçları
- **Büyük/Küçük Harf Duyarlılığı:** Metod, karşılaştırma için `toLowerCase()` kullanır, böylece “Cats” ve “cats” aynı şekilde davranır.  
- **Köşe Durumlar:** Ek uzunluğundan kısa kelimeler, boş string döndürmeyi önlemek için yok sayılır.  
- **Performans:** Büyük kelime dağarcıkları için sonuçları bir `ConcurrentHashMap` içinde önbelleğe almayı düşünün.

## Pratik Uygulamalar

Bir **create word forms provider** uygulamak, çeşitli gerçek‑dünya senaryolarını artırabilir:
1. **Arama Motorları:** “mouse” yazan kullanıcılar, “mice” içeren belgeleri de bulmalıdır. Sağlayıcı bu tür düzensiz formları üretebilir.  
2. **Metin Analiz Araçları:** Tüm kelime varyantları tanındığında duygu analizi veya varlık çıkarımı daha güvenilir olur.  
3. **İçerik Yönetim Sistemleri:** Otomatik etiket oluşturma, çoğul eşanlamlıları içerebilir, SEO ve iç bağlantıları iyileştirir.

## Performans Düşünceleri

Sağlayıcıyı bir üretim sistemine entegre ettiğinizde, şu ipuçlarını aklınızda bulundurun:
- **Sık Kullanılan Formları Önbellekle:** Aynı kelimeyi tekrar tekrar yeniden hesaplamaktan kaçınmak için sonuçları bellekte saklayın.  
- **JVM Heap'i İzle:** Büyük indeksler bellek baskısını artırabilir; `-Xmx` ayarını buna göre yapılandırın.  
- **Verimli Koleksiyonlar Kullan:** `ArrayList` küçük setler için uygundur, ancak binlerce form için `HashSet` kullanarak tekrarları hızlıca ortadan kaldırabilirsiniz.

**En İyi Uygulamalar**
- Kütüphaneyi güncel tutarak performans yamalarından yararlanın.  
- Sağlayıcıyı gerçekçi sorgu yükleriyle profil çıkararak darboğazları erken tespit edin.

## Sonuç

Artık GroupDocs.Search ile özel bir `SimpleWordFormsProvider` kullanarak **Java'da tekil çoğul formları oluşturmayı** öğrendiniz. Bu hafif bileşen, arama sonuçlarının alaka düzeyini ve birçok uygulamadaki dilsel analiz doğruluğunu büyük ölçüde artırabilir.

**Sonraki adımlar:**  
- Daha karmaşık dil kuralları (düzensiz çoğullar, kök bulma) deneyin.  
- Sağlayıcıyı bir indeksleme hattına entegre edin ve geri getirme (recall) iyileştirmelerini ölçün.  
- Eşanlamlı sözlükler ve özel analizörler gibi diğer GroupDocs.Search özelliklerini keşfedin.

**Eylem Çağrısı:** `SimpleWordFormsProvider`'ı bugün kendi projenize ekleyin ve arama deneyiminizi nasıl zenginleştirdiğini görün!

## SSS Bölümü

**1. GroupDocs.Search for Java nedir?**  
Tam metin arama, indeksleme ve dil özellikleri sunan güçlü bir kütüphanedir—özelleştirilmiş kelime‑form sağlayıcıları ekleme yeteneği dahil.

**2. SimpleWordFormsProvider nasıl çalışır?**  
Basit ek‑tabanlı kuralları (“s/es” kaldırma, “y”yi “is”e dönüştürme ve “s/es” ekleme) uygulayarak alternatif formlar üretir.

**3. Kelime formu oluşturma kurallarını özelleştirebilir miyim?**  
Kesinlikle. `getWordForms` metodunu düzensiz formları, yerel‑spesifik kuralları veya dış sözlüklerle entegrasyonu içerecek şekilde değiştirin.

**4. Bu özellik için yaygın uygulamalar nelerdir?**  
Arama motorları, metin‑analiz hatları ve CMS platformları tekil/çoğul varyantları tanıyarak fayda sağlar.

**5. Üretim kullanımı için ticari bir lisansa ihtiyacım var mı?**  
Evet—deneme sürümü API'yi keşfetmenizi sağlarken, satın alınan lisans kullanım sınırlamalarını kaldırır ve destek sunar.

---

**Son Güncelleme:** 2026-02-21  
**Test Edilen:** GroupDocs.Search 25.4 (Java)  
**Yazar:** GroupDocs