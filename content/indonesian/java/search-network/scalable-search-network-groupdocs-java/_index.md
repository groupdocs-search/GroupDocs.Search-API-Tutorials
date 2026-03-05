---
date: '2026-01-24'
description: Pelajari cara mengonfigurasi basis GroupDocs untuk jaringan pencarian
  yang dapat diskalakan menggunakan GroupDocs.Search Java, mengoptimalkan kecepatan
  pengambilan, dan menyiapkan sistem multi-node.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Konfigurasikan port dasar groupdocs dalam Jaringan Pencarian Java
type: docs
url: /id/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Konfigurasi base port groupdocs dalam Java Search Network

Dalam aplikasi modern yang berat data, **configuring base port groupdocs** merupakan langkah dasar untuk membangun infrastruktur pencarian yang cepat dan handal. Baik Anda menangani ribuan PDF atau menskalakan ke beberapa server, mengatur port dan jalur yang tepat memastikan setiap node berkomunikasi dengan yang lain tanpa konflik. Tutorial ini memandu Anda melalui setiap detail—dari prasyarat hingga konfigurasi multi‑node lengkap—sehingga Anda dapat meluncurkan jaringan pencarian yang dapat diskalakan dengan percaya diri menggunakan GroupDocs.Search untuk Java.

## Jawaban Cepat
- **What is the primary purpose?** Untuk mengatur port dan direktori unik bagi setiap node pencarian, mencegah konflik.
- **Do I need a license?** Ya, lisensi percobaan atau penuh diperlukan untuk penggunaan produksi.
- **Which Java version is supported?** Java 8 atau lebih tinggi.
- **Can I run this on cloud servers?** Tentu—pastikan port terbuka di grup keamanan Anda.
- **How many nodes can I add?** Tidak ada batas keras; tambahkan sebanyak yang diizinkan oleh perangkat keras dan jaringan Anda.

## Apa itu “configure base port groupdocs”?
Saat Anda **configure base port groupdocs**, Anda menetapkan port TCP awal yang akan digunakan setiap node (dan meningkatkannya untuk node berikutnya). Langkah sederhana ini menghilangkan kesalahan “port already in use” yang menakutkan dan menyiapkan dasar untuk klaster pencarian yang bersih dan dapat diskalakan secara horizontal.

## Mengapa menggunakan GroupDocs.Search untuk jaringan yang dapat diskalakan?
- **High performance** – algoritma pengindeksan dan pencarian yang dioptimalkan.
- **Flexible architecture** – Anda dapat mencampur indexer, searcher, shard, dan extractor di seluruh node.
- **Easy integration** – bekerja dengan aplikasi Java apa pun, on‑premise atau cloud.
- **Robust licensing** – opsi percobaan memungkinkan Anda menguji sebelum berkomitmen.

## Prasyarat
- **Java Development Kit (JDK)** 8 atau lebih baru.
- **IDE** seperti IntelliJ IDEA atau Eclipse.
- **GroupDocs.Search for Java** library (versi 25.4 atau lebih baru) diinstal melalui Maven atau unduhan manual.
- Pengetahuan dasar jaringan (port TCP, localhost vs. host remote).

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

Alternatifnya, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi

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

### Cara mengkonfigurasi base port groupdocs

#### Menyiapkan Jalur Dasar

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Why**: Struktur direktori yang konsisten memungkinkan setiap node menemukan file indeks, shard, atau extractor tanpa ambiguitas.

#### Mengkonfigurasi Base Port

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: Memulai dengan nomor port tinggi (mis., 49100) mengurangi kemungkinan bentrok dengan layanan umum. Tingkatkan port untuk setiap node tambahan.

#### Menentukan Alamat Host

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: Menggunakan `localhost` ideal untuk pengembangan; ganti dengan IP atau nama DNS server Anda untuk produksi.

#### Membuat Konfigurasi Jaringan

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

- **Why**: Opsi-opsi ini menyeimbangkan kecepatan dan efisiensi penyimpanan, memberikan indeks pencarian yang ramping namun kuat.

#### Menambahkan Node

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

- **Why**: Membagi tanggung jawab di antara node (pengindeksan vs. pencarian, sharding vs. ekstraksi) meningkatkan paralelisme dan toleransi kesalahan.

#### Menyelesaikan Konfigurasi

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Masalah Umum & Solusi
- **Port Conflicts** – Selalu tingkatkan `basePort` untuk setiap node baru. Verifikasi dengan `netstat` atau monitor port OS Anda.
- **Missing Directories** – Pastikan setiap folder yang direferensikan (`Indexer0`, `Searcher0`, dll.) ada dan proses Java memiliki izin baca/tulis.
- **Network Reachability** – Saat beralih ke setup multi‑mesin, ganti `127.0.0.1` dengan IP host yang sebenarnya dan buka port yang dipilih di firewall.

## Aplikasi Praktis

| Scenario | Manfaat Mengkonfigurasi Base Port GroupDocs |
|----------|--------------------------------------------|
| Enterprise Document Management | Skalabilitas mulus antar departemen tanpa downtime |
| Large CMS Platforms | Pengambilan konten lebih cepat karena indeks didistribusikan |
| Legal Case Management | Ekstraksi paralel PDF mengurangi latensi pencarian |

## Pertimbangan Kinerja

- **Monitor CPU/Memory** – Gunakan JMX Java atau alat profiling untuk memantau penggunaan thread.
- **Adjust Compression** – `Compression.High` menghemat ruang disk tetapi dapat menambah beban CPU; uji both `High` dan `Normal`.
- **Update Regularly** – Rilis GroupDocs.Search baru sering menyertakan perbaikan kinerja.

## Kesimpulan

Anda kini telah mempelajari cara **configure base port groupdocs** dan menyiapkan jaringan pencarian multi‑node menggunakan GroupDocs.Search untuk Java. Bereksperimenlah dengan node tambahan, sesuaikan pengaturan indeks, dan integrasikan jaringan ke dalam aplikasi Anda yang ada untuk solusi pencarian yang benar‑benar dapat diskalakan.

## Pertanyaan yang Sering Diajukan

**Q: What is the purpose of disabling stop words in indexing?**  
A: Menonaktifkan stop words dapat meningkatkan akurasi pencarian dengan mempertahankan istilah umum yang mungkin penting dalam domain khusus.

**Q: How do I handle port conflicts when adding multiple nodes?**  
A: Mulailah dengan `basePort` tinggi (mis., 49100) dan tingkatkan untuk setiap node berikutnya, memastikan setiap node memiliki endpoint TCP yang unik.

**Q: Can I use this setup for cloud‑based applications?**  
A: Ya—pastikan port yang dipilih terbuka di grup keamanan cloud Anda dan ganti `127.0.0.1` dengan IP publik atau privat yang sesuai.

**Q: What is the difference between NormalIndex and other index types?**  
A: `NormalIndex` menawarkan kompromi seimbang antara kecepatan dan penggunaan memori, sementara indeks khusus (mis., `FastIndex`) menargetkan skenario kinerja khusus.

**Q: Is there a limit to the number of nodes I can add?**  
A: Secara teknis tidak; batasnya ditentukan oleh sumber daya perangkat keras dan bandwidth jaringan Anda.

---

**Last Updated:** 2026-01-24  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs