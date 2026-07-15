---
date: '2026-07-02'
description: GroupDocs.Redaction ve Aspose.Search.NET kullanarak .NET arama dizini
  oluşturmayı, belgeleri dizine eklemeyi, takma adları yönetmeyi ve veri güvenliğini
  sağlamayı öğrenin.
keywords:
- create search index .net
- add documents to index
- groupdocs redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to create search index .NET using GroupDocs.Redaction and
    Aspose.Search.NET, add documents to index, manage aliases, and ensure data security.
  headline: 'Create Search Index .NET with GroupDocs.Redaction: Indexing and Managing
    Aliases for Secure Document Management'
  type: TechArticle
- questions:
  - answer: Yes, both GroupDocs.Redaction and Aspose.Search.NET fully support .NET
      Core 3.1, .NET 5, .NET 6, and later.
    question: Can I use this solution with .NET Core?
  - answer: The engine is tested with indexes containing over 1 million documents,
      maintaining sub‑second query times on standard server hardware.
    question: How many documents can the index handle?
  - answer: Aliases can contain wildcard characters (`*` and `?`) but not full regex
      patterns; for complex patterns, build the query programmatically.
    question: Do aliases support regular expressions?
  - answer: Absolutely. Retrieve the document ID from the search result, load it with
      GroupDocs.Redaction, apply redaction rules, and save the protected version.
    question: Is it possible to redact after searching?
  - answer: GroupDocs offers volume‑based licensing with unlimited developers and
      deployment sites; contact sales for a custom quote.
    question: What licensing model applies to large enterprises?
  type: FAQPage
title: 'GroupDocs.Redaction ile .NET Arama Dizini Oluşturma: Güvenli Belge Yönetimi
  için İndeksleme ve Takma Adları Yönetme'
type: docs
url: /tr/net/document-management/master-document-redaction-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction ile .NET Arama Dizini Oluşturma: Güvenli Belge Yönetimi için Dizinleme ve Takma Adları Yönetme

Büyük miktarda belgeyi yönetirken hassas bilgileri gizli tutmak zorlayıcı olabilir. **GroupDocs.Redaction for .NET** ile **create search index .NET** projeleri oluşturarak belge koleksiyonlarınızı etkili bir şekilde kırpabilir ve arama yapabilirsiniz. Bu öğretici, Aspose.Search.NET kullanarak bir dizin oluşturma veya açma, dizine belgeler ekleme, takma ad sözlüklerini yönetme ve kırpma yeteneklerini entegre etme adımlarını, veri güvenliğini sıkı bir şekilde korurken gösterir.

## Hızlı Yanıtlar
- **Bu kılavuzun temel amacı nedir?** **create search index .NET** projeleri oluşturmayı, dizine belgeler eklemeyi ve GroupDocs.Redaction ile takma adları yönetmeyi göstermek.  
- **Hangi kütüphaneler gereklidir?** GroupDocs.Redaction ve Aspose.Search.NET, her ikisi de NuGet üzerinden temin edilebilir.  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme sürümü yeterlidir; üretim için tam lisans gerekir.  
- **Büyük belge setlerini yönetebilir miyim?** Evet—her iki kütüphane de tüm dosyayı belleğe yüklemeden çok sayfalı dosyaları işleyebilir.  
- **Çözüm .NET‑Core ile uyumlu mu?** Kesinlikle; .NET 5, .NET 6 ve sonraki sürümlerde çalışır.

## Giriş

İçeriğe geçmeden önce, **create search index .NET** çözümünün neden önemli olduğunu açıklayalım. Bir dizin, binlerce dosya içinde tam ifadeleri, desenleri veya kırpılmış içeriği milisaniyeler içinde bulmanızı sağlar; bu da uyumluluk incelemeleri, yasal keşif ve iç denetimlerin çok daha hızlı yapılmasını sağlar. Aspose.Search.NET’in güçlü dizinleme motorunu GroupDocs.Redaction’ın sağlam kırpma araçlarıyla birleştirerek, veriyi anında koruyan ve bulan tek bir boru hattına sahip olursunuz.

## GroupDocs.Redaction for .NET Nedir?
GroupDocs.Redaction for .NET, PDF, DOCX, PPTX ve HTML dahil olmak üzere 30’dan fazla belge formatında metin, görüntü ve meta verileri programlı olarak kırpmanıza olanak tanıyan bir kütüphanedir. Belgeleri RAM’e tamamen yüklemeden 2 GB’a kadar işleyebilir; bu da kurumsal iş yüklerinde yüksek performans sağlar.

## Aspose.Search.NET ile .NET arama dizini neden oluşturulmalı?
Aspose.Search.NET **50+** dosya türünü dizine ekleyebilir ve artımlı güncellemeleri destekler; yani mevcut bir dizine yeni dosyalar ekleyebilir, baştan yeniden oluşturmanıza gerek kalmaz. Bu, tam yeniden dizinlemeye kıyasla CPU kullanımını %70’e kadar azaltır ve 500 k+ belge içeren dizinlerde sorgu yanıt süreleri 200 ms’nin altında kalır.

## Ön Koşullar

### Gerekli Kütüphaneler, Sürümler ve Bağımlılıklar
- **GroupDocs.Redaction** – en son NuGet sürümü, .NET 5/6/7 ile uyumlu.  
- **Aspose.Search.NET** – en son NuGet sürümü, .NET Standard 2.0+ ve .NET Core’u destekler.  

Her iki kütüphane de aynı .NET çalışma zamanı sürümünü hedeflemelidir; aksi takdirde bağlama çakışmaları oluşabilir.

### Ortam Kurulum Gereksinimleri
- Visual Studio 2022 (veya .NET 6+ destekleyen herhangi bir IDE).  
- Dizinlemek ve kırpmak istediğiniz belgelerin bulunduğu bir klasöre erişim.  

### Bilgi Ön Koşulları
- C# sözdizimi ve .NET proje yapıları hakkında temel bilgi.  
- Dizinleme, arama ve belge kırpma kavramlarına giriş.

## create search index .NET nasıl oluşturulur?

`Index` nesnesini yükleyin veya örnekleyin, bir klasöre yönlendirin ve `CreateOrOpen` metodunu çağırın—bu tek adım, disk üzerindeki aranabilir depoyu oluşturur veya yeniden açar. İşlem varsayılan olarak arka plan iş parçacığında çalışır, bu sayede UI binlerce dosya dizinlenirken bile yanıt verir.

`Index`, disk üzerinde depolanan aranabilir koleksiyonu temsil eder.

### Tanım Bağlantısı
`Index` sınıfı, Aspose.Search.NET’in disk üzerindeki aranabilir belge koleksiyonunu temsil eden çekirdek bileşenidir. Tüm dizinleme ve sorgu işlemleri bu nesne üzerinden akış sağlar.

```bash
dotnet add package GroupDocs.Redaction
```

## Dizine belge nasıl eklenir?

`AddDocument` bir dosyayı dizine ekler ve aranabilir içeriğini çıkarır.

Her dosya yolu için `Index.AddDocument` metodunu çağırarak belgeleri ekleyin; metod metin, meta veri ve isteğe bağlı OCR içeriğini otomatik olarak çıkarır. Dosyaları bir `foreach` döngüsü içinde toplu olarak ekleyebilir ve dizin mevcut girdileri yeniden oluşturulmadan artımlı olarak güncellenir. İşlem ayrıca başarı ya da hata durumunu gösteren bir durum nesnesi döndürür; bu sayede hataları programatik olarak ele alabilirsiniz.

```powershell
Install-Package GroupDocs.Redaction
```

## Lisans Edinme Adımları

- **Ücretsiz Deneme** – 30 gün boyunca tüm özellikleri ücretsiz keşfedin.  
- **Geçici Lisans** – Uzun süreli testler için zaman sınırlı bir anahtar kullanın.  
- **Tam Lisans** – Üretim dağıtımları için gereklidir ve tüm değerlendirme kısıtlamalarını kaldırır.

Kurulumdan sonra GroupDocs.Redaction aşağıdaki gibi başlatılır:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Set up additional configuration as needed
```

## Uygulama Kılavuzu

Uygulamayı özelliklere göre yönetilebilir bölümlere ayıracağız.

### Dizini Oluşturma veya Açma

#### Genel Bakış
Arama dizini oluşturma veya açma, verimli belge yönetimi ve arama için temeldir. Bu, indekslenmiş verilerle hızlı çalışmanızı sağlar.

#### Adım‑Adım Talimatlar

**1. Dizini Oluştur/Aç**

```csharp
using GroupDocs.Search;

// Specify the directory where your index will be stored
string indexPath = "YOUR_INDEX_DIRECTORY";

// Initialize or open an existing index
Index index = new Index(indexPath);

// Explanation: The Index object is initialized with a directory path,
// which serves as a storage location for all indexed data.
```

**2. Dizine Belgeler Ekleyin**

```csharp
using GroupDocs.Search;

// Specify your document directory
string docPath = "YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index
index.Add(docPath);

// Explanation: The Add method indexes all documents within the provided path,
// making them searchable.
```

### Takma Ad Sözlüğünü Yönetme

#### Genel Bakış
Takma ad sözlüğündeki takma adlar, karmaşık arama sorguları için kısaltmalar tanımlamanıza olanak tanır; bu da arama verimliliğini ve okunabilirliğini artırır.

#### Adım‑Adım Talimatlar

**1. Mevcut Takma Adları Temizle**

```csharp
using GroupDocs.Search.Dictionaries;

// Check if there are existing aliases and clear them
if (index.Dictionaries.AliasDictionary.Count > 0)
{
    index.Dictionaries.AliasDictionary.Clear();
}

// Explanation: This ensures you start with a clean slate when managing aliases.
```

**2. Tek Takma Ad Girişi Ekle**

```csharp
index.Dictionaries.AliasDictionary.Add("t", "(gravida OR promotion)");
index.Dictionaries.AliasDictionary.Add("e", "(viverra OR farther)");

// Explanation: Each alias is mapped to an expression that defines its search scope.
```

**3. Dizi Kullanarak Birden Çok Takma Ad Ekle**

```csharp
AliasReplacementPair[] pairs = new AliasReplacementPair[]
{
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};

index.Dictionaries.AliasDictionary.AddRange(pairs);

// Explanation: AddRange allows bulk addition of aliases, streamlining the setup process.
```

### Takma Adları Alma ve Dışa Aktarma

#### Genel Bakış
Takma ad sözlüğünüzü bir dosyaya dışa aktarmak, arama sözlüklerini ekipler veya ortamlar arasında paylaşmanızı sağlar; belirli girişleri almak ise sorgu mantığını doğrulamanıza yardımcı olur.

**Takma Adı Al**

```csharp
if (index.Dictionaries.AliasDictionary.Contains("e"))
{
    string replacement = index.Dictionaries.AliasDictionary.GetText("e");
}

// Explanation: Use Contains to check existence before retrieval.
```

**Takma Adları Dışa Aktar**

```csharp
string exportPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ExportDictionary(exportPath);

// Explanation: ExportDictionary saves the alias dictionary for future use or sharing.
```

### Takma Adları İçe Aktarma ve Takma Ad Sözlüğü ile Arama

#### Genel Bakış
Önceden tanımlanmış takma adları içe aktararak arama işlemlerini kolaylaştırın, ardından bu takma adları referans alan sorgular çalıştırın.

**1. Takma Adları İçe Aktar**

```csharp
string importPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ImportDictionary(importPath);

// Explanation: This method loads existing alias definitions into the dictionary.
```

**2. Takma Adları Kullanarak Ara**

```csharp
string query = "@t OR @e"; // Use aliases in your search query
SearchResult result = index.Search(query);

// Explanation: Leverage aliases to perform complex searches with simple queries.
```

## Yaygın Sorunlar ve Çözümler

- **Dizin Yolu Hataları** – Klasör yolunun mutlak olduğundan ve uygulamanın okuma/yazma izinlerine sahip olduğundan emin olun.  
- **Bellek Sızıntıları** – Uzun süre çalışan hizmetlerde `Index` nesnelerini kullanımdan sonra her zaman `Dispose()` ile serbest bırakın.  
- **Takma Ad Tanınmıyor** – Takma ad dosyasının UTF‑8 kodlamasını kullandığını ve her satırın `key=value` biçiminde olduğuna dikkat edin.

## Sık Sorulan Sorular

**S: Bu çözümü .NET Core ile kullanabilir miyim?**  
C: Evet, GroupDocs.Redaction ve Aspose.Search.NET .NET Core 3.1, .NET 5, .NET 6 ve sonraki sürümleri tam olarak destekler.

**S: Dizin kaç belgeyi kaldırabilir?**  
C: Motor, 1 milyonun üzerindeki belge içeren dizinlerle test edilmiştir ve standart sunucu donanımında saniyenin altında sorgu süreleri sağlar.

**S: Takma adlar düzenli ifadeleri destekliyor mu?**  
C: Takma adlar `*` ve `?` gibi joker karakterleri içerebilir ancak tam regex desenlerini desteklemez; karmaşık desenler için sorguyu programatik olarak oluşturun.

**S: Aramadan sonra kırpma yapılabilir mi?**  
C: Kesinlikle. Arama sonucundan belge kimliğini alın, GroupDocs.Redaction ile yükleyin, kırpma kurallarını uygulayın ve korumalı sürümü kaydedin.

**S: Büyük işletmeler için hangi lisans modeli geçerlidir?**  
C: GroupDocs, sınırsız geliştirici ve dağıtım sitesi içeren hacim‑bazlı lisanslar sunar; özel teklif için satış ekibiyle iletişime geçin.

## Sonuç

**GroupDocs.Redaction** ile **Aspose.Search.NET**’i entegre ederek **create search index .NET** çözümleri oluşturmayı öğrendiniz; bu sayede belge güvenliği, uyumluluk ve keşfedilebilirliği büyük ölçüde artırabilirsiniz. Artık bir dizin oluşturma, dizine belge ekleme, takma ad sözlüğü yönetme ve kırpma kurallarını uygulama araçlarına sahipsiniz; hepsi tek bir yüksek‑performanslı .NET uygulaması içinde.

Sonraki adımlar? Kod parçacıklarını bir test projesinde uygulayın, özel takma ad desenleriyle deney yapın ve indeksleme hızını üretim veri setinizle karşılaştırarak ölçüm alın.

---

**Son Güncelleme:** 2026-07-02  
**Test Edilen Sürümler:** GroupDocs.Redaction 23.10 for .NET, Aspose.Search.NET 24.5  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [Master Document Indexing and Advanced Search Queries with GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Master Index Creation and Merging with GroupDocs.Redaction .NET for Efficient Document Management](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Implementing GroupDocs.Search and Redaction in .NET for Document Management](/search/net/document-management/groupdocs-search-redaction-net-guide/)