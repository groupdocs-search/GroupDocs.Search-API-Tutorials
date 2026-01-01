---
date: '2025-12-19'
description: GroupDocs.Search for Java kullanarak bir Java dosya uzantısı filtresinin
  nasıl uygulanacağını öğrenin; mantıksal operatörler, oluşturma/değiştirme tarihleri
  ve yol filtrelerini kapsar.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: GroupDocs.Search ile Java dosya uzantısı filtresi – Rehber
type: docs
url: /tr/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Search ile java file extension filter'ı ustalaşma

Artan bir belge deposunu yönetmek hızla bunaltıcı bir hâle gelebilir. Yalnızca belirli belge türlerini indekslemek ya da alakasız dosyaları dışlamak isterken, **java file extension filter** işlenmesi gereken dosyalar üzerinde ince ayar kontrolü sağlar. Bu rehberde GroupDocs.Search for Java kurulumunu adım adım gösterecek ve dosya‑uzantısı filtrelemesini mantıksal AND, OR ve NOT operatörleriyle, ayrıca tarih‑aralığı ve yol filtreleriyle nasıl birleştireceğinizi anlatacağız.

## Hızlı Yanıtlar
- **java file extension filter nedir?** GroupDocs.Search'ün indeksleme sırasında hangi dosya uzantılarını dahil edeceğini ya da hariç tutacağını belirten bir yapılandırma.  
- **Bu özelliği hangi kütüphane sağlar?** GroupDocs.Search for Java.  
- **Lisans gerekir mi?** Değerlendirme için ücretsiz deneme yeterlidir; üretim ortamı için tam lisans gereklidir.  
- **Filtreleri birleştirebilir miyim?** Evet – uzantı, tarih, boyut ve yol filtrelerini AND, OR, NOT mantığıyla zincirleyebilirsiniz.  
- **Maven uyumlu mu?** Kesinlikle – `pom.xml` dosyanıza GroupDocs.Search bağımlılığını ekleyin.

## Giriş

Artan bir dosya deposunu verimli bir şekilde yönetmekte zorlanıyor musunuz? Belgeleri türlerine göre düzenlemek ya da indeksleme sırasında gereksiz dosyaları filtrelemek istiyorsanız, doğru araçlar olmadan bu görev göz korkutucu olabilir. **GroupDocs.Search for Java**, güçlü dosya filtreleme yetenekleriyle bu zorlukları basitleştiren gelişmiş bir arama kütüphanesidir. Bu öğreticide .NET Dosya Filtreleme tekniklerini GroupDocs.Search kullanarak uygulamayı, Mantıksal AND, OR ve NOT Filtrelerine odaklanarak anlatacağız.

### Öğrenecekleriniz
- Java ortamınızda GroupDocs.Search kurulumunu yapma  
- Çeşitli filtreleri uygulama: Dosya Uzantısı, Mantıksal Operatörler (AND, OR, NOT), Oluşturulma Zamanı, Değiştirilme Zamanı, Dosya Yolu ve Uzunluk  
- Bu filtrelerin belge yönetiminde gerçek dünya uygulamaları  
- Büyük ölçekli indeksleme görevleri için performans optimizasyon ipuçları  

Java’da dosya filtrelemenin tam potansiyelini ortaya çıkarmaya hazır mısınız? Öncelikle gereksinimlere göz atalım.

## Gereksinimler

Başlamadan önce aşağıdakilerin kurulu olduğundan emin olun:

### Gerekli Kütüphaneler ve Bağımlılıklar
- **GroupDocs.Search for Java**: 25.4 veya daha yeni bir sürüm  
- **Java Development Kit (JDK)**: Sisteminizde uyumlu bir sürüm yüklü olmalı  

### Ortam Kurulumu
- Entegre Geliştirme Ortamı (IDE): IntelliJ IDEA, Eclipse veya Maven projelerini destekleyen herhangi bir IDE kullanın.

### Bilgi Gereksinimleri
- Java programlamaya temel hakimiyet  
- Java’da dosya I/O işlemlerine aşinalık  
- Düzenli ifadeler ve tarih‑zaman manipülasyonlarını anlama  

## GroupDocs.Search for Java Kurulumu
GroupDocs.Search'ü kullanmaya başlamak için projenize bağımlılık olarak eklemeniz gerekir. İşte nasıl yapılacağı:

### Maven Yapılandırması
Aşağıdaki depo ve bağımlılık yapılandırmasını `pom.xml` dosyanıza ekleyin:

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
Alternatif olarak, en yeni sürümü doğrudan [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

#### Lisans Edinme
1. **Ücretsiz Deneme**: GroupDocs.Search özelliklerini keşfetmek için ücretsiz deneme ile başlayın.  
2. **Geçici Lisans**: Sınırlama olmadan tam işlevselliğe erişmek için geçici lisans başvurusu yapın.  
3. **Satın Alma**: Uzun vadeli kullanım için bir abonelik satın alın.  

### Temel Başlatma ve Kurulum
Kütüphane eklendikten sonra indeksleme ortamınızı başlatın:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Uygulama Kılavuzu
Şimdi, GroupDocs.Search kullanarak çeşitli dosya filtreleme özelliklerini nasıl uygulayacağınızı inceleyelim.

### Dosya Uzantısı Filtreleme
İndeksleme sırasında dosyaları uzantılarına göre filtreleyin. Bu özellik, yalnızca FB2, EPUB ve TXT gibi belirli belge türlerini işlemek istediğinizde faydalıdır.

#### Genel Bakış
Özel bir filtre yapılandırmasıyla dosya uzantısına göre belgeleri filtreleyin.

#### Uygulama Adımları
1. **Filtre Oluşturma**:
    
    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **İndeksi Başlat ve Belgeleri Ekle**:
    
    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal NOT Filtre
HTM, HTML ve PDF gibi belirli dosya uzantılarını indeksleme sırasında dışlayın.

#### Uygulama Adımları
1. **Hariç Tutma Filtresi Oluşturma**:
    
    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **İndeks Ayarlarına Uygulama**:
    
    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Belgeleri Ekleme**:
    
    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal AND Filtre
Tüm belirtilen koşulları karşılayan dosyaları dahil etmek için birden fazla kriteri birleştirin.

#### Genel Bakış
Oluşturulma zamanı, dosya uzantısı ve uzunluk gibi kriterlere göre dosyaları filtrelemek için mantıksal AND işlemleri kullanın.

#### Uygulama Adımları
1. **Filtreleri Tanımlama**:
    
    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Filtreleri Birleştirme**:
    
    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Belgeleri İndeksleme**:
    
    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Mantıksal OR Filtre
Belirtilen kriterlerden herhangi birini karşılayan dosyaları dahil edin.

#### Uygulama Adımları
1. **Filtreleri Tanımlama**:
    
    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Mantıksal Koşullarla Filtreleri Birleştirme**:
    
    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **OR Filtreyi Sonlandırma**:
    
    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Oluşturulma Zamanı Filtreleri
Dosyaları, belirli bir tarih aralığı içinde kalanları dahil etmek için oluşturulma zamanına göre filtreleyin.

#### Uygulama Adımları
1. **Tarih Aralığı Filtresi Tanımlama**:
    
    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Belg İndeksleme**:
    
    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Değiştirilme Zamanı Filtreleri
Belirli bir tarihten sonra değiştirilmiş dosyaları dışlayın.

#### Uygulama Adımları
1. **Filtre Tanımlama**:
    
    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Belgeleri İndeksleme**:
    
    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Dosya Yolu Filtreleme
Dosyaları, belirli dizinlerde bulunanları dahil etmek için dosya yollarına göre filtreleyin.

#### Uygulama Adımları
1. **Dosya Yolu Filtresi Tanımlama**:
    
    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **İndeksi Başlat ve Belgeleri Ekle**:
    
    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Yaygın Hatalar ve İpuçları

- **Aynı filtre yapılandırmasında mutlak ve göreli yolları karıştırmayın** – bu, beklenmeyen dışlamalara yol açabilir.  
- **`IndexSettings`i sıfırlamayı unutmayın**; bir filtre setinden diğerine geçerken önceki filtreler kalabilir.  
- **Büyük dosya koleksiyonları**, bellek kullanımını düşük tutmak için uzunluk üst sınırıyla uzantı filtresini birleştirerek fayda sağlar.  

## Sık Sorulan Sorular

**S: İndeks oluşturulduktan sonra filtre kriterlerini değiştirebilir miyim?**  
C: Evet. Yeni bir `DocumentFilter` ile indeksi yeniden oluşturabilir veya güncellenmiş ayarlarla artımlı indeksleme yapabilirsiniz.

**S: java file extension filter sıkıştırılmış arşivlerde (ör. ZIP) çalışır mı?**  
C: GroupDocs.Search desteklenen arşiv formatlarını indeksleyebilir, ancak uzantı filtresi arşivin kendisine uygulanır, içindeki dosyalara değil. Gerekirse iç içe filtreler kullanın.

**S: Belirli bir dosyanın neden dışlandığını nasıl debug ederim?**  
C: Kütüphanenin günlük kaydını etkinleştirin (`LoggingOptions.setEnabled(true)`) ve oluşturulan log dosyasını inceleyin – hangi filtrenin dosyayı reddettiği raporlanır.

**S: java file extension filter'ı özel regex filtreleriyle birleştirmek mümkün mü?**  
C: Kesinlikle. Uzantı filtresiyle birlikte `DocumentFilter.createAnd()` içinde bir regex filtresi sarabilirsiniz.

**S: Çok sayıda filtre eklemek performansı nasıl etkiler?**  
C: Her ek filtre indeksleme sırasında küçük bir ek yük getirir, ancak indeks boyutunun azalması genellikle maliyeti aşar. Optimal dengeyi bulmak için örnek bir veri setiyle test edin.

---

**Son Güncelleme:** 2025-12-19  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs