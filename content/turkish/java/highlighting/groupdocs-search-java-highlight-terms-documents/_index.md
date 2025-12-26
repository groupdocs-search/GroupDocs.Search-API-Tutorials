---
date: '2025-12-26'
description: GroupDocs.Search for Java kullanarak belgelerde metin aramayı ve vurgulamayı
  öğrenin. Tam belge ve parça vurgulama tekniklerini keşfedin.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Java için GroupDocs.Search ile Metin Arama ve Vurgulama
type: docs
url: /tr/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# GroupDocs.Search for Java Kullanarak Belgelerde Metin Arama ve Vurgulama

Günümüz dijital çağında, **metin arama ve vurgulama**, büyük belge koleksiyonları içinde yaygın bir gereksinimdir. Hukuki inceleme aracı, akademik araştırma portalı ya da müşteri‑destek panosu geliştiriyor olsanız da, anahtar terimleri anında bulup vurgulayabilmek kullanılabilirliği büyük ölçüde artırır. Bu kapsamlı rehberde, GroupDocs for Java ile **metin arama ve vurgulama** nasıl uygulanır, tam belge vurgulaması ve bağlam odaklı fragment‑seviyesi vurgulama nasıl yapılır öğrenebileceksiniz.

## Hızlı Yanıtlar
- **“Metin arama ve vurgulama” ne anlama geliyor?** Bir belge içinde sorgu terimlerini bulup görsel olarak (ör. arka plan rengiyle) vurgulamayı ifade eder.  
- **Bu yeteneği hangi kütüphane sağlıyor?** GroupDocs.Search for Java.  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme sürümü çalışır; üretim ortamı için tam lisans gerekir.  
- **Vurgulama renklerini özelleştirebilir miyim?** Evet—`HighlightOptions` aracılığıyla herhangi bir RGB rengi ayarlanabilir.  
- **Fragment (parça) vurgulama destekleniyor mu?** Kesinlikle; eşleşmenin öncesi/sonrası terimleri tanımlayarak kısa snippet’ler oluşturabilirsiniz.

## Metin Arama ve Vurgulama Nedir?
Metin arama ve vurgulama, bir sorgu için belge indeksini tarama, eşleşen belgeleri getirme ve ardından sorgu teriminin her geçtiği yeri belge çıktısında (HTML, PDF vb.) işaretleme sürecidir. Bu görsel ipucu, son kullanıcıların ilgili bilgiyi anında fark etmesini sağlar.

## Neden GroupDocs.Search for Java Kullanmalısınız?
- **Yüksek‑performanslı indeksleme** ve yapılandırılabilir sıkıştırma.  
- **Zengin vurgulama API’si**; hem bütün belgeler hem de özel fragment’ler üzerinde çalışır.  
- **Çoklu format desteği** (DOCX, PDF, PPTX, TXT ve daha fazlası).  
- **Kolay Maven entegrasyonu** ve net Java‑odaklı API.

## Ön Koşullar
- Java Development Kit (JDK) 8 veya daha yeni bir sürüm.  
- Bağımlılık yönetimi için Maven.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Java sözdizimine temel aşinalık.

## GroupDocs.Search for Java Kurulumu

`pom.xml` dosyanıza GroupDocs deposunu ve bağımlılığı ekleyin:

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

Ayrıca en yeni JAR dosyasını doğrudan resmi siteden indirebilirsiniz: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinimi
Ücretsiz deneme ile başlayın ya da değerlendirme için geçici bir lisans alın. Üretim dağıtımları için tüm özelliklerin kilidini açan tam lisansı satın alın.

## Uygulama Rehberi

Uygulama iki pratik bölüme ayrılmıştır: **tüm belgelerde vurgulama** ve **fragment’lerde vurgulama**. Her iki bölüm de GroupDocs.Search kullanarak **Java belgelerinde nasıl vurgulama yapılır** adımlarını içerir.

### İndeks Ayarlarını Yapılandırma
İndekslemeden önce, yüksek sıkıştırma kullanacak şekilde depolamayı yapılandırın—bu, disk kullanımını azaltırken arama hızını korur.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Tüm Belgelerde Vurgulama

#### Adım 1: İndeksi Oluşturun ve Doldurun
Arama yapmak istediğiniz tüm kaynak dosyaları ekleyerek bir indeks klasörü oluşturun.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Adım 2: Aramayı Gerçekleştirip Vurgulamayı Uygulayın
Terimi (ör. `ipsum`) arayın ve vurgulanmış eşleşmelerle bir HTML dosyası üretin.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Temel seçeneklerin açıklaması**
- **Compression** – yüksek sıkıştırma depolamayı tasarruflu kılar.  
- **HighlightColor** – UI paletinize uygun herhangi bir RGB değeri ayarlayın.  
- **UseInlineStyles** – `false` değeri, CSS ile global olarak stil verilebilen temiz HTML üretir.

### Fragment’lerde Vurgulama

#### Adım 1: İndeksleme ve Arama (yukarıdakiyle aynı)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Adım 2: Fragment Bağlamını Tanımlayın ve Vurgulayın
Her fragment içinde eşleşmenin öncesi ve sonrasında kaç terim gösterileceğini belirleyin.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Adım 3: Vurgulanan Fragment’leri Alın ve Yazın
Oluşturulan fragment’leri toplayıp bir HTML dosyasına yazın.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Pratik Uygulamalar
1. **Hukuki Belge İncelemesi** – kanun maddelerini, maddeleri veya dava referanslarını anında vurgulayın.  
2. **Akademik Araştırma** – onlarca PDF ve Word dosyası arasında anahtar terminolojiyi ortaya çıkarın.  
3. **Müşteri Desteği** – bilet geçmişinde sipariş numaralarını veya hata kodlarını hızlıca bulun.

## Performans Düşünceleri
- **İndeks Boyutu** – yüksek sıkıştırma (`Compression.High`) disk ayak izini azaltır.  
- **Fragment Bağlamı** – daha büyük `termsBefore/After` değerleri doğruluğu artırır ancak hızı etkileyebilir.  
- **Bellek Yönetimi** – büyük veri setlerini indekslerken JVM heap’ini izleyin; çok büyük koleksiyonlar için artımlı indekslemeyi değerlendirin.

## Yaygın Sorunlar ve Çözümler
- **İndeksleme Hataları** – dosya yollarını doğrulayın ve uygulamanın okuma/yazma izinlerine sahip olduğundan emin olun.  
- **Vurgulama Görünmüyor** – `UseInlineStyles` değerinin çıktınızın formatına (HTML vs. PDF) uygun olduğundan emin olun.  
- **Renk Uygulanmadı** – RGB değerlerinin 0‑255 aralığında olduğundan ve HTML görüntüleyicisinin stili desteklediğinden emin olun.

## Sıkça Sorulan Sorular

**S: GroupDocs.Search for Java kullanmanın avantajları nelerdir?**  
C: Hızlı, ölçeklenebilir indeksleme, özelleştirilebilir vurgulama ve çok sayıda belge formatı desteği sunar.

**S: GroupDocs.Search’u bir REST API ile nasıl entegre edebilirim?**  
C: Arama ve vurgulama metodlarını Spring Boot denetleyicileri aracılığıyla dışa aktarın; HTML ya da JSON payload döndürün.

**S: Kütüphane şifre‑korumalı dosyaları destekliyor mu?**  
C: Evet—belgeyi indekse eklerken şifreyi sağlayın.

**S: Vurgulama işaretlemesini renkten başka nasıl özelleştirebilirim?**  
C: `HighlightOptions` ile CSS sınıfları ekleyebilir veya HTML üretildikten sonra değiştirebilirsiniz.

**S: Bu rehber hangi sürümle test edildi?**  
C: Kod, GroupDocs.Search 25.4 sürümüyle doğrulandı.

---

**Son Güncelleme:** 2025-12-26  
**Test Edilen Sürüm:** GroupDocs.Search 25.4  
**Yazar:** GroupDocs