---
date: '2026-02-21'
description: Pelajari cara menambahkan dokumen ke indeks dan meningkatkan kinerja
  pencarian dengan pencarian berbasis chunk di Java menggunakan GroupDocs.Search,
  mengoptimalkan memori indeks pencarian Java untuk kumpulan dokumen besar.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Tambahkan dokumen ke indeks dengan pencarian berbasis potongan di Java
type: docs
url: /id/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Tambahkan dokumen ke indeks dengan pencarian berbasis chunk dalam Java

Dalam aplikasi modern yang perlu **add documents to index** dengan cepat dan kemudian melakukan kueri berbasis chunk yang cepat, Anda akan menginginkan solusi yang dapat diskalakan tanpa membebani memori. Tutorial ini memandu Anda menyiapkan GroupDocs.Search untuk Java, menambahkan beberapa folder dokumen, dan mengonfigurasi mesin untuk **increase search performance** sambil menjaga penggunaan **java search index memory** tetap terkendali. Apakah Anda mengindeks kontrak hukum, tiket dukungan, atau makalah penelitian, langkah‑langkah di bawah ini akan memberi Anda implementasi siap produksi.

## Jawaban Cepat
- **Apa langkah pertama?** Buat folder indeks pencarian.  
- **Bagaimana cara saya memasukkan banyak file?** Gunakan `index.add()` untuk setiap folder dokumen.  
- **Opsi mana yang mengaktifkan pencarian chunk?** `options.setChunkSearch(true)`.  
- **Apakah saya dapat melanjutkan pencarian setelah chunk pertama?** Ya, panggil `index.searchNext()` dengan token.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis atau lisensi sementara dapat digunakan untuk pengembangan; lisensi penuh diperlukan untuk produksi.  

## Apa yang Akan Anda Pelajari
- Cara membuat indeks pencarian di folder yang ditentukan.  
- Langkah‑langkah untuk **add documents to index** dari beberapa lokasi.  
- Mengonfigurasi opsi pencarian untuk mengaktifkan pencarian berbasis chunk.  
- Melakukan pencarian berbasis chunk awal dan selanjutnya.  
- Skenario dunia nyata di mana pencarian dokumen berbasis chunk bersinar.  

## Prasyarat
- **Required Libraries**: GroupDocs.Search untuk Java 25.4 atau lebih baru.  
- **Environment Setup**: Java Development Kit (JDK) yang kompatibel terpasang.  
- **Knowledge Prerequisites**: Pemrograman Java dasar dan familiaritas dengan Maven.  

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
- **Free Trial** – menguji fitur inti tanpa komitmen.  
- **Temporary License** – akses tambahan untuk pengembangan.  
- **Purchase** – lisensi penuh untuk penggunaan produksi.  

### Inisialisasi dan Penyiapan Dasar
Buat indeks di folder tempat Anda ingin data yang dapat dicari berada:

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
Sekarang indeks sudah ada, langkah logis berikutnya adalah **add documents to index** dari lokasi tempat file Anda disimpan.

### 1. Membuat Indeks
**Overview**: Siapkan direktori untuk indeks pencarian.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Menambahkan Dokumen ke Indeks
**Overview**: Mengambil file dari beberapa folder sumber.

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

### 3. Mengonfigurasi Opsi Pencarian untuk Pencarian Chunk
Aktifkan pencarian berbasis chunk dengan menyesuaikan objek opsi.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Melakukan Pencarian Chunk‑Berbasis Awal
Jalankan kueri pertama menggunakan opsi yang mengaktifkan chunk.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Melanjutkan Pencarian Chunk‑Berbasis
Iterasi melalui chunk yang tersisa sampai pencarian selesai.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Mengapa menggunakan pencarian berbasis chunk?
Pencarian berbasis chunk memecah koleksi dokumen besar menjadi bagian yang dapat dikelola, mengurangi tekanan memori dan mempercepat waktu respons. Ini sangat bermanfaat ketika:
1. **Legal teams** perlu menemukan klausa spesifik di antara ribuan kontrak.  
2. **Customer support portals** harus menampilkan artikel basis pengetahuan yang relevan secara instan.  
3. **Researchers** menyaring dataset yang luas tanpa memuat seluruh file ke memori.  

## Bagaimana pendekatan ini **increases search performance**
Dengan mencari chunk yang lebih kecil daripada seluruh file, mesin dapat:
- Melewati bagian yang tidak relevan lebih awal, mengurangi siklus CPU.  
- Menyimpan hanya chunk aktif di memori, yang secara langsung menurunkan konsumsi **java search index memory**.  
- Paralelisasi pemrosesan chunk pada mesin multi‑core untuk hasil yang lebih cepat.  

## Mengelola **java search index memory**
Meskipun pencarian berbasis chunk sudah mengurangi jejak memori, Anda dapat menyesuaikan JVM lebih lanjut:
- Alokasikan heap yang cukup (`-Xmx2g` atau lebih) berdasarkan ukuran indeks.  
- Gunakan `index.optimize()` setelah penambahan massal untuk mengompresi struktur indeks.  
- Pantau jeda GC dengan alat seperti VisualVM untuk menghindari lonjakan latensi.  

## Pertimbangan Kinerja
- **Memory Management** – Alokasikan ruang heap yang cukup (`-Xmx`) untuk indeks besar.  
- **Resource Monitoring** – Pantau penggunaan CPU selama operasi pengindeksan dan pencarian.  
- **Index Maintenance** – Secara berkala bangun kembali atau bersihkan indeks untuk membuang data usang.  

## Kesalahan Umum & Pemecahan Masalah
| Masalah | Mengapa Terjadi | Perbaikan |
|-------|----------------|-----|
| `OutOfMemoryError` selama pengindeksan | Ukuran heap terlalu kecil | Tingkatkan heap JVM (`-Xmx2g` atau lebih tinggi) |
| Tidak ada hasil yang dikembalikan | Token chunk tidak diproses | Pastikan loop `while` berjalan hingga `getNextChunkSearchToken()` menjadi `null` |
| Kinerja pencarian lambat | Indeks tidak dioptimalkan | Jalankan `index.optimize()` setelah penambahan massal |

## Pertanyaan yang Sering Diajukan

**Q: Apa itu pencarian berbasis chunk?**  
A: Pencarian berbasis chunk membagi dataset menjadi bagian‑bagian yang lebih kecil, memungkinkan kueri yang efisien pada volume data yang besar tanpa memuat seluruh dokumen ke memori.

**Q: Bagaimana cara memperbarui indeks saya dengan file baru?**  
A: Cukup panggil `index.add()` dengan jalur ke dokumen baru; indeks akan menggabungkannya secara otomatis.

**Q: Apakah GroupDocs.Search dapat menangani berbagai format file?**  
A: Ya, ia mendukung PDF, DOCX, XLSX, PPTX, dan banyak format umum lainnya.

**Q: Apa saja bottleneck kinerja yang umum?**  
A: Kendala memori dan indeks yang tidak dioptimalkan adalah yang paling umum; alokasikan heap yang cukup dan secara rutin optimalkan indeks.

**Q: Di mana saya dapat menemukan dokumentasi yang lebih detail?**  
A: Kunjungi [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) resmi untuk panduan mendalam dan referensi API.

**Q: Apakah pencarian berbasis chunk bekerja dengan PDF terenkripsi?**  
A: Ya, selama Anda menyediakan kata sandi melalui overload API yang sesuai.

**Q: Bagaimana saya dapat memantau kemajuan pengindeksan?**  
A: Gunakan overload `Index.add()` yang mengembalikan objek `Progress` atau hubungkan ke callback logging.

## Sumber Daya
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Terakhir Diperbarui:** 2026-02-21  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs  

---