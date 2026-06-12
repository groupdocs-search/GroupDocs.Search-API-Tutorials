---
date: '2026-06-12'
description: GroupDocs.Search ve GroupDocs.Redaction kullanarak .NET'te arama dizini
  oluşturmayı ve PDF'ye redaksiyon uygulamayı öğrenin. Kurulum, dağıtım, indeksleme
  ve gelişmiş arama açıklanmıştır.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: GroupDocs Search ve Redaction ile .NET'te Arama Dizini Oluşturma – Kapsamlı
  Bir Rehber
type: docs
url: /tr/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# GroupDocs Search ve Redaction ile .NET'te Arama Dizini Oluşturma – Kapsamlı Bir Rehber

Günümüz dijital ortamında, **creating a search index .NET** çözümü, bilgiyi hızlıca bulabilen ve hassas verileri koruyabilen, herhangi bir organizasyon için en önemli önceliktir. Bu öğretici, ölçeklenebilir bir GroupDocs.Search ağı yapılandırmayı, düğüm dağıtımını, belge indekslemeyi ve GroupDocs.Redaction'ı **apply redaction to PDF** dosyalarına uygulamayı—tüm bunları .NET ortamında—adım adım gösterir.

## Hızlı Cevaplar
- **Bir .NET arama dizini oluşturmanın ilk adımı nedir?** Temel bir yol ve port tanımlayın, ardından ağ düğümlerini dağıtın.  
- **GroupDocs ile PDF'ye nasıl redaction uygulanır?** `Redactor` örneğini başlatın, PDF'yi yükleyin ve istediğiniz desenlerle `Redact` metodunu çağırın.  
- **Arama ağını birden fazla makinede çalıştırabilir miyim?** Evet—düğümleri ayrı sunucularda dağıtın ve ana düğümün indeksleme ve sorguları koordine etmesine izin verin.  
- **Üretim kullanımında lisansa ihtiyacım var mı?** Üretim için geçerli bir GroupDocs lisansı gereklidir; değerlendirme için geçici bir deneme lisansı mevcuttur.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.7.2+, .NET Core 3.1+, ve .NET 5/6/7 tam olarak desteklenir.

## “create search index .net” nedir?
*Creating a search index .NET* .NET kütüphanelerini kullanarak belge meta verileri ve içeriğinin aranabilir bir deposunu oluşturmayı ifade eder; bu, metni çıkarır, terimleri tokenleştirir ve optimize edilmiş bir indeks yapısında saklar. Bu, dağıtılmış düğümler arasında anlık sorgu yanıtları sağlar, çeşitli dosya formatlarını destekler ve kurumsal uygulamalarda ölçeklenebilir, yüksek performanslı belge geri getirmeye olanak tanır.

## GroupDocs Search ve Redaction'ı birlikte neden kullanmalısınız?
GroupDocs.Search **50+ dosya formatını** destekler—DOCX, PDF, PPTX ve HTML dahil—ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri indeksleyebilir. **apply redaction to PDF** işlemini sayfa başına 200 ms'den az sürede gerçekleştirebilen GroupDocs.Redaction ile birleştirildiğinde, güvenli ve yüksek performanslı bir belge yönetim hattı elde edersiniz.

## Önkoşullar

### Gerekli Kütüphaneler ve Bağımlılıklar
Bu öğreticiyi takip etmek için aşağıdaki paketleri kurun:
- **GroupDocs.Search** for .NET
- **GroupDocs.Redaction** for .NET  

Gerekli kütüphaneleri kurmak için aşağıdaki yöntemlerden herhangi birini kullanabilirsiniz:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
"GroupDocs.Search" ve "GroupDocs.Redaction" için arama yapın ve en son sürümü kurun.

### Ortam Kurulum Gereksinimleri
- .NET Framework 4.7.2 veya üzeri (veya .NET Core 3.1+)
- Visual Studio IDE (Community, Professional veya Enterprise)

### Bilgi Önkoşulları
- Temel C# programlama
- Nesne‑yönelimli kavramlar
- Ağ yapılandırmaları ve belge yönetim sistemleri hakkında aşinalık

## .NET için GroupDocs.Redaction Kurulumu

### Kurulum Bilgileri
Uygulamanıza redaction özelliklerini entegre etmek için önce GroupDocs.Redaction kütüphanesini ekleyin:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
"GroupDocs.Redaction" için arama yapın ve kurun.

### Lisans Edinimi
Ücretsiz deneme veya geçici bir lisansla başlamak için aşağıdaki adımları izleyin:
- [GroupDocs web sitesi](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret ederek geçici bir lisans talep edin.  
- Satın alma seçenekleri için [fiyatlandırma sayfası](https://groupdocs.com/pricing) adresine gidin.

Lisans dosyanızı aldıktan sonra, uygulama kurulumunuzda uygulayın:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Temel Başlatma
Temel işlemler için GroupDocs.Redaction'ı başlatmak üzere aşağıdaki kod parçacığını kullanın:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Uygulama Kılavuzu

### Konfigürasyon Ayarı

#### Genel Bakış
Bu özellik, temel bir yol ve port numarası kullanarak arama ağınızı yapılandırır ve belge yönetim sisteminizin temelini oluşturur.

#### Tanım Bağlantısı
`SearchNetworkDeployment`, ağ üzerindeki arama düğümlerinin dağıtımını yöneten sınıftır.

#### Adım 1: Temel Yol ve Port Tanımla  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Adım 2: Ağı Yapılandır  
`Configure` metodunu kullanarak belirtilen yol ve port ile arama ağını kurun:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Ağ Düğümü Dağıtımı

#### Genel Bakış
Dağıtılmış belge araması için yapılandırılmış arama ağınız içinde düğümleri dağıtın.

#### Tanım Bağlantısı
`SearchNetworkNode`, ana düğümle iletişim kuran bireysel bir aranabilir düğümü temsil eder.

#### Adım 1: Dağıtımı Başlat  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Ana Düğüm için Olay Aboneliği

#### Genel Bakış
Ağ operasyonlarını etkili bir şekilde izlemek ve yönetmek için ana düğümdeki olaylara abone olun.

#### Tanım Bağlantısı
`SearchNetworkNodeEvents`, indeksleme, sorgu yürütme ve hata yönetimi için geri çağrılar sağlar.

#### Adım 1: Ana Düğümü Belirle
İlk düğümü ana düğüm olarak seçin:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Adım 2: Olaylara Abone Ol
Olaylara aşağıdaki şekilde abone olun:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Belgeleri İndeksleme

#### Genel Bakış
Verimli arama işlemleri için belgeleri indeksleyin. Bu adım, ağınızın gerekli verileri hızlıca alabilmesini sağlamak için kritiktir.

#### Tanım Bağlantısı
`SearchIndex`, her indekslenmiş dosya için aranabilir tokenları ve meta verileri saklayan temel nesnedir.

#### Adım 1: Dizinleri İndekse Ekle
Belgelerinizi içeren dizinleri belirtin:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Arama İşlevselliği – Temel Kullanım

#### Genel Bakış
Ağdaki düğümler arasında temel arama işlemlerini gerçekleştirin.

#### Doğrudan Cevap
Ana düğümde `SearchNetwork.Query("your term")` metodunu çağırarak eşleşen belgeleri anında alın. Metot, dosya yolları ve alaka düzeyi puanlarını içeren `SearchResult` nesnelerinin bir koleksiyonunu döndürür.  
`SearchNetwork.Query`, tüm ağda bir arama sorgusu çalıştıran ve eşleşen sonuçları döndüren bir yöntemdir.

#### Adım 1: Arama Parametrelerini Tanımla  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Gelişmiş Arama İşlevselliği

#### Genel Bakış
Daha kesin sonuçlar için özelleştirilebilir parametrelerle gelişmiş arama tekniklerini kullanın.

#### Doğrudan Cevap
`SearchOptions` nesnesi oluşturan, `UseFuzzySearch`, `Highlight` ve `PageSize` özelliklerini ayarlayan ve ardından `SearchNetwork.QueryAdvanced` metoduna geçiren bir yöntem uygulayın. Bu, sayfalı, vurgulanmış sonuçları bulanık eşleşme etkinleştirilmiş şekilde üretir.  
`SearchNetwork.QueryAdvanced`, bulanık eşleşme ve sayfalama gibi gelişmiş seçeneklerle bir sorgu çalıştıran bir yöntemdir.

#### Adım 1: Gelişmiş Arama Yöntemini Uygula  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### PDF Dosyalarına Redaction Uygulama

#### Genel Bakış
PDF içeriğini depolanmadan veya paylaşılmadan önce redaction uygulayarak hassas bilgileri güvence altına alın.

#### Doğrudan Cevap
`Redactor` örneği oluşturun, hedef PDF'yi yükleyin, bir `RedactionPattern` (ör. SSN regex) tanımlayın, `redactor.Apply(pattern)` metodunu çağırın ve sonunda redaction uygulanmış belgeyi kaydedin. Bu süreç, kişisel verilerin kalıcı olarak kaldırılmasını sağlar.

#### Tanım Bağlantısı
`Redactor`, GroupDocs.Redaction içinde belgeleri işleyen ve redaction kurallarını uygulayan birincil sınıftır.

#### Örnek İş Akışı (yeni kod bloğu yok)  
1. Lisansınızla `Redactor`'ı başlatın.  
2. `redactor.Load("sample.pdf")` kullanarak PDF'yi yükleyin.  
3. `RedactionPattern`, redaction uygulanacak metin veya deseni belirten bir kuralı temsil eder. `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")` gibi desenler tanımlayın.  
4. `redactor.Apply(pattern)` metodunu çalıştırın.  
5. `redactor.Save("sample_redacted.pdf")` ile çıktıyı kaydedin.

### Pratik Uygulamalar

#### Gerçek Dünya Kullanım Durumları
1. **Legal Document Management** – Sözleşmeleri verimli bir şekilde arayın ve müşteri tanımlayıcılarını otomatik olarak redaction uygulayın.  
2. **Healthcare Records** – Hasta notlarını bulun ve HIPAA uyumlu PHI redaction'ı sağlayın.  
3. **Corporate Compliance** – İç iletişimleri yasaklı terimler için tarayın ve arşivlemeden önce redaction uygulayın.

## Sonuç
Bu rehber, **creating a search index .NET** çözümünün ölçeklenebilir, hızlı indekslenen ve redaction ile veriyi koruyan kapsamlı bir yol haritasını sunar. Düğümleri yapılandırarak, belgeleri indeksleyerek, gelişmiş arama özelliklerinden yararlanarak ve redaction uygulayarak, geliştiriciler belge yönetim iş akışlarını büyük ölçüde iyileştirebilir ve katı güvenlik standartlarını sürdürebilir.

## Sıkça Sorulan Sorular

**S: .NET'te GroupDocs ile dağıtılmış bir arama ağı nasıl kurulur?**  
C: Temel bir yol ve port tanımlayın, ardından `SearchNetworkDeployment.Deploy()` metodunu çağırarak makineler arasında ana ve işçi düğümleri başlatın.

**S: GroupDocs'ta birden fazla parametreyle gelişmiş aramalar yapabilir miyim?**  
C: Evet—tek bir sorguda bulanık eşleşme, joker karakter desteği ve sonuç vurgulamasını birleştirmek için `SearchOptions` kullanın.

**S: Ana düğümde ağ etkinliğini izlemek mümkün mü?**  
C: Kesinlikle—gerçek zamanlı içgörüler için `IndexingCompleted` ve `QueryExecuted` gibi `SearchNetworkNodeEvents`'e abone olun.

**S: GroupDocs kullanarak PDF dosyalarına redaction nasıl uygulanır?**  
C: Bir `Redactor` başlatın, PDF'yi yükleyin, `RedactionPattern` nesneleri (regex veya literal string) tanımlayın, `Apply` metodunu çağırın ve temizlenmiş belgeyi kaydedin.

**S: Ağ ortamında arama performansını artırmanın en kolay yolu nedir?**  
C: Sorgulardan önce belge setinizi tamamen indeksleyin, düğümleri paralel işlem için dağıtın ve önbellekleme ve sayfalama için `SearchOptions`'ı ayarlayın.

---

**Son Güncelleme:** 2026-06-12  
**Test Edilen Versiyonlar:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [GroupDocs.Search ile .NET Belge İndeksleme&#58; Kapsamlı Bir Rehber](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [GroupDocs.Redaction .NET ile Belge İndeksleme ve Gelişmiş Arama Sorguları](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [.NET'te GroupDocs Search ve Redaction'ı Ustalıkla Kullanma&#58; Gelişmiş Belge Yönetimi](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)