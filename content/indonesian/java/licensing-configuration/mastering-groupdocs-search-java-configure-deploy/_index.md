---
date: '2026-05-02'
description: Pelajari cara mengkonfigurasi pencarian dan mengaktifkan pembaruan pencarian
  waktu nyata menggunakan GroupDocs.Search untuk Java. Panduan langkah demi langkah
  tentang penyiapan jaringan, penyebaran node, dan pengindeksan.
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: Cara Mengonfigurasi Pencarian dengan GroupDocs.Search di Java - Panduan Konfigurasi
  & Penyebaran
type: docs
url: /id/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Cara Mengonfigurasi Pencarian dengan GroupDocs.Search di Java

Di dunia digital yang bergerak cepat saat ini, **cara mengonfigurasi pencarian** secara efisien dapat menentukan keberhasilan sebuah proyek. Baik Anda menangani ribuan kontrak, makalah penelitian, atau laporan internal, jaringan pencarian yang dirancang dengan baik memungkinkan Anda menemukan dokumen yang tepat dalam hitungan detik. Tutorial ini memandu Anda melalui konfigurasi jaringan pencarian, penyebaran node, dan mengaktifkan **pembaruan pencarian waktu nyata** dengan GroupDocs.Search untuk Java.

## Jawaban Cepat
- **Apa tujuan utama jaringan pencarian?** Untuk mendistribusikan proses pengindeksan dan kueri ke beberapa node guna skalabilitas dan kecepatan.  
- **Versi perpustakaan apa yang diperlukan?** GroupDocs.Search untuk Java v25.4 atau yang lebih baru.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Bagaimana pembaruan waktu nyata ditangani?** Dengan berlangganan ke acara node yang dipicu pada perubahan pengindeksan.  
- **Bisakah saya menambahkan folder dokumen baru secara dinamis?** Ya—gunakan metode `addDirectories` pada indexer.

## Apa itu “cara mengonfigurasi pencarian” dalam konteks GroupDocs?
Mengonfigurasi pencarian berarti menyiapkan **jaringan pencarian** yang mengetahui lokasi dokumen Anda, cara node berkomunikasi, dan bagaimana pengindeksan dikoordinasikan. Setelah jaringan dikonfigurasi, Anda dapat menambah atau menghapus node tanpa waktu henti, memastikan akses berkelanjutan ke hasil pencarian yang selalu terbaru.

## Mengapa Menggunakan GroupDocs.Search untuk Java?
- **Skalabilitas:** Mendistribusikan beban kerja ke beberapa mesin.  
- **Pembaruan waktu nyata:** Secara instan mencerminkan file yang baru diindeks di seluruh jaringan.  
- **Kemudahan integrasi:** Pengaturan Maven yang sederhana dan API Java yang jelas.  
- **Siap untuk perusahaan:** Menangani korpus besar dan skenario kueri yang kompleks.

## Prasyarat
- **Java Development Kit (JDK) 8+** terpasang.  
- **Maven** untuk manajemen dependensi.  
- Familiaritas dasar dengan Java, Maven, dan konsep pencarian.  

## Menyiapkan GroupDocs.Search untuk Java

### Dependensi Maven
Add the repository and dependency to your `pom.xml`:

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

**Unduhan Langsung:** Anda juga dapat memperoleh perpustakaan dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Percobaan Gratis:** Dapatkan lisensi percobaan untuk menjelajahi semua fitur.  
- **Lisensi Sementara:** Minta untuk periode evaluasi yang diperpanjang.  
- **Lisensi Komersial:** Diperlukan untuk penyebaran produksi.

### Inisialisasi Dasar
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Cara mengonfigurasi jaringan pencarian di Java

### Langkah 1: Impor Paket yang Diperlukan
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Langkah 2: Konfigurasikan Jaringan
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parameter:** `basePath` menunjuk ke folder dokumen Anda; `basePort` adalah port TCP yang digunakan untuk komunikasi node.

## Menyebarkan Node Jaringan Pencarian

### Langkah 1: Impor Paket Penyebaran
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Langkah 2: Sebarkan Node
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Node Master:** Mengkoordinasikan pencarian dan pengindeksan di semua node. Anda dapat **mengonfigurasi node master** seperti alokasi shard dan pemeriksaan kesehatan.

## Berlangganan ke Acara Node untuk Pembaruan Pencarian Waktu Nyata

### Langkah 1: Impor Paket Acara
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Langkah 2: Berlangganan ke Acara Node Master
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Penanganan Acara:** Mengaktifkan **pembaruan pencarian waktu nyata** setiap kali dokumen ditambahkan, diperbarui, atau dihapus.

## Menambahkan Direktori untuk Pengindeksan

### Langkah 1: Impor Paket Indexer
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Langkah 2: Tambahkan Direktori Dokumen
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Pengindeksan Dinamis:** Gunakan metode `addDirectories` untuk **menambahkan direktori ke indeks** secara dinamis tanpa memulai ulang jaringan.

## Mengambil Dokumen yang Diindeks

### Langkah 1: Impor Paket Pencari
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Langkah 2: Ambil Informasi Dokumen
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Manajemen Shard:** Menangani dataset besar secara efisien dengan mendistribusikan dokumen ke seluruh shard. Untuk **mengoptimalkan ukuran shard**, pantau statistik shard dan sesuaikan konfigurasi `shardSize` pada rilis mendatang.

## Mengapa ini penting untuk proyek Anda
Jaringan pencarian yang dikonfigurasi dengan baik menghilangkan bottleneck, mengurangi latensi, dan memastikan pengguna selalu melihat versi terbaru dari sebuah dokumen. Pembaruan waktu nyata dan kemampuan untuk **menambahkan direktori ke indeks** tanpa waktu henti sangat berharga bagi firma hukum, institusi riset, dan organisasi mana pun yang menangani koleksi dokumen yang terus berubah.

## Aplikasi Praktis
1. **Manajemen Dokumen Perusahaan:** Memusatkan pencarian di seluruh jutaan file.  
2. **Firma Hukum:** Dengan cepat menemukan berkas kasus, kontrak, dan bukti.  
3. **Riset Akademik:** Mengindeks jurnal dan makalah untuk pengambilan instan.

## Pertimbangan Kinerja
- **Optimalkan Pengindeksan:** Jadwalkan penyegaran indeks secara reguler dan hapus data usang.  
- **Manajemen Memori:** Pantau heap JVM, terutama saat menangani shard besar.  
- **Perencanaan Skalabilitas:** Tambahkan node seiring pertumbuhan korpus Anda; jaringan secara otomatis menyeimbangkan beban.  
- **Optimalkan ukuran shard:** Shard yang lebih kecil meningkatkan latensi kueri, sementara shard yang lebih besar mengurangi overhead. Sesuaikan berdasarkan perangkat keras dan pola kueri Anda.

## Masalah Umum & Solusi
| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| Node tidak dapat terhubung | Konflik port atau firewall | Pastikan `basePort` terbuka dan tidak digunakan oleh layanan lain |
| Indeks tidak memperbarui | Langganan acara tidak ada | Panggil `SearchNetworkNodeEvents.subscribe(masterNode)` setelah penyebaran |
| Kesalahan kehabisan memori | Terlalu banyak shard besar yang dimuat | Kurangi ukuran shard atau tingkatkan heap JVM (`-Xmx` flag) |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menambahkan direktori baru setelah jaringan berjalan?**  
**A:** Ya—gunakan metode `indexer.addDirectories()`; acara yang berlangganan akan menyebarkan pembaruan secara waktu nyata.

**Q: Bagaimana cara memantau kesehatan node?**  
**A:** Setiap `SearchNetworkNode` menyediakan API status; integrasikan dengan alat pemantauan pilihan Anda.

**Q: Apakah memungkinkan menjalankan node master pada mesin terpisah?**  
**A:** Tentu saja. Pastikan semua node menggunakan `basePort` yang sama dan dapat terhubung satu sama lain melalui jaringan.

**Q: Format file apa yang didukung?**  
**A:** GroupDocs.Search mendukung PDF, Word, Excel, PowerPoint, teks biasa, dan banyak lainnya secara langsung.

**Q: Apakah saya perlu memulai ulang jaringan setelah menambahkan node baru?**  
**A:** Tidak—node dapat ditambahkan atau dihapus secara dinamis; node master akan menyeimbangkan kembali shard secara otomatis.

## Kesimpulan
Sekarang Anda telah mengetahui **cara mengonfigurasi pencarian** menggunakan GroupDocs.Search untuk Java, Anda dapat membangun solusi pencarian dokumen yang cepat, skalabel, dan handal yang mengikuti pertumbuhan organisasi Anda. Terapkan pola ini untuk menciptakan pengalaman pencarian terdistribusi dan waktu nyata untuk industri apa pun.

---

**Terakhir Diperbarui:** 2026-05-02  
**Diuji Dengan:** GroupDocs.Search for Java 25.4  
**Penulis:** GroupDocs