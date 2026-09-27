---
date: '2026-09-27'
description: GroupDocs.Search for Java kullanarak java metin vurgulamayı öğrenin;
  search documents java, index documents java ve fragment highlighting konularını
  kapsar.
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: GroupDocs.Search for Java kullanarak java metin vurgulamayı öğrenin.
  Hızlı sonuçlar için indeksleme, arama ve fragment highlighting konusunda adım adım
  rehberlik alın.
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: GroupDocs.Search ile java metin vurgulama – Hızlı belge vurgulama
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: GroupDocs.Search ile java metin vurgulama
type: docs
url: /tr/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# GroupDocs.Search ile Java metin vurgulama

Modern kurumsal uygulamalarda, **highlight text java** ham arama sonuçlarını anında okunabilir içgörülere dönüştürmek için çok önemlidir. Hukuk‑inceleme portalı, akademik araştırma motoru veya müşteri‑destek panosu oluşturuyor olsanız da, sorgu terimlerini bulabilmek ve görsel olarak vurgulayabilmek, kullanıcıların manuel tarama süresini sayısız saniye tasarruf ettirir. Bu öğreticide, **GroupDocs.Search for Java** kullanarak **search documents java**, **index documents java** nasıl yapılır ve hem tam‑belge hem de parça‑düzeyinde vurgulamanın nasıl uygulanacağını sadece birkaç satır kodla gösteriyoruz.

## Hızlı cevaplar
- **What does “search and highlight text” mean?** Bir belgedeki sorgu terimlerini bulmak ve görsel olarak vurgulamak anlamına gelir (örneğin, renkli bir arka planla).  
- **Which library provides this capability?** GroupDocs.Search for Java.  
- **Do I need a license?** Değerlendirme için ücretsiz deneme çalışır; üretim kullanımı için tam lisans gereklidir.  
- **Can I customize highlight colors?** Evet—herhangi bir RGB renk `HighlightOptions` aracılığıyla ayarlanabilir.  
- **Is fragment highlighting supported?** Kesinlikle; eşleşmeden önce/sonra terimleri tanımlayarak özlü parçacıklar oluşturabilirsiniz.

## Belgelerde Java metin vurgulama nasıl yapılır

Belgelerde Java metin vurgulamak için, önce uygun sıkıştırma ayarlarıyla kaynak dosyaların bir dizinini oluşturun, ardından istenen terimleri bulmak için bir arama sorgusu çalıştırın ve son olarak sonuçları HTML, PDF veya düz metin olarak dışa aktarın; her eşleşme bir vurgulama etiketiyle sarılır. Bu üç adımlı süreç, büyük koleksiyonlarda hızlı ve doğru vurgulama sağlar.

1. **Create an index** depolama alanını düşük tutan sıkıştırma ayarlarıyla bir dizin oluşturun.  
2. **Execute a search** vurgulamak istediğiniz sorgu dizesini kullanarak bir arama yürütün.  
3. **Generate output** (HTML, PDF veya düz metin) sorgu teriminin her oluşumu bir vurgulama etiketiyle sarılmış şekilde oluşturun.

## Arama ve metin vurgulama nedir?

Arama ve metin vurgulama, indekslenmiş bir koleksiyonda belirli bir sorguyu tarama, eşleşen belgeleri getirme ve ardından çıktıda (HTML, PDF vb.) sorgu teriminin her oluşumunu işaretleme sürecidir. Bu görsel ipucu, son kullanıcıların ilgili bilgiyi anında fark etmesine yardımcı olur.

## Neden GroupDocs.Search for Java kullanmalı?

GroupDocs.Search for Java, **high‑performance indexing** (her dizin için `Compression.High` ile 50 GB'a kadar), **rich highlighting** tüm belgeler ve özel parçalar üzerinde çalışan ve **cross‑format support** 30'dan fazla dosya türü—DOCX, PDF, PPTX ve TXT dahil—için destek sunar. Kütüphane ayrıca **incremental indexing** sağlar; bu sayede tüm dizini yeniden oluşturmak zorunda kalmadan yeni dosyalar ekleyebilir ve büyük ölçekli dağıtımlarda kesinti süresini %80'e kadar azaltabilirsiniz.

## Önkoşullar
- Java Development Kit (JDK) 8 ve üzeri.  
- Bağımlılık yönetimi için Maven.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Java sözdizimi hakkında temel bilgi.

## GroupDocs.Search for Java Kurulumu

`pom.xml` dosyanıza GroupDocs deposunu ve bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

Ayrıca en son JAR dosyasını doğrudan resmi siteden indirebilirsiniz: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans edinme
Ücretsiz deneme ile başlayın veya değerlendirme için geçici bir lisans edinin. Üretim dağıtımları için tüm özelliklerin kilidini açmak amacıyla tam bir lisans satın alın.

## Uygulama rehberi

Uygulama iki pratik bölüme ayrılmıştır: **highlighting in entire documents** ve **highlighting in fragments**. Her iki bölüm de GroupDocs.Search kullanarak **how to highlight Java** belgeleri için temel adımları içerir.

### Dizin ayarlarını yapılandırma

Dizinlemeden önce, yüksek sıkıştırma kullanacak şekilde depolamayı yapılandırın—bu, arama hızını korurken disk kullanımını %70'e kadar azaltır.

`IndexSettings` dizinin disk üzerinde nasıl saklanacağını kontrol eden yapılandırma nesnesidir. Bu optimizasyonu etkinleştirmek için `Compression` değerini `Compression.High` olarak ayarlayın.  
`Compression`, dizin dosyalarına uygulanan veri sıkıştırma seviyesini belirtir; `Compression.High` en yüksek boyut azaltmasını sağlar.

## Tüm belgelerde vurgulama

### Adım 1: dizini oluştur ve doldur

Bir dizin klasörü oluşturun ve aramak istediğiniz tüm kaynak dosyaları ekleyin. `Index` sınıfı aranabilir konteyneri temsil eder.

### Adım 2: arama yap ve vurgulamayı uygula

Terimi (ör. `ipsum`) arayın ve vurgulanan eşleşmelerle bir HTML dosyası oluşturun. Vurgulama rengini ve satır içi stillerin kullanılmasını belirtmek için `HighlightOptions` kullanın.

`HighlightOptions`, ön plan ve arka plan renklerini, ayrıca her vurgulanan terime uygulanacak CSS sınıfını tanımlamanızı sağlar.  
`HtmlHighlighter`, sağlanan seçeneklere göre vurgulanan terimlerle HTML çıktısı üretir.  
`SearchResult`, eşleşen belgelerin listesini ve bulunan her terimin konumlarını içerir.

**Direct answer:** Dizininizi yükleyin, `search("ipsum")` çağrısını yapın ve elde edilen `SearchResult` nesnesini yapılandırılmış bir `HighlightOptions` örneğiyle birlikte `HtmlHighlighter`'a geçirin. Yüksekleyici, “ipsum” kelimesinin her oluşumunu seçilen arka plan rengiyle bir `<span>` içinde sarılmış HTML döndürür.

Anahtar seçeneklerin açıklaması  
- **Compression** – yüksek sıkıştırma depolamayı tasarruf eder.  
- **HighlightColor** – UI paletinize uygun herhangi bir RGB değeri ayarlayın.  
- **UseInlineStyles** – `false` temiz HTML üretir; bu HTML global olarak CSS ile stillendirilebilir.

## Parçacıklarda vurgulama

### Adım 1: dizin oluştur ve ara (yukarıdaki gibi)

Aynı dizin ve arama adımları geçerlidir; `Index` ve `SearchResult` nesnelerini yeniden kullanırsınız.

### Adım 2: parça bağlamını tanımla ve vurgula

`FragmentOptions` ile eşleşmeden önce ve sonra kaç terimin her parçacıkta görüneceğini belirtin.  
`FragmentOptions`, her snippet'te dahil edilen çevre kelime sayısını (`termsBefore` ve `termsAfter`) kontrol eder; bu sayede bağlam ile snippet uzunluğunu dengeleyebilirsiniz.

### Adım 3: vurgulanan parçacıkları al ve yaz

Oluşturulan parçacıkları toplayın ve bir HTML dosyasına yazın. Her parçacık, yapılandırdığınız `HighlightOptions`'a göre zaten vurgulanmıştır.  
`fragmentHighlighter`, belirtilen parça ve vurgulama seçeneklerini kullanarak bir `SearchResult`'tan vurgulanan snippet'ler oluşturan bir yardımcı programdır.

**Direct answer:** `SearchResult` elde edildikten sonra `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)` çağrısını yapın. Metot, eşleşen terimi yapılandırılmış bağlam kelimeleriyle çevreleyen ve seçilen renk ile vurgulanan HTML snippet'lerinin bir listesini döndürür.

## Pratik uygulamalar
1. **Legal document review** – binlerce sözleşme içinde kanunları, maddeleri veya dava referanslarını anında vurgular.  
2. **Academic research** – onlarca PDF ve Word dosyasında anahtar terminolojiyi ortaya çıkarır, literatür inceleme süresini %60'a kadar azaltır.  
3. **Customer support** – bilet geçmişlerinde sipariş numaralarını veya hata kodlarını tespit eder, ajanların sorunları daha hızlı çözmesini sağlar.

## Performans değerlendirmeleri
- **Index size** – yüksek sıkıştırma (`Compression.High`) gecikme etkisi olmadan disk alanını %70'e kadar azaltır.  
- **Fragment context** – daha büyük `termsBefore/After` değerleri snippet okunurluğunu artırır ancak sorgu başına 10–15 ms ekleyebilir.  
- **Memory management** – büyük veri kümelerini indekslerken JVM yığınını izleyin; veri seti 2 GB'yi aşıyorsa bellek kullanımını 1 GB altında tutmak için incremental indexing'i düşünün.

## Yaygın sorunlar ve çözümler
- **Indexing errors** – dosya yollarını doğrulayın ve uygulamanın dizin klasöründe okuma/yazma izinlerine sahip olduğundan emin olun.  
- **No highlights appear** – `UseInlineStyles`'ın çıktınızın formatıyla (HTML vs. PDF) eşleştiğini doğrulayın.  
- **Color not applied** – RGB değerlerinin 0‑255 aralığında olduğundan ve görüntüleyicinin satır içi CSS'i veya sağlanan CSS sınıfını desteklediğinden emin olun.

## Sıkça sorulan sorular

**Q: GroupDocs.Search for Java kullanmanın faydaları nelerdir?**  
A: Hızlı, ölçeklenebilir indeksleme, özelleştirilebilir vurgulama ve 30'dan fazla belge formatı desteği sunar; tipik bir sunucuda 500 sayfalık dosyaları 2 saniyeden kısa sürede işler.

**Q: GroupDocs.Search'ı bir REST API ile nasıl entegre edebilirim?**  
A: Arama ve vurgulama metodlarını Spring Boot denetleyicileri aracılığıyla açığa çıkarın; vurgulanan parçacıkları içeren HTML snippet'leri veya JSON yükleri döndürün.

**Q: Kütüphane şifre korumalı dosyaları işleyebiliyor mu?**  
A: Evet—belgeyi `addDocument(filePath, password)` ile dizine eklerken şifreyi sağlayın.

**Q: Vurgulama işaretlemesini renkten öte özelleştirebilir miyim?**  
A: Kesinlikle; `options.setCssClass("myHighlight")` ile bir CSS sınıfı atayabilir ve bunu global olarak stillendirebilir, ya da vurgulama sonrası oluşturulan HTML'yi değiştirebilirsiniz.

**Q: Bu kılavuz için hangi sürüm test edildi?**  
A: Kod, GroupDocs.Search 25.4 ile doğrulandı.

**Q: Highlight options java'yi satır içi stiller yerine bir CSS sınıfı kullanacak şekilde nasıl ayarlarım?**  
A: `options.setUseInlineStyles(false)` çağırın ve `options.setCssClass("myHighlight")` ile atadığınız sınıf için bir CSS kuralı tanımlayın.

**Q: PDF çıktısında terimleri doğrudan vurgulamanın bir yolu var mı?**  
A: Evet—GroupDocs.Search PDF girişiyle çalışır ve yüksekleyici, PDF görüntüleyicide gömülebilecek veya GroupDocs.Conversion kullanılarak PDF'ye yeniden dönüştürülebilecek HTML çıktısı üretir.

**Son güncelleme:** 2026-09-27  
**Test edildi:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

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

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

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

## İlgili Öğreticiler

- [Java tam metin araması nasıl uygulanır: GroupDocs.Search ile indeks dizini oluşturma](/search/java/indexing/groupdocs-search-java-create-index/)
- [GroupDocs.Search for Java ile Arama Dizinini Yönetmeyi Öğrenin](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [Java'da parça tabanlı arama ile belgelere indeks ekleme](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)