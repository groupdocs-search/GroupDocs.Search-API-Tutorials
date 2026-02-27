---
date: '2026-01-14'
description: GroupDocs.Search for Java kullanarak indeks oluşturmayı ve metin çıkarmayı
  verimli bir şekilde öğrenin. Belge aramasını optimize edin, metni dosyaya çıkartın
  ve yapılandırılmış metin çıkarımını yönetin.
keywords:
- GroupDocs.Search for Java
- efficient document search
- index creation in Java
title: Java için GroupDocs.Search ile indeks nasıl oluşturulur
type: docs
url: /tr/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# GroupDocs.Search for Java ile Verimli Belge Aramayı Ustalaşma

Belge yönetimi dünyasında, çok sayıda belge içinde belirli içeriği hızlı bir şekilde bulmak çok önemlidir. Hukuki sözleşmeler ya da akademik makalelerle çalışıyor olun, **create index java** yetenekleri saatler süren manuel işi tasarruf ettirebilir. Bu öğreticide **GroupDocs.Search for Java** kullanımı inceleniyor; güçlü bir **java search library** olup indeksler oluşturmanıza, **add documents to index** ve dosyalarınızdan **extract text java** verimli bir şekilde almanıza yardımcı olur. Bu rehberin sonunda, özel ayarlarla indekslemeyi nasıl yapılandıracağınızı ve belge metnini çeşitli formatlarda, yapılandırılmış metin çıkarımı dahil, nasıl dışa aktaracağınızı öğreneceksiniz.

## Hızlı Yanıtlar
- **Ana amaç nedir?** To **create index java** and retrieve document content quickly.  
- **Hangi kütüphaneyi kullanmalıyım?** The **GroupDocs.Search for Java** **java search library**.  
- **Metni bir dosyaya çıkartabilir miyim?** Yes, use the **output text to file** adapters provided.  
- **Yapılandırılmış çıkarım destekleniyor mu?** Absolutely – use the **structured text extraction** adapter.  
- **Bir lisansa ihtiyacım var mı?** A trial or permanent license is required for production use.

## Öğrenecekleriniz
- GroupDocs.Search for Java kullanarak **create index java** ve **add documents to index** nasıl yapılır.  
- **output text to file**, akışlar, stringler ve yapılandırılmış veri için teknikler.  
- Verimli arama ve bellek yönetimi için performans optimizasyon ipuçları.  
- Bu özelliklerin gerçek dünya uygulamaları.

### Ön Koşullar
Öğreticiye başlamadan önce aşağıdakilerin hazır olduğundan emin olun:
- **Java Development Kit (JDK)**: Version 8 or above is recommended.  
- **GroupDocs.Search for Java** library.  
- **Maven** for dependency management and building your project.  
- Basic knowledge of Java programming, particularly file I/O operations.

### GroupDocs.Search for Java Kurulumu
GroupDocs.Search for Java kullanmaya başlamak için projenize gerekli bağımlılıkları eklemeniz gerekir. Maven kullanarak nasıl kurabileceğiniz aşağıdadır:

**Maven Setup**  
Aşağıdaki depo ve bağımlılık yapılandırmalarını `pom.xml` dosyanıza ekleyin:

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

Doğrudan indirmeyi tercih edenler, en son sürümü [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) adresinden edinebilir.

**License Acquisition**  
GroupDocs.Search kullanmak için ücretsiz deneme veya geçici bir lisans almayı düşünün. Tam bir satın alma için resmi sitelerini ziyaret ederek kalıcı bir lisans edinebilirsiniz.

## Özel ayarlarla create index java nasıl oluşturulur
Bu bölüm, bir indeks oluşturma, belgeleri ekleme ve optimal depolama için sıkıştırma yapılandırmasını adım adım gösterir.

### İndeks Oluşturma ve Belge İndeksleme

#### Genel Bakış
Bir indeks oluşturmak, belgelerinizi verimli bir şekilde aramanızı sağlar. Aşağıdaki örnek, yüksek sıkıştırma ile **create index java** ve ardından **add documents to index** nasıl yapılacağını gösterir.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**Explanation**  
- **Index Settings**: We enable high compression for text storage, optimizing disk space usage.  
- **Adding Documents**: The `index.add()` method **adds documents to index**, scanning the folder recursively.

## Metni dosyaya, akışa, stringe ve yapılandırılmış formatlara nasıl çıkartılır
Aşağıda, **created index java** yaptıktan sonra çıkarılan içeriği almanın ve depolamanın dört yaygın yolu verilmiştir.

### Belge Metni Dosyaya Çıktısı

#### Genel Bakış
Bu örnek, **output text to file** işlemini HTML formatında gösterir; görsel inceleme veya daha ileri işleme için kullanışlıdır.

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**Explanation**  
- **FileOutputAdapter**: Converts the indexed document's text into HTML and writes it to the specified file path.

### Belge Metni Akışa Çıktısı

#### Genel Bakış
Bellek içi işleme ihtiyacınız olduğunda—dinamik web içeriği üretmek gibi—akışa çıkartmak idealdir.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**Explanation**  
- **StreamOutputAdapter**: Streams the document's text into a `ByteArrayOutputStream`, allowing flexible handling without touching the file system.

### Belge Metni Stringe Çıktısı

#### Genel Bakış
İçeriği sadece kaydetmek veya göstermek istiyorsanız, sonucu bir `String`'e dönüştürmek en hızlı yoldur.

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**Explanation**  
- **StringOutputAdapter**: Captures the document's text in a `String`, making it easy to embed in logs or UI components.

### Belge Metni Yapılandırılmış Formata Çıktısı

#### Genel Bakış
Alanlar, tablolar veya özel meta verileri çıkarmak gibi ileri düzey ayrıştırma için yapılandırılmış çıktı adaptörünü kullanın.

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**Explanation**  
- **StructuredOutputAdapter**: Extracts document text into a **structured text extraction** format, enabling fine‑grained analysis or downstream data pipelines.

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|-------|-------|
| **İndeks oluşturulmadı** | Yanlış klasör yolu veya yazma izinlerinin eksik olması | `indexFolder`'ın mevcut olduğunu ve uygulamanın yazma erişimine sahip olduğunu doğrulayın |
| **Belge döndürülmedi** | `index.add()` çağrılmadı veya yanlış kaynak klasörü | `documentsFolder`'ın doğru dizine işaret ettiğinden ve desteklenen dosya türlerini içerdiğinden emin olun |
| **Çıktı dosyası boş** | Çıktı adaptörü yolu geçersiz veya dizinler eksik | Çalıştırmadan önce hedef dizini (`YOUR_OUTPUT_DIRECTORY`) oluşturun |
| **Büyük dosyalarda bellek dalgalanmaları** | Tüm dosyanın belleğe yüklenmesi | Veriyi artımlı işlemek için akış adaptörlerini (`StreamOutputAdapter`) kullanın |

## Sıkça Sorulan Sorular

**S: GroupDocs.Search'i Kotlin veya Scala gibi diğer JVM dilleriyle kullanabilir miyim?**  
C: Evet, kütüphane saf Java'dır ve herhangi bir JVM diliyle sorunsuz çalışır.

**S: Sıkıştırma arama hızını nasıl etkiler?**  
C: Yüksek sıkıştırma disk kullanımını azaltır ancak indeksleme sırasında hafif bir CPU yükü ekleyebilir. Arama performansı hızlı kalır çünkü kütüphane veriyi anlık olarak sıkıştırmadan çıkarır.

**S: Mevcut bir indeksi yeniden oluşturmadan güncellemek mümkün mü?**  
C: Kesinlikle. Yeni dosyalar için `index.add()` ve eski dosyaları silmek için `index.remove()` kullanın.

**S: Daha ileri doğal dil işleme için hangi çıktı formatı en iyisidir?**  
C: **structured text extraction** adaptörü aracılığıyla `PlainText` temiz, dil bağımsız içerik sağlar ve NLP boru hatları için idealdir.

**S: Geliştirme ve test için bir lisansa ihtiyacım var mı?**  
C: Geliştirme ve değerlendirme için ücretsiz deneme lisansı yeterlidir. Üretim ortamları için satın alınmış bir lisans gereklidir.

---

**Last Updated:** 2026-01-14  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs