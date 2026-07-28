---
date: '2026-02-27'
description: GroupDocs.Search for Java kullanarak Java’da metin vurgulamayı öğrenin;
  arama belgeleri Java, indeksleme belgeleri Java ve parça vurgulama konularını kapsar.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: GroupDocs.Search ile Java'da Metni Vurgulama
type: docs
url: /tr/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

 GroupDocs

Now ensure we didn't miss any markdown elements.

Check for any images: none.

Check for any shortcodes: none.

Check for any code blocks: placeholders only.

Check for any markdown links: one link.

All good.

Now produce final translated markdown content.

# GroupDocs.Search ile Java Metin Vurgulama

Bugünün hızlı tempolu dijital ortamında, büyük dosya koleksiyonları içinde **highlight text java** yapabilmek vazgeçilmez bir özelliktir. İster bir yasal inceleme platformu, ister akademik araştırma motoru, ister müşteri destek konsolu oluşturuyor olun, kullanıcıların aradığı terimleri anında bulmak deneyimi çok daha verimli kılar. Bu öğretici, **GroupDocs.Search for Java** kullanarak **search documents java**, **index documents java** ve zengin vurgulama uygulamayı—tam belgeler için ve odaklanmış parçalar için—adım adım gösterir.

## Hızlı Yanıtlar
- **What does “search and highlight text” mean?** Belge içinde sorgu terimlerini bulmak ve görsel olarak vurgulamak (ör. arka plan rengi ile) anlamına gelir.  
- **Which library provides this capability?** GroupDocs.Search for Java.  
- **Do I need a license?** Değerlendirme için ücretsiz deneme çalışır; üretim için tam lisans gereklidir.  
- **Can I customize highlight colors?** Evet—herhangi bir RGB renk `HighlightOptions` aracılığıyla ayarlanabilir.  
- **Is fragment highlighting supported?** Kesinlikle; eşleşmenin öncesi/sonrası terimleri tanımlayarak özlü snippet'ler oluşturabilirsiniz.

## Belgelerde Java Metin Vurgulama Nasıl Yapılır
Java metin vurgulama üç temel adımı içerir:

1. **Index the source files** böylece hızlıca aranabilirler.  
2. **Run a query** indekse karşı sorgu çalıştırarak eşleşen belgeleri bulmak.  
3. **Render the results with visual cues** highlighter API'si kullanarak sonuçları görsel ipuçlarıyla sunmak.

Aşağıda her adımı ayrıntılı olarak inceliyoruz; önce tam belge çıktısı, ardından parça‑seviyesindeki snippet'ler.

## Arama ve Metin Vurgulama Nedir?
Search and highlight text, belirli bir sorgu için belge indeksini tarama, eşleşen belgeleri getirme ve ardından sorgu teriminin belge çıktısı (HTML, PDF vb.) içinde her bir oluşumunu işaretleme sürecidir. Bu görsel ipucu, son kullanıcıların ilgili bilgiyi anında fark etmesine yardımcı olur.

## Neden GroupDocs.Search for Java Kullanılır?
- **High‑performance indexing** yapılandırılabilir sıkıştırma ile (`index documents java`).  
- **Rich highlighting API** tüm belgelerde ve özel parçacıklarda çalışır (`highlight search terms java`).  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT ve daha fazlası).  
- **Simple Maven integration** ve temiz bir Java‑merkezli tasarım.

## Ön Koşullar
- Java Development Kit (JDK) 8 veya daha yenisi.  
- Bağımlılık yönetimi için Maven.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Java sözdizimi hakkında temel bilgi.

## GroupDocs.Search for Java Kurulumu

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

Ayrıca en son JAR dosyasını doğrudan resmi siteden indirebilirsiniz: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Alımı
Ücretsiz deneme ile başlayabilir veya değerlendirme için geçici bir lisans edinebilirsiniz. Üretim dağıtımları için tüm özelliklerin kilidini açmak amacıyla tam lisans satın alın.

## Uygulama Kılavuzu

Uygulama iki pratik bölüme ayrılmıştır: **highlighting in entire documents** ve **highlighting in fragments**. Her iki bölüm de GroupDocs.Search kullanarak **how to highlight Java** belgeleri için gerekli adımları içerir.

### İndeks Ayarlarını Yapılandırma
İndekslemeden önce, yüksek sıkıştırma kullanacak şekilde depolamayı yapılandırın—bu, arama hızını korurken disk kullanımını azaltır.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Tam Belgelerde Vurgulama

#### Adım 1: İndeksi Oluştur ve Doldur
Aramak istediğiniz tüm kaynak dosyaları ekleyerek bir indeks klasörü oluşturun.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Adım 2: Aramayı Gerçekleştir ve Vurgulamayı Uygula
Terimi (ör. `ipsum`) arayın ve vurgulanmış eşleşmelerle bir HTML dosyası oluşturun.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Ana seçenekler açıklaması**  
- **Compression** – yüksek sıkıştırma depolamayı tasarruf sağlar.  
- **HighlightColor** – UI paletinize uyması için herhangi bir RGB değeri ayarlayın.  
- **UseInlineStyles** – `false` temiz HTML üretir ve bu, CSS ile global olarak stillendirilebilir.

### Parçacıklarda Vurgulama

#### Adım 1: İndeksle ve Ara (yukarıdaki gibi)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Adım 2: Parça Bağlamını Tanımla ve Vurgula
Her bir parçacıkta eşleşmenin öncesinde ve sonrasında kaç terim gösterileceğini belirtin.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Adım 3: Vurgulanan Parçacıkları Al ve Yaz
Oluşturulan parçacıkları toplayın ve bir HTML dosyasına yazın.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Pratik Uygulamalar
1. **Legal Document Review** – yasa maddelerini, maddeleri veya dava referanslarını anında vurgulayın.  
2. **Academic Research** – onlarca PDF ve Word dosyası arasında anahtar terminolojiyi ortaya çıkarın.  
3. **Customer Support** – bilet geçmişlerinde sipariş numaralarını veya hata kodlarını tespit edin.

## Performans Düşünceleri
- **Index Size** – yüksek sıkıştırma (`Compression.High`) disk alanını azaltır.  
- **Fragment Context** – daha büyük `termsBefore/After` değerleri doğruluğu artırır ancak hızı etkileyebilir.  
- **Memory Management** – büyük veri kümelerini indekslerken JVM yığınını izleyin; çok büyük setler için artımlı indekslemeyi düşünün.

## Yaygın Sorunlar ve Çözümleri
- **Indexing Errors** – dosya yollarını doğrulayın ve uygulamanın okuma/yazma izinlerine sahip olduğundan emin olun.  
- **No Highlights Appear** – `UseInlineStyles` ayarının çıktınızın formatına (HTML vs. PDF) uygun olduğunu kontrol edin.  
- **Color Not Applied** – RGB değerlerinin 0‑255 aralığında olduğundan ve HTML görüntüleyicisinin stili desteklediğinden emin olun.

## Sıkça Sorulan Sorular

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: Hızlı, ölçeklenebilir indeksleme, özelleştirilebilir vurgulama ve birçok belge formatını destekleme sunar.

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: Arama ve vurgulama yöntemlerini Spring Boot denetleyicileri aracılığıyla ortaya çıkarın, HTML veya JSON yükleri döndürün.

**Q: Does the library handle password‑protected files?**  
A: Evet—belgeyi indekse eklerken şifreyi sağlayın.

**Q: Can I customize the highlight markup beyond color?**  
A: Kesinlikle; `HighlightOptions` aracılığıyla CSS sınıfları ekleyebilir veya oluşturulan HTML'yi sonradan değiştirebilirsiniz.

**Q: What version was tested for this guide?**  
A: Kod, GroupDocs.Search 25.4 ile doğrulandı.

**Q: How do I set highlight options java to use a CSS class instead of inline styles?**  
A: `options.setUseInlineStyles(false)` ayarlayın ve `options.setCssClass("myHighlight")` ile atadığınız sınıf için bir CSS kuralı ekleyin.

**Q: Is there a way to highlight terms pdf java directly when the source is a PDF?**  
A: Evet—GroupDocs.Search PDF girişiyle çalışır ve vurgulayıcı, bir PDF görüntüleyiciye gömebileceğiniz veya GroupDocs.Conversion kullanarak PDF'ye geri dönüştürebileceğiniz HTML çıktısı üretir.

**Son Güncelleme:** 2026-02-27  
**Test Edilen Sürüm:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs