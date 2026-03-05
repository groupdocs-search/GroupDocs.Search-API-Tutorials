---
date: '2026-02-19'
description: Pelajari cara menonaktifkan stop words dalam pencarian dan menambahkan
  dokumen ke indeks dengan GroupDocs.Search untuk Java, meningkatkan akurasi kueri.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Kata Henti dalam Pencarian: Tambahkan Dokumen ke Indeks dengan GroupDocs.Search
  Java'
type: docs
url: /id/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Stop Words dalam Pencarian: Tambahkan Dokumen ke Indeks dengan GroupDocs.Search Java

Jika Anda perlu **menambahkan dokumen ke indeks** sambil memastikan bahwa tidak ada istilah penting—terutama yang umum—yang diabaikan, Anda berada di tempat yang tepat. Dalam panduan ini kami akan menunjukkan cara **menonaktifkan stop words dalam pencarian** menggunakan GroupDocs.Search untuk Java, sehingga setiap token (bahkan “on”, “by”, atau “the”) menjadi dapat dicari dan hasil Anda jauh lebih akurat.

## Jawaban Cepat
- **Apa arti “menambahkan dokumen ke indeks”?** Artinya memuat file sumber Anda ke dalam indeks yang dapat dicari sehingga dapat dipertanyakan secara efisien.  
- **Mengapa saya harus menonaktifkan stop words?** Untuk menyertakan kata umum (misalnya “on”, “the”) dalam pencarian ketika istilah tersebut bermakna bagi domain Anda.  
- **Versi perpustakaan apa yang diperlukan?** GroupDocs.Search untuk Java 25.4 atau yang lebih baru.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Bisakah saya menggunakan ini dalam proyek Maven?** Ya – cukup tambahkan repositori dan dependensi yang ditunjukkan di bawah ini.

## Apa itu stop words dalam pencarian dan mengapa Anda mungkin ingin menonaktifkannya?
Stop words adalah istilah yang sering muncul yang banyak mesin pencari secara otomatis saring untuk mempercepat kueri. Meskipun ini meningkatkan kinerja untuk pencarian web umum, hal itu dapat menurunkan presisi dalam domain khusus—kontrak hukum, katalog e‑commerce, atau manual teknis—di mana kata seperti “on”, “by”, atau “as” memiliki makna nyata. Menonaktifkan stop words memungkinkan Anda memperlakukan setiap kata sebagai signifikan, memastikan tidak ada dokumen relevan yang terlewat.

## Bagaimana cara kerja penambahan dokumen ke indeks di GroupDocs.Search?
Saat Anda menambahkan dokumen, perpustakaan membaca setiap file, melakukan tokenisasi kontennya, dan menyimpan token-token tersebut dalam struktur data yang dioptimalkan (indeks). Setelah diindeks, mesin dapat mengambil dokumen yang cocok dalam hitungan milidetik, bahkan untuk koleksi yang besar.

## Prasyarat

- **Perpustakaan yang Diperlukan**: GroupDocs.Search untuk Java 25.4 (atau yang lebih baru).  
- **Lingkungan Pengembangan**: IntelliJ IDEA, Eclipse, atau IDE Java apa pun yang Anda sukai.  
- **Pengetahuan Dasar**: Familiaritas dengan sintaks Java dan konsep pengindeksan.

## Menyiapkan GroupDocs.Search untuk Java

### Instalasi Maven

Jika Anda menggunakan Maven, sertakan berikut ini dalam `pom.xml` Anda:

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

Sebagai alternatif, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Langkah-langkah Akuisisi Lisensi
- **Percobaan Gratis** – mulai menguji segera.  
- **Lisensi Sementara** – dapatkan kunci berjangka waktu untuk fungsionalitas penuh.  
- **Pembelian** – amankan lisensi permanen untuk penggunaan produksi.

## Inisialisasi dan Pengaturan Dasar

Buat sebuah instance `IndexSettings` untuk mengontrol cara kerja indeks:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Cara menonaktifkan stop words dalam pencarian (Java)

Baris berikut mematikan filter stop‑word bawaan:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parameter*: `setUseStopWords` menerima nilai boolean.  
*Tujuan*: Menjamin setiap kata—termasuk stop words umum—diindeks dan dapat dicari.

## Cara menambahkan dokumen ke indeks

### Menentukan Direktori Output

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Menentukan Direktori Dokumen

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Sekarang setiap file di `YOUR_DOCUMENT_DIRECTORY` **ditambahkan dokumen ke indeks** dan siap untuk dipertanyakan.

## Melakukan Kueri Pencarian

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Karena stop words dinonaktifkan, istilah `"on"` akan dipertimbangkan selama pencarian, mengembalikan hasil yang sebaliknya akan diabaikan.

## Aplikasi Praktis

1. **Pencarian Dokumen Perusahaan** – Pastikan terminologi penting tidak disaring.  
2. **Platform E‑commerce** – Tingkatkan penemuan produk dengan mengindeks setiap kata dalam deskripsi produk.  
3. **Alat Riset Hukum** – Tangkap setiap istilah hukum, bahkan yang biasanya diperlakukan sebagai stop words.

## Pertimbangan Kinerja

- **Tips Optimasi**: Secara rutin perbarui dan pangkas indeks Anda untuk menjaga kecepatan pencarian tetap tinggi.  
- **Penggunaan Sumber Daya**: Pantau ukuran heap JVM; indeks besar mungkin memerlukan penyesuaian pengaturan garbage collection.  
- **Manajemen Memori Java**: Gunakan struktur data yang efisien dan pertimbangkan penyimpanan off‑heap untuk korpus yang sangat besar.

## Masalah Umum dan Solusinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---|---|---|
| Tidak ada hasil untuk kata umum | `setUseStopWords(true)` (default) | Panggil `setUseStopWords(false)` seperti yang ditunjukkan di atas. |
| Kesalahan out‑of‑memory saat mengindeks | Mengindeks terlalu banyak file besar sekaligus | Indeks file secara batch; tingkatkan opsi JVM `-Xmx`. |
| Pencarian mengembalikan data usang | Indeks tidak diperbarui setelah menambahkan file baru | Panggil `index.update()` atau tambahkan kembali dokumen yang berubah. |

## Pertanyaan yang Sering Diajukan

**T: Apa itu stop words?**  
J: Stop words adalah istilah umum (misalnya “the”, “is”, “on”) yang banyak mesin pencari abaikan untuk mempercepat kueri. Menonaktifkannya memungkinkan Anda memperlakukan setiap token sebagai dapat dicari.

**T: Mengapa menonaktifkan stop words dalam indeks pencarian?**  
J: Ketika pencocokan frasa tepat diperlukan—seperti pada dokumen hukum atau teknis—setiap kata memiliki makna, sehingga Anda harus menyertakan stop words.

**T: Bagaimana GroupDocs.Search menangani dataset besar?**  
J: Perpustakaan menggunakan struktur data yang dioptimalkan dan pengindeksan inkremental untuk menjaga penggunaan memori tetap rendah, bahkan dengan jutaan dokumen.

**T: Bisakah saya mengintegrasikan GroupDocs.Search dengan aplikasi Java lain?**  
J: Ya, API dirancang untuk mudah disematkan ke sistem berbasis Java apa pun, mulai dari layanan web hingga aplikasi desktop.

**T: Apa yang harus saya lakukan jika hasil pencarian tidak akurat?**  
J: Pastikan indeks mencakup semua dokumen yang diperlukan (`add documents to index`), pastikan filter stop‑word dinonaktifkan bila diperlukan, dan pertimbangkan membangun ulang indeks setelah perubahan besar.

## Sumber Daya Tambahan

- **Dokumentasi**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Referensi API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Unduhan**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **Repositori GitHub**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Dukungan Gratis**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Lisensi Sementara**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Dengan mengikuti panduan ini, Anda kini tahu cara **menambahkan dokumen ke indeks** dan **menonaktifkan stop words dalam pencarian** untuk memberikan hasil yang lebih akurat dalam aplikasi Java Anda.

---

**Terakhir Diperbarui:** 2026-02-19  
**Diuji Dengan:** GroupDocs.Search untuk Java 25.4  
**Penulis:** GroupDocs  

---