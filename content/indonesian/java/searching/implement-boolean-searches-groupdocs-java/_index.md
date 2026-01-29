---
date: '2026-01-29'
description: Pelajari cara mengimplementasikan query boolean AND OR Java menggunakan
  GroupDocs.Search untuk Java, tambahkan dokumen ke indeks, dan tingkatkan pengambilan
  dokumen.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: Kuasai Pencarian Boolean dengan GroupDocs.Search untuk
  Java'
type: docs
url: /id/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Kuasai Pencarian Boolean dengan GroupDocs.Search untuk Java

Mencari koleksi dokumen yang sangat besar dapat terasa seperti mencari jarum dalam tumpukan jerami. Dengan kueri **java boolean and or** Anda dapat memberi tahu mesin persis apa yang Anda butuhkan—dokumen yang berisi *kedua* istilah, *salah satu* istilah, atau *mengecualikan* kata yang tidak diinginkan. Dalam panduan ini kami akan menjelaskan cara menyiapkan **GroupDocs.Search for Java**, menambahkan dokumen ke indeks, dan membuat kueri boolean yang kuat yang meningkatkan alur kerja **document retrieval java** Anda.

## Jawaban Cepat
- **Apa itu kueri boolean AND?** Mengembalikan hanya dokumen yang berisi *semua* istilah yang ditentukan.  
- **Bagaimana OR berbeda dari AND?** OR mencocokkan dokumen dengan *salah satu* istilah, memperluas kumpulan hasil.  
- **Kapan saya harus menggunakan NOT?** Gunakan NOT untuk menyaring dokumen yang mengandung kata yang tidak diinginkan.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi komersial diperlukan untuk produksi.  
- **Versi Java apa yang diperlukan?** Java 8+ didukung; JDK 11+ direkomendasikan.

## Apa itu **java boolean and or**?
Sebuah kueri **java boolean and or** menggabungkan operator logika (AND, OR, NOT) untuk memperbaiki hasil pencarian. Dengan menyusun kueri, Anda memberi tahu GroupDocs.Search secara tepat bagaimana istilah‑istilah saling berhubungan, memberikan kontrol yang presisi atas proses pengambilan.

## Mengapa menggunakan GroupDocs.Search untuk Java?
- **High performance** pada kumpulan dokumen besar.  
- **Rich API** yang mendukung kueri berbasis teks maupun objek.  
- **Built‑in language support** untuk stemming, stop‑words, dan pencocokan fuzzy.  
- **Easy integration** dengan Maven atau unduhan JAR langsung.

## Prasyarat
Sebelum memulai, pastikan Anda memiliki:

- **GroupDocs.Search for Java** (v25.4 atau lebih baru) – lihat tautan unduhan di bawah.  
- JDK 8+ terpasang dan dikonfigurasi di IDE Anda (IntelliJ IDEA, Eclipse, dll.).  
- Pengetahuan dasar Java dan Maven untuk manajemen dependensi.

## Menyiapkan GroupDocs.Search untuk Java

### Pengaturan Maven
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

### Unduhan Langsung
Sebagai alternatif, unduh JAR terbaru dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Mulailah dengan lisensi percobaan gratis untuk menjelajahi semua fitur. Untuk penggunaan produksi, beli lisensi komersial untuk membuka semua fungsionalitas.

### Inisialisasi dan Penyiapan Dasar
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

## java boolean and or: Menerapkan Pencarian Boolean
Di bawah ini kami akan membahas kueri **AND**, **OR**, **NOT**, dan **complex**. Setiap bagian menampilkan kueri teks biasa dan kueri berbasis objek yang setara, sehingga Anda dapat memilih gaya yang sesuai dengan basis kode Anda.

### Pencarian Boolean AND
Gabungkan istilah dengan **AND** untuk mengambil hanya dokumen yang berisi *semua* kata kunci.

#### Gambaran Umum
Kueri AND mempersempit hasil, meningkatkan relevansi ketika Anda membutuhkan dokumen yang memenuhi beberapa kriteria.

#### Langkah Implementasi

1. **Initialize Index** – this also demonstrates **add documents to index** for the AND scenario.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – using the plain string syntax.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – useful when building queries programmatically (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Pencarian Boolean OR
Gunakan **OR** untuk memperluas hasil, mencocokkan salah satu istilah yang diberikan.

#### Gambaran Umum
Kueri OR ideal untuk pencarian eksploratif di mana Anda ingin menangkap dokumen yang mengandung setidaknya satu dari beberapa kata kunci (**search with or java**).

#### Langkah Implementasi

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

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

### Pencarian Boolean NOT
Kecualikan istilah yang tidak diinginkan dengan **NOT** untuk menyaring kebisingan dari hasil Anda.

#### Gambaran Umum
Kueri NOT membantu Anda menghilangkan dokumen yang tidak relevan, seperti menyaring nama merek pesaing (**boolean search examples java**).

#### Langkah Implementasi

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

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

### Kueri Boolean Kompleks
Gabungkan **AND**, **OR**, dan **NOT** untuk membuat logika pencarian yang rumit bagi kebutuhan pengambilan yang sangat spesifik.

#### Gambaran Umum
Kueri kompleks memungkinkan Anda memodelkan skenario pencarian dunia nyata, seperti “temukan artikel olahraga yang bersifat positif tetapi kecualikan setiap penyebutan atlet tertentu”.

#### Langkah Implementasi

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

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

## Aplikasi Praktis Kueri java boolean and or
- **Document Management Systems** – temukan kontrak yang berisi baik “confidential” **AND** “renewal”.  
- **Legal Research** – saring kasus hukum dengan **AND**/ **OR** sambil mengecualikan undang‑undang yang usang menggunakan **NOT**.  
- **Customer Support** – ambil tiket yang menyebut “login” **AND** “error” tetapi tidak “resolved”.  
- **Content Curation** – kumpulkan posting blog tentang “cloud” **OR** “serverless” untuk buletin.

## Kesalahan Umum & Pemecahan Masalah
- **Missing Index Refresh** – setelah menambahkan dokumen baru, panggil `index.update()` untuk memastikan mereka dapat dicari.  
- **Incorrect Operator Spacing** – GroupDocs.Search mengharapkan spasi di sekitar operator (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – kueri tidak sensitif huruf besar/kecil secara default, tetapi analyzer khusus dapat memengaruhi hal ini.  
- **Large Result Sets** – gunakan paginasi (`search(query, 0, 100)`) untuk menghindari kelebihan memori.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggabungkan lebih dari dua istilah dalam kueri AND?**  
A: Tentu saja. Anda dapat menautkan beberapa objek `createWordQuery` dengan `createAndQuery`, atau cukup menulis "term1 AND term2 AND term3" dalam kueri teks.

**Q: Apakah GroupDocs.Search mendukung pencarian wildcard atau fuzzy?**  
A: Ya. Tambahkan `*` untuk wildcard (mis., `promot*`) atau gunakan `~` untuk pencocokan fuzzy (mis., `comfort~`).

**Q: Bagaimana cara membatasi pencarian pada tipe file tertentu?**  
A: Gunakan kelas `FileTypeQuery` untuk membatasi hasil ke PDF, DOCX, dll., dan gabungkan dengan kueri boolean Anda.

**Q: Apa cara terbaik untuk memantau kinerja pengindeksan?**  
A: Aktifkan logger bawaan (`index.getLogger().setLevel(Level.INFO)`) dan tinjau metrik waktu setelah setiap operasi `add`.

**Q: Apakah ada cara untuk meningkatkan relevansi istilah tertentu?**  
A: Ya. Bungkus kata penting dengan `BoostQuery` untuk meningkatkan bobotnya dalam algoritma penilaian.

---

**Last Updated:** 2026-01-29  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs