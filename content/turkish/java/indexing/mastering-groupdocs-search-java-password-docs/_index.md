---
date: '2026-10-28'
description: GroupDocs.Search kullanarak Java'da birden fazla file types aramayı ve
  password‑protected documents için searchable index oluşturmayı öğrenin. Adım adım
  rehber, code, tips ve performance tricks.
keywords:
- search multiple file types
- build searchable index
- password protected document indexing java
- groupdocs.search java api
lastmod: '2026-10-28'
og_description: GroupDocs.Search kullanarak Java'da birden fazla file types aramayı
  ve password‑protected documents için searchable index oluşturmayı öğrenin. Adım
  adım rehber, code, tips ve performance tricks.
og_image_alt: Guide showing Java code to search multiple file types and index password‑protected
  documents with GroupDocs.Search
og_title: Java'da birden fazla file types arama ve docs indeksleme
schemas:
- author: GroupDocs
  dateModified: '2026-10-28'
  description: Learn how to search multiple file types and build a searchable index
    for password‑protected documents in Java using GroupDocs.Search. Step‑by‑step
    guide with code, tips, and performance tricks.
  headline: How to search multiple file types and index docs in Java
  type: TechArticle
- questions:
  - answer: GroupDocs.Search supports 120+ formats including PDF, DOCX, XLSX, PPTX,
      and common image types. Install format plugins if required.
    question: How do I handle different file formats?
  - answer: The document is skipped and a warning is logged; verify your password
      dictionary or event handler.
    question: What happens if a password is wrong?
  - answer: Yes, but they must be downloaded to a local temporary folder first because
      the engine works with file‑system paths.
    question: Can I index files stored in the cloud?
  - answer: Adjust scoring with `IndexOptions`, add synonyms, and use advanced query
      syntax such as `field:term~` for fuzzy matching. `IndexOptions` is a configuration
      object that controls scoring and indexing behavior.
    question: How can I improve search relevance?
  - answer: Review the log output; common causes are missing passwords, corrupted
      files, or unsupported formats.
    question: What should I do if indexing fails for some files?
  type: FAQPage
tags:
- search multiple file types
- GroupDocs.Search
- Java indexing
- password‑protected docs
- document search
title: Java'da birden fazla file types arama ve docs indeksleme
type: docs
url: /tr/java/indexing/mastering-groupdocs-search-java-password-docs/
weight: 1
---

# Java'da birden çok dosya türünü arama ve belgeleri indeksleme

Modern işletmelerde genellikle **birden fazla dosya türünü arama** ihtiyacı duyarsınız ve gizli dosyaları şifrelerin arkasında kilitli tutarsınız. Bu öğretici, GroupDocs.Search kullanarak Java'da şifre korumalı belgeler için aranabilir bir indeks oluşturmanın yolunu gösterir. Şifre sözlüğünü nasıl yapılandıracağınızı, şifre‑gerektiren olayları nasıl ele alacağınızı ve büyük partiler için performansı nasıl optimize edeceğinizi göreceksiniz — tüm bunlar özel bir şifre çözme kodu yazmadan.

## Hızlı cevaplar
- **Bu öğretici neyi kapsıyor?** Şifre sözlüğü ve bir olay dinleyicisi ile şifre korumalı belgelerin indekslenmesi.  
- **Hangi kütüphane gerekli?** GroupDocs.Search for Java (en son sürüm).  
- **Lisans gerekiyor mu?** Değerlendirme için geçici ücretsiz deneme lisansı mevcuttur.  
- **Diğer dosya türlerini indeksleyebilir miyim?** Evet, GroupDocs.Search PDF, DOCX, XLSX, PPTX ve görüntüler dahil 120+ formatı destekler.  
- **Hangi Java sürümü gerekiyor?** JDK 8 veya üzeri.  

## “create document index java” nedir?

`create document index java` terimi, Java tarafından yönetilen dosyaların konumlarına terimleri eşleyen aranabilir bir veri yapısı oluşturma sürecini ifade eder. GroupDocs.Search ile motor, şifreli PDF'ler, Office belgeleri ve görüntüler dahil desteklenen formatlardan metni otomatik olarak çıkarır; böylece kendi şifre çözme kodunuzu yazmadan tam metin aramaları yapabilirsiniz. Bu yaklaşım, belge güvenliğini korurken arama uygulamasını basitleştirir.

## Şifre korumalı dosyalar için GroupDocs.Search neden kullanılmalı?

GroupDocs.Search, bir sözlükten veya bir olay işleyicisinden şifreleri uygulayan sıfır‑dokunma açma mekanizması sağlar; böylece şifreli dosyaları tek bir geçişte indeksleyebilirsiniz. Standart 8‑çekirdekli bir sunucuda saatte 2 milyon belge işleyebilir, 120+ dosya türünü destekler ve Boolean, wildcard ve fuzzy operatörleri içeren zengin bir sorgu dili sunar — çeşitli içeriklerde aranabilir bir indeks oluşturmak için gereklidir.

## Önkoşullar
- Java Development Kit (JDK) 8+ yüklü ve `PATH`'inize eklenmiş.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Bağımlılık yönetimi için Maven.  
- GroupDocs.Search for Java – kütüphaneyi Maven aracılığıyla ekleyin (kurulum bölümüne bakın).  

## GroupDocs.Search for java'yı kurma

### Maven Kullanarak
Depoyu ve bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

### Doğrudan indirme
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden indirebilirsiniz.

Deneme lisansı ile başlamak için [GroupDocs'un geçici lisans sayfasını](https://purchase.groupdocs.com/temporary-license/) ziyaret edin ve ücretsiz denemenizi almak için talimatları izleyin.

## Şifre sözlüğü ile belgeleri indeksleme

Bir dosya yolu ile şifrelerini eşleştiren bir sözlük sağlayarak **aranabilir bir indeks oluşturabilirsiniz**. Motor, indeksleme sırasında doğru şifreyi otomatik olarak alacaktır.

### Genel Bakış
Belge şifrelerini basit bir anahtar‑değer haritasında saklayın, böylece indeksleme motoru dosyaları gerektiğinde açabilir.

### Adım 1: indeks ve belgeler klasörünü tanımlayın
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordDictionary";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Adım 2: bir indeks oluşturun
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Adım 3: belge şifrelerini ekleyin
```java
// Add passwords for specific files using their absolute paths
String path1 = new File(documentsFolder + "/English.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path1, "123456");

String path2 = new File(documentsFolder + "/SampleDocument.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path2, "123456");
```

### Adım 4: belgeleri indeksleyin
```java
// Automatically retrieve passwords from the dictionary during indexing
index.add(documentsFolder);
```

### Adım 5: indeks içinde arama yapın
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

**İpucu:** Üretim senaryoları için şifreleri sabit kodlamak yerine güvenli bir kasadan (ör. Azure Key Vault veya AWS Secrets Manager) yükleyin.

#### Sorun Giderme
- Her şifrenin dosyanın gerçek koruma şifresiyle eşleştiğini doğrulayın.  
- Dosya yollarını iki kez kontrol edin; hatalı bir yol `FileNotFoundException` hatasına neden olur.

## Şifre gereksinimi için bir olay dinleyicisiyle belgeleri indeksleme

Motor bir şifre‑gerektiren olay tetiklediğinde yalnızca şifreleri sağlayabilirsiniz, böylece kimlik bilgileri bellekte tutulmaz ve dinamik şifre çözümlemesi sağlanır.

Motor şifreli bir dosyayla karşılaştığında, güvenli bir depodan şifreyi alabileceğiniz veya anlık olarak hesaplayabileceğiniz bir geri çağırma tetikler. Bu yöntem, tüm şifreleri bir sözlükte saklamaya kıyasla saldırı yüzeyini azaltır.

### Genel Bakış
Şifreleri olay geri çağırmasıyla anlık olarak sağlayın, kimlik bilgisi depolamanızı izole tutun.

### Adım 1: indeks ve belgeler klasörünü tanımlayın
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordEvent";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Adım 2: bir indeks oluşturun
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Adım 3: şifre‑gerektiren olaya abone olun
```java
index.getEvents().PasswordRequired.add(new EventHandler<PasswordRequiredEventArgs>() {
    @Override
    public void invoke(Object sender, PasswordRequiredEventArgs args) {
        // Provide password for DOCX files when needed
        if (args.getDocumentFullPath().endsWith(".docx")) {
            args.setPassword("123456");
        }
    }
});
```

### Adım 4: belgeleri indeksleyin
```java
// The event handler will supply passwords as required during indexing
index.add(documentsFolder);
```

### Adım 5: indeks içinde arama yapın
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

#### Sorun Giderme
- Olay işleyicisinin indekslemeniz gereken tüm dosya uzantılarını kapsadığından emin olun.  
- Şifrenin uygulandığını doğrulamak için önce birkaç örnek dosyayla test edin.

## Pratik uygulamalar

1. **Enterprise document management** – gizli sözleşmeler, İK dosyaları ve finansal raporların indekslenmesini otomatikleştirin, aynı zamanda dinlenirken şifreli kalmalarını sağlayın.  
2. **Legal archives** – hassas içeriği ortaya çıkarmadan dava dosyalarını hızlıca bulun.  
3. **Healthcare records** – HIPAA gereksinimlerine uygun olarak hasta PDF'lerini ve Word belgelerini indeksleyin.

## Performans Hususları

- **Memory allocation** – büyük partiler için yeterli yığın belleği (`-Xmx2g` veya daha yüksek) ayırın.  
- **Parallel indexing** – `index.addAsync(...)` kullanın veya birden fazla indeksleme iş parçacığı çalıştırarak 8‑çekirdekli bir makinede saatte **2 milyon belge** hedefine ulaşın. `index.addAsync(...)` asenkron indeksleme için belgeleri kuyruğa ekleyen bir yöntemdir.  
- **Index maintenance** – indeksin sıkıştırılması ve sorgu hızının artırılması için periyodik olarak `index.optimize()` çağırın.

## Yaygın sorunlar ve çözümler

- **Wrong password** – belge atlanır ve bir uyarı kaydedilir. Şifre kaynağınızı iki kez kontrol edin.  
- **Unsupported format** – gerekli format eklentilerini kurun veya indekslemeden önce dosyaları desteklenen bir tipe dönüştürün.  
- **Large files** – yığın boyutunu artırın ve `OutOfMemoryError` hatasından kaçınmak için dosyaları daha küçük partiler halinde indekslemeyi düşünün.

## Sıkça Sorulan Sorular

**S: Farklı dosya formatlarıyla nasıl başa çıkabilirim?**  
C: GroupDocs.Search PDF, DOCX, XLSX, PPTX ve yaygın görüntü türleri dahil 120+ formatı destekler. Gerekirse format eklentilerini kurun.

**S: Şifre yanlış olduğunda ne olur?**  
C: Belge atlanır ve bir uyarı kaydedilir; şifre sözlüğünüzü veya olay işleyicinizi doğrulayın.

**S: Bulutta depolanan dosyaları indeksleyebilir miyim?**  
C: Evet, ancak motor dosya‑sistemi yolları ile çalıştığı için önce yerel geçici bir klasöre indirilmeleri gerekir.

**S: Arama alaka düzeyini nasıl artırabilirim?**  
C: `IndexOptions` ile puanlamayı ayarlayın, eşanlamlılar ekleyin ve `field:term~` gibi gelişmiş sorgu sözdizimini fuzzy eşleşme için kullanın. `IndexOptions` puanlama ve indeksleme davranışını kontrol eden bir yapılandırma nesnesidir.

**S: Bazı dosyalar için indeksleme başarısız olursa ne yapmalıyım?**  
C: günlük çıktısını inceleyin; yaygın nedenler eksik şifreler, bozuk dosyalar veya desteklenmeyen formatlardır.

## Kaynaklar
- [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

Bu rehberi izleyerek artık **birden fazla dosya türünü arama** ve **Java'da şifre korumalı belgeleri indeksleme** konusunda bilgi sahibisiniz; bu da uygulamalarınızda güvenliği ve keşfedilebilirliği artırır.

---

**Son Güncelleme:** 2026-10-28  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [How to index password‑protected documents in Java using GroupDocs.Search](/search/java/indexing/mastering-groupdocs-search-java-password-docs/)
- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)