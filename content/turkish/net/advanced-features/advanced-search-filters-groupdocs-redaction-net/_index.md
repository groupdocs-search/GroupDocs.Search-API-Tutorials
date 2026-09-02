---
date: '2026-04-02'
description: GroupDocs.Redaction for .NET ile dosya uzantısına göre filtrelemeyi ve
  yalnızca txt dosyalarını aramayı öğrenin—belge yönetimi verimliliğini artırın.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: .NET'te GroupDocs.Redaction kullanarak dosya uzantısına göre filtreleme
type: docs
url: /tr/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# .NET'te GroupDocs.Redaction kullanarak dosya uzantısına göre filtreleme

Massif bir dosya koleksiyonunda arama yapmak bunaltıcı olabilir, özellikle yalnızca belirli dosya türlerinden sonuçlara ihtiyacınız olduğunda. Bu öğreticide **dosya uzantısına göre nasıl filtreleneceğini** GroupDocs.Redaction for .NET ile keşfedecek, sadece txt dosyalarını ya da seçtiğiniz başka bir uzantıyı arayabileceksiniz. Dosya‑tipi ve yol‑tabanlı filtrelerin nasıl kurulacağını adım adım gösterecek, böylece ihtiyacınız olan belgeleri hızlıca bulabileceksiniz.

## Hızlı Yanıtlar
- **“filter by file extension” ne yapar?** Bir aramayı verilen dosya uzantısına (ör. *.txt) uyan belgelere sınırlar.  
- **Bunun için neden GroupDocs.Redaction kullanılmalı?** Hızlı ve kolay entegre edilebilen yerleşik filtreleme API'leri sağlar.  
- **Bir lisansa ihtiyacım var mı?** Ücretsiz deneme testi için çalışır; üretim için ücretli lisans gereklidir.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Dosya tipi ve yol filtrelerini birleştirebilir miyim?** Evet—çok hassas aramalar için birden fazla filtre uygulayabilirsiniz.

## Öğrenecekleriniz
- Sadece metin dosyalarının aranmasını sağlayacak **dosya uzantısına göre filtreleme** nasıl yapılır.  
- **dosya yolu filtreleri** nasıl ayarlanır, sonuçları belirli klasörlere veya adlandırma desenlerine daraltır.  
- Dizinizi hızlı ve bellek‑verimli tutmak için ipuçları.

## Ön Koşullar

Aramaya başlamadan önce şunların kurulu olduğundan emin olun:

- **GroupDocs.Redaction Kütüphanesi** yüklü ve .NET projenizle uyumlu olduğundan emin olun.  
- Visual Studio veya VS Code gibi bir geliştirme ortamı.  
- Temel C# bilgisi ve .NET proje yapısına aşinalık.

## .NET için GroupDocs.Redaction Kurulumu

İlk olarak, kütüphaneyi projenize ekleyin.

**.NET CLI Kullanarak:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Paket Yöneticisi Kullanarak:**  
```bash
Install-Package GroupDocs.Redaction
```

Veya NuGet Paket Yöneticisi UI'de “GroupDocs.Redaction”ı bulun ve en son sürümü yükleyin.

### Lisans Alımı

Ücretsiz deneme ile başlayabilir veya geçici bir lisans talep edebilirsiniz. Uzun vadeli projeler için resmi siteden lisans satın alın.

### Temel Başlatma

Paket yüklendikten sonra, belgelerinize referans tutacak bir indeks oluşturun:  
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Uygulama Kılavuzu

### Özellik 1: Metin belgeleri (.txt) için filtre ayarlama

#### Metin belgeleri için dosya uzantısına göre nasıl filtreleme yapılır

1. **Dizin ve belge klasörlerini tanımlayın**  
   Kaynak dosyalarınızın bulunduğu yolları ayarlayın:  
   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Bir Dizin Oluşturun**  
   Kaynak klasörden tüm dosyaları dizine yükleyin:  
   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Dosya uzantısı filtresi ile Arama Seçeneklerini yapılandırın**  
   Motoru sadece *.txt dosyalarını dikkate alması için söyleyin:  
   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Aramayı gerçekleştir**  
   Bir sorgu çalıştırın; filtre metin dışı dosyaların göz ardı edilmesini sağlar:  
   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Açıklama*: `Search` yöntemi, filtreyi karşılayan eşleşmeleri döndürür, gürültüyü büyük ölçüde azaltır ve performansı artırır.

### Özellik 2: DosyaYolu Filtreleri

#### Neden dosya yolu filtreleri kullanılır?

Bazen aramaları belirli bir departman klasörüne veya ortak bir adlandırma kuralına sahip dosyalara sınırlamanız gerekir. Yol filtreleri tam da bunu yapmanızı sağlar.

1. **Dizin ve belge klasörlerini tanımlayın**  
   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Bir Dizin Oluşturun**  
   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Yol‑tabanlı düzenli ifade ile Arama Seçeneklerini yapılandırın**  
   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Bu düzenli ifade, tam yolu içinde “Lorem” kelimesi geçen tüm dosyaları eşleştirir, böylece belirli alt‑klasörleri hedefleyebilirsiniz.

4. **Yol‑tabanlı aramayı yürütün**  
   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Pratik Uygulamalar
- **Hukuki Belge Yönetimi** – Düz metin dosyaları olarak saklanan ilgili sözleşmeleri hızlıca bulun.  
- **Akademik Araştırma** – Belirli bir proje klasörüne ait sadece *.txt araştırma notlarını çekin.  
- **Kurumsal Raporlama** – İç raporları departman yoluna göre filtreleyin (ör. `/Finance/2025/`).  

## Performans Hususları
- Yalnızca gerçekten ihtiyaç duyduğunuz belge tiplerini indeksleyin; gereksiz dosyalar dizin boyutunu ve arama süresini artırır.  
- Yeni veya değişen dosyalar için `index.Add()` çağıran planlanmış bir iş ile dizininizi güncel tutun.  
- Basit düzenli ifadeler kullanın; aşırı karmaşık desenler arama motorunu yavaşlatabilir.  
- Artık ihtiyaç duyulmadığında `Index` nesnelerini serbest bırakarak belleği boşaltın.

## Sonuç
Artık GroupDocs.Redaction for .NET kullanarak **dosya uzantısına göre filtreleme** ve **dosya yolu filtreleri** uygulamayı biliyorsunuz. Bu teknikler, büyük belge koleksiyonları üzerinde ayrıntılı kontrol sağlar, aramaları daha hızlı ve daha ilgili hâle getirir. Sonraki adımda, birden fazla filtreyi birleştirerek ya da aramayı daha büyük bir uygulama iş akışına entegre ederek deneyler yapabilirsiniz.

## SSS Bölümü

**S1: Metin dosyaları dışındaki belgeleri filtreleyebilir miyim?**  
A1: Evet, GroupDocs.Redaction birçok formatı destekler. `CreateFileExtension` içindeki argümanı istediğiniz uzantıya (ör. ".pdf") değiştirin.

**S2: Arama dizinimi düzenli olarak nasıl güncellerim?**  
A2: `index.Add()`'ı çalıştıran bir arka plan servisi veya cron işi planlayarak, güncel tutmak istediğiniz dizinlerde çalıştırın.

**S3: Dosya yoluna göre filtreleme performansı etkiler mi?**  
A3: İyi optimize edilmiş düzenli ifadeler minimal etki yapar, ancak her zaman kendi veri setinizle performans testi yapın.

**S4: Daha hassas aramalar için birden fazla filtreyi birleştirebilir miyim?**  
A4: Kesinlikle. Filtreleri zincirleyebilir veya birleşik filtreler oluşturarak hem dosya tipi hem de yolu aynı anda hedefleyebilirsiniz.

**S5: GroupDocs.Redaction hakkında daha fazla kaynağa nereden ulaşabilirim?**  
A5: Detaylı kılavuzlar ve API referansları için resmi dokümantasyona [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) adresinden göz atın.

## Sıkça Sorulan Sorular

**S: `SearchDocumentFilter` şifreli dosyalarla çalışır mı?**  
A: Filtre, dosya meta verileri üzerinde çalışır, bu yüzden indeksleme sırasında gerekli şifre çözme kimlik bilgilerini sağlarsanız şifreli dosyalar da indekslenir.

**S: Yol filtresi için düzenli ifade yerine joker karakter (*) kullanabilir miyim?**  
A: API şu anda bir düzenli ifade gerektirir, ancak basit joker karakterleri (ör. `.*` herhangi bir karakter için) taklit edebilirsiniz.

**S: Sharding düşünmeden önce indeks ne kadar büyük olabilir?**  
A: Birkaç yüz gigabaytlık indeksler, birden fazla mantıksal indekse bölünerek fayda sağlayabilir; koleksiyonunuz büyüdükçe performansı test edin.

**S: İndeksten belgeleri kaldırmak için yerleşik yöntemler var mı?**  
A: Evet—`index.Delete(documentId)` veya `index.DeleteAll()` çağırarak eski girişleri yönetebilirsiniz.

**S: Tam belgeyi yüklemeden önce arama sonuçlarını önizlemek mümkün mü?**  
A: `SearchResult` nesnesi, tüm dosyayı açmadan UI'da gösterebileceğiniz snippet bilgilerini içerir.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API Referansı**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **İndirme**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Ücretsiz Destek**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Geçici Lisans**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---
**Son Güncelleme:** 2026-04-02  
**Test Edilen Versiyon:** GroupDocs.Redaction 23.12 for .NET  
**Yazar:** GroupDocs