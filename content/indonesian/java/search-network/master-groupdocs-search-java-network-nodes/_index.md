---
date: '2026-07-02'
description: Pelajari cara mendapatkan lisensi sementara untuk GroupDocs.Search, menambahkan
  direktori ke indeks, dan menambahkan atribut dokumen khusus sambil mengelola node
  jaringan pencarian Java.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Dapatkan Lisensi Sementara GroupDocs – Master Search Nodes (Java)
type: docs
url: /id/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Dapatkan Lisensi Sementara GroupDocs – Node Pencarian Master (Java)

Dalam panduan komprehensif ini Anda akan **mendapatkan lisensi sementara untuk GroupDocs.Search**, mengkonfigurasi jaringan pencarian multi‑node, dan belajar cara **menambahkan direktori ke indeks** serta **menambahkan atribut dokumen khusus** menggunakan Java. Baik Anda membangun sistem manajemen dokumen perusahaan atau katalog produk yang dapat dicari, menguasai langkah‑langkah ini memungkinkan Anda mengevaluasi platform tanpa batasan dan dengan cepat meningkatkan kemampuan pencarian Anda.

## Jawaban Cepat
- **Apa langkah pertama untuk mulai menggunakan GroupDocs.Search?** Dapatkan lisensi sementara dari portal GroupDocs.  
- **Repository Maven mana yang menyimpan pustaka?** `https://releases.groupdocs.com/search/java/`.  
- **Bagaimana cara menambahkan direktori ke indeks?** Panggil helper `addDirectoriesToIndex` pada node master.  
- **Bisakah saya menambahkan atribut dokumen khusus?** Ya—panggil `addAttribute` dengan kunci dokumen dan nama atribut.  
- **Bagaimana cara mematikan node dengan bersih?** Panggil `closeNodes` untuk melepaskan sumber daya.

## Apa itu lisensi sementara dan mengapa saya membutuhkannya?
Lisensi sementara memungkinkan Anda mengevaluasi GroupDocs.Search tanpa batasan evaluasi apa pun. Ini sempurna untuk pengembangan, pengujian, atau proyek proof‑of‑concept sebelum berkomitmen pada pembelian penuh. Lisensi ini memberikan akses penuh ke semua fitur untuk periode terbatas, memungkinkan Anda mengukur kinerja, menguji titik integrasi, dan memastikan solusi memenuhi kebutuhan Anda tanpa komitmen finansial.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

### Perpustakaan dan Ketergantungan yang Diperlukan
Untuk bekerja dengan GroupDocs.Search untuk Java, sertakan ketergantungan Maven yang diperlukan:
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
Anda juga dapat mengunduh versi terbaru langsung dari [rilis GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

### Penyiapan Lingkungan
- Pastikan Anda memiliki JDK yang kompatibel terpasang (Java 8 atau lebih baru).  
- Siapkan IDE Anda untuk mendukung proyek Maven.

### Prasyarat Pengetahuan
Pemahaman dasar tentang pemrograman Java dan familiaritas dengan manajemen proyek Maven akan sangat membantu. Jika Anda baru dengan konsep-konsep ini, pertimbangkan untuk menjelajahi sumber daya pengantar untuk memulai.

## Cara mendapatkan lisensi sementara
Lisensi sementara diperoleh dengan mengunjungi portal GroupDocs, mengisi formulir permintaan singkat, dan menempatkan file `.lic` yang diterima ke dalam folder `resources` proyek Anda. Kemudian inisialisasi lisensi dengan beberapa baris kode (lihat potongan di bawah). Untuk formulir permintaan, gunakan halaman resmi: [Lisensi Sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Menyiapkan GroupDocs.Search untuk Java

### Informasi Instalasi
Untuk mulai menggunakan GroupDocs.Search untuk Java dalam proyek Anda, ikuti langkah‑langkah Maven di atas atau unduh versi terbaru langsung dari halaman rilis resmi.

#### Langkah-langkah Akuisisi Lisensi
1. **Uji Coba Gratis** – Jelajahi fitur tanpa komitmen apa pun.  
2. **Lisensi Sementara** – Dapatkan kunci jangka pendek untuk pengujian (lihat bagian di atas).  
3. **Pembelian** – Untuk penggunaan produksi, beli lisensi penuh dari **[Halaman Pembelian GroupDocs](https://purchase.groupdocs.com/)**.

### Inisialisasi dan Penyiapan Dasar
Inisialisasi proyek Anda dengan GroupDocs.Search sebagai berikut:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Langkah inisialisasi ini penting untuk memastikan semua komponen berfungsi mulus dalam jaringan pencarian Anda.

## Panduan Implementasi
Sekarang, mari kita uraikan proses menjadi bagian‑bagian yang dapat dikelola, masing‑masing berfokus pada fitur spesifik dalam penyebaran dan pengelolaan node jaringan pencarian.

### Fitur 1: Penyiapan Konfigurasi
**Gambaran Umum:** Menyiapkan konfigurasi untuk jaringan pencarian Anda adalah langkah pertama dalam menyebarkan node. Penyiapan ini melibatkan penentuan jalur dan port yang penting untuk penyebaran node.

#### Langkah-langkah Implementasi:
##### Langkah 1: Tentukan Jalur Dasar dan Port
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Langkah 2: Konfigurasikan Jaringan Pencarian
Fungsi `configureSearchNetwork` menyiapkan objek konfigurasi yang diperlukan untuk menyebarkan node.  
`Configuration` adalah kelas yang menyimpan semua pengaturan seperti folder indeks, port jaringan, dan peran node.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parameter:** Jalur dasar dan port digunakan untuk menemukan sumber daya dan membangun saluran komunikasi.  
- **Nilai Kembali:** Objek `Configuration` yang dikonfigurasi sesuai kebutuhan penyebaran Anda.

### Fitur 2: Penyebaran Jaringan Pencarian
**Gambaran Umum:** Menyebarkan node penting untuk memperluas kemampuan pencarian Anda di berbagai lingkungan atau segmen data.

#### Langkah-langkah Implementasi:
##### Langkah 1: Sebarkan Node
Fungsi `deploySearchNetwork` menginisialisasi dan mengembalikan array node jaringan pencarian.  
`SearchNetworkNodes` mewakili setiap instance node yang berpartisipasi dalam klaster pencarian terdistribusi.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parameter:** Jalur dasar, port, dan konfigurasi digunakan untuk menentukan lingkungan penyebaran.  
- **Nilai Kembali:** Sebuah array yang berisi `SearchNetworkNodes` yang telah diinisialisasi.

### Fitur 3: Berlangganan ke Peristiwa Jaringan
**Gambaran Umum:** Memantau aktivitas jaringan pencarian Anda penting untuk menjaga kinerja optimal dan keandalan.

#### Langkah-langkah Implementasi:
##### Langkah 1: Berlangganan ke Peristiwa Node Master
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Tujuan:** Langkah ini memastikan Anda diberi tahu tentang peristiwa penting atau perubahan dalam jaringan pencarian Anda.

### Fitur 4: Pengindeksan Dokumen
**Gambaran Umum:** Menambahkan direktori yang berisi dokumen untuk diindeks memungkinkan pengambilan data yang efisien di seluruh jaringan Anda.

#### Cara menambahkan direktori ke indeks
`addDirectoriesToIndex` adalah metode helper yang mendaftarkan jalur folder untuk diindeks pada node master.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Tujuan:** Memfasilitasi akses cepat dan kemampuan pencarian semua dokumen dalam direktori yang ditentukan.

### Fitur 5: Menambahkan Atribut ke Dokumen
**Gambaran Umum:** Atribut khusus meningkatkan metadata dokumen, membuat pencarian lebih fleksibel dan informatif.

#### Cara menambahkan atribut dokumen khusus
`addAttribute` menambahkan atribut metadata khusus ke dokumen tertentu dalam indeks.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parameter:** Tentukan node, kunci dokumen, dan atribut yang akan ditambahkan.  
- **Tujuan:** Memperluas fungsionalitas pencarian dengan memperkaya dokumen dengan metadata tambahan.

### Fitur 6: Mengambil Dokumen yang Diindeks
**Gambaran Umum:** Mengambil dan mendaftar dokumen yang diindeks secara efisien untuk memastikan akurasi dan kelengkapan data.

#### Langkah-langkah Implementasi:
##### Langkah 1: Dapatkan Dokumen yang Diindeks
```java
getIndexedDocuments(nodes[0]);
```  
- **Tujuan:** Memverifikasi keberhasilan pengindeksan semua dokumen yang diperlukan dalam jaringan pencarian Anda.

### Fitur 7: Menutup Node Jaringan
**Gambaran Umum:** Menutup node dengan benar penting untuk manajemen sumber daya dan mencegah kebocoran memori.

#### Langkah-langkah Implementasi:
##### Langkah 1: Tutup Semua Node
`closeNodes` mematikan semua node pencarian yang aktif dan melepaskan sumber daya yang dialokasikan.  
```java
closeNodes(nodes);
```  
- **Tujuan:** Melepaskan sumber daya yang ditempati oleh setiap node, memastikan proses penutupan yang bersih.

## Mengapa menggunakan lisensi sementara untuk GroupDocs.Search?
Lisensi sementara memberikan **akses penuh ke semua fitur selama 30 hari** dan mendukung hingga **50.000 dokumen yang diindeks** tanpa pembatasan kinerja. Ini memungkinkan Anda mengukur kecepatan pengindeksan, latensi kueri, dan skalabilitas pada data dunia nyata sebelum membeli lisensi produksi. Lisensi ini juga menghapus watermark evaluasi, memberikan representasi sejati dari kemampuan produk akhir.

## Kasus Penggunaan Umum
1. **Manajemen Dokumen Perusahaan** – Mengindeks jutaan file internal di seluruh departemen, memungkinkan pencarian teks penuh secara instan.  
2. **Platform E‑commerce** – Membangun katalog produk yang dapat dicari yang mencakup banyak gudang dan umpan pihak ketiga.  
3. **Firma Hukum** – Mengatur berkas kasus, kontrak, dan bukti dengan metadata khusus untuk pengambilan cepat.

Kemungkinan integrasi dengan sistem lain mencakup platform CRM, sistem manajemen konten (CMS), dan alat analitik data, memanfaatkan fitur pengindeksan dan pencarian yang kuat yang disediakan oleh GroupDocs.Search untuk Java.

## Pertimbangan Kinerja
Untuk mengoptimalkan kinerja saat menggunakan GroupDocs.Search untuk Java:
- **Optimalkan Konfigurasi** – Sesuaikan pengaturan konfigurasi Anda agar cocok dengan lingkungan penyebaran spesifik Anda.  
- **Pantau Penggunaan Sumber Daya** – Secara rutin periksa CPU, memori, dan I/O untuk mencegah bottleneck atau kebocoran memori.  
- **Ikuti Praktik Terbaik** – Patuhi pedoman manajemen memori Java, memastikan pemanfaatan sumber daya sistem yang efisien.

## Pertanyaan yang Sering Diajukan

**T: Berapa lama lisensi sementara tetap berlaku?**  
J: Lisensi sementara biasanya berlaku selama 30 hari, memberi Anda waktu yang cukup untuk mengevaluasi produk.

**T: Bisakah saya beralih dari lisensi sementara ke lisensi penuh tanpa menginstal ulang?**  
J: Ya—ganti file lisensi sementara dengan file lisensi penuh dan restart aplikasi Anda.

**T: Apakah saya perlu mengindeks ulang dokumen setelah menerapkan lisensi baru?**  
J: Tidak, indeks tetap utuh; lisensi hanya mengatur hak penggunaan.

**T: Apa yang terjadi jika saya lupa menutup node?**  
J: Sumber daya yang tidak dilepaskan dapat menyebabkan kebocoran memori; selalu panggil `closeNodes` saat penutupan.

**T: Apakah memungkinkan menambahkan lebih dari satu atribut khusus per dokumen?**  
J: Tentu—panggil `addAttribute` beberapa kali dengan nama atribut yang berbeda.

---
**Terakhir Diperbarui:** 2026-07-02  
**Diuji Dengan:** GroupDocs.Search untuk Java 25.4  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Menyebarkan Node Jaringan Pencarian di .NET menggunakan GroupDocs untuk Pengindeksan dan Pengambilan Dokumen yang Efisien](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Cara Mengimplementasikan Jaringan Pencarian dengan GroupDocs.Search di .NET untuk Sistem Manajemen Dokumen](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Mengonfigurasi Jaringan Aspose.Search & Menambahkan Atribut Dokumen dengan GroupDocs.Redaction untuk .NET: Panduan Komprehensif](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)