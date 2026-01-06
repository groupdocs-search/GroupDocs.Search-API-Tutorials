---
date: '2026-01-06'
description: GroupDocs.Search Java ile belgeleri indekse eklemeyi ve meta veriye göre
  belge aramayı öğrenin. İndeks ayarlarını ustalaşın, indeksler oluşturun, belgeler
  ekleyin ve kesin aramalar gerçekleştirin.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: Java'da GroupDocs.Search kullanarak Metaveri İndeksleme ile belgelere indeks
  ekleme
type: docs
url: /tr/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Java'da GroupDocs.Search kullanarak Metadata Indexing ile belgeleri indekse ekleme

Modern uygulamalarda, **belgeleri indekse ekleme** işlemini hızlı ve güvenilir bir şekilde gerçekleştirmek, hızlı arama deneyimleri sunmak için esastır. İster bir hukuk deposu, ister müşteri‑destek bilgi tabanı, ister dahili bir belge portalı oluşturuyor olun, metadata kullanmak, yazar, başlık veya özel etiketler gibi **metadata ile belgeleri arama** yapmanıza olanak tanır. Bu kılavuz, indeks ayarlarını yapılandırmayı, metadata odaklı bir indeks oluşturmayı, dosyalarınızı eklemeyi ve güçlü aramalar çalıştırmayı—hepsini Java için GroupDocs.Search ile—adım adım anlatır.

## Hızlı Yanıtlar
- **Metadata indexing'in birincil amacı nedir?** Belge özelliklerine dayalı hızlı aramaları, tam metin içeriğine göre mümkün kılar.  
- **İndekse dosyaları ekleyen yöntem hangisidir?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Özel metadata alanlarıyla arama yapabilir miyim?** Evet, alanlar indekslendikten sonra doğrudan sorgulayabilirsiniz.  
- **Geliştirme için lisansa ihtiyacım var mı?** Değerlendirme için geçici bir deneme lisansı yeterlidir; üretim için tam lisans gereklidir.  
- **Hangi Java sürümü gereklidir?** JDK 8 ve üzeri önerilir.

## GroupDocs.Search'te metadata indexing nedir?
Metadata indexing, belge niteliklerini (ör. yazar, oluşturma tarihi, özel etiketler) aranabilir bir yapıda çıkarır ve depolar. **belgeleri indekse ekleme** yaptığınızda, motor bu nitelikleri kaydeder ve “*John Doe* tarafından yazılmış tüm PDF'leri bul” gibi kesin sorgular çalıştırmanıza olanak tanır.

## Neden metadata indexing için GroupDocs.Search kullanmalısınız?
- **Performans:** Metadata aramaları hafiftir ve sonuçları milisaniyeler içinde döndürür.  
- **Esneklik:** Çok çeşitli dosya formatlarını (PDF, DOCX, PPT vb.) destekler.  
- **Ölçeklenebilirlik:** Milyonlarca belgeyi minimum bellek tüketimiyle işler.

## Önkoşullar
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 ve üzeri kurulu ve yapılandırılmış.  
- Java ve Maven konusunda temel bilgi.

## GroupDocs.Search for Java Kurulumu

### Kurulum Talimatları
`pom.xml` dosyanıza GroupDocs deposunu ve bağımlılığı ekleyin:

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

En son ikili dosyaları doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden de indirebilirsiniz.

### Lisans Alımı
Test için geçici bir lisans almak:

1. GroupDocs web sitesini ziyaret edin ve **Purchase** (Satın Alma) bölümüne gidin.  
2. Değerlendirme ihtiyaçlarınıza uygun bir **temporary license** (geçici lisans) planı seçin.

## Adım Adım Uygulama

### Özellik 1: Index Ayarları Yapılandırması
İndeksi metadata'ya odaklanacak şekilde yapılandırın:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` motorun tam metin içeriği yerine metadata'yı önceliklendirmesini sağlar.

### Özellik 2: Belirtilen Klasörde Index Oluşturma
Tüm metadata'nın depolanacağı fiziksel bir indeks dizini oluşturun:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

`YOUR_DOCUMENT_DIRECTORY` ifadesini projenizin yapısına uygun yol ile değiştirin.

### Özellik 3: Belgeleri indekse ekleme
İndeks oluşturulduğuna göre, **belgeleri indekse ekleme** yaparak bunların aranabilir olmasını sağlayabilirsiniz:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**İpuçları:**  
- Klasör yolunun doğru olduğundan ve uygulamanın okuma izinlerine sahip olduğundan emin olun.  
- GroupDocs.Search her dosyadan desteklenen metadata'yı otomatik olarak çıkarır.

### Özellik 4: Metadata ile belge arama
Metadata alanlarını hedefleyen bir sorgu çalıştırın; örneğin dilin İngilizce olduğu belgeleri arama:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

- `search(query)` indekslenmiş metadata'yı tarar ve eşleşen belgeleri döndürür.

## Pratik Uygulamalar
1. **Kurumsal Belge Yönetimi:** Sözleşmeleri sözleşme tarihi veya imzalayan adıyla getirin.  
2. **Dijital Kütüphane Katalogları:** Kullanıcıların kitapları tür, yayın yılı veya yazarına göre göz atmasını sağlayın.  
3. **CRM Sistemleri:** Müşteri ID'si veya bölge gibi özel metadata kullanarak müşteri dosyalarını hızlıca bulun.

## Performans Düşünceleri
- **Artımlı Güncellemeler:** Tüm indeksi yeniden oluşturmak yerine yeni veya değişen dosyalar için `index.addOrUpdate()` kullanın.  
- **Bellek Ayarı:** İndekslenen metadata miktarına göre JVM yığın boyutunu (`-Xmx`) ayarlayın.  
- **Optimum Depolama:** İndeksi sıkıştırmak ve sorgu hızını artırmak için periyodik olarak `index.optimize()` çağırın.

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|----------|
| **Sonuç döndürülmedi** | Beklediğiniz metadata alanlarının gerçekten kaynak dosyalarda mevcut olduğunu doğrulayın. |
| **İzin hataları** | Java sürecinin belge klasörüne ve indeks dizinine okuma erişimine sahip olduğundan emin olun. |
| **Bellek yetersizliği hataları** | JVM yığın boyutunu artırın veya `add` işlemini daha küçük gruplar halinde işlemek için toplu (batch) çalıştırın. |

## Sık Sorulan Sorular

**S: Metadata indexing nedir?**  
C: Metadata indexing, belge niteliklerini (yazar, başlık, özel etiketler) aranabilir bir yapıda depolar ve tam metni taramadan hızlı aramalar yapmayı sağlar.

**S: Geçici bir lisans nasıl alınır?**  
C: GroupDocs satın alma sayfasını ziyaret edin ve deneme lisansı almak için adımları izleyin.

**S: Bu kurulumla PDF'leri indeksleyebilir miyim?**  
C: Evet, GroupDocs.Search PDF, DOCX, PPT ve birçok diğer formatı destekler.

**S: Belgeleri eklerken yaygın sorunlar nelerdir?**  
C: Doğru dosya yollarını doğrulayın ve uygulamanın dizinler için okuma izinlerine sahip olduğundan emin olun.

**S: Arama performansını nasıl optimize ederim?**  
C: İndeksinizi düzenli olarak güncelleyin, artımlı eklemeler kullanın ve JVM bellek ayarlarını optimize edin.

## Kaynaklar

- **Dokümantasyon:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **API Referansı:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **İndirme:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Deposu:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ücretsiz Destek Forumu:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-01-06  
**Test Edilen Versiyon:** GroupDocs.Search Java 25.4  
**Yazar:** GroupDocs