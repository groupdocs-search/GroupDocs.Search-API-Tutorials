---
date: '2026-01-21'
description: Pelajari cara mengoptimalkan shard menggunakan GroupDocs.Search untuk
  Java serta cara mengkonfigurasi jaringan pencarian, melakukan pencarian teks, dan
  menangani konflik port.
keywords:
- GroupDocs.Search Java
- search network configuration
- document indexing
title: 'Cara Mengoptimalkan Shard di GroupDocs.Search untuk Java: Panduan Komprehensif'
type: docs
url: /id/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Cara Mengoptimalkan Shards di GroupDocs.Search untuk Java: Panduan Komprehensif

Pencarian dokumen yang efisien sangat penting bagi pengembang dan bisnis yang mengelola basis data besar atau yang ingin menyederhanakan proses pengambilan dokumen internal. Jika Anda bertanya-tanya **bagaimana cara mengoptimalkan shards**, panduan ini akan memandu Anda melalui langkah-langkah untuk meningkatkan kinerja, mengonfigurasi jaringan pencarian Anda, dan menangani tantangan umum seperti konflik port. **GroupDocs.Search Java** menawarkan konfigurasi dan optimisasi jaringan pencarian yang mulus, meningkatkan baik kinerja maupun pengalaman pengguna.

## Jawaban Cepat
- **What is shard optimization?** Ini mengatur ulang data indeks untuk mempercepat kueri dan mengurangi beban penyimpanan.  
- **How to configure a search network?** Tentukan direktori dasar dan port, lalu deploy node menggunakan API yang disediakan.  
- **How to perform text search?** Gunakan `TextSearchInNetwork.searchAll` dengan string kueri Anda.  
- **How to index documents in Java?** Tambahkan direktori dokumen ke node master dengan `IndexingDocuments.addDirectories`.  
- **How to handle port conflicts?** Ubah variabel `basePort` ke port yang tidak digunakan pada mesin Anda.

## Cara Mengonfigurasi Jaringan Pencarian
Sebelum menyelami proses pengindeksan dan pencarian, Anda memerlukan fondasi jaringan yang solid. Bagian ini menjelaskan langkah-langkah untuk menyiapkan jaringan, memilih port, dan menghindari masalah konflik port yang umum.

## Cara Mengindeks Dokumen di Java
Setelah jaringan aktif, langkah selanjutnya adalah mengisinya dengan konten. Kami akan menunjukkan cara menambahkan beberapa folder dokumen sehingga mesin dapat membangun indeks yang dapat dicari.

## Cara Melakukan Pencarian Teks
Setelah pengindeksan, Anda ingin mengambil informasi dengan cepat. Bagian ini menunjukkan cara paling sederhana untuk menjalankan kueri teks di semua node.

## Cara Menangani Konflik Port
Jika port default (`49132`) sudah digunakan, cukup ubah nilai `basePort` ke port yang bebas dan restart konfigurasi. Ini mencegah kesalahan saat memulai dan menjaga jaringan Anda tetap stabil.

## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

### Perpustakaan, Versi, dan Dependensi yang Diperlukan
Untuk mengimplementasikan solusi ini, sertakan perpustakaan GroupDocs.Search menggunakan Maven dengan menambahkan konfigurasi berikut ke file `pom.xml` Anda:

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

### Persyaratan Penyiapan Lingkungan
- Pastikan lingkungan pengembangan Anda mendukung Java (JDK 8 atau lebih baru).
- Akses ke konfigurasi jaringan yang memungkinkan penggunaan port.

### Prasyarat Pengetahuan
Pemahaman dasar tentang pemrograman Java, termasuk prinsip berorientasi objek dan penanganan pengecualian, akan sangat membantu untuk tutorial ini.

## Menyiapkan GroupDocs.Search untuk Java
Untuk mulai menggunakan GroupDocs.Search dalam proyek Anda, ikuti langkah-langkah berikut:

1. **Add the Dependency**: Seperti yang ditunjukkan di atas, tambahkan dependensi Maven yang diperlukan ke proyek Anda atau unduh langsung dari halaman rilis.

2. **License Acquisition**:
   - Untuk percobaan gratis, gunakan perpustakaan tanpa pembatasan fitur tetapi dengan beberapa batasan penggunaan.
   - Dapatkan lisensi sementara untuk akses penuh fitur selama evaluasi dengan mengunjungi [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).
   - Beli lisensi penuh jika Anda memutuskan mengintegrasikan GroupDocs.Search ke lingkungan produksi Anda.

3. **Basic Initialization and Setup**: Inisialisasi konfigurasi menggunakan kelas `Configuration`, mengatur jalur dasar untuk dokumen dan menentukan nomor port:

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Panduan Implementasi
Sekarang mari kita jelajahi implementasi fitur utama menggunakan GroupDocs.Search Java.

### Fitur: Mengonfigurasi Jaringan Pencarian
**Overview**: Menyiapkan jaringan pencarian melibatkan penentuan direktori dokumen Anda dan mengkonfigurasinya dengan port tertentu untuk komunikasi antar node.

#### Langkah 1: Tentukan Direktori Dokumen dan Port
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

#### Langkah 2: Konfigurasikan Jaringan Pencarian
Buat objek konfigurasi menggunakan jalur yang telah ditentukan:

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

### Fitur: Menyebarkan Node Jaringan Pencarian
**Overview**: Menyebarkan node untuk menangani pencarian dokumen secara efisien di seluruh jaringan Anda.

#### Langkah 1: Menyebarkan Node Menggunakan Konfigurasi
Sebarkan node jaringan pencarian dan identifikasi node master untuk manajemen terpusat:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```

### Fitur: Berlangganan ke Event Node Jaringan
**Overview**: Pantau jaringan pencarian Anda dengan berlangganan ke event yang memberi tahu Anda tentang perubahan atau tindakan penting.

#### Langkah 1: Berlangganan ke Event Node Master
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

### Fitur: Mengindeks Dokumen di Node Jaringan
**Overview**: Tambahkan direktori yang berisi dokumen ke proses pengindeksan untuk pencarian yang efisien.

#### Langkah 1: Tambahkan Direktori Dokumen ke Proses Pengindeksan
```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

### Fitur: Pencarian Teks di Node Jaringan
**Overview**: Jalankan pencarian teks di semua dokumen yang diindeks dalam jaringan pencarian Anda.

#### Langkah 1: Lakukan Pencarian Teks
```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Fitur: Mengoptimalkan Shards
**Overview**: Tingkatkan kinerja dengan mengoptimalkan shards dalam indeks pada node jaringan pencarian Anda.

#### Langkah 1: Optimalkan Shards pada Indexer
Optimalkan shards untuk meningkatkan efisiensi pencarian (di sinilah **bagaimana cara mengoptimalkan shards** menjadi penting):

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

## Aplikasi Praktis
GroupDocs.Search untuk Java dapat diterapkan dalam berbagai skenario dunia nyata:

1. **Enterprise Document Management**: Memfasilitasi pengambilan dokumen di seluruh basis data perusahaan yang besar.
2. **E‑commerce Platforms**: Meningkatkan kemampuan pencarian produk dengan menggunakan pengindeksan dan fitur kueri yang dioptimalkan.
3. **Legal Firms**: Mengelola dan mengambil file kasus serta dokumen dari arsip yang luas secara efisien.
4. **Library Systems**: Menyederhanakan proses katalog dengan mengintegrasikan sistem perpustakaan digital untuk pencarian cepat.
5. **Content Management Systems (CMS)**: Meningkatkan penemuan konten melalui kemampuan pencarian lanjutan.

## Pertimbangan Kinerja
Untuk memastikan kinerja optimal dari implementasi GroupDocs.Search Anda:
- Secara rutin optimalkan shards untuk mengurangi waktu respons kueri.
- Pantau dan kelola penggunaan memori, terutama di lingkungan yang menangani dataset besar.
- Ikuti praktik terbaik Java untuk pengumpulan sampah (garbage collection) dan manajemen sumber daya guna mempertahankan efisiensi sistem.

## Kesimpulan
Dengan mengikuti panduan komprehensif ini, Anda telah mempelajari cara menyiapkan dan mengoptimalkan jaringan pencarian menggunakan GroupDocs.Search untuk Java. Dengan keterampilan ini, Anda kini siap menangani pencarian dokumen yang efisien di berbagai aplikasi, meningkatkan kinerja proyek dan pengalaman pengguna. Untuk lebih mengeksplorasi kemampuan GroupDocs.Search, pertimbangkan mengintegrasikannya dengan sistem lain atau menjelajahi fitur tambahan yang tersedia dalam dokumentasi mereka.

## Bagian FAQ
- **What is shard optimization?**
  - Optimasi shard meningkatkan kinerja jaringan pencarian dengan mengatur data lebih efisien di setiap shard.
- **How do I handle port conflicts when configuring a search network?**
  - Ubah variabel basePort ke port yang tidak digunakan pada sistem Anda dan restart proses konfigurasi.
- **Can GroupDocs.Search be integrated with existing Java applications?**
  - Ya, dapat diintegrasikan secara mulus dengan menyertakan dependensi perpustakaan dalam proyek Anda.
- **What are some common issues faced during setup?**
  - Masalah umum meliputi konfigurasi port yang salah dan dependensi yang hilang; pastikan Anda mengikuti prasyarat dengan tepat.

## Pertanyaan yang Sering Diajukan

**Q: How does shard optimization affect query speed?**  
A: Optimizing shards memadatkan indeks, mengurangi I/O disk, dan biasanya menghasilkan respons kueri yang lebih cepat.

**Q: Is it safe to run `optimizeShards` on a live node?**  
A: Ya, operasi ini dirancang untuk berjalan tanpa downtime, tetapi sebaiknya dijadwalkan pada periode lalu lintas rendah untuk indeks yang besar.

**Q: Can I customize the `OptimizeOptions`?**  
A: Tentu saja. Anda dapat mengatur parameter seperti `maxSegmentSize` atau `mergeFactor` untuk menyesuaikan proses optimisasi.

**Q: What should I do if I encounter an `IOException` during optimization?**  
A: Verifikasi izin sistem file, pastikan ruang disk cukup, dan pastikan tidak ada proses lain yang mengunci file indeks.

**Q: Does optimizing shards also reclaim deleted document space?**  
A: Ya, optimizer menggabungkan segmen dan menghapus tombstone, membebaskan ruang yang ditempati dokumen yang dihapus.

---

**Terakhir Diperbarui:** 2026-01-21  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs