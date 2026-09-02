---
date: '2026-09-02'
description: Pelajari cara membuat indeks pencarian java dan mengaktifkan koreksi
  ejaan menggunakan GroupDocs.Search. Ikuti petunjuk step‑by‑step untuk menambahkan
  dokumen, mengonfigurasi max mistake count, dan meningkatkan search accuracy.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Pelajari cara membuat indeks pencarian java dan mengaktifkan koreksi
  ejaan menggunakan GroupDocs.Search. Ikuti petunjuk step‑by‑step untuk menambahkan
  dokumen, mengonfigurasi max mistake count, dan meningkatkan search accuracy.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Cara membuat indeks pencarian java dan mengaktifkan ejaan
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Cara membuat indeks pencarian java dan mengaktifkan ejaan
type: docs
url: /id/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Cara membuat indeks pencarian java dan mengaktifkan ejaan

Dalam aplikasi Java modern, menyediakan hasil pencarian yang akurat adalah fitur yang wajib dimiliki. Tutorial ini menunjukkan **cara membuat indeks pencarian java** dan mengaktifkan koreksi ejaan dengan GroupDocs.Search, sehingga pengguna menerima hasil yang relevan bahkan ketika mereka salah mengetik kueri. Anda akan melihat cara menyiapkan pustaka, menambahkan dokumen, mengonfigurasi jumlah kesalahan maksimum, dan menjalankan pencarian toleran typo—semua tanpa menulis satu baris kode konfigurasi tambahan.

## Jawaban Cepat
- **Apa yang dilakukan “enable spelling”?** Itu mengaktifkan pemeriksa ejaan bawaan yang menulis ulang istilah yang salah eja ke bentuk yang paling dekat dan benar selama pencarian.  
- **Perpustakaan mana yang menyediakan fitur ini?** GroupDocs.Search untuk Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk evaluasi; lisensi penuh diperlukan untuk penggunaan produksi.  
- **Bisakah saya mengontrol toleransi?** Ya – gunakan `setMaxMistakeCount` untuk menentukan berapa banyak typo yang diizinkan per kueri.  
- **Apakah cocok untuk indeks besar?** Tentu – mesin ini menangani indeks dengan jutaan catatan sambil menjaga latensi kueri di bawah 100 ms pada perangkat keras server standar.

## Apa itu GroupDocs.Search?
GroupDocs.Search adalah pustaka Java yang menyediakan pengindeksan teks penuh yang cepat dan fitur pencarian lanjutan, termasuk koreksi ejaan bawaan. Ia mendukung lebih dari 50 format input dan dapat memproses dokumen berukuran ratusan halaman tanpa memuat seluruh file ke memori.

## Mengapa mengaktifkan koreksi ejaan dalam aplikasi Java?
- **Meningkatkan kepuasan pengguna** – pengunjung mendapatkan hasil yang tepat meskipun mengetik dengan tidak sempurna.  
- **Mengurangi tingkat pentalan** – hasil yang akurat membuat pengguna tetap terlibat lebih lama.  
- **Berfungsi di berbagai domain** – mulai dari katalog perpustakaan hingga pencarian produk e‑commerce, koreksi ejaan meningkatkan relevansi di mana saja.

## Prasyarat
- Java Development Kit (JDK) terpasang.  
- Pengetahuan dasar tentang Java dan Maven.  
- Memahami konsep pengindeksan.  
- Lisensi percobaan atau kunci berlisensi GroupDocs.Search.

### Menyiapkan GroupDocs.Search untuk Java
Integrasikan pustaka ke dalam proyek Maven Anda.

**Maven setup**  
Add the repository and dependency to your `pom.xml` file:

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

**Unduh langsung**  
Sebagai alternatif, unduh versi terbaru dari [Rilis GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

## Akuisisi Lisensi
Dapatkan lisensi percobaan gratis untuk evaluasi. Untuk penggunaan produksi, beli lisensi penuh atau minta kunci sementara dari situs resmi.

## Bagaimana cara membuat indeks pencarian di Java?
`SearchIndex` adalah kelas utama yang mewakili indeks yang dapat dicari yang disimpan di disk.  
Buat instance `SearchIndex` yang menunjuk ke folder di disk, lalu tambahkan dokumen dari direktori sumber. Mesin membangun indeks terbalik yang memungkinkan pencarian cepat. Anda dapat memanggil `index.add()` untuk setiap file; pustaka secara otomatis mengekstrak teks berdasarkan tipe file.

## Bagaimana cara mengaktifkan koreksi ejaan?
`getSpellingOptions()` mengembalikan objek konfigurasi ejaan untuk indeks, memungkinkan Anda mengaktifkan atau menyesuaikan fitur pemeriksaan ejaan.  
Aktifkan ejaan dengan memanggil `index.getSpellingOptions().setEnabled(true)`. Ini memberi tahu mesin untuk menganalisis istilah kueri dan menyarankan alternatif yang diperbaiki ketika terdeteksi ketidaksesuaian. Fitur ini berfungsi langsung untuk semua bahasa yang diindeks yang didukung oleh pustaka.

## Apa pengaturan jumlah kesalahan maksimum?
`setMaxMistakeCount` mengonfigurasi jumlah maksimum edit karakter yang dapat ditoleransi pemeriksa ejaan per istilah.  
`setMaxMistakeCount(int)` menentukan jumlah maksimum edit karakter (penyisipan, penghapusan, substitusi) yang dapat ditoleransi pemeriksa ejaan per istilah. Menetapkannya ke **2** memungkinkan mesin memperbaiki typo dua karakter yang umum sambil menghindari koreksi yang terlalu agresif yang dapat menghasilkan hasil yang tidak terkait.

## Cara melakukan pencarian dengan koreksi ejaan
`search()` mengeksekusi kueri terhadap indeks dan mengembalikan objek `SearchResult` yang berisi hasil yang cocok serta istilah yang telah diperbaiki.  
Jalankan kueri pencarian menggunakan metode `search()`. Jika kueri mengandung kata yang salah eja, mesin mengembalikan `SearchResult` yang mencakup istilah yang diperbaiki dan daftar dokumen paling relevan. Anda dapat menampilkan baik kueri asli maupun versi yang diperbaiki kepada pengguna untuk transparansi.  
`SearchResult` menyimpan daftar dokumen yang cocok dan informasi tentang koreksi kueri.

## Aplikasi Praktis
1. **Sistem perpustakaan** – secara otomatis memperbaiki judul buku atau nama penulis yang salah eja.  
2. **Platform e‑commerce** – memperbaiki typo nama produk untuk meningkatkan tingkat konversi.  
3. **Manajemen konten** – membantu staf editorial menemukan artikel meskipun dengan kata kunci yang tidak sempurna.

## Pertimbangan Kinerja
- **Jaga indeks tetap terbaru** – lakukan pengindeksan ulang file baru atau yang berubah secara teratur.  
- **Sesuaikan pengaturan memori JVM** – alokasikan heap yang cukup untuk indeks besar (mis., `-Xmx4g`).  
- **Pantau penggunaan sumber daya** – sesuaikan flag garbage‑collector jika Anda melihat jeda selama pengindeksan massal.

## Masalah Umum & Pemecahan Masalah
| Gejala | Penyebab kemungkinan | Solusi |
|--------|----------------------|--------|
| Tidak ada hasil setelah mengaktifkan ejaan | Jalur folder indeks salah atau kosong | Verifikasi `indexFolder` mengarah ke indeks yang valid dan bahwa `index.add()` berhasil |
| Pemeriksa ejaan tidak memperbaiki typo yang jelas | `setMaxMistakeCount` diatur terlalu rendah | Tingkatkan jumlah menjadi 2 atau 3 untuk koreksi yang lebih toleran |
| Aplikasi crash pada kumpulan dokumen besar | Heap JVM tidak cukup | Tingkatkan opsi `-Xmx` (mis., `-Xmx4g`) |

## Pertanyaan yang Sering Diajukan

**T: Apa itu GroupDocs.Search?**  
**J:** GroupDocs.Search adalah pustaka Java yang menyediakan pengindeksan cepat, kemampuan kueri lanjutan, dan koreksi ejaan bawaan untuk aplikasi Java apa pun.

**T: Bagaimana cara mendapatkan lisensi untuk GroupDocs.Search?**  
**J:** Kunjungi situs resmi untuk mengunduh percobaan gratis atau membeli lisensi penuh; kunci sementara juga tersedia untuk pengujian jangka pendek.

**T: Bisakah saya mengintegrasikan GroupDocs.Search dengan kerangka kerja Java lain?**  
**J:** Ya, ia bekerja mulus dengan Spring, Jakarta EE, dan aplikasi Java standar apa pun.

**T: Apa masalah umum saat menyiapkan indeks?**  
**J:** Jalur folder yang salah, izin file yang hilang, atau ketergantungan Maven yang tidak ada biasanya menjadi penyebabnya.

**T: Bagaimana koreksi ejaan meningkatkan hasil pencarian?**  
**J:** Ia secara otomatis menulis ulang kueri yang salah eja ke istilah yang paling dekat dan benar, menghasilkan hasil yang lebih relevan dan mengurangi frustrasi pengguna.

## Sumber Daya Tambahan
- [Dokumentasi](https://docs.groupdocs.com/search/java/)
- [Referensi API](https://reference.groupdocs.com/search/java)
- [Unduh](https://releases.groupdocs.com/search/java/)
- [Repositori GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

**Terakhir Diperbarui:** 2026-09-02  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Tutorial Terkait

- [Cara Membuat Indeks Dokumen dan Menambahkan Dokumen Menggunakan API GroupDocs.Search untuk Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Pemrosesan Bahasa Java – Membuat Kamus Sinonim dengan GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Kata Henti dalam Pencarian: Tambahkan Dokumen ke Indeks dengan GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)