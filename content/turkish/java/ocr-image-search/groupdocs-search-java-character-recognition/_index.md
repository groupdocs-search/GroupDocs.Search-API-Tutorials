---
date: '2026-03-17'
description: GroupDocs.Search for Java ile indeks oluşturmayı, normal ve karışık karakterleri
  yapılandırmayı ve yasal dava numaraları ile OCR görüntüleri için aramayı optimize
  etmeyi öğrenin.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Java'da Karakter Tanıma ile İndeks Oluşturma
type: docs
url: /tr/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

 GroupDocs  

But keep bold formatting.

Now ensure we didn't translate any URLs, code placeholders, variable names, function names. We kept them.

Check for any markdown links: we kept them.

Check for any shortcodes: none.

Check for any code fences: placeholders only.

Now produce final content.# Karakter Tanıma Kullanarak GroupDocs.Search for Java ile Index Oluşturma

Modern belge‑ağırlıklı uygulamalarda, **index oluşturma** yönteminin metninizin inceliklerini—örneğin tireler, alt çizgiler veya dile özgü semboller—göz önünde bulundurması hızlı ve doğru geri getirme için çok önemlidir. Bu öğreticide **GroupDocs.Search for Java** içinde karakter tanımını yapılandırmayı adım adım göstereceğiz; hem normal karakterleri (harfler, rakamlar, alt çizgiler) hem de birleşik karakterleri (ör. tire) kapsayacak. Sonunda, OCR veya görüntü‑arama senaryonuzun tam ihtiyaçlarına uygun bir index oluşturabileceksiniz; ister yasal dava numaralarını, kaynak‑kod depolarını ya da çok dilli PDF'leri indeksliyor olun.

## Hızlı Yanıtlar
- **“create custom search index” ne anlama geliyor?** Bir index'i belirli sembolleri harf ya da birleşik karakter olarak ele alacak şekilde yapılandırmak, yok saymak yerine.  
- **Hangi kütüphane kullanılıyor?** GroupDocs.Search for Java (yazım zamanı v25.4).  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme yeterlidir; üretim için ücretli lisans gereklidir.  
- **PDF'leri ve görüntüleri aynı anda indeksleyebilir miyim?** Evet—GroupDocs.Search, doğru yapılandırıldığında görüntüler ve PDF'lerde OCR'ı destekler.  
- **Maven gerekli mi?** Maven, bağımlılıkları yönetmenin önerilen yoludur, ancak Gradle ya da manuel JAR'lar da kullanılabilir.  

## Özel Arama Index'i Nedir?
Özel bir arama index'i, arama motorunun karakterleri nasıl yorumlayacağını tanımlamanıza olanak verir. Varsayılan olarak, birçok sembol yok sayılır; bu da dava numaraları (`2023-AB-456`) veya kod parçacıkları (`my_variable`) gibi şeylerde eşleşmelerin kaçırılmasına yol açabilir. Alfabe sözlüğünü ayarlamak, motorun arama yapılabilir metin olarak neyi kabul edeceği üzerinde tam kontrol sağlar.

## Neden Yasal Dava Numaraları İçin Normal ve Birleşik Karakterleri Yapılandırmalıyız?
- **Normal karakterler** (harfler, rakamlar, alt çizgiler) ayrı ayrı tokenleştirilir, tanımlayıcılar için tam eşleşmeli aramaları mümkün kılar.  
- **Birleşik karakterler** (tireler, bölücü çizgiler) ilgili tokenleri bir arada tutar, dava numaraları, ürün kodları veya dosya yollarının istenmeyen bölünmesini önler.  
- Bu yapılandırma, token parçalanmasını azaltarak ve OCR‑oluşmuş içerik için alaka düzeyini artırarak **arama index'i performansını optimize eder**.  

## Ön Koşullar
- **JDK 8** veya daha yeni bir sürüm yüklü olmalı.  
- **Maven**, bağımlılık yönetimi için.  
- **GroupDocs.Search for Java** kütüphanesine erişim (Maven üzerinden ya da resmi siteden indirilebilir).  

### Gerekli Kütüphaneler ve Bağımlılıklar
`pom.xml` dosyanıza (aşağıda gösterildiği gibi) depo ve bağımlılık girişlerini ekleyin. XML bloğu değiştirilmemelidir.

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

En son JAR dosyalarını ayrıca [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Lisans Edinme
- **Ücretsiz Deneme** – erken denemeler için mükemmeldir.  
- **Geçici Lisans** – daha uzun geliştirme döngüleri için faydalıdır.  
- **Üretim Lisansı** – ticari dağıtım için gereklidir.  

Resmi portal üzerinden lisans alın: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Temel Başlatma
Aşağıdaki kod parçacığı, boş bir index oluşturmak için gereken en temel kodu gösterir. Değiştirmeden bırakın; daha sonra üzerine ekleyeceğiz.

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
*Ön Koşullar* bölümündeki Maven yapılandırması ihtiyacınız olan tek şeydir. Ekledikten sonra ikili dosyaları indirmek için `mvn clean install` komutunu çalıştırın.

### Ortam Kurulum Gereksinimleri
- **index klasörünün** ve **belge klasörünün** diskte mevcut olduğundan emin olun.  
- Mutlak yollar kullanın veya IDE'nizin göreli yolları doğru çözümleyecek şekilde yapılandırın.  

## Uygulama Kılavuzu

Aşağıda iki ayrı özelliği ele alıyoruz: **normal karakterler** ve **birleşik karakterler**. Her özellik aynı modeli izler—yolları tanımlayın, index'i oluşturun, karakter sözlüğünü ayarlayın ve son olarak belgelerinizi indeksleyin.

### Özellik 1 – Normal Karakterler

#### Genel Bakış
Normal karakterler bağımsız tokenler olarak ele alınır. Bu, rakamların, harflerin ve alt çizgilerin tam olarak göründükleri şekilde aranabilir olmasını istediğinizde idealdir.

#### Adım‑Adım Uygulama

**1️⃣ Yolları Ayarla**  
Index'in nerede saklanacağını ve kaynak belgelerinizin nerede olduğunu tanımlayın.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index Oluştur ve Yapılandır**  
Index'i örnekleyin ve önceden var olan alfabe yapılandırmasını temizleyin.

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
Kaynak klasörden tüm dosyaları yeni yapılandırılmış index'e ekleyin.

```java
index.add(documentFolder);
```

### Özellik 2 – Birleşik Karakterler

#### Genel Bakış
Birleşik karakterler (tire gibi) genellikle iki kelimeyi bağlar. Onları *birleşik* olarak işaretlemek, motorun indeksleme sırasında çevredeki tokenleri bir arada tutmasını sağlar.

#### Adım‑Adım Uygulama

**1️⃣ Yolları Ayarla**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Index Oluştur ve Yapılandır**  

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
Hukuki dosyalar genellikle `2023-AB-456` gibi dava numaraları içerir. Alt çizgileri ve tireleri yapılandırarak, aramalar tanımlayıcıyı bölmeden tam eşleşmeler döndürür ve **hukuki dava numaralarını** verimli bir şekilde aramanıza yardımcı olur.

### Kullanım Durumu 2 – Kaynak‑Kod Depoları
Geliştiriciler, alt çizgilerin (`my_variable`) ve tirelerin (`my-function`) anlamlı olduğu kod parçacıklarını aramalıdır. Özel karakter tanıma, arama motorunun bu sembollere saygı göstermesini sağlar.

### Kullanım Durumu 3 – Çok Dilli Veri Setleri
Ek alfabeler kullanan dillerle çalışırken, bu aralıkları içerecek şekilde **Unicode karakter setini genişletebilir** ve doğru çok‑dilli arama sonuçları garantileyebilirsiniz.

### Kullanım Durumu 4 – PDF Görüntülerini İndeksleme
Taralı PDF'leri veya görüntü dosyalarını indeksliyorsanız, OCR çıktısı genellikle karışık karakterler içerir. Normal ve birleşik karakterleri doğru şekilde yapılandırmak, görüntü‑tabanlı içerik için **arama index'i performansını optimize eder**.

## Performans Düşünceleri

- **Kaynak Yönetimi** – Yığın kullanımına dikkat edin; büyük index'ler artımlı commit'lerden fayda sağlar.  
- **Garbage Collection** – İşiniz bittiğinde `Index` nesnelerini serbest bırakın, böylece JVM belleği geri alabilir.  
- **Index Optimizasyonu** – Index'i sıkıştırmak ve sorgu hızını artırmak için periyodik olarak `index.optimize()` (varsa) çağırın.  

## Sonuç

Artık **index oluşturma** konusunda, GroupDocs.Search for Java kullanarak normal ve birleşik karakterleri ayırt edebileceğinizi biliyorsunuz. Bu ince ayar kontrol, OCR‑bilinçli, yüksek performanslı arama çözümlerini hukuki, geliştirme ya da çok dilli ortamlar için özelleştirmenizi sağlar.

### Sonraki Adımlar
- Latin dışı alfabeler için ek Unicode aralıkları denemek.  
- Karakter yapılandırmasını, kök bulma (stemming) veya eş anlamlılar gibi diğer GroupDocs.Search özellikleriyle birleştirmek.  
- Index'i bir REST API'ye entegre ederek arama yeteneklerini ön‑uç uygulamalarına sunmak.

## Sıkça Sorulan Sorular

**Q:** *`CharacterType.Letter` ne amaçla kullanılır?*  
**A:** Index'e sağlanan karakterleri normal harfler olarak ele almasını söyler, böylece indeksleme sırasında ayrı ayrı tokenleştirilir.

**Q:** *Aynı index içinde normal ve birleşik karakterleri karıştırabilir miyim?*  
**A:** Evet—her tip için `setRange` metodunu çağırmanız yeterlidir; sözlük her iki yapılandırmayı aynı anda yönetir.

**Q:** *Alfabe değiştirildikten sonra index'i yeniden oluşturmalı mıyım?*  
**A:** Kesinlikle. Karakter sözlüğü değişiklikleri tokenleştirmeyi etkiler, bu yüzden yeni kuralları uygulamak için belgeleri yeniden indekslemeniz gerekir.

**Q:** *Tanımlayabileceğim özel karakter sayısında bir limit var mı?*  
**A:** Kütüphane tam Unicode aralığını destekler; çok büyük bir set eklenirse performans düşebilir, bu yüzden yalnızca gerçekten ihtiyaç duyduğunuz karakterlerle sınırlayın.

**Q:** *Bu, OCR doğruluğunu nasıl etkiler?*  
**A:** Index'in karakter setini OCR motorunun çıktısıyla hizalayarak, yanlış negatifleri azaltır ve genel arama alaka düzeyini artırır.

---

**Son Güncelleme:** 2026-03-17  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs