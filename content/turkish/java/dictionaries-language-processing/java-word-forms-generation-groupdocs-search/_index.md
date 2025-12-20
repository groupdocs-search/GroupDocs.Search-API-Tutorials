---
date: '2025-12-20'
description: GroupDocs.Search ile Java’da kelime biçimleri sağlayıcısı oluşturmayı
  öğrenin. Arama, metin analizi ve daha fazlası için tekil ve çoğul biçimler oluşturun.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Java'da GroupDocs.Search API Kullanarak Word Formları Sağlayıcısı Oluştur
type: docs
url: /tr/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Java'da GroupDocs.Search API Kullanarak Kelime Formları Sağlayıcısı Oluşturma

Tekil kelimeleri çoğula—veya tersine—dönüştürmek, dil‑bilgisine duyarlı uygulamalar geliştirirken sık karşılaşılan bir engeldir. Bu rehberde **kelime formları sağlayıcısı** oluşturacak ve arama motorunuzun ya da metin‑analiz aracınızın farklı kelime varyasyonlarını otomatik olarak anlayıp eşleştirebilmesini sağlayacaksınız.

İster bir arama motoru, ister bir içerik‑yönetim sistemi, ister doğal dil işleyen herhangi bir Java uygulaması geliştirin, kelime‑formu üretimini öğrenmek sonuçlarınızı daha doğru hâle getirir ve kullanıcılarınızı mutlu eder. Başlamadan önce gerekli ön koşullara göz atalım.

## Hızlı Yanıtlar
- **Kelime formları sağlayıcısı ne yapar?** Verilen bir kelimenin alternatif formlarını (tekil, çoğul vb.) üretir, böylece aramalar tüm varyantları eşleştirebilir.  
- **Hangi kütüphane gereklidir?** GroupDocs.Search for Java (sürüm 25.4 veya daha yenisi).  
- **Lisans gerekir mi?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gerekir.  
- **Hangi Java sürümü desteklenir?** JDK 8 ve üzeri.  
- **Kaç satır kod gerekir?** Basit bir sağlayıcı uygulaması için yaklaşık 30 satır.

## “Create Word Forms Provider” özelliği nedir?
Bir **kelime formları sağlayıcısı** bileşeni, `IWordFormsProvider` arayüzünü uygulayan özel bir sınıftır. Bir kelime alır ve kurallarınıza göre olası formların bir dizisini döndürür—tekil, çoğul veya diğer dilsel varyasyonlar. Bu sayede indeks “cat” ve “cats” gibi kelimeleri eşdeğer kabul eder, geri çağırma (recall) artar ve kesinlik (precision) kaybolmaz.

## Kelime‑formu üretimi için neden GroupDocs.Search kullanmalı?
- **Yerleşik genişletilebilirlik:** Kendi sağlayıcınızı indeksleme boru hattına doğrudan takabilirsiniz.  
- **Performans‑optimizasyonu:** Kütüphane büyük indeksleri verimli bir şekilde işler ve sonuçları önbelleğe alarak ekstra hız elde edebilirsiniz.  
- **Çapraz‑dil desteği:** Bu öğretici Java üzerine odaklansa da aynı kavramlar .NET ve diğer platformlarda da geçerlidir.

## Ön Koşullar

**Kelime formları sağlayıcısını** uygulamaya koymadan önce şunların kurulu olduğundan emin olun:

- **Maven** yüklü ve makinenizde JDK 8 veya daha yenisi kurulu.  
- Java geliştirme ve Maven’in `pom.xml` yapılandırması hakkında temel bilgi.  
- GroupDocs.Search Java kütüphanesine erişim (sürüm 25.4 veya sonrası).  

## GroupDocs.Search for Java Kurulumu

### Maven Yapılandırması

Aşağıda gösterildiği gibi `pom.xml` dosyanıza depo ve bağımlılığı **tam olarak** ekleyin:

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

Alternatif olarak, resmi sürüm sayfasından en yeni JAR dosyasını indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinme Adımları

GroupDocs.Search’i sınırlama olmadan kullanmak için:

1. **Ücretsiz Deneme:** Temel özellikleri keşfetmek üzere bir deneme hesabı oluşturun.  
2. **Geçici Lisans:** Uzun vadeli testler için geçici bir anahtar talep edin.  
3. **Satın Alma:** Sınırsız üretim kullanımı için ticari bir lisans alın.

### Temel Başlatma ve Kurulum

Aşağıdaki kod parçası, belgeler ve kelime‑formu mantığı ekleyeceğiniz bir indeks oluşturmayı gösterir:

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

Aşağıda, basit tekil‑çoğul ve çoğul‑tekil dönüşümleri yapan **kelime formları sağlayıcısı** oluşturma adımlarını bulacaksınız.

### SimpleWordFormsProvider’ı Gerçekleştirme

#### Genel Bakış

Özel sağlayıcımız şunları yapacak:

- Tekil tahmini için sonundaki “es” veya “s” karakterlerini kaldıracak.  
- Sonu “y” ile biten kelimelerde “y”yi “is” ile değiştirerek çoğul form üretecek (ör. “city” → “citis”).  
- Temel çoğul adayları oluşturmak için “s” ve “es” ekleyecek.

#### Adım 1 – Sınıf İskeletini Oluşturma

`IWordFormsProvider` arayüzünü uygulayan bir sınıf tanımlayarak başlayın. İçe aktarma (import) satırlarını değiştirmeyin:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Adım 2 – `getWordForms` Metodunu Uygulama

Olası formların listesini oluşturan metodu ekleyin. Bu blok, temel mantığı içerir; daha karmaşık kurallar eklemek isterseniz ileride genişletebilirsiniz.

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

- **Tekilleştirme:** Yaygın çoğul eklerini (`es`, `s`) tespit eder ve temel kelimeyi tahmin etmek için kaldırır.  
- **Çoğullama:** `y` ile biten isimlerde onu `is` ile değiştirir; bu basit kural birçok İngilizce kelime için işe yarar.  
- **Ek Ekleme:** Önceki kontrollerle yakalanamayan düzenli çoğul formları için `s` ve `es` ekler.

#### Sorun Giderme İpuçları

- **Büyük/Küçük Harf Duyarlılığı:** Metod, karşılaştırma için `toLowerCase()` kullanır; böylece “Cats” ve “cats” aynı davranışı gösterir.  
- **Köşe Durumları:** Ek uzunluğundan kısa kelimeler, boş string döndürmemek için yok sayılır.  
- **Performans:** Büyük sözlüklerde sonuçları bir `ConcurrentHashMap` içinde önbelleğe almayı düşünün.

## Pratik Uygulamalar

**Kelime formları sağlayıcısı** uygulamak, aşağıdaki gerçek‑dünya senaryolarını güçlendirebilir:

1. **Arama Motorları:** Kullanıcı “mouse” yazdığında “mice” içeren belgeler de bulunmalıdır. Sağlayıcı, bu tür düzensiz formları üretebilir.  
2. **Metin Analiz Araçları:** Duygu analizi veya varlık çıkarımı, tüm kelime varyantları tanındığında daha güvenilir olur.  
3. **İçerik Yönetim Sistemleri:** Otomatik etiket oluşturma, çoğul eşanlamlıları da kapsayarak SEO ve iç bağlantıları iyileştirir.

## Performans Düşünceleri

Sağlayıcıyı üretim ortamına entegre ederken şu ipuçlarını aklınızda tutun:

- **Sık Kullanılan Formları Önbellekle:** Aynı kelimeyi tekrar tekrar hesaplamaktan kaçınmak için sonuçları bellekte saklayın.  
- **JVM Heap’ini İzle:** Büyük indeksler bellek baskısını artırabilir; `-Xmx` ayarını uygun şekilde yapılandırın.  
- **Verimli Koleksiyonlar Kullan:** Küçük setler için `ArrayList` yeterli, ancak binlerce form söz konusu olduğunda `HashSet` kullanarak tekrarları hızlıca ortadan kaldırabilirsiniz.

**En İyi Uygulamalar**

- Performans yamalarından faydalanmak için kütüphaneyi güncel tutun.  
- Gerçekçi sorgu yükleriyle sağlayıcıyı profil çıkararak olası darboğazları erken tespit edin.  

## Sonuç

GroupDocs.Search for Java kullanarak **kelime formları sağlayıcısı** oluşturmayı öğrendiniz. Bu hafif bileşen, arama sonuçlarının alaka düzeyini ve dilsel analiz doğruluğunu birçok uygulamada büyük ölçüde artırabilir.  

**Sonraki adımlar:**  
- Daha sofistike dil kuralları (düzensiz çoğullar, kök bulma) deneyin.  
- Sağlayıcıyı bir indeksleme boru hattına entegre edin ve geri çağırma (recall) iyileştirmelerini ölçün.  
- GrupDocs.Search’in eşanlamlı sözlükleri ve özel analizörleri gibi diğer özelliklerini keşfedin.

**Eylem Çağrısı:** `SimpleWordFormsProvider` sınıfını kendi projenize ekleyin ve arama deneyiminizin nasıl zenginleştiğini görün!

## SSS Bölümü

**1. GroupDocs.Search for Java nedir?**  
Tam‑metin arama, indeksleme ve dil özellikleri sunan güçlü bir kütüphanedir—özelleştirilebilir kelime‑formu sağlayıcıları da dahil.

**2. SimpleWordFormsProvider nasıl çalışır?**  
Basit ek‑tabanlı kuralları (“s/es” kaldırma, “y”yi “is”e çevirme ve “s/es” ekleme) uygulayarak alternatif formlar üretir.

**3. Kelime formu üretim kurallarını özelleştirebilir miyim?**  
Kesinlikle. `getWordForms` metodunu değiştirerek düzensiz formlar, bölge‑spesifik kurallar veya harici sözlük entegrasyonları ekleyebilirsiniz.

**4. Bu özelliğin yaygın uygulamaları nelerdir?**  
Arama motorları, metin‑analiz boru hatları ve CMS platformları tekil/çoğul varyantları tanıyarak fayda sağlar.

**5. Üretim kullanımı için ticari lisans gerekir mi?**  
Evet—deneme sürümü API’yı keşfetmenizi sağlar, ancak üretim ortamında sınırsız kullanım ve destek için satın alınmış bir lisans gereklidir.

---

**Son Güncelleme:** 2025-12-20  
**Test Edilen Sürüm:** GroupDocs.Search 25.4 (Java)  
**Yazar:** GroupDocs  

---