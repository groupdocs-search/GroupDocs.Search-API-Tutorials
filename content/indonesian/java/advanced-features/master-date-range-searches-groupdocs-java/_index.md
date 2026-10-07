---
date: '2026-10-07'
description: Pelajari cara mengimplementasikan pencarian format tanggal khusus java
  dengan GroupDocs, mencakup kueri rentang tanggal, pola khusus, dan tips kinerja.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: Tutorial format tanggal khusus java menunjukkan cara mengonfigurasi
  GroupDocs.Search untuk Java, menjalankan kueri rentang tanggal, dan meningkatkan
  kinerja. Ikuti contoh langkah demi langkah.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Format tanggal khusus java – panduan pencarian rentang tanggal dengan GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Format tanggal khusus java | pencarian rentang tanggal dengan GroupDocs
type: docs
url: /id/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Format tanggal khusus java | pencarian rentang tanggal dengan GroupDocs

Mencari dokumen berdasarkan tanggal adalah kebutuhan yang sering—baik Anda sedang membangun sistem arsip, alat pelaporan keuangan, atau portal manajemen konten. Dalam tutorial ini Anda akan mempelajari teknik **custom date format java** menggunakan GroupDocs.Search, mencakup kueri rentang tanggal, definisi pola khusus, dan tips untuk **optimize search performance**. Pada akhir tutorial, Anda akan dapat memungkinkan pengguna mengambil catatan yang berada dalam interval tanggal apa pun, terlepas dari format yang mereka gunakan.

## Jawaban Cepat
- **Apa kelas utama untuk pengindeksan?** `Index` from the `com.groupdocs.search` package.  
- **Bagaimana cara mendefinisikan pola tanggal khusus?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Bisakah saya mencari dengan kueri teks?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Koordinat Maven apa yang diperlukan?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Apakah saya memerlukan lisensi untuk pengembangan?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## Apa itu custom date format java?
Custom date format java memberi tahu GroupDocs.Search cara menginterpretasikan string tanggal yang tidak mengikuti pola ISO default (YYYY‑MM‑DD). Dengan mendefinisikan pola Anda sendiri—seperti `MM/dd/yyyy` atau `dd‑MM‑yyyy`—Anda memungkinkan mesin mengenali tanggal yang tertanam dalam dokumen yang menggunakan format regional atau warisan. Kemampuan ini memungkinkan Anda mengindeks dan mengkueri tanggal secara konsisten di seluruh sumber yang heterogen, meningkatkan baik recall maupun precision untuk pencarian yang berfokus pada tanggal.

## Mengapa menggunakan GroupDocs.Search untuk kueri rentang tanggal?
GroupDocs.Search menggabungkan pengindeksan berkecepatan tinggi dengan konstruksi kueri yang fleksibel, menjadikannya ideal untuk skenario rentang tanggal. Mesin dapat dengan cepat menemukan dokumen yang berisi tanggal dalam interval tertentu, bahkan ketika tanggal tersebut muncul dalam teks bebas atau bidang metadata. Dukungan bawaan untuk banyak format file dan parser tanggal yang dapat disesuaikan berarti Anda dapat menangani koleksi dokumen yang beragam tanpa menulis kode khusus format, sambil tetap mencapai waktu respons sub‑detik pada indeks besar.

## Cara mencari dokumen berdasarkan tanggal dengan GroupDocs.Search
Anda akan menyiapkan pustaka, mengindeks folder contoh, dan kemudian menjalankan baik kueri bentuk teks sederhana maupun kueri berbasis objek yang lebih kaya. Proses dimulai dengan membuat instance `Index`, mengkonfigurasi format tanggal khusus yang Anda perlukan, dan kemudian memanggil API pencarian dengan string biasa atau `SearchQuery` terstruktur. Pendekatan ini memungkinkan Anda memilih tingkat kontrol yang sesuai dengan kebutuhan aplikasi Anda.

### Prasyarat
- Java 8 atau yang lebih baru terpasang.  
- Maven untuk manajemen dependensi.  
- Akses ke lisensi GroupDocs.Search (trial atau sementara cukup untuk pengembangan).  

### Menyiapkan GroupDocs.Search untuk Java

#### Instalasi menggunakan Maven
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

#### Unduhan langsung
Sebagai alternatif, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Inisialisasi dan pengaturan dasar
Buat instance `Index` dan tambahkan dokumen Anda:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Penanda definisi:** Kelas `Index` adalah kontainer inti yang menyimpan metadata yang dapat dicari untuk setiap file yang Anda tambahkan, memungkinkan pencarian cepat di seluruh koleksi besar.

## Fitur 1: membuat kueri pencarian rentang tanggal

### Menggunakan kueri bentuk teks
Cara paling sederhana adalah menyisipkan rentang tanggal langsung dalam string kueri:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Jawaban langsung:** Muat indeks Anda, lalu panggil `search("daterange(2022-01-01 ~~ 2022-12-31)")` untuk mengambil setiap dokumen yang tanggal terindeksnya berada antara 1 Januari 2022 dan 31 Desember 2022. Kueri satu baris ini berfungsi langsung dan mengembalikan hasil yang diurutkan berdasarkan relevansi.

**Penjelasan:** Sintaks `daterange` mengharapkan tanggal dalam format `YYYY‑MM‑DD`. Ia mengembalikan semua dokumen yang tanggal terindeksnya berada dalam interval tersebut.

### Menggunakan objek kueri
Untuk kontrol programatik dan parsing khusus, bangun objek `SearchQuery`. Kelas `SearchQuery` mewakili kueri terstruktur yang dapat menggabungkan beberapa kriteria seperti kata kunci, filter, dan rentang tanggal.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Jawaban langsung:** Buat `SearchQuery` dengan `createDateRangeQuery(startDate, endDate)` dimana `startDate` dan `endDate` adalah instance `java.util.Date`; kemudian berikan kueri tersebut ke `index.search(query)` untuk mendapatkan hasil yang tepat yang menghormati offset zona waktu dan kalender spesifik locale.

**Penanda definisi:** Kelas `SearchQuery` mengenkapsulasi semua kriteria pencarian, memungkinkan Anda menggabungkan rentang tanggal dengan filter kata kunci, operator Boolean, dan aturan boosting.

**Penjelasan:** `createDateRangeQuery` memungkinkan Anda menyediakan objek `java.util.Date`, memberi Anda fleksibilitas penuh atas zona waktu dan penanganan spesifik locale.

## Fitur 2: menentukan pola custom date format java

### Menetapkan format tanggal khusus
Kelas `DateFormat` memberi tahu mesin cara memecah dan menginterpretasikan string tanggal berdasarkan urutan elemen dan karakter pemisah. Definisikan `DateFormat` yang cocok dengan representasi tanggal dokumen Anda:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Jawaban langsung:** Hapus format default dengan `dateFormat.clear()`, lalu tambahkan `DateFormat` baru yang dibangun dari objek `DateFormatElement` (bulan, hari, tahun) dan atur pemisah menjadi `/`. Setelah ini, mesin akan secara benar mengurai tanggal yang ditulis sebagai `MM/dd/yyyy` selama proses pengindeksan dan kueri.

**Penanda definisi:** `DateFormat` adalah objek konfigurasi yang memberi tahu GroupDocs.Search cara memecah dan menginterpretasikan string tanggal berdasarkan urutan elemen dan karakter pemisah.

**Penjelasan:** Dengan menghapus format default dan menambahkan `DateFormat` yang menggunakan `/` sebagai pemisah, mesin kini memahami tanggal yang ditulis sebagai `MM/dd/yyyy`. Ini penting untuk **search documents by date** di wilayah yang lebih menyukai notasi bulan‑dulu.

## Tips untuk mengoptimalkan kinerja pencarian
- **Index incrementally:** Tambahkan file baru ke indeks yang ada alih‑alih membangun ulang dari awal; ini mengurangi penggunaan CPU hingga 70 % untuk pembaruan harian.  
- **Prune stale data:** Secara berkala hapus dokumen yang tidak lagi diperlukan; indeks yang ramping meningkatkan tingkat hit cache dan mengurangi latensi kueri.  
- **Adjust memory settings:** Tingkatkan heap JVM (`-Xmx4g` atau lebih tinggi) saat bekerja dengan indeks lebih besar dari 5 GB untuk menghindari error out‑of‑memory.  
- **Enable multi‑threaded indexing:** Gunakan `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` untuk memparalelkan pemrosesan dokumen dan mengurangi waktu pengindeksan sekitar jumlah core CPU.

## Masalah umum dan solusi
- **Date parsing errors:** Verifikasi bahwa string tanggal dokumen persis cocok dengan pola khusus yang Anda definisikan; pemisah yang tidak cocok atau nol di depan yang hilang menyebabkan kegagalan.  
- **Missing results:** Pastikan bidang yang diindeks berisi metadata tanggal; jika dokumen hanya memiliki tanggal dalam paragraf teks bebas, aktifkan opsi `ExtractDateMetadata` selama pengindeksan.  
- **Index access exceptions:** Pastikan jalur `indexFolder` dapat ditulis dan tidak terkunci oleh proses lain; gunakan folder khusus per lingkungan (dev, test, prod) untuk menghindari konflik.

## Aplikasi praktis
1. **Archival systems** – Ambil catatan dari periode historis tertentu tanpa harus menormalkan tanggal secara manual.  
2. **Content management** – Dukung format tanggal regional seperti `dd/MM/yyyy` untuk audiens Eropa, meningkatkan kepuasan pengguna.  
3. **Financial software** – Filter transaksi berdasarkan kuartal atau tahun fiskal dengan cepat, memungkinkan dasbor pelaporan real‑time.

## Mengapa ini penting
Menerapkan penanganan **custom date format java** menghilangkan gesekan dalam menangani representasi tanggal yang tidak konsisten di seluruh dokumen. Ini memungkinkan Anda **handle multiple date formats** dalam satu indeks, memastikan bahwa pengguna akhir mendapatkan hasil yang akurat tidak peduli bagaimana tanggal awalnya dicatat. Fleksibilitas ini meningkatkan relevansi pencarian, mengurangi upaya pra‑pemrosesan, dan memperpendek waktu‑ke‑nilai untuk aplikasi yang berfokus pada tanggal.

## Langkah selanjutnya
- Jelajahi kombinasi kueri lanjutan menggunakan operator `AND`, `OR`, dan `NOT`.  
- Bereksperimen dengan analyzer khusus jika Anda perlu mengindeks metadata temporal tambahan seperti timestamp yang tertanam dalam tag XML.  
- Tinjau panduan penyetelan kinerja dalam dokumentasi resmi untuk menskalakan solusi Anda ke jutaan dokumen dan lingkungan multi‑tenant.

## Pertanyaan yang sering diajukan

**Q: Apa perbedaan antara kueri bentuk teks dan kueri tanggal berbasis objek?**  
A: Bentuk teks cepat dan mudah tetapi terbatas pada format ISO default; kueri berbasis objek memungkinkan Anda menyediakan objek `Date` dan format khusus untuk fleksibilitas lebih besar.

**Q: Bisakah saya mencari beberapa rentang tanggal dalam satu kueri?**  
A: Ya, gabungkan klausa `daterange` dengan operator logika seperti `AND` atau `OR` untuk membangun kueri kompleks.

**Q: Apakah format tanggal khusus memperlambat pencarian?**  
A: Ada overhead kecil untuk parsing tambahan, tetapi dampaknya tidak signifikan untuk beban kerja tipikal dan terbayar oleh peningkatan akurasi.

**Q: Apakah GroupDocs.Search cocok untuk penyebaran skala besar?**  
A: Tentu saja. Dengan strategi pengindeksan yang tepat dan penyetelan JVM, ia dapat menskalakan hingga jutaan dokumen sambil mempertahankan waktu respons kueri sub‑detik.

**Q: Di mana saya dapat menemukan contoh Java lebih banyak?**  
A: Jelajahi [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) untuk contoh tambahan dan implementasi kasus penggunaan.

---

**Resources**

- **Dokumentasi:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Referensi API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Unduh:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **Repositori GitHub:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Lihat di GitHub:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum dukungan gratis:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Lisensi sementara:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-10-07  
**Diuji Dengan:** GroupDocs.Search Java 25.4  
**Penulis:** GroupDocs  

## Tutorial Terkait

- [Fitur Pencarian Lanjutan Groupdocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Perpustakaan Pencarian Teks Penuh Java – Optimalkan Indeks dengan GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Cara menambahkan dokumen ke indeks dengan Metadata Indexing di Java menggunakan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)