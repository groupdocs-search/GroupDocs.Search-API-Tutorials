---
date: '2026-10-12'
description: Pelajari cara memperbarui index java untuk java full text search menggunakan
  GroupDocs.Search. Membahas penambahan dokumen, peningkatan versi index, pengaturan
  Maven, dan tips kinerja.
keywords:
- java full text search
- update index java
- add documents to index
- upgrade search index
lastmod: '2026-10-12'
og_description: Temukan cara memperbarui index java untuk java full text search dengan
  GroupDocs.Search. Panduan langkah demi langkah mencakup pengaturan Maven, penambahan
  dokumen, dan upgrade versi index.
og_image_alt: Guide to updating Java full text search index using GroupDocs.Search
og_title: Cara memperbarui index java untuk java full text search
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: Learn how to update index java for java full text search using GroupDocs.Search.
    Covers adding documents, upgrading index versions, Maven setup, and performance
    tips.
  headline: How to update index java for java full text search
  type: TechArticle
- description: Learn how to update index java for java full text search using GroupDocs.Search.
    Covers adding documents, upgrading index versions, Maven setup, and performance
    tips.
  name: How to update index java for java full text search
  steps:
  - name: '**Maven setup** – Add the repository and dependency to your `pom.xml` as
      shown above.'
    text: '**Maven setup** – Add the repository and dependency to your `pom.xml` as
      shown above.'
  - name: '**Direct download** – If you prefer not to use Maven, grab the JAR from
      the [GroupDocs downloads page](https://releases.groupdocs.com/search/java/).'
    text: '**Direct download** – If you prefer not to use Maven, grab the JAR from
      the [GroupDocs downloads page](https://releases.groupdocs.com/search/java/).'
  - name: '**Content management systems** – Keep search indexes fresh as articles,
      PDFs, and images are added or edited.'
    text: '**Content management systems** – Keep search indexes fresh as articles,
      PDFs, and images are added or edited.'
  - name: '**Legal document repositories** – Automatically reflect amendments to contracts,
      statutes, and case files.'
    text: '**Legal document repositories** – Automatically reflect amendments to contracts,
      statutes, and case files.'
  - name: '**Enterprise data warehousing** – Regularly refresh indexed data for accurate
      analytics and reporting.'
    text: '**Enterprise data warehousing** – Regularly refresh indexed data for accurate
      analytics and reporting.'
  type: HowTo
- questions:
  - answer: Yes, as long as the old index is still readable by the library; the `canUpdateVersion`
      method will confirm compatibility.
    question: Can I upgrade an index created with a very old version of GroupDocs.Search?
  - answer: Not necessarily. Updating the index version is sufficient in most cases,
      saving time and resources.
    question: Do I need to recreate the index after every library update?
  - answer: Start with 2‑4 threads and monitor CPU usage; increase only if the system
      has spare cores and memory.
    question: How many threads should I use for large indexes?
  - answer: The trial license removes feature limits, making it ideal for development
      and QA environments.
    question: Is a trial license enough for production testing?
  - answer: The index structure is migrated, but the searchable content remains unchanged,
      so results stay consistent.
    question: What happens to existing search results after an index version update?
  type: FAQPage
tags:
- java full text search
- GroupDocs.Search
- document indexing
title: Cara memperbarui index java untuk java full text search
type: docs
url: /id/java/document-management/guide-updating-index-versions-groupdocs-search-java/
weight: 1
---

# Cara memperbarui indeks java untuk pencarian teks penuh java

Menjaga indeks **java full text search** tetap terbaru sangat penting untuk aplikasi Java berkinerja tinggi. Dalam panduan ini Anda akan belajar cara memperbarui indeks java dengan GroupDocs.Search, mulai dari menambahkan dokumen baru hingga meningkatkan versi indeks, serta mendapatkan tips penyetelan kinerja yang bekerja untuk CMS, repositori hukum, dan gudang data besar.

## Jawaban Cepat
- **Apa arti “update index java”?** Ini adalah proses menyegarkan indeks di disk sehingga mencerminkan perubahan dokumen terbaru dan versi perpustakaan.  
- **Artifact Maven mana yang saya perlukan?** Tambahkan dependensi `groupdocs-search` ke `pom.xml` Anda.  
- **Apakah saya memerlukan lisensi untuk mencobanya?** Ya – lisensi percobaan gratis tersedia untuk evaluasi.  
- **Bisakah saya memperbarui indeks secara paralel?** Tentu – konfigurasikan `UpdateOptions` dengan beberapa thread.  
- **Apakah pendekatan ini efisien memori?** Pengaturan thread yang tepat dan pembersihan rutin menjaga penggunaan heap Java tetap rendah.

## Apa itu “update index java”?

Memperbarui indeks di Java menyinkronkan struktur indeks di disk dengan kumpulan dokumen sumber saat ini dan versi perpustakaan GroupDocs.Search yang Anda gunakan. Ketika perpustakaan berkembang, Anda mungkin juga perlu **mengupgrade indeks pencarian** untuk menjaga kompatibilitas.

## Mengapa menggunakan GroupDocs.Search untuk Java?

GroupDocs.Search menyediakan pencarian teks penuh yang kuat untuk **lebih dari 50 format dokumen** (PDF, DOCX, XLSX, PPTX, HTML, XML, dan banyak tipe gambar). Ia mendukung pengindeksan multi‑thread yang dapat memproses **ratusan megabyte per detik** pada server tipikal, dan menawarkan manajemen versi bawaan sehingga indeks Anda tetap dapat digunakan setelah pembaruan perpustakaan.

## Prasyarat
- Java Development Kit (JDK) 8 atau lebih tinggi.  
- IDE seperti IntelliJ IDEA atau Eclipse.  
- Pengetahuan dasar tentang Java dan Maven.  

## Dependensi Maven groupdocs

Untuk bekerja dengan GroupDocs.Search, Anda memerlukan koordinat Maven yang tepat. Tambahkan repositori dan dependensi yang ditunjukkan di bawah ini ke file `pom.xml` Anda.

**Konfigurasi Maven:**  
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
Sebagai alternatif, Anda dapat [unduh versi terbaru secara langsung](https://releases.groupdocs.com/search/java/).

## Menyiapkan GroupDocs.Search untuk Java

### Instruksi instalasi
1. **Pengaturan Maven** – Tambahkan repositori dan dependensi ke `pom.xml` Anda seperti yang ditunjukkan di atas.  
2. **Unduhan langsung** – Jika Anda lebih memilih tidak menggunakan Maven, dapatkan JAR dari [halaman unduhan GroupDocs](https://releases.groupdocs.com/search/java/).

### Akuisisi lisensi
GroupDocs menawarkan lisensi percobaan gratis yang memungkinkan Anda menjelajahi semua fitur tanpa batasan. Dapatkan lisensi sementara dari [portal pembelian](https://purchase.groupdocs.com/temporary-license/). Untuk produksi, beli lisensi penuh.

### Inisialisasi dan pengaturan dasar
```java
import com.groupdocs.search.Index;

// Define the index directory path
String indexFolder = "YOUR_OUTPUT_DIRECTORY/UpdateIndexedDocuments/Index";

// Create an Index instance
Index index = new Index(indexFolder);
```

## Panduan implementasi

### Perbarui dokumen terindeks – **tambahkan dokumen ke indeks**

Menjaga indeks Anda sinkron dengan file sumber adalah bagian inti dari **update index java**.

#### Implementasi langkah demi langkah
**1. Tentukan jalur direktori**  
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/UpdateIndexedDocuments/Index";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY/Documents";
```  

**2. Siapkan data**  
```java
Utils.cleanDirectory(documentFolder);
Utils.copyFiles(Utils.DocumentsPath, documentFolder);
```  

**3. Buat indeks**  
```java
Index index = new Index(indexFolder);
```  

**4. Tambahkan dokumen ke indeks**  
```java
index.add(documentFolder);
```  

**5. Lakukan pencarian awal**  
```java
String query = "son";
SearchResult searchResult = index.search(query);
```  

**6. Simulasikan perubahan dokumen**  
```java
Utils.copyFiles(Utils.DocumentsPath4, documentFolder);
```  

**7. Atur opsi pembaruan**  
`UpdateOptions` menentukan bagaimana indeksator berperilaku selama pembaruan, seperti jumlah thread, ukuran batch, dan apakah menghapus file yang hilang.  
```java
UpdateOptions options = new UpdateOptions();
options.setThreads(2); // Using two threads for faster indexing
```  

**8. Perbarui indeks**  
```java
index.update(options);
```  

**9. Verifikasi pembaruan dengan pencarian lain**  
```java
SearchResult searchResult2 = index.search(query);
```  

**Tips pemecahan masalah**
- Verifikasi bahwa semua jalur file benar dan dapat diakses.  
- Pastikan proses memiliki izin baca/tulis pada folder indeks.  
- Pantau penggunaan CPU dan memori saat meningkatkan jumlah thread.

### Perbarui versi indeks – **upgrade search index**

Saat Anda mengupgrade GroupDocs.Search, Anda mungkin perlu **upgrade search index** untuk menjaga indeks yang ada tetap dapat digunakan.

#### Implementasi langkah demi langkah
**1. Tentukan jalur direktori**  
```java
String oldIndexFolder = Utils.OldIndexPath;
String sourceIndexFolder = "YOUR_DOCUMENT_DIRECTORY/SourceIndex";
String targetIndexFolder = "YOUR_OUTPUT_DIRECTORY/TargetIndex";
```  

**2. Siapkan data**  
```java
Utils.cleanDirectory(sourceIndexFolder);
Utils.cleanDirectory(targetIndexFolder);
Utils.copyFiles(oldIndexFolder, sourceIndexFolder);
```  

**3. Buat IndexUpdater**  
Kelas `IndexUpdater` menangani migrasi indeks yang ada ke versi perpustakaan saat ini.  
```java
IndexUpdater updater = new IndexUpdater();
```  

**4. Periksa dan perbarui versi**  
```java
if (updater.canUpdateVersion(sourceIndexFolder)) {
    VersionUpdateResult result = updater.updateVersion(sourceIndexFolder, targetIndexFolder);
}
```  

**Tips pemecahan masalah**
- Pastikan indeks sumber dibuat dengan versi lama yang didukung.  
- Pastikan ruang disk cukup untuk folder indeks target.  
- Perbarui semua dependensi Maven ke versi yang sama untuk menghindari masalah kompatibilitas.

## Aplikasi praktis
1. **Sistem manajemen konten** – Jaga indeks pencarian tetap segar saat artikel, PDF, dan gambar ditambahkan atau diedit.  
2. **Repositori dokumen hukum** – Secara otomatis mencerminkan amandemen pada kontrak, undang‑undang, dan berkas kasus.  
3. **Gudang data perusahaan** – Secara teratur menyegarkan data terindeks untuk analitik dan pelaporan yang akurat.

## Pertimbangan kinerja
- **Manajemen thread** – Gunakan multi‑threading secara bijak; terlalu banyak thread dapat menyebabkan tekanan GC.  
- **Pemantauan memori** – Secara berkala panggil `System.gc()` atau gunakan alat profiling untuk memantau penggunaan heap.  
- **Optimisasi kueri** – Tulis string pencarian yang singkat dan manfaatkan filter untuk mengurangi ukuran set hasil.

## Masalah umum dan solusi
| Gejala | Penyebab kemungkinan | Solusi |
|---------|----------------------|--------|
| `Index not found` error | Jalur folder salah | Periksa kembali `indexFolder` dan pastikan direktori ada. |
| Out‑of‑memory during update | Jumlah thread berlebih | Kurangi `options.setThreads()` atau tingkatkan heap (`-Xmx`). |
| No results after version upgrade | Indeks lama tidak kompatibel | Verifikasi `updater.canUpdateVersion()` mengembalikan `true` sebelum melanjutkan. |
| License exception | Lisensi percobaan kedaluwarsa | Minta percobaan baru atau terapkan kunci lisensi yang dibeli. |

## Pertanyaan yang sering diajukan

**Q: Bisakah saya mengupgrade indeks yang dibuat dengan versi sangat lama dari GroupDocs.Search?**  
A: Ya, selama indeks lama masih dapat dibaca oleh perpustakaan; metode `canUpdateVersion` akan mengonfirmasi kompatibilitas.

**Q: Apakah saya perlu membuat ulang indeks setelah setiap pembaruan perpustakaan?**  
A: Tidak selalu. Memperbarui versi indeks sudah cukup dalam kebanyakan kasus, menghemat waktu dan sumber daya.

**Q: Berapa banyak thread yang harus saya gunakan untuk indeks besar?**  
A: Mulailah dengan 2‑4 thread dan pantau penggunaan CPU; tingkatkan hanya jika sistem memiliki inti dan memori yang tersedia.

**Q: Apakah lisensi percobaan cukup untuk pengujian produksi?**  
A: Lisensi percobaan menghapus batas fitur, menjadikannya ideal untuk lingkungan pengembangan dan QA.

**Q: Apa yang terjadi pada hasil pencarian yang ada setelah pembaruan versi indeks?**  
A: Struktur indeks dimigrasikan, tetapi konten yang dapat dicari tetap tidak berubah, sehingga hasil tetap konsisten.

## Kesimpulan
Dengan mengikuti langkah-langkah di atas, Anda kini memiliki pemahaman yang kuat tentang cara **update index java** untuk **java full text search** dengan GroupDocs.Search. Menyegarkan baik konten dokumen maupun versi indeks memastikan pengalaman pencarian Anda tetap cepat, akurat, dan kompatibel dengan rilis perpustakaan di masa mendatang.

### Langkah selanjutnya
- Bereksperimen dengan konfigurasi `UpdateOptions` yang berbeda untuk menemukan titik optimal bagi beban kerja Anda.  
- Jelajahi fitur kueri lanjutan seperti faceting dan highlighting yang ditawarkan oleh GroupDocs.Search.  
- Integrasikan alur kerja pengindeksan ke dalam pipeline CI/CD Anda untuk pembaruan otomatis.

---

**Terakhir Diperbarui:** 2026-10-12  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara mengimplementasikan java full text search: buat direktori indeks dengan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Perpustakaan Java Full Text Search – Optimalkan Indeks dengan GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Pencarian Fuzzy Java: Tambahkan Dokumen ke Indeks dengan GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)