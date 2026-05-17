---
date: '2026-05-17'
description: Pelajari cara mengkonfigurasi base port groupdocs untuk jaringan GroupDocs.Search
  Java yang dapat diskalakan, mengoptimalkan retrieval speed, dan menyiapkan multi‑node
  systems.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: Konfigurasi base port groupdocs dalam Java Search Network
type: docs
url: /id/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Konfigurasi port dasar groupdocs dalam Jaringan Pencarian Java

Dalam aplikasi modern yang berat data, **configure base port groupdocs** adalah langkah pertama untuk membangun infrastruktur pencarian yang cepat dan dapat diandalkan. Baik Anda mengindeks ribuan PDF atau memperluas ke beberapa server, penetapan port dan direktori unik mencegah konflik antar node dan menjaga kesehatan klaster. Tutorial ini memandu Anda melalui prasyarat, instalasi, dan konfigurasi multi‑node lengkap menggunakan GroupDocs.Search untuk Java, sehingga Anda dapat meluncurkan jaringan pencarian yang benar‑benar dapat diskalakan hari ini.

## Jawaban Cepat
- **Apa tujuan utama?** Untuk menetapkan port unik dan direktori dasar untuk setiap node pencarian, menghilangkan konflik.  
- **Apakah saya memerlukan lisensi?** Ya – lisensi percobaan atau lisensi penuh diperlukan untuk penyebaran produksi.  
- **Versi Java apa yang didukung?** Java 8 atau lebih tinggi (Java 11+ direkomendasikan).  
- **Apakah saya dapat menjalankannya di server cloud?** Tentu saja – cukup buka port yang dipilih di grup keamanan cloud Anda.  
- **Berapa banyak node yang dapat saya tambahkan?** Tidak ada batasan keras; Anda hanya dibatasi oleh perangkat keras dan kapasitas jaringan.

## Apa itu “configure base port groupdocs”?

**Configure base port groupdocs** adalah proses penetapan port TCP awal yang akan digunakan setiap node pencarian dan meningkatkannya untuk node berikutnya. Langkah sederhana ini menghilangkan kesalahan “port already in use” yang menakutkan dan menyiapkan dasar untuk klaster pencarian yang bersih dan dapat diskalakan secara horizontal, memastikan setiap node berkomunikasi melalui endpoint yang berbeda.

## Mengapa menggunakan GroupDocs.Search untuk jaringan yang dapat diskalakan?

GroupDocs.Search menyediakan **high‑performance indexing** (hingga 50 GB/menit pada server standar 8‑core) dan mendukung **50+ file formats** termasuk PDF, DOCX, PPTX, dan HTML. Arsitektur modularnya memungkinkan Anda mencampur indexer, searcher, shard, dan extractor di seluruh node, memberikan skalabilitas linear saat Anda menambah perangkat keras. Perpustakaan ini juga menawarkan opsi kompresi bawaan yang mengurangi penggunaan disk hingga 70 % sambil menjaga latensi kueri di bawah 200 ms untuk beban kerja tipikal.

## Prasyarat
- **Java Development Kit (JDK)** 8 atau lebih baru (Java 11+ direkomendasikan untuk garbage‑collection yang lebih baik).  
- **IDE** seperti IntelliJ IDEA atau Eclipse.  
- **GroupDocs.Search for Java** library (versi 25.4 atau lebih baru) diinstal melalui Maven atau unduhan manual.  
- Pengetahuan jaringan dasar (port TCP, localhost vs. remote hosts).  
- Lisensi **GroupDocs.Search** yang valid (percobaan atau penuh).

## Menyiapkan GroupDocs.Search untuk Java

### Instruksi Instalasi

**Maven Setup:**

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

**Direct Download:**

Sebagai alternatif, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Perolehan Lisensi

- **Free Trial** – mulai menguji segera.  
- **Temporary License** – dapatkan percobaan diperpanjang di [Temporary License](https://purchase.groupdocs.com/temporary-license).  
- **Full Purchase** – diperlukan untuk penyebaran produksi.

### Inisialisasi dan Penyiapan Dasar

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Panduan Implementasi

### Bagaimana cara mengkonfigurasi base port groupdocs?

Untuk mengkonfigurasi base port, edit file konfigurasi jaringan atau secara programatis atur properti `basePort` ke nilai tinggi yang tidak terpakai seperti 49100. Untuk setiap node berikutnya tingkatkan nomor port satu per satu (atau dengan offset tetap) sehingga setiap node terikat pada endpoint TCP yang unik, menghilangkan kesalahan tabrakan port dan menyederhanakan aturan firewall.

#### Menyiapkan Jalur Dasar

Sebelum menulis kode apa pun, tentukan tata letak folder yang konsisten. Misalnya, buat direktori terpisah untuk indexer (`Indexer0`), searcher (`Searcher0`), dan extractor (`Extractor0`). Struktur ini memungkinkan setiap node menemukan file dengan cepat.

- **Why**: Sebuah hierarki direktori yang dapat diprediksi mencegah kesalahan “file not found” ketika node memulai pada mesin yang berbeda.

#### Mengkonfigurasi Base Port

Pilih port awal yang tinggi untuk menghindari benturan dengan layanan umum (HTTP 80, SSH 22, dll.). Tingkatkan nomor port untuk setiap node baru yang Anda tambahkan.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: Memulai pada port tinggi (mis., 49100) mengurangi kemungkinan bertabrakan dengan layanan yang ada dan menyederhanakan pembuatan aturan firewall.

#### Tentukan Alamat Host

Selama pengembangan, `localhost` berfungsi baik. Untuk produksi, ganti dengan alamat IP server atau nama DNS sehingga node remote dapat saling menjangkau.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: Menggunakan alamat host yang nyata memungkinkan komunikasi lintas mesin, yang penting untuk klaster cloud atau on‑premise.

#### Buat Konfigurasi Jaringan

Kelas `NetworkConfig` menggabungkan semua opsi jaringan—base port, host, dan pengaturan SSL opsional—ke dalam satu objek yang dikonsumsi mesin Pencarian.

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Why**: Memusatkan opsi-opsi ini membuat konfigurasi dapat digunakan kembali dan lebih mudah dipelihara di banyak node.

#### Tambahkan Node

`SearchNode` mewakili node individual dalam klaster GroupDocs.Search yang melakukan fungsi spesifik seperti pengindeksan atau pencarian. Instansiasi `SearchNode` untuk setiap peran (indexer, searcher, extractor) dan daftarkan ke `SearchEngine`. Distribusi tanggung jawab di seluruh node meningkatkan paralelisme dan toleransi kesalahan.

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Why**: Membagi pekerjaan di antara node khusus mengurangi kontensi dan memungkinkan setiap mesin mengkhususkan diri pada satu tugas, meningkatkan throughput keseluruhan.

#### Selesaikan Konfigurasi

Setelah menambahkan semua node, panggil `engine.start()` untuk menghidupkan jaringan. Mesin secara otomatis akan mengikat setiap node ke port yang ditetapkan dan memverifikasi konektivitas.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Masalah Umum & Solusi

- **Port Conflicts** – Selalu tingkatkan `basePort` untuk setiap node baru. Verifikasi port terbuka dengan `netstat` atau monitor jaringan OS Anda.  
- **Missing Directories** – Pastikan setiap folder (`Indexer0`, `Searcher0`, dll.) ada dan proses Java memiliki izin baca/tulis.  
- **Network Reachability** – Saat beralih ke pengaturan multi‑mesin, ganti `127.0.0.1` dengan IP host sebenarnya dan buka port yang dipilih di firewall.  

## Aplikasi Praktis

| Skenario | Manfaat mengkonfigurasi base port groupdocs |
|----------|--------------------------------------------|
| Manajemen Dokumen Perusahaan | Skalabilitas mulus di seluruh departemen tanpa downtime |
| Platform CMS Besar | Pengambilan konten lebih cepat karena indeks didistribusikan |
| Manajemen Kasus Hukum | Ekstraksi paralel PDF mengurangi latensi pencarian |

## Pertimbangan Kinerja

- **Monitor CPU/Memory** – Gunakan JMX Java atau alat profiling untuk memantau penggunaan thread.  
- **Adjust Compression** – `Compression.High` menghemat ruang disk tetapi dapat menambah beban CPU; uji baik `High` maupun `Normal` untuk menemukan titik optimal.  
- **Regular Updates** – Rilis baru GroupDocs.Search sering menyertakan perbaikan kinerja; tetap perbarui perpustakaan.

## Kesimpulan

Anda kini telah mempelajari cara **configure base port groupdocs** dan menyiapkan jaringan pencarian multi‑node menggunakan GroupDocs.Search untuk Java. Bereksperimenlah dengan node tambahan, sesuaikan pengaturan indeks, dan integrasikan jaringan ke dalam aplikasi Anda yang ada untuk solusi pencarian yang benar‑benar dapat diskalakan.

## Pertanyaan yang Sering Diajukan

**Q: Apa tujuan menonaktifkan stop words dalam pengindeksan?**  
A: Menonaktifkan stop words dapat meningkatkan akurasi pencarian dengan mempertahankan istilah umum yang mungkin penting dalam domain khusus.

**Q: Bagaimana cara menangani konflik port saat menambahkan banyak node?**  
A: Mulailah dengan `basePort` tinggi (mis., 49100) dan tingkatkan untuk setiap node berikutnya, memastikan setiap node memiliki endpoint TCP yang unik.

**Q: Apakah saya dapat menggunakan pengaturan ini untuk aplikasi berbasis cloud?**  
A: Ya—pastikan port yang dipilih terbuka di grup keamanan cloud Anda dan ganti `127.0.0.1` dengan IP publik atau privat yang sesuai.

**Q: Apa perbedaan antara NormalIndex dan tipe indeks lainnya?**  
A: `NormalIndex` menawarkan kompromi seimbang antara kecepatan dan penggunaan memori, sementara indeks khusus (mis., `FastIndex`) menargetkan skenario kinerja niche.

**Q: Apakah ada batasan jumlah node yang dapat saya tambahkan?**  
A: Secara teknis tidak; batasannya ditentukan oleh sumber daya perangkat keras dan bandwidth jaringan Anda.

---

**Terakhir Diperbarui:** 2026-05-17  
**Diuji Dengan:** GroupDocs.Search Java 25.4  
**Penulis:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## Tutorial Terkait

- [Cara Mengonfigurasi Jaringan Pencarian .NET Menggunakan GroupDocs.Search dan Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Cara Mengimplementasikan Jaringan Pencarian dengan GroupDocs.Search di .NET untuk Sistem Manajemen Dokumen](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Menyebarkan Node Jaringan Pencarian di .NET menggunakan GroupDocs untuk Pengindeksan dan Pengambilan Dokumen yang Efisien](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)