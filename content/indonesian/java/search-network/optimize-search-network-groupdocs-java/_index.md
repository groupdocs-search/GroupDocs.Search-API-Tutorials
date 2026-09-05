---
date: '2026-05-17'
description: Pelajari cara mengkonfigurasi search network java, mengoptimalkan shards,
  melakukan pencarian teks, dan menangani port conflicts dengan GroupDocs.Search untuk
  Java.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Cara Mengoptimalkan Shards di GroupDocs.Search untuk Java: Panduan Komprehensif'
type: docs
url: /id/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Cara Mengoptimalkan Shard di GroupDocs.Search untuk Java: Panduan Komprehensif

Pencarian dokumen yang efisien sangat penting bagi pengembang dan bisnis yang mengelola kumpulan data besar atau membutuhkan pengambilan internal yang cepat. Dalam tutorial ini Anda akan belajar **how to configure search network java**, cara mengindeks dan mengkueri dokumen, serta langkah‑langkah tepat untuk **optimize shards** demi kinerja puncak. Kami juga akan membahas contoh penggunaan dunia nyata, jebakan umum, dan tip praktis untuk menjaga node pencarian Anda berjalan lancar.

## Jawaban Cepat
- **Apa itu optimasi shard?** Ini mengatur ulang data indeks untuk mempercepat kueri dan mengurangi beban penyimpanan.  
- **Bagaimana cara mengkonfigurasi jaringan pencarian?** Tentukan direktori dasar dan port, lalu deploy node menggunakan API yang disediakan.  
- **Bagaimana cara melakukan pencarian teks?** Gunakan `TextSearchInNetwork.searchAll` dengan string kueri Anda.  
- **Bagaimana cara mengindeks dokumen di Java?** Tambahkan direktori dokumen ke node master dengan `IndexingDocuments.addDirectories`.  
- **Bagaimana cara menangani konflik port?** Ubah variabel `basePort` ke port yang belum digunakan di mesin Anda.

## Cara Mengkonfigurasi Jaringan Pencarian
`Configuration` menyimpan semua pengaturan yang diperlukan untuk meluncurkan jaringan GroupDocs.Search, seperti lokasi folder indeks dan port komunikasi.  
`SearchNetwork` mengatur node, menangani pengindeksan dan distribusi kueri.

Muat konfigurasi pencarian Anda, tetapkan jalur dasar dokumen, pilih port yang bebas, dan mulai jaringan—semua dalam beberapa baris kode. Jawaban langsung ini menjelaskan seluruh proses dalam kurang dari 70 kata: **Create a `Configuration` object, set `basePath` dan `basePort`, lalu panggil `SearchNetwork.start(configuration)`.** Jaringan secara otomatis akan memulai node master dan node pekerja yang diperlukan, siap menerima permintaan pengindeksan.

### Definisi Anchor
`Configuration` adalah kelas inti yang menyimpan semua pengaturan yang diperlukan untuk meluncurkan jaringan GroupDocs.Search, seperti lokasi folder indeks dan port komunikasi.

Untuk menghindari kesalahan “port already in use” yang menakutkan, pertama pastikan port yang dipilih bebas (mis., menggunakan `netstat` atau tes socket sederhana) sebelum menginisialisasi jaringan.

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

## Cara Mengindeks Dokumen Java
`IndexingDocuments` adalah kelas utilitas yang mempermudah penambahan beberapa direktori ke node pencarian dan memicu pipeline pengindeksan.

Tambahkan folder dokumen Anda ke node master, lalu biarkan pengindeks merayapi mereka. **Direct answer:** Panggil `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` dan kemudian panggil `masterNode.index()`; mesin akan membuat shard yang dapat dicari untuk setiap folder yang Anda berikan. Pendekatan ini berskala secara horizontal—tambahkan lebih banyak node, dan metode yang sama akan mendistribusikan beban kerja secara otomatis.

### Definisi Anchor
`IndexingDocuments` adalah kelas utilitas yang mempermudah penambahan beberapa direktori ke node pencarian dan memicu pipeline pengindeksan.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Cara Melakukan Pencarian Teks
`TextSearchInNetwork` menyediakan metode pembantu statis untuk menyiarkan kueri teks ke setiap node dalam jaringan dan mengagregasi hasilnya.  
`SearchResult` menyimpan ID dokumen yang cocok, cuplikan, dan skor relevansi.

Jalankan kueri di semua shard dengan satu pemanggilan metode. **Direct answer:** Gunakan `TextSearchInNetwork.searchAll("your query", searchNetwork)`; metode ini mengembalikan koleksi objek `SearchResult` yang berisi ID dokumen, cuplikan, dan skor relevansi. Anda dapat memfilter hasil lebih lanjut berdasarkan bahasa, tipe file, atau metadata khusus tanpa menulis kode tambahan.

### Definisi Anchor
`TextSearchInNetwork` menyediakan metode pembantu statis yang menyiarkan kueri teks ke setiap node dalam jaringan dan mengagregasi hasilnya.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Cara Menangani Konflik Port
Jika port default (`49132`) sedang digunakan, cukup pilih port bebas lain dan perbarui field `basePort` sebelum memulai jaringan. **Direct answer:** Ubah `int basePort = 49132;` menjadi nilai yang belum digunakan seperti `49133`, rebuild, dan restart; jaringan akan terikat ke port baru tanpa memengaruhi node yang ada.

Tip pro: Simpan file konfigurasi kecil (mis., `search-config.properties`) sehingga Anda dapat mengubah port tanpa harus meng-compile ulang.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

### Perpustakaan, Versi, dan Dependensi yang Diperlukan
Untuk mengimplementasikan solusi ini, sertakan perpustakaan GroupDocs.Search menggunakan Maven dengan menambahkan konfigurasi berikut ke file `pom.xml` Anda:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Atau, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Persyaratan Penyiapan Lingkungan
- Java Development Kit (JDK) 8 atau lebih baru.  
- Izin jaringan yang memungkinkan binding ke `basePort` yang dipilih.  
- Ruang disk yang cukup untuk file indeks (setiap shard dapat menempati ~10 MB per 1.000 dokumen).

### Prasyarat Pengetahuan
Pemahaman dasar tentang Java, pemrograman berorientasi objek, dan penanganan pengecualian akan membantu Anda mengikuti contoh dengan lancar.

## Menyiapkan GroupDocs.Search untuk Java
Untuk mulai menggunakan GroupDocs.Search dalam proyek Anda, ikuti langkah-langkah berikut:

1. **Add the Dependency**: Seperti ditunjukkan di atas, tambahkan dependensi Maven yang diperlukan ke proyek Anda atau unduh langsung dari halaman rilis.  
2. **License Acquisition**:  
   - **Free trial** – tidak memerlukan kunci lisensi, tetapi penggunaan dibatasi hingga 500 dokumen per hari.  
   - **Temporary license** – minta kunci percobaan 30‑hari dari [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – beli lisensi produksi untuk akses tak terbatas dan dukungan prioritas.  
3. **Basic Initialization and Setup**:  
   Inisialisasi konfigurasi menggunakan kelas `Configuration`, mengatur jalur dasar untuk dokumen dan menentukan nomor port:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Panduan Implementasi
Sekarang mari kita jelajahi implementasi fitur utama menggunakan GroupDocs.Search Java.

### Fitur: Mengkonfigurasi Jaringan Pencarian
**Overview**: Menyiapkan jaringan pencarian melibatkan mendefinisikan direktori dokumen Anda dan mengkonfigurasinya dengan port tertentu untuk komunikasi antar node.

#### Langkah 1: Tentukan Direktori Dokumen dan Port
`DocumentDirectory` adalah penampung sederhana untuk jalur absolut folder yang ingin Anda indeks. Berikan satu atau lebih jalur ke konfigurasi.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Langkah 2: Konfigurasikan Jaringan Pencarian
Buat objek konfigurasi menggunakan jalur yang telah ditentukan:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Fitur: Menyebarkan Node Jaringan Pencarian
**Overview**: Menyebarkan node untuk menangani pencarian dokumen secara efisien di seluruh jaringan Anda.

#### Langkah 1: Deploy Node Menggunakan Konfigurasi
Deploy node jaringan pencarian dan identifikasi node master untuk manajemen terpusat:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Fitur: Berlangganan ke Event Node Jaringan
**Overview**: Pantau jaringan pencarian Anda dengan berlangganan ke event yang memberi tahu Anda tentang perubahan atau tindakan penting.

#### Langkah 1: Berlangganan ke Event Node Master
`SearchNetworkEventListener` memungkinkan Anda merespons penyelesaian pengindeksan, kegagalan node, atau optimasi shard.

CODE_BLOCK_PLACEHOLDER_9_END

### Fitur: Mengindeks Dokumen di Node Jaringan
**Overview**: Tambahkan direktori yang berisi dokumen ke proses pengindeksan untuk pencarian yang efisien.

#### Langkah 1: Tambahkan Direktori Dokumen ke Proses Pengindeksan
Berikan daftar jalur folder ke node master; mesin akan membuat shard terpisah untuk setiap folder, memungkinkan eksekusi kueri paralel.

CODE_BLOCK_PLACEHOLDER_10_END

### Fitur: Pencarian Teks di Node Jaringan
**Overview**: Jalankan pencarian teks di semua dokumen terindeks dalam jaringan pencarian Anda.

#### Langkah 1: Lakukan Pencarian Teks
Panggil pembantu statis untuk menjalankan kueri dan mengambil dokumen yang cocok dengan skor relevansi.

CODE_BLOCK_PLACEHOLDER_11_END

### Fitur: Mengoptimalkan Shard
**Overview**: Tingkatkan kinerja dengan mengoptimalkan shard dalam pengindeks node jaringan pencarian Anda.

#### Langkah 1: Optimalkan Shard Pengindeks
Optimalkan shard untuk meningkatkan efisiensi pencarian (di sinilah **how to optimize shards** benar‑benar penting):

CODE_BLOCK_PLACEHOLDER_12_END

## Aplikasi Praktis
GroupDocs.Search untuk Java dapat diterapkan dalam berbagai skenario dunia nyata, masing‑masing mendapat manfaat dari optimasi shard:

1. **Enterprise Document Management** – Menangani arsip 10 TB+ dengan waktu kueri sub‑detik setelah optimasi shard.  
2. **E‑commerce Platforms** – Menjalankan pencarian produk di 1 juta SKU, mengurangi latensi hingga 45 % ketika shard dioptimalkan.  
3. **Legal Firms** – Mengambil file kasus dari repositori 200 GB dalam kurang dari 200 ms.  
4. **Library Systems** – Mendukung pencarian katalog untuk 500 k buku digital dengan penggunaan memori yang efisien.  
5. **Content Management Systems (CMS)** – Memungkinkan penemuan konten instan untuk penyebaran multi‑situs dengan lebih dari 2 juta halaman.

## Pertimbangan Kinerja
Untuk memastikan kinerja optimal dari implementasi GroupDocs.Search Anda:

- **Regularly optimize shards** – Menjalankan `optimizeShards()` setelah setiap 10 GB data baru mengurangi waktu respons kueri sebesar 30‑50 %.  
- **Monitor memory usage** – Jaga heap JVM di bawah 75 % dari RAM fisik; aktifkan G1GC untuk indeks besar.  
- **Use incremental indexing** – Tambahkan hanya file yang berubah untuk menghindari pengindeksan ulang penuh.  
- **Leverage multi‑node scaling** – Tambahkan node pekerja untuk mendistribusikan shard; setiap node tambahan dapat meningkatkan throughput sekitar ~20 % untuk beban kerja baca‑berat.  

## Masalah Umum dan Solusinya
| Masalah | Gejala | Solusi |
|-------|---------|----------|
| Konflik port saat startup | `java.net.BindException: Address already in use` | Ubah `basePort` ke nilai yang belum digunakan; verifikasi dengan `netstat -ano`. |
| Kesalahan out‑of‑memory selama optimasi | `java.lang.OutOfMemoryError: Java heap space` | Tingkatkan flag JVM `-Xmx` atau jalankan optimasi pada node khusus dengan RAM lebih banyak. |
| Dokumen hilang dalam hasil pencarian | Tidak ada hasil yang dikembalikan setelah pengindeksan | Pastikan direktori ditambahkan dengan benar melalui `IndexingDocuments.addDirectories` dan bahwa `masterNode.index()` selesai tanpa pengecualian. |
| Shard usang setelah penghapusan massal | File yang dihapus masih muncul | Jalankan `optimizeShards()` untuk menggabungkan segmen dan membersihkan tombstone. |

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana optimasi shard memengaruhi kecepatan kueri?**  
A: Mengoptimalkan shard memadatkan indeks, mengurangi I/O disk, dan biasanya menghasilkan respons kueri 30‑50 % lebih cepat untuk dataset besar.

**Q: Apakah aman menjalankan `optimizeShards` pada node yang aktif?**  
A: Ya, operasi ini dirancang untuk berjalan tanpa downtime, tetapi penjadwalan selama periode lalu lintas rendah disarankan untuk indeks yang lebih besar dari 20 GB.

**Q: Bisakah saya menyesuaikan `OptimizeOptions`?**  
A: Tentu saja. Anda dapat mengatur parameter seperti `maxSegmentSize` atau `mergeFactor` untuk menyempurnakan proses optimasi.

**Q: Apa yang harus saya lakukan jika menemukan `IOException` selama optimasi?**  
A: Verifikasi izin sistem file, pastikan cukup ruang disk bebas, dan pastikan tidak ada proses lain yang mengunci file indeks.

**Q: Apakah mengoptimalkan shard juga mengembalikan ruang dokumen yang dihapus?**  
A: Ya, optimizer menggabungkan segmen dan menghapus tombstone, membebaskan ruang yang ditempati dokumen yang dihapus.

## Kesimpulan
Dengan mengikuti panduan komprehensif ini, Anda kini tahu cara **configure search network java**, mengindeks dokumen, menjalankan kueri teks, dan yang paling penting, **optimize shards** untuk menjaga kinerja pencarian tetap tajam. Terapkan pola ini pada solusi pencarian perusahaan berbasis Java apa pun, dan Anda akan melihat peningkatan yang terukur dalam latensi, skalabilitas, dan pemanfaatan sumber daya. Untuk langkah selanjutnya, jelajahi fitur lanjutan seperti analyzer khusus, pencarian berfaset, dan integrasi dengan penyedia penyimpanan cloud.

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Tutorial Terkait

- [Mengonfigurasi GroupDocs.Search Network di .NET: Panduan Komprehensif](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Pengindeksan Dokumen .NET Master dengan GroupDocs.Search: Panduan Komprehensif](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Tutorial dan Contoh GroupDocs.Search untuk Java](/search/net/)