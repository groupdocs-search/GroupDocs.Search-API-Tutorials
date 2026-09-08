---
date: '2026-07-21'
description: Java Boolean Sorgu Oluşturma öğreticisi, GroupDocs.Search for Java kullanarak
  boolean AND, OR, NOT aramaları nasıl uygulanacağını, belgeleri bir index'e eklemeyi
  ve belge retrieval'ını artırmayı gösterir.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Java Boolean Sorgu Oluşturma öğreticisi, adım adım GroupDocs.Search
  for Java ile AND, OR, NOT sorgularının nasıl oluşturulacağını, belgeleri bir index'e
  eklemeyi ve retrieval performansını artırmayı açıklar.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Java'da Boolean Sorgu Oluşturma – GroupDocs.Search ile Boolean Aramaları
  Ustalaşın
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Java''da Boolean Sorgu Oluşturma: GroupDocs.Search for Java ile Boolean Aramaları
  Ustalaşın'
type: docs
url: /tr/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Boolean Sorgu Oluşturma Java: GroupDocs.Search for Java ile Boolean Aramaları Ustalaştırın

Devasa belge koleksiyonlarını aramak, samanlıkta iğne bulmak gibi hissettirebilir. **Create Boolean Query Java** size motoru tam olarak ne istediğinizi söylemenizi sağlar—*her iki* terimi içeren belgeler, *herhangi bir* terimi içeren belgeler veya istenmeyen kelimeleri *hariç tutan* belgeler. Bu rehberde **GroupDocs.Search for Java** kurulumunu, belgeleri bir indekse eklemeyi ve **document retrieval java** iş akışlarınızı güçlendiren güçlü boolean sorgularını nasıl oluşturacağınızı adım adım göstereceğiz. Sonunda, sadece birkaç satırla Java'da boolean sorgular oluşturan temiz ve sürdürülebilir kodlar yazabilecek olacaksınız.

## Hızlı Cevaplar
- **Boolean AND sorgusu nedir?** Belirtilen *tüm* terimleri içeren belgeleri döndürür.  
- **OR, AND'den nasıl farklıdır?** OR, *herhangi* bir terimi içeren belgeleri eşleştirir, sonuç kümesini genişletir.  
- **NOT ne zaman kullanılmalı?** İstenmeyen kelimeleri içeren belgeleri filtrelemek için NOT kullanın.  
- **Lisans gerekli mi?** Test için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **Hangi Java sürümü gerekiyor?** Java 8+ desteklenir; JDK 11+ önerilir.  

## **create boolean query java** nedir?
`create boolean query java` Java'da AND, OR ve NOT gibi mantıksal operatörleri GroupDocs.Search API'si kullanarak bir arama sorgusu oluşturmayı ifade eder. Bu operatörleri bir araya getirerek hangi belgelerin eşleşeceğini kesin olarak kontrol edebilir, gelişmiş filtreleme, alaka düzeyi ayarlaması ve karmaşık arama senaryolarını etkinleştirebilirsiniz.

## GroupDocs.Search for Java neden kullanılmalı?
- **High performance** büyük belge setlerinde – standart bir sunucuda bir dakikadan kısa sürede 500 GB metni indeksleyip arayabilir.  
- **Rich API** hem metin‑tabanlı hem de nesne‑tabanlı sorguları destekler, mimarinize uygun stili seçmenizi sağlar.  
- **Built‑in language support** 30+ dilde kök bulma, durak kelimeler ve bulanık eşleştirme desteği sunar.  
- **Easy integration** Maven veya doğrudan JAR indirme ile kolay entegrasyon sağlar, başlamak için sadece birkaç satır kod gerekir.  

## Önkoşullar
Before diving in, make sure you have:

- **GroupDocs.Search for Java** (v25.4 veya daha yeni) – aşağıdaki indirme bağlantısına bakın.  
- IDE'nizde (IntelliJ IDEA, Eclipse, vb.) JDK 8+ yüklü ve yapılandırılmış olmalı.  
- Temel Java bilgisi ve bağımlılık yönetimi için Maven.  

## GroupDocs.Search for Java Kurulumu

### Maven Kurulumu
Add the repository and dependency to your `pom.xml`:

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

### Doğrudan İndirme
Alternatif olarak, resmi siteden en son JAR'ı indirin: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisans Edinme
Tüm özellikleri keşfetmek için ücretsiz deneme lisansı ile başlayın. Üretim kullanımı için tam işlevselliği açmak amacıyla ticari bir lisans satın alın.

### Temel Başlatma ve Kurulum
Create an index folder and instantiate the `Index` object:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Boolean sorgu java nasıl oluşturulur?
The `Index` class represents a searchable collection of documents stored on disk. A `BooleanQuery` combines multiple sub‑queries with logical operators. `createAndQuery`, `createOrQuery`, and `createNotQuery` construct AND, OR, and NOT sub‑queries respectively. Load or create an `Index` instance, add documents, then build a `BooleanQuery` object using `createAndQuery`, `createOrQuery`, or `createNotQuery`. Call `index.search(query)` to retrieve matching documents. This pattern works for simple and complex scenarios alike and requires only three logical steps: index initialization, document addition, and query execution.

## Boolean AND Arama

### Genel Bakış
AND sorgusu sonuçları daraltır, birden fazla kritere uyan belgeler gerektiğinde alaka düzeyini artırır.

### Uygulama Adımları

1. **Initialize Index** – bu aynı zamanda **add documents to index**'i AND senaryosu için gösterir.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – düz metin sözdizimini kullanarak.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – sorguları programlı olarak oluştururken faydalıdır (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Boolean OR Arama

### Genel Bakış
OR sorgusu, birkaç anahtar kelimeden en az birini içeren belgeleri yakalamak istediğiniz keşif amaçlı aramalar için idealdir (**search with or java**).

### Uygulama Adımları

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Boolean NOT Arama

### Genel Bakış
NOT sorgusu, rakip bir marka adını filtrelemek gibi alakasız belgeleri ortadan kaldırmanıza yardımcı olur (**boolean search examples java**).

### Uygulama Adımları

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Karmaşık Boolean Sorguları

### Genel Bakış
Karmaşık sorgular, gerçek dünya arama senaryolarını modellemenizi sağlar; örneğin “olumlu olan spor makalelerini bul, ancak belirli sporcuların herhangi bir bahsini hariç tut”.

### Uygulama Adımları

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## **java boolean and or** Sorgularının Pratik Uygulamaları
- **Document Management Systems** – “confidential” **AND** “renewal” içeren sözleşmeleri bulun.  
- **Legal Research** – **AND**/**OR** ile dava hukukunu filtreleyin, eski yasaları **NOT** ile hariç tutun.  
- **Customer Support** – “login” **AND** “error” içeren ancak “resolved” olmayan biletleri alın.  
- **Content Curation** – bülten için “cloud” **OR** “serverless” hakkında blog gönderilerini toplayın.  

## Yaygın Tuzaklar ve Sorun Giderme
- **Missing Index Refresh** – yeni belgeler ekledikten sonra, aranabilir olmalarını sağlamak için `index.update()` çağırın.  
- **Incorrect Operator Spacing** – GroupDocs.Search operatörlerin (`AND`, `OR`, `NOT`) etrafında boşluklar bekler.  
- **Case Sensitivity** – sorgular varsayılan olarak büyük/küçük harfe duyarsızdır, ancak özel analizörler bunu etkileyebilir.  
- **Large Result Sets** – bellek aşımını önlemek için sayfalama (`search(query, 0, 100)`) kullanın.  

## Sıkça Sorulan Sorular

**S: AND sorgusunda iki terimden fazla birleştirebilir miyim?**  
C: Kesinlikle. Birden fazla `createWordQuery` nesnesini `createAndQuery` ile zincirleyebilir ya da metin sorgusunda doğrudan `"term1 AND term2 AND term3"` yazabilirsiniz.

**S: GroupDocs.Search wildcard veya fuzzy aramaları destekliyor mu?**  
C: Evet. Wildcard için `*` ekleyin (ör. `promot*`) veya fuzzy eşleşme için `~` kullanın (ör. `comfort~`).

**S: Aramayı belirli dosya türleriyle nasıl sınırlayabilirim?**  
`FileTypeQuery` arama sonuçlarını PDF veya DOCX gibi belirli dosya formatlarıyla sınırlar.  
C: Sonuçları PDF, DOCX vb. ile sınırlamak için `FileTypeQuery` sınıfını kullanın ve boolean sorgunuzla birleştirin.

**S: İndeksleme performansını izlemek için en iyi yol nedir?**  
C: Yerleşik logger'ı etkinleştirin (`index.getLogger().setLevel(Level.INFO)`) ve her `add` işleminden sonra zaman ölçümlerini inceleyin.

**S: Belirli terimlerin alaka düzeyini artırmanın bir yolu var mı?**  
`BoostQuery` bir arama sorgusunda belirtilen terimlerin alaka puanını artırır.  
C: Evet. Önemli kelimeleri `BoostQuery` ile sararak puanlama algoritmasındaki ağırlıklarını artırabilirsiniz.

---

**Son Güncelleme:** 2026-07-21  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 (Java)  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [Boolean Operatörleri Java – Arama İndeksi Oluşturma ve Faceted Arama](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [GroupDocs.Search Java&#58; Verimli Belge Arama ve İndeks Yönetimi](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - GroupDocs.Search Java’yı Ustalaştırma – Arama İndeksi Oluşturma ve Yönetme](/search/java/indexing/groupdocs-search-java-create-index-guide/)