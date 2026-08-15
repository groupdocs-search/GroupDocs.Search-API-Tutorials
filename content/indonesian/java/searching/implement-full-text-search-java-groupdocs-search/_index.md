---
date: '2026-08-15'
description: Pelajari contoh full text search dalam Java dengan GroupDocs.Search,
  mencakup penambahan dokumen ke index, boolean query java, dan performance optimization.
keywords:
- full text search example
- add documents to index
- boolean query java
lastmod: '2026-08-15'
og_description: Jelajahi contoh full text search dalam Java dengan GroupDocs.Search.
  Pelajari cara menambahkan dokumen ke index, menyusun pernyataan boolean query java,
  dan meningkatkan search performance.
og_image_alt: Guide showing how to implement a full text search example in Java with
  GroupDocs.Search
og_title: Contoh full text search dalam Java menggunakan GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  headline: Full text search example in Java using GroupDocs.Search
  type: TechArticle
- description: Learn a full text search example in Java with GroupDocs.Search, covering
    adding documents to index, boolean query java, and performance optimization.
  name: Full text search example in Java using GroupDocs.Search
  steps:
  - name: create an index
    text: The `Index` class is the searchable container that stores indexed documents
      on disk.
  - name: add documents (add documents to index)
    text: You can index everything in a folder or limit to certain extensions using
      a `DocumentFilter`. > **Explanation:** > - `Index` represents the searchable
      database. > - `add()` ingests files; the wildcard `*.*` grabs all files, while
      `DocumentFilter` lets you fine‑tune the **add documents to index** ste
  - name: execute the search
    text: '> **Explanation:** > - `search()` runs the query against the index. > -
      `getDocumentCount()` tells you how many documents matched—useful for quick sanity
      checks.'
  type: HowTo
- questions:
  - answer: It indexes the raw text of every document so you can query any word or
      phrase instantly.
    question: What is full text search example?
  - answer: GroupDocs.Search for Java handles PDF, DOCX, XLSX, PPTX, HTML, TXT, and
      over 50 other file types.
    question: Which library supports multiple formats?
  - answer: Call the `index.add()` method with a folder path or a custom `DocumentFilter`.
    question: How do I add documents to index?
  - answer: Yes—combine terms with AND, OR, NOT for precise results.
    question: Can I run Boolean queries?
  - answer: Use incremental indexing, enable result caching, and disable phonetic
      search unless needed.
    question: How do I improve performance?
  type: FAQPage
tags:
- full text search
- GroupDocs.Search
- Java document indexing
- search performance
title: Contoh full text search dalam Java menggunakan GroupDocs.Search
type: docs
url: /id/java/searching/implement-full-text-search-java-groupdocs-search/
weight: 1
---

# Contoh pencarian teks penuh dalam Java dengan GroupDocs.Search

Jika Anda membutuhkan **full text search example** yang bekerja di seluruh PDF, file Word, spreadsheet, dan lainnya, Anda berada di tempat yang tepat. Memindai ribuan dokumen secara manual merupakan hambatan besar, tetapi GroupDocs.Search untuk Java mengotomatiskan pengindeksan dan kueri dengan kecepatan tinggi. Dalam tutorial ini kami akan membahas semua yang Anda perlukan untuk memulai— mulai dari menambahkan dokumen ke indeks, membuat pernyataan boolean query java, hingga mengoptimalkan kinerja pencarian untuk beban kerja produksi.

## Jawaban Cepat
- **Apa itu full text search example?** It indexes the raw text of every document so you can query any word or phrase instantly.  
- **Perpustakaan mana yang mendukung banyak format?** GroupDocs.Search for Java handles PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 50 other file types.  
- **Bagaimana cara menambahkan dokumen ke indeks?** Call the `index.add()` method with a folder path or a custom `DocumentFilter`.  
- **Apakah saya dapat menjalankan kueri Boolean?** Yes—combine terms with AND, OR, NOT for precise results.  
- **Bagaimana cara meningkatkan kinerja?** Use incremental indexing, enable result caching, and disable phonetic search unless needed.

## Apa itu full text search example?
A full text search example lets you scan the entire textual content of documents, store it in an efficient index, and retrieve matching records instantly. Unlike filename‑only searches, it looks inside PDFs, Word docs, spreadsheets, and other supported formats, making it ideal for document management systems, support portals, and any application where users need to locate information quickly.

## Mengapa menggunakan GroupDocs.Search untuk Java?
GroupDocs.Search for Java provides multi‑format support for over 50 file types, including PDF, DOCX, XLSX, PPTX, HTML and plain text. It scales to millions of files while keeping memory usage low by storing the index on disk. The library includes an advanced query language with built‑in Boolean, fuzzy and phonetic searches, and it integrates with a single Maven dependency, allowing you to start indexing within minutes.

## Prasyarat
Sebelum Anda memulai, pastikan Anda memiliki:

- **Java 11+** (Java 8 berfungsi, tetapi Java 11 atau lebih baru disarankan untuk kinerja yang lebih baik).  
- **Maven** untuk manajemen dependensi.  
- Sebuah lisensi **GroupDocs.Search** (kunci percobaan gratis sudah cukup untuk pengembangan).  

### Perpustakaan dan dependensi yang diperlukan
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

Untuk penggunaan detail lihat [dokumentasi](https://docs.groupdocs.com/search/java/).

### Pengaturan lingkungan
- Instal JDK (8 atau lebih baru) dan konfigurasikan `JAVA_HOME`.  
- Gunakan IDE seperti IntelliJ IDEA atau Eclipse untuk debugging yang lebih mudah.  

### Prasyarat pengetahuan
- Konsep dasar pemrograman Java.  
- Familiaritas dengan struktur `pom.xml` Maven.  

## Menyiapkan GroupDocs.Search untuk Java
Anda dapat membawa perpustakaan melalui Maven (ditunjukkan di atas) atau mengunduh JAR secara manual.

### Unduhan langsung (jika Anda lebih suka pengaturan manual)
Unduh paket terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Langkah-langkah memperoleh lisensi
1. **Free trial** – Daftar dan terima kunci sementara.  
2. **Temporary license** – Minta kunci jangka panjang untuk pengujian lanjutan.  
3. **Purchase** – Tingkatkan ke lisensi komersial penuh saat Anda siap untuk produksi.

### Inisialisasi dan pengaturan dasar
Create an index folder on disk and verify the library loads correctly:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index in the specified directory
        Index index = new Index("C:\\MyIndex");
        
        System.out.println("GroupDocs.Search initialized!");
    }
}
```

> **Pro tip:** Simpan direktori indeks pada SSD cepat untuk meminimalkan latensi kueri.

## Menambahkan dokumen ke indeks
**Mengapa ini penting:** No search results are possible without indexed content. Below we show how to add whole folders or filter specific file types.

### Langkah 1: buat indeks
The `Index` class is the searchable container that stores indexed documents on disk.

```java
Index index = new Index("C:\\MyIndex");
```

### Langkah 2: tambahkan dokumen (add documents to index)
You can index everything in a folder or limit to certain extensions using a `DocumentFilter`.

```java
index.add("C:\\Documents\\*.*"); // Adds all documents from the specified directory
// For specific file types, use:
index.add("C:\\Reports", new DocumentFilter() {
    @Override
    public boolean accept(String fileName) {
        return fileName.endsWith(".pdf") || fileName.endsWith(".docx");
    }
});
```

> **Penjelasan:**  
> - `Index` mewakili basis data yang dapat dicari.  
> - `add()` mengimpor file; wildcard `*.*` mengambil semua file, sementara `DocumentFilter` memungkinkan Anda menyesuaikan langkah **add documents to index**.

## Melakukan pencarian (search documents java)
Now that the index holds data, you can query it.

### Langkah 1: buat kueri
```java
String query = "GroupDocs";
```

### Langkah 2: jalankan pencarian
```java
SearchResult result = index.search(query);
System.out.println("Documents found: " + result.getDocumentCount());
```

> **Penjelasan:**  
> - `search()` menjalankan kueri terhadap indeks.  
> - `getDocumentCount()` memberi tahu berapa banyak dokumen yang cocok—berguna untuk pemeriksaan cepat.

## Teknik kueri lanjutan (boolean query java)
For precise control, combine terms with Boolean logic.

### Kueri Boolean
The `BooleanQuery` class lets you build complex expressions using AND, OR, NOT operators.

```java
String booleanQuery = "GroupDocs AND Java";
SearchResult booleanResult = index.search(booleanQuery);
```

### Pencarian fonetik (opsional untuk pencocokan fuzzy)
The `PhoneticSearch` feature enables phonetic matching for misspelled terms, but it adds overhead.

```java
index.getSettings().setPhoneticSearch(true);
```

> **Kapan digunakan:** Aktifkan pencarian fonetik hanya jika pengguna sering salah eja istilah; jika tidak, tetap nonaktifkan untuk **optimize search performance**.

## Masalah umum dan solusi
| Masalah | Mengapa terjadi | Solusi |
|---------|----------------|--------|
| **Dokumen hilang** | Path file tidak benar atau izin tidak cukup | Verifikasi path dan berikan akses baca |
| **Kueri lambat** | Indeks besar tanpa caching atau pencarian fonetik yang tidak perlu | Aktifkan caching, nonaktifkan pencarian fonetik, dan pertimbangkan memisahkan indeks |
| **Kesalahan Out‑of‑Memory** | Ukuran indeks melebihi heap JVM | Tingkatkan `-Xmx` atau gunakan pengindeksan incremental |

## Aplikasi praktis
GroupDocs.Search shines in real‑world scenarios:

1. **Content management systems** – Menyediakan pencarian teks penuh instan di seluruh artikel, PDF, dan aset media.  
2. **Customer support portals** – Agen dapat menemukan manual atau kebijakan yang relevan dalam hitungan detik.  
3. **Enterprise document repositories** – Mencari di seluruh kontrak, laporan, dan dokumen kepatuhan tanpa memindahkan data ke basis data terpisah.

## Pertimbangan kinerja
### Mengoptimalkan kinerja pencarian
- **Incremental indexing:** Tambahkan atau perbarui hanya file yang berubah alih-alih membangun ulang seluruh indeks.  
- **Caching:** Simpan hasil kueri yang sering digunakan di memori.  
- **Resource monitoring:** Sesuaikan heap JVM (`-Xmx2g` atau lebih tinggi) berdasarkan ukuran indeks.

### Pedoman penggunaan sumber daya
- Simpan folder indeks pada SSD atau drive NVMe yang cepat.  
- Pantau CPU dan memori selama pengindeksan massal; batasi operasi batch untuk menghindari lonjakan.

### Praktik terbaik untuk manajemen memori Java
- Gunakan `try‑with‑resources` saat bekerja dengan stream.  
- Setel objek besar ke null setelah digunakan untuk membantu pengumpulan sampah.

## Kesimpulan
You now have a complete, production‑ready **full text search example** in Java using GroupDocs.Search. From setting up the library, **adding documents to index**, crafting **boolean query java** statements, to **optimizing search performance**, every step is covered.  

### Langkah selanjutnya
Jelajahi fitur yang lebih dalam seperti analyzer khusus, kamus sinonim, dan integrasi penyimpanan cloud dengan memeriksa [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/).

---

## Pertanyaan yang sering diajukan

**Q:** Format file apa yang didukung oleh GroupDocs.Search?  
**A:** Lebih dari 50 format, termasuk PDF, DOCX, XLSX, PPTX, HTML, TXT, dan banyak jenis gambar.

**Q:** Bagaimana cara menangani dataset besar?  
**A:** Bagi menjadi beberapa indeks, perbarui secara incremental, dan aktifkan caching hasil untuk menjaga latensi tetap rendah.

**Q:** Apakah GroupDocs.Search dapat dijalankan di lingkungan cloud?  
**A:** Ya—Anda dapat mengarahkan folder indeks ke penyimpanan cloud yang dipasang (mis., Azure Blob, AWS S3 via driver sistem file).

**Q:** Apa keunggulan GroupDocs.Search dibanding perpustakaan lain?  
**A:** Dukungan multi‑format, kueri Boolean/phonetic bawaan, dan API Java yang ringan yang memproses jutaan dokumen dengan jejak memori rendah.

**Q:** Bagaimana cara mengatasi masalah kinerja?  
**A:** Tinjau pengaturan indeks, nonaktifkan pencarian fonetik jika tidak diperlukan, dan pantau penggunaan memori/CPU JVM selama pengindeksan dan kueri.

**Terakhir Diperbarui:** 2026-08-15  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs  

**Sumber Daya**  
- **Dokumentasi:** [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)  
- **Referensi API:** [Panduan Referensi API](https://reference.groupdocs.com/search/java)  
- **Unduhan:** [Rilis Terbaru](https://releases.groupdocs.com/search/java/)  
- **GitHub:** [Kode Sumber di GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Dukungan:** [Forum dan Dukungan Komunitas](https://forum.groupdocs.com/c/search/10)  
- **Lisensi:** [Minta Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Tutorial Terkait

- [Cara mengimplementasikan pencarian teks penuh java: buat direktori indeks dengan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Cara Menambahkan Dokumen ke Indeks dengan GroupDocs.Search untuk Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Meningkatkan Kinerja Kueri dengan GroupDocs.Search Java: Optimalkan Indeks & Pencarian](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)