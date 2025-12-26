---
date: '2025-12-26'
description: Pelajari cara membuat indeks pencarian Java dengan GroupDocs.Search untuk
  Java, menambahkan file untuk pencarian, dan menambahkan direktori ke node.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Buat Indeks Pencarian Java – Deploy GroupDocs.Search untuk Java
type: docs
url: /id/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Buat Indeks Pencarian Java – Menyebarkan GroupDocs.Search for Java

Di dunia yang didorong oleh data saat ini, aplikasi **membuat indeks pencarian java** perlu menangani koleksi dokumen yang masif secara efisien. Baik Anda membangun layanan pencarian tingkat perusahaan maupun proyek yang lebih kecil, jaringan pencarian yang terkonfigurasi dengan baik dapat secara dramatis meningkatkan kecepatan pengambilan dan relevansi. Dalam panduan ini kami akan membahas seluruh proses menyiapkan **GroupDocs.Search for Java**, mulai dari menambahkan file ke pencarian hingga menambahkan direktori ke node, sehingga Anda dapat mulai mengindeks dokumen Anda segera.

## Jawaban Cepat
- **Apa tujuan utama GroupDocs.Search?** Ia menyediakan mesin berbasis Java yang skalabel untuk mengindeks dan mencari dokumen di seluruh jaringan terdistribusi.  
- **Versi mana yang harus saya gunakan?** Rilis stabil terbaru (mis., 25.4) direkomendasikan untuk proyek baru.  
- **Apakah saya memerlukan lisensi?** Tersedia percobaan gratis 30 hari; lisensi permanen diperlukan untuk penggunaan produksi.  
- **Bisakah saya menambahkan file dan seluruh direktori?** Ya – gunakan pembantu `addFiles` dan `addDirectories` untuk memasukkan konten.  
- **Versi Java apa yang dibutuhkan?** Java 8 atau lebih tinggi, dengan Maven untuk manajemen dependensi.

## Apa itu “membuat indeks pencarian java”?
Membuat indeks pencarian dalam Java berarti membangun struktur data yang memetakan istilah ke dokumen yang mengandungnya, memungkinkan kueri teks penuh yang cepat. GroupDocs.Search mengabstraksi pekerjaan berat, memungkinkan Anda fokus pada memasukkan dokumen dan menyesuaikan perilaku pencarian.

## Mengapa menggunakan GroupDocs.Search for Java?
- **Arsitektur jaringan yang skalabel** – Menyebarkan beberapa node yang berbagi beban kerja pengindeksan.  
- **Dukungan format dokumen yang kaya** – PDF, Word, Excel, PowerPoint, gambar, dan lainnya.  
- **Pembaruan berbasis peristiwa** – Berlangganan ke peristiwa node untuk menjaga indeks tetap segar secara real time.  
- **Integrasi Maven yang sederhana** – Tambahkan beberapa baris ke `pom.xml` dan mulai mengindeks.

## Prasyarat
- **JDK 8+** terpasang di mesin pengembangan Anda.  
- IDE seperti **IntelliJ IDEA** atau **Eclipse**.  
- Pengetahuan dasar tentang **Java** dan **Maven**.  
- Akses ke perpustakaan **GroupDocs.Search for Java** (unduh atau Maven).

## Menyiapkan GroupDocs.Search for Java

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

> **Tip Pro:** Jaga nomor versi tetap terbaru dengan memeriksa halaman rilis resmi.

Anda juga dapat mengunduh JAR secara langsung dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Percobaan Gratis:** evaluasi 30 hari.  
- **Lisensi Sementara:** Minta untuk pengujian yang diperpanjang.  
- **Pembelian:** Diperlukan untuk penyebaran produksi.

### Inisialisasi Dasar
Create a configuration object that points to a folder where index files will be stored and defines the base communication port:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## Cara membuat indeks pencarian java dengan GroupDocs.Search?

Di bawah ini kami menjabarkan fitur inti yang Anda perlukan untuk **menambahkan file ke pencarian** dan **menambahkan direktori ke node**, sambil juga menyebarkan jaringan yang skalabel.

### Fitur 1 – Konfigurasi dan Penyiapan Jaringan
Configuring the search network is the first step toward building a searchable index.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – Direktori tempat data indeks akan disimpan.  
- **`basePort`** – Port awal; setiap node akan meningkat dari nilai ini.

### Fitur 2 – Menyebarkan Node Jaringan Pencarian
Deploying nodes distributes indexing workload across multiple machines or processes.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Setiap `SearchNetworkNode` menjalankan layanan pengindeksan sendiri, memungkinkan Anda **membuat indeks pencarian java** yang dapat diskalakan secara horizontal.

### Fitur 3 – Berlangganan ke Peristiwa Node
Real‑time updates keep the index synchronized with file system changes.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Dengan mendengarkan peristiwa, Anda dapat secara otomatis memicu pengindeksan ulang ketika file baru tiba.

### Fitur 4 – Menambahkan Direktori ke Node Jaringan
Use this helper to **add directories to node**, recursively collecting all supported documents.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### Fitur 5 – Menambahkan File ke Node Jaringan
When you need fine‑grained control, **add files to search** individually:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Metode ini memberi Anda fleksibilitas untuk mengindeks file yang berasal dari aliran, penyimpanan cloud, atau lokasi sementara.

## Masalah Umum & Solusi
| Masalah | Alasan | Solusi |
|-------|--------|-----|
| **Tidak ada dokumen yang muncul dalam hasil pencarian** | Indeks belum dikomit | Panggil `node.getIndexer().commit()` setelah menambahkan file. |
| **Kesalahan konflik port** | Layanan lain menggunakan `basePort` | Pilih `basePort` yang berbeda atau verifikasi port yang bebas. |
| **Format file tidak didukung** | Perpustakaan tidak memiliki parser | Pastikan ekstensi file didukung atau tambahkan ekstraktor khusus. |

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menggunakan GroupDocs.Search pada aplikasi Java berbasis cloud?**  
J: Ya. Perpustakaan ini bekerja dengan runtime Java apa pun, dan Anda dapat mengarahkan `basePath` ke folder yang dipasang di jaringan atau penyimpanan cloud yang dipasang secara lokal.

**T: Bagaimana cara memperbarui indeks ketika sebuah file berubah?**  
J: Berlangganan ke peristiwa node (lihat Fitur 3) dan panggil `addFiles` atau `addDirectories` lagi untuk jalur yang dimodifikasi.

**T: Apakah ada batasan jumlah node yang dapat saya sebarkan?**  
J: Secara praktis, batasannya ditentukan oleh perangkat keras dan bandwidth jaringan Anda. API itu sendiri tidak memberlakukan batasan keras.

**T: Apakah saya perlu memulai ulang node setelah menambahkan file baru?**  
J: Tidak. Menambahkan file memicu pengindeksan secara otomatis; Anda hanya perlu mengkomit jika menunda operasi.

**T: Format dokumen apa yang didukung secara bawaan?**  
J: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, dan banyak tipe gambar. Lihat dokumentasi resmi untuk daftar lengkap.

---

**Terakhir Diperbarui:** 2025-12-26  
**Diuji Dengan:** GroupDocs.Search for Java 25.4  
**Penulis:** GroupDocs