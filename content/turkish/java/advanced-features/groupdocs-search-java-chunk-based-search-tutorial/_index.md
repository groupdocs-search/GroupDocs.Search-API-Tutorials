---
date: '2026-02-21'
description: GroupDocs.Search kullanarak Java'da chunk‑tabanlı arama ile belgelere
  indeks eklemeyi ve arama performansını artırmayı öğrenin; büyük belge setleri için
  Java arama indeksi belleğini optimize edin.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Java'da parça tabanlı arama ile belgeleri indekse ekle
type: docs
url: /tr/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Java'da parça‑tabanlı arama ile belgeleri indekse ekleme

Modern uygulamalarda **add documents to index** hızlı bir şekilde yapılmalı ve ardından hızlı, parça‑tabanlı sorgular çalıştırılmalıdır; belleği aşırı tüketmeden ölçeklenebilen bir çözüm istersiniz. Bu öğretici, GroupDocs.Search for Java'yı kurmanızı, birden fazla belge klasörünü eklemenizi ve motoru **increase search performance** sağlarken **java search index memory** kullanımını kontrol altında tutmanızı gösterir. Hukuki sözleşmeler, destek biletleri veya araştırma makaleleri gibi belgeleri indekslerken, aşağıdaki adımlar üretim‑hazır bir uygulama sunar.

## Hızlı Yanıtlar
- **İlk adım nedir?** Create a search index folder.  
- **Birçok dosyayı nasıl eklerim?** Use `index.add()` for each document folder.  
- **Hangi seçenek parça aramayı etkinleştirir?** `options.setChunkSearch(true)`.  
- **İlk parçadan sonra aramaya devam edebilir miyim?** Yes, call `index.searchNext()` with the token.  
- **Bir lisansa ihtiyacım var mı?** A free trial or temporary license works for development; a full license is required for production.  

## Öğrenecekleriniz
- Belirli bir klasörde arama indeksi nasıl oluşturulur.  
- Birden fazla konumdan **add documents to index** adımları.  
- Parça‑tabanlı aramayı etkinleştirmek için arama seçeneklerini yapılandırma.  
- İlk ve sonraki parça‑tabanlı aramaları gerçekleştirme.  
- Parça‑tabanlı belge aramasının öne çıktığı gerçek dünya senaryoları.  

## Önkoşullar
- **Gerekli Kütüphaneler**: GroupDocs.Search for Java 25.4 or later.  
- **Ortam Kurulumu**: Uyumlu bir Java Development Kit (JDK) yüklü.  
- **Bilgi Önkoşulları**: Temel Java programlama ve Maven bilgisi.  

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

### Lisans Edinme
GroupDocs.Search'i denemek için:

- **Free Trial** – taahhüt olmadan temel özellikleri test edin.  
- **Temporary License** – geliştirme için genişletilmiş erişim.  
- **Purchase** – üretim kullanımı için tam lisans.  

### Temel Başlatma ve Kurulum
Aranabilir verilerin bulunmasını istediğiniz klasörde bir indeks oluşturun:

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

## Belgeleri indekse nasıl eklenir
İndeks mevcut olduğuna göre, bir sonraki mantıklı adım, dosyalarınızın bulunduğu konumlardan **add documents to index** yapmaktır.

### 1. İndeks Oluşturma
**Genel Bakış**: Arama indeksi için bir dizin ayarlayın.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Belgeleri İndekse Eklemek
**Genel Bakış**: Birkaç kaynak klasörden dosyaları alın.

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

### 3. Parça Arama için Arama Seçeneklerini Yapılandırma
Seçenekler nesnesini ayarlayarak parça‑tabanlı aramayı etkinleştirin.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. İlk Parça‑Tabanlı Aramayı Gerçekleştirme
Parça‑etkin seçenekleri kullanarak ilk sorguyu çalıştırın.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Parça‑Tabanlı Aramaya Devam Etme
Arama tamamlanana kadar kalan parçalar üzerinde yineleme yapın.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Neden parça‑tabanlı arama kullanılır?
Parça‑tabanlı arama, büyük belge koleksiyonlarını yönetilebilir parçalara ayırarak bellek baskısını azaltır ve yanıt sürelerini hızlandırır. Özellikle şu durumlarda faydalıdır:

1. **Legal teams** binlerce sözleşme içinde belirli maddeleri bulmak zorundadır.  
2. **Customer support portals** ilgili bilgi tabanı makalelerini anında göstermek zorundadır.  
3. **Researchers** tüm dosyaları belleğe yüklemeden geniş veri setlerini tarar.  

## Bu yaklaşım **increases search performance** nasıl artırır
Tam dosyalar yerine daha küçük parçalar arandığında, motor şunları yapabilir:

- Alakasız bölümleri erken atlayarak CPU döngülerini azaltır.  
- Bellekte yalnızca aktif parçayı tutar, bu da **java search index memory** tüketimini doğrudan düşürür.  
- Çok çekirdekli makinelerde parça işleme paralelleştirerek daha hızlı sonuçlar elde eder.

## **java search index memory** yönetimi
Parça‑tabanlı arama zaten bellek ayak izini azaltırken, JVM'i daha da ayarlayabilirsiniz:

- İndeks boyutuna göre yeterli yığın ayırın (`-Xmx2g` veya daha yüksek).  
- Toplu eklemelerden sonra indeks yapısını sıkıştırmak için `index.optimize()` kullanın.  
- Gecikme artışlarını önlemek için VisualVM gibi araçlarla GC duraklamalarını izleyin.

## Performans Düşünceleri
- **Memory Management** – Büyük indeksler için yeterli yığın alanı (`-Xmx`) ayırın.  
- **Resource Monitoring** – İndeksleme ve arama işlemleri sırasında CPU kullanımını izleyin.  
- **Index Maintenance** – Eski verileri temizlemek için periyodik olarak indeksi yeniden oluşturun veya temizleyin.

## Yaygın Tuzaklar ve Sorun Giderme
| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| `OutOfMemoryError` indeksleme sırasında | Yığın boyutu çok düşük | JVM yığınını artırın (`-Xmx2g` veya daha yüksek) |
| Sonuç döndürülmedi | Parça tokenı işlenmedi | `while` döngüsünün `getNextChunkSearchToken()` `null` olana kadar çalıştığından emin olun |
| Yavaş arama performansı | İndeks optimize edilmemiş | Toplu eklemelerden sonra `index.optimize()` çalıştırın |

## Sıkça Sorulan Sorular

**Q: Parça‑tabanlı arama nedir?**  
**A:** Parça‑tabanlı arama, veri kümesini daha küçük parçalara bölerek, tüm belgeleri belleğe yüklemeden büyük veri hacimlerinde verimli sorgular yapılmasını sağlar.

**Q: Yeni dosyalarla indeksimi nasıl güncellerim?**  
**A:** Yeni belgelerin yolunu `index.add()` ile çağırmanız yeterlidir; indeks otomatik olarak onları ekleyecektir.

**Q: GroupDocs.Search farklı dosya formatlarını destekliyor mu?**  
**A:** Evet, PDF, DOCX, XLSX, PPTX ve birçok diğer yaygın formatı destekler.

**Q: Tipik performans darboğazları nelerdir?**  
**A:** Bellek kısıtlamaları ve optimize edilmemiş indeksler en yaygın olanlardır; yeterli yığın ayırın ve indeksi düzenli olarak optimize edin.

**Q: Daha ayrıntılı belgeleri nereden bulabilirim?**  
**A:** Derinlemesine kılavuzlar ve API referansları için resmi [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) adresini ziyaret edin.

**Q: Parça‑tabanlı arama şifreli PDF'lerde çalışır mı?**  
**A:** Evet, uygun API aşırı yüklemesiyle şifreyi sağladığınız sürece çalışır.

**Q: İndeksleme ilerlemesini nasıl izleyebilirim?**  
**A:** `Index.add()`'ın `Progress` nesnesi döndüren aşırı yüklemesini kullanın veya günlük geri çağırmalarına bağlanın.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Son Güncelleme:** 2026-02-21  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs