---
date: '2026-05-28'
description: Pelajari cara mencari frasa dengan pola wildcard menggunakan GroupDocs.Search
  untuk Java. Termasuk membuat indeks pencarian, menambahkan dokumen, dan mengeksekusi
  kueri frasa tepat serta wildcard.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Cara Mencari Frasa dengan Wildcard di GroupDocs.Search untuk Java
type: docs
url: /id/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Cara Mencari Frasa dengan Wildcard di GroupDocs.Search untuk Java

Dalam aplikasi modern yang berfokus pada dokumen, **how to search phrase** dengan cepat dan akurat menjadi faktor penentu pengalaman pengguna. Baik Anda membangun basis pengetahuan, katalog e‑commerce, atau repositori yang berorientasi kepatuhan, kemampuan untuk menemukan frasa tepat—atau variasi fleksibel darinya—menjaga produktivitas pengguna dan mengurangi beban dukungan. Tutorial ini memandu Anda melalui instalasi **GroupDocs.Search for Java**, pembuatan indeks pencarian, pemuatan dokumen, dan menjalankan kueri frasa tepat serta kueri yang ditingkatkan dengan wildcard, semuanya dengan contoh kode yang jelas dan siap produksi.

## Jawaban Cepat
- **Apa manfaat utama pencarian frasa?** Pencocokan tepat urutan kata dan kedekatan, menjamin bahwa hanya dokumen yang berisi urutan tepat yang dikembalikan.  
- **Apakah wildcard dapat digunakan di dalam frasa?** Ya—wildcard memungkinkan Anda melewatkan atau mengganti kata sambil mempertahankan urutan keseluruhan.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Uji coba gratis dapat digunakan untuk pengujian; lisensi penuh diperlukan untuk penerapan produksi.  
- **Versi Maven mana yang harus saya gunakan?** Rilis terbaru GroupDocs.Search for Java (misalnya, 25.4 pada saat penulisan).  
- **Apakah pendekatan ini cocok untuk kumpulan dokumen besar?** Tentu—GroupDocs.Search dapat menangani koleksi dokumen ratusan ribu dengan latensi kueri sub‑detik ketika indeks dioptimalkan.

## Apa itu “how to search phrase”?
**Mencari frasa berarti mencari urutan kata tertentu dalam sebuah dokumen.**  
Saat Anda menjalankan kueri frasa, mesin memeriksa bahwa kata‑kata muncul dalam urutan tepat dan dalam kedekatan yang ditentukan, menghilangkan hasil yang tidak relevan yang berisi kata‑kata yang sama dalam konteks berbeda. Hal ini membuat pencarian frasa ideal untuk menemukan klausa hukum, kode produk, atau teks apa pun di mana urutan penting.

## Mengapa Menggunakan GroupDocs.Search untuk Kueri Frasa dan Wildcard?
GroupDocs.Search menyediakan **pengindeksan berkecepatan tinggi hingga 1 juta dokumen sambil mempertahankan waktu respons kueri sub‑detik** pada perangkat keras server standar. Bahasa kueri-nya mendukung frasa tepat, wildcard sederhana `*` dan `?`, serta pola lanjutan seperti rentang numerik (`*2~5`). Perpustakaan ini terintegrasi dengan aplikasi Java apa pun melalui Maven atau unduhan JAR langsung, dan berjalan pada Java 8+ tanpa layanan eksternal.

## Prasyarat
- Java 8 atau lebih baru (Java 11 LTS disarankan).  
- Maven 3 atau lebih baru (jika Anda lebih suka manajemen dependensi).  
- Pemahaman dasar tentang struktur proyek Java dan konsep berorientasi objek.  

## Menyiapkan GroupDocs.Search untuk Java

### Menggunakan Maven
Tambahkan repositori resmi dan dependensi GroupDocs.Search ke `pom.xml` Anda:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Unduhan Langsung
Alternatifnya, unduh JAR terbaru dari halaman rilis resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Free Trial:** Ideal untuk percobaan cepat; terbatas pada 100 MB data terindeks.  
- **Temporary License:** Minta kunci evaluasi 30‑hari dari portal GroupDocs.  
- **Full License:** Diperlukan untuk penggunaan produksi dan kapasitas pengindeksan tak terbatas.

## Inisialisasi dan Pengaturan Dasar
Buat folder yang akan menyimpan file indeks dan buat instance objek `Index`. Kelas `Index` mewakili indeks yang dapat dicari yang disimpan di disk dan menyediakan metode untuk menambah, memperbarui, dan mengkueri dokumen.

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

Tambahkan dokumen yang ingin Anda jadikan dapat dicari:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Cara Mencari Frasa dengan Wildcard di GroupDocs.Search
Bagian ini menunjukkan tiga tingkat pencarian frasa—cocok tepat, wildcard sederhana, dan pola wildcard lanjutan—menunjukkan cara membuat indeks, menambah dokumen, dan mengeksekusi setiap tipe kueri dengan kode Java yang ringkas. Contoh-contoh menggambarkan kueri berbasis teks maupun konstruksi kueri berbasis objek, memungkinkan pengembang mengintegrasikan kemampuan pencarian fleksibel ke dalam aplikasi mereka.

### Pencarian Frasa Sederhana

#### Ikhtisar
Gunakan pendekatan ini ketika Anda membutuhkan **cocok tepat** dari urutan kata, seperti klausa hukum atau nomor model produk.

#### Jawaban Langsung
Muat indeks, panggil `search` dengan frasa dalam tanda kutip (mis., `"quick brown fox"`), dan mesin mengembalikan hanya dokumen yang berisi urutan tepat tersebut, mempertahankan urutan kata dan spasi. Kueri dijalankan dalam milidetik, bahkan pada indeks yang berisi ratusan ribu file.

#### Langkah 1: Buat Indeks
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Langkah 2: Tambahkan Dokumen ke Indeks
```java
Index index = new Index(indexFolder);
```

#### Langkah 3: Cari Frasa Spesifik (Bentuk Teks)
```java
index.add(documentsFolder);
```

#### Langkah 4: Kueri Berbasis Objek (Cari Frasa Tepat)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Pencarian Frasa dengan Wildcard

#### Ikhtisar
Placeholder wildcard (`*` untuk sejumlah karakter apa pun, `?` untuk satu karakter) memungkinkan Anda **melewatkan kata variabel** sambil tetap menegakkan urutan di sekitarnya.

#### Jawaban Langsung
Sisipkan token wildcard (`*`) di dalam frasa yang diapit tanda kutip—mis., `"quick * fox"`—untuk mencocokkan kata apa pun antara *quick* dan *fox*. Mesin memperluas wildcard pada saat kueri, memindai hanya istilah terindeks yang memenuhi pola, sehingga kinerja tetap sebanding dengan kueri frasa biasa.

#### Langkah 1: Buat Indeks
*(Sama seperti Pencarian Frasa Sederhana.)*

#### Langkah 2: Tambahkan Dokumen ke Indeks
*(Sama seperti di atas.)*

#### Langkah 3: Pencarian Bentuk Teks dengan Wildcard
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Langkah 4: Kueri Berbasis Objek dengan Wildcard (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Pencarian Wildcard Lanjutan

#### Ikhtisar
Gabungkan rentang numerik, karakter opsional, dan pola mirip regex khusus untuk **pencocokan canggih**, seperti nomor versi atau kode produk.

#### Jawaban Langsung
Gunakan sintaks wildcard diperluas `*min~max` untuk mendefinisikan rentang jarak kata yang diizinkan, atau `?` untuk mencocokkan satu karakter. Misalnya, `"error *2~5 code"` menemukan kata *error* diikuti oleh dua hingga lima kata apa pun dan kemudian *code*. Presisi ini mengurangi hasil positif palsu sambil tetap menawarkan fleksibilitas.

#### Langkah 1: Buat Indeks
*(Diulang untuk kejelasan.)*

#### Langkah 2: Tambahkan Dokumen ke Indeks
*(Diulang.)*

#### Langkah 3: Pencarian Bentuk Teks dengan Pola Wildcard Kompleks
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Langkah 4: Kueri Berbasis Objek dengan Wildcard Lanjutan
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Aplikasi Praktis
- **Sistem Manajemen Konten:** Editor dapat menemukan klausa tepat atau kutipan fleksibel tanpa harus memindai ratusan halaman secara manual.  
- **Katalog E‑commerce:** Pembeli menemukan produk bahkan ketika mereka menghilangkan deskripsi atau menggunakan sinonim, berkat toleransi wildcard.  
- **Legal & Compliance:** Dengan cepat mengisolasi bahasa kontrak yang mungkin muncul dengan variasi kecil di seluruh perjanjian.  

## Pertimbangan Kinerja
- **Buat Indeks Pencarian** hanya sekali per set dokumen stabil; gunakan kembali instance `Index` yang sama untuk semua kueri.  
- **Tambahkan Dokumen Secara Inkremen** saat file baru tiba—hindari membangun ulang seluruh indeks untuk menjaga penggunaan CPU tetap rendah.  
- **Rancang Pola Wildcard yang Tepat**; pola yang lebih luas (`*`) meningkatkan jumlah ekspansi istilah dan dapat meningkatkan beban CPU.  
- **Panggil `index.optimize()`** secara berkala (jika didukung) untuk memadatkan indeks dan menjaga konsumsi memori tetap terkendali.  

## Masalah Umum & Solusi
| Issue | Solution |
|-------|----------|
| Tidak ada hasil yang dikembalikan untuk kueri wildcard | Verifikasi sintaks wildcard (`*min~max`) dan pastikan kata target ada dalam jarak yang ditentukan. |
| Indeks menjadi usang setelah pembaruan file | Gunakan `index.add(updatedFolder)` atau API pembaruan inkremen untuk menyegarkan hanya file yang berubah. |
| Konsumsi memori tinggi pada dataset besar | Tingkatkan heap JVM (`-Xmx4g` atau lebih) dan pertimbangkan membagi indeks menjadi beberapa shard untuk pemrosesan paralel. |

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara wildcard dan pencarian frasa?**  
A: Pencarian frasa memerlukan urutan kata dan spasi yang tepat, sementara wildcard memungkinkan Anda mengganti atau melewatkan kata dalam urutan tersebut, menawarkan pencocokan fleksibel.

**Q: Apakah saya dapat menggunakan wildcard dengan data numerik dalam pencarian?**  
A: Ya—parameter rentang wildcard (`*min~max`) berfungsi dengan angka maupun kata, memungkinkan kueri seperti `"version *1~3"`.

**Q: Bagaimana saya harus menangani koleksi dokumen yang sangat besar?**  
A: Pertahankan indeks teroptimasi, lakukan pembaruan inkremen, dan buat pola wildcard spesifik untuk membatasi ekspansi istilah. GroupDocs.Search dapat mengindeks 1 juta dokumen sambil menjaga latensi kueri di bawah 200 ms pada perangkat keras standar.

**Q: Apakah GroupDocs.Search cocok untuk skenario pencarian waktu nyata?**  
A: Tentu—setelah indeks dibangun, kueri dijalankan dalam milidetik, menjadikannya ideal untuk kotak pencarian interaktif dan fitur auto‑complete.

**Q: Apakah saya dapat mengintegrasikan perpustakaan ini ke dalam proyek Java yang ada?**  
A: Ya. Tambahkan dependensi Maven atau JAR, buat instance `Index` seperti yang ditunjukkan, dan Anda siap melakukan kueri tanpa mengubah kode yang ada.

---

**Terakhir Diperbarui:** 2026-05-28  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Tutorial Terkait

- [Buat Indeks Pencarian Java – Tutorial GroupDocs.Search](/search/java/)
- [Tambahkan Dokumen ke Indeks – Tutorial GroupDocs.Search Java](/search/java/document-management/)
- [Buat Indeks Pencarian - Tutorial GroupDocs.Search Java](/search/java/advanced-features/)