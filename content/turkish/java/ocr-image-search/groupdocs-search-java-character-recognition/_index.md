---
date: '2026-01-11'
description: GroupDocs.Search for Java kullanarak özel arama dizini oluşturmayı, gelişmiş
  OCR ve görüntü araması için normal ve karışık karakterleri yapılandırmayı öğrenin.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Karakter Tanıma ile Özel Arama Dizini Oluşturma – GroupDocs.Search Java
type: docs
url: /tr/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Karakter Tanıma ile GroupDocs.Search for Java Kullanarak Özel Arama Dizini Oluşturma

Modern belge‑ağırlıklı uygulamalarda, **özel bir arama dizini oluşturmak**, metninizin inceliklerini—tireler, alt çizgiler veya dile özgü semboller gibi—anlayan bir indeks, hızlı ve doğru geri getirme için gereklidir. Bu öğretici, **GroupDocs.Search for Java** içinde karakter tanımasını yapılandırmayı, hem normal karakterleri (harfler, rakamlar, alt çizgiler) hem de birleşik karakterleri (ör. tire) kapsayacak şekilde adım adım gösterir. Sonunda, OCR veya görüntü‑arama senaryonuzun tam ihtiyaçlarına uygun bir indeks oluşturabileceksiniz.

## Hızlı Yanıtlar
- **“Özel arama dizini oluşturmak” ne anlama geliyor?** Belirli sembolleri harf ya da birleşik karakter olarak ele alacak şekilde bir indeks yapılandırmak, bunları yok saymamak demektir.  
- **Hangi kütüphane kullanılıyor?** GroupDocs.Search for Java (yazım zamanı v25.4).  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme çalışır; üretim için ücretli lisans gerekir.  
- **Hem PDF hem de görüntüleri indeksleyebilir miyim?** Evet—GroupDocs.Search, doğru yapılandırıldığında görüntüler ve PDF’lerde OCR’ı destekler.  
- **Maven gerekli mi?** Maven, bağımlılık yönetimi için önerilen yoldur, ancak Gradle ya da manuel JAR’lar da kullanılabilir.

## Özel Arama Dizini Nedir?
Özel bir arama dizini, arama motorunun karakterleri nasıl yorumladığını tanımlamanıza izin verir. Varsayılan olarak birçok sembol yok sayılır; bu da `ABC-123` gibi dava numaraları ya da `my_variable` gibi kod parçacıkları için eşleşmelerin kaçırılmasına yol açabilir. Alfabe sözlüğünü ayarlayarak, motorun arama yapılabilir metin olarak neyi kabul edeceği üzerinde tam kontrol sahibi olursunuz.

## Normal ve Birleşik Karakterleri Neden Yapılandırmalıyız?
- **Normal karakterler** (harfler, rakamlar, alt çizgiler) bağımsız tokenlar olarak ele alınır, tam eşleşme aramalarını iyileştirir.  
- **Birleşik karakterler** (tireler, eğik çizgiler) kelimeleri birleştirir; bunları yapılandırmak, istenmeyen token bölünmesini önler ve bu durum yasal referanslar, ürün kodları veya kaynak‑kod indekslemesi için kritiktir.

## Ön Koşullar
- **JDK 8** veya daha yeni bir sürüm yüklü olmalı.  
- **Maven** bağımlılık yönetimi için gerekli.  
- **GroupDocs.Search for Java** kütüphanesine erişim (Maven üzerinden ya da resmi siteden indirilebilir).  

### Gerekli Kütüphaneler ve Bağımlılıklar
`pom.xml` dosyanıza aşağıdaki depo ve bağımlılık girdilerini ekleyin. XML bloğu değiştirilmemelidir.

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

Ayrıca en yeni JAR’ları [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Lisans Edinme
- **Ücretsiz Deneme** – erken denemeler için idealdir.  
- **Geçici Lisans** – daha uzun geliştirme döngüleri için kullanışlıdır.  
- **Üretim Lisansı** – ticari dağıtımda zorunludur.  

Resmi portal üzerinden lisans alın: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Temel Başlatma
Aşağıdaki kod parçacığı, boş bir indeks oluşturmak için gereken minimum kodu gösterir. Değiştirmeden bırakın; ilerleyen bölümlerde üzerine ekleyeceğiz.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## GroupDocs.Search for Java Kurulumu

### Maven ile Kurulum
*Ön Koşullar* bölümündeki Maven yapılandırması ihtiyacınız olan tek şeydir. Ekledikten sonra `mvn clean install` komutunu çalıştırarak ikili dosyaları indirin.

### Ortam Kurulum Gereksinimleri
- **İndeks klasörü** ve **belge klasörü** diskte mevcut olmalı.  
- Mutlak yollar kullanın ya da IDE’nizin göreli yolları doğru çözümleyecek şekilde ayarlandığından emin olun.  

## Uygulama Kılavuzu

Aşağıda iki ayrı özelliği adım adım inceliyoruz: **normal karakterler** ve **birleşik karakterler**. Her özellik aynı desen izler—yolları tanımla, indeksi oluştur, karakter sözlüğünü ayarla ve sonunda belgelerini indeksle.

### Özellik 1 – Normal Karakterler

#### Genel Bakış
Normal karakterler bağımsız tokenlar olarak ele alınır. Bu, rakamların, harflerin ve alt çizgilerin tam olarak göründükleri gibi aranabilir olmasını istediğinizde idealdir.

#### Adım‑Adım Uygulama

**1️⃣ Yolları Ayarla**  
İndeksin nerede saklanacağını ve kaynak belgelerinizin nerede bulunduğunu tanımlayın.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ İndeksi Oluştur ve Yapılandır**  
İndeksi örnekleyin ve önceden var olan alfabe yapılandırmasını temizleyin.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Normal Karakterleri Tanımla**  
Rakamları, Latin harflerini ve alt çizgiyi içeren bir karakter dizisi oluşturun.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Belgeleri İndeksle**  
Kaynak klasörden tüm dosyaları yeni yapılandırılmış indekse ekleyin.

```java
index.add(documentFolder);
```

### Özellik 2 – Birleşik Karakterler

#### Genel Bakış
Birleşik karakterler (tire gibi) genellikle iki kelimeyi birleştirir. Bunları *birleşik* olarak işaretlemek, motorun indeksleme sırasında çevredeki tokenları bir arada tutmasını sağlar.

#### Adım‑Adım Uygulama

**1️⃣ Yolları Ayarla**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ İndeksi Oluştur ve Yapılandır**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Birleşik Karakterleri Tanımla**  
Burada sözlüğe tire karakterinin birleşik karakter olarak ele alınması gerektiğini söylüyoruz.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Belgeleri İndeksle**  

```java
index.add(documentFolder);
```

## Pratik Uygulamalar

### Kullanım Durumu 1 – Hukuki Belge Yönetimi
Hukuki dosyalarda genellikle `2023-AB-456` gibi dava numaraları bulunur. Alt çizgi ve tireleri yapılandırarak, aramalar bu tanımlayıcıları bölmeden tam eşleşme döndürür.

### Kullanım Durumu 2 – Kaynak‑Kod Depoları
Geliştiriciler, alt çizgi (`my_variable`) ve tire (`my-function`) gibi sembollerin anlamlı olduğu kod parçacıklarını aramak zorundadır. Özel karakter tanıma, arama motorunun bu sembolleri korumasını sağlar.

### Kullanım Durumu 3 – Çok Dilli Veri Setleri
Ek alfabeler kullanan dillerle çalışırken, normal karakter kümesini bu Unicode aralıklarını içerecek şekilde genişletebilir, böylece çapraz‑dil arama sonuçlarının doğruluğunu garantileyebilirsiniz.

## Performans Düşünceleri

- **Kaynak Yönetimi** – Yığın kullanımına dikkat edin; büyük indeksler artımlı commit’lerden faydalanır.  
- **Çöp Toplama** – İşiniz bittiğinde `Index` nesnelerini serbest bırakın, böylece JVM belleği geri kazanabilir.  
- **İndeks Optimizasyonu** – Mümkünse periyodik olarak `index.optimize()` (varsa) çağırarak indeksi sıkıştırın ve sorgu hızını artırın.  

## Sonuç

Artık **GroupDocs.Search for Java** kullanarak normal ve birleşik karakterleri ayırt eden **özel bir arama dizini** oluşturmayı biliyorsunuz. Bu ince ayar, OCR‑bilinçli, yüksek performanslı arama çözümlerini yasal, geliştirme veya çok dilli ortamlara göre özelleştirmenizi sağlar.

**Sonraki Adımlar**  
- Latin dışı alfabeler için ek Unicode aralıklarıyla deneyler yapın.  
- Karakter yapılandırmasını, stemming ya da eş anlamlılar gibi diğer GroupDocs.Search özellikleriyle birleştirin.  
- İndeksi bir REST API’ye entegre ederek arama yeteneklerini ön‑uç uygulamalarına sunun.

## Sıkça Sorulan Sorular

**S:** *`CharacterType.Letter` ne amaçla kullanılır?*  
**C:** Sağlanan karakterleri normal harfler olarak ele almasını söyler; böylece indeksleme sırasında ayrı tokenlar olarak işlenir.

**S:** *Aynı indekste normal ve birleşik karakterleri karıştırabilir miyim?*  
**C:** Evet—her tip için `setRange` metodunu çağırmanız yeterlidir; sözlük her iki yapılandırmayı aynı anda yönetir.

**S:** *Alfabe değiştirildikten sonra indeksi yeniden oluşturmak gerekir mi?*  
**C:** Kesinlikle. Karakter sözlüğü değişiklikleri tokenizasyonu etkiler, bu yüzden yeni kuralları uygulamak için belgeleri yeniden indekslemelisiniz.

**S:** *Tanımlayabileceğim özel karakter sayısında bir sınırlama var mı?*  
**C:** Kütüphane tam Unicode aralığını destekler; çok büyük bir set eklemek performansı düşürebilir, bu yüzden yalnızca ihtiyacınız olan karakterleri ekleyin.

**S:** *Bu, OCR doğruluğunu nasıl etkiler?*  
**C:** İndeksin karakter setini OCR motorunun çıktısıyla hizalayarak yanlış negatifleri azaltır ve genel arama alaka düzeyini artırır.

---

**Son Güncelleme:** 2026-01-11  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs