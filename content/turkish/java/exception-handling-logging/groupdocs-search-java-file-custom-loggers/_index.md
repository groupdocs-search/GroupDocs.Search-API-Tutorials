---
date: '2025-12-24'
description: Log dosyası boyutunu sınırlamayı ve GroupDocs.Search for Java ile konsol
  kaydedicisini kullanmayı öğrenin. Bu kılavuz, günlük yapılandırmalarını, sorun giderme
  ipuçlarını ve performans optimizasyonunu kapsar.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: GroupDocs.Search Java Günlükçüleri ile günlük dosyası boyutunu sınırlayın
type: docs
url: /tr/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search Java Günlükçüleri ile Günlük Dosyası Boyutunu Sınırlama

Büyük belge koleksiyonlarını yönetirken verimli günlük tutma çok önemlidir, özellikle **log dosyası boyutunu sınırlamak** ve depolamayı kontrol altında tutmak gerektiğinde. **GroupDocs.Search for Java**, güçlü arama yetenekleriyle günlükleri yönetmek için sağlam çözümler sunar. Bu öğretici, GroupDocs.Search kullanarak dosya ve özel günlükçüler uygulamanıza rehberlik eder ve uygulamanızın olayları izleme ve sorunları ayıklama yeteneğini artırır.

## Quick Answers
- **“log dosyası boyutunu sınırlama” ne anlama geliyor?** Bir log dosyasının maksimum boyutunu sınırlar ve diskte kontrolsüz büyümeyi önler.  
- **Hangi günlükçü log dosyası boyutunu sınırlamanıza izin verir?** Yerleşik `FileLogger` bir maksimum‑boyut parametresi alır.  
- **Java’da console logger nasıl kullanılır?** `ConsoleLogger` örneği oluşturun ve `IndexSettings` üzerine ayarlayın.  
- **GroupDocs.Search için lisansa ihtiyacım var mı?** Değerlendirme için bir deneme sürümü çalışır; üretim için ticari lisans gereklidir.  
- **İlk adım nedir?** Maven projenize GroupDocs.Search bağımlılığını ekleyin.

## Log dosyası boyutunu sınırlama nedir?
Log dosyası boyutunu sınırlamak, günlükçüyü dosya önceden tanımlanmış bir eşiğe (ör. 4 MB) ulaştığında büyümeyi durduracak veya devre dışı bırakacak şekilde yapılandırmak anlamına gelir. Bu, uygulamanızın depolama ayak izini öngörülebilir tutar ve performans düşüşünü önler.

## GroupDocs.Search ile dosya ve özel günlükçüler neden kullanılmalı?
- **Denetlenebilirlik:** İndeksleme ve arama olaylarının kalıcı kaydını tutun.  
- **Hata Ayıklama:** Kısa günlükleri inceleyerek sorunları hızlıca tespit edin.  
- **Esneklik:** Kalıcı dosya günlükleri ile anlık console çıktısı (`use console logger java`) arasında seçim yapın.  

## Prerequisites
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 veya daha yeni, IDE (IntelliJ IDEA, Eclipse, vb.).  
- Temel Java ve Maven bilgisi.  

## Setting Up GroupDocs.Search for Java

Kütüphaneyi projenize aşağıdaki yöntemlerden birini kullanarak ekleyin.

**Maven Setup:**

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

**Doğrudan İndirme:**  
Resmi siteden en son JAR'ı indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
Deneme sürümünü edinin veya lisansı [lisans sayfası](https://purchase.groupdocs.com/temporary-license/) üzerinden satın alın.

## How to limit log file size with File Logger
İşte `FileLogger`'ı, log dosyasının belirttiğiniz boyutu aşmamasını sağlayacak şekilde yapılandırmayı gösteren adım‑adım bir rehber.

### 1️⃣ Gerekli Paketleri İçe Aktarın
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Dosya Günlükçüsü ile Index Settings'i Ayarlayın
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ İndeksi Oluşturun veya Yükleyin
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Belgeleri İndekse Ekleyin
```java
index.add(documentsFolder);
```

### 5️⃣ Bir Arama Sorgusu Gerçekleştirin
```java
SearchResult result = index.search(query);
```

**Önemli nokta:** `FileLogger` yapıcısının ikinci argümanı (`4.0`), megabayt cinsinden maksimum log dosyası boyutunu tanımlar ve **log dosyası boyutunu sınırlama** gereksinimini doğrudan karşılar.

## How to use console logger java
Eğer terminalde anlık geri bildirim tercih ediyorsanız, dosya günlükçüsünü console logger ile değiştirin.

### 1️⃣ Console Logger'ı İçe Aktarın
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Console Logger ile Index Settings'i Ayarlayın
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ İndeksi Oluşturun veya Yükleyin
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Belgeleri Ekleyin ve Bir Arama Gerçekleştirin
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**İpucu:** Console logger, geliştirme sırasında idealdir çünkü her log girişini anında yazdırır ve indeksleme ile aramanın beklendiği gibi çalıştığını doğrulamanıza yardımcı olur.

## Practical Applications
1. **Belge Yönetim Sistemleri:** İndekslenen her belgenin denetim izini tutun.  
2. **Kurumsal Arama Motorları:** Sorgu performansını ve hata oranlarını gerçek zamanlı izleyin.  
3. **Hukuk ve Uyumluluk Yazılımları:** Düzenleyici raporlamalar için arama terimlerini kaydedin.

## Performance Considerations
- **Log Boyutu:** Log dosyası boyutunu sınırlayarak, uygulamanızı yavaşlatabilecek aşırı disk kullanımını önlersiniz.  
- **Asenkron Günlükleme:** Daha yüksek verimlilik gerekiyorsa, günlükçüyü asenkron bir kuyruğa sarmayı düşünün (bu kılavuzun kapsamı dışında).  
- **Bellek Yönetimi:** JVM ayak izini düşük tutmak için `Index` nesnelerini artık ihtiyaç duyulmadığında serbest bırakın.

## Common Issues & Solutions
- **Log yolu erişilemez:** Dizinin var olduğunu ve uygulamanın yazma izinlerine sahip olduğunu doğrulayın.  
- **Logger çalışmıyor:** `Index` nesnesini oluşturmadan önce `settings.setLogger(...)` çağrısını yaptığınızdan emin olun.  
- **Console çıktısı eksik:** Uygulamayı `System.out`'u gösteren bir terminalde çalıştırdığınızdan emin olun.

## Frequently Asked Questions

**S: `FileLogger`'ın ikinci parametresi neyi kontrol eder?**  
C: Megabayt cinsinden log dosyasının maksimum boyutunu ayarlar ve log dosyası boyutunu sınırlamanıza olanak tanır.

**S: Dosya ve console logger'ı birleştirebilir miyim?**  
C: Evet, mesajları her iki hedefe de yönlendiren özel bir logger oluşturarak bunu yapabilirsiniz.

**S: İlk oluşturmanın ardından indekse belge nasıl eklenir?**  
C: İstediğiniz zaman `index.add(pathToNewDocs)` çağırın; logger işlemi kaydeder.

**S: `ConsoleLogger` thread‑safe mi?**  
C: Doğrudan `System.out`'a yazar; JVM tarafından senkronize edildiği için çoğu kullanım senaryosunda güvenlidir.

**S: Log dosyası boyutunu sınırlamak saklanan bilgi miktarını etkiler mi?**  
C: Boyut sınırına ulaşıldığında, yeni girişler kaybolabilir veya logger implementasyonuna bağlı olarak dosya devre dışı bırakılabilir.

## Resources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Son Güncelleme:** 2025-12-24  
**Test Edilen Versiyon:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs