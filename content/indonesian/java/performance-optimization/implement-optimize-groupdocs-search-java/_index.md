---
date: '2026-07-07'
description: Pelajari cara menghapus index, melakukan full text search Java, dan mengoptimalkan
  search performance menggunakan GroupDocs.Search untuk Java. Panduan langkah demi
  langkah dengan network setup dan indexing.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Cara menghapus index dan melakukan full text search Java menggunakan
  GroupDocs.Search. Ikuti panduan ini untuk menyiapkan search network, membuat searchable
  index, dan mengoptimalkan search performance.
og_title: Cara Menghapus Index dan Melakukan Text Search dengan GroupDocs.Search untuk
  Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Cara Menghapus Index dan Melakukan Text Search dengan GroupDocs.Search untuk
  Java
type: docs
url: /id/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Cara Menghapus Indeks dan Melakukan Pencarian Teks dengan GroupDocs.Search untuk Java

Di dunia yang didorong oleh data saat ini, **how to delete index** dengan cepat sambil tetap memberikan kemampuan pencarian teks penuh Java yang sangat cepat merupakan keunggulan kompetitif. Baik Anda membangun basis pengetahuan internal, repositori kasus hukum, atau katalog produk e‑commerce, jaringan pencarian yang teroptimasi dapat secara dramatis meningkatkan kepuasan pengguna. Dalam panduan ini Anda akan belajar cara **set up a search network**, **create a searchable index**, **optimize search performance**, dan **delete documents from the index** bila diperlukan—semua menggunakan GroupDocs.Search untuk Java.

## Jawaban Cepat
- **Apa tujuan utama GroupDocs.Search untuk Java?** Ia menyediakan pencarian teks penuh pada lebih dari 50 format dokumen, memungkinkan pengambilan kata kunci yang cepat.  
- **Bagaimana cara melakukan pencarian teks di lingkungan terdistribusi?** Sebarkan jaringan pencarian, indeks dokumen pada node master, kemudian query pada node manapun.  
- **Apakah saya dapat menghapus dokumen dari indeks tanpa membangun ulang?** Ya, gunakan Delete API untuk menghapus file yang dipilih, secara efektif *how to delete index* tanpa melakukan re‑indexing penuh.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi.  
- **Apakah lisensi diperlukan untuk produksi?** Lisensi GroupDocs.Search yang valid diperlukan; versi percobaan gratis tersedia.

## Apa itu “perform text search”?
Melakukan pencarian teks berarti melakukan query pada indeks teks penuh untuk mengambil dokumen yang berisi kata kunci atau frasa yang ditentukan. GroupDocs.Search membangun indeks terbalik yang membuat pencarian ini sangat cepat, bahkan pada ribuan file.

## Mengapa menyiapkan jaringan pencarian?
Jaringan pencarian mendistribusikan beban kerja pengindeksan dan query ke beberapa node, memungkinkan Anda **optimize search performance**, melakukan skala secara horizontal, dan mempertahankan ketersediaan tinggi. Arsitektur ini ideal untuk repositori dokumen tingkat perusahaan di mana latensi dan throughput penting.

## Cara Mengimplementasikan dan Mengoptimalkan Jaringan Pencarian dengan GroupDocs.Search untuk Java
Muat konfigurasi Anda, mulai node master, kemudian tambahkan node pekerja yang berbagi jalur dasar dan port yang sama. Menyebarkan jaringan dengan cara ini memungkinkan setiap node menangani permintaan pengindeksan atau query, memberikan waktu respons yang konsisten bahkan ketika jumlah dokumen meningkat menjadi ratusan ribu.

### Ikhtisar langkah‑demi‑langkah
1. **Define a base configuration** yang mencakup direktori bersama dan port TCP.  
2. **Start the master node** untuk mengelola indeks dan mengoordinasikan node pekerja.  
3. **Add worker nodes** yang terhubung ke master, memungkinkan pengindeksan dan pencarian paralel.  
4. **Monitor resource usage** dan sesuaikan pengaturan heap JVM untuk menjaga latensi tetap rendah.

## Cara Menghapus Indeks di GroupDocs.Search untuk Java
`SearchNode` mewakili sebuah node dalam jaringan GroupDocs.Search yang mengelola operasi pengindeksan dan query. Metode `delete` menghapus dokumen yang ditentukan dari indeks.

### Langkah penghapusan langsung
- Panggil metode `delete` pada instance `SearchNode`.  
- Berikan array jalur file relatif.  
- Commit perubahan; indeks langsung diperbarui dan pencarian selanjutnya tidak lagi mengembalikan file yang dihapus.

## Apa itu Jaringan Pencarian?
Sebuah **search network** adalah kumpulan node yang saling terhubung dan berbagi repositori indeks bersama, memungkinkan pengindeksan terdistribusi dan eksekusi query. Ini memungkinkan skala horizontal dan toleransi kesalahan untuk koleksi dokumen berskala besar.

## Cara Membuat Indeks yang Dapat Dicari (index documents java)
Metode `add` mengindeks sebuah dokumen ke dalam indeks pencarian. Tambahkan dokumen ke node master menggunakan metode `add`; jaringan menyebarkan perubahan ke semua node pekerja. Pendekatan ini memastikan setiap node dapat melayani query terhadap indeks terbaru tanpa langkah sinkronisasi tambahan.

### Tindakan utama
- Arahkan node master ke folder yang berisi file sumber.  
- Jalankan rutin pengindeksan; jaringan memproses setiap file dan memperbarui indeks terbalik.  
- Verifikasi bahwa file indeks muncul di direktori penyimpanan yang ditentukan.

## Cara Menghapus File yang Diindeks (remove indexed files)
Ketika sebuah dokumen menjadi usang, panggil API `delete` dengan jalurnya. Sistem menghapus entri file tersebut dari indeks terbalik, membebaskan ruang penyimpanan dan mencegah hasil usang.

## Menyiapkan GroupDocs.Search untuk Java
Untuk memulai, integrasikan GroupDocs.Search ke dalam proyek Java Anda menggunakan pengaturan berikut:

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
Sebagai alternatif, Anda dapat [unduh versi terbaru langsung dari GroupDocs](https://releases.groupdocs.com/search/java/).

### Perolehan Lisensi
GroupDocs menawarkan percobaan gratis, yang memungkinkan Anda mengevaluasi fiturnya sebelum membeli. Anda dapat memperoleh lisensi sementara dengan mengikuti langkah‑langkah pada [halaman pembelian](https://purchase.groupdocs.com/temporary-license/). Ini akan mengaktifkan fungsionalitas penuh selama fase pengujian Anda.

### Inisialisasi dan Pengaturan Dasar
Inisialisasi GroupDocs.Search dalam aplikasi Java Anda dengan:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Panduan Implementasi

### Mengonfigurasi Jaringan Pencarian
**Overview:** Tetapkan jalur dasar dan port untuk jaringan pencarian Anda, memungkinkan node berkomunikasi secara efektif.

#### Langkah 1: Tentukan Konfigurasi Dasar
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameter:**  
  - `basePath`: Jalur direktori untuk operasi jaringan.  
  - `basePort`: Nomor port yang digunakan oleh jaringan pencarian.

#### Langkah 2: Pemecahan Masalah
Pastikan port yang Anda tentukan tidak diblokir oleh pengaturan firewall atau sedang digunakan oleh aplikasi lain. Sesuaikan bila perlu untuk menghindari konflik.

### Menyebarkan Node Jaringan Pencarian
**Overview:** Menggunakan konfigurasi Anda, sebarkan node di seluruh jaringan untuk pengindeksan dan pencarian terdistribusi.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Opsi Konfigurasi Utama:**  
  - **Base Path & Port:** Nilai-nilai ini harus cocok dengan yang digunakan dalam konfigurasi awal Anda untuk memastikan konsistensi.

### Mengindeks Dokumen (`create searchable index`)
**Overview:** Tambahkan dokumen ke indeks pencarian secara efisien menggunakan node master.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Tujuan:**  
  - `masterNode`: Node utama yang mengelola pengindeksan dokumen.  
  - `documentsPath`: Jalur ke direktori yang berisi dokumen.

#### Tips Pemecahan Masalah
Verifikasi bahwa jalur dokumen Anda benar dan dapat diakses. Pastikan izin memungkinkan pembacaan dari direktori tersebut.

### Mencari Teks dalam Jaringan (`perform text search`)
**Overview:** Lakukan pencarian teks komprehensif di seluruh jaringan yang diindeks.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameter:**  
  - `query`: Teks yang Anda cari.  
  - `masterNode`: Node yang melakukan pencarian.

### Menghapus Dokumen dari Indeks (`delete documents index`)
**Overview:** Hapus dokumen tertentu dari indeks Anda menggunakan jalur file mereka.

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

- **Tujuan Metode:**  
  - `node`: Node target untuk operasi penghapusan.  
  - `filePaths`: Jalur dokumen yang akan dihapus dari indeks.

#### Pemecahan Masalah
Pastikan jalur file tepat dan file ada di direktori Anda. Jika masalah berlanjut, periksa izin jaringan dan konektivitas.

## Aplikasi Praktis
1. **Enterprise Document Management:** Mempercepat pengambilan pengetahuan internal.  
2. **Legal Case Analysis:** Dengan cepat menemukan file kasus yang relevan di berbagai repositori.  
3. **E‑commerce Platforms:** Meningkatkan kecepatan pencarian produk dengan mengindeks deskripsi dan ulasan.  
4. **Academic Research:** Secara efisien mencari perpustakaan digital besar berisi makalah dan tesis.  
5. **Customer Support Systems:** Mengurangi waktu respons dengan memungkinkan agen mencari tiket sebelumnya secara instan.

## Pertimbangan Kinerja
- **Optimize Indexing Speed:** Tambahkan dokumen baru secara bertahap selama jam off‑peak untuk menjaga latensi rendah.  
- **Resource Usage Guidelines:** Pantau CPU dan memori, terutama saat meningkatkan jumlah node.  
- **Java Memory Management:** Sesuaikan pengaturan heap JVM berdasarkan beban kerja Anda (mis., `-Xmx2g` untuk indeks berukuran menengah).

## Kesimpulan
Dengan mengikuti panduan ini Anda telah belajar cara **set up a search network**, **create a searchable index**, **perform text search**, dan **delete documents index** menggunakan GroupDocs.Search untuk Java. Kemampuan ini memungkinkan pengambilan dokumen yang cepat dan handal di lingkungan terdistribusi.

**Next Steps** - Bereksperimen dengan konfigurasi node yang berbeda untuk menemukan keseimbangan optimal bagi beban kerja Anda.  - Selami lebih dalam opsi pengindeksan lanjutan seperti analis khusus dan penyesuaian relevansi.  - Jelajahi integrasi dengan produk GroupDocs lainnya untuk pemrosesan dokumen end‑to‑end.

## Pertanyaan yang Sering Diajukan

**Q: Apa kasus penggunaan utama untuk GroupDocs.Search untuk Java?**  
A: Ia menyediakan pencarian teks penuh pada banyak format dokumen, memungkinkan Anda **perform text search** dalam repositori besar.

**Q: Bagaimana saya dapat meningkatkan kecepatan pencarian di jaringan besar?**  
A: Sebarkan node tambahan, sesuaikan heap JVM, dan jadwalkan pengindeksan selama periode lalu lintas rendah untuk **optimize search performance**.

**Q: Apakah memungkinkan menghapus satu dokumen tanpa melakukan re‑index seluruh koleksi?**  
A: Ya, gunakan API **delete documents index** seperti yang ditunjukkan dalam contoh kode untuk menghapus file tertentu.

**Q: Apakah saya memerlukan lisensi untuk pengembangan?**  
A: Lisensi percobaan gratis cukup untuk pengujian; lisensi komersial diperlukan untuk penerapan produksi.

**Q: Bisakah saya mengindeks PDF, file Word, dan email secara bersamaan?**  
A: Tentu—GroupDocs.Search mendukung berbagai format secara langsung.

---

**Terakhir Diperbarui:** 2026-07-07  
**Diuji Dengan:** GroupDocs.Search for Java 25.4  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara Mengindeks Teks di Java dengan Panduan GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Optimalkan Kinerja Pencarian dengan Teknik Pengindeksan Lanjutan di GroupDocs.Search untuk Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Tingkatkan Kinerja Query dengan GroupDocs.Search Java: Optimalkan Indeks & Pencarian](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)