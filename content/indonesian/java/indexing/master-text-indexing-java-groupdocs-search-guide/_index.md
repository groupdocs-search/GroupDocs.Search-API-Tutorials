---
date: '2026-11-02'
description: Pelajari cara menambahkan folder ke indeks dengan GroupDocs.Search di
  Java, mengonfigurasi kompresi tinggi, dan menjalankan kueri teks lengkap yang cepat.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Pelajari cara menambahkan folder ke indeks dengan GroupDocs.Search
  di Java, mengonfigurasi kompresi, dan mengeksekusi pencarian teks lengkap yang cepat.
  Ideal untuk kumpulan dokumen besar.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Cara menambahkan folder ke indeks dengan GroupDocs.Search di Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: Cara menambahkan folder ke indeks dengan GroupDocs.Search di Java
type: docs
url: /id/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# Cara menambahkan folder ke indeks dengan GroupDocs.Search di Java

Jika Anda membutuhkan **java full text search** yang dapat diskalakan hingga jutaan dokumen, Anda berada di tempat yang tepat. Dalam tutorial ini Anda akan belajar cara **menambahkan folder ke indeks** menggunakan GroupDocs.Search, mengonfigurasi penyimpanan kompresi tinggi, dan menjalankan kueri super cepat. Pada akhir tutorial Anda akan memiliki solusi siap produksi yang dapat Anda masukkan ke proyek Java mana pun.

## Jawaban Cepat
- **Apa perpustakaan utama?** GroupDocs.Search for Java  
- **Bagaimana cara menambahkan folder ke indeks?** Use `index.add(folderPath)`  
- **Apakah saya dapat mengonfigurasi kompresi teks?** Yes, via `TextStorageSettings(Compression.High)`  
- **Versi Java apa yang diperlukan?** JDK 8 or higher  
- **Di mana mendapatkan lisensi percobaan?** From the GroupDocs website or the repository page  

## Apa itu java full text search dan mengapa penting?

Java full text search mengubah dokumen mentah menjadi indeks terbalik, memungkinkan pengambilan istilah dalam hitungan sub‑detik di antara ribuan file. Kemampuan ini penting untuk repositori hukum, perpustakaan riset, dan basis pengetahuan perusahaan di mana pengguna mengharapkan hasil instan. Ini juga meningkatkan produktivitas dalam aplikasi modern.

## Mengapa menggunakan groupdocs.search untuk java full text search?

GroupDocs.Search menyediakan pengindeksan dan eksekusi kueri dengan throughput tinggi sambil menawarkan kompresi tinggi bawaan. Ia mendukung **lebih dari 50 format input dan output**—termasuk PDF, DOCX, EML, dan HTML—dan dapat memproses dokumen berukuran ratusan halaman tanpa memuat seluruh file ke memori, menjaga jejak memori di bawah 200 MB untuk beban kerja tipikal.

## Prasyarat

- **GroupDocs.Search for Java** (version 25.4 atau lebih baru) – perpustakaan inti yang menggerakkan pengindeksan dan pencarian.  
- **JDK 8+** terpasang dan dikonfigurasi – runtime minimum yang diperlukan untuk SDK.  
- **Maven** untuk manajemen dependensi – mempermudah menambahkan perpustakaan ke proyek Anda.  
- IDE seperti **IntelliJ IDEA** atau **Eclipse** – untuk menulis dan men-debug kode Java.

## Menyiapkan GroupDocs.Search untuk java

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
Sebagai alternatif, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Akuisisi Lisensi
- **Free trial** – jelajahi semua fitur tanpa komitmen.  
- **Temporary license** – periode pengujian yang diperpanjang.  
- **Purchase** – membuka semua kemampuan produksi.  

### Inisialisasi dan Pengaturan Dasar
`Index` adalah kelas inti yang digunakan untuk membuat, membuka, dan mengelola indeks pencarian.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Mengindeks teks dengan kompresi khusus

### Langkah 1: definisikan folder indeks
Pilih direktori tempat file indeks akan disimpan:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Langkah 2: konfigurasikan pengaturan indeks
`TextStorageSettings` mengonfigurasi cara teks disimpan dalam indeks, termasuk tingkat kompresi. `Compression` adalah enum yang menentukan algoritma kompresi yang diinginkan.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Langkah 3: buat indeks dengan pengaturan khusus
Instansiasi indeks menggunakan konfigurasi yang didefinisikan di atas:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Cara menambahkan folder ke indeks

`Index` adalah kelas utama yang mewakili indeks yang dapat dicari.

Muat indeks yang ada (atau buat yang baru) lalu panggil metode `add` pada objek `Index`. Operasi `add` memindai direktori yang diberikan, mengekstrak teks dari setiap file yang didukung, dan menyimpannya dalam indeks terkompresi, siap untuk pencarian instan.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## Cara mencari dokumen yang diindeks

`SearchResult` mewakili satu kecocokan dengan jalur dokumen dan relevansi.

Definisikan string kueri pencarian yang mewakili istilah atau frasa yang ingin Anda temukan, lalu panggil metode `search` pada instance `Index`. Metode ini mengembalikan koleksi objek `SearchResult`, masing-masing berisi jalur dokumen, skor relevansi, dan potongan teks yang menyoroti kecocokan.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Aplikasi Praktis

Skenario dunia nyata di mana **java full text search** bersinar:

1. **Manajemen dokumen hukum** – pengambilan berkas kasus secara instan.  
2. **Perpustakaan riset akademik** – pencarian cepat makalah dan tesis.  
3. **Basis pengetahuan perusahaan** – akses cepat ke manual dan FAQ.  
4. **Sistem manajemen konten** – penemuan konten yang efisien untuk situs besar.  
5. **Arsip layanan pelanggan** – pencarian cepat tiket dan percakapan sebelumnya.  

## Pertimbangan Kinerja

- **Kompresi vs. kecepatan**: Kompresi tinggi menghemat hingga 70 % ruang disk tetapi menambah overhead pengindeksan yang sedang; jalankan tes benchmark untuk volume data Anda.  
- **Manajemen memori**: Alokasikan setidaknya 2 GB heap untuk indeks yang lebih besar dari 10 GB guna menghindari `OutOfMemoryError`.  
- **Pembaruan indeks**: Tambahkan dokumen baru secara inkremental dengan `index.add()` dan secara berkala panggil `index.optimize()` untuk menjaga indeks tetap kompak.  
- **Optimasi kueri**: Gunakan sintaks kueri lanjutan (wildcard, proximity, fuzzy search) untuk mempersempit hasil dan mengurangi waktu respons.  

## Kesalahan Umum & Tips Pro

- **Kesalahan:** Lupa memanggil `index.optimize()` setelah penambahan massal.  
  **Tips pro:** Jalankan `index.optimize()` setiap malam untuk menjaga indeks tetap kompak.  

- **Kesalahan:** Menggunakan kompresi default (rendah) pada dataset besar.  
  **Tips pro:** Beralih ke `Compression.High` untuk lingkungan produksi guna mengurangi biaya penyimpanan.  

- **Kesalahan:** Tidak menangani `IOException` saat menambahkan file dari jaringan bersama.  
  **Tips pro:** Bungkus `index.add()` dalam blok try‑catch dan log setiap kegagalan untuk ditinjau nanti.  

## Pertanyaan yang Sering Diajukan

**Q: Apa itu GroupDocs.Search?**  
A: Ini adalah perpustakaan Java yang kuat yang menyediakan kemampuan pencarian teks penuh lanjutan, termasuk pengindeksan, kompresi, dan dukungan kueri kompleks.

**Q: Bagaimana cara menangani dataset besar dengan GroupDocs.Search?**  
A: Aktifkan kompresi tinggi (`Compression.High`) dan secara berkala commit perubahan untuk menjaga indeks tetap ramping. Juga, alokasikan memori heap yang cukup (mis., 4 GB untuk indeks di atas 20 GB).

**Q: Bisakah saya mengintegrasikan GroupDocs.Search dengan sistem perusahaan yang ada?**  
A: Ya, perpustakaan ini dapat disematkan dalam backend berbasis Java apa pun, layanan REST, atau arsitektur mikro‑service.

**Q: Bagaimana jika indeks saya menjadi usang?**  
A: Gunakan metode `index.add()` untuk menambahkan file baru dan `index.delete()` untuk menghapus yang usang, lalu jalankan kembali `index.optimize()` jika diperlukan.

**Q: Di mana saya dapat mendapatkan bantuan atau dukungan?**  
A: Kunjungi forum komunitas di [GroupDocs forums](https://forum.groupdocs.com/c/search/10) untuk pemecahan masalah dan tips praktik terbaik.

## Sumber Daya Tambahan

- Panduan penggunaan detail: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Referensi API lengkap: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Tetap up‑to‑date dengan fitur baru: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Terakhir Diperbarui:** 2026-11-02  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Tutorial Terkait

- [Panduan Membuat Indeks Groupdocs Search Java](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Panduan Manajemen Indeks Groupdocs Search Java](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Perpustakaan Java Full Text Search – Optimalkan Indeks dengan GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)