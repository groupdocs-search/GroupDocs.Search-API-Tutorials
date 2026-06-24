---
date: '2026-03-06'
description: GroupDocs.Search for Java ile birden fazla takma ad eklemeyi, belgeleri
  indekse eklemeyi ve aranabilir indeksleri verimli bir şekilde yönetmeyi öğrenin.
keywords:
- GroupDocs.Search Java
- index management
- alias dictionary
title: GroupDocs.Search for Java'da Birden Çok Takma Ad Eklemek ve Belgeleri İndexe
  Eklemek
type: docs
url: /tr/java/indexing/groupdocs-search-java-efficient-index-alias-management/
weight: 1
---

# GroupDocs.Search Java'da Birden Çok Takma Ad Eklemek ve Belge Dizinine Eklemek: Kapsamlı Rehber

Bugünün veri odaklı dünyasında, **birden çok takma ad eklemek** ve **belge dizinine eklemek**, arama çözümünüze belirgin bir performans avantajı sağlar. İster binlerce sözleşme, ürün kataloğu ya da araştırma makalesi indeksliyor olun, GroupDocs.Search for Java, **arama yapılabilir indeks** yapıları oluşturmanıza ve takma ad sözlükleriyle sorguları ince ayarlamanıza olanak tanır—tüm bunlar uygulamayı basit ve hızlı tutarak.

## Hızlı Yanıtlar
- **GroupDocs.Search'i kullanmaya başlamak için ilk adım nedir?** Maven bağımlılığını ekleyin ve bir `Index` nesnesi başlatın.  
- **Belge dizinine nasıl eklenir?** Dosyalarınızı içeren klasörle `index.add("<folder_path>")` metodunu çağırın.  
- **Karmaşık sorgular için takma adlar oluşturabilir miyim?** Evet—kısa tokenları tam sorgu ifadelerine eşlemek için takma ad sözlüğünü kullanın ve ayrıca **birden çok takma ad ekleyebilirsiniz** toplu olarak.  
- **Takma ad sözlüklerini dışa ve içe aktarmak mümkün mü?** Kesinlikle—`exportDictionary` ve `importDictionary` metodlarını kullanın.  
- **Hangi GroupDocs.Search sürümü gereklidir?** 25.4 veya üzeri (öğreticide 25.4 kullanılmıştır).  

## “Belge dizinine eklemek” ne demektir?
Bir indeks'e belge eklemek, ham dosyaları (PDF, DOCX, TXT vb.) GroupDocs.Search'e beslemek anlamına gelir; böylece kütüphane içeriği analiz eder ve bir **arama yapılabilir indeks** oluşturur. İndeksleme tamamlandığında, tüm bu belgeler üzerinde hızlı, tam metin sorguları çalıştırabilirsiniz.

## Neden Takma Adları Yönetmeliyiz?
Takma adlar, uzun ve tekrarlayan sorgu parçalarını kısa, akılda kalıcı tokenlarla (ör. `@t` → `(gravida OR promotion)`) değiştirmenizi sağlar. Bu, sadece arama dizelerinizi kısaltmakla kalmaz, aynı zamanda okunabilirliği, bakım kolaylığını ve **arama performansını optimize eder**, özellikle sorgular karmaşıklaştığında.

## Birden Çok Takma Ad Nasıl Eklenir?
GroupDocs.Search, bir kerede birçok takma ad‑değiştirme çiftini eklemenizi sağlayan kullanışlı bir `addRange` metodu sunar. Bu toplu işlem, her takma adı tek tek eklemeye göre yükü azaltır.

## Önkoşullar

- **GroupDocs.Search for Java** ≥ 25.4.  
- **JDK** (herhangi bir yeni sürüm, ör. 11+).  
- **IntelliJ IDEA** veya **Eclipse** gibi bir IDE.  
- Temel Java ve Maven bilgisi.  

## GroupDocs.Search for Java'ı Kurma

### Maven Kullanarak
Depoyu ve bağımlılığı `pom.xml` dosyanıza ekleyin:

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
Alternatif olarak, resmi siteden en son JAR dosyasını indirin:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Lisans Edinme Adımları
1. **Ücretsiz Deneme** – taahhüt olmadan tüm özellikleri keşfedin.  
2. **Geçici Lisans** – değerlendirme için kısa vadeli bir anahtar isteyin.  
3. **Tam Satın Alma** – üretim kullanımı için kalıcı bir lisans edinin.

### Temel Başlatma ve Kurulum

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        // Specify the directory to store indices
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
        
        // Create or open an index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## Uygulama Kılavuzu

Aşağıda her özelliğin tam bir yürütmesi yer almaktadır. Önce açıklamaları okuyun, ardından ilgili kod bloğunu kopyalayın.

### Bir İndeks Oluşturma veya Açma

**Belge dizinine eklemek – önce aktif bir Index örneğine ihtiyacınız var.**

#### Adım 1: Index sınıfını içe aktarın
```java
import com.groupdocs.search.Index;
```

#### Adım 2: İndeks dosyalarının nerede saklanacağını tanımlayın
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
```

#### Adım 3: Yeni bir indeks oluşturun veya mevcut birini açın
```java
Index index = new Index(indexFolder);
```

### Bir İndekse Belge Eklemek

İndeks artık mevcut olduğuna göre, **belge dizinine ekleyelim**.

#### Adım 1: Kaynak klasörünüze işaret edin
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/Documents";
```

#### Adım 2: O klasörden desteklenen her dosyayı ekleyin
```java
index.add(documentsFolder);
```

> **Pro ipucu:** Yeni dosyalar geldiğinde bu adımı çalıştırın. GroupDocs.Search yalnızca yeni içeriği indeksleyecek, mevcut girişleri dokunulmaz bırakacaktır. Bu, **incremental indexing java**'nın özüdür.

### Takma Ad Sözlüğünü Yönetme

Takma adlar, kısa tokenları karmaşık sorgu dizelerine eşlemenizi sağlar. Eski girişleri temizlemeyi, tek takma ad eklemeyi ve toplu olarak **birden çok takma ad eklemeyi** ele alacağız.

#### Mevcut Takma Adları Temizleme
```java
if (index.getDictionaries().getAliasDictionary().getCount() > 0) {
    index.getDictionaries().getAliasDictionary().clear();
}
```

#### Tek Takma Ad Eklemek
```java
index.getDictionaries().getAliasDictionary().add("t", "(gravida OR promotion)");
index.getDictionaries().getAliasDictionary().add("e", "(viverra OR farther)");
```

#### Birden Çok Takma Ad Eklemek
```java
AliasReplacementPair[] pairs = new AliasReplacementPair[] {
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};
index.getDictionaries().getAliasDictionary().addRange(pairs);
```

### Takma Ad Değişimlerini Sorgulama

Tanımladığınız herhangi bir takma adın tam metnini alabilirsiniz:

```java
if (index.getDictionaries().getAliasDictionary().contains("e")) {
    String replacement = index.getDictionaries().getAliasDictionary().getText("e");
}
```

### Takma Ad Sözlüğünü Dışa ve İçe Aktarma

Dışa aktarma, yedekleme veya ortamlar arasında paylaşım için kullanışlıdır.

#### Takma Adları Dışa Aktar
```java
String fileName = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.getDictionaries().getAliasDictionary().exportDictionary(fileName);
```

#### Takma Adları İçe Aktar
```java
index.getDictionaries().getAliasDictionary().importDictionary(fileName);
```

### Takma Ad Sorgularını Kullanarak Arama

Takma adlar yerinde olduğunda, arama dizeleriniz çok daha temiz olur:

```java
String query = "@t OR @e";
SearchResult result = index.search(query);
```

`@` sembolü, GroupDocs.Search'e tokenı aramayı yürütmeden önce tam ifadesiyle değiştirmesini söyler.

## Pratik Uygulamalar

| Senaryo | Takma Adlar Nasıl Yardımcı Olur |
|----------|-------------------------------|
| **Hukuki Belge Yönetimi** | Dava numaralarını (`@case123`) karmaşık Boolean ifadelerine eşleyerek geri getirmeyi hızlandırır. |
| **E‑ticaret Ürün Araması** | Yaygın özellik kombinasyonlarını (`@sale`) `(discounted OR clearance)` ile değiştirir. |
| **Araştırma Veritabanları** | `@year2020` kullanarak birçok makale için tarih aralığı filtresine genişletir. |

## Performans Düşünceleri

- **Artımlı İndeksleme:** Yalnızca yeni veya değişen dosyaları ekleyin; tam yeniden indekslemeden kaçının.  
- **JVM Ayarı:** Büyük veri kümeleri için yeterli yığın belleği ayırın (`-Xmx4g`).  
- **Toplu Takma Ad Güncellemeleri:** Bir kerede birçok takma ad eklemek için `addRange` kullanın, yükü azaltır.  
- **Arama Performansını Optimize Et:** Takma ad sözlüğünü hafif tutun ve tokenları akıllıca yeniden kullanarak sorgu ayrıştırma süresini minimize edin.

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|-------|
| Yeni dosyalar aranabilir değil | `index.add(newFolder)` komutunu tekrar çalıştırın; GroupDocs.Search yalnızca görülmemiş dosyaları indeksler. |
| Takma ad boş sonuç döndürüyor | Takma ad anahtarının (`@`) doğru şekilde ön eklenmiş olduğunu ve sözlüğün tokenı içerdiğini doğrulayın. |
| Toplu indeksleme sırasında yüksek bellek kullanımı | JVM yığın belleğini artırın (`-Xmx`) ve daha küçük partilerde indekslemeyi düşünün. |

## Sıkça Sorulan Sorular

**S: GroupDocs.Search for Java'ı kullanmanın temel faydası nedir?**  
C: Güçlü, kutudan çıkar çıkmaz indeksleme ve tam metin arama yetenekleri sunar, **belge dizinine eklemenizi** hızlı bir şekilde yapmanızı ve yüksek performansla sorgulamanızı sağlar.

**S: GroupDocs.Search'ı veritabanlarıyla kullanabilir miyim?**  
C: Evet—herhangi bir kaynaktan (SQL, NoSQL, CSV) veri çıkarıp aynı `add` metodlarıyla indekse besleyebilirsiniz.

**S: Takma adlar arama verimliliğini nasıl artırır?**  
C: Takma adlar, karmaşık sorgu mantığını bir kez depolayıp kısa tokenlarla yeniden kullanmanıza olanak tanır, sorgu ayrıştırma süresini azaltır ve **takma adlarla arama** yaparken insan hatasını en aza indirir.

**S: Tüm sözlüğü yeniden oluşturmadan mevcut bir takma adı güncellemek mümkün mü?**  
C: Kesinlikle—aynı anahtarla `add` metodunu çağırın; kütüphane önceki değeri üzerine yazar.

**S: Aramam beklenmedik sonuçlar döndürürse ne yapmalıyım?**  
C: Takma ad tanımlarının doğru olduğunu doğrulayın, yeni eklenen belgeleri yeniden indeksleyin ve tokenizasyon sorunları için analizör ayarlarını kontrol edin.

---

**Son Güncelleme:** 2026-03-06  
**Test Edilen Sürüm:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs