---
date: '2026-04-02'
description: GroupDocs.Search ve GroupDocs.Redaction kullanarak .NET'te faceted arama
  uygularken arama dizini oluşturmayı ve dizine belge eklemeyi öğrenin.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Redaction .NET Faceted Search ile GroupDocs Arama Dizini Oluştur
type: docs
url: /tr/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Redaction .NET Faceted Search ile GroupDocs Arama Dizini Oluştur

Modern uygulamalarda, **GroupDocs ile bir arama dizini oluşturmak** hızlı ve doğru belge getirme için gereklidir. Hukuki sözleşmeler, ürün katalogları veya büyük bilgi tabanlarıyla çalışıyor olun, iyi tasarlanmış bir dizin **belgeleri dizine eklemenizi** sağlar ve birkaç saniye içinde güçlü faceted aramaları çalıştırır. Bu öğretici, sürecin tamamını adım adım gösterir—GroupDocs.Redaction kurulumundan basit ve karmaşık faceted sorguların oluşturulmasına kadar— böylece .NET projelerinizde duyarlı bir arama deneyimi sunabilirsiniz.

## Hızlı Yanıtlar
- **Ana amaç nedir?** GroupDocs ile bir arama dizini oluşturmak ve faceted aramayı etkinleştirmek.  
- **Hangi kütüphaneler gereklidir?** .NET için GroupDocs.Redaction ve GroupDocs.Search.  
- **Belgeyi dizine nasıl eklerim?** Dizini başlattıktan sonra `index.Add(documentsFolder)` kullanın.  
- **Karmaşık sorgular çalıştırabilir miyim?** Evet, gelişmiş filtreleme için nesne sorgularını mantıksal operatörlerle birleştirin.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari bir lisans gereklidir.

## Faceted arama nedir ve GroupDocs ile neden kullanılır?
Faceted arama, kullanıcıların sonuçları aynı anda birden fazla filtre (kategori, tarih veya yazar gibi) uygulayarak daraltmasına olanak tanır. **GroupDocs.Redaction** ile birleştirildiğinde, kırpma kurallarına saygı gösteren güvenli ve aranabilir içerik elde edersiniz; bu da uyumluluğun yüksek olduğu ortamlar için idealdir.

## Önkoşullar

### Gerekli Kütüphaneler, Sürümler ve Bağımlılıklar
- **GroupDocs.Redaction .NET** – en son stabil sürüm.  
- **GroupDocs.Search .NET** – indeksleme için Redaction ile el ele çalışır.

### Ortam Kurulum Gereksinimleri
- **IDE**: Visual Studio 2019 ve sonrası.  
- **Framework**: .NET Core 3.1, .NET 5 veya .NET 6.  
- **OS Compatibility**: Windows, Linux, macOS.

### Bilgi Önkoşulları
Temel C# becerileri ve faceted arama kavramlarına yüksek seviyede bir anlayış yardımcı olur, ancak adım adım rehber yeni başlayanlar için de dostça hazırlanmıştır.

## GroupDocs.Redaction'ı .NET için Kurma

### Kurulum Bilgileri
Aşağıdaki yöntemlerden herhangi birini kullanarak GroupDocs.Redaction paketini ekleyebilirsiniz:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- "GroupDocs.Redaction"ı arayın ve en son sürümü yükleyin.

### Lisans Edinme Adımları
Tüm özelliklerin kilidini açmak için ücretsiz deneme ile başlayın veya kalıcı bir lisans edinin:

1. Lisans seçeneklerini incelemek için [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin.  
2. Ekrandaki talimatları izleyerek deneme veya satın alınmış lisans dosyanızı alın.

### Temel Başlatma ve Kurulum
Paket yüklendikten sonra, uygulamanızda Redactor'ı başlatın:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## GroupDocs arama dizini nasıl oluşturulur

Aşağıda uygulamayı iki bölüme ayırıyoruz: **Simple Faceted Search** ve **Complex Query**. Her bölüm, **search index groupdocs oluşturmayı**, belgeleri eklemeyi ve sorguları çalıştırmayı gösterir.

### Özellik 1: Basit Faceted Arama

**Overview**  
Faceted arama, kullanıcıların birden fazla kriter seçerek sonuçları daraltmasına olanak tanır. Bu bölüm, GroupDocs.Search kullanarak basit bir yaklaşımı gösterir.

#### Adım 1: Dizin ve Belgeler Klasörlerini Tanımlayın
Dizinin bulunacağı ve kaynak belgelerinizin yer alacağı klasör yollarını ayarlayın.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Adım 2: Bir Dizin Oluşturun
Tanımladığınız klasörde arama dizinini başlatın.

```csharp
Index index = new Index(indexFolder);
```

#### Adım 3: Belgeleri Dizine Ekleyin
Belgelerinizi yükleyin, böylece aranabilir hale gelirler.

```csharp
index.Add(documentsFolder);
```

#### Adım 4: Metin Sorgusu Araması Yapın
**content** alanına karşı temel bir metin sorgusu çalıştırın.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Adım 5: Nesne Sorgusu Araması Gerçekleştirin
Daha ince kontrol için nesne‑yönelimli sorgular kullanın.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Özellik 2: Karmaşık Sorgu

**Overview**  
Birden fazla filtreyi—dosya adı desenleri ve ifade eşleşmeleri gibi—birleştirmeniz gerektiğinde, mantıksal operatörler kullanarak karmaşık bir sorgu oluşturabilirsiniz.

#### Adım 1: Dizin ve Belgeler Klasörlerini Tanımlayın
Daha gelişmiş bir senaryo için aynı klasör yapısını yeniden kullanın.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Adım 2: Bir Dizin Oluşturun ve Belgeleri Ekleyin
(Basit örnekten adım 2‑3'ü görün; aynı kalır.)

#### Adım 3: Metin Sorgusu Araması Yapın
Dosya adı ve içerik kriterlerini karıştıran birleşik bir metin sorgusu çalıştırın.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Adım 4: Nesne Sorgularını Oluşturun ve Çalıştırın
Aynı mantığı programatik olarak oluşturun.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

İfade, aralık ve boolean operatörlerini birleştirerek tam iş kurallarınıza uymaya devam edin.

## Pratik Uygulamalar
1. **E‑Commerce Platforms** – Kategorilere, fiyata ve puana göre ürünleri filtreleyin.  
2. **Document Management Systems** – Sözleşmeleri yazar, tarih veya gizlilik seviyesine göre bulun.  
3. **Content Portals** – Okuyucuların etiketler, konular ve yayın tarihleriyle derinlemesine arama yapmasına izin verin.

## Performans Düşünceleri
- **Index Refresh**: Aramayı hızlı tutmak için yeni veya güncellenen dosyaları düzenli olarak yeniden indeksleyin.  
- **Memory Management**: Özellikle büyük veri setlerinde, işiniz bittiğinde `Index` nesnelerini serbest bırakın.  
- **Asynchronous Indexing**: Yoğun indeksleme sırasında UI donmalarını önlemek için `Task.Run` veya arka plan hizmetlerini kullanın.

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| **Index not found** | `indexFolder` yolunu doğrulayın ve klasörün yazma izinlerine sahip olduğundan emin olun. |
| **No results returned** | Sorguladığınız alanların (ör. `Content`, `Filename`) indekslendiğini kontrol edin. |
| **Out‑of‑memory errors** | Belgeleri partiler halinde işleyin ve .NET GC yığın boyutunu artırmayı düşünün. |

## Sıkça Sorulan Sorular

**Q: Faceted arama nedir?**  
A: Faceted arama, kullanıcıların kategori, tarih veya yazar gibi birden fazla bağımsız filtre kullanarak sonuçları daraltmasına olanak tanır.

**Q: GroupDocs.Search ile büyük veri setlerini nasıl yönetirim?**  
A: Bellek kullanımını düşük tutmak ve performansı yüksek tutmak için artımlı indeksleme, toplu işleme ve asenkron operasyonlar kullanın.

**Q: GroupDocs işlevlerini mevcut .NET uygulamalarına entegre edebilir miyim?**  
A: Evet, kütüphaneler herhangi bir .NET projesiyle sorunsuz entegrasyon için tasarlanmıştır.

**Q: Faceted arama ile ilgili yaygın sorunlar nelerdir?**  
A: Karmaşık sorgu sözdizimi ve ilgili tüm alanların indekslenmesini sağlamak tipik zorluklardır; uygun test ve indeks bakımı bunları azaltır.

**Q: GroupDocs için geçici bir lisans nasıl alınır?**  
A: Değerlendirme sırasında tam işlevselliğin kilidini açan bir deneme lisansı almak için [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API Referansı**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Son Güncelleme:** 2026-04-02  
**Test Edilen Versiyonlar:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Yazar:** GroupDocs