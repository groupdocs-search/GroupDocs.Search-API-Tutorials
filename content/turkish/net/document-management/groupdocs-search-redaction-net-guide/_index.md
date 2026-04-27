---
date: '2026-04-27'
description: GroupDocs.Search ve Redaction kullanarak .NET'te hassas verileri nasıl
  karartacağınızı öğrenin ve büyük belgeleri aramak için belgeleri indekse nasıl ekleyeceğinizi
  keşfedin.
keywords:
- redact sensitive data
- add documents to index
- search large documents
title: GroupDocs.Search ve Redaction .NET'te – hassas verileri gizle
type: docs
url: /tr/net/document-management/groupdocs-search-redaction-net-guide/
weight: 1
---

# GroupDocs.Search & Redaction in .NET – hassas verileri gizleme

Büyük miktarda belgeyi yönetmek zorlayıcı olabilir, özellikle **hassas verileri gizleme** ihtiyacınız olduğunda ve hâlâ hızlı arama yetenekleri sunmanız gerektiğinde. Bu rehberde GroupDocs.Search'i GroupDocs.Redaction ile birlikte kurmayı, **belgeleri indekse ekle** nasıl yapılacağını gösterecek, verimli **büyük belgeleri ara** işlemlerini gerçekleştirecek ve her şeyi gizlilik gereksinimlerine uygun tutacağız.

## Hızlı Yanıtlar
- **“hassas verileri gizleme” ne anlama geliyor?** Bu, belgelerden gizli bilgileri kalıcı olarak kaldırmak veya maskelemek anlamına gelir.
- **Hangi kütüphanelere ihtiyacım var?** GroupDocs.Search ve GroupDocs.Redaction for .NET (NuGet üzerinden temin edilebilir).
- **.NET projelerini otomatik olarak indeksleyebilir miyim?** Evet – adım adım rehberlik için “How to index .NET” bölümüne bakın.
- **Büyük dosyalarla nasıl başa çıkabilirim?** Verileri yönetilebilir parçalar halinde işlemek için parça‑temelli aramayı kullanın.
- **Üretim için lisans gerekli mi?** Üretim kullanımında geçerli bir GroupDocs lisansı gereklidir; ücretsiz denemeler mevcuttur.

## Hassas verileri gizleme nedir?
Hassas verileri gizleme, kişisel, finansal veya sınıflandırılmış bilgileri bir belgeden kalıcı olarak kaldırma veya gizleme sürecidir; böylece bu bilgiler yetkisiz kullanıcılar tarafından geri getirilemez veya görüntülenemez.

## Neden GroupDocs.Search ile Redaction'ı birleştirmelisiniz?
- **Hız:** Milisaniyeler içinde sonuç döndüren aranabilir indeksler oluşturun.  
- **Güvenlik:** Belgeler paylaşılmadan veya depolanmadan önce gizleme kurallarını uygulayın.  
- **Ölçeklenebilirlik:** Parça arama, belleği tüketmeden terabaytlarca metinle çalışmanıza olanak tanır.  
- **Uyumluluk:** Gizli verilerin asla sızmamasını sağlayarak GDPR, HIPAA ve diğer düzenlemelere uyun.

## Önkoşullar
- .NET geliştirme ortamı (Visual Studio önerilir).  
- Temel C# bilgisi.  
- Gerekli paketleri kurmak için NuGet erişimi.

## GroupDocs.Redaction'ı .NET için Kurma

### Kurulum .NET CLI aracılığıyla
```bash
dotnet add package GroupDocs.Redaction
```

### Package Manager Kurulumu
```powershell
Install-Package GroupDocs.Redaction
```

### NuGet Paket Yöneticisi UI
**"GroupDocs.Redaction"** aratın ve en son sürümü kurun.

### Lisans Edinme Adımları
- **Ücretsiz Deneme:** Özellikleri keşfetmek için ücretsiz deneme ile başlayın.  
- **Geçici Lisans:** Uzun süreli erişim için geçici lisans isteyin.  
- **Satın Alma:** Uzun vadeli üretim kullanımı için satın almayı düşünün.

### Temel Başlatma ve Kurulum
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## Uygulama Kılavuzu

### GroupDocs.Search ile .NET projelerini nasıl indekslersiniz
Aşağıda uygulamayı net, numaralı adımlara bölüyoruz, böylece kolayca takip edebilirsiniz.

#### Adım 1: İndeks Klasörünü Belirleyin
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*Neden?* Ayrı bir klasör tanımlamak, indeksinizi düzenli tutar ve ham belgelere karşı izole eder.

#### Adım 2: İndeksi Oluşturun ve Yapılandırın
```csharp
Index index = new Index(indexFolder);
```
*Amaç:* Tanımladığınız konumda yeni bir aranabilir indeks oluşturur.

#### Adım 3: **Belgeyi indekse ekle**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*Açıklama:* Her çağrı, bir dosyayı (veya klasörü) indekse ekler ve içeriğinin aranabilir olmasını sağlar.

### Parça Arama ile Büyük Belgeleri Ara
Parça arama, büyük dosyaları daha küçük parçalara bölmenizi sağlar ve bellek kullanımını düşük tutar.

#### Adım 1: Arama Sorgusunu Tanımlayın
```csharp
string query = "invitation";
```
*Amaç:* Tüm indekslenmiş dosyalarda aradığınız terim.

#### Adım 2: Parça Arama Seçeneklerini Yapılandırın
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*Açıklama:* `IsChunkSearch` özelliğini etkinleştirmek, motorun verileri parçalara ayırarak işlemesini sağlar.

#### Adım 3: İlk Aramayı Gerçekleştir
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*Sonuç:* Terimi içeren belge sayısını ve toplam kaç kez bulunduğunu gösterir.

#### Adım 4: Sonraki Parçalarla Devam Et
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*Neden bu döngü?* Tüm veri kümesi işlenene kadar her parçadan sonuç almanızı sağlar.

### GroupDocs.Redaction ile hassas verileri nasıl gizlersiniz
Korumanız gereken bilgiyi bulduktan sonra, gizleme kurallarını uygulayın.

#### Adım 1: Gizleme Ayarlarını Başlat
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### Adım 2: Gizlemeleri Uygula
`Redactor` sınıfını (orijinal kodu korumak için burada gösterilmemiştir) maskelemek istediğiniz desenleri, metinleri veya resimleri tanımlamak için kullanın.  
*İpucu:* Kazara veri kaybını önlemek için gizleme kurallarınızı önce belgenin bir kopyasında test edin.

## Pratik Uygulamalar
Bu yetenekler birçok sektörde öne çıkar:

1. **Legal Document Management** – Dava dosyalarını hızlıca arayın ve müşteri‑gizli detayları gizleyin.  
2. **Healthcare Data Handling** – Hasta PHI'sını koruyun ve klinisyenlerin ilgili kayıtları bulmasına izin verin.  
3. **Financial Auditing** – Büyük işlem günlüklerini indeksleyin ve hesap numaralarını ya da kişisel tanımlayıcıları gizleyin.

## Performans Hususları
- **İndekslemeyi Optimize Et:** Gereksiz iş yükü olmadan indeksi güncel tutmak için yalnızca değişen dosyaları yeniden indeksleyin.  
- **Kaynakları Yönet:** Sunucunuzun RAM'ine göre parça boyutlarını (`options.ChunkSize`) ayarlayın.  
- **Asenkron İşlemler:** Büyük toplular için UI'nizin yanıt vermesini sağlamak amacıyla asenkron indeksleme kullanın.

## Sık Sorulan Sorular

**S: Büyük dosyaları verimli bir şekilde nasıl yönetirim?**  
A: Verileri daha küçük parçalar halinde işlemek ve bellek baskısını azaltmak için parça‑temelli aramaları (`IsChunkSearch = true`) kullanın.

**S: GroupDocs.Redaction şifreli belgelerle çalışabilir mi?**  
A: Evet – önce dosyanın şifresini çözün, gizlemeyi uygulayın ve gerekirse yeniden şifreleyin.

**S: Hangi lisans seçenekleri mevcuttur?**  
A: Ücretsiz deneme, değerlendirme için geçici lisans ve üretim için tam ticari lisanslar.

**S: İndeks hatalarını nasıl gideririm?**  
A: İndeks klasör yolunun doğru olduğunu doğrulayın, uygulamanın okuma/yazma izinlerine sahip olduğundan emin olun ve tüm belge formatlarının desteklendiğini kontrol edin.

**S: Arama sorgularını daha da özelleştirmek mümkün mü?**  
A: Kesinlikle. `SearchOptions` API'sini kullanarak Boolean operatörlerini, joker karakterleri ve yakınlık aramalarını birleştirebilirsiniz.

## Kaynaklar
- **Dokümantasyon:** [GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **API Referansı:** [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)  
- **İndirme:** [Latest Releases](https://releases.groupdocs.com/search/net/)  
- **Ücretsiz Destek:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans:** [Request Here](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-04-27  
**Test Edilen:** GroupDocs.Search 23.9 and GroupDocs.Redaction 23.9 for .NET  
**Yazar:** GroupDocs