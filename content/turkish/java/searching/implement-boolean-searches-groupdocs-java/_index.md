---
date: '2026-01-29'
description: GroupDocs.Search for Java kullanarak Java boolean ve or sorgularını nasıl
  uygulayacağınızı öğrenin, belgeleri indekse ekleyin ve belge geri getirmeyi geliştirin.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: GroupDocs.Search for Java ile Boolean Aramalarında Usta'
type: docs
url: /tr/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: GroupDocs.Search for Java ile Boolean Aramaları Ustalıkla Yönetin

Devasa belge koleksiyonlarını aramak, samanlıkta iğne aramaya benzer bir his verebilir. **java boolean and or** sorgularıyla motoru tam olarak ne istediğinizi söyleyebilirsiniz—*her iki* terimi içeren belgeler, *herhangi bir* terimi içeren belgeler veya istenmeyen kelimeleri *hariç tutan* belgeler. Bu rehberde **GroupDocs.Search for Java** kurulumunu, bir indekse belge eklemeyi ve **document retrieval java** iş akışlarınızı güçlendiren güçlü boolean sorgularını nasıl oluşturacağınızı adım adım göstereceğiz.

## Hızlı Yanıtlar
- **Boolean AND sorgusu nedir?** Belirtilen *tüm* terimleri içeren belgeleri döndürür.  
- **OR, AND'den nasıl farklıdır?** OR, terimlerin *herhangi birine* sahip belgeleri eşleştirir ve sonuç kümesini genişletir.  
- **NOT ne zaman kullanılmalı?** İstenmeyen kelimeleri içeren belgeleri filtrelemek için NOT kullanın.  
- **Lisans gerekli mi?** Test için ücretsiz deneme yeterlidir; üretim için ticari lisans gereklidir.  
- **Hangi Java sürümü gereklidir?** Java 8+ desteklenir; JDK 11+ önerilir.  

## **java boolean and or** nedir?
Bir **java boolean and or** sorgusu, arama sonuçlarını iyileştirmek için mantıksal operatörleri (AND, OR, NOT) birleştirir. Sorguları yapılandırarak GroupDocs.Search'e terimlerin birbirleriyle nasıl ilişkili olduğunu tam olarak belirtir ve geri getirme sürecinde kesin kontrol sağlarsınız.

## Neden GroupDocs.Search for Java Kullanmalı?
- **Yüksek performans** büyük belge setlerinde.  
- **Zengin API** hem metin‑tabanlı hem de nesne‑tabanlı sorguları destekler.  
- **Yerleşik dil desteği** kök bulma, durak kelimeler ve bulanık eşleştirme için.  
- **Kolay entegrasyon** Maven ile ya da doğrudan JAR indirme ile.  

## Önkoşullar
Başlamadan önce, aşağıdakilere sahip olduğunuzdan emin olun:
- **GroupDocs.Search for Java** (v25.4 veya daha yeni) – aşağıdaki indirme bağlantısına bakın.  
- JDK 8+ yüklü ve IDE'nizde (IntelliJ IDEA, Eclipse vb.) yapılandırılmış.  
- Temel Java bilgisi ve bağımlılık yönetimi için Maven.  

## GroupDocs.Search for Java Kurulumu

### Maven Kurulumu
`pom.xml` dosyanıza depo ve bağımlılığı ekleyin:

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
Alternatif olarak, resmi siteden en son JAR'ı indirin: [GroupDocs.Search for Java sürümleri](https://releases.groupdocs.com/search/java/).

### Lisans Edinme
Tüm özellikleri keşfetmek için ücretsiz deneme lisansı ile başlayın. Üretim kullanımı için, tam işlevselliği açmak amacıyla ticari lisans satın alın.

### Temel Başlatma ve Kurulum
`Index` nesnesini oluşturmak için bir indeks klasörü oluşturun ve örnekleyin:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or: Boolean Aramaları Uygulama

Aşağıda **AND**, **OR**, **NOT** ve **complex** sorgularını ele alacağız. Her bölüm, hem düz metin sorgusunu hem de eşdeğer nesne‑tabanlı sorguyu gösterir, böylece kod tabanınıza uygun stili seçebilirsiniz.

### Boolean AND Araması
*AND* ile terimleri birleştirerek sadece *tüm* anahtar kelimeleri içeren belgeleri alın.

#### Genel Bakış
AND sorgusu sonuçları daraltır, birden fazla kritere uyan belgeler gerektiğinde alaka düzeyini artırır.

#### Uygulama Adımları

1. **Index'i Başlat** – bu aynı zamanda AND senaryosu için **add documents to index** işlemini gösterir.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Metin Sorgu Araması Yap** – düz string sözdizimini kullanarak.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Nesne Sorgu Araması Yap** – sorguları programlı olarak oluştururken faydalıdır (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Boolean OR Araması
**OR** kullanarak sonuçları genişletin, verilen terimlerin herhangi birine uyanları eşleştirin.

#### Genel Bakış
OR sorgusu, birkaç anahtar kelimeden en az birini içeren belgeleri yakalamak istediğiniz keşif amaçlı aramalar için idealdir (**search with or java**).

#### Uygulama Adımları

1. **Index'i Başlat**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Metin Sorgu Araması Yap**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Nesne Sorgu Araması Yap**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Boolean NOT Araması
Sonuçlarınızdan istenmeyen terimleri **NOT** ile hariç tutarak gürültüyü filtreleyin.

#### Genel Bakış
NOT sorgusu, bir rakibin marka adını filtrelemek gibi alakasız belgeleri ortadan kaldırmanıza yardımcı olur (**boolean search examples java**).

#### Uygulama Adımları

1. **Index'i Başlat**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Metin Sorgu Araması Yap**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Nesne Sorgu Araması Yap**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Karmaşık Boolean Sorguları
**AND**, **OR** ve **NOT** kombinasyonunu kullanarak son derece spesifik geri getirme ihtiyaçları için karmaşık arama mantığı oluşturun.

#### Genel Bakış
Karmaşık sorgular, “olumlu olan spor makalelerini bul, ancak belirli sporcuların herhangi bir bahsini hariç tut” gibi gerçek dünya arama senaryolarını modellemenizi sağlar.

#### Uygulama Adımları

1. **Index'i Başlat**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Belgeleri İndeksle**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Metin Sorgu Araması Yap**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Nesne Sorgu Araması Yap**

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

## java boolean and or Sorgularının Pratik Uygulamaları
- **Belge Yönetim Sistemleri** – “confidential” **AND** “renewal” içeren sözleşmeleri bulun.  
- **Hukuki Araştırma** – **AND**/**OR** ile dava hukukunu filtreleyin, eski mevzuatı **NOT** ile hariç tutun.  
- **Müşteri Desteği** – “login” **AND** “error” içeren ancak “resolved” olmayan biletleri alın.  
- **İçerik Kürasyonu** – bülten için “cloud” **OR** “serverless” hakkında blog gönderilerini toplayın.  

## Yaygın Tuzaklar ve Sorun Giderme
- **Eksik Index Yenileme** – yeni belgeler ekledikten sonra, aranabilir olmalarını sağlamak için `index.update()` çağırın.  
- **Yanlış Operatör Boşlukları** – GroupDocs.Search operatörlerin (`AND`, `OR`, `NOT`) etrafında boşluk olmasını bekler.  
- **Büyük/Küçük Harf Duyarlılığı** – sorgular varsayılan olarak büyük/küçük harfe duyarsızdır, ancak özel analizörler bunu etkileyebilir.  
- **Büyük Sonuç Kümeleri** – bellek aşımını önlemek için sayfalama (`search(query, 0, 100)`) kullanın.  

## Sıkça Sorulan Sorular

**S: AND sorgusunda iki terimden fazla birleştirebilir miyim?**  
C: Kesinlikle. Birden fazla `createWordQuery` nesnesini `createAndQuery` ile zincirleyebilir veya metin sorgusunda `"term1 AND term2 AND term3"` şeklinde yazabilirsiniz.

**S: GroupDocs.Search wildcard veya fuzzy aramaları destekliyor mu?**  
C: Evet. Wildcard için `*` ekleyin (örn., `promot*`) veya fuzzy eşleşme için `~` kullanın (örn., `comfort~`).

**S: Aramayı belirli dosya türleriyle sınırlamak nasıl yapılır?**  
C: Sonuçları PDF, DOCX vb. ile sınırlamak için `FileTypeQuery` sınıfını kullanın ve bunu boolean sorgunuzla birleştirin.

**S: Indexleme performansını izlemek için en iyi yol nedir?**  
C: Yerleşik logger'ı etkinleştirin (`index.getLogger().setLevel(Level.INFO)`) ve her `add` işleminden sonra zaman ölçümlerini inceleyin.

**S: Belirli terimlerin alaka düzeyini artırmanın bir yolu var mı?**  
C: Evet. Önemli kelimeleri `BoostQuery` ile sararak puanlama algoritmasındaki ağırlıklarını artırabilirsiniz.

---

**Son Güncelleme:** 2026-01-29  
**Test Edilen Versiyon:** GroupDocs.Search 25.4 (Java)  
**Yazar:** GroupDocs