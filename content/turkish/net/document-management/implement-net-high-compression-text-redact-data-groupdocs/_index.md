---
date: '2026-06-07'
description: GroupDocs.Search ve GroupDocs.Redaction kullanarak .NET uygulamalarında
  metin depolama için high compression .NET'i nasıl uygulayacağınızı ve gizli verileri
  nasıl redakte edeceğinizi öğrenin.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'GroupDocs ile Yüksek Sıkıştırma .NET: Metin ve Redaksiyon Kılavuzu'
type: docs
url: /tr/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# GroupDocs ile Yüksek Sıkıştırmalı .NET Uygulaması: Metin ve Redaksiyon Rehberi

Modern .NET çözümlerinde, **implement high compression .net** büyük metin koleksiyonlarını disk kullanımını artırmadan depolamanız gerektiğinde hayati öneme sahiptir. Aynı zamanda, kişisel kimlik bilgileri veya finansal rakamlar gibi hassas bilgileri korumak güvenilir redaksiyona ihtiyaç duyar. Bu öğretici, adım adım, **GroupDocs.Search** ile yüksek sıkıştırmalı metin depolamayı nasıl yapılandıracağınızı ve **GroupDocs.Redaction** kullanarak gizli verileri nasıl güvenli bir şekilde redakte edeceğinizi gösterir. Sonunda, indekslenmiş metni %90’a kadar sıkıştırabilecek ve PDF'ler, Word dosyaları ve birçok diğer formatta özel içeriği kaldırabileceksiniz.

## Hızlı Yanıtlar
- **Yüksek sıkıştırmalı indekslemeyi sağlayan kütüphane hangisidir?** GroupDocs.Search for .NET.  
- **Hassas verileri redakte eden araç hangisidir?** GroupDocs.Redaction for .NET.  
- **Belgeleri otomatik olarak indekse ekleyebilir miyim?** Evet—bir klasör tarama döngüsü içinde `AddDocument` API'sini kullanın.  
- **Sıkıştırma arama için kayıpsız mı?** Evet, metin sıkıştırma sonrası tamamen aranabilir kalır.  
- **Üretim için lisansa ihtiyacım var mı?** Ticari kullanım için kalıcı bir GroupDocs lisansı gereklidir.

## “implement high compression .net” nedir?
Implement high compression .net, GroupDocs.Search indeksleme motorunu çıkarılan metin içeriğini sıkıştırılmış bir biçimde depolayacak şekilde yapılandırmak anlamına gelir. Bu, disk üzerindeki indeks boyutunu büyük ölçüde azaltırken metnin tamamen aranabilir kalmasını sağlar. Sıkıştırma kayıpsızdır, bu yüzden sorgu alaka düzeyi ve snippet çıkarımı sıkıştırılmamış bir indeksle aynı şekilde çalışır.

## Sıkıştırma ve redaksiyon için neden GroupDocs kullanılmalı?
GroupDocs.Search, elliden fazla girdi formatını destekler ve indekslenmiş metni yüzde doksan’a kadar sıkıştırabilir, bu da büyük belge koleksiyonlarının orijinal boyutlarının sadece bir kısmını kaplamasını sağlar. GroupDocs.Redaction ise otuzdan fazla dosya türünde hassas bilgileri kalıcı olarak silerek veya maskeleyerek bu süreci tamamlar ve GDPR ve HIPAA gibi katı uyumluluk düzenlemelerini ek araçlar olmadan karşılamanıza yardımcı olur.

## Önkoşullar
- **Geliştirme ortamı:** Visual Studio 2022 veya daha yeni, .NET 6+ (veya .NET Framework 4.7.2).  
- **Kütüphaneler:** `GroupDocs.Search` ve `GroupDocs.Redaction` NuGet paketleri.  
- **İzinler:** Kaynak belgeleri ve indeks çıkış konumunu içeren klasörlere okuma/yazma erişimi.  
- **Temel bilgi:** C# sözdizimi, dosya G/Ç ve .NET proje yapısına aşinalık.

## GroupDocs ile yüksek sıkıştırmalı .NET nasıl uygulanır?
GroupDocs ile yüksek sıkıştırmalı .NET uygulamak için, önce bir `TextStorageSettings` örneği oluşturup `CompressionLevel` özelliğini `High` olarak ayarlayın. Ardından ayarları ve indeksin depolanacağı klasörü geçerek bir `Index` nesnesi örnekleyin. İndeks hazır olduğunda `AddDocument` kullanarak belgeleri ekleyin ve sonunda `Search` yöntemiyle aramalar gerçekleştirin; bu süreçte motor sıkıştırma ve sıkıştırma çözmeyi şeffaf bir şekilde yönetir.

### Adım 1: Gerekli NuGet paketlerini kurun
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- “GroupDocs.Search” için arama yapın ve **Install**'a tıklayın.  

### Adım 2: GroupDocs.Redaction'ı kurun (veri redaksiyonu için)
- **NuGet Package Manager**'ı açın.  
- **GroupDocs.Redaction** için arama yapın ve en son stabil sürümü kurun.  

### Adım 3: Lisans alın ve uygulayın
- **Ücretsiz deneme:** 30 günlük deneme anahtarı için GroupDocs portalına kaydolun.  
- **Geçici lisans:** Geliştirme ortamları için geçici bir anahtar isteyin.  
- **Kalıcı lisans:** Değerlendirme sınırlamalarını kaldırmak için üretim lisansı satın alın.

### Adım 4: Her iki kütüphanenin temel başlatılması
`Search` ve `Redaction` motorları ortak bir lisans modelini paylaşır. Uygulama başlangıcında bunları başlatın:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Özellik 1: Yüksek Sıkıştırmalı Metin Depolama Ayarları

### İndeksleme Yapılandırmasını Ayarlama
`TextStorageSettings`, GroupDocs.Search'e çıkarılan metni nasıl saklayacağını söyleyen sınıftır. Yüksek sıkıştırmayı etkinleştirmek, arama hızını etkilemeden indeks boyutunu **10×** kadar azaltır.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Açıklama:**  
- `CompressionLevel.High` verimli bir şekilde metin bloklarını sıkıştıran ZSTD tabanlı bir algoritmayı etkinleştirir.  
- `UseMemoryCache = false` motoru verileri diskten akış olarak zorlar, bu büyük ölçekli dağıtımlar için idealdir.

### İndeksi Oluşturma ve Yönetme
`Index` nesnesi, disk üzerindeki aranabilir depoyu temsil eder. İndeks dosyalarının depolanacağı klasörü belirler ve yukarıda tanımlanan sıkıştırma ayarlarını iletirsiniz.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Açıklama:**  
- `indexFolder`, sıkıştırılmış indeks dosyalarının nerede bulunduğunu belirler.  
- `settings`, yüksek sıkıştırma yapılandırmasını enjekte eder ve eklenen her belgenin bundan faydalanmasını sağlar.

## Özellik 2: Belgeleri İndekse Eklemek

### Belgelerinizi İndekse Ekleyin
`AddDocument`, tek bir dosyayı indekse ekler, metnini çıkarır, yapılandırılmış ayarlara göre sıkıştırır ve sonucu depolar. GroupDocs.Search bir dizin ağacından dosyaları alabilir. Aşağıdaki döngü `documentsFolder` içinde dolaşır, her dosyayı ekler ve ilerlemeyi kaydeder.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Açıklama:**  
- `AddDocument` dosyayı ayrıştırır, aranabilir metni çıkarır, `TextStorageSettings`'e göre sıkıştırır ve indekse kaydeder.  
- Bu yaklaşım **PDF, DOCX, TXT, HTML** ve **30**'dan fazla diğer format için çalışır.

## Özellik 3: Arama Sorgusu Çalıştırma

### Arama Gerçekleştirme
`Search`, sıkıştırılmış indeks üzerinde bir sorgu çalıştırır ve alaka puanları ve vurgulanan snippet'ler içeren eşleşen `DocumentResult` nesnelerinin bir koleksiyonunu döndürür. İndeks doldurulduktan sonra hızlı sorgular çalıştırabilirsiniz. `Search` yöntemi, dosya yolları ve vurgulanan snippet'ler içeren `DocumentResult` nesnelerinin bir koleksiyonunu döndürür.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Açıklama:**  
- Arama motoru sıkıştırılmış metni doğrudan tarar, bu yüzden **milyonlarca sayfa** içeren indekslerde bile sorgu gecikmesi düşük kalır.  
- `Score`, alaka düzeyini gösterir; daha yüksek değerler daha iyi bir eşleşme anlamına gelir.

## GroupDocs.Redaction ile gizli verileri nasıl redakte ederim?
GroupDocs.Redaction ile gizli verileri redakte etmek, hedef dosya için bir `Redactor` örneği oluşturarak başlar. Sosyal güvenlik numaraları gibi kaldırılacak metni tanımlayan bir veya daha fazla `SearchPattern` nesnesi tanımlayın. Her deseni `Redact` kullanarak uygulayın, `BlackOut` gibi bir `RedactionType` belirleyin ve sonucu yeni bir belge olarak kaydedin, böylece orijinal doküman dokunulmaz kalır.

`Redactor`, GroupDocs.Redaction içinde bir belgeyi yüklemek ve redaksiyon işlemleri yapmak için kullanılan ana sınıftır.  
`SearchPattern`, redakte edilecek metni tanımlayan bir düzenli ifadeyi tanımlar.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Açıklama:**  
- `SearchPattern`, sosyal güvenlik numaralarını bulmak için bir düzenli ifade kullanır.  
- `RedactionType.BlackOut`, eşleşen metni katı bir siyah dikdörtgenle değiştirir, böylece verinin geri kazanılamaması sağlanır.

## Pratik Uygulamalar
1. **Hukuki Belge Yönetimi:** Büyük dava dosyalarını otomatik olarak sıkıştırın ve arşivlemeden önce müşteri kimlik bilgilerini redakte edin.  
2. **Sağlık Kayıtları:** Yılların hasta notlarını sıkıştırılmış bir indeksde saklayın ve araştırma ortaklarıyla paylaşmadan önce PHI (Korunan Sağlık Bilgisi) kaldırın.  
3. **Finansal Raporlama:** Denetim sorguları için aranabilir metni korurken hesap numaralarını redakte ederek çeyrek dönem raporlarını güvence altına alın.

## Performans Düşünceleri
- **Sıkıştırma etkisi:** Yüksek sıkıştırma, indeks boyutunu **%90**’a kadar azaltır, bu da SSD aşınmasını düşürür ve yedekleme işlemlerini hızlandırır.  
- **Bellek kullanımı:** Çok büyük indeksler için bellek içi önbelleği devre dışı bırakın, böylece işlem ayak izi **500 MB** altında kalır.  
- **G/Ç optimizasyonu:** Disk çalkantısını azaltmak için belge eklemeyi 100’lük gruplar halinde toplu yapın.  
- **Asenkron işleme:** `AddDocument` çağrılarını `Task.Run` içinde sararak masaüstü uygulamalarda UI iş parçacıklarının yanıt vermesini sağlayın.

## Yaygın Tuzaklar ve Sorun Giderme
- **Yanlış dosya yolları:** `documentsFolder` ve `indexFolder`'ın mutlak yollar olduğundan ve uygulamanın okuma/yazma izinlerine sahip olduğundan emin olun.  
- **Lisans hataları:** `.lic` dosyalarının çalıştırılabilir dosyanın yanında dağıtıldığından veya kaynak olarak gömülü olduğundan emin olun.  
- **Arama sonuç döndürmüyor:** `TextStorageSettings` sıkıştırma seviyesinin indeksleme sırasında kullanılan seviyeyle eşleştiğini kontrol edin; eşleşmeyen ayarlar serileştirme hatalarına neden olabilir.

## Sıkça Sorulan Sorular

**S: İlk oluşturmanın ardından belgelere indeks ekleyebilir miyim?**  
C: Evet—yeni dosyalar için sadece `index.AddDocument` çağırın; motor sıkıştırılmış indeksi artımlı olarak günceller.

**S: Redaksiyon orijinal dosyayı değiştirir mi?**  
C: Hayır—orijinal dosya dokunulmaz kalır; redakte edilmiş sürüm yeni bir dosya olarak kaydedilir, belge bütünlüğü korunur.

**S: GroupDocs.Redaction hangi formatları destekliyor?**  
C: PDF, DOCX, PPTX, XLSX, görüntüler (PNG, JPEG) ve düz metin dahil olmak üzere **30**'dan fazla format.

**S: Yüksek sıkıştırma arama alakasını nasıl etkiler?**  
C: Etkilemez. Sıkıştırma metin için kayıpsızdır, bu yüzden alaka puanları sıkıştırılmamış bir indeksle aynıdır.

**S: İndeksleyebileceğim belge boyutu için bir limit var mı?**  
C: GroupDocs.Search, içeriği akış olarak işleyerek çok gigabaytlık dosyaları yönetebilir; ancak sıkıştırılmış indeks için yeterli disk alanı (orijinal boyutun yaklaşık %10’u) sağlandığından emin olun.

## Kaynaklar
- [Dokümantasyon](https://docs.groupdocs.com/search/net/)
- [API Referansı](https://reference.groupdocs.com/redaction/net)
- [.NET için GroupDocs.Redaction İndir](https://releases.groupdocs.com/search/net/)
- [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/search/10)
- [Geçici Lisans Alımı](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-06-07  
**Test Edilen Versiyon:** GroupDocs.Search 23.12 ve GroupDocs.Redaction 23.12 for .NET  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [GroupDocs.Search ve Redaction'ı .NET'te Belge Yönetimi için Uygulama](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [.NET için GroupDocs.Redaction'ı Optimize Etme: Verimli İndeks ve Yazım Yönetimi Rehberi](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [GroupDocs Redaction ve Search'ı .NET'te Ustalıkla Kullanma: Verimli Belge Yönetimi ve Güvenli Arama](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)