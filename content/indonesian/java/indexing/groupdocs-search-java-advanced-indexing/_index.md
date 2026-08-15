---
date: '2026-08-15'
description: Pelajari cara meningkatkan latensi pencarian menggunakan fitur pengindeksan
  lanjutan dari GroupDocs.Search for Java, termasuk pembatalan, operasi async, multithreading,
  dan penyesuaian metadata.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Meningkatkan latensi pencarian dengan GroupDocs.Search for Java dengan
  menggunakan pembatalan, pengindeksan asynchronous, multithreading, dan penyesuaian
  metadata. Tingkatkan kinerja dan kurangi penggunaan sumber daya.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Meningkatkan latensi pencarian dengan pengindeksan lanjutan di GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Meningkatkan latensi pencarian dengan pengindeksan lanjutan di GroupDocs
type: docs
url: /id/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Tingkatkan latensi pencarian dengan pengindeksan lanjutan di GroupDocs

Dalam lingkungan digital yang bergerak cepat saat ini, **meningkatkan latensi pencarian** sangat penting untuk memberikan hasil instan kepada pengguna. Apakah Anda membangun mesin pencari khusus atau meningkatkan sistem manajemen dokumen yang ada, strategi pengindeksan yang tepat dapat secara dramatis mengurangi latensi, menurunkan konsumsi sumber daya, dan **meningkatkan latensi pencarian** secara keseluruhan. Dalam tutorial ini kami akan membahas fitur paling kuat dari GroupDocs.Search untuk Java—pembatalan, pengindeksan asinkron, multithreading, dan penyesuaian metadata—sehingga Anda dapat **menambahkan dokumen ke indeks** lebih cepat dan lebih efisien.

**Apa yang akan Anda pelajari**

- Cara membatalkan operasi pengindeksan setelah waktu tertentu  
- Melakukan operasi pengindeksan asinkron dan menangani perubahan status  
- Mengonfigurasi multithreading untuk pengindeksan yang lebih cepat  
- Menyesuaikan opsi pengindeksan metadata untuk **menyesuaikan metadata pencarian**  

Pastikan Anda memiliki semua yang diperlukan sebelum kami menyelami kode.

## Jawaban Cepat
- **Apa yang dilakukan pembatalan?** Itu menghentikan pengindeksan setelah batas waktu tertentu, membebaskan CPU dan memori untuk tugas lain.  
- **Bisakah saya mengindeks dokumen secara asinkron?** Ya – aktifkan dengan `options.setAsync(true)`.  
- **Berapa banyak thread yang dapat saya gunakan?** Bilangan bulat positif apa saja; 2‑4 thread biasanya untuk kebanyakan server.  
- **Apakah pengindeksan metadata opsional?** Tentu – Anda dapat mengaktifkan atau menyesuaikannya per bidang.  
- **Apakah saya memerlukan lisensi untuk fitur ini?** Versi percobaan cukup untuk pengujian; lisensi penuh diperlukan untuk produksi.

## Prasyarat

- **GroupDocs.Search library** – versi 25.4 atau lebih baru.  
- **Java Development Environment** – JDK 8 atau lebih tinggi disarankan.  
- Familiaritas dasar dengan Java dan konsep pengindeksan.

### Menyiapkan GroupDocs.Search untuk Java

#### Instalasi Maven

Tambahkan repositori dan dependensi ke file `pom.xml` Anda:

`pom.xml` configuration tells Maven which GroupDocs.Search artifacts to download and include in your project.

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

#### Unduhan Langsung

Sebagai alternatif, unduh JAR terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License acquisition** – Mulailah dengan percobaan gratis atau minta lisensi sementara untuk membuka semua fitur.

### Inisialisasi dan Penyiapan Dasar

Kelas `SearchIndex` adalah titik masuk yang mewakili indeks yang dapat dicari yang disimpan di disk atau di memori.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Apa itu “optimalkan kinerja pencarian” dalam konteks ini?

Mengoptimalkan kinerja pencarian berarti mengonfigurasi proses pengindeksan sehingga mengonsumsi jumlah CPU, memori, dan waktu yang tepat sambil memberikan hasil paling relevan secara instan. Dengan mengendalikan pembatalan, eksekusi async, threading, dan penanganan metadata, Anda secara langsung memengaruhi seberapa cepat mesin dapat **menambahkan dokumen ke indeks** dan merespons kueri.

## Mengapa menggunakan fitur pengindeksan lanjutan?

Pengindeksan asinkron dan multithreaded menjaga aplikasi tetap responsif, sementara pembatalan mencegah proses yang berjalan lama. Opsi metadata yang disesuaikan memungkinkan Anda menampilkan informasi terpenting, yang secara langsung **meningkatkan latensi pencarian** bagi pengguna akhir. Selain itu, fitur-fitur ini mengurangi lonjakan CPU, menurunkan tekanan memori, dan memungkinkan penskalaan yang lebih mulus saat menangani volume dokumen besar.

## Bagaimana cara meningkatkan latensi pencarian dengan pengindeksan lanjutan?

Muat instance `SearchIndex` Anda, konfigurasikan `IndexingOptions` dengan pengaturan pembatalan, async, dan thread, lalu panggil `index.add(document)` — kombinasi ini mengurangi waktu pengindeksan keseluruhan hingga 60 % pada beban kerja tipikal dan menjamin pekerjaan yang berjalan lama tidak memblokir operasi lain. Anda juga dapat menyesuaikan batas pengindeksan metadata dan memantau kemajuan melalui event status‑changed untuk memastikan pipeline tetap dalam batas anggaran kinerja.

## Panduan Implementasi

### Properti Pembatalan

**Overview** – Batalkan pengindeksan setelah durasi tertentu untuk menghindari konsumsi sumber daya berlebih.

#### Langkah 1: siapkan lingkungan

Buat instance `SearchIndex` yang menunjuk ke folder indeks Anda.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: buat opsi pengindeksan dengan pembatalan

`IndexingOptions` memungkinkan Anda menentukan perilaku mesin pengindeksan.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Poin penting**

- `setCancellation()` mengaktifkan fitur.  
- `cancelAfter(int milliseconds)` menentukan batas waktu (3 detik dalam contoh ini).

### Properti Asinkron

**Overview** – Jalankan pengindeksan pada thread latar belakang dan dengarkan perubahan status.

#### Langkah 1: siapkan lingkungan

Instansiasi indeks dan siapkan koleksi dokumen.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: berlangganan ke acara status‑changed

Event `StatusChanged` memberi tahu Anda ketika pekerjaan pengindeksan berpindah antar status.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Langkah 3: konfigurasikan opsi asinkron

Aktifkan mode async sehingga panggilan mengembalikan segera dan pemrosesan berlanjut di latar belakang.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Properti Thread

**Overview** – Percepat pengindeksan dengan memanfaatkan banyak core CPU.

#### Langkah 1: siapkan lingkungan

Siapkan indeks dan pastikan JVM memiliki memori heap yang cukup.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: konfigurasikan multithreading

Atur jumlah thread pekerja; setiap thread memproses subset dokumen.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Properti Opsi Pengindeksan Metadata

**Overview** – Sesuaikan secara halus metadata dokumen mana yang diindeks dan bagaimana penyimpanannya.

#### Langkah 1: siapkan lingkungan

Muat dokumen yang berisi bidang metadata seperti penulis, judul, dan tag khusus.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: konfigurasikan opsi metadata

`MetadataIndexingOptions` memungkinkan Anda mengaktifkan atau menonaktifkan bidang metadata individual dan menentukan batas ukuran.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Aplikasi Praktis

1. **Sistem manajemen dokumen** – Gunakan pengindeksan asinkron untuk menjaga UI tetap responsif sementara batch besar diproses di latar belakang.  
2. **Mesin pencari konten** – Terapkan pembatalan untuk mencegah pekerjaan yang berjalan lama menyedot sumber daya server selama puncak lalu lintas.  
3. **Pipeline ingest skala besar** – Manfaatkan multithreading untuk **menambahkan dokumen ke indeks** secara masif, memotong waktu pemrosesan secara dramatis.  

## Pertimbangan Kinerja

- **Manajemen thread** – Pantau penggunaan CPU; terlalu banyak thread dapat menyebabkan overhead pergantian konteks.  
- **Jejak memori** – Batas metadata (mis., `setMaxBytesToIndexField`) menjaga penggunaan memori tetap dapat diprediksi.  
- **Garbage collection** – Gunakan flag JVM yang tepat (`-Xmx`, `-XX:+UseG1GC`) saat mengindeks korpus yang sangat besar.  

## Masalah Umum dan Solusinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Pengindeksan tidak pernah selesai | Pembatalan diatur terlalu rendah | Tingkatkan nilai `cancelAfter` atau hapus pembatalan untuk pekerjaan yang lama |
| Tidak ada pembaruan status dalam mode async | Penangkap acara tidak terpasang dengan benar | Pastikan `index.getEvents().StatusChanged.add(...)` dipanggil sebelum `index.add` |
| Kesalahan kehabisan memori | Terlalu banyak thread atau batas metadata tinggi | Kurangi `options.setThreads` dan turunkan batas bidang metadata |
| Metadata hilang dalam hasil | Pengindeksan metadata dinonaktifkan | Verifikasi `options.getMetadataIndexingOptions()` telah dikonfigurasi dan tidak diatur untuk mengabaikan bidang |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Search?**  
J: Kunjungi [halaman lisensi sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/) dan ikuti instruksi di layar.

**T: Bisakah saya membatalkan operasi pengindeksan di tengah jalan?**  
J: Ya – gunakan properti pembatalan dengan `cancelAfter()` atau panggil `Cancellation.cancel()` secara programatik.

**T: Apa saja contoh penggunaan pengindeksan asinkron?**  
J: Pengambilan dokumen real‑time, pemrosesan batch latar belakang, dan aplikasi yang memerlukan UI responsif mendapat manfaat dari pengindeksan async.

**T: Apakah aman meningkatkan jumlah thread pada server bersama?**  
J: Tingkatkan secara bertahap dan pantau beban CPU; pada lingkungan yang sangat berbagi, pertahankan jumlah thread yang wajar (2‑4).

**T: Bagaimana pengindeksan metadata memengaruhi relevansi pencarian?**  
J: Metadata yang diindeks dengan baik (penulis, tanggal pembuatan, tag) dapat diberi bobot lebih tinggi dalam kueri, meningkatkan akurasi hasil.

## Kesimpulan

Dengan memanfaatkan fitur lanjutan dari GroupDocs.Search untuk Java, Anda akan **meningkatkan latensi pencarian** dalam berbagai skenario—dari ingest dokumen cepat hingga kontrol metadata yang halus. Bereksperimenlah dengan konfigurasi berbeda, pantau penggunaan sumber daya, dan sesuaikan pengaturan dengan beban kerja spesifik Anda untuk mendapatkan hasil terbaik.

---

**Last Updated:** 2026-08-15  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Tutorial Terkait

- [Meningkatkan Kinerja Kuiri dengan GroupDocs.Search Java: Optimalkan Indeks & Pencarian](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Cara menambahkan dokumen ke indeks dengan Pengindeksan Metadata di Java menggunakan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Cara Menambahkan Beberapa Alias dan Menambahkan Dokumen ke Indeks di GroupDocs.Search untuk Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)