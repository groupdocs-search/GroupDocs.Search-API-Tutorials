---
date: '2026-09-21'
description: GroupDocs.Search kullanarak java tam metin arama dizini oluşturmayı,
  belgeleri eklemeyi ve daha doğru sonuçlar için homophone desteğini etkinleştirmeyi
  öğrenin.
keywords:
- java full text search
- homophone search java
- GroupDocs.Search Java
- document indexing java
- search index java
lastmod: '2026-09-21'
og_description: GroupDocs.Search ile java tam metin arama dizini oluşturmayı, belgeleri
  eklemeyi ve daha hızlı, daha doğru aramalar için homophone desteğini etkinleştirmeyi
  keşfedin.
og_image_alt: Illustration of a Java full text search index with homophone support
og_title: Homophones ile java tam metin arama dizini nasıl oluşturulur
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  headline: How to build a java full text search index with homophones
  type: TechArticle
- description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  name: How to build a java full text search index with homophones
  steps:
  - name: '**Install via Maven** or download directly from the provided links.'
    text: '**Install via Maven** or download directly from the provided links.'
  - name: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
    text: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
  - name: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
    text: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
  - name: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
    text: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
  - name: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
    text: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
  type: HowTo
- questions:
  - answer: A data structure that enables fast full‑text search across documents.
    question: What is a search index?
  - answer: It improves recall by matching words that sound alike, e.g., “mail” vs.
      “male”.
    question: Why use homophone recognition?
  - answer: GroupDocs.Search for Java (v25.4).
    question: Which library provides this in Java?
  - answer: A free trial works for evaluation; a permanent license is required for
      production.
    question: Do I need a license?
  - answer: JDK 8 or higher.
    question: What Java version is required?
  type: FAQPage
tags:
- java full text search
- homophone search
- GroupDocs.Search
- document indexing
- search index
title: Homophones ile java tam metin arama dizini nasıl oluşturulur
type: docs
url: /tr/java/document-management/groupdocs-search-java-homophone-document-management-guide/
weight: 1
---

# Java tam metin arama indeksi homofonlarla nasıl oluşturulur

Bu rehberde GroupDocs.Search kullanarak **java full text search** indeksi oluşturmayı, belgelere eklemeyi ve homofon desteğini etkinleştirerek aramaların benzer sesli kelimeleri anlamasını öğreneceksiniz. Öğreticinin sonunda milisaniyeler içinde sorgulanabilen hızlı, dil‑bilinçli bir indeksiniz olacak ve uygulamalarınız daha kullanıcı‑dostu ve doğru hâle gelecek.

## Hızlı cevaplar
- **Search indeksi nedir?** Belgeler arasında hızlı tam‑metin arama sağlayan bir veri yapısı.  
- **Homofon tanıma neden kullanılır?** Benzer sesli kelimeleri eşleştirerek hatırlamayı artırır, ör. “mail” vs. “male”.  
- **Java’da bunu sağlayan kütüphane hangisidir?** GroupDocs.Search for Java (v25.4).  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gerekir.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya üzeri.

## Java tam metin arama nedir?
`java full text search` belge içeriğini indeksleme sürecidir, böylece metni hızlıca sorgulayabilir ve gerçek zamanlı olarak ilgili dosyaları alabilirsiniz. İndeks, tokenleştirilmiş terimleri, konumları ve meta verileri saklar, büyük koleksiyonlarda bile alt‑saniyelik arama yanıtları sağlar.

## Neden GroupDocs.Search for Java kullanmalısınız?
GroupDocs.Search **50+ dosya formatını**—PDF, DOCX, XLSX, PPTX ve HTML dahil—destekler ve belirsiz terimler için hatırlamayı **%30** kadar artıran yerleşik bir homofon sözlüğü sunar. API, düşük‑seviye indeksleme detaylarını soyutlayarak iş mantığına odaklanmanızı sağlar. Ayrıca Maven projeleriyle kolay entegrasyon ve hızlı geliştirme için net belgeler sunar.

## Önkoşullar

Koda geçmeden önce aşağıdakilere sahip olduğunuzdan emin olun:

- **GroupDocs.Search for Java** (Maven veya doğrudan indirme yoluyla mevcut).  
- **Uyumlu bir JDK** (8 veya daha yeni).  
- **IntelliJ IDEA** veya **Eclipse** gibi bir IDE.  
- Java ve Maven hakkında temel bilgi.

### Gerekli kütüphaneler ve bağımlılıklar
GroupDocs.Search for Java gerekir. Maven ile ekleyin veya doğrudan indirin.

**Maven kurulumu:**  
Aşağıdakileri `pom.xml` dosyanıza ekleyin:

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

**Doğrudan indirme:**  
Alternatif olarak, en son sürümü [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Ortam kurulum gereksinimleri
Uyumlu bir JDK (JDK 8 veya üzeri) kurulu ve IntelliJ IDEA veya Eclipse gibi bir IDE'nin makinenizde ayarlandığından emin olun.

### Bilgi önkoşulları
Java programlama kavramlarına aşina olmak ve bağımlılık yönetimi için Maven kullanma deneyimi faydalı olacaktır. Belge indeksleme ve arama algoritmaları hakkında temel bir anlayış da yardımcı olabilir.

## GroupDocs.Search for Java kurulumu

Önkoşullar halledildikten sonra GroupDocs.Search kurulumu basittir:

1. **Maven ile kurun** veya sağlanan bağlantılardan doğrudan indirin.  
2. **Lisans edinin:** Ücretsiz deneme ile başlayabilir veya [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret ederek geçici bir lisans alabilirsiniz.  
3. **Kütüphaneyi başlatın:** Aşağıdaki kod parçacığı, GroupDocs.Search kullanmaya başlamak için gereken minimum kodu gösterir.

```java
import com.groupdocs.search.*;

public class SetupExample {
    public static void main(String[] args) {
        // Define the directory for storing index files.
        String indexFolder = "path/to/index/directory";
        
        // Initialize an Index instance.
        Index index = new Index(indexFolder);
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Uygulama rehberi

Ortam hazır olduğuna göre, **java full text search indeksi oluşturmak** ve homofonları yönetmek için ihtiyaç duyacağınız temel özellikleri inceleyelim.

### Bir indeks oluşturma ve yönetme
#### Genel Bakış
Arama indeksi oluşturmak, belgeleri etkili bir şekilde yönetmenin ilk adımıdır. Bu, belge içeriğinize dayalı bilgilerin hızlıca alınmasını sağlar.

#### İndeks oluşturma adımları
**Adım 1:** İndeks dosyalarınız için dizini belirtin.

```java
String indexFolder = "YOUR_INDEX_DIRECTORY";
Index index = new Index(indexFolder);
```

*`Index` sınıfı, her belge için tokenleştirilmiş terimleri ve meta verileri tutan aranabilir bir kapsayıcıyı temsil eder; bu, hızlı sorgu yürütmesini ve tüm indeks boyunca belge bilgilerinin verimli depolanmasını sağlayan temel yapıyı sunar.*

**Adım 2:** Belirtilen klasörden belgeleri bu indekse ekleyin.

```java
String documentsFolder = "YOUR_DOCUMENTS_SOURCE_DIRECTORY";
index.add(documentsFolder);
System.out.println("Documents added to the index.");
```

*`index.add()` çağrısı her dosyayı alır, metni çıkarır ve hızlı sorgular için gerekli iç yapıları doldurur; böylece her belge tam olarak indekslenir ve ayrı bir işleme adımı gerektirmeden hemen aranabilir hâle gelir.*

### İndekse belge ekleme
Daha sonra `index.add()`'ı yeni bir klasör yolu veya tek tek dosya yolları ile tekrar çağırarak programlı bir şekilde daha fazla dosya ekleyebilirsiniz. Bu artımlı yaklaşım, indeksi tam bir yeniden oluşturma yapmadan güncel tutar. Bu şekilde belge eklemek, en son içerik değişikliklerini yansıtan canlı bir indeks sürdürmenizi sağlar, son kullanıcılar için sürekli arama kullanılabilirliğini destekler ve toplu yeniden indeksleme işlemleriyle ilişkili kesinti süresini azaltır.

### Bir kelime için homofonları alma
Belirli bir terim için homofonları almak, arama motorunun aynı sesli alternatif yazımları dikkate almasını sağlar, kullanıcıların hatalı yazması veya farklı varyantlar kullanması durumunda hatırlamayı artırır. Sorguyu fonetik eşdeğerlerle genişleterek, motor homofonik formlardan herhangi birini içeren belgeleri eşleştirebilir ve daha kapsamlı sonuçlar sunar.

*`HomophoneDictionary` sınıfı aynı telaffuza sahip kelime gruplarını saklar; bu, arama motorunun fonetik alternatiflerle sorguları genişletirken başvurduğu merkezi bir depodur ve böylece arama sonuçlarının alaka düzeyini artırır.*

```java
String[] homophones = index.getDictionaries().getHomophoneDictionary().getHomophones("braid");
```

### Homofon gruplarını alma
Homofonları gruplamak, birden fazla anlamı olan kelimeleri yönetmek için yapılandırılmış bir yol sunar; geliştiricilerin tek bir işlemde tüm fonetik eşdeğer setlerini almasına olanak tanır. Bu, analiz, özel sözlük yönetimi veya homofon listesinin toplu güncellemeleri için yararlı olabilir.

*`getGroups()` tarafından döndürülen her grup, fonetik aramalarda değiştirilebilir kelimeler içerir ve yöntem bu grupların kapsamlı bir koleksiyonunu sunar; böylece sözlükte tutulan homofon ilişkilerinin tam setini inceleyebilir, değiştirebilir veya dışa aktarabilirsiniz.*

```java
String[][] groups = index.getDictionaries().getHomophoneDictionary().getHomophoneGroups("braid");
```

### Homofon sözlüğünü temizleme
Eski veya gereksiz girişleri temizlemek, sözlüğünüzün ilgili kalmasını ve arama sonuçlarına gürültü eklememesini sağlar. Bu işlem genellikle yeni bir özel set yüklemeden önce sözlüğü varsayılan durumuna sıfırlamanız gerektiğinde yapılır.

*`clear()` yöntemi tüm özel girişleri kaldırır, varsayılan sete geri döner ve daha önce eklenen homofon gruplarının tamamen silindiğini garanti eder; böylece sonraki sözlük yapılandırması için temiz bir başlangıç sağlar.*

```java
if (index.getDictionaries().getHomophoneDictionary().getCount() > 0) {
    index.getDictionaries().getHomophoneDictionary().clear();
}
System.out.println("Homophone dictionary cleared.");
```

### Sözlüğe homofon ekleme
Homofon sözlüğünüzü özelleştirmek, alan‑spesifik terminoloji, argo veya marka adlarını yansıtan özel arama yetenekleri sağlar. Yeni gruplar ekleyerek, aramaların uygulamanıza özgü fonetik ilişkileri tanımasını sağlayabilirsiniz.

*`addGroup()` kullanarak eş sesli kelimeler listesini ekleyin; bu, alan‑spesifik terminoloji için hatırlamayı artırır ve yöntem, yinelenenleri önlemek için her girişi doğrular ve yeni grubu mevcut sözlük yapısına sorunsuz bir şekilde entegre eder.*

```java
String[][] homophoneGroups = {
    new String[] { "awe", "oar", "or", "ore" },
    new String[] { "aye", "eye", "i" },
    new String[] { "call", "caul" }
};
index.getDictionaries().getHomophoneDictionary().addRange(homophoneGroups);
System.out.println("Homophones added to the dictionary.");
```

### Homofon sözlüklerini dışa ve içe aktarma
Sözlükleri dışa ve içe aktarmak, yedekleme veya taşıma amaçları için faydalı olabilir; özel yapılandırmaları ortamlar arasında korumanızı veya ekip üyeleriyle paylaşmanızı sağlar. Bu işlevsellik, kolay okunabilirlik ve diğer araçlarla entegrasyon için JSON formatını destekler.

*Bu yöntemler, özel sözlükleri kolay yeniden kullanım için JSON dosyaları olarak kalıcı hale getirmenizi sağlar; dışa aktarma süreci sözlüğün tam durumunu yakalar, içe aktarma rutini ise JSON yapısını doğruladıktan sonra aktif sözlük örneğine uygular.*

```java
String fileName = "path/to/exported/dictionary.file";
index.getDictionaries().getHomophoneDictionary().exportDictionary(fileName);
```

**Adım 2:** Gerekirse bir dosyadan yeniden içe aktar.

```java
index.getDictionaries().getHomophoneDictionary().importDictionary(fileName);
System.out.println("Homophone dictionary imported successfully.");
```

*İçe aktarma işlemi JSON dosyasını okur, her homofon grubunu yeniden oluşturur ve mevcut sözlüğe birleştirir; böylece tüm özel girişlerin doğru bir şekilde geri yüklendiği ve arama sorgularında hemen kullanılmaya hazır olduğu garantilenir.*

### Homofonları kullanarak arama
Homofon aramayı, kapsamlı belge geri getirme için kullanın; kullanıcıların aynı sesi veren farklı yazımları kullansalar bile ilgili içeriği bulmalarını sağlar. Bu özellik, çok dilli veya fonetik‑ağır alanlarda kullanıcı deneyimini büyük ölçüde iyileştirebilir.

*`setUseHomophoneSearch(true)` ayarı, motorun sorguyu yürütmeden önce fonetik eşdeğerlerle genişletmesini sağlar ve bu seçenek, bulanık eşleşme gibi diğer arama ayarlarıyla birlikte çalışarak geniş bir ilgili sonuç yelpazesini yakalayan sağlam, esnek bir arama deneyimi sunar.*

```java
String query = "caul";
SearchOptions options = new SearchOptions();
options.setUseHomophoneSearch(true);
SearchResult result = index.search(query, options);

System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Pratik uygulamalar

Bu özelliklerin nasıl uygulanacağını anlamak, bir dizi pratik uygulamanın kapılarını açar:

1. **Hukuki belge yönetimi:** “lease” vs. “least” gibi benzer‑sesli hukuki terimleri ayırt edin.  
2. **Eğitim içeriği oluşturma:** Öğretim materyallerinin öğrenenleri şaşırtabilecek belirsiz ifadelerden arındırılmış olmasını sağlayın.  
3. **Müşteri destek sistemleri:** Bilgi tabanı arama doğruluğunu artırın, ajanların doğru makaleleri daha hızlı bulmasına yardımcı olun.

## Performans değerlendirmeleri

**java full text search** performansını korumak için:

- **İndeksi düzenli olarak güncelleyin** belge değişikliklerini yansıtmak için.  
- **Bellek kullanımını izleyin** ve büyük veri setleri için Java yığın ayarlarını ayarlayın.  
- **Kullanılmayan kaynakları hemen kapatın** (ör. işiniz bittiğinde `index.close()` çağırın).

## Sonuç

Şimdiye kadar GroupDocs.Search ile **belgeleri nasıl indeksleyeceğinizi**, homofonları yönetmeyi ve arama deneyiminizi ince ayar yapmayı sağlam bir şekilde kavramış olmalısınız. Bu araçlar, kesin sonuçlar sunmak ve genel belge yönetimi verimliliğini artırmak için çok değerlidir.

## Sıkça Sorulan Sorular

**S:** Homofon sözlüğünü İngilizce dışı dillerde kullanabilir miyim?  
**C:** Evet, uygun kelime gruplarını sağladığınız sürece sözlüğü herhangi bir dilde doldurabilirsiniz.

**S:** Geliştirme testleri için lisans gerekli mi?  
**C:** Geliştirme ve test için ücretsiz deneme lisansı yeterlidir; üretim dağıtımları için ücretli lisans gerekir.

**S:** İndeksim ne kadar büyük olabilir?  
**C:** İndeks boyutu yalnızca donanım kaynaklarınızla sınırlıdır; optimum performans için yeterli disk alanı ve bellek ayırın.

**S:** Homofon aramayı bulanık eşleşme ile birleştirmek mümkün mü?  
**C:** Kesinlikle. `SearchOptions` içinde hem `setUseHomophoneSearch(true)` hem de `setFuzzySearch(true)`'ı etkinleştirerek her iki özelliğin de avantajlarından yararlanabilirsiniz.

**S:** Yinelenen homofon grupları eklersem ne olur?  
**C:** Yinelenen girişler göz ardı edilir; sözlük benzersiz bir kelime grubu seti tutar.

---

**Son Güncelleme:** 2026-09-21  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [java tam metin arama nasıl uygulanır: GroupDocs.Search ile indeks dizini oluşturma](/search/java/indexing/groupdocs-search-java-create-index/)
- [GroupDocs.Search kullanarak Java'da Metadata Indexing ile indeks'e belge ekleme](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Java Tam Metin Arama Kütüphanesi – GroupDocs.Search ile İndeksi Optimize Et](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)