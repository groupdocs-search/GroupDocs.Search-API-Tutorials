---
date: '2026-09-21'
description: GroupDocs.Search for Java'da logger oluşturmayı, maksimum log boyutunu
  ayarlamayı ve konsol logger'ını kullanmayı öğrenin.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: GroupDocs.Search for Java'da logger oluşturmayı, maksimum log boyutunu
  ayarlamayı ve konsol logger'ını kullanmayı öğrenin. Adım adım talimatları ve en
  iyi uygulama ipuçlarını izleyin.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: GroupDocs.Search'te logger oluşturma ve log boyutunu sınırlama
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: GroupDocs.Search for Java'da logger oluşturma ve log boyutunu sınırlama
type: docs
url: /tr/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search for Java'da logger oluşturma ve log dosyası boyutunu sınırlama

Bu öğreticide GroupDocs.Search için **logger oluşturma** uygulamalarını, maksimum log dosyası boyutunu yapılandırmayı ve dosya tabanlı ile konsol tabanlı loglamalar arasında geçiş yapmayı öğreneceksiniz. Doğru log yönetimi, büyük indeksleme görevleri sırasında disklerin dolmasını önler, sorun giderme sürecini iyileştirir ve geliştirme sırasında anlık geri bildirim sağlar. Maven kurulumuyla başlayacak, logger yapılandırmasını adım adım inceleyecek ve logger'ın çalışmasını gösteren basit bir arama sorgusuyla sonlandıracağız.

## Hızlı cevaplar
- **“Log dosyası boyutunu sınırlama” ne anlama gelir?** Bir log dosyasının maksimum boyutunu sınırlar ve diskte kontrolsüz büyümeyi önler.  
- **Hangi logger log dosyası boyutunu sınırlamanıza izin verir?** Yerleşik `FileLogger` bir maksimum‑boyut parametresi alır.  
- **Java'da console logger nasıl kullanılır?** `ConsoleLogger`'ı örnekleyin ve `IndexSettings` üzerine ayarlayın.  
- **GroupDocs.Search için lisans gerekir mi?** Değerlendirme için bir deneme sürümü çalışır; üretim için ticari lisans gereklidir.  
- **İlk adım nedir?** Maven projenize GroupDocs.Search bağımlılığını ekleyin.  

## Log dosyası boyutunu sınırlama nedir?
**Log dosyası boyutunu sınırlama** ayarı, dosya belirli bir eşiğe (örneğin 4 MB) ulaştığında logger'ın yeni girişler yazmayı durdurmasını söyler. Limit aşıldığında, logger ya sonraki mesajları yok sayar ya da yeni bir dosyaya geçerek disk kullanımını öngörülebilir tutar.

## GroupDocs.Search ile dosya ve özel logger'ları neden kullanmalısınız?
Dosya ve özel logger'lar denetlenebilirlik, hata ayıklama içgörüsü ve esneklik sağlar. Üretim ortamlarında, dosya logları her indeksleme ve arama işleminin kalıcı kaydını tutarken, konsol logları geliştirme sırasında anlık geri bildirim verir. Bu loglar ekiplerin performansı izlemelerine, hataları izlemelerine ve ayrıntılı bir aktivite izi tutarak uyumluluk gereksinimlerini karşılamalarına yardımcı olur.

## Önkoşullar
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 veya daha yeni bir sürüm, IntelliJ IDEA veya Eclipse gibi bir IDE ile.  
- Maven ve Java programlamaya temel aşinalık.  

## GroupDocs.Search for Java Kurulumu

Kütüphaneyi projenize aşağıdaki yöntemlerden biriyle ekleyin.

**Maven kurulumu:**  

```text
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
```

**Doğrudan indirme:**  
Resmi siteden en son JAR'ı indirin: [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/).

### Lisans edinme
Deneme sürümü edinin veya [lisans sayfası](https://purchase.groupdocs.com/temporary-license/) üzerinden bir lisans satın alın.

## GroupDocs.Search için özel logger nasıl oluşturulur
Özel bir logger oluşturmak basittir çünkü GroupDocs.Search `ILogger` arayüzüne dayanır. Bu arayüzü uygulayarak—veya sağlanan `FileLogger` ya da `ConsoleLogger`'ı genişleterek—uzak yönlendirme veya log döndürme gibi ek davranışlar ekleyebilirsiniz. Ağ bağlantılarını açma gibi başlatma mantığını da ekleyebilir ve logger'ın kapanış metodunda kaynakların kapatılmasını sağlayabilirsiniz. Bu yaklaşım, ELK veya Splunk gibi izleme platformlarıyla entegrasyon yapmanıza olanak tanır.

### Tanım bağlantısı
`ILogger`, GroupDocs.Search'teki temel loglama sözleşmesidir; `log(Level, String)` metodunu uygulayan herhangi bir sınıf logger olabilir.

### Örnek yaklaşım (kod bloğu yok)
1. `ILogger`'ı uygulayan bir sınıf oluşturun.  
2. `log` metodunu geçersiz kılarak mesajları seçtiğiniz hedefe (dosya, veritabanı, HTTP uç noktası) yazın.  
3. İndeks yapılandırmasında `settings.setLogger(new YourCustomLogger())` çağrısını yapın.  

## File Logger ile log dosyası boyutunu sınırlama
`FileLogger` sınıfı log girişlerini diskte bir dosyaya yazar ve maksimum boyut argümanını kabul eder. Boyut limitini belirleyerek logger, eşik aşıldığında otomatik olarak yeni giriş eklemeyi durdurur veya yeni bir dosya oluşturur, böylece kontrolsüz disk büyümesi önlenir. Bu davranış, loglamanın indeksleme performansını etkilememesini ve olayların özlü bir kaydını tutmasını sağlar.

### Tanım bağlantısı
`FileLogger`, mesajları bir metin dosyasına kalıcı olarak kaydeden ve yapılandırılabilir bir maksimum dosya boyutunu destekleyen yerleşik bir logger'dır.

### Adım adım kılavuz
1️⃣ **Gerekli paketleri içe aktarın**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **File Logger ile indeks ayarlarını yapılandırın**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **İndeksi oluşturun veya yükleyin**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Belgeleri indekse ekleyin**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Bir arama sorgusu gerçekleştirin**  
```text
```java
SearchResult result = index.search(query);
```
```

**Önemli nokta:** `FileLogger` yapıcısının ikinci argümanı (`4.0`), megabayt cinsinden **maksimum log boyutunu ayarlar** ve doğrudan **log dosyası boyutunu sınırlama** gereksinimini karşılar.

## Java'da console logger nasıl kullanılır
Log olaylarını anında görmek istediğinizde, `ConsoleLogger` her mesajı `System.out`'a yazar. Bu logger hafif ve thread‑safe'dir, bu da geliştirme ve hata ayıklama oturumları için uygundur. Dosya I/O gerektirmeden indeksleme ilerlemesi, arama sorguları ve hata durumları hakkında anlık geri bildirim sağlar, bu da yinelemeli testleri hızlandırabilir.

### Tanım bağlantısı
`ConsoleLogger`, log girişlerini standart konsol akışına çıktılan bir hafif logger'dır ve hata ayıklama oturumları için idealdir.

### Yapılandırma adımları
1️⃣ **Console logger'ı içe aktarın**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Console Logger ile indeks ayarlarını yapılandırın**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **İndeksi oluşturun veya yükleyin**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Belgeleri ekleyin ve bir arama gerçekleştirin**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**İpucu:** Console logger geliştirme sırasında idealdir çünkü her log girişini anında yazdırır, bu da indeksleme ve aramanın beklenildiği gibi çalıştığını doğrulamanıza yardımcı olur.

## Pratik uygulamalar
1. **Belge yönetim sistemleri:** İndekslenen her belgenin denetim izini tutar, uyumluluk gereksinimlerini karşılar.  
2. **Kurumsal arama motorları:** Sorgu performansını ve hata oranlarını gerçek zamanlı izler, hızlı SLA uyumluluk kontrolleri sağlar.  
3. **Hukuk ve uyumluluk yazılımları:** Düzenleyici raporlamalar için arama terimlerini ve zaman damgalarını kaydeder, loglar zorunlu saklama süresi boyunca tutulur.

## Performans değerlendirmeleri
- **Log boyutu:** **Maksimum log boyutunu ayarlayarak**, JVM'nin çöp toplayıcısını yavaşlatabilecek aşırı disk kullanımını önlersiniz.  
- **Asenkron loglama:** Yüksek verim senaryoları için logger'ınızı asenkron bir kuyruğa sararak I/O'yu indeksleme iş parçacığından ayırabilirsiniz (bu kılavuzun kapsamı dışında bir uygulamadır).  
- **Bellek yönetimi:** `Index` nesnelerini artık ihtiyaç duyulmadığında `index.close()` ile serbest bırakarak JVM ayak izini düşük tutun.

## Yaygın sorunlar ve çözümler
- **Log yolu erişilemez:** Dizin mevcut mu ve JVM'i çalıştıran kullanıcı hesabının yazma izinlerine sahip mi kontrol edin.  
- **Logger çalışmıyor:** `Index` nesnesini oluşturmadan önce `settings.setLogger(...)` çağrısını yaptığınızdan emin olun; aksi takdirde varsayılan logger kullanılır.  
- **Console çıktısı eksik:** Uygulamayı `System.out`'u gösteren bir terminalde çalıştırdığınızdan ve hiçbir logging çerçevesinin (ör. SLF4J) çıktıyı yakalamadığından emin olun.

## Sıkça sorulan sorular

**S: `FileLogger`'ın ikinci parametresi neyi kontrol eder?**  
C: Log dosyasının maksimum boyutunu megabayt cinsinden ayarlar, böylece **maksimum log boyutunu ayarlayabilir** ve kontrolsüz büyümeyi önleyebilirsiniz.

**S: Dosya ve console logger'larını birleştirebilir miyim?**  
C: Evet. Her `log` çağrısını hem bir `FileLogger` hem de bir `ConsoleLogger`'a yönlendiren özel bir logger oluşturun ve bu birleşik logger'ı `IndexSettings` ile kaydedin.

**S: İlk oluşturulmadan sonra indekse belgeleri nasıl eklerim?**  
C: İstediğiniz zaman `index.add(pathToNewDocs)` çağırın; yapılandırılmış logger otomatik olarak eklemeyi kaydeder.

**S: `ConsoleLogger` thread‑safe mi?**  
C: `System.out`'a doğrudan yazar, JVM içsel olarak senkronize eder, bu da tipik çoklu iş parçacıklı kullanım senaryoları için güvenli olmasını sağlar.

**S: Log dosyası boyutunu sınırlamak saklanan bilgi miktarını etkiler mi?**  
C: Boyut limiti aşıldığında, yeni girişler ya yok sayılır ya da logger seçtiğiniz uygulamaya bağlı olarak yeni bir dosyaya geçer.

## Kaynaklar
- [Dokümantasyon](https://docs.groupdocs.com/search/java/)
- [API Referansı](https://reference.groupdocs.com/search/java/)

---

**Last Updated:** 2026-09-21  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

## İlgili Öğreticiler

- [Logging Uygulama - Hata İşleme ve Logging Öğreticileri for GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Java'da Asenkron Logging Uygulama – GroupDocs.Search – Özel Logger Rehberi](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Java'da Arama İndeksi Oluşturma – GroupDocs.Search Öğreticileri](/search/java/indexing/)