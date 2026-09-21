---
date: '2026-09-21'
description: Pelajari cara membuat indeks pencarian teks penuh java menggunakan GroupDocs.Search,
  menambahkan dokumen, dan mengaktifkan dukungan homophone untuk hasil yang lebih
  akurat.
keywords:
- java full text search
- homophone search java
- GroupDocs.Search Java
- document indexing java
- search index java
lastmod: '2026-09-21'
og_description: Temukan cara membuat indeks pencarian teks penuh java dengan GroupDocs.Search,
  menambahkan dokumen, dan mengaktifkan dukungan homophone untuk pencarian yang lebih
  cepat dan lebih akurat.
og_image_alt: Illustration of a Java full text search index with homophone support
og_title: Cara membangun indeks pencarian teks penuh java dengan homophones
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  headline: How to build a java full text search index with homophones
  type: TechArticle
- description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  name: How to build a java full text search index with homophones
  steps:
  - name: '**Install via Maven** or download directly from the provided links.'
    text: '**Install via Maven** or download directly from the provided links.'
  - name: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
    text: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
  - name: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
    text: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
  - name: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
    text: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
  - name: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
    text: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
  type: HowTo
- questions:
  - answer: A data structure that enables fast full‑text search across documents.
    question: What is a search index?
  - answer: It improves recall by matching words that sound alike, e.g., “mail” vs.
      “male”.
    question: Why use homophone recognition?
  - answer: GroupDocs.Search for Java (v25.4).
    question: Which library provides this in Java?
  - answer: A free trial works for evaluation; a permanent license is required for
      production.
    question: Do I need a license?
  - answer: JDK 8 or higher.
    question: What Java version is required?
  type: FAQPage
tags:
- java full text search
- homophone search
- GroupDocs.Search
- document indexing
- search index
title: Cara membangun indeks pencarian teks penuh java dengan homophones
type: docs
url: /id/java/document-management/groupdocs-search-java-homophone-document-management-guide/
weight: 1
---

# Cara Membuat Indeks Pencarian Teks Penuh Java dengan Homofon

## Jawaban Cepat
- **Apa itu indeks pencarian?** Struktur data yang memungkinkan pencarian teks penuh yang cepat di seluruh dokumen.  
- **Mengapa menggunakan pengenalan homofon?** Ini meningkatkan recall dengan mencocokkan kata yang terdengar serupa, misalnya “mail” vs. “male”.  
- **Perpustakaan mana yang menyediakan ini di Java?** GroupDocs.Search untuk Java (v25.4).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi.

## Apa itu pencarian teks penuh Java?
`java full text search` adalah proses mengindeks konten dokumen sehingga Anda dapat melakukan kueri teks dengan cepat dan mengambil file yang relevan secara real time. Indeks menyimpan istilah yang ditokenisasi, posisi, dan metadata, memungkinkan respons pencarian sub‑detik bahkan pada koleksi besar.

## Mengapa Menggunakan GroupDocs.Search untuk Java?
GroupDocs.Search mendukung **lebih dari 50 format file**—termasuk PDF, DOCX, XLSX, PPTX, dan HTML—sementara menyediakan kamus homofon bawaan yang meningkatkan recall hingga **30 %** untuk istilah ambigu. API mengabstraksi detail pengindeksan tingkat rendah, memungkinkan Anda fokus pada logika bisnis. Ini juga menawarkan integrasi mudah dengan proyek Maven dan dokumentasi yang jelas untuk pengembangan cepat.

## Prasyarat

Sebelum kita masuk ke kode, pastikan Anda memiliki hal berikut:

- **GroupDocs.Search untuk Java** (tersedia melalui Maven atau unduhan langsung).  
- Sebuah **JDK yang kompatibel** (8 atau lebih baru).  
- IDE seperti **IntelliJ IDEA** atau **Eclipse**.  
- Pengetahuan dasar tentang Java dan Maven.

### Perpustakaan dan dependensi yang diperlukan
Anda akan membutuhkan GroupDocs.Search untuk Java. Sertakan melalui Maven atau unduh secara langsung.

**Instalasi Maven:**  
Tambahkan berikut ke file `pom.xml` Anda:

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

**Unduhan langsung:**  
Atau, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Persyaratan penyiapan lingkungan
Pastikan Anda memiliki JDK yang kompatibel terpasang (JDK 8 atau lebih tinggi) dan IDE seperti IntelliJ IDEA atau Eclipse yang sudah disiapkan di mesin Anda.

### Prasyarat pengetahuan
Keterbiasaan dengan konsep pemrograman Java dan pengalaman menggunakan Maven untuk manajemen dependensi akan sangat membantu. Pemahaman dasar tentang pengindeksan dokumen dan algoritma pencarian juga dapat membantu.

## Menyiapkan GroupDocs.Search untuk Java

Setelah prasyarat terpenuhi, menyiapkan GroupDocs.Search menjadi sederhana:

1. **Instal melalui Maven** atau unduh langsung dari tautan yang disediakan.  
2. **Dapatkan lisensi:** Anda dapat memulai dengan percobaan gratis atau memperoleh lisensi sementara dengan mengunjungi [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).  
3. **Inisialisasi perpustakaan:** Potongan kode di bawah menunjukkan kode minimal yang diperlukan untuk mulai menggunakan GroupDocs.Search.

```java
import com.groupdocs.search.*;

public class SetupExample {
    public static void main(String[] args) {
        // Define the directory for storing index files.
        String indexFolder = "path/to/index/directory";
        
        // Initialize an Index instance.
        Index index = new Index(indexFolder);
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Panduan Implementasi

Sekarang lingkungan siap, mari jelajahi fitur inti yang Anda perlukan untuk **membuat indeks pencarian teks penuh java** dan mengelola homofon.

### Membuat dan mengelola indeks
#### Ikhtisar
Membuat indeks pencarian adalah langkah pertama dalam mengelola dokumen secara efektif. Ini memungkinkan pengambilan informasi yang cepat berdasarkan konten dokumen Anda.

#### Langkah-langkah membuat indeks
**Langkah 1:** Tentukan direktori untuk file indeks Anda.

```java
String indexFolder = "YOUR_INDEX_DIRECTORY";
Index index = new Index(indexFolder);
```

*Kelas `Index` mewakili kontainer yang dapat dicari yang menyimpan istilah yang ditokenisasi dan metadata untuk setiap dokumen, menyediakan struktur inti yang memungkinkan eksekusi kueri yang cepat dan penyimpanan informasi dokumen yang efisien di seluruh indeks.*

**Langkah 2:** Tambahkan dokumen dari folder yang ditentukan ke dalam indeks ini.

```java
String documentsFolder = "YOUR_DOCUMENTS_SOURCE_DIRECTORY";
index.add(documentsFolder);
System.out.println("Documents added to the index.");
```

*Memanggil `index.add()` mengimpor setiap file, mengekstrak teks, dan mengisi struktur internal yang diperlukan untuk kueri cepat, memastikan setiap dokumen terindeks sepenuhnya dan dapat dicari segera tanpa memerlukan langkah pemrosesan terpisah.*

### Cara menambahkan dokumen ke indeks
Anda dapat menambahkan lebih banyak file secara programatis nanti dengan memanggil `index.add()` lagi dengan jalur folder baru atau jalur file individual. Pendekatan inkremental ini menjaga indeks tetap terbaru tanpa harus membangun ulang secara penuh. Menambahkan dokumen dengan cara ini memungkinkan Anda mempertahankan indeks yang hidup yang mencerminkan perubahan konten terbaru, mendukung ketersediaan pencarian berkelanjutan bagi pengguna akhir dan mengurangi waktu henti yang terkait dengan operasi re‑indeks batch.

### Mengambil homofon untuk sebuah kata
Mengambil homofon untuk istilah tertentu membantu mesin pencari mempertimbangkan ejaan alternatif yang terdengar sama, meningkatkan recall untuk kueri di mana pengguna mungkin salah ketik atau menggunakan varian berbeda. Dengan memperluas kueri dengan ekivalen fonetik, mesin dapat mencocokkan dokumen yang berisi salah satu bentuk homofon, memberikan hasil yang lebih komprehensif.

*Kelas `HomophoneDictionary` menyimpan kelompok kata yang memiliki pengucapan yang sama, berfungsi sebagai repositori pusat yang dikonsultasikan mesin pencari saat memperluas kueri dengan alternatif fonetik, sehingga meningkatkan relevansi hasil pencarian.*

```java
String[] homophones = index.getDictionaries().getHomophoneDictionary().getHomophones("braid");
```

### Mengambil kelompok homofon
Mengelompokkan homofon memberikan cara terstruktur untuk mengelola kata dengan banyak makna, memungkinkan pengembang mengambil seluruh set ekivalen fonetik dalam satu operasi. Ini dapat berguna untuk analitik, manajemen kamus khusus, atau pembaruan massal daftar homofon.

*Setiap grup yang dikembalikan oleh `getGroups()` berisi kata yang dapat dipertukarkan dalam pencarian fonetik, dan metode ini menyediakan koleksi lengkap grup tersebut sehingga Anda dapat memeriksa, memodifikasi, atau mengekspor seluruh set hubungan homofon yang dipelihara oleh kamus.*

```java
String[][] groups = index.getDictionaries().getHomophoneDictionary().getHomophoneGroups("braid");
```

### Menghapus kamus homofon
Menghapus entri yang usang atau tidak diperlukan memastikan kamus Anda tetap relevan dan tidak menambahkan kebisingan pada hasil pencarian. Operasi ini biasanya dilakukan ketika Anda perlu mengatur ulang kamus ke keadaan default sebelum memuat set khusus baru.

*Metode `clear()` menghapus semua entri khusus, mengembalikan ke set default, dan menjamin bahwa semua grup homofon yang sebelumnya ditambahkan sepenuhnya dihapus, menyediakan kanvas bersih untuk konfigurasi kamus selanjutnya.*

```java
if (index.getDictionaries().getHomophoneDictionary().getCount() > 0) {
    index.getDictionaries().getHomophoneDictionary().clear();
}
System.out.println("Homophone dictionary cleared.");
```

### Menambahkan homofon ke kamus
Menyesuaikan kamus homofon Anda memungkinkan kemampuan pencarian yang disesuaikan yang mencerminkan terminologi spesifik domain, slang, atau nama merek. Dengan menambahkan grup baru, Anda dapat memastikan pencarian mengenali hubungan fonetik yang dimaksud unik untuk aplikasi Anda.

*Gunakan `addGroup()` untuk memasukkan daftar kata dengan bunyi sinonim, meningkatkan recall untuk terminologi spesifik domain, dan metode ini memvalidasi setiap entri untuk mencegah duplikat sambil mengintegrasikan grup baru secara mulus ke dalam struktur kamus yang ada.*

```java
String[][] homophoneGroups = {
    new String[] { "awe", "oar", "or", "ore" },
    new String[] { "aye", "eye", "i" },
    new String[] { "call", "caul" }
};
index.getDictionaries().getHomophoneDictionary().addRange(homophoneGroups);
System.out.println("Homophones added to the dictionary.");
```

### Mengekspor dan mengimpor kamus homofon
Mengekspor dan mengimpor kamus dapat bermanfaat untuk tujuan pencadangan atau migrasi, memungkinkan Anda mempertahankan konfigurasi khusus di berbagai lingkungan atau membagikannya dengan anggota tim. Fungsionalitas ini mendukung format JSON untuk kemudahan pembacaan dan integrasi dengan alat lain.

*Metode-metode ini memungkinkan Anda menyimpan kamus khusus sebagai file JSON untuk penggunaan ulang yang mudah, dan proses ekspor menangkap seluruh status kamus sementara prosedur impor memvalidasi struktur JSON sebelum menerapkannya ke instance kamus yang aktif.*

```java
String fileName = "path/to/exported/dictionary.file";
index.getDictionaries().getHomophoneDictionary().exportDictionary(fileName);
```

**Langkah 2:** Impor ulang dari file jika diperlukan.

```java
index.getDictionaries().getHomophoneDictionary().importDictionary(fileName);
System.out.println("Homophone dictionary imported successfully.");
```

*Operasi impor membaca file JSON, merekonstruksi setiap grup homofon, dan menggabungkannya ke dalam kamus saat ini, memastikan semua entri khusus dipulihkan dengan akurat dan siap digunakan segera dalam kueri pencarian.*

### Mencari menggunakan homofon
Manfaatkan pencarian homofon untuk pengambilan dokumen yang komprehensif, memungkinkan pengguna menemukan konten relevan bahkan ketika mereka menggunakan ejaan berbeda yang terdengar serupa. Fitur ini dapat secara dramatis meningkatkan pengalaman pengguna dalam domain multibahasa atau yang banyak menggunakan fonetik.

*Mengatur `setUseHomophoneSearch(true)` memberi instruksi pada mesin untuk memperluas kueri dengan ekivalen fonetik sebelum eksekusi, dan opsi ini bekerja bersama dengan pengaturan pencarian lain seperti pencocokan fuzzy untuk memberikan pengalaman pencarian yang kuat dan fleksibel yang menangkap berbagai hasil relevan.*

```java
String query = "caul";
SearchOptions options = new SearchOptions();
options.setUseHomophoneSearch(true);
SearchResult result = index.search(query, options);

System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Aplikasi Praktis

Memahami cara mengimplementasikan fitur-fitur ini membuka dunia aplikasi praktis:

1. **Manajemen dokumen hukum:** Membedakan antara istilah hukum yang terdengar serupa seperti “lease” vs. “least”.  
2. **Pembuatan konten edukatif:** Memastikan materi pengajaran bebas dari kata yang ambigu yang dapat membingungkan pelajar.  
3. **Sistem dukungan pelanggan:** Meningkatkan akurasi pencarian basis pengetahuan, membantu agen menemukan artikel yang tepat lebih cepat.

## Pertimbangan Kinerja

Untuk menjaga **pencarian teks penuh java** Anda tetap berperforma:

- **Perbarui indeks secara teratur** untuk mencerminkan perubahan dokumen.  
- **Pantau penggunaan memori** dan sesuaikan pengaturan heap Java untuk kumpulan data besar.  
- **Tutup sumber daya yang tidak digunakan dengan cepat** (mis., panggil `index.close()` saat selesai).  

## Kesimpulan

Sekarang Anda seharusnya memiliki pemahaman yang kuat tentang **cara mengindeks dokumen** dengan GroupDocs.Search, mengelola homofon, dan menyempurnakan pengalaman pencarian Anda. Alat-alat ini sangat berharga untuk memberikan hasil yang tepat dan meningkatkan efisiensi manajemen dokumen secara keseluruhan.

## Pertanyaan yang Sering Diajukan

**Q:** Bisakah saya menggunakan kamus homofon dengan bahasa non‑Inggris?  
**A:** Ya, Anda dapat mengisi kamus dengan bahasa apa pun selama Anda menyediakan grup kata yang sesuai.

**Q:** Apakah saya memerlukan lisensi untuk pengujian pengembangan?  
**A:** Lisensi percobaan gratis sudah cukup untuk pengembangan dan pengujian; lisensi berbayar diperlukan untuk penerapan produksi.

**Q:** Seberapa besar indeks saya dapat?  
**A:** Ukuran indeks hanya dibatasi oleh sumber daya perangkat keras Anda; alokasikan ruang disk dan memori yang cukup untuk kinerja optimal.

**Q:** Apakah memungkinkan menggabungkan pencarian homofon dengan pencocokan fuzzy?  
**A:** Tentu saja. Aktifkan kedua `setUseHomophoneSearch(true)` dan `setFuzzySearch(true)` dalam `SearchOptions` untuk mendapatkan manfaat keduanya.

**Q:** Apa yang terjadi jika saya menambahkan grup homofon duplikat?  
**A:** Entri duplikat diabaikan; kamus mempertahankan set unik grup kata.

---

**Terakhir Diperbarui:** 2026-09-21  
**Diuji dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara mengimplementasikan pencarian teks penuh java: membuat direktori indeks dengan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Cara menambahkan dokumen ke indeks dengan Metadata Indexing di Java menggunakan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Perpustakaan Pencarian Teks Penuh Java – Optimalkan Indeks dengan GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)