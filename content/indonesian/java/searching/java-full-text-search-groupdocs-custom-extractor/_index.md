---
date: '2026-08-05'
description: Pelajari cara membuat ekstraktor file log untuk pencarian teks penuh
  di Java menggunakan GroupDocs.Search. Tambahkan dokumen ke indeks, optimalkan kinerja
  pencarian, dan tangani file log besar secara efisien.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Tutorial pencarian teks penuh java menunjukkan cara membuat ekstraktor
  file log khusus menggunakan GroupDocs.Search, menambahkan dokumen ke indeks, dan
  mengoptimalkan kinerja pencarian untuk arsip log yang masif.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Pencarian teks penuh java: ekstraktor file log dengan GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Pencarian teks penuh java: ekstraktor file log dengan GroupDocs'
type: docs
url: /id/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Pencarian teks penuh java: pengekstrak file log dengan GroupDocs

Pencarian teks penuh java adalah fondasi bagi setiap sistem yang harus dengan cepat menemukan informasi di dalam koleksi dokumen yang sangat besar. Dalam tutorial ini Anda akan belajar cara mengkonfigurasi GroupDocs.Search, membuat pengekstrak file log khusus, menambahkan dokumen ke indeks, dan mengoptimalkan kinerja pencarian saat menangani gigabyte data log.

## Apa yang akan Anda pelajari
- Mengatur dan mengkonfigurasi GroupDocs.Search untuk Java.  
- Menerapkan **log file extractor** yang mengurai log teks biasa sesuai kebutuhan Anda.  
- **Add documents to index** bersama PDF, DOCX, dan format lainnya.  
- Skenario dunia nyata di mana **log file extractor** menambah nilai yang dapat diukur.  
- Tips terbukti untuk **optimise search performance** pada arsip log multi‑gigabyte.

## Jawaban Cepat
- **What is a log file extractor?** Komponen khusus yang memberi tahu GroupDocs.Search cara membaca dan mengindeks file log teks biasa.  
- **Why use GroupDocs.Search?** Mendukung pengindeksan lebih dari 50 format, menyediakan auto‑reindexing, dan menangani indeks hingga 10 GB dengan kurang dari 2 GB RAM.  
- **Do I need a license?** Ya – lisensi percobaan atau lisensi penuh diperlukan untuk mengaktifkan perpustakaan.  
- **Can I index other file types simultaneously?** Tentu saja; campurkan PDF, DOCX, dan file log khusus dalam indeks yang sama.  
- **How to improve performance?** Gunakan pengindeksan inkremental, sesuaikan `IndexSettings`, dan aktifkan flag `autoReindex`.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki hal berikut:

### Perpustakaan yang Diperlukan
Tambahkan dependensi Maven GroupDocs.Search ke `pom.xml` Anda. Gunakan versi terbaru yang sesuai dengan level Java proyek Anda.

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

Atau, unduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Penyiapan Lingkungan
- JDK 8 atau lebih tinggi.  
- Familiaritas dengan pemrograman Java dan konsep dasar penanganan file.

### Akuisisi Lisensi
Mulailah dengan mengunduh lisensi percobaan gratis untuk menjelajahi fitur GroupDocs.Search. Untuk penggunaan produksi, beli lisensi penuh atau minta lisensi sementara melalui [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## Menyiapkan GroupDocs.Search untuk Java

Untuk memulai, inisialisasi perpustakaan dan terapkan file lisensi Anda:

1. **Maven setup** – pastikan dependensi dari langkah sebelumnya ada.  
2. **License initialisation** – muat file lisensi sebelum panggilan API lainnya.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

Dengan lingkungan siap, Anda dapat melanjutkan ke pembuatan **log file extractor** khusus.

## Apa itu log file extractor?

Log file extractor adalah potongan kode yang memberi tahu GroupDocs.Search cara membaca file log mentah (biasanya `.log`) dan mengubah isinya menjadi teks yang dapat dicari. Dengan menyediakan extractor Anda sendiri, Anda mendapatkan kontrol penuh atas aturan parsing, penyaringan kebisingan, dan mengekstrak hanya informasi yang penting bagi kasus penggunaan pencarian Anda.

## Buat log file extractor

GroupDocs.Search memungkinkan Anda memasang extractor teks khusus untuk jenis file apa pun. Ikuti langkah-langkah berikut untuk membuat satu untuk file log.

### Langkah 1: definisikan extractor khusus
`TextExtractorBase` adalah kelas dasar abstrak yang Anda perpanjang untuk membuat extractor khusus. Ia mendeklarasikan ekstensi file yang didukung oleh extractor dan berisi logika ekstraksi inti.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Poin penting**  
- `getFileExtensions()` mendaftarkan extractor untuk file `.log`.  
- `extractText` adalah tempat Anda dapat menghapus timestamp, menyaring baris debug, atau menerapkan pra‑pemrosesan apa pun yang diperlukan untuk **search large log files**.

### Langkah 2: konfigurasikan pengaturan indeks dengan extractor
Tambahkan extractor Anda ke `IndexSettings` dan aktifkan `autoReindex` sehingga log baru diindeks secara otomatis tanpa intervensi manual.

`IndexSettings` mengkonfigurasi perilaku indeks seperti batas memori dan extractor khusus.  
`autoReindex` secara otomatis memperbarui indeks ketika file sumber berubah.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### Langkah 3: tambahkan dokumen ke indeks
Sekarang indeks mengenali file log, Anda dapat **add documents to index** seperti format lain yang didukung.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### Langkah 4: cari di indeks
Lakukan kueri teks biasa. Extractor khusus menjamin setiap entri log dapat dicari.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Tips untuk mengoptimalkan kinerja pencarian

- **Incremental indexing** – tambahkan hanya file log baru atau yang berubah alih-alih membangun ulang seluruh indeks.  
- **Memory management** – flag `autoReindex` menjaga penggunaan RAM tetap rendah dengan membuang data menengah ke disk.  
- **Index settings** – sesuaikan `setMaxMemoryUsage` berdasarkan kapasitas server Anda; pengaturan umum adalah 1 GB untuk indeks 10 GB.  
- **Query optimisation** – gunakan kueri frasa, wildcard, atau filter untuk mempersempit hasil saat mencari arsip log yang besar.

## Aplikasi Praktis

GroupDocs.Search dapat diterapkan dalam banyak skenario dunia nyata, seperti:

- **Log management** – temukan pesan error, tindakan pengguna, atau timestamp spesifik di seluruh gigabyte data log dalam hitungan detik.  
- **Document retrieval systems** – pertahankan repositori yang dapat dicari tunggal yang mencakup PDF, dokumen Word, spreadsheet, dan file log khusus.  
- **Content analysis** – jalankan laporan frekuensi kata kunci atau deteksi anomali dalam data log streaming.

## Pertimbangan Kinerja

Saat menerapkan GroupDocs.Search dalam skala besar, ingat praktik terbaik berikut:

- Simpan indeks pada SSD cepat untuk meminimalkan latensi baca/tulis.  
- Pantau penggunaan heap JVM; pertimbangkan memindahkan indeks besar ke proses terpisah jika memori menjadi kendala.  
- Aktifkan `autoReindex` (seperti yang ditunjukkan) untuk menjaga indeks tetap segar tanpa pembangunan ulang manual.

## Kesimpulan

Sekarang Anda telah membuat **log file extractor**, mempelajari cara **add documents to index**, dan menemukan cara untuk **optimise search performance** pada arsip log besar. Kombinasi ini memungkinkan aplikasi Java Anda menyediakan pencarian teks penuh yang cepat dan akurat di semua jenis dokumen.

Untuk eksplorasi lebih dalam, periksa [GroupDocs documentation](https://docs.groupdocs.com/search/java/) resmi atau bereksperimen dengan implementasi extractor yang berbeda untuk menyesuaikan dengan kasus penggunaan unik Anda.

## Bagian FAQ
1. **What file types can I index using GroupDocs.Search?**  
   - Anda dapat mengindeks PDF, dokumen Word, spreadsheet, dan banyak format lainnya, serta file log khusus melalui extractor teks.  
2. **How do I handle large document collections efficiently?**  
   - Gunakan pembaruan inkremental, partisi indeks, dan sesuaikan `IndexSettings` untuk mengelola sumber daya secara efektif.  
3. **Can GroupDocs.Search be integrated with other systems?**  
   - Ya, ia menawarkan API Java yang bersih yang dapat disematkan dalam layanan yang ada, mikro‑layanan, atau aplikasi web.  
4. **What is a temporary license, and how do I acquire one?**  
   - Lisensi sementara memberikan fungsionalitas penuh untuk evaluasi tanpa batas waktu. Ajukan melalui [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## Pertanyaan yang Sering Diajukan

**Q: How does a log file extractor differ from the default extractor?**  
A: Extractor default menangani format umum (PDF, DOCX, dll.). Extractor log file khusus memungkinkan Anda menentukan secara tepat bagaimana entri log teks biasa diparsing dan diindeks.

**Q: Can I index compressed log archives (e.g., .zip)?**  
A: Ya, dengan menambahkan langkah pra‑pemrosesan yang mengekstrak file dari arsip sebelum memasukkannya ke indeks.

**Q: What’s the best way to keep the index up‑to‑date with continuously generated logs?**  
A: Aktifkan `autoReindex` dan jadwalkan pemantau latar belakang yang memanggil `index.add(newLogFile)` setiap kali file baru muncul.

**Q: Is there a limit to the size of a single log file that can be indexed?**  
A: Secara praktis, batasnya ditentukan oleh memori yang tersedia. Disarankan memecah log yang sangat besar menjadi potongan lebih kecil sebelum diindeks.

**Q: Does GroupDocs.Search support fuzzy or wildcard searches?**  
A: Ya, API pencarian mencakup pencocokan fuzzy, wildcard, dan kueri kedekatan untuk meningkatkan relevansi hasil.

---

**Terakhir Diperbarui:** 2026-08-05  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Java Full Text Search: Build Index with GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)