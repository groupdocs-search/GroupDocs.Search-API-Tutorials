---
date: '2026-07-21'
description: Tutorial Create Boolean Query Java menunjukkan cara mengimplementasikan
  pencarian boolean AND, OR, NOT menggunakan GroupDocs.Search for Java, menambahkan
  dokumen ke dalam indeks, dan boost retrieval dokumen.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Tutorial Create Boolean Query Java menjelaskan langkah demi langkah
  cara membangun query AND, OR, NOT dengan GroupDocs.Search for Java, menambahkan
  dokumen ke dalam indeks, dan meningkatkan kinerja retrieval.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Buat Query Boolean Java – Kuasai Pencarian Boolean dengan GroupDocs.Search
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
title: 'Buat Query Boolean Java: Kuasai Pencarian Boolean dengan GroupDocs.Search
  for Java'
type: docs
url: /id/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Buat Kuery Boolean Java: Kuasai Pencarian Boolean dengan GroupDocs.Search untuk Java

Mencari koleksi dokumen yang sangat besar dapat terasa seperti mencari jarum di dalam tumpukan jerami. **Create Boolean Query Java** memungkinkan Anda memberi tahu mesin persis apa yang Anda butuhkan—dokumen yang berisi *kedua* istilah, *salah satu* istilah, atau *mengecualikan* kata yang tidak diinginkan. Dalam panduan ini kami akan menjelaskan cara menyiapkan **GroupDocs.Search for Java**, menambahkan dokumen ke indeks, dan membuat kueri boolean yang kuat yang meningkatkan alur kerja **document retrieval java** Anda. Pada akhir panduan Anda akan dapat menulis kode yang bersih dan dapat dipelihara yang membuat kueri boolean di Java dengan hanya beberapa baris.

## Jawaban Cepat
- **Apa itu kueri boolean AND?** Mengembalikan hanya dokumen yang berisi *semua* istilah yang ditentukan.  
- **Bagaimana OR berbeda dari AND?** OR mencocokkan dokumen dengan *salah satu* istilah, memperluas set hasil.  
- **Kapan saya harus menggunakan NOT?** Gunakan NOT untuk menyaring dokumen yang berisi kata yang tidak diinginkan.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi komersial diperlukan untuk produksi.  
- **Versi Java apa yang diperlukan?** Java 8+ didukung; JDK 11+ disarankan.

## Apa itu **create boolean query java**?
`create boolean query java` mengacu pada pembuatan kueri pencarian di Java yang menggabungkan operator logika seperti AND, OR, dan NOT menggunakan API GroupDocs.Search. Dengan menyusun operator-operator ini Anda dapat mengontrol secara tepat dokumen mana yang cocok, memungkinkan penyaringan lanjutan, penyesuaian relevansi, dan skenario pencarian yang kompleks.

## Mengapa menggunakan GroupDocs.Search untuk Java?
- **Kinerja tinggi** pada set dokumen besar – dapat mengindeks dan mencari 500 GB teks dalam kurang dari satu menit pada server standar.  
- **API kaya** yang mendukung kueri berbasis teks maupun objek, memungkinkan Anda memilih gaya yang sesuai dengan arsitektur Anda.  
- **Dukungan bahasa bawaan** untuk stemming, stop‑words, dan pencocokan fuzzy pada lebih dari 30 bahasa.  
- **Integrasi mudah** dengan Maven atau unduhan JAR langsung, hanya memerlukan beberapa baris kode untuk memulai.

## Prasyarat
Sebelum memulai, pastikan Anda memiliki:
- **GroupDocs.Search for Java** (v25.4 atau lebih baru) – lihat tautan unduhan di bawah.  
- JDK 8+ terpasang dan dikonfigurasi di IDE Anda (IntelliJ IDEA, Eclipse, dll.).  
- Pengetahuan dasar Java dan Maven untuk manajemen dependensi.  

## Menyiapkan GroupDocs.Search untuk Java

### Pengaturan Maven
Tambahkan repositori dan dependensi ke `pom.xml` Anda:

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
Sebagai alternatif, unduh JAR terbaru dari situs resmi: [rilisan GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Mulailah dengan lisensi percobaan gratis untuk menjelajahi semua fitur. Untuk penggunaan produksi, beli lisensi komersial untuk membuka semua fungsi.

### Inisialisasi dan Penyiapan Dasar
Buat folder indeks dan buat instance objek `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Bagaimana cara membuat boolean query java?
`Index` class mewakili koleksi dokumen yang dapat dicari yang disimpan di disk. `BooleanQuery` menggabungkan beberapa sub‑kueri dengan operator logika. `createAndQuery`, `createOrQuery`, dan `createNotQuery` membangun sub‑kueri AND, OR, dan NOT masing‑masing. Muat atau buat instance `Index`, tambahkan dokumen, lalu bangun objek `BooleanQuery` menggunakan `createAndQuery`, `createOrQuery`, atau `createNotQuery`. Panggil `index.search(query)` untuk mengambil dokumen yang cocok. Pola ini bekerja untuk skenario sederhana maupun kompleks dan hanya memerlukan tiga langkah logis: inisialisasi indeks, penambahan dokumen, dan eksekusi kueri.

## Pencarian Boolean AND

### Gambaran Umum
Kueri AND mempersempit hasil, meningkatkan relevansi ketika Anda membutuhkan dokumen yang memenuhi beberapa kriteria.

### Langkah Implementasi
1. **Inisialisasi Indeks** – ini juga menunjukkan **menambahkan dokumen ke indeks** untuk skenario AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Indeks Dokumen**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Lakukan Pencarian Kuery Teks** – menggunakan sintaks string biasa.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Lakukan Pencarian Kuery Objek** – berguna saat membangun kueri secara programatis (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Pencarian Boolean OR

### Gambaran Umum
Kueri OR ideal untuk pencarian eksploratif di mana Anda ingin menangkap dokumen yang berisi setidaknya satu dari beberapa kata kunci (**search with or java**).

### Langkah Implementasi
1. **Inisialisasi Indeks**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Indeks Dokumen**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Lakukan Pencarian Kuery Teks**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Lakukan Pencarian Kuery Objek**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Pencarian Boolean NOT

### Gambaran Umum
Kueri NOT membantu Anda menghilangkan dokumen yang tidak relevan, seperti menyaring nama merek pesaing (**boolean search examples java**).

### Langkah Implementasi
1. **Inisialisasi Indeks**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Indeks Dokumen**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Lakukan Pencarian Kuery Teks**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Lakukan Pencarian Kuery Objek**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Kueri Boolean Kompleks

### Gambaran Umum
Kueri kompleks memungkinkan Anda memodelkan skenario pencarian dunia nyata, seperti “temukan artikel olahraga yang menguntungkan tetapi mengecualikan penyebutan atlet tertentu”.

### Langkah Implementasi
1. **Inisialisasi Indeks**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Indeks Dokumen**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Lakukan Pencarian Kuery Teks**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Lakukan Pencarian Kuery Objek**

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

## Aplikasi Praktis dari Kueri **java boolean and or**
- **Sistem Manajemen Dokumen** – temukan kontrak yang berisi baik “confidential” **AND** “renewal”.  
- **Penelitian Hukum** – saring kasus hukum dengan **AND**/ **OR** sambil mengecualikan undang‑undang usang menggunakan **NOT**.  
- **Dukungan Pelanggan** – ambil tiket yang menyebut “login” **AND** “error” tetapi tidak “resolved”.  
- **Kurasi Konten** – kumpulkan posting blog tentang “cloud” **OR** “serverless” untuk buletin.

## Kesalahan Umum & Pemecahan Masalah
- **Kehilangan Penyegaran Indeks** – setelah menambahkan dokumen baru, panggil `index.update()` untuk memastikan mereka dapat dicari.  
- **Spasi Operator Tidak Tepat** – GroupDocs.Search mengharapkan spasi di sekitar operator (`AND`, `OR`, `NOT`).  
- **Sensitivitas Huruf** – kueri tidak sensitif huruf secara default, tetapi analis khusus dapat memengaruhi hal ini.  
- **Set Hasil Besar** – gunakan paginasi (`search(query, 0, 100)`) untuk menghindari kelebihan memori.  

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggabungkan lebih dari dua istilah dalam kueri AND?**  
A: Tentu saja. Anda dapat menautkan beberapa objek `createWordQuery` dengan `createAndQuery`, atau cukup menulis `"term1 AND term2 AND term3"` dalam kueri teks.

**Q: Apakah GroupDocs.Search mendukung pencarian wildcard atau fuzzy?**  
A: Ya. Tambahkan `*` untuk wildcard (mis., `promot*`) atau gunakan `~` untuk pencocokan fuzzy (mis., `comfort~`).

**Q: Bagaimana cara membatasi pencarian ke tipe file tertentu?**  
`FileTypeQuery` membatasi hasil pencarian ke format file tertentu seperti PDF atau DOCX.  
A: Gunakan kelas `FileTypeQuery` untuk membatasi hasil ke PDF, DOCX, dll., dan gabungkan dengan kueri boolean Anda.

**Q: Apa cara terbaik untuk memantau kinerja pengindeksan?**  
A: Aktifkan logger bawaan (`index.getLogger().setLevel(Level.INFO)`) dan tinjau metrik waktu setelah setiap operasi `add`.

**Q: Apakah ada cara untuk meningkatkan relevansi istilah tertentu?**  
`BoostQuery` meningkatkan skor relevansi istilah yang ditentukan dalam kueri pencarian.  
A: Ya. Bungkus kata penting dengan `BoostQuery` untuk meningkatkan bobotnya dalam algoritma penilaian.

---

**Terakhir Diperbarui:** 2026-07-21  
**Diuji Dengan:** GroupDocs.Search 25.4 (Java)  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Operator Boolean Java – Buat Indeks Pencarian & Pencarian Faceted](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Kuasi GroupDocs.Search Java&#58; Pencarian Dokumen Efisien dan Manajemen Indeks](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Menguasai GroupDocs.Search Java – Buat dan Kelola Indeks Pencarian](/search/java/indexing/groupdocs-search-java-create-index-guide/)