---
date: '2026-02-19'
description: GroupDocs.Search for Java ile aramalarda stop kelimeleri devre dışı bırakmayı
  ve belgeleri indekse eklemeyi öğrenerek sorgu doğruluğunu artırın.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Aramada Durdurma Kelimeleri: GroupDocs.Search Java ile Belgeleri İndexe Ekle'
type: docs
url: /tr/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Arama'da Durdurma Kelimeleri: GroupDocs.Search Java ile Belgeleri İndekse Ekle

Eğer **belgeleri indekse eklemek** istiyor ve özellikle yaygın olan önemli terimlerin göz ardı edilmediğinden emin olmak istiyorsanız doğru yerdesiniz. Bu rehberde, GroupDocs.Search for Java kullanarak **arama sırasında durdurma kelimelerini devre dışı bırakmayı** göstereceğiz; böylece “on”, “by” veya “the” gibi her token aranabilir hâle gelir ve sonuçlarınız çok daha doğru olur.

## Hızlı Yanıtlar
- **“Belge eklemek” ne anlama geliyor?** Kaynak dosyalarınızı sorgulanabilir bir indeks içine yüklemek ve böylece verimli bir şekilde sorgulanabilmesini sağlamak demektir.  
- **Neden durdurma kelimelerini devre dışı bırakmalıyım?** Alanınızda anlam taşıyan yaygın kelimeleri (ör. “on”, “the”) aramalara dahil etmek için.  
- **Hangi kütüphane sürümü gerekiyor?** GroupDocs.Search for Java 25.4 veya daha yenisi.  
- **Lisans gerekir mi?** Değerlendirme için ücretsiz deneme çalışır; üretim ortamı için kalıcı bir lisans gerekir.  
- **Bunu bir Maven projesinde kullanabilir miyim?** Evet – aşağıda gösterildiği gibi depoyu ve bağımlılığı eklemeniz yeterlidir.

## Durdurma kelimeleri nedir ve neden devre dışı bırakmak isteyebilirsiniz?
Durdurma kelimeleri, birçok arama motorunun sorgu hızını artırmak için otomatik olarak filtrelediği sık kullanılan terimlerdir. Bu, genel web aramaları için performansı artırsa da, “on”, “by” veya “as” gibi kelimelerin gerçek anlam taşıdığı özel alanlarda (hukuki sözleşmeler, e‑ticaret katalogları, teknik kılavuzlar vb.) kesinliği azaltabilir. Durdurma kelimelerini devre dışı bırakmak, her kelimeyi önemli kabul etmenizi sağlar ve ilgili hiçbir belge kaçırılmaz.

## GroupDocs.Search’te belge ekleme nasıl çalışır?
Belgeleri eklediğinizde kütüphane her dosyayı okur, içeriğini token’lara ayırır ve bu token’ları optimize edilmiş bir veri yapısında (indeks) saklar. İndeksleme tamamlandığında motor, büyük koleksiyonlarda bile milisaniyeler içinde eşleşen belgeleri geri getirebilir.

## Önkoşullar

- **Gerekli Kütüphaneler**: GroupDocs.Search for Java 25.4 (veya daha yenisi).  
- **Geliştirme Ortamı**: IntelliJ IDEA, Eclipse veya tercih ettiğiniz herhangi bir Java IDE.  
- **Temel Bilgi**: Java sözdizimi ve indeksleme kavramına aşina olmak.

## GroupDocs.Search for Java Kurulumu

### Maven Kurulumu

Maven kullanıyorsanız `pom.xml` dosyanıza aşağıdakileri ekleyin:

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

Alternatif olarak en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Lisans Alma Adımları
- **Ücretsiz Deneme** – hemen test etmeye başlayın.  
- **Geçici Lisans** – tam işlevsellik için zaman sınırlı bir anahtar alın.  
- **Satın Alma** – üretim kullanımı için kalıcı bir lisans edinin.

## Temel Başlatma ve Ayarlar

İndeksin davranışını kontrol etmek için bir `IndexSettings` örneği oluşturun:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Arama sırasında durdurma kelimelerini nasıl devre dışı bırakılır (Java)

Aşağıdaki satır, yerleşik durdurma‑kelime filtresini kapatır:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parametreler*: `setUseStopWords` bir boolean alır.  
*Amaç*: Yaygın durdurma kelimeleri dahil olmak üzere **her kelimenin** indekslenip aranabilir olmasını sağlar.

## Belgeleri indekse nasıl eklenir

### Çıktı Dizini Tanımlama

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Belge Dizini Belirleme

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Artık `YOUR_DOCUMENT_DIRECTORY` içindeki her dosya **belgeleri indekse eklenmiş** ve sorgulanmaya hazırdır.

## Arama Sorgusu Çalıştırma

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Durdurma kelimeleri devre dışı bırakıldığı için `"on"` terimi arama sırasında dikkate alınır ve aksi takdirde göz ardı edilecek eşleşmeler döndürülür.

## Pratik Kullanım Alanları

1. **Kurumsal Belge Arama** – Kritik terminolojinin filtrelenmediğinden emin olun.  
2. **E‑ticaret Platformları** – Ürün açıklamalarındaki her kelimeyi indeksleyerek ürün keşfini iyileştirin.  
3. **Hukuki Araştırma Araçları** – Yaygın olarak durdurma kelimesi olarak kabul edilen terimler dâhil, her hukuki terimi yakalayın.

## Performans Düşünceleri

- **Optimizasyon İpuçları**: Arama hızını yüksek tutmak için indeksinizi düzenli olarak güncelleyin ve temizleyin.  
- **Kaynak Kullanımı**: JVM heap boyutunu izleyin; büyük indeksler çöp toplama ayarlarının ayarlanmasını gerektirebilir.  
- **Java Bellek Yönetimi**: Verimli veri yapıları kullanın ve çok büyük veri kümeleri için off‑heap depolamayı değerlendirin.

## Yaygın Sorunlar ve Çözümler

| Belirti | Muhtemel Neden | Çözüm |
|---|---|---|
| Yaygın kelimeler için sonuç gelmiyor | `setUseStopWords(true)` (varsayılan) | Yukarıda gösterildiği gibi `setUseStopWords(false)` çağırın. |
| İndeksleme sırasında bellek dışı hatalar | Aynı anda çok fazla büyük dosya indeksleniyor | Dosyaları partiler halinde indeksleyin; `-Xmx` JVM seçeneğini artırın. |
| Arama eski verileri döndürüyor | Yeni dosyalar eklendikten sonra indeks yenilenmemiş | `index.update()` çağırın veya değişen belgeleri yeniden ekleyin. |

## Sık Sorulan Sorular

**S: Durdurma kelimeleri nedir?**  
C: Durdurma kelimeleri, birçok arama motorunun sorgu hızını artırmak için göz ardı ettiği yaygın terimlerdir (ör. “the”, “is”, “on”). Bunları devre dışı bırakmak, her token’ın aranabilir olmasını sağlar.

**S: Neden arama indekslerinde durdurma kelimeleri devre dışı bırakılır?**  
C: Hukuki veya teknik belgelerde tam ifade eşleşmesi gerektiğinde, her kelime anlam taşır; bu yüzden durdurma kelimeleri dahil edilmelidir.

**S: GroupDocs.Search büyük veri setlerini nasıl yönetir?**  
C: Kütüphane, bellek kullanımını düşük tutmak için optimize edilmiş veri yapıları ve artımlı indeksleme kullanır; milyonlarca belgeyle bile çalışabilir.

**S: GroupDocs.Search başka Java uygulamalarıyla entegre edilebilir mi?**  
C: Evet, API herhangi bir Java‑tabanlı sistem (web servisleri, masaüstü uygulamaları vb.) içine kolayca gömülmek üzere tasarlanmıştır.

**S: Arama sonuçlarım doğru değilse ne yapmalıyım?**  
C: İndeksin tüm gerekli belgeleri içerdiğini (`add documents to index`) doğrulayın, gerektiğinde durdurma kelime filtresinin devre dışı bırakıldığını kontrol edin ve büyük değişikliklerden sonra indeksi yeniden oluşturmayı düşünün.

## Ek Kaynaklar

- **Dokümantasyon**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API Referansı**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **İndirme**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- **GitHub Deposu**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ücretsiz Destek**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Bu rehberi izleyerek artık **belgeleri indekse eklemeyi** ve **arama sırasında durdurma kelimelerini devre dışı bırakmayı** öğrenerek Java uygulamalarınızda daha doğru sonuçlar sunabilirsiniz.

---

**Son Güncelleme:** 2026-02-19  
**Test Edilen Sürüm:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs  

---