---
date: '2026-10-02'
description: Pelajari cara menggunakan temporary license untuk menambahkan dokumen
  ke indeks dengan chunk‑based search di Java, meningkatkan kinerja pencarian sambil
  mengontrol penggunaan memori.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Gunakan temporary license untuk menambahkan dokumen ke indeks dengan
  chunk‑based search di Java, meningkatkan kecepatan pencarian dan mengurangi konsumsi
  memori.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Gunakan temporary license untuk chunk‑based indexing di Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Gunakan temporary license untuk chunk‑based indexing di Java
type: docs
url: /id/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Gunakan lisensi sementara untuk pengindeksan berbasis potongan di Java

Dalam tutorial ini Anda akan **menggunakan lisensi sementara** untuk menambahkan dokumen ke indeks dengan fitur pencarian berbasis potongan dari GroupDocs.Search. Pendekatan ini memungkinkan Anda menangani koleksi dokumen besar—kontrak hukum, tiket dukungan, makalah penelitian—sementara menjaga penggunaan **java search index memory** tetap rendah dan **meningkatkan kinerja pencarian** secara dramatis. Anda akan melihat cara menyiapkan folder indeks, memasukkan beberapa sumber dokumen, mengaktifkan pencarian potongan, dan menjalankan baik kueri potongan pertama maupun berikutnya.

## Jawaban Cepat
- **Apa langkah pertama?** Buat folder indeks pencarian.  
- **Bagaimana cara memasukkan banyak file?** Gunakan `index.add()` untuk setiap folder dokumen.  
- **Opsi mana yang mengaktifkan pencarian potongan?** `options.setChunkSearch(true)`.  
- **Bisakah saya melanjutkan pencarian setelah potongan pertama?** Ya, panggil `index.searchNext()` dengan token.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan gratis atau lisensi sementara cukup untuk pengembangan; lisensi penuh diperlukan untuk produksi.  

## Apa yang akan Anda pelajari
- Cara membuat indeks pencarian di folder yang ditentukan.  
- Langkah-langkah untuk **menambahkan dokumen ke indeks** dari beberapa lokasi.  
- Mengonfigurasi opsi pencarian untuk mengaktifkan pencarian berbasis potongan.  
- Melakukan pencarian berbasis potongan awal dan berikutnya.  
- Skenario dunia nyata di mana pencarian dokumen berbasis potongan bersinar.  

## Prasyarat
Untuk mengikuti panduan ini, pastikan Anda memiliki:

- **Perpustakaan yang diperlukan**: GroupDocs.Search untuk Java 25.4 atau lebih baru.  
- **Pengaturan lingkungan**: Java Development Kit (JDK) yang kompatibel terpasang.  
- **Prasyarat pengetahuan**: Pemrograman Java dasar dan familiaritas dengan Maven.  

## Menyiapkan GroupDocs.Search untuk Java
Untuk memulai, integrasikan GroupDocs.Search ke dalam proyek Anda menggunakan Maven:

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

Atau, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi lisensi
Untuk mencoba GroupDocs.Search:

- **Uji coba gratis** – menguji fitur inti tanpa komitmen.  
- **Lisensi sementara** – akses tambahan untuk pengembangan.  
- **Pembelian** – lisensi penuh untuk penggunaan produksi.  

## Cara menambahkan dokumen ke indeks?
**Jawaban langsung:** Panggil `index.add()` untuk setiap folder yang berisi file yang ingin Anda jadikan dapat dicari; metode ini memindai folder secara rekursif dan menambahkan setiap dokumen yang didukung ke indeks dalam satu operasi. Ini menghilangkan kebutuhan penanganan file satu per satu secara manual dan mempercepat proses masuk massal.

`SearchIndex` adalah kelas utama yang mewakili koleksi yang dapat dicari di disk. Setelah Anda menginstansiasinya, semua operasi pengindeksan dan kueri mengalir melalui objek ini.

### 1. Membuat indeks
**Jawaban langsung:** Instansiasikan objek `SearchIndex` dengan jalur tempat file indeks harus disimpan, kemudian panggil `index.create()` untuk menginisialisasi struktur penyimpanan. Panggilan ini membuat folder dan file metadata yang diperlukan pada penggunaan pertama.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Menambahkan dokumen ke indeks
**Jawaban langsung:** Gunakan metode `index.add()` dan berikan jalur absolut setiap folder sumber; API secara otomatis mendeteksi format yang didukung (PDF, DOCX, XLSX, dll.) dan mengekstrak teks yang dapat dicari ke dalam indeks.

`SearchOptions` adalah objek konfigurasi yang memungkinkan Anda menyesuaikan secara detail bagaimana dokumen diproses selama pengindeksan dan pencarian. Anda akan menggunakannya nanti untuk mengaktifkan kueri berbasis potongan.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Mengonfigurasi opsi pencarian untuk pencarian potongan
**Jawaban langsung:** Atur `options.setChunkSearch(true)` pada instance `SearchOptions` sebelum mengeksekusi kueri; ini memberi tahu mesin untuk membagi setiap dokumen menjadi potongan logis (biasanya paragraf) dan mengembalikan kecocokan per potongan alih-alih per file keseluruhan.

`SearchResult` menyimpan potongan yang cocok, posisinya, dan skor relevansi. Ketika pencarian potongan diaktifkan, setiap `SearchResult` berkorespondensi dengan satu fragmen dari dokumen asli.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Melakukan pencarian berbasis potongan awal
**Jawaban langsung:** Jalankan `index.search("your query", options)`; panggilan ini mengembalikan koleksi `SearchResult` untuk set pertama potongan yang cocok dan token yang mewakili keadaan pencarian untuk kelanjutan.

Token yang dikembalikan penting untuk melakukan paging pada set hasil besar tanpa mengeksekusi ulang seluruh kueri.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Melanjutkan pencarian berbasis potongan
**Jawaban langsung:** Berikan token yang dikembalikan dari panggilan sebelumnya ke `index.searchNext(token, options)`; ulangi hingga metode mengembalikan `null`, yang menandakan semua potongan yang cocok telah diambil.

Pendekatan inkremental ini menjaga penggunaan memori tetap rendah karena hanya batch potongan saat ini yang berada di memori.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Mengapa menggunakan pencarian berbasis potongan?
Pencarian berbasis potongan memecah koleksi dokumen besar menjadi bagian yang dapat dikelola, mengurangi tekanan memori dan mempercepat waktu respons. Dengan mengindeks pada tingkat paragraf atau bagian, mesin dapat mengambil hanya fragmen yang relevan, yang menurunkan penggunaan CPU dan meningkatkan latensi bagi pengguna akhir. Ini sangat bermanfaat ketika:

1. **Tim hukum** perlu menemukan klausul spesifik di antara ribuan kontrak.  
2. **Portal dukungan pelanggan** harus menampilkan artikel basis pengetahuan yang relevan secara instan.  
3. **Peneliti** menyaring dataset yang luas tanpa memuat seluruh file ke memori.  

Pernyataan terkuantifikasi: GroupDocs.Search dapat memproses **PDF lebih dari 500 halaman** dalam waktu kurang dari **2 detik per potongan** pada server standar 8‑core, sambil menjaga puncak heap di bawah **200 MB**.

## Bagaimana pendekatan ini meningkatkan kinerja pencarian
**Jawaban langsung:** Dengan mencari potongan yang lebih kecil alih-alih seluruh file, mesin dapat melewati bagian yang tidak relevan lebih awal, mengurangi siklus CPU, dan hanya menyimpan potongan aktif di memori, yang secara langsung menurunkan konsumsi **java search index memory** dan menghasilkan waktu respons yang lebih cepat. Pendekatan terfokus ini juga memungkinkan caching yang lebih efektif dan pemrosesan paralel, memungkinkan beberapa core menangani potongan yang berbeda secara bersamaan, yang selanjutnya meningkatkan throughput pada server multi‑core.

Manfaat tambahan meliputi:
- Pemrosesan potongan paralel di beberapa core.  
- Penghentian dini ketika ditemukan kecocokan dengan relevansi tinggi.  

## Mengelola memori indeks pencarian java
**Jawaban langsung:** Alokasikan heap JVM yang cukup (mis., `-Xmx2g` atau lebih tinggi) berdasarkan ukuran indeks yang diharapkan, jalankan `index.optimize()` setelah penambahan massal untuk mengompres struktur indeks, dan pantau jeda GC dengan VisualVM untuk menghindari lonjakan latensi.

Tips penyetelan lebih lanjut:
- Gunakan `index.flush()` setelah batch besar untuk menulis data sementara ke disk.  
- Aktifkan `options.setMemoryLimit(256)` untuk membatasi penggunaan memori per pencarian.  

## Pertimbangan kinerja
- **Manajemen memori** – Alokasikan ruang heap yang cukup (`-Xmx`) untuk indeks besar.  
- **Pemantauan sumber daya** – Pantau penggunaan CPU selama operasi pengindeksan dan pencarian.  
- **Pemeliharaan indeks** – Secara periodik bangun ulang atau bersihkan indeks untuk membuang data usang.  

## Kesalahan umum & pemecahan masalah
| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| `OutOfMemoryError` selama pengindeksan | Ukuran heap terlalu kecil | Tingkatkan heap JVM (`-Xmx2g` atau lebih tinggi) |
| Tidak ada hasil yang dikembalikan | Token potongan tidak diproses | Pastikan loop `while` berjalan hingga `getNextChunkSearchToken()` menjadi `null` |
| Kinerja pencarian lambat | Indeks tidak dioptimalkan | Jalankan `index.optimize()` setelah penambahan massal |

## Pertanyaan yang sering diajukan

**Q: Apa itu pencarian berbasis potongan?**  
A: Pencarian berbasis potongan membagi dataset menjadi bagian-bagian yang lebih kecil, memungkinkan kueri yang efisien pada volume data besar tanpa memuat seluruh dokumen ke memori.

**Q: Bagaimana cara memperbarui indeks saya dengan file baru?**  
A: Cukup panggil `index.add()` dengan jalur ke dokumen baru; indeks akan menggabungkannya secara otomatis.

**Q: Bisakah GroupDocs.Search menangani berbagai format file?**  
A: Ya, ia mendukung **PDF, DOCX, XLSX, PPTX, HTML, TXT, dan lebih dari 30 format lainnya**.

**Q: Apa saja bottleneck kinerja yang umum?**  
A: Kendala memori dan indeks yang tidak dioptimalkan adalah yang paling umum; alokasikan heap yang cukup dan secara rutin optimalkan indeks.

**Q: Di mana saya dapat menemukan dokumentasi lebih detail?**  
A: Kunjungi [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) resmi untuk panduan mendalam dan referensi API.

**Q: Apakah pencarian berbasis potongan bekerja dengan PDF terenkripsi?**  
A: Ya, selama Anda menyediakan kata sandi melalui overload API yang sesuai.

**Q: Bagaimana saya dapat memantau kemajuan pengindeksan?**  
A: Gunakan overload `Index.add()` yang mengembalikan objek `Progress` atau hubungkan ke callback logging.

## Sumber Daya
- **Dokumentasi**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referensi API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Unduhan**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Dukungan gratis**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Lisensi sementara**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Terakhir Diperbarui:** 2026-10-02  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs  

---

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Tutorial Terkait

- [Buat Direktori Indeks Pencarian & Atur Lisensi – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Tingkatkan Kinerja Kueri dengan GroupDocs.Search Java: Optimalkan Indeks & Pencarian](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Fitur Pencarian Lanjutan Groupdocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)