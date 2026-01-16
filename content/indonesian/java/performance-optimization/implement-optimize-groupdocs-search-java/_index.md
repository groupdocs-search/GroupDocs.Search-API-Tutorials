---
date: '2026-01-16'
description: Pelajari cara melakukan pencarian teks dan mengoptimalkan kinerja pencarian
  menggunakan GroupDocs.Search untuk Java. Termasuk langkah-langkah untuk menyiapkan
  jaringan pencarian, membuat indeks yang dapat dicari, dan menghapus indeks dokumen.
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: Lakukan Pencarian Teks dengan GroupDocs.Search untuk Java
type: docs
url: /id/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Lakukan Pencarian Teks dengan GroupDocs.Search untuk Java
## Optimisasi Kinerja

## Cara Mengimplementasikan dan Mengoptimalkan Jaringan Pencarian dengan GroupDocs.Search untuk Java

### Pendahuluan
Di dunia yang didorong oleh data saat ini, kemampuan untuk **perform text search** dengan cepat di seluruh koleksi dokumen yang masif merupakan keunggulan kompetitif. Baik Anda membangun basis pengetahuan internal, repositori kasus hukum, atau katalog produk e‑commerce, jaringan pencarian yang teroptimasi dengan baik dapat secara dramatis meningkatkan kepuasan pengguna. Dalam panduan ini Anda akan belajar cara **set up search network**, **create searchable index**, **optimize search performance**, dan bahkan **delete documents index** bila diperlukan—semua menggunakan GroupDocs.Search untuk Java.

**Apa yang Akan Anda Pelajari**
- Mengonfigurasi jaringan pencarian dengan GroupDocs.Search  
- Menyebarkan node dalam jaringan  
- Mengindeks dokumen secara efisien (`index documents java`)  
- Melakukan pencarian teks di seluruh jaringan Anda (`perform text search`)  
- Menghapus dokumen spesifik dari indeks (`delete documents index`)  

Mari kita selami bagaimana Anda dapat memanfaatkan fitur-fitur ini untuk menciptakan pengalaman pencarian yang dioptimalkan.

## Jawaban Cepat
- **Apa tujuan utama GroupDocs.Search untuk Java?** It provides full‑text search across many document formats.  
- **How do I perform text search in a distributed environment?** Deploy a search network, index documents on a master node, then query any node.  
- **Can I delete documents from the index without rebuilding it?** Yes, use the Delete API to remove selected files.  
- **What Java version is required?** JDK 8 or higher.  
- **Is a license needed for production?** A valid GroupDocs.Search license is required; a free trial is available.

## Apa itu “perform text search”?
Melakukan pencarian teks berarti melakukan query pada indeks full‑text untuk mengambil dokumen yang berisi kata kunci atau frasa yang ditentukan. GroupDocs.Search membangun indeks terbalik yang membuat pencarian ini sangat cepat, bahkan pada ribuan file.

## Mengapa menyiapkan jaringan pencarian?
Jaringan pencarian mendistribusikan beban kerja pengindeksan dan query ke beberapa node, memungkinkan Anda **optimize search performance**, memperluas secara horizontal, dan mempertahankan ketersediaan tinggi. Arsitektur ini ideal untuk repositori dokumen tingkat perusahaan di mana latensi dan throughput penting.

### Prasyarat
- **Perpustakaan yang Diperlukan:** GroupDocs.Search untuk Java versi 25.4 (terbaru).  
- **Lingkungan:** Java JDK 8+, Maven.  
- **Pengetahuan:** Pemrograman Java dasar dan pemahaman konsep jaringan.

### Menyiapkan GroupDocs.Search untuk Java
Untuk memulai, integrasikan GroupDocs.Search ke dalam proyek Java Anda menggunakan pengaturan berikut:

#### Pengaturan Maven
Add the repository and dependency to your `pom.xml` file:

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

#### Unduhan Langsung
Sebagai alternatif, Anda dapat [mengunduh versi terbaru langsung dari GroupDocs](https://releases.groupdocs.com/search/java/).

#### Perolehan Lisensi
GroupDocs menawarkan trial gratis, yang memungkinkan Anda mengevaluasi fiturnya sebelum membeli. Anda dapat memperoleh lisensi sementara dengan mengikuti langkah‑langkah di [halaman pembelian](https://purchase.groupdocs.com/temporary-license/). Ini akan mengaktifkan fungsionalitas penuh selama fase pengujian Anda.

#### Inisialisasi dan Pengaturan Dasar
Initialize GroupDocs.Search in your Java application with:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

### Panduan Implementasi

#### Mengonfigurasi Jaringan Pencarian
**Gambaran Umum:** Tetapkan jalur dasar dan port untuk jaringan pencarian Anda, memungkinkan node berkomunikasi secara efektif.

##### Langkah 1: Tentukan Konfigurasi Dasar

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameters:**  
  - `basePath`: Jalur direktori untuk operasi jaringan.  
  - `basePort`: Nomor port yang digunakan oleh jaringan pencarian.

##### Langkah 2: Pemecahan Masalah
Pastikan port yang Anda tentukan tidak diblokir oleh pengaturan firewall atau sedang digunakan oleh aplikasi lain. Sesuaikan bila perlu untuk menghindari konflik.

#### Menyebarkan Node Jaringan Pencarian
**Gambaran Umum:** Using your configuration, deploy nodes across your network for distributed indexing and searching.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Key Configuration Options:**  
  - **Base Path & Port:** Nilai-nilai ini harus cocok dengan yang digunakan dalam konfigurasi awal Anda untuk memastikan konsistensi.

#### Mengindeks Dokumen (`create searchable index`)
**Gambaran Umum:** Add documents to the search index efficiently using a master node.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Purpose:**  
  - `masterNode`: Node utama yang mengelola pengindeksan dokumen.  
  - `documentsPath`: Jalur ke direktori yang berisi dokumen.

##### Tips Pemecahan Masalah
Verifikasi bahwa jalur dokumen Anda benar dan dapat diakses. Pastikan izin memungkinkan pembacaan dari direktori tersebut.

#### Mencari Teks di Jaringan (`perform text search`)
**Gambaran Umum:** Perform comprehensive text searches across your indexed network.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameters:**  
  - `query`: Teks yang Anda cari.  
  - `masterNode`: Node yang melakukan pencarian.

#### Menghapus Dokumen dari Indeks (`delete documents index`)
**Gambaran Umum:** Remove specific documents from your index using their file paths.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Method Purpose:**  
  - `node`: Node target untuk operasi penghapusan.  
  - `filePaths`: Jalur dokumen yang akan dihapus dari indeks.

##### Pemecahan Masalah
Pastikan jalur file tepat dan file ada di direktori Anda. Jika masalah berlanjut, periksa izin jaringan dan konektivitas.

### Aplikasi Praktis
1. **Manajemen Dokumen Perusahaan:** Mempercepat pengambilan pengetahuan internal.  
2. **Analisis Kasus Hukum:** Dengan cepat menemukan file kasus yang relevan di berbagai repositori.  
3. **Platform E‑commerce:** Meningkatkan kecepatan pencarian produk dengan mengindeks deskripsi dan ulasan.  
4. **Penelitian Akademik:** Mencari secara efisien perpustakaan digital besar berisi makalah dan tesis.  
5. **Sistem Dukungan Pelanggan:** Mengurangi waktu respons dengan memungkinkan agen mencari tiket sebelumnya secara instan.  

### Pertimbangan Kinerja
- **Optimalkan Kecepatan Pengindeksan:** Tambahkan dokumen baru secara bertahap selama jam tidak sibuk untuk menjaga latensi rendah.  
- **Panduan Penggunaan Sumber Daya:** Pantau CPU dan memori, terutama saat menambah jumlah node.  
- **Manajemen Memori Java:** Sesuaikan pengaturan heap JVM berdasarkan beban kerja Anda (mis., `-Xmx2g` untuk indeks berukuran sedang).

### Kesimpulan
Dengan mengikuti panduan ini Anda telah belajar cara **set up search network**, **create searchable index**, **perform text search**, dan **delete documents index** menggunakan GroupDocs.Search untuk Java. Kemampuan ini memungkinkan pengambilan dokumen yang cepat dan andal di lingkungan terdistribusi.

**Langkah Selanjutnya**
- Bereksperimen dengan konfigurasi node yang berbeda untuk menemukan keseimbangan optimal bagi beban kerja Anda.  
- Menyelami lebih dalam opsi pengindeksan lanjutan seperti analyzer khusus dan penyesuaian relevansi.  
- Jelajahi integrasi dengan produk GroupDocs lainnya untuk pemrosesan dokumen end‑to‑end.

## Pertanyaan yang Sering Diajukan

**Q: Apa kasus penggunaan utama untuk GroupDocs.Search untuk Java?**  
A: It provides full‑text search across many document formats, allowing you to **perform text search** in large repositories.

**Q: Bagaimana saya dapat meningkatkan kecepatan pencarian di jaringan besar?**  
A: Deploy additional nodes, tune the JVM heap, and schedule indexing during low‑traffic periods to **optimize search performance**.

**Q: Apakah memungkinkan menghapus satu dokumen tanpa mengindeks ulang seluruh koleksi?**  
A: Yes, use the **delete documents index** API as shown in the code example to remove specific files.

**Q: Apakah saya memerlukan lisensi untuk pengembangan?**  
A: A free trial license is sufficient for testing; a commercial license is required for production deployments.

**Q: Apakah saya dapat mengindeks PDF, file Word, dan email secara bersamaan?**  
A: Absolutely—GroupDocs.Search supports a wide range of formats out of the box.

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs