---
date: '2025-12-16'
description: Pelajari cara melakukan pencarian rentang tanggal dan fitur pencarian
  lanjutan lainnya seperti pencarian berfaset Java menggunakan GroupDocs.Search untuk
  Java, termasuk penanganan kesalahan dan optimisasi kinerja.
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: 'GroupDocs.Search Java: Pencarian Rentang Tanggal & Fitur Lanjutan'
type: docs
url: /id/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

# Menguasai GroupDocs.Search Java: Pencarian Rentang Tanggal & Fitur Lanjutan

Dalam aplikasi yang didorong oleh data saat ini, **date range search** adalah kemampuan inti yang memungkinkan Anda menyaring dokumen berdasarkan periode waktu, secara dramatis meningkatkan relevansi dan kecepatan. Baik Anda membangun portal kepatuhan, katalog e‑commerce, atau sistem manajemen konten, menguasai date range search bersama jenis kueri kuat lainnya akan membuat solusi Anda fleksibel dan tangguh. Panduan ini membawa Anda melalui penanganan error, rangkaian lengkap jenis kueri, dan tips kinerja, semuanya dengan kode Java nyata yang dapat Anda salin‑tempel.

## Jawaban Cepat
- **Apa itu date range search?** Menyaring dokumen yang berisi tanggal dalam interval mulai‑hingga‑akhir yang ditentukan.  
- **Perpustakaan mana yang menyediakannya?** GroupDocs.Search for Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi produksi diperlukan untuk penggunaan komersial.  
- **Bisakah saya menggabungkannya dengan kueri lain?** Ya—gabungkan rentang tanggal dengan kueri boolean, faceted, atau regex.  
- **Apakah cepat untuk dataset besar?** Ketika diindeks dengan benar, pencarian berjalan dalam waktu kurang dari satu detik bahkan pada jutaan catatan.

## Apa itu date range search?
Date range search memungkinkan Anda menemukan dokumen yang berisi tanggal yang berada di antara dua batas, seperti “2023‑01‑01 ~~ 2023‑12‑31”. Ini penting untuk laporan, log audit, dan skenario apa pun di mana penyaringan berbasis waktu penting.

## Mengapa menggunakan GroupDocs.Search untuk Java?
GroupDocs.Search menawarkan API terpadu untuk banyak jenis kueri—simple, wildcard, faceted, numeric, date range, regex, boolean, dan phrase—sehingga Anda dapat membangun pengalaman pencarian canggih tanpa harus mengelola banyak pustaka. Penanganan error berbasis event juga menjaga pipeline pengindeksan Anda tetap tahan banting.

## Prasyarat
- **GroupDocs.Search Java library** (v25.4 atau lebih baru).  
- **Java Development Kit (JDK)** yang kompatibel dengan proyek Anda.  
- Maven untuk manajemen dependensi (atau unduhan manual).  

### Perpustakaan dan Penyiapan Lingkungan yang Diperlukan
Tambahkan repositori GroupDocs dan dependensi ke `pom.xml` Anda:

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

### Penyiapan Alternatif
Untuk unduhan langsung, kunjungi [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisensi dan Penyiapan Awal
Mulailah dengan percobaan gratis atau lisensi sementara:

- Kunjungi [GroupDocs License Options](https://purchase.groupdocs.com/temporary-license/) untuk detail.

Sekarang mari buat folder indeks yang akan menyimpan data yang dapat dicari.

## Menyiapkan GroupDocs.Search untuk Java

### Inisialisasi Dasar
Pertama, buat objek `Index` yang menunjuk ke folder di disk:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

Anda sekarang memiliki gerbang ke semua operasi pencarian.

## Panduan Implementasi

### Fitur 1: Penanganan Error saat Pengindeksan
#### Cara menangkap error pengindeksan (Java)

```java
import com.groupdocs.search.events.*;

index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
    @Override
    public void invoke(Object sender, IndexErrorEventArgs args) {
        System.out.println(args.getMessage()); // Output the error message
    }
});

// Add documents to the index
index.add("YOUR_DOCUMENT_DIRECTORY");
```

*Why it matters*: Dengan mendengarkan `ErrorOccurred`, Anda dapat mencatat masalah, mencoba kembali file yang gagal, atau memberi peringatan kepada pengguna tanpa menghentikan seluruh proses.

### Fitur 2: Kueri Pencarian Sederhana
#### Apa itu pencarian sederhana?

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*Result*: Mengembalikan setiap dokumen yang berisi istilah **volutpat**.

### Fitur 3: Kueri Pencarian Wildcard
#### Bagaimana cara kerja pencarian wildcard?

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*Result*: Cocok dengan **affect** dan **effect**, menunjukkan kekuatan placeholder `?`.

### Fitur 4: Kueri Pencarian Faceted
#### Cara melakukan pencarian faceted Java

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*Result*: Membatasi pencarian ke bidang **Content**, ideal untuk menyaring berdasarkan metadata seperti kategori atau penulis.

### Fitur 5: Kueri Pencarian Rentang Numerik
#### Cara mencari rentang numerik

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*Result*: Mengambil dokumen di mana nilai numerik berada antara 2000 dan 3000.

### Fitur 6: Kueri Pencarian Rentang Tanggal
#### Cara mengeksekusi pencarian rentang tanggal

```java
import com.groupdocs.search.options.*;
import java.util.*;

String query = "daterange(2000-01-01 ~~ 2001-06-15)";
SearchOptions options = new SearchOptions();

options.getDateFormats().clear();
DateFormatElement[] elements = {
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

SearchResult result = index.search(query, options);
```

*Explanation*: Dengan menyesuaikan `SearchOptions`, Anda memberi tahu mesin untuk mengenali tanggal dalam format **MM/DD/YYYY**, kemudian mengambil semua catatan antara 1 Januari 2000 dan 15 Juni 2001.

### Fitur 7: Kueri Pencarian Ekspresi Reguler
#### Cara menjalankan pencarian regex Java

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*Result*: Menemukan urutan tiga atau lebih karakter yang sama (mis., “aaa”, “111”).

### Fitur 8: Kueri Pencarian Boolean
#### Cara menggabungkan kondisi dengan pencarian boolean Java

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*Result*: Mengembalikan dokumen yang berisi **justo** tetapi mengecualikan yang juga berisi **3456**.

### Fitur 9: Kueri Boolean Kompleks
#### Cara menyusun kueri boolean lanjutan

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*Result*: Mencari nama file yang mirip dengan “English” (memungkinkan variasi 1‑3 karakter) **atau** konten yang berisi **3456** dan **consequat**.

### Fitur 10: Kueri Pencarian Frasa
#### Cara mencari frasa tepat

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*Result*: Mengambil hanya dokumen yang berisi frasa tepat **ipsum dolor sit amet**.

## Aplikasi Praktis
1. **E‑commerce Platforms** – Gunakan faceted search Java untuk menyaring produk berdasarkan ukuran, warna, dan merek.  
2. **Content Management Systems** – Gabungkan boolean search Java dengan pencarian frasa untuk memperkuat alat editorial yang canggih.  
3. **Data Analysis Tools** – Manfaatkan date range search untuk menghasilkan laporan dan dasbor berbasis waktu.

## Masalah Umum & Solusi
- **Tidak ada hasil untuk date range search** – Pastikan format tanggal dalam dokumen Anda cocok dengan `DateFormat` khusus yang Anda tambahkan.  
- **Query regex mengembalikan terlalu banyak hasil** – Perbaiki pola atau batasi ruang lingkup pencarian dengan kualifikasi bidang tambahan.  
- **Error pengindeksan tidak tertangkap** – Pastikan event handler terpasang **sebelum** memanggil `index.add(...)`.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggabungkan date range search dengan jenis kueri lain?**  
A: Tentu saja. Anda dapat menggabungkan klausa rentang tanggal dengan operator boolean, filter faceted, atau pola regex dalam satu string kueri.

**Q: Apakah saya perlu membangun ulang indeks setelah mengubah format tanggal?**  
A: Ya. Indeks menyimpan istilah yang ditokenisasi; memperbarui `SearchOptions` saja tidak akan men-tokenisasi ulang data yang ada. Lakukan re‑indeks pada dokumen setelah mengubah format.

**Q: Bagaimana GroupDocs.Search menangani indeks besar?**  
A: Ia menggunakan pengindeksan inkremental dan penyimpanan di disk, memungkinkan Anda menskalakan hingga jutaan dokumen sambil menjaga penggunaan memori tetap rendah.

**Q: Apakah ada batasan jumlah karakter wildcard?**  
A: Wildcard diproses secara efisien, tetapi penggunaan banyak wildcard di awal (mis., `*term`) dapat menurunkan kinerja. Lebih baik gunakan wildcard prefiks atau sufiks.

**Q: Model lisensi apa yang direkomendasikan untuk produksi?**  
A: Lisensi perpetual atau berlangganan dari GroupDocs memastikan Anda menerima pembaruan, dukungan, dan kemampuan untuk menerapkan tanpa batasan percobaan.

## Kesimpulan
Dengan menguasai **date range search** dan rangkaian lengkap jenis kueri lanjutan yang ditawarkan oleh GroupDocs.Search untuk Java, Anda dapat membangun pengalaman pencarian yang sangat responsif dan kaya fitur. Terapkan penanganan error yang kuat, sesuaikan indeks Anda, dan gabungkan kueri untuk memenuhi hampir semua skenario pengambilan. Mulailah bereksperimen hari ini dan tingkatkan kemampuan akses data aplikasi Anda.

---

**Terakhir Diperbarui:** 2025-12-16  
**Diuji Dengan:** GroupDocs.Search 25.4 (Java)  
**Penulis:** GroupDocs