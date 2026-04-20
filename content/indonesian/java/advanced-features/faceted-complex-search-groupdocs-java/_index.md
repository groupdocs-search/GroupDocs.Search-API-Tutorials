---
date: '2026-02-16'
description: Pelajari cara menggunakan operator boolean Java dengan GroupDocs.Search
  untuk membuat indeks pencarian, melakukan pencarian konten Java dan kueri berfaset,
  serta meningkatkan kinerja dan pengalaman pengguna.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Operator Boolean Java – Membuat Indeks Pencarian & Pencarian Berfaset
type: docs
url: /id/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

2026-02-16". Similarly "**Tested With:** GroupDocs.Search 25.4 for Java" -> "**Diuji Dengan:** GroupDocs.Search 25.4 for Java". "**Author:** GroupDocs" -> "**Penulis:** GroupDocs". Keep values unchanged.

Now ensure we preserve all markdown formatting, code block placeholders, links, images none.

Check for any shortcodes: none.

Now produce final content.

# Boolean Operators Java – Membuat Indeks Pencarian & Pencarian Berfasilitas

Menerapkan **pengalaman pencarian** yang kuat dalam Java dapat terasa menakutkan, terutama ketika Anda perlu **membuat indeks pencarian Java** yang mendukung **boolean operators Java** untuk pencarian berfasilitas dan kueri kompleks. Dalam tutorial ini kami akan menjelaskan cara menyiapkan **GroupDocs.Search for Java**, membangun indeks, menambahkan dokumen, dan membuat pencarian berfasilitas sederhana serta kueri multi‑kriteria yang canggih yang menggunakan logika Boolean. Pada akhir tutorial Anda akan memahami cara memanfaatkan **content search Java**, **filename search Java**, dan bahkan operasi **update index java** untuk menjaga data Anda tetap segar.

## Quick Answers
- **Apa itu pencarian berfasilitas?** Cara untuk memfilter hasil berdasarkan kategori yang telah ditentukan seperti tipe file atau tanggal.  
- **Bagaimana cara membuat indeks pencarian Java?** Inisialisasi objek `Index` yang menunjuk ke folder dan tambahkan dokumen.  
- **Apakah saya dapat menggabungkan beberapa kriteria dengan boolean operators?** Ya—gunakan kueri berbasis objek atau Boolean operators dalam kueri teks.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial menghilangkan batasan.  
- **IDE mana yang paling cocok?** Semua IDE Java (IntelliJ IDEA, Eclipse, NetBeans) dapat digunakan dengan baik.

## Apa itu “create search index java”?
Membuat indeks pencarian dalam Java berarti membangun struktur data yang dapat dicari yang menyimpan metadata dan konten dokumen, memungkinkan pengambilan cepat berdasarkan kueri pengguna. Dengan GroupDocs.Search, indeks disimpan di disk, dapat diperbarui secara inkremental, dan mendukung fitur lanjutan seperti faceting, **boolean operators Java**, serta logika Boolean yang kompleks.

## Mengapa menggunakan GroupDocs.Search untuk kueri berfasilitas dan kompleks?
- **Faceting siap pakai** – memfilter berdasarkan bidang seperti nama file, ukuran, atau metadata khusus.  
- **Bahasa kueri kaya** – menggabungkan kueri teks, frasa, dan bidang menggunakan operator AND/OR/NOT (inti dari **boolean operators java**).  
- **Kinerja skalabel** – mengindeks jutaan dokumen sambil menjaga latensi rendah.  
- **Pure Java** – tanpa dependensi native, bekerja pada platform apa pun yang menjalankan JDK 8+.  
- **Pemeliharaan indeks mudah** – panggil `index.update()` untuk **update index java** setelah menambahkan atau menghapus file.

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki hal berikut:

- **JDK 8 atau lebih baru** terpasang dan dikonfigurasi di IDE Anda.  
- **Maven** (atau Gradle) untuk manajemen dependensi.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Pemahaman dasar tentang konsep OOP Java dan struktur proyek Maven.

## Setting Up GroupDocs.Search for Java

### Maven Setup
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

### Unduhan Langsung
Sebagai alternatif, unduh JAR terbaru dari halaman rilis resmi:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Akuisisi Lisensi
Untuk membuka semua fungsi:

1. **Free trial** – sempurna untuk pengembangan dan pengujian.  
2. **Temporary evaluation license** – memperpanjang batas percobaan.  
3. **Commercial license** – menghilangkan semua batasan untuk penggunaan produksi.

### Inisialisasi dan Penyiapan Dasar
Potongan kode berikut menunjukkan cara **create search index java** dengan menginstansiasi kelas `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

Dengan indeks siap, kita dapat melanjutkan ke kueri berfasilitas dan kompleks dunia nyata.

## Cara menggunakan boolean operators java – Pencarian Berfasilitas Sederhana

Pencarian berfasilitas memungkinkan pengguna akhir mempersempit hasil dengan memilih nilai dari kategori yang telah ditentukan (facets). Di bawah ini adalah panduan langkah demi langkah.

### Langkah 1: Membuat Indeks
Pertama, arahkan `Index` ke folder tempat file indeks akan disimpan.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Langkah 2: Menambahkan Dokumen ke Indeks
Beritahu GroupDocs.Search di mana dokumen sumber Anda berada. Semua tipe file yang didukung (PDF, DOCX, TXT, dll.) akan diindeks secara otomatis.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Langkah 3: Lakukan Pencarian di Kolom Konten dengan Kueri Teks
Kueri teks cepat memfilter berdasarkan kolom `content`. Sintaks `content: Pellentesque` membatasi hasil ke dokumen yang mengandung kata *Pellentesque* dalam teks badan mereka.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Langkah 4: Lakukan Pencarian Menggunakan Object Query
Kueri berbasis objek memberi Anda kontrol yang lebih halus. Di sini kami membangun kueri kata, membungkusnya dalam kueri bidang, dan mengeksekusinya.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Cara menggunakan boolean operators java – Pencarian Kueri Kompleks

Kueri kompleks menggabungkan beberapa bidang, operator Boolean, dan pencarian frasa. Ini ideal untuk skenario seperti filter e‑commerce atau penelitian dokumen hukum.

### Langkah 1: Membuat Indeks untuk Kueri Kompleks
Gunakan kembali struktur folder yang sama; Anda dapat berbagi indeks antara skenario sederhana dan kompleks.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Langkah 2: Lakukan Pencarian dengan Kueri Teks
Kueri berikut mencari file yang bernama *lorem* **dan** *ipsum* **atau** konten yang mengandung salah satu dari dua frasa tepat.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Langkah 3: Lakukan Pencarian dengan Object Query
Konstruksi berbasis objek mencerminkan kueri teks tetapi menawarkan keamanan tipe dan bantuan IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Aplikasi Praktis Pencarian Berfasilitas & Kompleks

| Skenario | Bagaimana Faceting Membantu | Contoh Kueri |
|----------|----------------------------|--------------|
| **E‑commerce catalog** | Filter berdasarkan kategori, harga, merek | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | Menyaring berdasarkan nomor kasus, yurisdiksi | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | Menggabungkan penulis, tahun publikasi, kata kunci | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | Mencari berdasarkan tipe file dan departemen | `filetype: pdf AND department: HR` |

## Kesalahan Umum & Pemecahan Masalah

- **Hasil kosong** – Verifikasi bahwa dokumen berhasil ditambahkan (`index.getDocumentCount()` dapat membantu).  
- **Indeks usang** – Setelah menambahkan atau menghapus file, panggil `index.update()` untuk **update index java** dan menjaga indeks tetap sinkron.  
- **Nama bidang tidak tepat** – Gunakan konstanta `CommonFieldNames` (`Content`, `FileName`, dll.) untuk menghindari kesalahan pengetikan.  
- **Bottleneck kinerja** – Untuk koleksi besar, pertimbangkan mengaktifkan `index.setCacheSize()` atau menggunakan SSD khusus untuk folder indeks.  
- **Highlight hilang** – Untuk **highlight search results java**, ambil fragmen yang cocok melalui `SearchResult.getFragments()` (tidak ditampilkan di sini tetapi tersedia di API).  

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan GroupDocs.Search dengan Spring Boot?**  
A: Tentu saja. Tambahkan dependensi Maven, konfigurasikan indeks sebagai Spring bean, dan injeksikan di mana pun Anda membutuhkan kemampuan pencarian.

**Q: Apakah perpustakaan ini mendukung bidang metadata khusus?**  
A: Ya – Anda dapat menambahkan bidang yang didefinisikan pengguna selama proses pengindeksan dan kemudian melakukan faceting pada mereka.

**Q: Seberapa besar ukuran indeks yang dapat dicapai?**  
A: Indeks berbasis disk dan dapat menangani jutaan dokumen; cukup pastikan penyimpanan cukup dan pantau pengaturan cache.

**Q: Apakah ada cara untuk memberi peringkat hasil berdasarkan relevansi?**  
A: GroupDocs.Search secara otomatis memberi skor pada kecocokan; Anda dapat mengambil skor melalui `SearchResult.getDocument(i).getScore()`.

**Q: Apa yang terjadi jika saya mengindeks PDF terenkripsi?**  
A: Berikan kata sandi saat menambahkan dokumen: `index.add(filePath, password)`.

## Kesimpulan

Sekarang Anda seharusnya merasa nyaman **creating a search index Java** dengan GroupDocs.Search, menambahkan dokumen, dan membuat kueri berfasilitas sederhana serta pencarian Boolean yang canggih menggunakan **boolean operators java**. Kemampuan ini memungkinkan Anda memberikan pengalaman pencarian yang cepat, akurat, dan ramah pengguna di berbagai aplikasi—dari platform e‑commerce hingga basis pengetahuan perusahaan.

Siap untuk langkah selanjutnya? Jelajahi fitur lanjutan **GroupDocs.Search** seperti **highlighting**, **suggestions**, dan **real‑time indexing** untuk lebih meningkatkan kekuatan pencarian aplikasi Anda.

---

**Terakhir Diperbarui:** 2026-02-16  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs