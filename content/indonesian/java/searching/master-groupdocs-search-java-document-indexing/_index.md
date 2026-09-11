---
date: '2026-09-11'
description: Pelajari cara menyorot hasil pencarian Java dan mengindeks dokumen Java
  menggunakan GroupDocs.Search untuk Java dengan pengindeksan sinkron dan asinkron.
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: Sorot hasil pencarian Java dengan GroupDocs.Search. Pelajari pengindeksan
  sinkron dan asinkron, pembaruan waktu nyata, serta penyorotan hasil dalam aplikasi
  Java.
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: Sorot hasil pencarian Java – Pengindeksan sinkron & async cepat
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: Sorot hasil pencarian Java – Pengindeksan sinkron & async
type: docs
url: /id/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Sorot hasil pencarian Java – Pengindeksan sinkron & async

Dalam panduan ini Anda akan menemukan cara **highlight search results Java** menggunakan pustaka GroupDocs.Search, dan Anda akan melihat langkah demi langkah cara mengindeks dokumen Java secara sinkron maupun asinkron. Baik Anda membangun alat desktop kecil atau layanan pencarian perusahaan berskala besar, teknik ini memungkinkan Anda memberikan hasil yang instan dan jelas secara visual tanpa memblokir thread aplikasi Anda.

## Jawaban Cepat
- **Apa arti “highlight search results Java”?** Itu berarti membungkus setiap istilah yang cocok dalam cuplikan yang dikembalikan dengan markup (misalnya, `<mark>`) sehingga pengguna dapat langsung melihat konteks hasilnya.  
- **Kapan saya harus menggunakan pengindeksan sinkron?** Gunakan untuk koleksi kecil‑menengah di mana Anda membutuhkan dokumen dapat dicari segera setelah ditambahkan.  
- **Kapan pengindeksan asinkron lebih disarankan?** Pilih untuk batch besar atau ketika thread UI harus tetap responsif sementara indeks dibangun di latar belakang.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengembangan; lisensi penuh menghapus batasan dan membuka fitur lanjutan.  
- **Versi Java mana yang didukung?** Java 8 atau yang lebih baru.

## Apa itu “highlight search results Java”?
`highlight search results java` adalah proses mengambil data kecocokan mentah dari GroupDocs.Search dan menyisipkan petunjuk visual—biasanya tag HTML `<mark>`—di sekitar setiap istilah yang ditemukan. Ini membuat cuplikan hasil langsung dapat dibaca di halaman web atau komponen Swing, meningkatkan pengalaman pengguna dengan menunjukkan secara tepat di mana kueri muncul.

## Mengapa menggunakan GroupDocs.Search untuk Java?
GroupDocs.Search menyediakan mesin berperforma tinggi dan tidak bergantung pada bahasa yang dapat **memproses hingga 5 000 dokumen per detik**, **mendukung lebih dari 30 format file**, dan **mengindeks koleksi 10 juta dokumen** tanpa harus memuat seluruh korpus ke memori. Fitur sorotan bawaan, pengindeksan waktu nyata, dan analis multi‑bahasa menjadikannya ideal untuk sistem manajemen konten, katalog e‑commerce, dan repositori dokumen perusahaan.

## Prasyarat
- **Java Development Kit** (JDK 8 atau lebih baru) terinstal dan `JAVA_HOME` sudah diatur dengan benar.  
- Sebuah IDE seperti **IntelliJ IDEA** atau **Eclipse**.  
- Sebuah folder (misalnya `documents/`) yang berisi file yang ingin Anda indeks—teks biasa, PDF, DOCX, dll.  
- Maven untuk manajemen dependensi (atau Anda dapat menambahkan JAR secara manual).

### Perpustakaan dan dependensi yang diperlukan
Add GroupDocs.Search to your Maven `pom.xml`:

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

Untuk unduhan langsung, dapatkan versi terbaru dari [rilis GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

### Penyiapan lingkungan
- Verifikasi `JAVA_HOME` mengarah ke JDK yang kompatibel.  
- Buat proyek Maven baru dan tempelkan cuplikan di atas ke dalam bagian `<dependencies>`.  
- Letakkan file contoh di direktori seperti `src/main/resources/documents/`.

## Cara menyiapkan GroupDocs.Search untuk Java
`Index` adalah kelas inti yang mewakili koleksi yang dapat dicari yang disimpan di disk.

Buat instance `Index` yang menunjuk ke folder di disk, terapkan lisensi jika Anda memilikinya, dan opsional konfigurasikan analyzer untuk tokenisasi spesifik bahasa. Langkah persiapan ini memastikan mesin dapat membaca, menulis, dan mencari indeks secara efisien dengan benar.

Kelas `Index` adalah komponen inti yang mewakili koleksi yang dapat dicari di disk. Setelah Anda menginstansiasinya, semua operasi pengindeksan dan kueri mengalir melalui objek ini.

1. **Instal pustaka** – Gunakan cuplikan Maven di atas atau unduh JAR dari [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Dapatkan lisensi** – Mulai dengan lisensi percobaan; ganti dengan kunci produksi sebelum penyebaran.  
3. **Inisialisasi indeks** – Cuplikan berikut menunjukkan cara membuat (atau membuka) folder indeks:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Cara menyorot hasil pencarian Java – pengindeksan sinkron
`DocumentHighlighter` adalah kelas utilitas yang menghasilkan cuplikan yang disorot dari hasil pencarian.

Muat indeks, tambahkan dokumen dengan `index.add(documentPath)`, jalankan kueri, lalu panggil `DocumentHighlighter` untuk membungkus kecocokan dalam tag `<mark>`. Seluruh proses berjalan pada thread pemanggil, sehingga dokumen menjadi dapat dicari segera setelah `add` selesai untuk pengguna akhir.

### Langkah 1: buat indeks dan lampirkan penanganan error
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Langkah 2: tambahkan dokumen dan jalankan pencarian
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Langkah 3: proses hasil dan sorot hasil pencarian Java
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## Cara menyorot hasil pencarian Java – pengindeksan asinkron
`IndexingOptions` mengonfigurasi bagaimana proses pengindeksan dijalankan, termasuk mode sinkron atau asinkron.

Konfigurasikan `IndexingOptions` untuk berjalan dalam mode latar belakang, berlangganan ke acara `StatusChanged`, dan biarkan mesin mengindeks file sementara UI Anda terus melayani permintaan lain. Setelah status berubah menjadi `Ready`, Anda dapat mengeksekusi pencarian dan memperoleh cuplikan yang disorot seperti pada mode sinkron.

`AsyncIndexingListener` menerima pembaruan progres, memungkinkan Anda menampilkan bilah progres atau mencatat status tanpa memblokir thread utama.

### Langkah 1: siapkan indeks dengan pendengar acara
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Langkah 2: aktifkan mode asinkron dan mulai mengindeks
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## Cara mengindeks dokumen Java – tips praktis
`index.update(path)` memperbarui dokumen yang sudah ada dalam indeks dengan file pada jalur yang ditentukan.

Bagi koleksi besar menjadi batch berukuran 1 000–5 000 file, filter berdasarkan ekstensi untuk menghindari parsing yang tidak perlu, dan gunakan `index.update(path)` untuk file yang berubah alih-alih membangun ulang seluruh indeks. Praktik ini menjaga penggunaan memori tetap rendah dan waktu pengindeksan dapat diprediksi untuk menjaga konsistensi.

- **Ukuran batch**: Untuk koleksi sangat besar, bagi folder menjadi batch lebih kecil untuk menghindari lonjakan memori.  
- **Filter file**: Gunakan `IndexingOptions.setFileExtensions` untuk menyertakan hanya format yang Anda butuhkan (misalnya, `.pdf`, `.docx`).  
- **Re‑indeks**: Ketika dokumen berubah, panggil `index.update(documentPath)` alih-alih membuat ulang indeks dari awal.

## Pertimbangan Kinerja
- **Memori**: Pantau penggunaan heap; tingkatkan `-Xmx` jika Anda memproses banyak file besar secara bersamaan.  
- **CPU**: Pengindeksan asinkron menyebarkan beban kerja ke beberapa thread tetapi tetap mengonsumsi CPU—lacak penggunaan dengan JVisualVM.  
- **Sorotan hasil**: Sorotan menambah overhead ringan (≈ 2–5 ms per hasil). Cache HTML yang dihasilkan jika Anda perlu menampilkan cuplikan yang sama berulang kali.

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menggabungkan pengindeksan sinkron dan asinkron dalam aplikasi yang sama?**  
J: Ya. Gunakan pengindeksan sinkron untuk set kecil yang sering diperbarui dan pengindeksan asinkron untuk impor massal atau pekerjaan latar belakang.

**T: Bagaimana cara menyesuaikan gaya sorotan?**  
J: Sediakan implementasi `DocumentHighlighter` khusus yang menulis tag HTML, CSS, atau XML yang diinginkan di sekitar istilah yang cocok.

**T: Jenis file apa yang didukung GroupDocs.Search secara bawaan?**  
J: Teks, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, dan banyak lagi melalui parser bawaan—lebih dari 30 format secara total.

**T: Apakah memungkinkan mencari dalam beberapa bahasa secara bersamaan?**  
J: Tentu saja. GroupDocs.Search menyertakan analis multi‑bahasa; cukup konfigurasikan `Analyzer` yang tepat saat membuat indeks.

**T: Bagaimana cara mengamankan folder indeks?**  
J: Simpan indeks di direktori yang dilindungi, atur izin sistem file yang ketat, dan opsional enkripsi indeks menggunakan fitur keamanan pustaka.

---

**Last Updated:** 2026-09-11  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Tutorial Terkait

- [Cara Membuat Indeks Dokumen dan Menambahkan Dokumen Menggunakan API GroupDocs.Search untuk Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Cara membuat repositori indeks java dengan GroupDocs.Search: Pengindeksan & Pencarian Dokumen Efisien](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [Pengindeksan Dokumen Efisien Pencarian Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)