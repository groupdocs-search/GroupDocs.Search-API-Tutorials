---
date: '2026-11-02'
description: Java'da GroupDocs.Search ile klasörü indekse eklemeyi öğrenin, yüksek
  sıkıştırmayı yapılandırın ve hızlı tam metin sorgularını çalıştırın.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Java'da GroupDocs.Search ile klasörü indekse eklemeyi öğrenin, sıkıştırmayı
  yapılandırın ve hızlı tam metin aramaları gerçekleştirin. Büyük belge setleri için
  idealdir.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Java'da GroupDocs.Search ile klasörü indekse ekleme
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: Java'da GroupDocs.Search ile klasörü indekse ekleme
type: docs
url: /tr/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# GroupDocs.Search ile Java'da klasörü indekse ekleme

Eğer milyonlarca belgeye ölçeklenebilen **java full text search**'e ihtiyacınız varsa, doğru yerdesiniz. Bu öğreticide GroupDocs.Search kullanarak **add folder to index**'i nasıl yapacağınızı, yüksek sıkıştırmalı depolamayı yapılandırmayı ve ışık hızında sorgular çalıştırmayı öğreneceksiniz. Sonunda, herhangi bir Java projesine ekleyebileceğiniz üretim‑hazır bir çözümünüz olacak.

## Hızlı cevaplar
- **Birincil kütüphane nedir?** GroupDocs.Search for Java  
- **Klasörü indekse nasıl eklenir?** Use `index.add(folderPath)`  
- **Metin sıkıştırmasını yapılandırabilir miyim?** Yes, via `TextStorageSettings(Compression.High)`  
- **Hangi Java sürümü gereklidir?** JDK 8 or higher  
- **Deneme lisansını nereden alabilirim?** From the GroupDocs website or the repository page  

## java full text search nedir ve neden önemlidir?
Java full text search, ham belgeleri ters bir indeks haline getirir ve binlerce dosya arasında herhangi bir terimin alt saniyede bulunmasını sağlar. Bu yetenek, kullanıcıların anında sonuç beklediği yasal depolar, araştırma kütüphaneleri ve kurumsal bilgi tabanları için hayati öneme sahiptir. Ayrıca modern uygulamalarda verimliliği artırır.

## Neden groupdocs.search'i java full text search için kullanmalısınız?
GroupDocs.Search, yüksek verimli indeksleme ve sorgu yürütmesi sağlar ve yerleşik yüksek sıkıştırma sunar. **50+ input and output formats**'i destekler—PDF, DOCX, EML ve HTML dahil—ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri işleyebilir, tipik iş yükleri için bellek ayak izini 200 MB'nin altında tutar.

## Önkoşullar
- **GroupDocs.Search for Java** (version 25.4 or later) – indeksleme ve aramayı sağlayan çekirdek kütüphane.  
- **JDK 8+** installed and configured – SDK için gereken minimum çalışma zamanı.  
- **Maven** for dependency management – kütüphaneyi projenize eklemeyi basitleştirir.  
- An IDE such as **IntelliJ IDEA** or **Eclipse** – Java kodu yazmak ve hata ayıklamak için.  

## GroupDocs.Search'i java için kurma

### Maven kurulumu
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

### Doğrudan indirme
Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

#### Lisans edinme
- **Free trial** – taahhüt olmadan tüm özellikleri keşfedin.  
- **Temporary license** – uzatılmış test süresi.  
- **Purchase** – tam üretim yeteneklerini açın.  

### Temel başlatma ve kurulum
`Index`, bir arama indeksini oluşturmak, açmak ve yönetmek için kullanılan çekirdek sınıftır.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Özel sıkıştırma ile metin indeksleme

### Adım 1: indeks klasörünü tanımlayın
İndeks dosyalarının bulunacağı bir dizin seçin:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Adım 2: indeks ayarlarını yapılandırın
`TextStorageSettings`, metnin indeks içinde nasıl saklanacağını, sıkıştırma seviyesini de içerecek şekilde yapılandırır. `Compression`, istenen sıkıştırma algoritmasını belirten bir enum'dur.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Adım 3: özel ayarlarla indeksi oluşturun
Yukarıda tanımlanan yapılandırmayı kullanarak indeksi örnekleyin:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Klasörü indekse nasıl eklenir
`Index`, aranabilir indeksi temsil eden ana sınıftır.

Mevcut indeksi (veya yeni bir tane oluşturun) yükleyin ve ardından `Index` nesnesi üzerinde `add` metodunu çağırın. `add` işlemi verilen dizini tarar, her desteklenen dosyadan metni çıkarır ve sıkıştırılmış indekse kaydeder, anında arama için hazır.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## İndekslenmiş belgelerde nasıl arama yapılır
`SearchResult`, belge yolu ve alaka düzeyi ile tek bir eşleşmeyi temsil eder.

Aramak istediğiniz terim veya ifadeyi temsil eden bir sorgu dizesi tanımlayın, ardından `Index` örneği üzerinde `search` metodunu çağırın. Metod, her biri belge yolunu, alaka puanını ve eşleşmeyi vurgulayan bir snippet'i içeren `SearchResult` nesnelerinin bir koleksiyonunu döndürür.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Pratik uygulamalar
**java full text search**'in parladığı gerçek dünya senaryoları:

1. **Legal document management** – dava dosyalarının anında alınması.  
2. **Academic research libraries** – makaleler ve tezlerin hızlı bulunması.  
3. **Enterprise knowledge bases** – kılavuzlar ve SSS'lere hızlı erişim.  
4. **Content management systems** – büyük siteler için verimli içerik keşfi.  
5. **Customer service archives** – geçmiş bilet ve sohbetlerin hızlı aranması.  

## Performans değerlendirmeleri
- **Compression vs. speed**: Yüksek sıkıştırma, disk alanının %70'ine kadar tasarruf sağlar ancak hafif bir indeksleme ek yükü ekler; veri hacminiz için benchmark testleri çalıştırın.  
- **Memory management**: 10 GB'den büyük indeksler için en az 2 GB yığın ayırın, `OutOfMemoryError`'ı önlemek için.  
- **Index updates**: Yeni belgeleri `index.add()` ile artımlı olarak ekleyin ve indeksi sıkı tutmak için periyodik olarak `index.optimize()` çağırın.  
- **Query optimization**: Sonuçları daraltmak ve yanıt süresini azaltmak için gelişmiş sorgu sözdizimini (joker karakterler, yakınlık, bulanık arama) kullanın.  

## Yaygın tuzaklar ve uzman ipuçları
- **Pitfall:** Toplu eklemelerden sonra `index.optimize()` çağırmayı unutmak.  
  **Pro tip:** İndeksi sıkı tutmak için `index.optimize()`'ı her gece çalıştırın.  

- **Pitfall:** Büyük veri setlerinde varsayılan (düşük) sıkıştırmayı kullanmak.  
  **Pro tip:** Üretim ortamları için depolama maliyetlerini azaltmak amacıyla `Compression.High`'a geçin.  

- **Pitfall:** Ağ paylaşımından dosya eklerken `IOException`'ı ele almamak.  
  **Pro tip:** `index.add()`'ı try‑catch bloğuna sarın ve sonraki inceleme için hataları kaydedin.  

## Sıkça sorulan sorular

**Q: GroupDocs.Search nedir?**  
A: İndeksleme, sıkıştırma ve karmaşık sorgu desteği dahil olmak üzere gelişmiş tam metin arama yetenekleri sağlayan sağlam bir Java kütüphanesidir.

**Q: GroupDocs.Search ile büyük veri setlerini nasıl yönetirim?**  
A: Yüksek sıkıştırmayı (`Compression.High`) etkinleştirin ve indeksi ince tutmak için değişiklikleri periyodik olarak commit edin. Ayrıca yeterli yığın belleği ayırın (örneğin, 20 GB'den büyük indeksler için 4 GB).

**Q: GroupDocs.Search'ı mevcut kurumsal sistemlerle entegre edebilir miyim?**  
A: Evet, kütüphane herhangi bir Java tabanlı backend, REST hizmeti veya mikro hizmet mimarisine gömülebilir.

**Q: İndeksim güncel olmadığında ne yapmalıyım?**  
A: Yeni dosyaları eklemek için `index.add()` metodunu, eski dosyaları silmek için `index.delete()` metodunu kullanın ve gerekirse `index.optimize()`'ı yeniden çalıştırın.

**Q: Yardım veya destek nereden alınabilir?**  
A: Sorun giderme ve en iyi uygulama ipuçları için [GroupDocs forums](https://forum.groupdocs.com/c/search/10) topluluk forumunu ziyaret edin.

## Ek kaynaklar
- Ayrıntılı kullanım kılavuzu: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Tam API referansı: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Yeni özelliklerle güncel kalın: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Son Güncelleme:** 2026-11-02  
**Test Edilen Versiyon:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## İlgili Öğreticiler
- [Groupdocs Search Java İndeks Oluşturma Kılavuzu](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Groupdocs Search Java İndeks Yönetimi Kılavuzunu Ustalıkla Kullanma](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java Full Text Search Kütüphanesi – GroupDocs.Search ile İndeksi Optimize Etme](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)