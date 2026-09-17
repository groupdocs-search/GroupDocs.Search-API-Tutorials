---
date: '2026-09-16'
description: GroupDocs ile .NET'te arama dizini oluşturmayı, dizine belgeler eklemeyi
  ve daha akıllı sorgu sonuçları için eşanlamlı aramayı etkinleştirmeyi öğrenin.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: GroupDocs ile .NET'te arama dizini oluşturmayı, dizine belgeler eklemeyi
  ve daha akıllı sorgu sonuçları için eşanlamlı aramayı etkinleştirmeyi öğrenin.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: GroupDocs ve .NET kullanarak arama dizini oluşturma ve eşanlamlı arama
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: GroupDocs ve .NET kullanarak arama dizini oluşturma ve eşanlamlı arama
type: docs
url: /tr/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# GroupDocs ve eşanlamlı arama ile .NET'te arama dizini oluşturma

Bu rehberde GroupDocs.Search kullanarak **arama dizini oluşturma** yöntemini, bu dizine belgeleri eklemeyi ve eşanlamlı aramayı etkinleştirerek kullanıcıların farklı terminoloji kullansalar bile ilgili içeriği bulabilmelerini öğreneceksiniz. Hukuki bir depo, kurumsal bir bilgi tabanı veya araştırma arşivi oluşturuyor olun, aşağıdaki adımlar .NET Framework 4.6.1+, .NET Core ve .NET 5+ üzerinde çalışan üretim‑hazır bir çözüm sunar.

## Hızlı cevaplar
- **“arama dizini oluşturma” ne anlama geliyor?** Belgelerinizin aranabilir bir kataloğunu oluşturur, çıkarılan metni milisaniye sürede arama yapabilecek şekilde optimize edilmiş bir yapıda saklar.  
- **Neden eşanlamlı arama kullanılmalı?** Sorguyu aynı anlamı taşıyan kelimelerle genişleterek tipik veri kümelerinde geri getirme oranını %30’a kadar artırır.  
- **Ana önkoşullar nelerdir?** .NET 4.6.1+ (veya .NET Core/5+), C# bilgisi ve GroupDocs.Search + GroupDocs.Redaction NuGet paketleri.  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme yeterlidir; üretim dağıtımları için kalıcı lisans gerekir.  
- **Bunu redaksiyonla birleştirebilir miyim?** Evet—GroupDocs.Redaction, aramadan önce veya sonra hassas verileri maskeleyebilir.

## “arama dizini oluşturma” nedir?
**Arama dizini**, her belgeden çıkarılan metin ve meta verileri tutan bir veri yapısıdır; bu sayede motor eşleşen dosyaları anında bulabilir. GroupDocs.Search, kaynak klasörü tarar, desteklenen formatları ayrıştırır ve belirttiğiniz bir dizine sıkıştırılmış dizin dosyaları yazarak bu dizini oluşturur.

## Neden eşanlamlı arama etkinleştirilmeli?
Eşanlamlı arama, kullanıcının sorgusuna otomatik olarak alternatif terimler ekler; böylece **“improve”** (iyileştir) araması, **“enhance,” “upgrade,”** veya **“optimize”** (optimize et) içeren belgeleri de döndürür. Pratikte bu, sonuç geri getirme oranını %20‑35 artırırken kesinliği yüksek tutar, çünkü yerleşik eşanlamlı sözlük her dil için özenle hazırlanmıştır.

## Önkoşullar
- **.NET Framework 4.6.1** veya üzeri (veya herhangi bir .NET Core/5+ çalışma zamanı).  
- Temel C# geliştirme becerileri ve Visual Studio (Community, Professional veya Enterprise).  
- NuGet üzerinden GroupDocs.Search ve GroupDocs.Redaction paketlerinin kurulmuş olması.

### Kurulum
GroupDocs.Redaction for .NET’i aşağıdaki yöntemlerden biriyle kurun (ayrıntılar için [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) belgesine bakın):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Alternatif olarak Visual Studio’da NuGet Package Manager UI’sini kullanarak “GroupDocs.Redaction” paketini aratıp doğrudan yükleyebilirsiniz. API referansı için [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net) sayfasına bakın.

### Lisans edinme
- **Ücretsiz deneme:** Tüm özellikleri keşfetmek için deneme sürümüyle başlayın.  
- **Geçici lisans:** [GroupDocs web sitesinden](https://purchase.groupdocs.com/temporary-license/) geçici lisans başvurusu yapın veya [GroupDocs Lisans Yönetimi](https://purchase.groupdocs.com/temporary-license/) portalı üzerinden lisansınızı yönetin.  
- **Tam satın alma:** Üretime geçmeye hazır olduğunuzda, değerlendirme sınırlamalarını kaldıran tam lisansı satın alın.

## GroupDocs.Redaction for .NET nasıl kurulur
GroupDocs.Redaction, aramadan önce veya sonra hassas içeriği gizlemek için temel işlevselliği sağlar. Bir `Redactor` sınıfı sunar; bu sınıfı bir lisans ve isteğe bağlı yapılandırma ayarlarıyla örnekleyebilirsiniz.

Aşağıdaki kod, bir redaktör örneği oluşturup lisans dosyasını yüklemeyi gösterir:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Redaktör hazır olduğunda, arama sonuçlarından elde ettiğiniz herhangi bir belge üzerinde `redactor.Redact(...)` metodunu çağırabilirsiniz.

## Arama dizini nasıl oluşturulur
Arama dizini oluşturmak, dizin dosyalarının saklanacağı bir klasör belirtmeyi ve ardından GroupDocs.Search’ten `Index` sınıfını başlatmayı içerir. Dizin, kaynak belgelerinizden çıkarılan tüm aranabilir verileri tutar.

İlk olarak dizin için bir klasör oluşturun ve ardından `Index` nesnesini örnekleyin:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Dizin oluşturulduğunda klasöre bir dizi ikili dosya yazılır; bu dosyalar genellikle 1.000 sayfa başına 200 KB’nın altında olur ve milyonlarca sayfayı disk alanı tükenmeden ölçeklendirmenizi sağlar.

## Belgeler dizine nasıl eklenir
Belgeleri eklemek, API’yi kaynak dosyaları içeren dizine yönlendirmeyi ve dizinin bunları almasını sağlar. İşlem, her desteklenen formatı ayrıştırır, metni çıkarır ve hızlı geri getirme için dizine kaydeder.

Aşağıdaki kod, bir kaynak klasördeki tüm dosyaları indekslemek için kullanılır:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search **30+** giriş formatını destekler—DOCX, PDF, PPTX, HTML ve yaygın görüntü türleri dahil—bu sayede ek dönüştürücülere ihtiyaç duymadan neredeyse her kurumsal arşivi indeksleyebilirsiniz.

## Eşanlamlı arama nasıl etkinleştirilir ve çalıştırılır
Eşanlamlı işleme, `SearchOptions` aracılığıyla açılır. Etkinleştirildiğinde, her sorgu otomatik olarak sözlüğün eşanlamlılarını içerir, böylece kesinliği kaybetmeden geri getirme artırılır.

Aşağıdaki snippet ile eşanlamlı aramayı etkinleştirin:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

Varsayılan eşanlamlı sözlük, İngilizce için **5.000**’den fazla terim çifti içerir. Endüstri‑spesifik jargon için özel bir `SynonymDictionary` dosyası da yükleyebilirsiniz.

## Özel eşanlamlı sözlük
Alan‑spesifik eşanlamlılara ihtiyacınız varsa, kendi sözlük dosyanızı yükleyin ve bir sorgu çalıştırmadan önce `SearchOptions` içine atayın.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Yaygın sorun giderme ipuçları
- **Yol sorunları:** Dizin ve kaynak klasörlerinin işlem hesabı tarafından erişilebilir olduğundan emin olun.  
- **Lisans sınırlamaları:** Lisanssız bir yapı, indekslenen dosya sayısını 100 ile sınırlayabilir.  
- **Sonuç yok:** Eşanlamlı sözlüğün yüklendiğini doğrulayın; çalışma zamanında `options.SynonymDictionary.Count` değerini inceleyebilirsiniz.  

## Pratik uygulamalar
1. **Hukuki belge yönetimi:** Hukuki terimler ve eşanlamlılarıyla dava içeriğini bulun.  
2. **Akademik araştırma:** Bilimsel PDF ve Word dosyaları arasında literatür aramalarını genişletin.  
3. **Kurumsal bilgi tabanları:** Kullanıcılar sorguyu farklı şekilde ifade ettiğinde bile iç politikaları geri getirin.  
4. **İçerik yönetim sistemleri:** Editörlere makaleleri etiketlerken daha zengin keşif imkanı sunun.  
5. **Müşteri‑destek biletleme:** Eşanlamlı problem tanımlarıyla biletleri bilinen sorunlarla eşleştirin.  

## Performans değerlendirmeleri
- **Dizin bakımı:** Toplu güncellemeler sonrası yeniden indeksleyin; artımlı indeksleme, kesinti süresini %70’e kadar azaltır.  
- **Kaynak izleme:** Standart bir VM (2 vCPU, 8 GB RAM) üzerinde 10 GB’lık bir parti indeksleme, ~1.2 GB RAM’e kadar çıkabilir; limitlere yaklaşınca parti boyutunu kısıtlayın.  
- **Nesne temizleme:** `index.Dispose()` ve `redactor.Dispose()` metodlarını işi bitirir bitirmez çağırarak yerel kaynakları serbest bırakın.  

## Sonuç
Artık GroupDocs ile **arama dizini oluşturma**, bu dizine belge ekleme ve daha sezgisel bir kullanıcı deneyimi için eşanlamlı aramayı etkinleştirme konusunda bilgi sahibisiniz. Bu temel, redaksiyon, özel sıralama veya bulanık eşleşme gibi ek katmanları sağlam bir arama motoru üzerine eklemenize de olanak tanır.

## Sonraki adımlar
- Yazım hatalarını yakalamak için `SearchOptions.FuzzySearch` ile deney yapın.  
- Öncelikli belgeleri artırmak için `Ranking` API’sini keşfedin.  
- İpuçlarını paylaşmak ve sorular sormak için [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) veya [Free Support Forum](https://forum.groupdocs.com/c/search/10) topluluğuna katılın.  
- Güncellemeler ve yeni özellikler için [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) sayfasını kontrol edin.  

## Sıkça sorulan sorular

**S: Eşanlamlı arama nedir?**  
C: Eşanlamlı arama, kullanıcının sorgusunu önceden tanımlanmış alternatif terimlerle genişleterek farklı ifadeler kullanan ilgili belgeleri bulma şansını artırır.

**S: GroupDocs lisansımı nasıl güncellerim?**  
C: Yeni lisans dosyasını `License.SetLicense("path/to/license.lic")` yöntemiyle yüklemek için [GroupDocs Lisans Yönetimi](https://purchase.groupdocs.com/temporary-license/) portalına gidin.

**S: Çok dilli bir ortamda eşanlamlı arama kullanabilir miyim?**  
C: Evet—desteklediğiniz her yerel dil için dil‑spesifik bir `SynonymDictionary` dosyası yükleyin; motor sorguya göre uygun eşanlamlı setini uygular.

**S: En yaygın indeksleme sorunları nelerdir?**  
C: Dosya erişim izinleri, desteklenmeyen formatlar ve deneme sürümü belge sınırını aşma, geliştiricilerin karşılaştığı başlıca üç sorundur.

**S: Çok büyük dizinler için performansı nasıl optimize edebilirim?**  
C: Artımlı indeksleme kullanın, dizini SSD’lerde tutun ve `IndexingOptions.MaxDegreeOfParallelism` ayarını CPU çekirdek sayınıza göre yapılandırın.

---

**Son Güncelleme:** 2026-09-16  
**Test Edilen:** GroupDocs.Search 23.10 for .NET  
**Yazar:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## İlgili Eğitimler

- [GroupDocs.Search .NET Eğitimleri ile Dökümanı Diziine Ekle](/search/net/document-management/)
- [GroupDocs.Search ve Redaction Kullanarak .NET Belgelerinde Arama Sonuçlarını Vurgulama](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [GroupDocs.Search & Redaction (.NET) ile Dizini Güncelleme](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)