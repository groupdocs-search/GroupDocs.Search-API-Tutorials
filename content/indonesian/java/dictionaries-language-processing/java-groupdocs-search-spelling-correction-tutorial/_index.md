---
date: '2025-12-20'
description: Pelajari cara mengaktifkan koreksi ejaan di Java menggunakan GroupDocs.Search,
  menambahkan dokumen ke indeks, dan mengatur jumlah kesalahan maksimum untuk meningkatkan
  akurasi pencarian.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: Cara Mengaktifkan Ejaan di Java dengan GroupDocs.Search
type: docs
url: /id/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Cara Mengaktifkan Pengejaan di Java Menggunakan GroupDocs.Search

Hasil pencarian yang akurat sangat penting untuk setiap aplikasi modern. Dalam tutorial ini Anda akan mempelajari **cara mengaktifkan koreksi ejaan** di Java dengan GroupDocs.Search, sehingga pengguna mendapatkan hasil yang tepat meskipun mereka salah mengetik kueri. Kami akan membahas cara membuat indeks, **menambahkan dokumen ke indeks**, mengonfigurasi opsi ejaan, dan menjalankan pencarian yang secara otomatis memperbaiki kesalahan.

## Jawaban Cepat
- **Apa arti “cara mengaktifkan ejaan”?** Itu mengaktifkan pemeriksa ejaan bawaan yang memperbaiki kesalahan ketik pengguna selama pencarian.  
- **Perpustakaan mana yang menyediakan fitur ini?** GroupDocs.Search untuk Java.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya mengontrol toleransi?** Ya – gunakan `setMaxMistakeCount` untuk menentukan berapa banyak kesalahan ketik yang diizinkan.  
- **Apakah cocok untuk indeks besar?** Tentu – mesin ini dioptimalkan untuk pengindeksan dan pencarian berperforma tinggi.

## Apa itu “cara mengaktifkan ejaan” di GroupDocs.Search?
Mengaktifkan ejaan memberi tahu mesin pencari untuk mencari istilah yang paling mendekati yang benar ketika kueri mengandung kesalahan. Fitur ini secara dramatis meningkatkan pengalaman pengguna dengan mengembalikan hasil yang relevan meskipun input salah eja.

## Mengapa mengaktifkan koreksi ejaan dalam aplikasi Java?
- **Meningkatkan kepuasan pengguna** – pengguna tidak perlu mengetik dengan sempurna.  
- **Mengurangi tingkat pentalan** – hasil yang lebih akurat membuat pengunjung tetap terlibat.  
- **Berfungsi di berbagai domain** – mulai dari katalog perpustakaan hingga pencarian produk e‑commerce.

## Prasyarat
- Java Development Kit (JDK) terpasang.
- Pengetahuan dasar tentang Java dan Maven.
- Memahami konsep pengindeksan.
- Lisensi percobaan atau kunci berlisensi GroupDocs.Search.

### Menyiapkan GroupDocs.Search untuk Java
Integrasikan pustaka ke dalam proyek Maven Anda.

**Pengaturan Maven**  
Tambahkan repositori dan dependensi ke file `pom.xml` Anda:

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

**Unduhan Langsung**  
Atau, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Dapatkan lisensi percobaan gratis untuk evaluasi. Untuk penggunaan produksi, beli lisensi penuh atau minta kunci sementara dari situs resmi.

## Cara Menambahkan Dokumen ke Indeks
Membuat indeks adalah dasar bagi setiap aplikasi yang mendukung pencarian. Berikut contoh minimal yang **menambahkan dokumen ke indeks** dari sebuah folder.

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

*Tip:* Pastikan jalur file sudah benar dan aplikasi memiliki izin menulis ke folder indeks.

## Cara Mengonfigurasi Koreksi Ejaan (set max mistake count)
Anda dapat menyesuaikan pemeriksa ejaan dengan mengaktifkannya dan mengatur toleransi untuk kesalahan.

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

*Mengapa `setMaxMistakeCount` penting:* Itu menentukan berapa banyak kesalahan ketik yang akan ditoleransi mesin. Sesuaikan nilai ini berdasarkan pola kesalahan umum di domain Anda.

## Cara Melakukan Pencarian dengan Koreksi Ejaan
Dengan indeks siap dan opsi ejaan dikonfigurasi, jalankan kueri yang mungkin mengandung kesalahan.

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

Pemanggilan `search()` mengembalikan `SearchResult` yang berisi istilah yang telah dikoreksi dan dokumen paling relevan.

## Aplikasi Praktis
1. **Sistem Perpustakaan:** Memperbaiki judul buku atau nama penulis yang salah eja.  
2. **Platform E‑commerce:** Memperbaiki kesalahan ketik pengguna dalam pencarian produk untuk meningkatkan konversi.  
3. **Sistem Manajemen Konten:** Meningkatkan pengambilan artikel bagi staf editorial.

## Pertimbangan Kinerja
- **Jaga indeks tetap terbaru** – lakukan re‑indeks pada file baru atau yang berubah secara teratur.  
- **Sesuaikan pengaturan memori JVM** – alokasikan heap yang cukup untuk indeks besar.  
- **Pantau penggunaan sumber daya** – sesuaikan flag garbage‑collector jika diperlukan.

## Pertanyaan yang Sering Diajukan

**Q: Apa itu GroupDocs.Search?**  
A: Itu adalah pustaka Java yang menyediakan pengindeksan cepat, fitur pencarian lanjutan, dan koreksi ejaan bawaan.

**Q: Bagaimana cara mendapatkan lisensi untuk GroupDocs.Search?**  
A: Kunjungi situs resmi untuk mengunduh lisensi percobaan gratis atau membeli lisensi penuh.

**Q: Bisakah saya mengintegrasikan GroupDocs.Search dengan kerangka kerja Java lain?**  
A: Ya, ia bekerja dengan Spring, Jakarta EE, dan aplikasi Java standar apa pun.

**Q: Apa masalah umum saat menyiapkan indeks?**  
A: Jalur folder yang salah, izin file yang tidak cukup, atau dependensi yang hilang di `pom.xml`.

**Q: Bagaimana koreksi ejaan meningkatkan hasil pencarian?**  
A: Ia secara otomatis menulis ulang kueri yang salah eja ke istilah yang paling mendekati yang benar, menghasilkan hasil yang lebih relevan.

## Sumber Daya Tambahan
- [Dokumentasi](https://docs.groupdocs.com/search/java/)
- [Referensi API](https://reference.groupdocs.com/search/java)
- [Unduhan](https://releases.groupdocs.com/search/java/)
- [Repositori GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2025-12-20  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs