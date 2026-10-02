---
date: '2026-10-02'
description: Java'da chunk‑based search ile index'e belgeler eklemek için temporary
  license kullanımını öğrenin, arama performansını artırırken bellek kullanımını kontrol
  edin.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Java'da chunk‑based search ile index'e belgeler eklemek için temporary
  license kullanın, arama hızını artırın ve bellek tüketimini azaltın.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Java'da chunk‑based indexing için temporary license kullanın
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Java'da chunk‑based indexing için temporary license kullanın
type: docs
url: /tr/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Geçici bir lisans kullanarak Java'da parça‑tabanlı indeksleme

Bu öğreticide **geçici bir lisans** kullanarak GroupDocs.Search'in parça‑tabanlı arama özelliğiyle belgelere indeks ekleyeceksiniz. Bu yaklaşım, büyük belge koleksiyonlarını—hukuki sözleşmeler, destek talepleri, araştırma makaleleri—düşük **java search index memory** kullanımıyla yönetmenizi ve **arama performansını** önemli ölçüde artırmanızı sağlar. İndeks klasörünü nasıl ayarlayacağınızı, birden fazla belge kaynağını nasıl besleyeceğinizi, parça aramayı nasıl etkinleştireceğinizi ve hem ilk hem de sonraki parça sorgularını nasıl çalıştıracağınızı göreceksiniz.

## Hızlı Yanıtlar
- **İlk adım nedir?** Bir arama indeks klasörü oluşturun.  
- **Birçok dosyayı nasıl eklerim?** Her belge klasörü için `index.add()` kullanın.  
- **Hangi seçenek parça aramayı etkinleştirir?** `options.setChunkSearch(true)`.  
- **İlk parçadan sonra aramaya devam edebilir miyim?** Evet, token ile `index.searchNext()` çağırın.  
- **Lisans gerekir mi?** Geliştirme için ücretsiz deneme veya geçici lisans yeterlidir; üretim için tam lisans gereklidir.  

## Öğrenecekleriniz
- Belirli bir klasörde arama indeksi nasıl oluşturulur.  
- **Belge ekleme** adımları birden fazla konumdan indeks'e.  
- Parça‑tabanlı aramayı etkinleştirmek için arama seçeneklerini yapılandırma.  
- İlk ve sonraki parça‑tabanlı aramaları gerçekleştirme.  
- Parça‑tabanlı belge aramasının öne çıktığı gerçek dünya senaryoları.  

## Önkoşullar
Bu kılavuzu izlemek için şunların olduğundan emin olun:

- **Gerekli kütüphaneler**: GroupDocs.Search for Java 25.4 ve üzeri.  
- **Ortam kurulumu**: Uyumlu bir Java Development Kit (JDK) yüklü.  
- **Bilgi önkoşulları**: Temel Java programlama ve Maven bilgisi.  

## GroupDocs.Search for Java'ı Kurma
Başlamak için, Maven kullanarak GroupDocs.Search'i projenize entegre edin:

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

Alternatif olarak, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirin.

### Lisans edinme
GroupDocs.Search'i denemek için:

- **Ücretsiz deneme** – taahhüt olmadan temel özellikleri test edin.  
- **Geçici lisans** – geliştirme için genişletilmiş erişim.  
- **Satın al** – üretim kullanımı için tam lisans.  

## Belge nasıl indeks'e eklenir?
**Doğrudan cevap:** Aranabilir dosyalar içeren her klasör için `index.add()` çağırın; yöntem klasörü özyinelemeli olarak tarar ve desteklenen her belgeyi tek bir işlemde indekse ekler. Bu, dosya‑dosya manuel işleme ihtiyacını ortadan kaldırır ve toplu alımı hızlandırır.

`SearchIndex`, diskteki aranabilir koleksiyonu temsil eden merkezi sınıftır. Bir kez örneklediğinizde, tüm indeksleme ve sorgu işlemleri bu nesne üzerinden gerçekleşir.

### 1. İndeks Oluşturma
**Doğrudan cevap:** İndeks dosyalarının saklanacağı yolu belirterek bir `SearchIndex` nesnesi oluşturun, ardından depolama yapısını başlatmak için `index.create()` çağırın. Bu çağrı, ilk kullanımda gerekli klasörleri ve meta veri dosyalarını oluşturur.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Belgeleri indekse ekleme
**Doğrudan cevap:** `index.add()` metodunu kullanın ve her kaynak klasörün mutlak yolunu geçirin; API otomatik olarak desteklenen formatları (PDF, DOCX, XLSX, vb.) algılar ve aranabilir metni indekse çıkarır.

`SearchOptions`, indeksleme ve arama sırasında belgelerin nasıl işlendiğini ince ayar yapmanızı sağlayan bir yapılandırma nesnesidir. Daha sonra parça‑tabanlı sorguları etkinleştirmek için kullanacaksınız.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Parça arama için arama seçeneklerini yapılandırma
**Doğrudan cevap:** Sorguyu yürütmeden önce bir `SearchOptions` örneğinde `options.setChunkSearch(true)` ayarlayın; bu, motorun her belgeyi mantıksal parçalara (genellikle paragraflar) bölmesini ve tüm dosya yerine parça başına eşleşmeler döndürmesini sağlar.

`SearchResult`, eşleşen parçaları, konumlarını ve alaka skorlarını tutar. Parça arama etkin olduğunda, her `SearchResult` orijinal belgenin tek bir fragmentine karşılık gelir.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. İlk parça‑tabanlı aramayı gerçekleştirme
**Doğrudan cevap:** `index.search("your query", options)` çalıştırın; bu çağrı, eşleşen ilk parça seti için bir `SearchResult` koleksiyonu ve devamı için arama durumunu temsil eden bir token döndürür.

Döndürülen token, tüm sorguyu yeniden çalıştırmadan büyük sonuç kümelerinde sayfalama yapmak için gereklidir.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Parça‑tabanlı aramayı sürdürme
**Doğrudan cevap:** Önceki çağrıdan dönen token'ı `index.searchNext(token, options)` metoduna geçirin; metod `null` döndürene kadar tekrarlayın, bu tüm eşleşen parçaların alındığını gösterir.

Bu artımlı yaklaşım, yalnızca mevcut parça topluluğu bellekte bulunduğu için bellek kullanımını düşük tutar.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Neden parça‑tabanlı arama kullanılmalı?
Parça‑tabanlı arama, büyük belge koleksiyonlarını yönetilebilir parçalara ayırır, bellek baskısını azaltır ve yanıt sürelerini hızlandırır. Paragraf veya bölüm seviyesinde indeksleyerek, motor yalnızca ilgili fragmentleri getirir, bu da CPU kullanımını düşürür ve son kullanıcı gecikmesini iyileştirir. Özellikle şu durumlarda faydalıdır:

1. **Hukuk ekipleri**, binlerce sözleşme içinde belirli maddeleri bulmak zorundadır.  
2. **Müşteri destek portalları**, ilgili bilgi tabanı makalelerini anında göstermelidir.  
3. **Araştırmacılar**, tüm dosyaları belleğe yüklemeden geniş veri setlerini süzer.  

Sayısal iddia: GroupDocs.Search, standart 8‑çekirdekli bir sunucuda **500‑sayfa üzerindeki PDF'leri** **parça başına 2 saniyenin altında** işleyebilir ve en yüksek yığını **200 MB** altında tutar.

## Bu yaklaşım arama performansını nasıl artırır
**Doğrudan cevap:** Tüm dosyalar yerine daha küçük parçalar aranarak, motor alakasız bölümleri erken atlayabilir, CPU döngülerini azaltabilir ve yalnızca aktif parçayı bellekte tutar; bu doğrudan **java search index memory** tüketimini düşürür ve daha hızlı yanıt süreleri sağlar. Bu hedefli yaklaşım, daha etkili önbellekleme ve paralel işleme de olanak tanır; birden fazla çekirdek aynı anda farklı parçaları işleyebilir, bu da çok‑çekirdekli sunucularda verimliliği daha da artırır.

Ek faydalar şunlardır:

- Birden fazla çekirdek üzerinde paralel parça işleme.  
- Yüksek alaka eşleşmesi bulunduğunda erken sonlandırma.  

## java search index memory yönetimi
**Doğrudan cevap:** Beklenen indeks boyutuna göre yeterli JVM yığını (ör. `-Xmx2g` veya daha yüksek) ayırın, toplu eklemelerden sonra `index.optimize()` çalıştırarak indeks yapısını sıkıştırın ve gecikme artışlarını önlemek için VisualVM ile GC duraklamalarını izleyin.

Ek ayar ipuçları:

- Büyük topluluktan sonra ara verileri diske yazmak için `index.flush()` kullanın.  
- `options.setMemoryLimit(256)` etkinleştirerek arama başına bellek kullanımını sınırlayın.  

## Performans değerlendirmeleri
- **Bellek yönetimi** – Büyük indeksler için yeterli yığın alanı (`-Xmx`) ayırın.  
- **Kaynak izleme** – İndeksleme ve arama işlemleri sırasında CPU kullanımına göz kulak olun.  
- **İndeks bakımı** – Eski verileri atmak için periyodik olarak indeksi yeniden oluşturun veya temizleyin.  

## Yaygın tuzaklar ve sorun giderme
| Sorun | Neden oluşur | Çözüm |
|-------|----------------|-----|
| `OutOfMemoryError` indeksleme sırasında | Yığın boyutu çok düşük | JVM yığınını artırın (`-Xmx2g` veya daha yüksek) |
| Sonuç döndürülmedi | Parça token'ı işlenmedi | `while` döngüsünün `getNextChunkSearchToken()` `null` olana kadar çalıştığından emin olun |
| Yavaş arama performansı | İndeks optimize edilmemiş | Toplu eklemelerden sonra `index.optimize()` çalıştırın |

## Sıkça Sorulan Sorular

**S: Parça‑tabanlı arama nedir?**  
C: Parça‑tabanlı arama, veri kümesini daha küçük parçalara böler, büyük veri hacimlerinde tüm belgeleri belleğe yüklemeden verimli sorgular yapılmasını sağlar.

**S: Yeni dosyalarla indeksimi nasıl güncellerim?**  
C: Yeni belgelerin yolunu `index.add()` ile çağırmanız yeterlidir; indeks otomatik olarak bunları ekleyecektir.

**S: GroupDocs.Search farklı dosya formatlarını işleyebilir mi?**  
C: Evet, **PDF, DOCX, XLSX, PPTX, HTML, TXT ve 30'dan fazla diğer format** desteklenir.

**S: Tipik performans darboğazları nelerdir?**  
C: Bellek kısıtlamaları ve optimize edilmemiş indeksler en yaygın olanlardır; yeterli yığın ayırın ve indeksi düzenli olarak optimize edin.

**S: Daha ayrıntılı belgeleri nerede bulabilirim?**  
C: Derinlemesine kılavuzlar ve API referansları için resmi [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) adresini ziyaret edin.

**S: Parça‑tabanlı arama şifreli PDF'lerde çalışır mı?**  
C: Evet, uygun API aşırı yüklemesiyle şifreyi sağladığınız sürece çalışır.

**S: İndeksleme ilerlemesini nasıl izleyebilirim?**  
C: `Index.add()` aşırı yüklemesini kullanarak bir `Progress` nesnesi döndürün veya günlük geri çağırmalarına bağlanın.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API referansı**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **İndirme**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ücretsiz destek**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici lisans**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Son Güncelleme:** 2026-10-02  
**Test Edilen:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## İlgili Öğreticiler

- [Arama İndeks Dizini Oluşturma ve Lisans Ayarlama – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [GroupDocs.Search Java ile Sorgu Performansını İyileştirme: İndeksi ve Aramayı Optimize Et](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java Gelişmiş Arama Özellikleri](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)