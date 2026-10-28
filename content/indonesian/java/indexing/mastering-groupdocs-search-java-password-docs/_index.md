---
date: '2026-10-28'
description: Pelajari cara mencari beberapa jenis file dan membuat indeks yang dapat
  dicari untuk dokumen yang dilindungi kata sandi di Java menggunakan GroupDocs.Search.
  Panduan langkah demi langkah dengan kode, tips, dan trik kinerja.
keywords:
- search multiple file types
- build searchable index
- password protected document indexing java
- groupdocs.search java api
lastmod: '2026-10-28'
og_description: Pelajari cara mencari beberapa jenis file dan membuat indeks yang
  dapat dicari untuk dokumen yang dilindungi kata sandi di Java menggunakan GroupDocs.Search.
  Panduan langkah demi langkah dengan kode, tips, dan trik kinerja.
og_image_alt: Guide showing Java code to search multiple file types and index password‑protected
  documents with GroupDocs.Search
og_title: Cara mencari beberapa jenis file dan mengindeks dokumen di Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-28'
  description: Learn how to search multiple file types and build a searchable index
    for password‑protected documents in Java using GroupDocs.Search. Step‑by‑step
    guide with code, tips, and performance tricks.
  headline: How to search multiple file types and index docs in Java
  type: TechArticle
- questions:
  - answer: GroupDocs.Search supports 120+ formats including PDF, DOCX, XLSX, PPTX,
      and common image types. Install format plugins if required.
    question: How do I handle different file formats?
  - answer: The document is skipped and a warning is logged; verify your password
      dictionary or event handler.
    question: What happens if a password is wrong?
  - answer: Yes, but they must be downloaded to a local temporary folder first because
      the engine works with file‑system paths.
    question: Can I index files stored in the cloud?
  - answer: Adjust scoring with `IndexOptions`, add synonyms, and use advanced query
      syntax such as `field:term~` for fuzzy matching. `IndexOptions` is a configuration
      object that controls scoring and indexing behavior.
    question: How can I improve search relevance?
  - answer: Review the log output; common causes are missing passwords, corrupted
      files, or unsupported formats.
    question: What should I do if indexing fails for some files?
  type: FAQPage
tags:
- search multiple file types
- GroupDocs.Search
- Java indexing
- password‑protected docs
- document search
title: Cara mencari beberapa jenis file dan mengindeks dokumen di Java
type: docs
url: /id/java/indexing/mastering-groupdocs-search-java-password-docs/
weight: 1
---

# Cara mencari beberapa jenis file dan mengindeks dokumen di Java

Di perusahaan modern Anda sering perlu **mencari beberapa jenis file** sambil menjaga file rahasia terkunci dengan kata sandi. Tutorial ini menunjukkan cara membuat indeks yang dapat dicari untuk dokumen yang dilindungi kata sandi di Java menggunakan GroupDocs.Search. Anda akan melihat cara mengonfigurasi kamus kata sandi, menangani peristiwa password‑required, dan mengoptimalkan kinerja untuk batch besar—semua tanpa menulis logika dekripsi khusus.

## Jawaban Cepat
- **Apa yang dibahas dalam tutorial ini?** Mengindeks dokumen yang dilindungi kata sandi dengan kamus kata sandi dan pendengar peristiwa.  
- **Perpustakaan apa yang diperlukan?** GroupDocs.Search untuk Java (versi terbaru).  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan gratis sementara tersedia untuk evaluasi.  
- **Bisakah saya mengindeks jenis file lain?** Ya, GroupDocs.Search mendukung lebih dari 120 format termasuk PDF, DOCX, XLSX, PPTX, dan gambar.  
- **Versi Java apa yang dibutuhkan?** JDK 8 atau lebih baru.  

## Apa itu “create document index java”?
`create document index java` mengacu pada proses membangun struktur data yang dapat dicari yang memetakan istilah ke lokasi file yang dikelola oleh Java. Dengan GroupDocs.Search, mesin secara otomatis mengekstrak teks dari format yang didukung—termasuk PDF terenkripsi, dokumen Office, dan gambar—sehingga Anda dapat melakukan pencarian full‑text tanpa menulis kode dekripsi apa pun. Pendekatan ini menyederhanakan implementasi pencarian sambil mempertahankan keamanan dokumen.

## Mengapa menggunakan GroupDocs.Search untuk file yang dilindungi kata sandi?
GroupDocs.Search menyediakan mekanisme membuka kunci tanpa sentuhan yang menerapkan kata sandi dari kamus atau penangan peristiwa, memungkinkan Anda mengindeks file terenkripsi dalam satu kali proses. Ia memproses hingga 2 juta dokumen per jam pada server standar 8‑core, mendukung lebih dari 120 jenis file, dan menawarkan bahasa kueri yang kaya dengan operator Boolean, wildcard, dan fuzzy—semua penting untuk membangun indeks yang dapat dicari yang mencakup konten beragam.

## Prasyarat
- Java Development Kit (JDK) 8+ terpasang dan ditambahkan ke `PATH` Anda.  
- IDE seperti IntelliJ IDEA atau Eclipse.  
- Maven untuk manajemen dependensi.  
- GroupDocs.Search untuk Java – tambahkan perpustakaan melalui Maven (lihat bagian penyiapan).  

## Menyiapkan GroupDocs.Search untuk java

### Menggunakan Maven
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

### Unduhan langsung
Sebagai alternatif, Anda dapat mengunduh versi terbaru langsung dari [rilisan GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

Untuk memulai dengan lisensi percobaan, kunjungi [halaman lisensi sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/) dan ikuti instruksi untuk mendapatkan percobaan gratis Anda.

## Cara mengindeks dokumen dengan kamus kata sandi

Anda dapat **membangun indeks yang dapat dicari** dengan menyediakan kamus yang memetakan jalur file ke kata sandinya. Mesin akan secara otomatis mengambil kata sandi yang tepat selama proses pengindeksan.

### Ikhtisar
Simpan kata sandi dokumen dalam peta key‑value sederhana sehingga mesin pengindeksan dapat membuka file sesuai permintaan.

### Langkah 1: definisikan indeks dan folder dokumen
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordDictionary";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Langkah 2: buat indeks
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Langkah 3: tambahkan kata sandi dokumen
```java
// Add passwords for specific files using their absolute paths
String path1 = new File(documentsFolder + "/English.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path1, "123456");

String path2 = new File(documentsFolder + "/SampleDocument.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path2, "123456");
```

### Langkah 4: indeks dokumen
```java
// Automatically retrieve passwords from the dictionary during indexing
index.add(documentsFolder);
```

### Langkah 5: cari dalam indeks
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

**Tip:** Untuk skenario produksi, muat kata sandi dari vault yang aman (misalnya Azure Key Vault atau AWS Secrets Manager) alih-alih menuliskannya secara hard‑code.

#### Pemecahan Masalah
- Verifikasi bahwa setiap kata sandi cocok dengan kata sandi perlindungan sebenarnya pada file.  
- Periksa kembali jalur file; jalur yang salah memicu `FileNotFoundException`.

## Cara mengindeks dokumen dengan pendengar peristiwa untuk kebutuhan kata sandi?

Anda dapat menyediakan kata sandi hanya ketika mesin memicu peristiwa password‑required, menjaga kredensial tetap di luar memori dan memungkinkan resolusi kata sandi secara dinamis.

Ketika mesin pengindeksan menemukan file terenkripsi, ia memicu callback di mana Anda dapat mencari kata sandi dari penyimpanan yang aman atau menghitungnya secara langsung. Metode ini mengurangi permukaan serangan dibandingkan menyimpan semua kata sandi dalam kamus.

### Ikhtisar
Sediakan kata sandi secara langsung melalui callback peristiwa, menjaga penyimpanan kredensial Anda terisolasi.

### Langkah 1: definisikan indeks dan folder dokumen
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordEvent";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Langkah 2: buat indeks
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Langkah 3: berlangganan ke peristiwa password‑required
```java
index.getEvents().PasswordRequired.add(new EventHandler<PasswordRequiredEventArgs>() {
    @Override
    public void invoke(Object sender, PasswordRequiredEventArgs args) {
        // Provide password for DOCX files when needed
        if (args.getDocumentFullPath().endsWith(".docx")) {
            args.setPassword("123456");
        }
    }
});
```

### Langkah 4: indeks dokumen
```java
// The event handler will supply passwords as required during indexing
index.add(documentsFolder);
```

### Langkah 5: cari dalam indeks
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

#### Pemecahan Masalah
- Pastikan penangan peristiwa mencakup semua ekstensi file yang perlu Anda indeks.  
- Uji dengan beberapa file contoh terlebih dahulu untuk memastikan kata sandi diterapkan.

## Aplikasi praktis

1. **Manajemen dokumen perusahaan** – mengotomatisasi pengindeksan kontrak rahasia, file HR, dan laporan keuangan sambil menjaga mereka tetap terenkripsi saat disimpan.  
2. **Arsip hukum** – dengan cepat mengambil file kasus tanpa mengungkapkan konten sensitif.  
3. **Rekaman kesehatan** – mengindeks PDF dan dokumen Word pasien sambil mematuhi persyaratan HIPAA.

## Pertimbangan kinerja

- **Alokasi memori** – alokasikan memori heap yang cukup (`-Xmx2g` atau lebih tinggi) untuk batch besar.  
- **Pengindeksan paralel** – gunakan `index.addAsync(...)` atau jalankan beberapa thread pengindeksan untuk mencapai hingga **2 juta dokumen per jam** pada mesin 8‑core. `index.addAsync(...)` adalah metode yang menempatkan dokumen dalam antrean untuk pengindeksan asinkron.  
- **Pemeliharaan indeks** – secara berkala panggil `index.optimize()` untuk memadatkan indeks dan meningkatkan kecepatan kueri.

## Masalah umum dan solusi

- **Kata sandi salah** – dokumen dilewati dan peringatan dicatat. Periksa kembali sumber kata sandi Anda.  
- **Format tidak didukung** – instal plugin format yang diperlukan atau konversi file ke tipe yang didukung sebelum pengindeksan.  
- **File besar** – tingkatkan ukuran heap dan pertimbangkan mengindeksnya dalam batch yang lebih kecil untuk menghindari `OutOfMemoryError`.

## Pertanyaan yang sering diajukan

**T: Bagaimana cara saya menangani format file yang berbeda?**  
J: GroupDocs.Search mendukung lebih dari 120 format termasuk PDF, DOCX, XLSX, PPTX, dan tipe gambar umum. Instal plugin format jika diperlukan.

**T: Apa yang terjadi jika kata sandi salah?**  
J: Dokumen dilewati dan peringatan dicatat; verifikasi kamus kata sandi atau penangan peristiwa Anda.

**T: Bisakah saya mengindeks file yang disimpan di cloud?**  
J: Ya, tetapi mereka harus diunduh ke folder sementara lokal terlebih dahulu karena mesin bekerja dengan jalur sistem file.

**T: Bagaimana saya dapat meningkatkan relevansi pencarian?**  
J: Sesuaikan skor dengan `IndexOptions`, tambahkan sinonim, dan gunakan sintaks kueri lanjutan seperti `field:term~` untuk pencocokan fuzzy. `IndexOptions` adalah objek konfigurasi yang mengontrol perilaku skor dan pengindeksan.

**T: Apa yang harus saya lakukan jika pengindeksan gagal untuk beberapa file?**  
J: Tinjau output log; penyebab umum adalah kata sandi yang hilang, file rusak, atau format yang tidak didukung.

## Sumber daya
- [Dokumentasi GroupDocs.Search](https://docs.groupdocs.com/search/java/)
- [Referensi API](https://reference.groupdocs.com/search/java)
- [Unduh GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [Repositori GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Informasi Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

Dengan mengikuti panduan ini, Anda kini mengetahui **cara mencari beberapa jenis file** dan **mengindeks dokumen yang dilindungi kata sandi** di Java, meningkatkan keamanan serta ketertemuan dalam aplikasi Anda.

---

**Last Updated:** 2026-10-28  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Tutorial Terkait

- [Cara mengindeks dokumen yang dilindungi kata sandi di Java menggunakan GroupDocs.Search](/search/java/indexing/mastering-groupdocs-search-java-password-docs/)
- [Meningkatkan Kinerja Kueri dengan GroupDocs.Search Java: Optimalkan Indeks & Pencarian](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)