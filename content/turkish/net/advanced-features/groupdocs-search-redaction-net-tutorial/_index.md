---
date: '2026-04-04'
description: GroupDocs.Search kullanarak yasal belgeleri nasıl arayacağınızı ve indeksleri
  nasıl yöneteceğinizi öğrenin ve .NET'te GroupDocs.Redaction ile tıbbi kayıtlar için
  kırpma (redaction) entegrasyonu yapın.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: GroupDocs Search & Redaction for .NET ile Hukuki Belgeleri Arayın
type: docs
url: /tr/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# GroupDocs Search & Redaction ile .NET'te Hukuki Belgeleri Arayın

Bugünün veri‑odaklı ortamında, **hukuki belgeleri** hızlı ve güvenli bir şekilde aramak, herhangi bir kuruluş için kritik bir gereksinimdir. Sözleşmeler, mahkeme dosyaları veya uyum raporlarıyla ilgileniyor olun, GroupDocs.Search size hızlı, ölçeklenebilir bir indeks sağlar, GroupDocs.Redaction ise hassas bilgilerin gizli kalmasını sağlar. Bu öğretici, aranabilir bir indeks kurmayı, birden fazla klasörden belgeler eklemeyi ve redaksiyonu yapılandırmayı adım adım gösterir, böylece tıbbi kayıtları ve diğer gizli dosyaları güvenle arayabilirsiniz.

## Hızlı Yanıtlar
- **GroupDocs.Search ne yapar?** Geniş bir belge formatı yelpazesi için tam metin aranabilir bir indeks oluşturur.  
- **Aramadan önce bilgiyi redakte edebilir miyim?** Evet – hassas verileri maskelemek veya kaldırmak için GroupDocs.Redaction kullanın.  
- **İndekse belgeleri nasıl eklerim?** Her klasör için `index.Add("folderPath")` çağırın.  
- **Hangi dosya türleri destekleniyor?** PDF'ler, DOCX, PPTX, TXT ve daha fazlası.  
- **Üretim için lisansa ihtiyacım var mı?** Geçici bir deneme sürümü mevcuttur; ticari kullanım için kalıcı bir lisans gereklidir.

## Önkoşullar
- .NET Core SDK (3.1 veya üzeri) yüklü.
- .NET'i destekleyen Visual Studio Code, Visual Studio veya başka bir IDE.
- C# programlamaya temel aşinalık.

### Lisans Edinme
Her iki kütüphane için de ücretsiz bir deneme sürümüyle başlayabilirsiniz. Uzun vadeli kullanım için geçici bir lisans edinmeyi veya [GroupDocs web sitesinden](https://purchase.groupdocs.com/temporary-license/) satın almayı düşünün.

## Gerekli Paketlerin Kurulumu

**GroupDocs.Search Kurulumu:**  
**.NET CLI** kullanarak çalıştırın:
```bash
dotnet add package GroupDocs.Search
```
Alternatif olarak, Visual Studio'daki Package Manager Console'u kullanın:
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction Kurulumu:**  
- .NET CLI kullanın:
```bash
dotnet add package GroupDocs.Redaction
```
- Veya Package Manager üzerinden:
```powershell
Install-Package GroupDocs.Redaction
```

NuGet Package Manager UI'yi ziyaret edin ve GUI tercih ediyorsanız "GroupDocs.Redaction" aratarak kurun.

## Redaktör Ayarlarını Yapılandırma
Redaksiyona başlamadan önce, redaktör davranışını (ör. redaksiyon rengini ayarlamak veya özel desenler tanımlamak) ince ayar yapmak isteyebilirsiniz. Aşağıdaki kod parçası temel başlatmayı gösterir:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Pro ipucu:** `redactorSettings`'i kuruluşunuzun uyum politikalarına (ör. metni siyah kutularla değiştirmek, redaksiyondan önce OCR uygulamak vb.) göre ayarlayın.

## Uygulama Kılavuzu

### Hukuki Belgeler Nasıl Aranır?
Aranabilir bir indeks oluşturmak, hukuki belgelerin hızlı bir şekilde geri alınmasının temelidir. GroupDocs.Search herhangi bir klasöre işaret etmenizi, bir indeks oluşturmanızı ve ardından binlerce dosya üzerinde karmaşık sorgular yürütmenizi sağlar.

### Belgeler İndekse Nasıl Eklenir
Belgeleri eklemek basittir—kütüphaneyi dosyalarınızı içeren dizinlere yönlendirin. Birden fazla klasör ekleyebilirsiniz; bu, hukuki veri kümeniz farklı konumlarda dağıtıldığında kullanışlıdır.

#### Bir İndeks Oluşturma ve Yönetme
**Genel Bakış:**  
Bir indeks oluşturmak, verimli belge arama işlemlerine giden ilk adımdır. GroupDocs.Search istediğiniz herhangi bir dizinde aranabilir bir indeks oluşturmanıza olanak tanır, bu da belgelerin hızlı geri alınmasını sağlar.

##### Adım 1: İndeksi Oluşturun
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Açıklama:* `Index`, belirtilen dizinde bir arama indeksi başlatır. Yolun proje klasör yapınızı yansıttığından emin olun.

##### Adım 2: Belgeleri İndekse Eklemek
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Açıklama:* `Add` yöntemi verilen klasörü tarar ve desteklenen her belgeyi indekse ekler. Bunu, sözleşmeler, dava dosyaları veya tıbbi kayıtlar gibi birden çok kaynaktan **belgeleri indekse eklemek** için kullanın.

### İndeksleme Raporlarını Almak ve Görüntülemek
**Genel Bakış:**  
İndeksleme raporları, kaç belgenin işlendiği, toplam terim sayısı ve depolama boyutu gibi performans ayarı için gerekli metrikler hakkında bilgi verir.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Açıklama:* `GetIndexingReports`, indeksleme sürecini ayrıntılı olarak gösteren raporların bir dizisini döndürür; bu da performansı izlemeye ve optimize etmeye yardımcı olur.

## Pratik Uygulamalar
1. **Hukuki Belge Yönetimi:** Yasaların, özetlerin ve kararların anında geri alınması için dava dosyalarının indekslenmesini otomatikleştirin.  
2. **Tıbbi Kayıt Sistemi:** Hasta kayıtlarını ararken, PHI'yi maskelemek için GroupDocs.Redaction kullanarak gizliliği koruyun.  
3. **Kurumsal İK Portalı:** Kişisel verileri korumak için aranabilir çalışan dosyalarını redaksiyonla birleştirin.

## Performans Düşünceleri
- **İndeks Boyutunu Optimize Etme:** Periyodik olarak eski girdileri temizleyin ve indeksi yeniden oluşturun, böylece hafif kalır.  
- **Bellek Yönetimi:** .NET'in çöp toplayıcısını kullanın; `Index` nesnelerini artık ihtiyaç duyulmadığında serbest bırakın.  
- **Ölçeklenebilirlik En İyi Uygulamaları:** İndeksi hızlı SSD depolamada tutun ve büyük veri kümelerini birden fazla indeks arasında bölmeyi (sharding) düşünün.

## Sıkça Sorulan Sorular

**S: GroupDocs.Search'ün temel kullanım alanları nelerdir?**  
C: Büyük belge koleksiyonlarından aranabilir indeksler oluşturmak için idealdir; bu da hukuki ve tıbbi dosyaların hızlı geri alınmasını sağlar.

**S: GroupDocs.Redaction veri gizliliğini nasıl sağlar?**  
C: Belge indekslenmeden veya paylaşılmadan önce hassas bilgileri kalıcı olarak kaldıran veya maskeleyen redaksiyon desenleri tanımlamanıza olanak tanır.

**S: Bu kütüphaneleri bulut ortamında kullanabilir miyim?**  
C: Evet—her iki kütüphane de uygun lisansla Azure, AWS veya herhangi bir konteynerleştirilmiş .NET dağıtımında çalışır.

**S: GroupDocs.Search hangi dosya formatlarını destekler?**  
C: PDF'ler, Word, Excel, PowerPoint, TXT, HTML ve daha birçok kurumsal format.

**S: İndeksleme hatalarını nasıl gideririm?**  
C: Klasör yollarını doğrulayın, dosya izinlerini kontrol edin ve belirli hata kodları için `IndexingReport`'un konsol çıktısını inceleyin.

## Kaynaklar
- **Dokümantasyon:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API Referansı:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **İndirme:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Ücretsiz Destek:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Geçici Lisans:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Son Güncelleme:** 2026-04-04  
**Test Edilen Versiyon:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Yazar:** GroupDocs