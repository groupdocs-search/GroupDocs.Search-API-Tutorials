---
date: '2026-02-06'
description: Pelajari cara menambahkan dokumen ke indeks dan mengaktifkan pencarian
  sensitif huruf besar/kecil di Java dengan GroupDocs.Search, meningkatkan akurasi
  aplikasi Anda.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Tambahkan dokumen ke indeks: pencarian Java yang sensitif huruf besar/kecil
  dengan GroupDocs'
type: docs
url: /id/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Tambahkan dokumen ke indeks: Menguasai Pencarian Sensitif Huruf di Java dengan GroupDocs

Mengambil potongan informasi yang tepat dari kumpulan dokumen yang sangat besar adalah kebutuhan inti bagi aplikasi modern. Dalam panduan ini, Anda akan belajar **cara menambahkan dokumen ke indeks** dan melakukan **pencarian sensitif huruf** menggunakan GroupDocs.Search untuk Java. Baik Anda membangun repositori dokumen hukum, katalog e‑commerce, atau sistem manajemen konten, hasil pencarian yang tepat membuat pengguna senang dan data Anda dapat dipercaya.

## Jawaban Cepat
- **Apa langkah utama untuk memulai pencarian?** Tambahkan dokumen ke indeks dengan `index.add(...)`.
- **Bagaimana mengaktifkan pencarian sensitif huruf?** Setel `options.setUseCaseSensitiveSearch(true)`.
- **Bisakah saya mencari di beberapa direktori?** Ya – panggil `index.add()` untuk setiap folder yang ingin Anda sertakan.
- **Metode apa yang memungkinkan saya mencari dengan objek?** Gunakan `SearchQuery.createWordQuery(...)`.
- **Apakah saya memerlukan lisensi untuk pengujian?** Lisensi sementara tersedia untuk tujuan percobaan.

## Apa arti “menambahkan dokumen ke indeks”?
Menambahkan dokumen ke indeks berarti memasukkan file sumber Anda (PDF, dokumen Word, teks biasa, dll.) ke dalam GroupDocs.Search sehingga dapat membangun struktur data yang dapat dicari. Setelah diindeks, mesin dapat mengeksekusi kueri cepat, termasuk yang sensitif huruf.

## Mengapa mengaktifkan pencarian sensitif huruf di Java?
- **Pencocokan istilah yang tepat** – membedakan “Apple” (perusahaan) dari “apple” (buah).  
- **Kepatuhan regulasi** – beberapa industri memerlukan pencocokan frasa yang tepat.  
- **Relevansi yang lebih baik** – pengguna sering mengharapkan hasil yang spesifik huruf dalam konteks teknis atau hukum.

## Prasyarat
- JDK (Java 17 atau lebih baru disarankan)  
- Maven untuk manajemen dependensi  
- IDE seperti IntelliJ IDEA atau Eclipse  
- Familiaritas dasar dengan pemrograman Java  

## Menyiapkan GroupDocs.Search untuk Java
Pertama, tambahkan repositori GroupDocs dan dependensinya ke `pom.xml` Anda:

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

Atau, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Lisensi
Untuk memulai dengan percobaan, kunjungi GroupDocs untuk memperoleh lisensi sementara. Ini akan memungkinkan Anda menguji semua fitur tanpa batasan.

## Cara menambahkan dokumen ke indeks – Pencarian Kuery Teks

### Langkah 1: Buat Indeks dan tambahkan dokumen Anda
Buat folder tempat file indeks akan disimpan, lalu tambahkan direktori sumber yang berisi dokumen yang ingin Anda cari.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Tips profesional:** Anda dapat memanggil `index.add()` beberapa kali untuk **mencari di banyak direktori** dalam satu indeks.

### Langkah 2: Aktifkan pencarian sensitif huruf
Konfigurasikan opsi pencarian agar memperhatikan kapitalisasi huruf.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Langkah 3: Jalankan kueri teks sensitif huruf
Jalankan kueri yang membedakan “Advantages” dari “advantages”.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Loop tersebut mencetak jalur lengkap setiap dokumen yang berisi istilah dengan kecocokan huruf yang tepat.

## Cara menambahkan dokumen ke indeks – Pencarian Kuery Objek

Kuery objek memberi Anda fleksibilitas lebih, terutama ketika Anda perlu menggabungkan beberapa kriteria.

### Langkah 1: Inisialisasi indeks kedua (opsional)
Jika Anda lebih suka memisahkan pencarian berbasis objek, buat folder indeks lain.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Langkah 2: Gunakan kembali opsi sensitif huruf
Instansi `SearchOptions` yang sama dapat dipakai untuk kueri objek.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Langkah 3: Bangun dan jalankan kueri objek
Buat objek kueri kata dan berikan ke mesin pencari.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Menggunakan `createWordQuery` memungkinkan Anda menggabungkannya nanti dengan kueri frasa, wildcard, atau Boolean untuk skenario yang lebih kompleks.

## Aplikasi Praktis
- **Manajemen Dokumen Hukum:** Mengambil undang‑undang spesifik kasus di mana kapitalisasi penting.  
- **Platform E‑commerce:** Membedakan SKU produk seperti “PRO‑X” vs. “pro‑x”.  
- **Sistem Manajemen Konten (CMS):** Memastikan penulis menemukan judul atau tag yang tepat.

## Pertimbangan Kinerja
- **Jaga indeks tetap terbaru** – lakukan re‑indeks ketika file baru ditambahkan atau yang lama diubah.  
- **Pantau penggunaan memori** – korpus besar mendapat manfaat dari indeks inkremental dan penyesuaian ukuran heap JVM yang tepat.  
- **Manfaatkan garbage collector Java** – lepaskan objek `Index` ketika tidak lagi diperlukan.

## Masalah Umum dan Solusinya
| Masalah | Solusi |
|-------|----------|
| `useCaseSensitiveSearch` tampak diabaikan | Pastikan Anda menggunakan versi GroupDocs.Search terbaru dan indeks dibangun ulang setelah mengubah opsi. |
| Tidak ada hasil untuk istilah yang diketahui | Pastikan kapitalisasi istilah cocok persis dan dokumen berhasil ditambahkan ke indeks. |
| Pencarian di banyak folder menjadi lambat | Tambahkan setiap folder secara terpisah dengan `index.add()` dan pertimbangkan membagi indeks menjadi shard untuk dataset sangat besar. |

## Pertanyaan yang Sering Diajukan

**T:** Bagaimana cara menangani dataset besar dengan GroupDocs.Search?  
**J:** Manfaatkan partisi indeks, sesuaikan pengaturan memori JVM, dan secara periodik kompak indeks untuk menjaga kinerja optimal.

**T:** Bisakah saya mencari di beberapa direktori secara bersamaan?  
**J:** Ya – panggil `index.add()` untuk setiap direktori yang ingin Anda sertakan, lalu jalankan satu kueri terhadap indeks gabungan.

**T:** Apa jebakan umum saat menyiapkan pencarian sensitif huruf?  
**J:** Lupa membangun ulang indeks setelah mengaktifkan `useCaseSensitiveSearch`, atau menggunakan kapitalisasi yang salah pada string kueri.

**T:** Bagaimana cara memecahkan masalah kesalahan pencarian?  
**J:** Periksa file log yang dihasilkan oleh GroupDocs.Search untuk jejak stack, dan pastikan semua dependensi Maven terresolusi dengan benar.

**T:** Apakah GroupDocs.Search cocok untuk aplikasi waktu‑nyata?  
**J:** Dengan strategi indeks yang tepat (pembaruan inkremental dan caching dalam memori), ia dapat memberikan hasil pencarian hampir secara waktu‑nyata.

## Sumber Daya
- **Dokumentasi:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **Referensi API:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Unduhan:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **Repositori GitHub:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Forum Dukungan:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Lisensi Sementara:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-02-06  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs