---
date: '2025-12-18'
description: Pelajari cara mengimplementasikan pencarian Java dengan format tanggal
  khusus menggunakan GroupDocs.Search, termasuk kueri rentang tanggal, pola khusus,
  dan tips kinerja.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'Format Tanggal Kustom Java: Pencarian Rentang Tanggal dengan GroupDocs'
type: docs
url: /id/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Format Tanggal Kustom Java: Pencarian Rentang Tanggal dengan GroupDocs

Mencari dokumen berdasarkan tanggal adalah kebutuhan yang sering—baik Anda membangun sistem arsip, alat pelaporan keuangan, atau portal manajemen konten. Dalam tutorial ini Anda akan mempelajari teknik **custom date format java** menggunakan GroupDocs.Search, mencakup kueri rentang tanggal, definisi pola kustom, dan tips untuk **mengoptimalkan kinerja pencarian**. Pada akhir tutorial, Anda dapat memungkinkan pengguna mengambil catatan yang berada dalam interval tanggal apa pun, terlepas dari format yang mereka gunakan.

## Jawaban Cepat
- **Apa kelas utama untuk pengindeksan?** `Index` dari paket `com.groupdocs.search`.  
- **Bagaimana cara mendefinisikan pola tanggal kustom?** Gunakan `DateFormat` dengan objek `DateFormatElement` dan pemisah.  
- **Apakah saya dapat mencari dengan kueri teks?** Ya, sintaks `daterange(start ~~ end)` bekerja langsung dalam string kueri.  
- **Koordinat Maven apa yang diperlukan?** `com.groupdocs:groupdocs-search:25.4` (atau yang lebih baru).  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi percobaan gratis atau lisensi sementara sudah cukup untuk pengujian; lisensi komersial diperlukan untuk produksi.

## Apa itu **custom date format java**?
Sebuah **custom date format java** memberi tahu GroupDocs.Search cara menginterpretasikan string tanggal yang tidak mengikuti pola ISO default (YYYY‑MM‑DD). Dengan mendefinisikan pola Anda sendiri—seperti `MM/dd/yyyy` atau `dd‑MM‑yyyy`—Anda memungkinkan mesin mengenali tanggal yang tertanam dalam dokumen yang menggunakan format regional atau warisan.

## Mengapa menggunakan GroupDocs.Search untuk kueri rentang tanggal?
- **Kecepatan:** Pengindeksan bawaan membuat pencarian menjadi O(log n).  
- **Fleksibilitas:** Mendukung pembuatan kueri berbasis teks maupun objek.  
- **Dukungan multi‑format:** Menangani PDF, Word, Excel, teks biasa, dan lainnya tanpa kode tambahan.  

## Cara **search documents by date** dengan GroupDocs.Search
Di bawah ini Anda akan menemukan panduan langkah‑demi‑langkah yang memandu Anda menyiapkan pustaka, mengindeks file, dan mengeksekusi pencarian rentang tanggal sederhana maupun lanjutan.

### Prasyarat
- Java 8 atau yang lebih baru terpasang.  
- Maven untuk manajemen dependensi.  
- Akses ke lisensi GroupDocs.Search (percobaan atau sementara cukup untuk pengembangan).  

### Menyiapkan GroupDocs.Search untuk Java

#### Instalasi Menggunakan Maven
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

#### Unduh Langsung
Sebagai alternatif, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Inisialisasi dan Penyiapan Dasar
Create an `Index` instance and add your documents:

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
The simplest way is to embed the date range directly in the query string:

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

**Penjelasan**: Sintaks `daterange` mengharapkan tanggal dalam format `YYYY‑MM‑DD`. Ini mengembalikan semua dokumen yang tanggal terindeksnya berada dalam interval tersebut.

### Menggunakan Objek Kueri
For programmatic control and custom parsing, build a `SearchQuery` object:

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

**Penjelasan**: `createDateRangeQuery` memungkinkan Anda menyediakan objek `java.util.Date`, memberi fleksibilitas penuh atas zona waktu dan penanganan spesifik lokal.

## Fitur 2: Menentukan Pola **custom date format java**

### Menetapkan Format Tanggal Kustom
Define a `DateFormat` that matches your document’s date representation:

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
- **Indeks Secara Inkremental**: Tambahkan file baru ke indeks yang ada alih-alih membangun ulang dari awal.  
- **Potong Data Usang**: Secara berkala hapus dokumen yang tidak lagi diperlukan.  
- **Sesuaikan Pengaturan Memori**: Tingkatkan heap JVM (`-Xmx`) saat bekerja dengan indeks besar.  

## Masalah Umum dan Solusinya
- **Kesalahan Parsing Tanggal**: Pastikan string tanggal dalam dokumen persis cocok dengan pola kustom yang Anda definisikan.  
- **Hasil Tidak Muncul**: Pastikan bidang yang diindeks berisi metadata tanggal; jika tidak, mesin tidak dapat mencocokkan kueri tanggal.  
- **Pengecualian Akses Indeks**: Pastikan jalur `indexFolder` dapat ditulisi dan tidak terkunci oleh proses lain.

## Aplikasi Praktis
1. **Sistem Arsip** – Mengambil catatan dari periode historis tertentu.  
2. **Manajemen Konten** – Mendukung format tanggal regional seperti `dd/MM/yyyy` untuk audiens Eropa.  
3. **Perangkat Lunak Keuangan** – Menyaring transaksi berdasarkan kuartal fiskal atau tahun dengan cepat.

## Kesimpulan
Anda kini memiliki kotak alat **custom date format java** lengkap untuk membangun pencarian rentang tanggal yang kuat dengan GroupDocs.Search. Terapkan pola-pola ini, sesuaikan kinerja, dan aplikasi Anda akan memberikan hasil yang cepat dan akurat untuk setiap kueri temporal.

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara kueri bentuk teks dan kueri berbasis objek?**  
A: Bentuk teks cepat dan mudah tetapi terbatas pada format ISO default; kueri berbasis objek memungkinkan Anda menyediakan objek `Date` dan format kustom untuk fleksibilitas lebih besar.

**Q: Bisakah saya mencari beberapa rentang tanggal dalam satu kueri?**  
A: Ya, gabungkan klausa `daterange` dengan operator logika seperti `AND` atau `OR` untuk membangun kueri kompleks.

**Q: Apakah format tanggal kustom memperlambat pencarian?**  
A: Ada overhead kecil untuk parsing tambahan, tetapi dampaknya dapat diabaikan untuk beban kerja tipikal dan terbayar oleh peningkatan akurasi.

**Q: Apakah GroupDocs.Search cocok untuk penerapan skala besar?**  
A: Tentu saja. Dengan strategi pengindeksan yang tepat dan penyesuaian JVM, ia dapat menangani jutaan dokumen.

**Q: Di mana saya dapat menemukan contoh Java lainnya?**  
A: Jelajahi [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) untuk contoh tambahan dan implementasi kasus penggunaan.

---

**Sumber Daya**

- **Dokumentasi**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Referensi API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Unduh**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **Repositori GitHub**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum Dukungan Gratis**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Lisensi Sementara**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2025-12-18  
**Diuji Dengan:** GroupDocs.Search Java 25.4  
**Penulis:** GroupDocs