---
date: '2026-04-21'
description: GroupDocs.Redaction for .NET kullanarak dosyaları nasıl filtreleyeceğinizi
  öğrenin; oluşturma tarihine, dosya boyutuna, değiştirme tarihine göre filtreleme
  ve NOT filtrelerini nasıl uygulayacağınızı da içeren.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: GroupDocs.Redaction for .NET ile Dosyaları Nasıl Filtreleyebilirsiniz
type: docs
url: /tr/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# GroupDocs.Redaction for .NET ile Dosyaları Nasıl Filtreleyebilirsiniz

Bugünün hızlı tempolu dijital ortamında, **dosyaları nasıl filtreleyeceğiniz** verimli bir şekilde üretkenliğinizi artırabilir ya da azaltabilir. Belgeleri uzantı, oluşturulma tarihi, boyut veya değiştirilme tarihine göre ayırmanız gerekse, sağlam bir filtreleme stratejisi zaman kazandırır, depolama maliyetlerini düşürür ve arama indeksinizi düzenli tutar. Bu öğreticide, GroupDocs.Redaction for .NET kullanarak gerçek dünya örneklerini adım adım inceleyecek ve yaygın iş ihtiyaçlarını karşılamak için dosyaları nasıl filtreleyeceğinizi göstereceğiz.

## Hızlı Yanıtlar
- **Hangi kütüphane gerekiyor?** GroupDocs.Redaction for .NET (NuGet üzerinden kurun).  
- **Oluşturulma tarihine göre filtreleyebilir miyim?** Evet – `CreateCreationTimeRange` kullanın.  
- **Belirli türleri nasıl dışarıda bırakırım?** `DocumentFilter.CreateNot` ile NOT filtresi uygulayın.  
- **Dosya boyutu filtresi destekleniyor mu?** Kesinlikle, `CreateFileLengthRange` veya üst/alt sınırlarla.  
- **Lisans gerekli mi?** Üretim kullanımı için deneme veya tam lisans gerekir.

## GroupDocs.Redaction ile dosya filtreleme nedir?
Dosya filtreleme, indeksleme motoruna hangi belgelerin dahil edileceğini veya göz ardı edileceğini uzantı, tarihler, yol desenleri veya boyut gibi meta verilerle belirtmenizi sağlar. Kesin `DocumentFilter` kuralları tanımlayarak indeksinizi hafif tutar ve aramalarınızı hızlı yaparsınız.

## Neden GroupDocs.Redaction for .NET kullanmalısınız?
- **Yerleşik filtre yardımcıları** – özel dosya sistemi kodu yazmanıza gerek yok.  
- **Mantıksal operatörler** – birden fazla kriteri AND, OR ve NOT ile birleştirin.  
- **Performans‑optimizeli** – filtreler indeksleme sırasında uygulanır, sonradan değil.  
- **Çapraz platform** – .NET Framework, .NET Core ve .NET 5/6+ ile çalışır.

## Önkoşullar
- .NET Framework 4.6+ veya .NET Core 3.1+ yüklü.  
- Visual Studio veya tercih ettiğiniz C# IDE.  
- Temel C# bilgisi.  

### Gerekli Kütüphaneler ve Kurulum
Tercih ettiğiniz yöntemle NuGet paketini kurun:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Pro ipucu:** Kurulumdan sonra lisans dosyanızı proje köküne ekleyin ve herhangi bir Redactor veya Index nesnesi oluşturmadan önce `License.SetLicense("license-file-path")` çağrısını yapın.

## GroupDocs.Redaction for .NET'i Kurma

İlk olarak, çalışmak istediğiniz belgeye işaret eden bir `Redactor` örneği oluşturun:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Neden önemli:** Redactor'ı başlatmak, kütüphanenin daha sonraki iş akışında filtreleri ve redaksiyon kurallarını uygulamaya hazır olmasını sağlar.

## Dosyaları uzantıya göre nasıl filtreleyebilirsiniz

Dosya uzantısına göre filtreleme, bir belge kümesini daraltmanın en yaygın yoludur. Aşağıda yalnızca FB2, EPUB ve TXT dosyalarını tutuyoruz.

### Uzantıya göre filtreleme

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## İstenmeyen türleri dışlamak için NOT filtresi nasıl uygulanır

Eğer **NOT filtresi** mantığını uygulamanız gerekiyorsa—örneğin HTML ve PDF dosyalarını dışarıda bırakmak—`CreateNot` kullanın.

### HTM, HTML ve PDF dosyalarını dışarıda bırak

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Dosyaları oluşturulma tarihine göre nasıl filtreleyebilirsiniz

**Oluşturulma tarihine göre filtrelemeniz** gerektiğinde, bir başlangıç ve bitiş `DateTime` belirtin.

### Oluşturulma tarihi aralığına göre filtreleme

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Dosyaları değiştirilme tarihine göre nasıl filtreleyebilirsiniz

Oluşturulma tarihine benzer şekilde, sonuçları belirli bir zamandan önce değiştirilmiş dosyalarla sınırlayabilirsiniz.

### Değiştirilme tarihine göre filtreleme

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Yol üzerinden düzenli ifadelerle dosyaları nasıl filtreleyebilirsiniz

Klasör yapınız adlandırma kurallarına uyuyorsa, bir regex belirli yolları hedefleyebilir.

### Dosya yolu desenine göre filtreleme

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Dosyaları boyuta göre nasıl filtreleyebilirsiniz

Bant genişliği veya depolama limitleriyle çalışırken belge boyutunu kontrol etmek çok önemlidir.

### Dosya boyutuna göre filtreleme (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Birden fazla koşulu AND ile nasıl birleştirirsiniz

Birden fazla kriteri aynı anda **dosyaları nasıl filtreleyeceğinizi** gerektiğinde, bunları `CreateAnd` ile birleştirin.

### AND mantıksal örneği

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Birden fazla koşulu OR ile nasıl birleştirirsiniz

Birden fazla kuraldan herhangi birinin geçmesi gerektiğinde `CreateOr` kullanın.

### OR mantıksal örneği

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Yaygın Sorunlar ve Çözümler
- **Filtre uygulanmadı:** `settings.DocumentFilter`'ı `Index` örneği oluşturmadan **önce** atadığınızdan emin olun.  
- **Beklenmeyen dosyalar görünüyor:** Dosya uzantılarının baştaki noktayı (`.txt`) içerdiğini iki kez kontrol edin.  
- **Performans yavaşlaması:** Filtreleri AND ile birleştirerek indeksleme hattının erken aşamasında taranan dosya sayısını azaltın.  
- **Regex hataları:** Yol deseninizdeki özel karakterleri kaçırın veya büyük/küçük harfe duyarsız eşleşmeler için `RegexOptions.IgnoreCase` kullanın.

## Sıkça Sorulan Sorular

**S: NOT filtresini AND filtresiyle birleştirebilir miyim?**  
C: Evet. Önce NOT filtresini oluşturun (`DocumentFilter.CreateNot`) ve ardından `DocumentFilter.CreateAnd`'e argümanlardan biri olarak ekleyin.

**S: 10 MB'den büyük dosyaları nasıl filtrelerim?**  
C: `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` kullanarak yalnızca bu boyutu aşan dosyaları dahil edin.

**S: Aynı anda hem oluşturulma hem de değiştirilme tarihine göre filtreleme mümkün mü?**  
C: Kesinlikle. Her bir filtreyi ayrı ayrı oluşturup `CreateAnd` ile birleştirin.

**S: Bu filtreler bulut depolama yollarıyla çalışır mı?**  
C: Filtreler yerel dosya sisteminde çalışır. Bulut kaynakları için önce dosyaları geçici bir klasöre indirin, ardından aynı filtreleri uygulayın.

**S: Filtreyi değiştirmek yeniden indeksleme gerektirir mi?**  
C: Evet. Filtreler `index.Add` çağrısı yapıldığında değerlendirilir. Bir filtreyi değiştirmek, yeni kriterleri yansıtmak için indeksi yeniden oluşturmanız gerektiği anlamına gelir.

## Sonuç

GroupDocs.Redaction for .NET ile **dosyaları nasıl filtreleyeceğinizi** uzantı, oluşturulma tarihi, değiştirilme tarihi, dosya boyutu veya NOT mantığıyla öğrenerek belge yönetimini sadeleştirebilir, indekslerin performansını koruyabilir ve gerçekten önemli içeriğe odaklanabilirsiniz. Mantıksal operatörlerle deney yaparak filtrelemeyi tam iş kurallarınıza göre özelleştirin; böylece hız ve depolama verimliliğinde anında kazanımlar göreceksiniz.

---

**Son Güncelleme:** 2026-04-21  
**Test Edilen Versiyon:** GroupDocs.Redaction 24.11 for .NET  
**Yazar:** GroupDocs