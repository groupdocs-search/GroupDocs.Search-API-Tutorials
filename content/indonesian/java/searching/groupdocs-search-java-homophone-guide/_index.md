---
date: '2026-05-28'
description: Pelajari cara membuat indeks java, menambahkan dokumen ke indeks, dan
  mengaktifkan pencarian homofon menggunakan GroupDocs.Search for Java untuk pengambilan
  yang cepat dan akurat.
keywords:
- create index java
- how to use homophone
- add documents to index
- search with homophone
- java search tutorial
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to create index java, add documents to index, and enable
    homophone search using GroupDocs.Search for Java for fast, accurate retrieval.
  headline: How to create index java with GroupDocs.Search and Enable Homophone Search
  type: TechArticle
- description: Learn how to create index java, add documents to index, and enable
    homophone search using GroupDocs.Search for Java for fast, accurate retrieval.
  name: How to create index java with GroupDocs.Search and Enable Homophone Search
  steps:
  - name: Define the Index Path
    text: Replace `YOUR_DOCUMENT_DIRECTORY` with the absolute path on your machine.
  - name: Instantiate the Index Object
    text: This line **creates the index** that will later hold all searchable content.
  - name: Point to Your Source Documents
    text: This folder should contain the files (PDF, DOCX, TXT, etc.) you wish to
      index.
  - name: Add All Files in the Folder
    text: The `add` method processes each file, extracts text, and stores term‑frequency
      data, effectively **adding documents to index**.
  - name: Create SearchOptions
    text: '`SearchOptions` configures how the engine interprets queries.'
  - name: Activate Homophone Search
    text: Setting `setUseHomophoneSearch(true)` tells the engine to consider phonetic
      equivalents when processing queries.
  type: HowTo
- questions:
  - answer: Initialize the `Index` object with a folder path.
    question: What is the first step to create an index?
  - answer: '`index.add(yourDocumentsFolder)`.'
    question: Which method adds files to the index?
  - answer: Set `options.setUseHomophoneSearch(true)`.
    question: How do I enable homophone search?
  - answer: A free trial or temporary license works for evaluation.
    question: Do I need a license?
  - answer: JDK 8 or later.
    question: Which Java version is required?
  type: FAQPage
title: Cara membuat indeks java dengan GroupDocs.Search dan Mengaktifkan Pencarian
  Homofon
type: docs
url: /id/java/searching/groupdocs-search-java-homophone-guide/
weight: 1
---

# Cara membuat indeks java dengan GroupDocs.Search dan Mengaktifkan Pencarian Homofon

Di perusahaan modern, **create index java** dengan cepat dan andal dapat menjadi perbedaan antara menemukan informasi penting atau kehilangan sepenuhnya. Baik Anda mengindeks kontrak hukum, umpan balik pelanggan, atau laporan internal, indeks pencarian yang dibangun dengan baik yang didukung oleh GroupDocs.Search untuk Java memberikan hasil yang instan dan akurat. Dalam tutorial ini kami akan membahas seluruh proses—mulai dari menyiapkan pustaka, membuat indeks, menambahkan dokumen, hingga mengaktifkan pencarian homofon untuk kueri yang lebih cerdas.

## Jawaban Cepat
- **Apa langkah pertama untuk membuat indeks?** Initialize the `Index` object with a folder path.  
- **Metode mana yang menambahkan file ke indeks?** `index.add(yourDocumentsFolder)`.  
- **Bagaimana cara mengaktifkan pencarian homofon?** Set `options.setUseHomophoneSearch(true)`.  
- **Apakah saya memerlukan lisensi?** A free trial or temporary license works for evaluation.  
- **Versi Java apa yang diperlukan?** JDK 8 or later.

## Apa itu Indeks dalam GroupDocs.Search?
`Index` adalah kelas inti yang menyimpan istilah yang dapat dicari dan lokasinya di seluruh dokumen. **Index** adalah struktur data inti GroupDocs.Search yang menyimpan istilah dan lokasinya di koleksi dokumen Anda, memungkinkan pencarian super cepat. Ia berfungsi seperti indeks buku tetapi dapat menangani jutaan istilah di puluhan format file, menyediakan pengambilan cepat bahkan untuk korpus besar.

## Mengapa Mengaktifkan Pencarian Homofon?
Pencarian homofon memperluas kueri untuk menyertakan kata-kata yang terdengar serupa (misalnya, “write” vs. “right”). Ini meningkatkan recall hingga **30 % dalam skenario input pengguna yang berisik**, memastikan pengguna mendapatkan hasil bahkan ketika mereka salah eja atau menggunakan ejaan alternatif. Ini sangat berharga untuk antarmuka berbasis suara dan lingkungan multibahasa.

## Prasyarat
- **Java Development Kit** 8 atau yang lebih baru.  
- **GroupDocs.Search for Java** library (tersedia via Maven).  
- Familiaritas dasar dengan sintaks Java dan penyiapan proyek.  

## Menyiapkan GroupDocs.Search untuk Java

Pertama, tambahkan repositori Maven GroupDocs.Search dan dependensinya ke `pom.xml` Anda:

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

Sebagai alternatif, Anda dapat [mengunduh versi terbaru dari rilis GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

**License Acquisition**: GroupDocs menawarkan lisensi percobaan gratis atau lisensi sementara untuk evaluasi. Untuk membeli, kunjungi situs resmi mereka.

### Inisialisasi dan Penyiapan Dasar

Buat kelas Java sederhana untuk menginisialisasi indeks pencarian:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        // Specify the path to store index files
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\HomophoneSearch";
        
        // Create an instance of Index
        Index index = new Index(indexFolder);
        
        System.out.println("Index created successfully!");
    }
}
```

## Cara membuat indeks java dengan GroupDocs.Search Java?
`Index` adalah kelas utama yang mewakili indeks yang dapat dicari yang disimpan di disk. Muat atau buat indeks dengan mengarahkan konstruktor `Index` ke folder tempat pustaka dapat menyimpan file internalnya. Operasi ini membuat file metadata yang diperlukan dan menyiapkan mesin untuk ingest dokumen, memungkinkan penambahan dokumen selanjutnya dan eksekusi kueri.

### Langkah 1: Tentukan Jalur Indeks
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\HomophoneSearch";
```  
Ganti `YOUR_DOCUMENT_DIRECTORY` dengan jalur absolut di mesin Anda.

### Langkah 2: Buat Instance Objek Index
```java
Index index = new Index(indexFolder);
```  
Baris ini **membuat indeks** yang nantinya akan menampung semua konten yang dapat dicari.

## Cara menambahkan dokumen ke indeks?
`add` adalah metode dari kelas `Index` yang mengimpor file dari folder ke dalam indeks. Setelah indeks ada, Anda perlu mengisinya dengan dokumen yang ingin Anda cari. Metode `add` memindai direktori secara rekursif dan mengindeks setiap file yang didukung, mengekstrak teks dan membangun tabel frekuensi istilah untuk pengambilan cepat.

### Langkah 1: Arahkan ke Dokumen Sumber Anda
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  
Folder ini harus berisi file (PDF, DOCX, TXT, dll.) yang ingin Anda indeks.

### Langkah 2: Tambahkan Semua File di Folder
```java
index.add(documentsFolder);
```  
Metode `add` memproses setiap file, mengekstrak teks, dan menyimpan data frekuensi istilah, secara efektif **menambahkan dokumen ke indeks**.

## Cara mengaktifkan pencarian homofon?
`setUseHomophoneSearch` adalah metode dari `SearchOptions` yang mengaktifkan pencocokan fonetik untuk kueri. Sekarang indeks telah terisi, Anda dapat mengaktifkan pencocokan fonetik untuk menangkap istilah yang terdengar serupa. Mengaktifkan fitur ini memberi instruksi kepada mesin untuk mempertimbangkan ekivalen fonetik selama pemrosesan kueri, meningkatkan recall untuk input yang salah eja atau diucapkan.

### Langkah 1: Buat SearchOptions
```java
import com.groupdocs.search.SearchOptions;

SearchOptions options = new SearchOptions();
```  
`SearchOptions` mengkonfigurasi cara mesin menafsirkan kueri.

### Langkah 2: Aktifkan Pencarian Homofon
```java
options.setUseHomophoneSearch(true);
```  
Menetapkan `setUseHomophoneSearch(true)` memberi tahu mesin untuk mempertimbangkan ekivalen fonetik saat memproses kueri.

## Aplikasi Praktis
1. **Legal Document Management** – Temukan kontrak yang menyebut “lease” bahkan jika pengguna mengetik “leas”.  
2. **Customer Feedback Analysis** – Tangkap variasi seperti “price” dan “prise” dalam tanggapan survei.  
3. **Content Management Systems** – Tingkatkan pencarian situs dengan mencocokkan “write” dengan “right”.

## Pertimbangan Kinerja
- **Regularly rebuild** indeks setelah pembaruan dokumen massal untuk menjaga statistik istilah tetap segar.  
- **Monitor memory** usage; mesin dapat memproses dokumen ratusan halaman tanpa memuat seluruh file ke memori berkat indeks inkremental.  
- Ikuti praktik terbaik Java (mis., try‑with‑resources, penanganan pengecualian yang tepat) untuk menjaga aplikasi tetap stabil di bawah beban.

## Kesimpulan
Anda kini tahu **cara membuat indeks java**, cara **menambahkan dokumen ke indeks**, dan cara mengaktifkan pencarian homofon dengan GroupDocs.Search untuk Java. Kemampuan ini memungkinkan Anda membangun pengalaman pencarian yang cepat dan cerdas di seluruh repositori dokumen apa pun.

### Langkah Selanjutnya
- Bereksperimen dengan **custom analyzers** untuk menyempurnakan tokenisasi.  
- Gabungkan **faceted search** dengan dukungan homofon untuk penyaringan yang lebih kaya.  
- Jelajahi **GroupDocs.Search REST API** untuk skenario lintas‑platform.

## Pertanyaan yang Sering Diajukan

**Q:** Apa itu indeks dalam konteks GroupDocs.Search?  
A: Indeks adalah struktur data yang memetakan istilah ke lokasi mereka dalam dokumen, memungkinkan pengambilan dalam tingkat milidetik serupa dengan indeks buku.

**Q:** Bagaimana cara memperbarui indeks saya dengan dokumen baru?  
A: Panggil `index.add(newFolder)` untuk mengimpor file tambahan atau mengindeks ulang yang sudah ada; mesin memperbarui tabel istilah secara inkremental.

**Q:** Bisakah GroupDocs.Search menangani volume data yang besar?  
A: Ya, ia dapat diskalakan hingga jutaan dokumen dan mendukung pemrosesan file lebih dari 500 MB tanpa memuat seluruh konten ke memori.

**Q:** Apa itu homofon dalam fungsi pencarian?  
A: Homofon adalah kata-kata yang terdengar serupa tetapi berbeda dalam ejaan, seperti “write” dan “right”; mengaktifkan fitur ini memperluas cakupan kueri.

**Q:** Bagaimana cara mengatasi kesalahan pengindeksan?  
A: Verifikasi jalur file, pastikan izin baca, dan tinjau output log untuk pesan pengecualian spesifik; masalah umum meliputi format yang tidak didukung atau file yang rusak.

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/search/java/)
- [Referensi API](https://reference.groupdocs.com/search/java)
- [Unduh Versi Terbaru](https://releases.groupdocs.com/search/java/)
- [Repositori GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

**Terakhir Diperbarui:** 2026-05-28  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs  

## Tutorial Terkait

- [Tambahkan Dokumen ke Indeks – Tutorial GroupDocs.Search Java](/search/java/document-management/)
- [Cara Membuat Indeks dengan GroupDocs.Search di Java - Panduan Lengkap](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Buat Indeks Java dengan GroupDocs.Search | Panduan Pengindeksan dan Pelaporan Komprehensif](/search/java/advanced-features/groupdocs-search-java-index-report-guide/)