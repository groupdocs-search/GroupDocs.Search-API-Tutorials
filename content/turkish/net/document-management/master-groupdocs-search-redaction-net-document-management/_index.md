---
date: '2026-07-16'
description: GroupDocs Search ve Redaction kullanarak .NET'te belgeleri nasıl redact
  edeceğinizi öğrenin, ayrıca daha hızlı belge yönetimi için arama sonuçlarını vurgulayın.
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: GroupDocs Search ve Redaction kullanarak .NET'te belgeleri nasıl redact
  edeceğinizi öğrenin, ayrıca daha hızlı belge yönetimi için arama sonuçlarını vurgulayın.
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: GroupDocs Search kullanarak .NET'te Belgeleri Redact Etme
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: GroupDocs Search kullanarak .NET'te Belgeleri Redact Etme
type: docs
url: /tr/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# GroupDocs Search ile .NET'te Belgeleri Kırpma

Modern işletmelerde, **belgeleri kırpma** hızlı ve güvenli bir şekilde günlük bir zorluktur. GroupDocs.Search'i GroupDocs.Redaction for .NET ile birlikte kullanmak, sadece hassas içeriği kırpmakla kalmayıp aynı zamanda bulanık aramalar yapmanıza ve HTML'de **arama sonuçlarını vurgulama** imkanı tanıyan sağlam, kutudan çıkar çıkmaz bir çözüm sunar. Bu öğretici, kütüphanelerin kurulumu, bir indeks oluşturma, bulanık sorgu çalıştırma ve vurgulanan çıktıyı üretme adımlarını net, üretim‑hazır kod parçacıklarıyla gösterir.

## Hızlı Yanıtlar
- **İlk adım nedir?** GroupDocs.Search ve GroupDocs.Redaction NuGet paketlerini kurun.  
- **PDF ve Word dosyalarını kırpabilir miyim?** Evet, her iki format da kutudan çıkar çıkmaz desteklenir.  
- **Bulanık arama mevcut mu?** Kesinlikle – doğruluğu %0 ile %100 arasında ayarlayabilirsiniz.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme lisansı yeterlidir; üretim için ücretli lisans gereklidir.  
- **Çözüm .NET 6'da çalışacak mı?** Evet, kütüphaneler .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ ve .NET 6+ ile uyumludur.

## GroupDocs.Search Nedir?
GroupDocs.Search, 100'den fazla dosya formatı üzerinde hızlı indeksleme ve tam metin arama sağlayan bir .NET kütüphanesidir. Tüm dosyayı belleğe yüklemeden 2 GB'a kadar belgeleri işleyebilir, bu da büyük ölçekli depolar için idealdir. Artımlı indekslemeyi, çok dilli analizi destekler ve .NET uygulamalarıyla sorunsuz bir şekilde bütünleşir, geliştiricilerin minimum kodla güçlü arama deneyimleri oluşturmasına olanak tanır.

## Belge Kırpma İçin GroupDocs.Redaction Neden Kullanılmalı?
GroupDocs.Redaction, 30'dan fazla yerleşik kırpma deseni sunar ve toplu işleme destek verir; kişisel verilerin, gizli maddelerin veya düzenleyici işaretlerin kalıcı olarak kaldırılmasını sağlar. Benchmark testlerinde, 500 sayfalık bir PDF'i kırpmak standart bir sunucuda 2 saniyeden kısa sürer. Motor, belgenin içerik akışı üzerinde çalışır, kırpılan alanların geri getirilemeyeceğini garanti eder ve orijinal biçimlendirme ve düzeni korur.

## Önkoşullar
- **Gerekli Kütüphaneler:** GroupDocs.Search, GroupDocs.Redaction  
- **Desteklenen Platformlar:** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE:** Visual Studio 2022 veya daha yeni (herhangi bir sürüm)  
- **Temel Beceriler:** C#, dosya G/Ç ve OOP kavramlarına aşinalık  

## Bir .NET projesinde GroupDocs.Search ve GroupDocs.Redaction Nasıl Kurulur?
NuGet paketlerini .NET CLI, Package Manager Console veya UI üzerinden kurun, ardından projenize bir lisans dosyası ekleyin. Bu iki adımlı kurulum, indeksleme veya kırpma kodu yazmadan önce ihtiyacınız olan tek şeydir. Paketleri ekledikten sonra lisans dosyasını uygulama kök dizinine yerleştirip kod dosyalarınızda ilgili ad alanlarını referans göstermelisiniz.

## GroupDocs.Redaction'ı .NET İçin Kurma
GroupDocs.Search ve GroupDocs.Redaction'ı .NET uygulamalarınızda kullanmaya başlamak için aşağıdaki kurulum adımlarını izleyin:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
“GroupDocs.Redaction”ı arayın ve en son sürümü kurun.

### Lisans Edinme Adımları
1. **Ücretsiz Deneme**: Geçici bir lisans almak için [GroupDocs](https://www.groupdocs.com) sitesine kaydolun.  
2. **Satın Alma**: Tam erişim için GroupDocs web sitesinden bir lisans satın alın.  
3. **Geçici Lisans**: Sağlanan bağlantı üzerinden değerlendirme amaçlı edin.

#### Temel Başlatma ve Kurulum
`Index` sınıfı, disk üzerinde depolanan bir aranabilir indeksi temsil eder ve belgeleri ekleme, güncelleme ve sorgulama yöntemleri sunar. Kurulumdan sonra projenizi gerekli yapılandırmalarla başlatın:  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## Uygulama Kılavuzu

### Belgeleri Oluşturma ve İndeksleme
**Genel Bakış**  
Bu özellik, birden fazla dosya içeren bir klasör için indeks oluşturarak belgeleri verimli bir şekilde düzenlemeyi gösterir.

#### Adım 1: Yolları Tanımla  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### Bulanık Arama Kurulumu ve Çalıştırılması
**Genel Bakış**  
Bulanık arama, arama terimlerindeki küçük farklılıklara rağmen belgeleri bulmanızı sağlar. Bu özellik, ayarlanabilir doğrulukla bir bulanık arama kurulumunu gösterir.

#### Adım 1: Bulanık Aramayı Etkinleştir  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### HTML Formatında Arama Sonuçlarını Vurgulama
**Genel Bakış**  
Arama sonuçlarını vurgulamak, bir dosya içinde ilgili bölümleri görsel olarak işaretler ve hızlı analiz yapmayı kolaylaştırır.

#### Adım 1: Yüksek Sıkıştırmayı Ayarla  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### Adım 2: Vurgula ve Çıktı Al  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### Sorun Giderme İpuçları
- Yolların doğru belirtildiğinden emin olun, dosya bulunamadı hatalarını önlemek için.  
- Dizinlerde okuma/yazma işlemleri için gerekli tüm izinlerin ayarlandığını doğrulayın.  

## Pratik Uygulamalar
1. **Hukuki Belge İncelemesi** – Büyük hukuki veri kümelerinde dava ile ilgili terimleri hızlıca bulun.  
2. **Akademik Araştırma** – Binlerce makalede belirli metodolojileri arayın.  
3. **İş Zekâsı** – Çeyrek raporlarından ana metrikleri manuel arama yapmadan çekin.  
4. **Müşteri Desteği** – Tekrarlayan sorunlar için destek biletlerini tarayın ve analiz öncesinde kişisel verileri kırpın.  
5. **İçerik Yönetim Sistemleri (CMS)** – Hassas parçaları otomatik kırpma ve bulanık arama ile içerik getirmeyi geliştirin.  

## Performans Hususları
- Hız ve disk kullanımını dengelemek için indeks depolama ayarlarını optimize edin.  
- Veriyi güncel tutmak ve gereksiz işlemeyi azaltmak için indeksleri düzenli olarak güncelleyin.  
- Özellikle büyük toplu işlemlerde bellek sızıntılarını önlemek için kullanılmayan nesneleri hemen serbest bırakın.  

## GroupDocs Redaction Kullanarak PDF'den Hassas Bilgileri Nasıl Kırparız?
`Redactor`, desteklenen belge formatlarına kırpma desenleri uygulamak için kullanılan ana sınıftır. Hedef PDF'i `Redactor redactor = new Redactor("file.pdf")` ile yükleyin, bir kırpma deseni tanımlayın (ör. `redactor.AddRedaction(new RedactionPhrase("confidential"))`) ve `redactor.Apply()` metodunu çağırın – kütüphane, orijinal dosyayı kırpılmış içerikle üzerine yazar ve düzeni korur. Bu tek‑adımlı iş akışı, korunan ifadenin hiçbir izinin kalmamasını garanti eder.

## Bulanık Sorgudan Sonra HTML'de Arama Sonuçlarını Nasıl Vurgularsınız?
`SearchResultHighlighter`, arama eşleşmelerinden vurgulanan HTML parçacıkları oluşturmak için yardımcı araçlar sunar. Bulanık sorguyu çalıştırın, eşleşen parçaları alın ve bunları `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")` metoduna gönderin. Metod, her bir oluşumu verilen etiketlerle sarar ve her ilgili terimin görsel olarak vurgulandığı bir HTML parçacığı üretir. Vurgulanan HTML doğrudan web sayfalarına gömülebilir veya rapor olarak kaydedilebilir, böylece son kullanıcıların her eşleşmenin bağlamını görmesi kolaylaşır.

## Sıkça Sorulan Sorular

**S: Bulanık arama nedir?**  
**C:** Bulanık arama, sorgu terimindeki yazım hatalarını veya hafif varyasyonları tolere ederek yaklaşık eşleşmeler bulur.

**S: Bu kütüphaneleri ticari bir projede kullanabilir miyim?**  
**C:** Evet, geçerli bir GroupDocs lisansı ticari kullanım hakları verir.

**S: Büyük belge setlerini verimli bir şekilde nasıl yönetirim?**  
**C:** Artımlı indeksleme kullanın, toplu işlem boyutu için `IndexingOptions` ayarlarını yapın ve performansı optimal tutmak için düzenli indeks yeniden oluşturma zamanlayın.

**S: GroupDocs.Search hangi dosya formatlarını destekliyor?**  
**C:** PDF, DOCX, XLSX, PPTX, HTML, TXT ve JPEG, PNG gibi görüntü tipleri dahil 100'den fazla format desteklenir.

**S: Arama ve kırpma için çok dilli destek var mı?**  
**C:** Evet, kütüphaneler 30'dan fazla dil için dil analizörleri içerir ve küresel içerikte doğru arama ve kırpma sağlar.

## Kaynaklar
- [dokümantasyon](https://docs.groupdocs.com/search/net/)  
- [Dokümantasyon](https://docs.groupdocs.com/search/net/)  
- [destek forumu](https://forum.groupdocs.com/c/search/10)  
- [API Referansı](https://reference.groupdocs.com/redaction/net)  
- [İndir](https://www.groupdocs.com/products/search-net)

---

**Son Güncelleme:** 2026-07-16  
**Test Edilen:** GroupDocs.Search 2.0.0 ve GroupDocs.Redaction 2.0.0 for .NET  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [GroupDocs.Search ve Redaction Kullanarak .NET Belgelerinde Arama Sonuçlarını Vurgulama](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [GroupDocs Redaction ve Search'ı .NET'te Ustalıkla Kullanma: Verimli Belge Yönetimi ve Güvenli Arama](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
- [GroupDocs.Redaction .NET ile Belge Kırpma Ustalığı: Güvenli Belge Yönetimi için İndeksleme ve Takma Ad Yönetimi](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)