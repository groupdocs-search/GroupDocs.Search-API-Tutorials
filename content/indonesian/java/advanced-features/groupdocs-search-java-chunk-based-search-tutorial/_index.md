---
date: '2025-12-19'
description: Pelajari cara menambahkan dokumen ke indeks dan mengaktifkan pencarian
  berbasis potongan di Java menggunakan GroupDocs.Search, meningkatkan kinerja untuk
  kumpulan dokumen besar.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Tambahkan dokumen ke indeks dengan pencarian berbasis potongan di Java
type: docs
url: /id/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Tambahkan dokumen ke indeks dengan pencarian berbasis potongan di Java

Di dunia yang didorong oleh data saat ini, kemampuan untuk **menambahkan dokumen ke indeks** dengan cepat dan kemudian melakukan pencarian berbasis potongan sangat penting bagi aplikasi apa pun yang menangani koleksi file besar. Baik Anda menangani kontrak hukum, arsip dukungan pelanggan, atau perpustakaan riset masif, tutorial ini menunjukkan secara tepat cara menyiapkan GroupDocs.Search untuk Java sehingga Anda dapat mengindeks dokumen secara efisien dan mengambil informasi relevan dalam potongan‑potongan kecil.

## Apa yang Akan Anda Pelajari
- Cara membuat indeks pencarian di folder yang ditentukan.  
- Langkah‑langkah untuk **menambahkan dokumen ke indeks** dari beberapa lokasi.  
- Mengonfigurasi opsi pencarian untuk mengaktifkan pencarian berbasis potongan.  
- Melakukan pencarian berbasis potongan awal dan selanjutnya.  
- Skenario dunia nyata di mana pencarian dokumen berbasis potongan bersinar.

## Jawaban Cepat
- **Apa langkah pertama?** Buat folder indeks pencarian.  
- **Bagaimana cara menyertakan banyak file?** Gunakan `index.add()` untuk setiap folder dokumen.  
- **Opsi mana yang mengaktifkan pencarian potongan?** `options.setChunkSearch(true)`.  
- **Apakah saya dapat melanjutkan pencarian setelah potongan pertama?** Ya, panggil `index.searchNext()` dengan tokennya.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan gratis atau lisensi sementara cukup untuk pengembangan; lisensi penuh diperlukan untuk produksi.

## Prasyarat
Untuk mengikuti panduan ini, pastikan Anda memiliki:

- **Pustaka yang Diperlukan**: GroupDocs.Search untuk Java 25.4 atau yang lebih baru.  
- **Pengaturan Lingkungan**: Java Development Kit (JDK) yang kompatibel terpasang.  
- **Prasyarat Pengetahuan**: Pemrograman Java dasar dan familiaritas dengan Maven.

## Menyiapkan GroupDocs.Search untuk Java
Untuk memulai, integrasikan GroupDocs.Search ke dalam proyek Anda menggunakan Maven:

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

Atau, unduh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Untuk mencoba GroupDocs.Search:

- **Percobaan Gratis** – uji fitur inti tanpa komitmen.  
- **Lisensi Sementara** – akses diperpanjang untuk pengembangan.  
- **Pembelian** – lisensi penuh untuk penggunaan produksi.

### Inisialisasi dan Penyiapan Dasar
Buat indeks di folder tempat Anda ingin data yang dapat dicari disimpan:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Cara menambahkan dokumen ke indeks
Sekarang indeks sudah ada, langkah logis berikutnya adalah **menambahkan dokumen ke indeks** dari lokasi tempat file Anda disimpan.

### 1. Membuat Indeks
**Gambaran Umum**: Siapkan direktori untuk indeks pencarian.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Menambahkan Dokumen ke Indeks
**Gambaran Umum**: Tarik file dari beberapa folder sumber.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Mengonfigurasi Opsi Pencarian untuk Pencarian Potongan
Aktifkan pencarian berbasis potongan dengan menyesuaikan objek opsi.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Melakukan Pencarian Berbasis Potongan Awal
Jalankan kueri pertama menggunakan opsi yang telah diaktifkan untuk potongan.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Melanjutkan Pencarian Berbasis Potongan
Iterasi melalui potongan yang tersisa hingga pencarian selesai.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Mengapa menggunakan pencarian berbasis potongan?
Pencarian berbasis potongan memecah koleksi dokumen besar menjadi bagian‑bagian yang dapat dikelola, mengurangi tekanan memori dan mempercepat waktu respons. Ini sangat bermanfaat ketika:

1. **Tim hukum** perlu menemukan klausa spesifik di antara ribuan kontrak.  
2. **Portal dukungan pelanggan** harus menampilkan artikel basis pengetahuan yang relevan secara instan.  
3. **Peneliti** menyaring dataset ekstensif tanpa harus memuat seluruh file ke memori.

## Pertimbangan Kinerja
- **Manajemen Memori** – Alokasikan ruang heap yang cukup (`-Xmx`) untuk indeks besar.  
- **Pemantauan Sumber Daya** – Pantau penggunaan CPU selama proses pengindeksan dan pencarian.  
- **Pemeliharaan Indeks** – Secara periodik bangun ulang atau bersihkan indeks untuk membuang data usang.

## Kesalahan Umum & Pemecahan Masalah
| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| `OutOfMemoryError` selama pengindeksan | Ukuran heap terlalu kecil | Tingkatkan heap JVM (`-Xmx2g` atau lebih tinggi) |
| Tidak ada hasil yang dikembalikan | Token potongan tidak diproses | Pastikan loop `while` berjalan hingga `getNextChunkSearchToken()` menjadi `null` |
| Kinerja pencarian lambat | Indeks tidak dioptimalkan | Jalankan `index.optimize()` setelah penambahan massal |

## Pertanyaan yang Sering Diajukan

**T: Apa itu pencarian berbasis potongan?**  
J: Pencarian berbasis potongan membagi dataset menjadi bagian‑bagian lebih kecil, memungkinkan kueri yang efisien pada volume data besar tanpa harus memuat seluruh dokumen ke memori.

**T: Bagaimana cara memperbarui indeks dengan file baru?**  
J: Cukup panggil `index.add()` dengan path ke dokumen baru; indeks akan secara otomatis memasukkannya.

**T: Bisakah GroupDocs.Search menangani berbagai format file?**  
J: Ya, mendukung PDF, DOCX, XLSX, PPTX, dan banyak format umum lainnya.

**T: Apa saja bottleneck kinerja yang umum?**  
J: Kendala memori dan indeks yang tidak dioptimalkan adalah yang paling umum; alokasikan heap yang cukup dan optimalkan indeks secara teratur.

**T: Di mana saya dapat menemukan dokumentasi lebih detail?**  
J: Kunjungi [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) resmi untuk panduan mendalam dan referensi API.

## Sumber Daya
- **Dokumentasi**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Referensi API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Unduhan**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Dukungan Gratis**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Lisensi Sementara**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Terakhir Diperbarui:** 2025-12-19  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs  

---