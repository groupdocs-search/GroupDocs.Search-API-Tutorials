---
date: '2026-02-27'
description: Pelajari cara membuat indeks yang dapat dicari dengan Java menggunakan
  GroupDocs.Search untuk Java, menambahkan file untuk pencarian, menambahkan direktori
  ke node, dan mengaktifkan pengindeksan waktu nyata dengan Java.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Buat Indeks Pencarian Java – Deploy GroupDocs.Search untuk Java
type: docs
url: /id/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Buat Indeks Pencarian Java – Deploy GroupDocs.Search untuk Java

Di dunia yang didorong oleh data saat ini, aplikasi **membuat indeks pencarian java** perlu menangani koleksi dokumen yang besar secara efisien. Baik Anda membangun layanan pencarian tingkat perusahaan atau proyek yang lebih kecil, jaringan pencarian yang terkonfigurasi dengan baik dapat secara dramatis meningkatkan kecepatan pengambilan dan relevansi. Dalam panduan ini kami akan membahas seluruh proses menyiapkan **GroupDocs.Search for Java**, mulai dari menambahkan file ke pencarian hingga menambahkan direktori ke node, sehingga Anda dapat mulai mengindeks dokumen Anda segera.

> **Mengapa ini penting:** Indeks pencarian mengurangi latensi kueri dari detik ke milidetik, skalabel dengan pertumbuhan data Anda, dan memungkinkan Anda menambahkan kemampuan teks penuh yang kuat ke solusi berbasis Java apa pun—baik itu portal web, aplikasi desktop, atau layanan mikro cloud.

## Jawaban Cepat
- **Apa tujuan utama GroupDocs.Search?** Ia menyediakan mesin berbasis Java yang skalabel untuk mengindeks dan mencari dokumen di seluruh jaringan terdistribusi.  
- **Versi mana yang harus saya gunakan?** Rilis stabil terbaru (mis., 25.4) direkomendasikan untuk proyek baru.  
- **Apakah saya memerlukan lisensi?** Tersedia percobaan gratis 30 hari; lisensi permanen diperlukan untuk penggunaan produksi.  
- **Bisakah saya menambahkan file dan seluruh direktori?** Ya – gunakan pembantu `addFiles` dan `addDirectories` untuk mengimpor konten.  
- **Versi Java apa yang diperlukan?** Java 8 atau lebih tinggi, dengan Maven untuk manajemen dependensi.  
- **Bagaimana cara kerja real time indexing java?** Dengan berlangganan ke acara node Anda dapat memicu re‑indeks otomatis saat file berubah.

## Apa itu “membuat indeks pencarian java”?
Membuat indeks pencarian dalam Java berarti membangun struktur data yang memetakan istilah ke dokumen yang memuatnya, memungkinkan kueri teks penuh yang cepat. GroupDocs.Search mengabstraksi pekerjaan berat, memungkinkan Anda fokus pada memasukkan dokumen dan menyesuaikan perilaku pencarian.

## Mengapa menggunakan GroupDocs.Search untuk Java?
- **Arsitektur jaringan yang skalabel** – Deploy beberapa node yang berbagi beban kerja pengindeksan.  
- **Dukungan format dokumen yang kaya** – PDF, Word, Excel, PowerPoint, gambar, dan lainnya.  
- **Pembaruan berbasis acara** – Berlangganan ke acara node untuk menjaga indeks tetap segar secara real time.  
- **Integrasi Maven yang sederhana** – Tambahkan beberapa baris ke `pom.xml` dan mulai mengindeks.

## Real time indexing java dengan GroupDocs.Search
GroupDocs.Search memicu acara setiap kali file ditambahkan, diperbarui, atau dihapus. Dengan menangani acara tersebut Anda dapat memanggil `addFiles` atau `addDirectories` secara otomatis, memastikan indeks tetap sinkron tanpa intervensi manual. Pendekatan ini ideal untuk sistem manajemen dokumen, portal konten, dan aplikasi apa pun di mana data sering berubah.

## Prasyarat
- **JDK 8+** terpasang di mesin pengembangan Anda.  
- Sebuah IDE seperti **IntelliJ IDEA** atau **Eclipse**.  
- Pengetahuan dasar tentang **Java** dan **Maven**.  
- Akses ke pustaka **GroupDocs.Search for Java** (unduh atau Maven).

## Menyiapkan GroupDocs.Search untuk Java

### Dependensi Maven
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

> **Tips pro:** Jaga nomor versi tetap terbaru dengan memeriksa halaman rilis resmi.

Anda juga dapat mengunduh JAR langsung dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Uji Coba Gratis:** evaluasi 30 hari.  
- **Lisensi Sementara:** Minta untuk pengujian yang diperpanjang.  
- **Pembelian:** Diperlukan untuk penyebaran produksi.

### Inisialisasi Dasar
Buat objek konfigurasi yang menunjuk ke folder tempat file indeks akan disimpan dan mendefinisikan port komunikasi dasar:

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

Di bawah ini kami merinci fitur inti yang Anda perlukan untuk **menambahkan file ke pencarian** dan **menambahkan direktori ke node**, sekaligus menyebarkan jaringan yang skalabel.

### Fitur 1 – Konfigurasi dan Penyiapan Jaringan
Mengonfigurasi jaringan pencarian adalah langkah pertama menuju pembuatan indeks pencarian.

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
Menyebarkan node mendistribusikan beban kerja pengindeksan di beberapa mesin atau proses.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Setiap `SearchNetworkNode` menjalankan layanan pengindeksan sendiri, memungkinkan Anda **membuat indeks pencarian java** yang skalabel secara horizontal.

### Fitur 3 – Berlangganan ke Acara Node
Pembaruan real‑time menjaga indeks tetap sinkron dengan perubahan sistem file.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Dengan mendengarkan acara, Anda dapat secara otomatis memicu re‑indeks ketika file baru tiba.

### Fitur 4 – Menambahkan Direktori ke Node Jaringan
Gunakan pembantu ini untuk **menambahkan direktori ke node**, mengumpulkan secara rekursif semua dokumen yang didukung.

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
Ketika Anda memerlukan kontrol yang lebih detail, **menambahkan file ke pencarian** secara individual:

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

## Kasus Penggunaan Umum
- **Portal dokumen perusahaan** yang membutuhkan pencarian instan di ribuan PDF dan file Office.  
- **Platform e‑discovery hukum** di mana bukti baru terus ditambahkan dan harus dapat dicari secara real time.  
- **Sistem manajemen konten** yang menyimpan gambar, presentasi, dan spreadsheet serta memerlukan pencarian teks penuh.

## Masalah Umum & Solusi
| Masalah | Alasan | Solusi |
|-------|--------|-----|
| **Tidak ada dokumen yang muncul dalam hasil pencarian** | Indeks belum dikomit | Panggil `node.getIndexer().commit()` setelah menambahkan file. |
| **Kesalahan konflik port** | Layanan lain menggunakan `basePort` | Pilih `basePort` yang berbeda atau verifikasi port yang bebas. |
| **Format file tidak didukung** | Pustaka tidak memiliki parser | Pastikan ekstensi file didukung atau tambahkan ekstraktor khusus. |

## Tips Pemecahan Masalah
- **Verifikasi kesehatan node:** Gunakan endpoint pemeriksaan kesehatan bawaan (`http://localhost:{port}/health`) untuk memastikan setiap node berjalan.  
- **Pantau penggunaan memori:** Batch dokumen besar dapat meningkatkan penggunaan memori; pertimbangkan mengindeks dalam potongan lebih kecil dan memanggil `commit()` secara berkala.  
- **Periksa log:** GroupDocs.Search menulis log terperinci ke folder `basePath`—tinjau untuk kesalahan parsing atau timeout jaringan.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan GroupDocs.Search pada aplikasi Java berbasis cloud?**  
A: Ya. Pustaka ini bekerja dengan runtime Java apa pun, dan Anda dapat mengarahkan `basePath` ke folder yang dipasang di jaringan atau penyimpanan cloud yang dipasang secara lokal.

**Q: Bagaimana cara memperbarui indeks ketika file berubah?**  
A: Berlangganan ke acara node (lihat Fitur 3) dan panggil `addFiles` atau `addDirectories` lagi untuk jalur yang dimodifikasi.

**Q: Apakah ada batasan jumlah node yang dapat saya deploy?**  
A: Secara praktis, batasannya ditentukan oleh perangkat keras dan bandwidth jaringan Anda. API itu sendiri tidak menetapkan batas keras.

**Q: Apakah saya perlu me-restart node setelah menambahkan file baru?**  
A: Tidak. Menambahkan file memicu pengindeksan secara otomatis; Anda hanya perlu melakukan commit jika menunda operasi.

**Q: Format dokumen apa yang didukung secara bawaan?**  
A: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, dan banyak tipe gambar. Lihat dokumen resmi untuk daftar lengkap.

**Q: Bagaimana saya dapat mengaktifkan real time indexing java untuk folder yang terus menerima unggahan?**  
A: Implementasikan pengawas sistem file (mis., `java.nio.file.WatchService`) yang memanggil `DirectoryAdder.addDirectories(node, path)` setiap kali file baru terdeteksi.

---

**Terakhir Diperbarui:** 2026-02-27  
**Diuji Dengan:** GroupDocs.Search for Java 25.4  
**Penulis:** GroupDocs