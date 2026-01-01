---
date: '2025-12-19'
description: GroupDocs.Search kullanarak Java'da belgeleri indekse eklemeyi ve parça
  tabanlı aramayı etkinleştirmeyi öğrenin; büyük belge setleri için performansı artırın.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Java'da parça tabanlı arama ile belgeleri indekse ekle
type: docs
url: /tr/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Parça tabanlı arama ile Java'da indeks'e belge ekleme

Günümüzün veri odaklı dünyasında, **belge ekleme** işlemini hızlı bir şekilde yapabilmek ve ardından parça tabanlı aramalar gerçekleştirebilmek, büyük dosya koleksiyonlarıyla çalışan her uygulama için hayati öneme sahiptir. İster hukuki sözleşmeler, ister müşteri destek arşivleri, ister devasa araştırma kütüphaneleriyle uğraşıyor olun, bu öğretici GroupDocs.Search for Java'yı nasıl kuracağınızı, belgeleri verimli bir şekilde indeksleyeceğinizi ve ilgili bilgileri parça‑parça alarak nasıl geri getireceğinizi adım adım gösterir.

## Neler Öğreneceksiniz
- Belirli bir klasörde arama indeksi oluşturma.  
- Birden çok konumdan **belge ekleme** adımları.  
- Parça‑tabanlı aramayı etkinleştirmek için arama seçeneklerini yapılandırma.  
- İlk ve sonraki parça‑tabanlı aramaları gerçekleştirme.  
- Parça‑tabanlı belge aramasının öne çıktığı gerçek‑dünya senaryoları.

## Hızlı Yanıtlar
- **İlk adım nedir?** Bir arama indeksi klasörü oluşturun.  
- **Birçok dosyayı nasıl eklerim?** Her belge klasörü için `index.add()` kullanın.  
- **Hangi seçenek parça aramayı etkinleştirir?** `options.setChunkSearch(true)`.  
- **İlk parçadan sonra aramaya devam edebilir miyim?** Evet, token ile `index.searchNext()` çağırın.  
- **Lisans gerekir mi?** Geliştirme için ücretsiz deneme veya geçici lisans yeterlidir; üretim için tam lisans gereklidir.

## Önkoşullar
Bu kılavuzu takip edebilmek için aşağıdakilere sahip olun:

- **Gerekli Kütüphaneler**: GroupDocs.Search for Java 25.4 ve üzeri.  
- **Ortam Kurulumu**: Uyumlu bir Java Development Kit (JDK) yüklü.  
- **Bilgi Önkoşulları**: Temel Java programlama ve Maven bilgisi.

## GroupDocs.Search for Java'ı Kurma
Projeye Maven aracılığıyla GroupDocs.Search'i eklemek için:

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

Alternatif olarak, en yeni sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

### Lisans Alımı
GroupDocs.Search'i denemek için:

- **Ücretsiz Deneme** – temel özellikleri taahhüt olmadan test edin.  
- **Geçici Lisans** – geliştirme için genişletilmiş erişim.  
- **Satın Alma** – üretim kullanımı için tam lisans.

### Temel Başlatma ve Kurulum
Aranabilir verilerin bulunacağı klasörde bir indeks oluşturun:

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

## İndekse belge ekleme
İndeks oluşturulduğuna göre, bir sonraki mantıklı adım, dosyalarınızın bulunduğu konumlardan **belge ekleme** işlemidir.

### 1. İndeks Oluşturma
**Genel Bakış**: Arama indeksi için bir dizin ayarlayın.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. İndekse Belgeleri Eklemek
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

### 4. İlk Parça Tabanlı Aramayı Gerçekleştirme
Parça‑etkin seçeneklerle ilk sorguyu çalıştırın.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Parça Tabanlı Aramaya Devam Etme
Arama tamamlanana kadar kalan parçalar üzerinde yineleme yapın.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Neden parça tabanlı arama kullanmalı?
Parça‑tabanlı arama, devasa belge koleksiyonlarını yönetilebilir parçalara ayırarak bellek baskısını azaltır ve yanıt sürelerini hızlandırır. Özellikle şu durumlarda faydalıdır:

1. **Hukuk ekipleri** binlerce sözleşme içinde belirli maddeleri bulmak zorunda.  
2. **Müşteri destek portalları** ilgili bilgi‑tabanı makalelerini anında göstermek istiyor.  
3. **Araştırmacılar** tüm dosyaları belleğe yüklemeden büyük veri setlerini süzmek istiyor.

## Performans Düşünceleri
- **Bellek Yönetimi** – Büyük indeksler için yeterli yığın alanı (`-Xmx`) ayırın.  
- **Kaynak İzleme** – İndeksleme ve arama işlemleri sırasında CPU kullanımını izleyin.  
- **İndeks Bakımı** – Eski verileri temizlemek ve indeksin taze kalmasını sağlamak için periyodik olarak yeniden oluşturun veya temizleyin.

## Yaygın Tuzaklar ve Sorun Giderme
| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| `OutOfMemoryError` indeksleme sırasında | Yığın boyutu çok düşük | JVM yığınını artırın (`-Xmx2g` veya daha yüksek) |
| Sonuç döndürülmüyor | Parça token'ı işlenmedi | `while` döngüsünün `getNextChunkSearchToken()` `null` olana kadar çalıştığından emin olun |
| Yavaş arama performansı | İndeks optimize edilmemiş | Toplu eklemeler sonrası `index.optimize()` çalıştırın |

## Sık Sorulan Sorular

**S: Parça‑tabanlı arama nedir?**  
C: Parça‑tabanlı arama, veri kümesini daha küçük parçalara bölerek, büyük hacimli veriler üzerinde bellek yüklemesi yapmadan verimli sorgular yapılmasını sağlar.

**S: İndeksimi yeni dosyalarla nasıl güncellerim?**  
C: Yeni belgelerin yolunu `index.add()` ile çağırmanız yeterlidir; indeks otomatik olarak bunları ekleyecektir.

**S: GroupDocs.Search farklı dosya formatlarını destekliyor mu?**  
C: Evet, PDF, DOCX, XLSX, PPTX ve birçok yaygın formatı destekler.

**S: Tipik performans darboğazları nelerdir?**  
C: Bellek kısıtlamaları ve optimize edilmemiş indeksler en yaygın sorunlardır; yeterli yığın ayırın ve indeksi düzenli olarak optimize edin.

**S: Daha ayrıntılı belgeleri nereden bulabilirim?**  
C: Ayrıntılı kılavuzlar ve API referansları için resmi [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) adresini ziyaret edin.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Referansı**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **İndirme**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ücretsiz Destek**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans**: [Geçici Lisans Alın](https://purchase.groupdocs.com/temporary-license)

---

**Son Güncelleme:** 2025-12-19  
**Test Edilen Sürüm:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs  

---