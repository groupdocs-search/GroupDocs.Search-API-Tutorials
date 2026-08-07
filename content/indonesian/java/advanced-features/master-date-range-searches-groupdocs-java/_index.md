---
date: '2026-03-04'
description: Pelajari cara mengimplementasikan pencarian format tanggal khusus di
  Java dengan GroupDocs.Search, mencakup kueri rentang tanggal, pola khusus, dan tips
  kinerja.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: Format Tanggal Kustom Java | Pencarian Rentang Tanggal dengan GroupDocs
type: docs
url: /id/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Custom Date Format Java | Pencarian Rentang Tanggal dengan GroupDocs

Mencari dokumen berdasarkan tanggal adalah kebutuhan yang sering—baik Anda sedang membangun sistem arsip, alat pelaporan keuangan, atau portal manajemen konten. Dalam tutorial ini Anda akan mempelajari teknik **custom date format java** menggunakan GroupDocs.Search, mencakup kueri rentang tanggal, definisi pola khusus, dan tips untuk **mengoptimalkan kinerja pencarian**. Pada akhir tutorial, Anda akan dapat memungkinkan pengguna mengambil catatan yang berada dalam interval tanggal apa pun, terlepas dari format yang mereka gunakan.

## Jawaban Cepat
- **Apa kelas utama untuk pengindeksan?** `Index` dari paket `com.groupdocs.search`.  
- **Bagaimana cara mendefinisikan pola tanggal khusus?** Gunakan `DateFormat` dengan objek `DateFormatElement` dan pemisah.  
- **Bisakah saya mencari dengan kueri teks?** Ya, sintaks `daterange(start ~~ end)` bekerja langsung di string kueri.  
- **Koordinat Maven apa yang diperlukan?** `com.groupdocs:groupdocs-search:25.4` (atau yang lebih baru).  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi percobaan atau sementara sudah cukup untuk pengujian; lisensi komersial diperlukan untuk produksi.

## Apa itu **custom date format java**?
Sebuah **custom date format java** memberi tahu GroupDocs.Search cara menafsirkan string tanggal yang tidak mengikuti pola ISO default (YYYY‑MM‑DD). Dengan mendefinisikan pola Anda sendiri—seperti `MM/dd/yyyy` atau `dd‑MM‑yyyy`—Anda memungkinkan mesin mengenali tanggal yang tertanam dalam dokumen yang menggunakan format regional atau warisan.

## Mengapa menggunakan GroupDocs.Search untuk kueri rentang tanggal?
- **Kecepatan:** Pengindeksan bawaan membuat pencarian menjadi O(log n).  
- **Fleksibilitas:** Mendukung pembuatan kueri berbasis teks maupun objek.  
- **Dukungan multi‑format:** Menangani PDF, Word, Excel, teks biasa, dan lainnya tanpa kode tambahan.  

## Cara **search documents by date** dengan GroupDocs.Search
Berikut panduan langkah demi langkah yang memandu Anda menyiapkan pustaka, mengindeks file, dan mengeksekusi pencarian rentang tanggal sederhana maupun lanjutan.

### Prasyarat
- Java 8 atau yang lebih baru terpasang.  
- Maven untuk manajemen dependensi.  
- Akses ke lisensi GroupDocs.Search (percobaan atau sementara cukup untuk pengembangan).  

### Menyiapkan GroupDocs.Search untuk Java

#### Instalasi Menggunakan Maven
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

#### Unduhan Langsung
Sebagai alternatif, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Inisialisasi dan Pengaturan Dasar
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

## Fitur 1: Membuat Kueri Pencarian Rentang Tanggal

### Menggunakan Kueri Bentuk Teks
Cara termudah adalah menyisipkan rentang tanggal langsung di string kueri:

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

**Penjelasan**: Sintaks `daterange` mengharapkan tanggal dalam format `YYYY‑MM‑DD`. Ia mengembalikan semua dokumen yang tanggal terindeksnya berada dalam interval tersebut.

### Menggunakan Objek Kueri
Untuk kontrol programatik dan parsing khusus, bangun objek `SearchQuery`:

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

**Penjelasan**: `createDateRangeQuery` memungkinkan Anda menyediakan objek `java.util.Date`, memberi fleksibilitas penuh atas zona waktu dan penanganan spesifik locale.

## Fitur 2: Menentukan Pola **custom date format java**

### Menetapkan Format Tanggal Khusus
Definisikan `DateFormat` yang cocok dengan representasi tanggal dalam dokumen Anda:

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

**Penjelasan**: Dengan menghapus format default dan menambahkan `DateFormat` yang menggunakan `/` sebagai pemisah, mesin kini memahami tanggal yang ditulis sebagai `MM/dd/yyyy`. Ini penting untuk **search documents by date** di wilayah yang lebih menyukai notasi bulan‑dulu.

## Tips untuk **optimize search performance**
- **Indeks Secara Inkremental**: Tambahkan file baru ke indeks yang sudah ada alih-alih membangun ulang dari awal.  
- **Buang Data Usang**: Secara periodik hapus dokumen yang tidak lagi diperlukan.  
- **Sesuaikan Pengaturan Memori**: Tingkatkan heap JVM (`-Xmx`) saat bekerja dengan indeks besar.  

## Masalah Umum dan Solusinya
- **Kesalahan Parsing Tanggal**: Pastikan string tanggal dalam dokumen persis cocok dengan pola khusus yang Anda definisikan.  
- **Hasil Tidak Muncul**: Pastikan bidang yang diindeks berisi metadata tanggal; jika tidak, mesin tidak dapat mencocokkan kueri tanggal.  
- **Pengecualian Akses Indeks**: Pastikan jalur `indexFolder` dapat ditulisi dan tidak terkunci oleh proses lain.  

## Aplikasi Praktis
1. **Sistem Arsip** – Mengambil catatan dari periode historis tertentu.  
2. **Manajemen Konten** – Mendukung format tanggal regional seperti `dd/MM/yyyy` untuk audiens Eropa.  
3. **Perangkat Lunak Keuangan** – Menyaring transaksi berdasarkan kuartal atau tahun fiskal dengan cepat.  

## Mengapa Ini Penting
Implementasi penanganan **custom date format java** menghilangkan gesekan akibat representasi tanggal yang tidak konsisten di berbagai dokumen. Ini memungkinkan Anda **handle multiple date formats** dalam satu indeks, memastikan pengguna akhir mendapatkan hasil yang akurat tidak peduli bagaimana tanggal awalnya dicatat.

## Langkah Selanjutnya
- Jelajahi kombinasi kueri lanjutan menggunakan operator `AND`, `OR`, dan `NOT`.  
- Bereksperimen dengan analyzer khusus jika Anda perlu mengindeks metadata temporal tambahan.  
- Tinjau panduan penyetelan kinerja dalam dokumentasi resmi untuk menskalakan solusi Anda ke jutaan dokumen.

## Pertanyaan yang Sering Diajukan

**T: Apa perbedaan antara kueri bentuk teks dan kueri berbasis objek?**  
J: Bentuk teks cepat dan mudah tetapi terbatas pada format ISO default; kueri berbasis objek memungkinkan Anda menyediakan objek `Date` dan format khusus untuk fleksibilitas lebih besar.

**T: Bisakah saya mencari beberapa rentang tanggal dalam satu kueri?**  
J: Ya, gabungkan klausa `daterange` dengan operator logika seperti `AND` atau `OR` untuk membangun kueri kompleks.

**T: Apakah format tanggal khusus memperlambat pencarian?**  
J: Ada sedikit overhead untuk parsing tambahan, tetapi dampaknya dapat diabaikan untuk beban kerja tipikal dan terbayar oleh peningkatan akurasi.

**T: Apakah GroupDocs.Search cocok untuk penyebaran skala besar?**  
J: Tentu saja. Dengan strategi pengindeksan yang tepat dan penyesuaian JVM, ia dapat diskalakan hingga jutaan dokumen.

**T: Di mana saya dapat menemukan contoh Java lainnya?**  
J: Jelajahi [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) untuk sampel tambahan dan implementasi kasus penggunaan.

---

**Sumber Daya**

- **Dokumentasi**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Referensi API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Unduhan**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **Repositori GitHub**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum Dukungan Gratis**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Lisensi Sementara**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-03-04  
**Diuji Dengan:** GroupDocs.Search Java 25.4  
**Penulis:** GroupDocs