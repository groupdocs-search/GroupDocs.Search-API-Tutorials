---
date: '2026-03-01'
description: Pelajari cara mengoptimalkan kinerja pencarian dan meningkatkan latensi
  pencarian menggunakan fitur pengindeksan lanjutan dari GroupDocs.Search untuk Java,
  termasuk pembatalan, operasi asinkron, multithreading, dan penyesuaian metadata.
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

Dalam lingkungan digital yang bergerak cepat saat ini, **optimalkan kinerja pencarian** sangat penting untuk memberikan hasil instan kepada pengguna. Baik Anda membangun mesin pencari khusus maupun meningkatkan sistem manajemen dokumen yang ada, strategi pengindeksan yang tepat dapat secara dramatis mengurangi latensi, menurunkan konsumsi sumber daya, dan **meningkatkan latensi pencarian** secara keseluruhan. Dalam tutorial ini kami akan membahas fitur paling kuat dari GroupDocs.Search untuk Java—pembatalan, pengindeksan asinkron, multi‑threading, dan penyesuaian metadata—sehingga Anda dapat **menambahkan dokumen ke indeks** lebih cepat dan lebih efisien.

**Apa yang Akan Anda Pelajari**

- Cara membatalkan operasi pengindeksan setelah waktu tertentu  
- Melakukan operasi pengindeksan asinkron dan menangani perubahan status  
- Mengonfigurasi multi‑threading untuk pengindeksan yang lebih cepat  
- Menyesuaikan opsi pengindeksan metadata  

Mari pastikan Anda memiliki semua yang diperlukan sebelum kita menyelam ke dalam kode.

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

Atau, unduh JAR terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Perolehan Lisensi** – Mulai dengan percobaan gratis atau minta lisensi sementara untuk membuka semua fitur.

### Inisialisasi dan Pengaturan Dasar

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
- **Apa yang dilakukan pembatalan?** Menghentikan pengindeksan setelah waktu tertentu untuk membebaskan sumber daya.  
- **Bisakah saya mengindeks dokumen secara asinkron?** Ya – setel `options.setAsync(true)`.  
- **Berapa banyak thread yang dapat saya gunakan?** Bilangan bulat positif apa saja; nilai tipikal 2‑4 untuk kebanyakan server.  
- **Apakah pengindeksan metadata opsional?** Tentu – Anda dapat mengaktifkan atau menyesuaikannya per bidang.  
- **Apakah saya memerlukan lisensi untuk fitur ini?** Versi percobaan cukup untuk pengujian; lisensi penuh diperlukan untuk produksi.

## Apa Itu “Optimalkan Kinerja Pencarian” dalam Konteks Ini?

Mengoptimalkan kinerja pencarian berarti mengonfigurasi proses pengindeksan sehingga mengonsumsi jumlah CPU, memori, dan waktu yang tepat sambil memberikan hasil paling relevan secara instan. Dengan mengendalikan pembatalan, eksekusi async, threading, dan penanganan metadata, Anda secara langsung memengaruhi seberapa cepat mesin dapat **menambahkan dokumen ke indeks** dan merespons kueri.

## Mengapa Menggunakan Fitur Pengindeksan Lanjutan?

- **Mengurangi latensi** – Pengindeksan asinkron dan multi‑threaded menjaga aplikasi tetap responsif.  
- **Manajemen sumber daya yang lebih baik** – Pembatalan mencegah proses berjalan tak terkendali.  
- **Relevansi pencarian yang disesuaikan** – Opsi metadata memungkinkan Anda menampilkan informasi terpenting.  

## Bagaimana cara meningkatkan latensi pencarian dengan pengindeksan lanjutan?

Saat Anda perlu **meningkatkan latensi pencarian**, pertimbangkan menggabungkan fitur-fitur yang akan kami bahas: batalkan pekerjaan yang berjalan lama, jalankan pengindeksan di latar belakang, dan sebarkan pekerjaan ke beberapa inti CPU. Pendekatan multi‑pronged ini biasanya menghasilkan peningkatan kecepatan terbesar.

## Panduan Implementasi

### Properti Pembatalan

**Gambaran Umum** – Batalkan pengindeksan setelah durasi tertentu untuk menghindari konsumsi sumber daya berlebih.

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

**Poin Penting**

- `setCancellation()` mengaktifkan fitur.  
- `cancelAfter(int milliseconds)` menentukan batas waktu (3 detik dalam contoh ini).

### Properti Asinkron

**Gambaran Umum** – Jalankan pengindeksan pada thread latar belakang dan dengarkan perubahan status.

#### Langkah 1: Siapkan Lingkungan

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: Langganan ke Event Status Changed

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

#### Langkah 3: Konfigurasikan Opsi Asinkron

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Properti Thread

**Gambaran Umum** – Mempercepat pengindeksan dengan memanfaatkan beberapa inti CPU.

#### Langkah 1: Siapkan Lingkungan

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: Konfigurasikan Multi‑threading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Properti Opsi Pengindeksan Metadata

**Gambaran Umum** – Menyesuaikan metadata dokumen mana yang diindeks dan bagaimana penyimpanannya.

#### Langkah 1: Siapkan Lingkungan

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Langkah 2: Konfigurasikan Opsi Metadata

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

1. **Sistem Manajemen Dokumen** – Gunakan pengindeksan asinkron untuk menjaga UI tetap responsif saat batch besar diproses di latar belakang.  
2. **Mesin Pencari Konten** – Terapkan pembatalan untuk mencegah pekerjaan lama menghabiskan sumber daya server selama puncak trafik.  
3. **Pipeline Ingesti Skala Besar** – Manfaatkan multi‑threading untuk **menambahkan dokumen ke indeks** secara masif, memotong waktu pemrosesan secara dramatis.

## Pertimbangan Kinerja

- **Manajemen Thread** – Pantau penggunaan CPU; terlalu banyak thread dapat menyebabkan overhead pergantian konteks.  
- **Jejak Memori** – Batas metadata (misalnya `setMaxBytesToIndexField`) membantu menjaga penggunaan memori tetap dapat diprediksi.  
- **Garbage Collection** – Gunakan flag JVM yang tepat (`-Xmx`, `-XX:+UseG1GC`) saat mengindeks korpus besar.

## Masalah Umum dan Solusinya

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| Pengindeksan tidak pernah selesai | Pembatalan diatur terlalu rendah | Tingkatkan nilai `cancelAfter` atau hapus pembatalan untuk pekerjaan panjang |
| Tidak ada pembaruan status dalam mode async | Event handler tidak terpasang dengan benar | Pastikan `index.getEvents().StatusChanged.add(...)` dipanggil sebelum `index.add` |
| Kesalahan out‑of‑memory | Terlalu banyak thread atau batas metadata tinggi | Kurangi `options.setThreads` dan turunkan batas bidang metadata |
| Metadata tidak muncul dalam hasil | Pengindeksan metadata dinonaktifkan | Verifikasi `options.getMetadataIndexingOptions()` telah dikonfigurasi dan tidak diatur untuk mengabaikan bidang |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Search?**  
J: Kunjungi [halaman lisensi sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**T: Bisakah saya membatalkan operasi pengindeksan di tengah jalan?**  
J: Ya – gunakan properti pembatalan dengan `cancelAfter()` atau panggil `Cancellation.cancel()` secara programatik.

**T: Apa saja kasus penggunaan untuk pengindeksan asinkron?**  
J: Pengambilan dokumen real‑time, pemrosesan batch di latar belakang, dan aplikasi yang memerlukan UI responsif mendapat manfaat dari pengindeksan async.

**T: Apakah aman meningkatkan jumlah thread pada server bersama?**  
J: Tingkatkan secara bertahap dan pantau beban CPU; pada lingkungan yang sangat berbagi, pertahankan jumlah thread yang wajar (2‑4).

**T: Bagaimana pengindeksan metadata memengaruhi relevansi pencarian?**  
J: Metadata yang diindeks dengan baik (penulis, tanggal pembuatan, tag) dapat diberi bobot lebih tinggi dalam kueri, meningkatkan akurasi hasil.

## Kesimpulan

Dengan memanfaatkan fitur lanjutan dari GroupDocs.Search untuk Java, Anda akan **mengoptimalkan kinerja pencarian** dalam berbagai skenario—dari ingesti dokumen cepat hingga kontrol metadata yang detail. Bereksperimenlah dengan konfigurasi berbeda, pantau penggunaan sumber daya, dan sesuaikan pengaturan sesuai beban kerja spesifik Anda untuk mendapatkan hasil terbaik.

---

**Terakhir Diperbarui:** 2026-03-01  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs  

---