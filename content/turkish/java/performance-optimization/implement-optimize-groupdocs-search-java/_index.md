---
date: '2026-07-07'
description: GroupDocs.Search for Java kullanarak dizini nasıl sileceğinizi, Java’da
  tam metin araması yapmayı ve arama performansını nasıl optimize edeceğinizi öğrenin.
  Ağ kurulumu ve indeksleme ile adım adım rehber.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: GroupDocs.Search kullanarak dizini silme ve Java’da tam metin araması
  yapma. Arama ağı kurmak, aranabilir bir indeks oluşturmak ve arama performansını
  optimize etmek için bu rehberi izleyin.
og_title: GroupDocs.Search for Java ile Dizini Silme ve Tam Metin Araması Yapma
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: GroupDocs.Search for Java ile Dizini Silme ve Tam Metin Araması Yapma
type: docs
url: /tr/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# GroupDocs.Search for Java ile Dizini Silme ve Metin Araması Yapma

Günümüzün veri odaklı dünyasında, **dizini silme** işlemini hızlı bir şekilde yaparken aynı zamanda ışık hızında tam metin arama Java yeteneklerini sunmak rekabet avantajıdır. İster dahili bir bilgi tabanı, ister bir hukuk davası deposu, ister bir e-ticaret ürün kataloğu oluşturuyor olun, iyi ayarlanmış bir arama ağı kullanıcı memnuniyetini büyük ölçüde artırabilir. Bu rehberde, gerektiğinde **bir arama ağı kurma**, **arama yapılabilir bir dizin oluşturma**, **arama performansını optimize etme** ve **dizinden belgeleri silme** konularını öğreneceksiniz — tümü GroupDocs.Search for Java kullanılarak.

## Hızlı Yanıtlar
- **GroupDocs.Search for Java'nın temel amacı nedir?** 50+ belge formatı üzerinde tam metin arama sağlar, hızlı anahtar kelime getirmeyi mümkün kılar.  
- **Dağıtık bir ortamda metin aramasını nasıl gerçekleştiririm?** Bir arama ağı dağıtın, belgeleri bir ana düğümde indeksleyin, ardından herhangi bir düğümde sorgu yapın.  
- **İndeksi yeniden oluşturmak zorunda kalmadan belgeleri silebilir miyim?** Evet, seçilen dosyaları kaldırmak için Delete API'sini kullanın, böylece *dizini silme* işlemini tam yeniden indekslemeden gerçekleştirebilirsiniz.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya üzeri.  
- **Üretim için lisans gerekli mi?** Geçerli bir GroupDocs.Search lisansı gereklidir; ücretsiz deneme mevcuttur.

## “perform text search” nedir?
Metin araması yapmak, belirtilen anahtar kelimeleri veya ifadeleri içeren belgeleri getirmek için tam metin indeksine sorgu göndermek anlamına gelir. GroupDocs.Search, binlerce dosya arasında bile bu aramaları son derece hızlı yapan ters bir indeks oluşturur.

## Neden bir arama ağı kurmalısınız?
Bir arama ağı, indeksleme ve sorgu iş yüklerini birden fazla düğüm arasında dağıtarak **arama performansını optimize etmenizi**, yatay ölçeklendirme yapmanızı ve yüksek kullanılabilirliği sürdürmenizi sağlar. Bu mimari, gecikme ve veri aktarım hızının önemli olduğu kurumsal düzeyde belge depoları için idealdir.

## GroupDocs.Search for Java ile Bir Arama Ağı Nasıl Uygulanır ve Optimize Edilir
Yapılandırmanızı yükleyin, bir ana düğüm başlatın ve aynı temel yol ve bağlantı noktasını paylaşan işçi düğümler ekleyin. Ağı bu şekilde dağıtmak, belge sayısı yüz binlere çıktıkça bile herhangi bir düğümün indeksleme veya sorgu isteklerini işlemesine ve tutarlı yanıt süreleri sunmasına olanak tanır.

### Adım adım genel bakış
1. **Paylaşılan bir dizin ve bir TCP bağlantı noktasını içeren temel bir yapılandırma tanımlayın.**  
2. **İndeksi yönetmek ve işçi düğümleri koordine etmek için ana düğümü başlatın.**  
3. **Ana düğüme bağlanan işçi düğümler ekleyin, paralel indeksleme ve aramayı etkinleştirin.**  
4. **Kaynak kullanımını izleyin** ve gecikmeyi düşük tutmak için JVM yığın ayarlarını ayarlayın.

## GroupDocs.Search for Java'da Dizini Silme
`SearchNode`, indeksleme ve sorgu işlemlerini yöneten GroupDocs.Search ağındaki bir düğümü temsil eder. `delete` yöntemi, belirtilen belgeleri indeksden kaldırır.

### Doğrudan silme adımları
- `SearchNode` örneği üzerinde `delete` metodunu çağırın.  
- Göreceli dosya yollarından oluşan bir dizi sağlayın.  
- Değişiklikleri onaylayın; indeks anında yenilenir ve sonraki aramalarda kaldırılan dosyalar artık döndürülmez.

## Arama Ağı Nedir?
Bir **arama ağı**, ortak bir indeks deposunu paylaşan birbirine bağlı düğümlerin bir kümesidir ve dağıtık indeksleme ve sorgu yürütmeye olanak tanır. Büyük ölçekli belge koleksiyonları için yatay ölçeklendirme ve hata toleransı sağlar.

## Arama Yapılabilir Bir Dizin Nasıl Oluşturulur (index documents java)
`add` metodu bir belgeyi arama indeksine ekler. Belgeleri `add` yöntemiyle ana düğüme ekleyin; ağ değişiklikleri tüm işçi düğümlere yayar. Bu yaklaşım, ek senkronizasyon adımları olmadan her düğümün en son indeks üzerinden sorgu hizmeti vermesini sağlar.

### Temel eylemler
- Ana düğümü kaynak dosyaları içeren klasöre yönlendirin.  
- İndeksleme rutinini çağırın; ağ her dosyayı işler ve ters indeksi günceller.  
- İndeks dosyalarının belirlenen depolama dizininde göründüğünden emin olun.

## İndekslenmiş Dosyaları Kaldırma (remove indexed files)
Bir belge artık kullanılmaz hale geldiğinde, `delete` API'sini yolu ile birlikte çağırın. Sistem, dosyanın ters indeksteki girişlerini kaldırır, depolamayı boşaltır ve eski sonuçların ortaya çıkmasını önler.

## GroupDocs.Search for Java Kurulumu
Başlamak için, aşağıdaki kurulumla GroupDocs.Search'ı Java projenize entegre edin:

### Maven Kurulumu
`pom.xml` dosyanıza depo ve bağımlılığı ekleyin:

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
Alternatif olarak, [GroupDocs'tan en son sürümü doğrudan indirebilirsiniz](https://releases.groupdocs.com/search/java/).

### Lisans Edinme
GroupDocs ücretsiz bir deneme sunar; bu, özelliklerini satın almadan önce değerlendirmenizi sağlar. Geçici bir lisans almak için [satın alma sayfalarındaki](https://purchase.groupdocs.com/temporary-license/) adımları izleyebilirsiniz. Bu, test aşamanızda tam işlevselliği etkinleştirecektir.

### Temel Başlatma ve Kurulum
Java uygulamanızda GroupDocs.Search'ı aşağıdaki şekilde başlatın:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Uygulama Kılavuzu

### Arama Ağını Yapılandırma
**Genel Bakış:** Arama ağınız için bir temel yol ve bağlantı noktası oluşturun, böylece düğümler etkili bir şekilde iletişim kurabilir.

#### Adım 1: Temel Yapılandırmayı Tanımla
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parametreler:**  
  - `basePath`: Ağ işlemleri için dizin yolu.  
  - `basePort`: Arama ağı tarafından kullanılan bağlantı noktası numarası.

#### Adım 2: Sorun Giderme
Belirttiğiniz bağlantı noktasının güvenlik duvarı ayarları tarafından engellenmediğinden veya başka bir uygulama tarafından kullanılmadığından emin olun. Çakışmaları önlemek için gerektiği gibi ayarlayın.

### Arama Ağı Düğümlerini Dağıtma
**Genel Bakış:** Yapılandırmanızı kullanarak, dağıtık indeksleme ve arama için ağınızda düğümler dağıtın.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Ana Yapılandırma Seçenekleri:**  
  - **Base Path & Port:** Bu değerler, tutarlılığı sağlamak için ilk yapılandırmanızda kullanılanlarla eşleşmelidir.

### Belgeleri İndeksleme (`create searchable index`)
**Genel Bakış:** Bir ana düğüm kullanarak belgeleri arama indeksine verimli bir şekilde ekleyin.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Amaç:**  
  - `masterNode`: Belge indekslemesini yöneten birincil düğüm.  
  - `documentsPath`: Belgeleri içeren dizinin yolu.

#### Sorun Giderme İpuçları
Belge yollarınızın doğru ve erişilebilir olduğundan emin olun. Bu dizinlerden okuma izni verildiğini kontrol edin.

### Ağda Metin Arama (`perform text search`)
**Genel Bakış:** İndekslenmiş ağınızda kapsamlı metin aramaları gerçekleştirin.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parametreler:**  
  - `query`: Aradığınız metin.  
  - `masterNode`: Aramayı gerçekleştiren düğüm.

### İndeksten Belgeleri Silme (`delete documents index`)
**Genel Bakış:** Dosya yollarını kullanarak indeksinizden belirli belgeleri kaldırın.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Metodun Amacı:**  
  - `node`: Silme işlemleri için hedef düğüm.  
  - `filePaths`: İndeksten kaldırılacak belgelerin yolları.

#### Sorun Giderme
Dosya yollarının kesin olduğundan ve dosyaların dizininizde mevcut olduğundan emin olun. Sorun devam ederse, ağ izinlerini ve bağlantıyı kontrol edin.

## Pratik Uygulamalar
1. **Kurumsal Belge Yönetimi:** İç bilgi alımını kolaylaştırın.  
2. **Hukuki Dava Analizi:** Birden fazla depodaki ilgili dava dosyalarını hızlıca bulun.  
3. **E‑ticaret Platformları:** Açıklamaları ve incelemeleri indeksleyerek ürün arama hızını artırın.  
4. **Akademik Araştırma:** Makaleler ve tezlerden oluşan büyük dijital kütüphanelerde verimli arama yapın.  
5. **Müşteri Destek Sistemleri:** Temsilcilerin geçmiş biletleri anında aramasını sağlayarak yanıt süresini azaltın.

## Performans Düşünceleri
- **İndeksleme Hızını Optimize Edin:** Gecikmeyi düşük tutmak için yeni belgeleri düşük yoğunluklu saatlerde artımlı olarak ekleyin.  
- **Kaynak Kullanım Kılavuzları:** Özellikle düğüm sayısını artırırken CPU ve belleği izleyin.  
- **Java Bellek Yönetimi:** İş yükünüze göre JVM yığın ayarlarını ayarlayın (ör. orta‑boyutlu indeksler için `-Xmx2g`).

## Sonuç
Bu kılavuzu izleyerek GroupDocs.Search for Java kullanarak **bir arama ağı kurma**, **arama yapılabilir bir indeks oluşturma**, **metin araması yapma** ve **indeksten belgeleri silme** konularını öğrendiniz. Bu yetenekler, dağıtık ortamlar içinde hızlı ve güvenilir belge getirmeyi sağlar.

**Sonraki Adımlar**
- İş yükünüz için optimal dengeyi bulmak amacıyla farklı düğüm yapılandırmalarıyla deney yapın.  
- Özel analizörler ve alaka düzeyi ayarlamaları gibi gelişmiş indeksleme seçeneklerine daha derinlemesine bakın.  
- Uçtan uca belge işleme için diğer GroupDocs ürünleriyle entegrasyonu keşfedin.

## Sıkça Sorulan Sorular

**S: GroupDocs.Search for Java'nın temel kullanım durumu nedir?**  
C: Birçok belge formatı üzerinde tam metin arama sağlar, büyük depolarda **metin araması yapmanıza** olanak tanır.

**S: Büyük bir ağda arama hızını nasıl artırabilirim?**  
C: Ek düğümler dağıtarak, JVM yığınını ayarlayarak ve indekslemeyi düşük trafik dönemlerinde planlayarak **arama performansını optimize edin**.

**S: Tüm koleksiyonu yeniden indekslemeden tek bir belgeyi silmek mümkün mü?**  
C: Evet, kod örneğinde gösterildiği gibi belirli dosyaları kaldırmak için **delete documents index** API'sini kullanın.

**S: Geliştirme için lisansa ihtiyacım var mı?**  
C: Test için ücretsiz deneme lisansı yeterlidir; üretim dağıtımları için ticari lisans gereklidir.

**S: PDF, Word dosyaları ve e-postaları birlikte indeksleyebilir miyim?**  
C: Kesinlikle—GroupDocs.Search kutudan çıktığı gibi geniş bir format yelpazesini destekler.

---

**Son Güncelleme:** 2026-07-07  
**Test Edilen Sürüm:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [Java'da Metin Nasıl İndekslenir - GroupDocs.Search Kılavuzu](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [GroupDocs.Search for Java'da Gelişmiş İndeksleme Teknikleriyle Arama Performansını Optimize Et](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [GroupDocs.Search Java ile Sorgu Performansını İyileştirin: İndeksi ve Aramayı Optimize Edin](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)