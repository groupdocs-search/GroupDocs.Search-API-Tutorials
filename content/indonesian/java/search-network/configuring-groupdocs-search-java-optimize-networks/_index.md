---
date: '2026-01-16'
description: Pelajari cara mengonfigurasi jaringan pencarian GroupDocs di Java dan
  menambahkan sinonim ke indeks untuk meningkatkan efisiensi pencarian.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Konfigurasi GroupDocs.Search Network di Java – Tingkatkan Pencarian
type: docs
url: /id/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Konfigurasi GroupDocs.Search Network di Java – Meningkatkan Pencarian

Dalam aplikasi yang didorong oleh data saat ini, **konfigurasi jaringan GroupDocs.Search** adalah langkah kunci untuk memberikan hasil yang cepat dan akurat pada koleksi dokumen yang sangat besar. Baik Anda membangun portal pencarian tingkat perusahaan atau memperluas solusi yang ada, jaringan GroupDocs.Search yang terkonfigurasi dengan baik memungkinkan Anda melakukan skala secara horizontal, menambahkan dukungan sinonim, dan menjaga latensi tetap rendah. Dalam tutorial ini Anda akan belajar cara menyiapkan, menyebarkan, dan menyempurnakan jaringan GroupDocs.Search menggunakan Java, serta tips praktis untuk menambahkan sinonim ke indeks dan mengelola siklus hidup node.

## Jawaban Cepat
- **Apa manfaat utama dari mengkonfigurasi jaringan GroupDocs.Search?** Ini memungkinkan pengindeksan dan kueri terdistribusi, meningkatkan kinerja dan skalabilitas.  
- **Apakah saya memerlukan lisensi untuk menjalankan contoh?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Apakah sinonim dapat ditambahkan tanpa membangun ulang indeks?** Ya—gunakan kamus sinonim pada waktu berjalan untuk **menambahkan sinonim ke indeks**.  
- **Berapa banyak node yang dapat saya deploy?** Anda dapat menyebarkan sebanyak mungkin node yang diizinkan oleh infrastruktur Anda; setiap node berjalan pada portnya masing‑masing.  

## Apa itu mengkonfigurasi jaringan GroupDocs.Search?
Mengkonfigurasi jaringan GroupDocs.Search berarti mendefinisikan struktur folder, port, dan pengaturan node yang memungkinkan beberapa instance JVM berkolaborasi dalam pengindeksan dan pencarian. Penyiapan ini membuat master‑node yang mengkoordinasikan pekerja (shard) dan memastikan kueri dijalankan di seluruh dataset.

## Mengapa mengkonfigurasi jaringan GroupDocs.Search?
- **Skalabilitas** – Membagi beban pengindeksan ke beberapa mesin.  
- **Reliabilitas** – Node dapat ditambahkan atau dihapus tanpa downtime.  
- **Relevansi pencarian** – Menambahkan sinonim ke indeks untuk hasil yang lebih kaya.  
- **Kinerja** – Eksekusi kueri paralel mengurangi waktu respons.

## Prasyarat
- Java Development Kit (JDK) 8 atau lebih baru  
- Maven untuk membangun proyek  
- Pemahaman dasar tentang sintaks Java  
- Akses ke pustaka GroupDocs.Search untuk Java (diunduh melalui Maven atau halaman rilis resmi)

## Menyiapkan GroupDocs.Search untuk Java

Tambahkan repositori dan dependensi ke **pom.xml** Maven Anda:

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

Atau, unduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Free Trial** – Jelajahi fitur inti tanpa biaya.  
- **Temporary License** – Membuka semua kemampuan untuk pengujian jangka pendek.  
- **Commercial License** – Diperlukan untuk penyebaran produksi.

### Inisialisasi dan Penyiapan Dasar
Buat kelas Java sederhana untuk memverifikasi pustaka dimuat dengan benar:

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

- **basePath** – Tempat kamus (misalnya file sinonim) berada.  
- **basePort** – Port pertama; node selanjutnya meningkat dari nilai ini.

### 2. Menyebarkan Node Jaringan Pencarian
Jalankan beberapa node pekerja yang berbagi konfigurasi yang sama.

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

Setiap node berjalan pada portnya masing‑masing (basePort + index) dan menyimpan shard dari indeks keseluruhan.

### 3. Berlangganan ke Event Node
Pantau kesehatan, kemajuan pengindeksan, dan kondisi error dengan melampirkan pendengar event ke master node.

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

Callback event memungkinkan Anda merespons start/stop node, penyelesaian pengindeksan, dan kegagalan tak terduga.

### 4. Menambahkan Sinonim ke Indexer Node  
Tingkatkan relevansi dengan **menambahkan sinonim ke indeks** pada waktu berjalan.

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
Beritahu master node folder mana yang berisi dokumen yang ingin Anda jadikan dapat dicari.

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

Metode ini memindai direktori secara rekursif dan mendistribusikan file ke seluruh shard.

### 6. Melakukan Pencarian Teks di Jaringan
Jalankan kueri di semua node, secara opsional memaksa perilaku exact‑match.

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

Ubah `exactMatchOnly` menjadi `true` ketika Anda memerlukan pencocokan istilah yang ketat tanpa stemming.

### 7. Menutup Node Jaringan
Lepaskan sumber daya secara elegan setelah pemrosesan selesai.

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

Penutupan yang tepat mencegah kebocoran memori dan menjaga JVM tetap sehat.

## Aplikasi Praktis
| Skenario | Bagaimana jaringan membantu |
|----------|-----------------------------|
| **Enterprise Search** | Distribusikan pengindeksan ke server data‑center untuk korpus berskala petabyte. |
| **Document Management** | Tambahkan sinonim ke indeks sehingga pengguna menemukan dokumen meskipun dengan terminologi yang berbeda. |
| **E‑commerce Catalog** | Sebarkan node spesifik wilayah untuk melayani pencarian produk terlokalisasi dengan cepat. |
| **Content Management** | Jaga konten tetap dapat dicari sementara editor menambahkan file baru ke direktori tertentu. |

## Masalah Umum & Solusi
- **Port Conflicts** – Pastikan port setiap node (basePort + index) bebas; sesuaikan `basePort` jika diperlukan.  
- **Synonym Not Applied** – Verifikasi Anda memanggil `indexer.setDictionary(dictionary)` setelah menambahkan istilah.  
- **Node Not Responding** – Berlangganan ke event; cari callback `NodeFailed` untuk mendiagnosa masalah jaringan.  
- **Memory Leak on Close** – Selalu panggil `node.close()` untuk setiap node yang disebarkan.

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana penyebaran banyak node meningkatkan kinerja pencarian?**  
A: Setiap node mengindeks shard data, memungkinkan pemrosesan paralel dan mengurangi latensi kueri karena beban kerja dibagi.

**Q: Bisakah saya menambahkan sinonim tanpa mengindeks ulang dokumen yang ada?**  
A: Ya, Anda dapat **menambahkan sinonim ke indeks** pada waktu berjalan melalui kamus sinonim; perubahan berlaku segera untuk kueri baru.

**Q: Apakah berlangganan ke event node wajib?**  
A: Meskipun tidak diperlukan untuk operasi dasar, berlangganan ke event memberi Anda visibilitas terhadap kesehatan node dan membantu Anda merespons kegagalan dengan cepat.

**Q: Apa praktik terbaik untuk mengelola sumber daya node?**  
A: Secara rutin tutup node yang tidak aktif, pantau penggunaan memori JVM, dan daur ulang node selama jam off‑peak untuk menjaga konsumsi sumber daya optimal.

**Q: Apakah GroupDocs.Search mendukung format non‑teks seperti PDF atau gambar?**  
A: Tentu saja. Pustaka ini mengekstrak teks dari PDF, file Office, dan bahkan melakukan OCR pada gambar, sehingga dapat dicari langsung.

---

**Terakhir Diperbarui:** 2026-01-16  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs