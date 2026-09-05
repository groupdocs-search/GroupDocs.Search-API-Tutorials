---
date: '2026-05-17'
description: Pelajari cara menambahkan groupdocs Maven dependency, menyiapkan jaringan
  pencarian Java, dan menambahkan direktori ke indeks untuk pengambilan dokumen yang
  cepat, skalabel.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Cara Menambahkan GroupDocs Maven Dependency untuk Jaringan Pencarian
type: docs
url: /id/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Cara Menambahkan Dependensi Maven GroupDocs untuk Jaringan Pencarian

Dalam panduan komprehensif ini Anda akan menemukan **cara menambahkan dependensi Maven groupdocs**, mengonfigurasi jaringan pencarian Java yang kuat menggunakan GroupDocs.Search, dan menjaga shard Anda tetap sinkron. Baik Anda mengindeks ringkasan hukum, laporan keuangan, atau makalah akademik, langkah-langkah di bawah ini akan membantu Anda membuat indeks yang dapat dicari, mendistribusikan beban kueri ke seluruh node, dan mempertahankan konsistensi data dengan upaya minimal.

## Jawaban Cepat
- **Apa itu dependensi Maven GroupDocs?** Sebuah artefak Maven yang mengemas pustaka GroupDocs.Search untuk proyek Java.  
- **Mengapa menggunakan jaringan pencarian?** Ia mendistribusikan beban pengindeksan dan kueri ke beberapa node, meningkatkan kecepatan dan keandalan.  
- **Bagaimana cara menambahkan direktori ke indeks?** Gunakan `IndexingDocuments.addDirectories` pada node master.  
- **Bagaimana cara menyinkronkan shard?** Panggil `SynchronizeOptions` pada setiap `Indexer` node.  
- **Apakah saya memerlukan lisensi?** Ya, lisensi percobaan atau komersial diperlukan untuk penggunaan produksi.

## Apa itu Dependensi Maven GroupDocs?

`GroupDocs Maven dependency` adalah artefak Maven yang mengemas pustaka GroupDocs.Search untuk proyek Java.  
Ia menyediakan semua kelas yang diperlukan untuk membuat indeks yang dapat dicari, mengelola node jaringan, dan mengeksekusi kueri cepat, serta Maven menyelesaikan dependensi transitif secara otomatis, memberi Anda mesin pencari siap pakai dengan hanya beberapa baris di `pom.xml` Anda.

## Cara Menambahkan Dependensi Maven GroupDocs

Tambahkan entri repositori dan dependensi ke `pom.xml` Anda, lalu jalankan `mvn clean install`; Maven mengunduh JAR `groupdocs-search` dan pustaka yang diperlukan, membuat API tersedia dalam proyek Anda. Setelah proses build berhasil, Anda dapat langsung mulai menggunakan kelas `com.groupdocs.search`.

### Konfigurasi Maven

Tambahkan repositori dan dependensi ke `pom.xml` Anda:

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

> **Tip Pro:** Jaga nomor versi tetap terbaru dengan memeriksa halaman rilis resmi.

Anda juga dapat mengunduh JAR secara langsung dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Mengapa Menggunakan Jaringan Pencarian?

Jaringan pencarian memungkinkan penskalaan horizontal dengan mempartisi indeks menjadi shard yang berada di node terpisah. GroupDocs.Search dapat menangani **lebih dari 50 format input** dan memproses **dokumen ratusan halaman** tanpa memuat seluruh file ke memori, memberikan respons kueri sub‑detik bahkan saat volume data meningkat.

## Prasyarat

- **JDK** (11 atau lebih baru) terpasang.  
- Sebuah IDE seperti IntelliJ IDEA atau Eclipse.  
- Pengetahuan dasar Java, familiaritas dengan Maven, dan pemahaman konsep node jaringan.  
- Lisensi GroupDocs.Search yang valid (percobaan gratis atau komersial).

## Inisialisasi dan Penyiapan Dasar

Mulailah dengan membuat direktori indeks:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Langkah sederhana ini menyiapkan lingkungan untuk konfigurasi jaringan selanjutnya.

## Panduan Implementasi

### Fitur 1: Konfigurasi Jaringan Pencarian

#### Gambaran Umum

Mengonfigurasi jaringan pencarian menetapkan jalur file dan port yang akan digunakan node untuk berkomunikasi.

##### Menyiapkan Jalur dan Port

`Configuration` adalah kelas yang menyimpan jalur jaringan, port, dan pengaturan lain untuk klaster pencarian.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
Objek `configuration` kini menyimpan semua pengaturan yang diperlukan untuk jaringan pencarian Anda.

### Fitur 2: Menyebarkan Node Jaringan Pencarian

#### Gambaran Umum

Sebarkan node untuk mendistribusikan beban kerja di seluruh jaringan Anda. Node master mengelola operasi dan peristiwa.

##### Kode Penyebaran

`SearchNetworkNode` mewakili sebuah node dalam jaringan pencarian yang dapat berperan sebagai master atau pekerja.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Fitur 3: Berlangganan ke Event Node Jaringan Pencarian

#### Gambaran Umum

Mendengarkan peristiwa memungkinkan penanganan dinamis terhadap perubahan atau pembaruan dalam jaringan Anda.

##### Implementasi Langganan

`SearchNetworkNodeEvents` menyediakan hook peristiwa untuk siklus hidup node dan aksi pengindeksan.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Fitur 4: Menambahkan Direktori ke Indeks

#### Gambaran Umum

Menambahkan direktori adalah langkah inti yang membuat dokumen Anda dapat dicari.

##### Penambahan Dokumen

`IndexingDocuments.addDirectories` menambahkan jalur folder ke indeks untuk diproses.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Fitur 5: Menyinkronkan Shard di Node Jaringan Pencarian

#### Gambaran Umum

Sinkronisasi memastikan konsistensi data di seluruh shard.

##### Kode Sinkronisasi

`SynchronizeOptions` mengonfigurasi cara shard disinkronkan antar node.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Fitur 6: Menutup Node Jaringan Pencarian

#### Gambaran Umum

Menutup node dengan benar melepaskan sumber daya dan mencegah kebocoran memori.

##### Penutupan Node

`close()` melepaskan sumber daya dan mematikan node jaringan pencarian.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Aplikasi Praktis

1. **Manajemen Dokumen Hukum** – Dengan cepat mengambil berkas kasus dan preseden.  
2. **Pencatatan Keuangan** – Mengakses laporan dan jejak audit dalam hitungan detik.  
3. **Penelitian Akademik** – Mencari di antara ribuan makalah untuk menemukan sitasi yang relevan.

## Pertimbangan Kinerja

- **Optimalkan Kueri** – Tulis kueri singkat untuk mengurangi waktu respons.  
- **Manajemen Memori** – Pantau penggunaan heap JVM; pertimbangkan penyesuaian GC untuk indeks besar.  
- **Strategi Penskalaan** – Tambahkan node secara proporsional dengan volume data dan beban kueri.

## Masalah Umum dan Solusinya

| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| Node gagal terhubung | Konflik port | Ubah `basePort` ke nilai yang tidak digunakan |
| Indeks tidak terbarui | Langganan event tidak ada | Pastikan `SearchNetworkNodeEvents.subscribe(masterNode)` dipanggil |
| Latensi tinggi | Shard tidak cukup | Tingkatkan jumlah node dan seimbangkan distribusi dokumen |

## Pertanyaan yang Sering Diajukan

**Q: Apa manfaat utama menggunakan GroupDocs.Search?**  
A: Ia menyediakan kemampuan pencarian cepat dan skalabel pada set dokumen besar dengan konfigurasi minimal.

**Q: Bisakah saya menyesuaikan konfigurasi node dalam jaringan pencarian?**  
A: Ya, Anda dapat mengatur jalur khusus, port, dan opsi lain melalui objek `Configuration`.

**Q: Bagaimana cara menambahkan direktori ke indeks setelah jaringan berjalan?**  
A: Panggil `IndexingDocuments.addDirectories(masterNode, "path")` kapan pun Anda perlu mengindeks folder baru.

**Q: Bagaimana cara menyinkronkan shard ketika node baru bergabung ke jaringan?**  
A: Gunakan metode `synchronizeShards` yang ditunjukkan di atas pada node yang baru ditambahkan.

**Q: Apakah saya memerlukan lisensi untuk pengembangan?**  
A: Lisensi percobaan gratis cukup untuk pengujian; lisensi komersial diperlukan untuk produksi.

## Kesimpulan

Dengan mengikuti panduan ini Anda kini tahu cara **menambahkan dependensi Maven groupdocs**, mengonfigurasi jaringan pencarian multi‑node, mengindeks direktori, dan menjaga shard tetap sinkron. Langkah-langkah ini meletakkan fondasi bagi solusi pencarian dokumen berperforma tinggi yang dapat berkembang seiring kebutuhan organisasi Anda.

---

**Terakhir Diperbarui:** 2026-05-17  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Tutorial dan Contoh GroupDocs.Search untuk Java](/search/net/)
- [Mengonfigurasi Jaringan GroupDocs.Search di .NET: Panduan Komprehensif](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Cara Mengimplementasikan Jaringan Pencarian dengan GroupDocs.Search di .NET untuk Sistem Manajemen Dokumen](/search/net/search-network/implement-search-network-groupdocs-dotnet/)