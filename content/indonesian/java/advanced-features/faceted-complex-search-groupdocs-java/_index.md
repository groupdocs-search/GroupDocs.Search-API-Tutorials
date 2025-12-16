---
date: '2025-12-16'
description: Pelajari cara membuat indeks pencarian Java dan mengimplementasikan pencarian
  berfaset serta kompleks menggunakan GroupDocs.Search, meningkatkan kinerja pencarian
  dan pengalaman pengguna.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Buat Indeks Pencarian Java – Pencarian Berfaset & Kompleks
type: docs
url: /id/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Buat Indeks Pencarian Java – Pencarian Berfaset & Kompleks

Mengimplementasikan **pengalaman pencarian** yang kuat di Java dapat terasa menakutkan, terutama ketika Anda perlu **membuat indeks pencarian Java** proyek yang menangani koleksi dokumen besar. Untungnya, **GroupDocs.Search for Java** menyediakan API yang kaya yang memungkinkan Anda membangun kueri berfaset dan kompleks dengan hanya beberapa baris kode. Dalam tutorial ini Anda akan menemukan cara menyiapkan pustaka, **membuat indeks pencarian Java**, menambahkan dokumen, dan menjalankan pencarian berfaset sederhana serta kueri multi‑kriteria yang canggih.

## Jawaban Cepat
- **Apa itu pencarian berfaset?** Cara menyaring hasil berdasarkan kategori yang telah ditentukan (mis., tipe file, tanggal).  
- **Bagaimana cara membuat indeks pencarian Java?** Inisialisasi objek `Index` yang menunjuk ke folder dan tambahkan dokumen.  
- **Bisakah saya menggabungkan beberapa kriteria?** Ya—gunakan kueri berbasis objek atau operator Boolean dalam kueri teks.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial menghapus batasan.  
- **IDE mana yang paling cocok?** Semua IDE Java (IntelliJ IDEA, Eclipse, NetBeans) berfungsi dengan baik.

## Apa itu “create search index java”?
Membuat indeks pencarian di Java berarti membangun struktur data yang dapat dicari yang menyimpan metadata dokumen dan kontennya, memungkinkan pengambilan cepat berdasarkan kueri pengguna. Dengan GroupDocs.Search, indeks disimpan di disk, dapat diperbarui secara inkremental, dan mendukung fitur lanjutan seperti faset dan logika Boolean kompleks.

## Mengapa menggunakan GroupDocs.Search untuk kueri berfaset dan kompleks?
- **Faseting siap pakai** – menyaring berdasarkan bidang seperti nama file, ukuran, atau metadata khusus.  
- **Bahasa kueri kaya** – menggabungkan kueri teks, frasa, dan bidang menggunakan operator AND/OR/NOT.  
- **Kinerja skalabel** – mengindeks jutaan dokumen sambil menjaga latensi pencarian tetap rendah.  
- **Java murni** – tanpa dependensi native, berfungsi di platform apa pun yang menjalankan JDK 8+.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal berikut:

- **JDK 8 atau lebih baru** terpasang dan dikonfigurasi di IDE Anda.  
- **Maven** (atau Gradle) untuk manajemen dependensi.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Familiaritas dasar dengan konsep OOP Java dan struktur proyek Maven.

## Menyiapkan GroupDocs.Search untuk Java

### Pengaturan Maven
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

1. **Uji coba gratis** – sempurna untuk pengembangan dan pengujian.  
2. **Lisensi evaluasi sementara** – memperpanjang batas uji coba.  
3. **Lisensi komersial** – menghapus semua pembatasan untuk penggunaan produksi.

### Inisialisasi dan Penyiapan Dasar
Potongan kode berikut menunjukkan cara **membuat indeks pencarian Java** dengan menginstansiasi kelas `Index`:

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

Dengan indeks siap, kita dapat melanjutkan ke kueri berfaset dan kompleks dunia nyata.

## Cara membuat search index java – Pencarian Berfaset Sederhana

Pencarian berfaset memungkinkan pengguna akhir mempersempit hasil dengan memilih nilai dari kategori yang telah ditentukan (faset). Berikut adalah panduan langkah demi langkah.

### Langkah 1: Buat Indeks
Pertama, arahkan `Index` ke folder tempat file indeks akan disimpan.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Langkah 2: Tambahkan Dokumen ke Indeks
Beritahu GroupDocs.Search di mana dokumen sumber Anda berada. Semua tipe file yang didukung (PDF, DOCX, TXT, dll.) akan diindeks secara otomatis.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Langkah 3: Lakukan Pencarian di Kolom Konten dengan Kueri Teks
Kueri teks cepat menyaring berdasarkan kolom `content`. Sintaks `content: Pellentesque` membatasi hasil ke dokumen yang mengandung kata *Pellentesque* dalam teks utama mereka.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Langkah 4: Lakukan Pencarian Menggunakan Kueri Objek
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

## Cara membuat search index java – Pencarian Kueri Kompleks

Kueri kompleks menggabungkan beberapa bidang, operator Boolean, dan pencarian frasa. Ini ideal untuk skenario seperti filter e‑commerce atau penelitian dokumen hukum.

### Langkah 1: Buat Indeks untuk Kueri Kompleks
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

### Langkah 3: Lakukan Pencarian dengan Kueri Objek
Konstruksi berbasis objek mencerminkan kueri tekstual tetapi menawarkan keamanan tipe dan bantuan IDE.

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

## Aplikasi Praktis Pencarian Berfaset & Kompleks

| Scenario | How Faceting Helps | Example Query |
|----------|-------------------|---------------|
| **Katalog E‑commerce** | Filter by category, price, brand | `category: Electronics AND price:[100 TO 500]` |
| **Repositori Dokumen Hukum** | Narrow by case number, jurisdiction | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Arsip Penelitian** | Combine author, publication year, keywords | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Intranet Perusahaan** | Search by file type and department | `filetype: pdf AND department: HR` |

## Kesalahan Umum & Pemecahan Masalah

- **Hasil kosong** – Pastikan dokumen berhasil ditambahkan (`index.getDocumentCount()` dapat membantu).  
- **Indeks usang** – Setelah menambahkan atau menghapus file, panggil `index.update()` untuk menjaga indeks tetap sinkron.  
- **Nama bidang tidak tepat** – Gunakan konstanta `CommonFieldNames` (`Content`, `FileName`, dll.) untuk menghindari kesalahan ketik.  
- **Bottleneck kinerja** – Untuk koleksi besar, pertimbangkan mengaktifkan `index.setCacheSize()` atau menggunakan SSD khusus untuk folder indeks.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan GroupDocs.Search dengan Spring Boot?**  
A: Tentu saja. Cukup tambahkan dependensi Maven, konfigurasikan indeks sebagai bean Spring, dan injeksikan di tempat yang diperlukan.

**Q: Apakah pustaka ini mendukung bidang metadata khusus?**  
A: Ya – Anda dapat menambahkan bidang yang didefinisikan pengguna selama proses pengindeksan dan kemudian melakukan faset pada bidang tersebut.

**Q: Seberapa besar indeks dapat tumbuh?**  
A: Indeks berbasis disk dan dapat menangani jutaan dokumen; pastikan penyimpanan cukup dan pantau pengaturan cache.

**Q: Apakah ada cara untuk memberi peringkat hasil berdasarkan relevansi?**  
A: GroupDocs.Search secara otomatis memberi skor pada kecocokan; Anda dapat mengambil skor melalui `SearchResult.getDocument(i).getScore()`.

**Q: Apa yang terjadi jika saya mengindeks PDF terenkripsi?**  
A: Berikan kata sandi saat menambahkan dokumen: `index.add(filePath, password)`.

## Kesimpulan

Sekarang Anda seharusnya merasa nyaman **membuat indeks pencarian Java** dengan GroupDocs.Search, menambahkan dokumen, dan menyusun baik kueri berfaset sederhana maupun pencarian Boolean yang canggih. Kemampuan ini memungkinkan Anda memberikan pengalaman pencarian yang cepat, akurat, dan ramah pengguna di berbagai aplikasi—dari platform e‑commerce hingga basis pengetahuan perusahaan.

Siap untuk langkah berikutnya? Jelajahi fitur lanjutan **GroupDocs.Search** seperti **penyorotan**, **saran**, dan **pengindeksan waktu nyata** untuk lebih meningkatkan kekuatan pencarian aplikasi Anda.

**Terakhir Diperbarui:** 2025-12-16  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs