---
date: '2026-05-12'
description: 'Pelajari pencarian teks lengkap java dengan GroupDocs.Search: tambahkan
  dokumen ke indeks, konfigurasikan opsi penggabungan, dan batalkan operasi penggabungan.
  Ideal untuk solusi manajemen dokumen java.'
keywords:
- java full text search
- document management java
- GroupDocs.Search merging
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: 'Learn java full text search with GroupDocs.Search: add documents to
    index, configure merge options, and cancel merge operation. Ideal for document
    management java solutions.'
  headline: java full text search – add docs & merge with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It tells GroupDocs.Search to scan a folder, extract searchable tokens,
      and store metadata for each file.
    question: What does “add documents to index” mean?
  - answer: Yes—use the `Cancellation` object to abort a merge after a configurable
      timeout.
    question: Can I stop a long merge?
  - answer: A free trial or temporary license works for testing; a commercial license
      unlocks full features.
    question: Do I need a license?
  - answer: JDK 8 or newer.
    question: Which Java version is required?
  - answer: Absolutely—GroupDocs.Search can handle multi‑hundred‑page documents with
      incremental indexing.
    question: Is this suitable for large datasets?
  type: FAQPage
title: pencarian teks lengkap java – tambahkan dokumen & gabungkan dengan GroupDocs.Search
type: docs
url: /id/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# pencarian teks lengkap java – tambahkan dokumen & gabungkan dengan GroupDocs.Search

Di lingkungan perusahaan modern, **java full text search** adalah tulang punggung dari sistem manajemen dokumen java yang kuat. Apakah Anda perlu mengindeks kontrak, faktur, atau laporan internal, indeks yang dirancang dengan baik memungkinkan Anda mengambil informasi yang tepat dalam hitungan milidetik. Tutorial ini memandu Anda melalui pembuatan indeks, menambahkan dokumen, mengonfigurasi opsi penggabungan, dan membatalkan operasi penggabungan dengan aman—semua menggunakan GroupDocs.Search untuk Java.

## Jawaban Cepat
- **Apa arti “add documents to index”?** Ini memberi tahu GroupDocs.Search untuk memindai folder, mengekstrak token yang dapat dicari, dan menyimpan metadata untuk setiap file.  
- **Bisakah saya menghentikan penggabungan yang lama?** Ya—gunakan objek `Cancellation` untuk membatalkan penggabungan setelah batas waktu yang dapat dikonfigurasi.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan gratis atau lisensi sementara dapat digunakan untuk pengujian; lisensi komersial membuka semua fitur.  
- **Versi Java apa yang diperlukan?** JDK 8 atau yang lebih baru.  
- **Apakah ini cocok untuk kumpulan data besar?** Tentu—GroupDocs.Search dapat menangani dokumen ratusan halaman dengan pengindeksan inkremental.

## Apa itu “add documents to index” dalam GroupDocs.Search?
**Menambahkan dokumen ke indeks berarti memasukkan kumpulan file ke GroupDocs.Search sehingga perpustakaan dapat menganalisis kontennya, mengekstrak token, dan membangun struktur data yang dapat dicari.** Proses ini membuat representasi kompak yang memungkinkan kueri teks lengkap yang sangat cepat di semua file yang diindeks.

## Mengapa menggunakan GroupDocs.Search untuk manajemen dokumen java?
GroupDocs.Search menyediakan **pengindeksan yang dapat diskalakan untuk lebih dari 50 format input** (PDF, DOCX, XLSX, PPTX, HTML, gambar, dll.) dan dapat memproses **dokumen hingga 2 GB tanpa memuat seluruh file ke memori**. API-nya memberi Anda kontrol detail atas pengindeksan, penggabungan, dan pembatalan, menjadikannya pilihan utama untuk solusi pencarian teks lengkap java tingkat perusahaan.

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
- **Free Trial:** Daftar di situs GroupDocs untuk mendapatkan lisensi percobaan.  
- **Temporary License:** Ajukan kunci sementara jika Anda memerlukan evaluasi yang lebih lama.  
- **Commercial License:** Beli untuk penggunaan produksi.

Setelah Anda memiliki file lisensi, letakkan di proyek Anda dan inisialisasi perpustakaan seperti yang ditunjukkan nanti.

## Panduan Implementasi

### Cara menambahkan dokumen ke indeks – Membuat Indeks Pertama
**Muat atau buat indeks kosong dengan menginstansiasi kelas `Index`, yang mewakili kontainer yang dapat dicari di disk.** Langkah ini menyiapkan lokasi penyimpanan untuk semua token yang akan dihasilkan dari dokumen Anda.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Mengapa:** Langkah ini menyiapkan kontainer penyimpanan tempat token yang diindeks akan disimpan.

#### Menambahkan dokumen ke indeks
**Panggil `index.add` dengan path folder; metode ini memindai setiap file, mengekstrak teks, dan menyimpan metadata yang dapat dicari di indeks.** Operasi ini berjalan dalam satu kali proses dan menghormati `IndexSettings` yang dikonfigurasi.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Mengapa:** Perpustakaan membaca setiap file, mengekstrak teks, dan menyimpannya di `index1`.

### Membuat indeks kedua untuk alur kerja fleksibel
**Instansiasi objek `Index` lain untuk menampung set dokumen terpisah, memungkinkan pemrosesan terisolasi sebelum penggabungan.** Pola ini berguna untuk skenario multi‑tenant atau pengindeksan bertahap.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Mengapa:** Beberapa indeks memungkinkan Anda mengelola set dokumen yang berbeda dan kemudian menggabungkannya.

### Cara mengonfigurasi opsi penggabungan dan membatalkan operasi penggabungan
**Buat instance `MergeOptions`, atur parameter yang diinginkan, dan lampirkan token `Cancellation` yang membatalkan penggabungan setelah batas waktu yang ditentukan.** Ini memberi Anda kontrol penuh atas penggunaan sumber daya selama penggabungan besar.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Mengapa:** `Cancellation` memberi Anda kontrol untuk **membatalkan operasi penggabungan** secara otomatis, mencegah tugas yang berjalan tanpa batas.

### Menggabungkan indeks
**Panggil `index1.merge(index2, mergeOptions)`; indeks utama menyerap semua dokumen dari indeks sekunder sambil mempertahankan integritas token.** Setelah penggabungan, Anda memiliki repositori pencarian yang terpadu.

```java
index1.merge(index2, options);
```

- **Mengapa:** Setelah pemanggilan ini, `index1` berisi semua dokumen dari kedua sumber, memberikan pengalaman pencarian yang terpadu.

## Aplikasi Praktis untuk Manajemen Dokumen Java
- **Legal firms:** Konsolidasikan berkas kasus dari banyak kantor ke dalam satu indeks yang dapat dicari.  
- **Financial institutions:** Gabungkan laporan kuartalan ke dalam repositori terpadu untuk kueri audit yang cepat.  
- **Enterprises:** Gabungkan kebijakan HR, manual kepatuhan, dan panduan internal untuk pencarian di seluruh perusahaan.

## Pertimbangan Kinerja
- **Incremental indexing:** Tambahkan file baru secara berkala alih-alih membangun ulang seluruh indeks.  
- **Memory monitoring:** Batch besar dapat mengonsumsi RAM; proses file dalam potongan lebih kecil atau aktifkan mode streaming.  
- **Garbage collection:** Lepaskan objek `Index` yang tidak terpakai dengan cepat untuk membebaskan sumber daya.  
- **SSD storage:** Menyimpan file indeks di SSD dapat meningkatkan kecepatan penggabungan hingga 2×.

## Masalah Umum & Solusi

| Masalah | Solusi |
|-------|----------|
| **Path folder tidak benar** | Verifikasi path absolut dan pastikan aplikasi memiliki izin baca. |
| **Memori tidak cukup** | Tingkatkan heap JVM (`-Xmx`) atau indeks file secara batch. |
| **Pembatalan tidak terpicu** | Pastikan `cancelAfter` diatur sebelum memanggil `merge`. |
| **Format file tidak didukung** | Instal plugin format tambahan dari GroupDocs jika diperlukan. |

## Pertanyaan yang Sering Diajukan

**Q:** *Mengapa saya membuat beberapa indeks alih-alih satu saja?*  
**A:** Indeks terpisah memungkinkan Anda mengisolasi domain data, menerapkan kebijakan keamanan yang berbeda, dan menggabungkan hanya saat diperlukan, yang meningkatkan kinerja dan organisasi.

**Q:** *Bisakah saya membatalkan operasi pengindeksan dengan cara yang sama seperti membatalkan penggabungan?*  
**A:** Ya—gunakan objek `Cancellation` dengan metode `add` untuk menghentikan tugas pengindeksan yang berjalan lama.

**Q:** *Bagaimana cara memastikan kinerja optimal dengan koleksi dokumen yang sangat besar?*  
**A:** Lakukan pengindeksan inkremental, pantau memori JVM, dan simpan indeks di SSD. Pertimbangkan menggunakan pengaturan `BatchSize` untuk membatasi dokumen dalam memori.

**Q:** *Apa yang harus saya lakukan jika menerima error “Access denied”?*  
**A:** Periksa izin folder untuk pengguna yang menjalankan proses Java dan pastikan file lisensi dapat dibaca.

**Q:** *Apakah GroupDocs.Search kompatibel dengan perpustakaan GroupDocs lainnya?*  
**A:** Tentu—Anda dapat mengintegrasikannya dengan GroupDocs.Viewer, GroupDocs.Conversion, dan lainnya untuk membangun solusi dokumen full‑stack.

## Kesimpulan
Dengan mengikuti panduan ini Anda sekarang tahu cara **add documents to index**, mengonfigurasi perilaku penggabungan, dan dengan aman **cancel merge operation** ketika diperlukan—semua dalam alur kerja **java full text search** yang kuat. Bereksperimenlah dengan dataset yang lebih besar, jelajahi tokenizer khusus, atau gabungkan GroupDocs.Search dengan produk GroupDocs lainnya untuk membangun solusi tingkat perusahaan.

**Sumber Daya**
- **Dokumentasi:** [Dokumen GroupDocs.Search Java](https://docs.groupdocs.com/search/java/)  
- **Referensi API:** [Referensi API GroupDocs](https://reference.groupdocs.com/search/java)  
- **Unduh:** [Rilis Terbaru](https://releases.groupdocs.com/search/java/)  
- **Repositori GitHub:** [GroupDocs Search untuk Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Forum Dukungan Gratis:** [Forum GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Aplikasi Lisensi Sementara:** [Lisensi Sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Terakhir Diperbarui:** 2026-05-12  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara menambahkan dokumen ke indeks dengan Metadata Indexing di Java menggunakan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Tambahkan Dokumen ke Indeks dan Nonaktifkan Stop Words dalam GroupDocs.Search Java untuk Akurasi Pencarian yang Lebih Baik](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
- [Menambahkan Dokumen ke Indeks – Tutorial GroupDocs.Search Java](/search/java/document-management/)