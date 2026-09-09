---
date: '2026-08-26'
description: Pelajari bagaimana boolean operators Java memungkinkan Anda membangun
  search index yang cepat, melakukan content search Java, dan menjalankan faceted
  queries dengan GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Pelajari bagaimana boolean operators Java memungkinkan Anda membangun
  search index yang cepat, melakukan content search Java, dan mengeksekusi faceted
  queries dengan GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – bangun search index dan faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – buat search index & faceted search
type: docs
url: /id/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Operator Boolean Java – buat indeks pencarian & pencarian berfaset

Implementasi **pengalaman pencarian** yang kuat dalam Java dapat terasa menakutkan, terutama ketika Anda perlu **create a search index Java** yang mendukung **boolean operators Java** untuk pencarian berfaset dan kueri kompleks. Dalam tutorial ini kami akan memandu penyiapan **GroupDocs.Search for Java**, membangun indeks, menambahkan dokumen, dan membuat pencarian berfaset sederhana serta kueri multi‑kriteria yang canggih menggunakan logika Boolean. Pada akhir tutorial Anda akan memahami cara memanfaatkan operasi **content search Java**, **filename search Java**, dan bahkan **update index Java** untuk menjaga data tetap segar.

## Jawaban Cepat
- **Apa itu pencarian berfaset?** Cara untuk memfilter hasil berdasarkan kategori yang telah ditentukan seperti tipe file atau tanggal.  
- **Bagaimana cara membuat search index Java?** Inisialisasi objek `Index` yang menunjuk ke folder dan tambahkan dokumen.  
- **Bisakah saya menggabungkan beberapa kriteria dengan boolean operators?** Ya—gunakan kueri berbasis objek atau Boolean operators dalam kueri teks.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial menghapus batasan.  
- **IDE mana yang paling cocok?** Semua IDE Java (IntelliJ IDEA, Eclipse, NetBeans) dapat digunakan dengan baik.

## Apa itu “create search index java”?
Membuat search index Java berarti membangun struktur berbasis disk yang menyimpan teks dokumen dan metadata, memungkinkan pengambilan instan dokumen yang cocok melalui kueri. Indeks memetakan istilah ke pengidentifikasi dokumen, mendukung pencarian cepat, dan dapat diperbarui secara inkremental saat file berubah, menyediakan fondasi untuk fitur pencarian yang kuat.

## Mengapa menggunakan GroupDocs.Search untuk pencarian berfaset dan kueri kompleks?
GroupDocs.Search untuk Java menyediakan faceting bawaan, dukungan kueri Boolean, dan pengindeksan berperforma tinggi yang dapat menangani hingga 10 juta dokumen sambil menjaga latensi kueri di bawah 200 ms pada perangkat keras server standar. Ini menawarkan filter bidang siap pakai, bahasa kueri yang kaya, dan kompatibilitas pure‑Java, menjadikannya ideal untuk skenario pencarian skala perusahaan.

## Prasyarat
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

### Perolehan Lisensi
Untuk membuka semua fungsi:

1. **Free trial** – sempurna untuk pengembangan dan pengujian.  
2. **Temporary evaluation license** – memperpanjang batas percobaan.  
3. **Commercial license** – menghapus semua pembatasan untuk penggunaan produksi.

### Inisialisasi dan Pengaturan Dasar
Kelas `Index` adalah komponen inti yang mewakili indeks yang dapat dicari yang disimpan di disk. Potongan kode berikut menunjukkan cara **create a search index Java** dengan menginstansiasi kelas `Index`:

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

Dengan indeks siap, kami dapat melanjutkan ke kueri berfaset dan kompleks dunia nyata.

## Cara menggunakan boolean operators java – Pencarian berfaset sederhana

Muat indeks Anda, tambahkan dokumen, dan lakukan kueri bidang; pola dua‑langkah memungkinkan Anda mengambil hitungan faset dan hasil yang difilter dalam satu panggilan. Pendekatan ini memberi pengguna cara intuitif untuk mempersempit hasil berdasarkan kategori seperti tipe file, penulis, atau metadata khusus.

### Langkah 1: Buat indeks
Pertama, arahkan `Index` ke folder tempat file indeks akan disimpan.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Langkah 2: Tambahkan dokumen ke indeks
Beritahu GroupDocs.Search di mana dokumen sumber Anda berada. Semua tipe file yang didukung (PDF, DOCX, TXT, dll.) akan diindeks secara otomatis.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Langkah 3: Lakukan pencarian di bidang konten dengan kueri teks
Kueri teks cepat memfilter berdasarkan bidang `content`. Sintaks `content: Pellentesque` membatasi hasil pada dokumen yang mengandung kata *Pellentesque* dalam teks badan mereka.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Langkah 4: Lakukan pencarian menggunakan kueri objek
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

## Cara menggunakan boolean operators java – Pencarian kueri kompleks

Untuk mengeksekusi kueri kompleks, gabungkan beberapa kondisi bidang dengan operator AND/OR/NOT, dan secara opsional sertakan pencarian frasa. Anda dapat menentukan setiap kondisi menggunakan kueri bidang, menumpuknya dengan Boolean operators, dan mengontrol relevansi dengan boosting, memungkinkan Anda mengambil hanya dokumen paling relevan yang memenuhi semua kriteria yang diperlukan.

### Langkah 1: Buat indeks untuk kueri kompleks
Gunakan kembali struktur folder yang sama; Anda dapat berbagi indeks antara skenario sederhana dan kompleks.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Langkah 2: Lakukan pencarian dengan kueri teks
Kueri berikut mencari file bernama *lorem* **and** *ipsum* **or** konten yang berisi salah satu dari dua frasa tepat.

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

### Langkah 3: Lakukan pencarian dengan kueri objek
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

## Aplikasi praktis pencarian berfaset & kompleks

| Skenario | Bagaimana faceting membantu | Contoh kueri |
|----------|----------------------------|--------------|
| **Katalog e‑commerce** | Filter berdasarkan kategori, harga, merek | `category: Electronics AND price:[100 TO 500]` |
| **Repositori dokumen hukum** | Persempit berdasarkan nomor kasus, yurisdiksi | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Arsip penelitian** | Gabungkan penulis, tahun publikasi, kata kunci | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Intranet perusahaan** | Cari berdasarkan tipe file dan departemen | `filetype: pdf AND department: HR` |

Contoh-contoh ini menggambarkan mengapa menguasai teknik **boolean operators java** dan **filename search java** menjadi pengubah permainan bagi aplikasi yang intensif data.

## Jebakan umum & pemecahan masalah

Objek `SearchResult` berisi dokumen yang cocok dengan kueri dan menyediakan akses ke skor relevansi serta fragmen yang disorot.  
Kelas `CommonFieldNames` mendefinisikan nama bidang standar seperti `Content` dan `FileName` yang digunakan di seluruh API.

- **Empty results** – Verifikasi bahwa dokumen berhasil ditambahkan (`index.getDocumentCount()` dapat membantu).  
- **Stale index** – Setelah menambahkan atau menghapus file, panggil `index.update()` untuk **update index java** dan menjaga indeks tetap sinkron.  
- **Incorrect field names** – Gunakan konstanta `CommonFieldNames` (`Content`, `FileName`, dll.) untuk menghindari kesalahan pengetikan.  
- **Performance bottlenecks** – Untuk koleksi besar, pertimbangkan mengaktifkan `index.setCacheSize()` atau menggunakan SSD khusus untuk folder indeks.  
- **Missing highlights** – Untuk **highlight search results java**, ambil fragmen yang cocok melalui `SearchResult.getFragments()` (tidak ditampilkan di sini tetapi tersedia di API).  

## Pertanyaan yang sering diajukan

**Q: Bisakah saya menggunakan GroupDocs.Search dengan Spring Boot?**  
A: Tentu saja. Tambahkan dependensi Maven, konfigurasikan indeks sebagai bean Spring, dan injeksikan di mana pun Anda memerlukan kemampuan pencarian.

**Q: Apakah perpustakaan mendukung bidang metadata khusus?**  
A: Ya – Anda dapat menambahkan bidang yang didefinisikan pengguna selama pengindeksan dan kemudian melakukan faceting pada mereka.

**Q: Seberapa besar indeks dapat tumbuh?**  
A: Indeks berbasis disk dapat menangani hingga 10 juta dokumen; pastikan penyimpanan cukup dan pantau pengaturan cache.

**Q: Apakah ada cara untuk memberi peringkat hasil berdasarkan relevansi?**  
A: GroupDocs.Search secara otomatis memberi skor pada kecocokan; Anda dapat mengambil skor melalui `SearchResult.getDocument(i).getScore()`.

**Q: Apa yang terjadi jika saya mengindeks PDF terenkripsi?**  
A: Berikan kata sandi saat menambahkan dokumen: `index.add(filePath, password)`.

## Kesimpulan

Pada saat ini Anda seharusnya merasa nyaman **create a search index Java** dengan GroupDocs.Search, menambahkan dokumen, dan membuat baik kueri berfaset sederhana maupun pencarian Boolean yang canggih menggunakan **boolean operators java**. Kemampuan ini memungkinkan Anda memberikan pengalaman pencarian yang cepat, akurat, dan ramah pengguna di berbagai aplikasi—dari platform e‑commerce hingga basis pengetahuan perusahaan.

Siap untuk langkah selanjutnya? Jelajahi fitur lanjutan **GroupDocs.Search** seperti **highlighting**, **suggestions**, dan **real‑time indexing** untuk lebih meningkatkan kekuatan pencarian aplikasi Anda.

**Terakhir Diperbarui:** 2026-08-26  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Wildcard Search Java dengan GroupDocs.Search – Fitur Lanjutan](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Cara Memperbarui Index Java dengan GroupDocs.Search – Panduan Komprehensif](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Cara mengimplementasikan pencarian teks penuh java: buat direktori indeks dengan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)