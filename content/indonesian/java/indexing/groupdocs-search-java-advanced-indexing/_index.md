---
date: '2025-12-29'
description: Pelajari cara mengoptimalkan kinerja pencarian menggunakan fitur pengindeksan
  lanjutan dari GroupDocs.Search untuk Java, termasuk pembatalan, operasi asinkron,
  multi‑threading, dan penyesuaian metadata.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: Optimalkan Kinerja Pencarian dengan Teknik Pengindeksan Lanjutan di GroupDocs.Search
  untuk Java
type: docs
url: /id/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Optimalkan Kinerja Pencarian dengan Teknik Pengindeksan Lanjutan di GroupDocs.Search untuk Java

Dalam lingkungan digital yang bergerak cepat saat ini, **mengoptimalkan kinerja pencarian** sangat penting untuk memberikan hasil instan kepada pengguna. Baik Anda membangun mesin pencari khusus maupun meningkatkan sistem manajemen dokumen yang ada, strategi pengindeksan yang tepat dapat secara dramatis mengurangi latensi dan konsumsi sumber daya. Dalam tutorial ini kami akan membahas fitur paling kuat dari GroupDocs.Search untuk Java—pembatalan, pengindeksan asinkron, multi‑threading, dan penyesuaian metadata—sehingga Anda dapat **add documents index** lebih cepat dan lebih efisien.

**Apa yang Akan Anda Pelajari**

- Cara membatalkan operasi pengindeksan setelah waktu tertentu
- Melakukan operasi pengindeksan asinkron dan menangani perubahan status
- Mengonfigurasi multi‑threading untuk pengindeksan yang lebih cepat
- Menyesuaikan opsi pengindeksan metadata

Pastikan Anda memiliki semua yang diperlukan sebelum kami menyelami kode.

## Prasyarat

- **GroupDocs.Search Library** – versi 25.4 atau lebih baru.  
- **Java Development Environment** – JDK 8 atau lebih tinggi disarankan.  
- Familiaritas dasar dengan Java dan konsep pengindeksan.

### Menyiapkan GroupDocs.Search untuk Java

#### Instalasi Maven

Tambahkan repositori dan dependensi ke file `pom.xml` Anda:

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

**License Acquisition** – Mulai dengan percobaan gratis atau minta lisensi sementara untuk membuka semua fitur.

### Inisialisasi dan Penyiapan Dasar

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

## Jawaban Cepat
- **What does cancellation do?** Menghentikan pengindeksan setelah waktu tertentu untuk membebaskan sumber daya.  
- **Can I index documents asynchronously?** Ya – atur `options.setAsync(true)`.  
- **How many threads can I use?** Bilangan bulat positif apa saja; nilai tipikal adalah 2‑4 untuk kebanyakan server.  
- **Is metadata indexing optional?** Tentu – Anda dapat mengaktifkan atau menyesuaikannya per bidang.  
- **Do I need a license for these features?** Versi percobaan berfungsi untuk pengujian; lisensi penuh diperlukan untuk produksi.

## Apa Itu “Optimalkan Kinerja Pencarian” dalam Konteks Ini?

Mengoptimalkan kinerja pencarian berarti mengonfigurasi proses pengindeksan sehingga mengonsumsi jumlah CPU, memori, dan waktu yang tepat sambil memberikan hasil paling relevan secara instan. Dengan mengendalikan pembatalan, eksekusi async, threading, dan penanganan metadata, Anda secara langsung memengaruhi seberapa cepat mesin dapat **add documents index** dan merespons kueri.

## Mengapa Menggunakan Fitur Pengindeksan Lanjutan?

- **Reduced latency** – Pengindeksan asinkron dan multi‑threaded menjaga aplikasi Anda tetap responsif.  
- **Better resource management** – Pembatalan mencegah proses yang tidak terkendali.  
- **Tailored search relevance** – Opsi metadata memungkinkan Anda menampilkan informasi terpenting.

## Panduan Implementasi

### Properti Pembatalan

**Overview** – Batalkan pengindeksan setelah durasi tertentu untuk menghindari konsumsi sumber daya berlebih.

#### Langkah 1: Siapkan Lingkungan

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: Buat Opsi Pengindeksan dengan Pembatalan

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

**Key Points**

- `setCancellation()` mengaktifkan fitur tersebut.  
- `cancelAfter(int milliseconds)` menentukan batas waktu (3 detik dalam contoh ini).

### Properti Asinkron

**Overview** –ankan pengindeksan pada thread latar belakang dan dengarkan perubahan status.

#### Langkah 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: Subscribe to Status Changed Event

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

#### Langkah 3: Configure Asynchronous Options

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Properti Thread

**Overview** – Mempercepat pengindeksan dengan memanfaatkan banyak core CPU.

#### Langkah 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: Configure Multi‑threading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Properti Opsi Pengindeksan Metadata

**Overview** – Menyesuaikan secara detail metadata dokumen mana yang diindeks dan bagaimana penyimpanannya.

#### Langkah 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: Configure Metadata Options

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

1. **Document Management Systems** – Gunakan pengindeksan asinkron untuk menjaga UI tetap responsif saat batch besar diproses di latar belakang.  
2. **Content Search Engines** – Terapkan pembatalan untuk mencegah pekerjaan yang berjalan lama menghabiskan sumber daya server selama lalu lintas puncak.  
3. **Large‑Scale Ingestion Pipelines** – Manfaatkan multi‑threading untuk **add documents index** secara skala besar, memotong waktu pemrosesan secara dramatis.

## Pertimbangan Kinerja

- **Thread Management** – Pantau penggunaan CPU; terlalu banyak thread dapat menyebabkan overhead pergantian konteks.  
- **Memory Footprint** – Batas metadata (mis., `setMaxBytesToIndexField`) membantu menjaga penggunaan memori tetap dapat diprediksi.  
- **Garbage Collection** – Gunakan flag JVM yang tepat (`-Xmx`, `-XX:+UseG1GC`) saat mengindeks korpus besar.

## Common Issues and Solutions

| Gejala | Kemungkinan Penyebab | Solusi |
|---------|----------------------|--------|
| Indexing never finishes | Cancellation set too low | Tingkatkan nilai `cancelAfter` atau hapus pembatalan untuk pekerjaan yang panjang |
| No status updates in async mode | Event handler not attached correctly | Pastikan `index.getEvents().StatusChanged.add(...)` dipanggil sebelum `index.add` |
| Out‑of‑memory errors | Too many threads or high metadata limits | Kurangi `options.setThreads` dan turunkan batas bidang metadata |
| Missing metadata in results | Metadata indexing disabled | Verifikasi `options.getMetadataIndexingOptions()` telah dikonfigurasi dan tidak diset untuk mengabaikan bidang |

## Pertanyaan yang Sering Diajukan

**Q: How do I obtain a temporary license for GroupDocs.Search?**  
A: Kunjungi [halaman lisensi sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q: Can I cancel an indexing operation midway through?**  
A: Ya – gunakan properti pembatalan dengan `cancelAfter()` atau panggil `Cancellation.cancel()` secara programatik.

**Q: What are some use cases for asynchronous indexing?**  
A: Pengambilan dokumen secara real‑time, pemrosesan batch di latar belakang, dan aplikasi yang responsif terhadap UI mendapat manfaat dari pengindeksan async.

**Q: Is it safe to increase the thread count on a shared server?**  
A: Tingkatkan secara bertahap dan pantau beban CPU; pada lingkungan yang sangat berbagi, pertahankan jumlah thread tetap wajar (2‑4).

**Q: How does metadata indexing affect search relevance?**  
A: Metadata yang diindeks dengan baik (penulis, tanggal pembuatan, tag) dapat diberi bobot lebih tinggi dalam kueri, meningkatkan akurasi hasil.

## Kesimpulan

Dengan memanfaatkan fitur lanjutan ini dari GroupDocs.Search untuk Java, Anda akan **mengoptimalkan kinerja pencarian** di berbagai skenario—dari ingest dokumen yang cepat hingga kontrol metadata yang detail. Bereksperimenlah dengan konfigurasi yang berbeda, pantau penggunaan sumber daya, dan sesuaikan pengaturan dengan beban kerja spesifik Anda untuk mendapatkan hasil terbaik.

---

**Terakhir Diperbarui:** 2025-12-29  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs