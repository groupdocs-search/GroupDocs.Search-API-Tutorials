---
date: '2026-01-03'
description: Pelajari cara menambahkan dokumen ke indeks dan membatalkan operasi penggabungan
  dalam Java menggunakan GroupDocs.Search. Panduan lengkap untuk manajemen dokumen
  Java.
keywords:
- document indexing in Java
- merging documents with GroupDocs
- GroupDocs.Search Java tutorial
title: Menambahkan dokumen ke indeks & menggabungkan dalam Java menggunakan GroupDocs.Search
type: docs
url: /id/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# Tambahkan dokumen ke indeks & gabungkan dalam Java menggunakan GroupDocs.Search

Dalam lingkungan digital yang bergerak cepat saat ini, mempelajari **cara menambahkan dokumen ke indeks** secara efisien sangat penting untuk solusi **document management java** apa pun. Baik Anda menangani kontrak, faktur, atau laporan internal, indeks yang terstruktur dengan baik memungkinkan Anda mengambil informasi dalam milidetik. Tutorial ini memandu Anda melalui pembuatan indeks, penambahan dokumen, konfigurasi opsi penggabungan, dan bahkan **membatalkan operasi penggabungan** jika diperlukan—semua dengan GroupDocs.Search untuk Java.

## Quick Answers
- **Apa arti “add documents to index”?** Itu memberi tahu GroupDocs.Search untuk memindai folder dan menyimpan metadata yang dapat dicari untuk setiap file.  
- **Bisakah saya menghentikan penggabungan yang lama?** Ya—gunakan objek `Cancellation` untuk **membatalkan operasi penggabungan** setelah batas waktu.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan gratis atau lisensi sementara dapat digunakan untuk pengujian; lisensi komersial membuka semua fitur.  
- **Versi Java apa yang diperlukan?** JDK 8 atau yang lebih baru.  
- **Apakah ini cocok untuk dataset besar?** Tentu—hanya perlu memantau memori dan menggunakan pengindeksan inkremental.

## Apa itu “add documents to index” dalam GroupDocs.Search?
Menambahkan dokumen ke indeks berarti memasukkan kumpulan file ke dalam GroupDocs.Search sehingga perpustakaan dapat menganalisis kontennya, mengekstrak token, dan membangun struktur data yang dapat dicari. Setelah diindeks, Anda dapat melakukan pencarian full‑text cepat di semua dokumen.

## Mengapa menggunakan GroupDocs.Search untuk document management java?
- **Pengindeksan skalabel** – Menangani ribuan file tanpa menurunkan kinerja.  
- **API kaya** – Menawarkan kontrol detail atas pengindeksan, penggabungan, dan pembatalan.  
- **Dukungan lintas format** – Bekerja dengan PDF, Word, Excel, dan banyak format lainnya secara langsung.  

## Prasyarat
- **GroupDocs.Search for Java** versi 25.4 atau lebih baru.  
- Maven (atau unduhan JAR manual).  
- Pengetahuan dasar Java dan lingkungan JDK 8+.

## Menyiapkan GroupDocs.Search untuk Java

### Instalasi Maven
Jika Anda mengelola dependensi dengan Maven, tambahkan repositori dan dependensi ke `pom.xml` Anda:

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

### Unduhan Langsung
Sebagai alternatif, unduh JAR terbaru dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Free Trial:** Daftar di situs GroupDocs untuk lisensi percobaan.  
- **Temporary License:** Ajukan kunci sementara jika Anda memerlukan evaluasi yang diperpanjang.  
- **Commercial License:** Beli untuk penggunaan produksi.

Setelah Anda memiliki file lisensi, letakkan di proyek Anda dan inisialisasi perpustakaan seperti yang ditunjukkan nanti.

## Panduan Implementasi

### Cara menambahkan dokumen ke indeks – Membuat Indeks Pertama
Pertama, buat indeks kosong yang akan menyimpan data yang dapat dicari.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Mengapa:** Langkah ini menyiapkan wadah penyimpanan tempat token yang diindeks akan disimpan.

#### Menambahkan dokumen ke indeks
Sekarang beri tahu GroupDocs.Search untuk memindai folder dan **menambahkan dokumen ke indeks**.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Mengapa:** Perpustakaan membaca setiap file, mengekstrak teks, dan menyimpannya di `index1`.

### Membuat indeks kedua untuk alur kerja fleksibel
Terkadang Anda memerlukan indeks terpisah—misalnya, untuk mengisolasi data klien.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Mengapa:** Beberapa indeks memungkinkan Anda mengelola kumpulan dokumen yang berbeda dan kemudian menggabungkannya.

### Cara mengonfigurasi opsi penggabungan dan membatalkan operasi penggabungan
Sebelum menggabungkan, Anda dapat menyetel proses secara detail dan bahkan menghentikannya jika berjalan terlalu lama.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Mengapa:** `Cancellation` memberi Anda kontrol untuk **membatalkan operasi penggabungan** secara otomatis, mencegah tugas yang tidak terkendali.

### Menggabungkan indeks
Akhirnya, gabungkan indeks sekunder ke dalam indeks utama.

```java
index1.merge(index2, options);
```

- **Mengapa:** Setelah pemanggilan ini, `index1` berisi semua dokumen dari kedua sumber, memberikan pengalaman pencarian yang terpadu.

## Aplikasi Praktis untuk Document Management Java
- **Firma hukum:** Mengkonsolidasikan berkas kasus dari banyak kantor.  
- **Institusi keuangan:** Menggabungkan laporan kuartalan ke dalam repositori yang dapat dicari tunggal.  
- **Perusahaan:** Menggabungkan dokumen HR, kepatuhan, dan kebijakan untuk pencarian di seluruh perusahaan.

## Pertimbangan Kinerja
- **Pengindeksan inkremental:** Tambahkan file baru secara berkala alih-alih membangun ulang seluruh indeks.  
- **Pemantauan memori:** Batch besar dapat mengonsumsi RAM; pertimbangkan pemrosesan dalam potongan lebih kecil.  
- **Garbage collection:** Lepaskan objek `Index` yang tidak terpakai dengan cepat untuk membebaskan sumber daya.

## Masalah Umum & Solusi

| Masalah | Solusi |
|-------|----------|
| **Path folder tidak benar** | Verifikasi path absolut dan pastikan aplikasi memiliki izin membaca. |
| **Memori tidak cukup** | Tingkatkan heap JVM (`-Xmx`) atau indeks file secara batch. |
| **Pembatalan tidak terpicu** | Pastikan `cancelAfter` diatur sebelum memanggil `merge`. |
| **Format file tidak didukung** | Instal plugin format tambahan dari GroupDocs jika diperlukan. |

## Pertanyaan yang Sering Diajukan

**Q:** *Mengapa saya membuat beberapa indeks alih-alih satu saja?*  
A: Indeks terpisah memungkinkan Anda mengisolasi domain data, menerapkan kebijakan keamanan yang berbeda, dan menggabungkan hanya ketika diperlukan, yang meningkatkan kinerja dan organisasi.

**Q:** *Bisakah saya membatalkan operasi pengindeksan dengan cara yang sama seperti membatalkan penggabungan?*  
A: Ya—gunakan objek `Cancellation` dengan metode `add` untuk menghentikan tugas pengindeksan yang berjalan lama.

**Q:** *Bagaimana saya memastikan kinerja optimal dengan koleksi dokumen yang sangat besar?*  
A: Lakukan pengindeksan inkremental, pantau memori JVM, dan pertimbangkan menggunakan penyimpanan SSD untuk direktori indeks.

**Q:** *Apa yang harus saya lakukan jika menerima error “Access denied”?*  
A: Periksa izin folder untuk pengguna yang menjalankan proses Java dan pastikan file lisensi dapat dibaca.

**Q:** *Apakah GroupDocs.Search kompatibel dengan pustaka GroupDocs lainnya?*  
A: Tentu—Anda dapat mengintegrasikannya dengan GroupDocs.Viewer, GroupDocs.Conversion, dll., untuk solusi dokumen full‑stack.

## Kesimpulan
Dengan mengikuti panduan ini Anda kini mengetahui cara **menambahkan dokumen ke indeks**, mengonfigurasi perilaku penggabungan, dan dengan aman **membatalkan operasi penggabungan** bila diperlukan—semua dalam alur kerja **document management java** yang kuat. Bereksperimenlah dengan dataset yang lebih besar, jelajahi tokenizer khusus, atau gabungkan GroupDocs.Search dengan produk GroupDocs lainnya untuk membangun solusi kelas perusahaan yang sesungguhnya.

## Sumber Daya
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License Application:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-01-03  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  
