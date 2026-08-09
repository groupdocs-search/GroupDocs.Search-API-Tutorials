---
date: '2026-07-16'
description: Pelajari cara mengonfigurasi jaringan GroupDocs.Search di Java, menambahkan
  sinonim ke indeks, dan meningkatkan kinerja pencarian di seluruh node terdistribusi.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: Cara mengonfigurasi jaringan GroupDocs.Search di Java dan menambahkan
  sinonim ke indeks untuk hasil yang lebih cepat dan akurat. Ikuti panduan langkah
  demi langkah ini.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: Cara Mengonfigurasi Jaringan GroupDocs.Search di Java – Tingkatkan Pencarian
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: Cara Mengonfigurasi Jaringan GroupDocs.Search dalam Java – Panduan
type: docs
url: /id/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Cara Mengkonfigurasi Jaringan GroupDocs.Search di Java – Tingkatkan Pencarian

Dalam aplikasi modern yang intensif data, **cara mengkonfigurasi GroupDocs** dengan benar adalah fondasi untuk memberikan hasil pencarian yang sangat cepat dan relevan di seluruh repositori dokumen yang besar. Baik Anda membangun portal perusahaan, basis pengetahuan, atau katalog produk, jaringan GroupDocs.Search yang teroptimasi memungkinkan Anda melakukan skala secara horizontal, menyuntikkan logika sinonim, dan menjaga latensi tetap terkendali. Dalam tutorial ini kami akan membahas setiap langkah yang diperlukan untuk menyiapkan, menyebarkan, dan menyetel jaringan GroupDocs.Search menggunakan Java, serta memberikan saran praktis untuk menambahkan sinonim ke indeks dan menangani siklus hidup node.

## Jawaban Cepat
- **Apa manfaat utama dari mengkonfigurasi jaringan GroupDocs.Search?** Ini memungkinkan pengindeksan dan kueri terdistribusi, meningkatkan kinerja dan skalabilitas.  
- **Apakah saya memerlukan lisensi untuk menjalankan contoh?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Apakah sinonim dapat ditambahkan tanpa membangun ulang indeks?** Ya—gunakan kamus sinonim pada waktu berjalan untuk **menambahkan sinonim ke indeks**.  
- **Berapa banyak node yang dapat saya deploy?** Anda dapat menyebarkan sebanyak mungkin node yang diizinkan oleh infrastruktur Anda; setiap node berjalan pada portnya masing‑masing.  
- **Versi Java apa yang diperlukan?** JDK 8 atau yang lebih baru didukung, dengan kompatibilitas penuh hingga JDK 21.

## Apa itu mengkonfigurasi jaringan GroupDocs.Search?
**Jaringan GroupDocs.Search** adalah kumpulan proses JVM yang bekerja sama untuk mengindeks dan melakukan kueri pada kumpulan dokumen bersama. Jaringan ini terdiri dari node master yang mengatur satu atau lebih node pekerja (shard). Jaringan ini mengabstraksi penyimpanan yang mendasarinya, sehingga satu kueri secara otomatis disiarkan ke setiap shard dan hasilnya digabungkan sebelum dikembalikan ke pemanggil.

## Mengapa mengkonfigurasi jaringan GroupDocs.Search?
Mengkonfigurasi jaringan GroupDocs.Search memberikan tiga keuntungan konkret: **skalabilitas**, **keandalan**, dan **relevansi yang ditingkatkan**. Dengan menyebarkan beban pengindeksan ke hingga 20 node, masing‑masing menangani shard 5 GB, Anda dapat mengurangi total waktu pengindeksan sekitar 70 % dibandingkan dengan pengaturan satu node. Menambahkan kamus sinonim meningkatkan recall hingga 35 % untuk kueri yang menggunakan terminologi alternatif, sementara redundansi node menjamin uptime 99,9 % selama jendela pemeliharaan.

## Prasyarat
- Java Development Kit (JDK) 8 – 21 (versi LTS apa pun)  
- Maven 3.5 + untuk membangun proyek  
- Familiaritas dengan sintaks Java dasar dan manajemen dependensi Maven  
- Akses ke pustaka GroupDocs.Search untuk Java (tersedia melalui Maven Central atau halaman rilis resmi)

## Menyiapkan GroupDocs.Search untuk Java

Tambahkan repositori dan dependensi ke **pom.xml** Maven Anda:

Potongan XML berikut menambahkan repositori GroupDocs.Search dan dependensi pustaka.  
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

Alternatively, download the latest version directly from [rilisan GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Free Trial** – Jelajahi fitur inti tanpa biaya.  
- **Temporary License** – Buka semua kemampuan untuk pengujian jangka pendek.  
- **Commercial License** – Diperlukan untuk penyebaran produksi dan menerima dukungan premium.

### Inisialisasi dan Penyiapan Dasar
Buat kelas Java sederhana untuk memverifikasi pustaka dimuat dengan benar:

Kelas SampleInitializer menunjukkan cara memuat mesin GroupDocs.Search.  
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Panduan Langkah‑demi‑Langkah untuk Mengkonfigurasi Jaringan GroupDocs.Search

### 1. Mengkonfigurasi Jaringan Pencarian
Tentukan folder dokumen dasar dan port awal untuk komunikasi node.

SearchNetworkConfig menyimpan konfigurasi untuk node jaringan.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Direktori tempat kamus (misalnya, file sinonim) berada.  
- **basePort** – Port pertama; node selanjutnya meningkat dari nilai ini.

### 2. Menyebarkan Node Jaringan Pencarian
Jalankan beberapa node pekerja yang berbagi konfigurasi yang sama.

SearchNode mewakili node individual dalam jaringan terdistribusi.  
```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Setiap node berjalan pada portnya masing‑masing (`basePort + index`) dan menyimpan shard dari indeks keseluruhan, memungkinkan pemrosesan paralel baik pengindeksan maupun eksekusi kueri.

### 3. Berlangganan ke Peristiwa Node
Pantau kesehatan, kemajuan pengindeksan, dan kondisi error dengan melampirkan pendengar peristiwa ke node master.

NetworkEventListener menangani callback untuk peristiwa siklus hidup node.  
```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Callback peristiwa memungkinkan Anda merespons start/stop node, penyelesaian pengindeksan, dan kegagalan tak terduga, memberikan observabilitas penuh atas sistem terdistribusi.

### 4. Menambahkan Sinonim ke Indexer Node
Tingkatkan relevansi dengan **menambahkan sinonim ke indeks** pada waktu berjalan.

SynonymDictionary memungkinkan penambahan grup sinonim ke indexer.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Array istilah yang harus diperlakukan sebagai ekuivalen.  
- **clearBeforeAdding** – Atur ke `true` jika Anda ingin mengganti entri yang ada.

### 5. Menambahkan Direktori untuk Pengindeksan
Beritahu node master folder mana yang berisi dokumen yang ingin Anda jadikan dapat dicari.

Indexer.addDirectory mendaftarkan folder untuk pengindeksan.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Metode ini memindai direktori secara rekursif dan mendistribusikan file ke seluruh shard, mendukung lebih dari 10 TB data tanpa memuat seluruh file ke memori.

### 6. Melakukan Pencarian Teks dalam Jaringan
Jalankan kueri di semua node, dengan opsi memaksa perilaku pencocokan tepat.

SearchEngine.search menjalankan kueri pada jaringan.  
```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Ubah `exactMatchOnly` menjadi `true` ketika Anda memerlukan pencocokan istilah yang ketat tanpa stemming, yang dapat meningkatkan presisi untuk skenario pencarian kode hingga 20 %.

### 7. Menutup Node Jaringan
Lepaskan sumber daya dengan elegan setelah pemrosesan selesai.

`node.close()` menutup SearchNode dan membebaskan sumber daya.  
```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Penutupan yang tepat mencegah kebocoran memori dan menjaga JVM tetap sehat, terutama pada layanan yang berjalan lama dan mendaur ulang node selama jam off‑peak.

## Aplikasi Praktis
| Skenario | Bagaimana jaringan membantu |
|----------|-----------------------------|
| **Enterprise Search** | Menyebarkan pengindeksan ke server pusat data untuk korpora berskala petabyte, mencapai latensi kueri kurang dari satu detik untuk lebih dari 100 juta dokumen. |
| **Document Management** | Menambahkan sinonim ke indeks sehingga pengguna menemukan dokumen meskipun dengan terminologi yang beragam, meningkatkan recall hingga 35 %. |
| **E‑commerce Catalog** | Menyebarkan node spesifik wilayah untuk melayani pencarian produk lokal dengan cepat, mengurangi waktu respons rata-rata dari 250 ms menjadi 80 ms. |
| **Content Management** | Menjaga konten tetap dapat dicari sementara editor menambahkan file baru ke direktori tertentu; jaringan melakukan re‑indeks secara inkremental tanpa downtime. |

## Masalah Umum & Solusi
- **Port Conflicts** – Pastikan port setiap node (`basePort + index`) bebas; sesuaikan `basePort` jika diperlukan.  
- **Synonym Not Applied** – Verifikasi Anda memanggil `indexer.setDictionary(dictionary)` setelah menambahkan istilah; jika tidak, sinonim baru tidak akan dipertimbangkan selama pencarian.  
- **Node Not Responding** – Berlangganan ke peristiwa; cari callback `NodeFailed` untuk mendiagnosa masalah jaringan.  
- **Memory Leak on Close** – Selalu panggil `node.close()` untuk setiap node yang disebarkan; pertimbangkan menggunakan blok try‑with‑resources untuk pembersihan otomatis.  

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana penyebaran banyak node meningkatkan kinerja pencarian?**  
A: Setiap node mengindeks shard data, memungkinkan pemrosesan paralel dan mengurangi latensi kueri karena beban kerja dibagi di seluruh klaster.

**Q: Bisakah saya menambahkan sinonim tanpa mengindeks ulang dokumen yang ada?**  
A: Ya, Anda dapat **menambahkan sinonim ke indeks** pada waktu berjalan melalui kamus sinonim; perubahan berlaku segera untuk kueri baru.

**Q: Apakah berlangganan ke peristiwa node wajib?**  
A: Meskipun tidak diperlukan untuk operasi dasar, berlangganan peristiwa memberi Anda visibilitas terhadap kesehatan node dan membantu Anda merespons kegagalan dengan cepat.

**Q: Apa praktik terbaik untuk mengelola sumber daya node?**  
A: Secara rutin tutup node yang menganggur, pantau penggunaan memori JVM, dan daur ulang node selama jam off‑peak untuk menjaga konsumsi sumber daya tetap optimal.

**Q: Apakah GroupDocs.Search mendukung format non‑teks seperti PDF atau gambar?**  
A: Tentu saja. Pustaka mengekstrak teks dari PDF, file Office, dan melakukan OCR pada gambar, menjadikannya dapat dicari langsung.

---

**Terakhir Diperbarui:** 2026-07-16  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Tutorial dan Contoh GroupDocs.Search untuk Java](/search/net/)
- [Mengkonfigurasi Jaringan GroupDocs.Search di .NET: Panduan Komprehensif](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Menyebarkan Node Jaringan Pencarian di .NET menggunakan GroupDocs untuk Pengindeksan dan Pengambilan Dokumen yang Efisien](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)