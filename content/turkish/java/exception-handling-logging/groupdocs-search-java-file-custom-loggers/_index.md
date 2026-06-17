---
date: '2026-02-24'
description: GroupDocs.Search for Java'da özel bir logger oluşturmayı, maksimum günlük
  boyutunu ayarlamayı ve konsol ya da dosya logger'ını yapılandırmayı öğrenin.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: GroupDocs.Search Java ile özel logger nasıl oluşturulur ve log dosyası boyutu
  nasıl sınırlanır
type: docs
url: /tr/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search Java Günlükçüleri ile günlük dosyası boyutunu sınırlama

Bu rehberde GroupDocs.Search for Java kullanırken **create custom logger** uygulamaları oluşturacak ve **limit log file size** yöntemini öğreneceksiniz. Günlük büyümesini kontrol etmek, büyük ölçekli belge indekslemesi için kritik öneme sahiptir ve yerleşik logger'lar **set max log size**, **roll over log file** gibi seçenekler sunar ya da anlık geri bildirim için **use console logger**'a geçmenizi sağlar. Maven yapılandırmasından bir arama sorgusu çalıştırmaya kadar tam kurulumu adım adım inceleyecek ve logger etkinken **add documents index** nasıl yapılır göreceksiniz.

## Hızlı Yanıtlar
- **“limit log file size” ne anlama geliyor?** Bir günlük dosyasının maksimum boyutunu sınırlar, diskte kontrolsüz büyümeyi önler.  
- **Hangi logger log dosyası boyutunu sınırlamanıza izin verir?** Yerleşik `FileLogger` bir max‑size parametresi alır.  
- **Java'da console logger nasıl kullanılır?** `ConsoleLogger`'ı örnekleyin ve `IndexSettings` üzerine ayarlayın.  
- **GroupDocs.Search için lisansa ihtiyacım var mı?** Değerlendirme için bir deneme sürümü çalışır; üretim için ticari lisans gereklidir.  
- **İlk adım nedir?** Maven projenize GroupDocs.Search bağımlılığını ekleyin.  

## Log dosyası boyutunu sınırlama nedir?
Log dosyası boyutunu sınırlamak, logger'ı dosya önceden belirlenmiş bir eşiğe (ör. 4 MB) ulaştığında büyümeyi durduracak veya rollover yapacak şekilde yapılandırmak anlamına gelir. Bu, uygulamanızın depolama ayak izini öngörülebilir tutar ve performans düşüşünü önler.

## GroupDocs.Search ile dosya ve özel logger'lar neden kullanılmalı?
- **Auditability:** İndeksleme ve arama olaylarının kalıcı kaydını tutun.  
- **Debugging:** Kısa logları inceleyerek sorunları hızlıca tespit edin.  
- **Flexibility:** Kalıcı dosya logları ile anlık console çıktısı (`use console logger`) arasında seçim yapın.  

## Prerequisites
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 veya daha yeni, IDE (IntelliJ IDEA, Eclipse, vb.).  
- Temel Java ve Maven bilgisi.  

## GroupDocs.Search for Java Kurulumu

Kütüphaneyi projenize aşağıdaki yöntemlerden birini kullanarak ekleyin.

**Maven Kurulumu:**

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

### Lisans Alımı
Bir deneme sürümü edinin veya [lisans sayfası](https://purchase.groupdocs.com/temporary-license/) üzerinden lisans satın alın.

## GroupDocs.Search için özel logger nasıl oluşturulur
GroupDocs.Search, `ILogger` arayüzünün herhangi bir uygulamasını takmanıza izin verir. `FileLogger` veya `ConsoleLogger`'ı genişleterek log dosyasının rollover yapması veya mesajların uzaktaki bir izleme hizmetine yönlendirilmesi gibi ek davranışlar ekleyebilirsiniz. Bu esneklik, birçok ekibin operasyonel ihtiyaçlarına uygun **create custom logger** çözümleri oluşturmasının nedenidir.

## File Logger ile log dosyası boyutunu sınırlama
Aşağıda, log dosyasının belirttiğiniz boyutu aşmamasını sağlayacak şekilde **configure file logger**'ı gösteren adım adım bir rehber bulunmaktadır.

### 1️⃣ Gerekli Paketleri İçe Aktarın
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ File Logger ile Index Settings'i Ayarlayın
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

**Önemli nokta:** `FileLogger` yapıcı metodunun ikinci argümanı (`4.0`), megabayt cinsinden **set max log size**'ı tanımlar ve **limit log file size** gereksinimini doğrudan karşılar.

## Java'da console logger nasıl kullanılır
Terminalde anlık geri bildirim istiyorsanız, dosya logger'ını console logger ile değiştirin.

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

## Pratik Uygulamalar
1. **Document Management Systems:** İndekslenen her belgenin denetim izlerini tutun.  
2. **Enterprise Search Engines:** Sorgu performansını ve hata oranlarını gerçek zamanlı izleyin.  
3. **Legal & Compliance Software:** Düzenleyici raporlamalar için arama terimlerini kaydedin.

## Performans Düşünceleri
- **Log Size:** **set max log size** sayesinde uygulamanızı yavaşlatabilecek aşırı disk kullanımını önlersiniz.  
- **Asynchronous Logging:** Daha yüksek verimlilik gerekiyorsa, logger'ı bir async kuyruk içinde sarmayı düşünün (bu rehberin kapsamı dışında).  
- **Memory Management:** JVM ayak izini düşük tutmak için `Index` nesnelerini artık ihtiyaç duyulmadığında serbest bırakın.

## Yaygın Sorunlar ve Çözümler
- **Log path not accessible:** Dizin mevcut mu ve uygulamanın yazma izinleri var mı kontrol edin.  
- **Logger not firing:** `Index` nesnesini oluşturmadan önce `settings.setLogger(...)` çağırdığınızdan emin olun.  
- **Console output missing:** Uygulamayı `System.out`'u gösteren bir terminalde çalıştırdığınızı doğrulayın.

## Sıkça Sorulan Sorular

**Q: `FileLogger`'ın ikinci parametresi neyi kontrol eder?**  
A: Log dosyasının megabayt cinsinden maksimum boyutunu ayarlar ve **set max log size** yapmanıza olanak tanır.

**Q: Dosya ve console logger'ları birleştirebilir miyim?**  
A: Evet, mesajları her iki hedefe de yönlendiren özel bir logger oluşturarak bunu yapabilirsiniz.

**Q: İlk oluşturmanın ardından indeks'e belge nasıl eklenir?**  
A: `index.add(pathToNewDocs)` metodunu istediğiniz zaman çağırın; logger işlemi kaydeder.

**Q: `ConsoleLogger` thread‑safe mi?**  
A: Doğrudan `System.out`'a yazar; JVM tarafından senkronize edildiği için çoğu kullanım senaryosunda güvenlidir.

**Q: Log dosyası boyutunu sınırlamak saklanan bilgi miktarını etkiler mi?**  
A: Boyut sınırına ulaşıldığında yeni girişler atılabilir veya logger uygulamasına bağlı olarak dosya **roll over log file** yapabilir.

## Kaynaklar
- [Dokümantasyon](https://docs.groupdocs.com/search/java/)
- [API Referansı](https://reference.groupdocs.com/search/java/)

---

**Son Güncelleme:** 2026-02-24  
**Test Edilen Versiyon:** GroupDocs.Search for Java 25.4  
**Yazar:** GroupDocs