---
date: '2026-01-06'
description: Pelajari cara menambahkan dokumen ke indeks dan mencari dokumen berdasarkan
  metadata dengan GroupDocs.Search Java. Kuasai pengaturan indeks, buat indeks, tambahkan
  dokumen, dan lakukan pencarian yang tepat.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: Cara menambahkan dokumen ke indeks dengan Pengindeksan Metadata di Java menggunakan
  GroupDocs.Search
type: docs
url: /id/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Cara menambahkan dokumen ke indeks dengan Metadata Indexing di Java menggunakan GroupDocs.Search

Dalam aplikasi modern, **menambahkan dokumen ke indeks** dengan cepat dan dapat diandalkan sangat penting untuk memberikan pengalaman pencarian yang cepat. Baik Anda membangun repositori hukum, basis pengetahuan dukungan pelanggan, atau portal dokumen internal, memanfaatkan metadata memungkinkan **mencari dokumen berdasarkan metadata** seperti penulis, judul, atau tag khusus. Panduan ini memandu Anda melalui proses lengkap—mengonfigurasi pengaturan indeks, membuat indeks yang berfokus pada metadata, menambahkan file Anda, dan menjalankan pencarian yang kuat—semua dengan GroupDocs.Search untuk Java.

## Jawaban Cepat
- **Apa tujuan utama metadata indexing?** Ini memungkinkan pencarian cepat berdasarkan properti dokumen bukan konten teks penuh.  
- **Metode mana yang menambahkan file ke indeks?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Apakah saya dapat mencari berdasarkan bidang metadata khusus?** Ya, setelah bidang tersebut diindeks Anda dapat menanyakan mereka secara langsung.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi percobaan sementara sudah cukup untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi disarankan.

## Apa itu metadata indexing di GroupDocs.Search?
Metadata indexing mengekstrak dan menyimpan atribut dokumen (misalnya, penulis, tanggal pembuatan, tag khusus) dalam struktur yang dapat dicari. Ketika Anda **menambahkan dokumen ke indeks**, mesin mencatat atribut-atribut ini, memungkinkan Anda menjalankan kueri yang tepat seperti “temukan semua PDF yang ditulis oleh *John Doe*”.

## Mengapa menggunakan GroupDocs.Search untuk metadata indexing?
- **Kinerja:** Pencarian metadata ringan dan mengembalikan hasil dalam milidetik.  
- **Fleksibilitas:** Mendukung berbagai format file (PDF, DOCX, PPT, dll.).  
- **Skalabilitas:** Menangani jutaan dokumen dengan jejak memori minimal.  

## Prasyarat
- GroupDocs.Search untuk Java ≥ 25.4.  
- JDK 8 atau yang lebih baru terpasang dan dikonfigurasi.  
- Familiaritas dasar dengan Java dan Maven.  

## Menyiapkan GroupDocs.Search untuk Java

### Instruksi Instalasi
Tambahkan repositori GroupDocs dan dependensi ke `pom.xml` Anda:

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

Anda juga dapat mengunduh binary terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Untuk mendapatkan lisensi sementara untuk pengujian:

1. Kunjungi situs web GroupDocs dan buka bagian **Purchase**.  
2. Pilih paket **temporary license** yang sesuai dengan kebutuhan evaluasi Anda.  

## Implementasi Langkah‑per‑Langkah

### Fitur 1: Konfigurasi Pengaturan Indeks
Konfigurasikan indeks untuk fokus pada metadata:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` memberi tahu mesin untuk memprioritaskan metadata dibandingkan konten teks penuh.

### Fitur 2: Membuat Indeks di Folder yang Ditentukan
Buat direktori indeks fisik tempat semua metadata akan disimpan:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Ganti `YOUR_DOCUMENT_DIRECTORY` dengan jalur yang sesuai dengan tata letak proyek Anda.

### Fitur 3: Cara menambahkan dokumen ke indeks
Sekarang indeks sudah ada, Anda dapat **menambahkan dokumen ke indeks** sehingga mereka dapat dicari:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tips:**  
- Verifikasi bahwa jalur folder sudah benar dan aplikasi memiliki izin baca.  
- GroupDocs.Search secara otomatis mengekstrak metadata yang didukung dari setiap file.

### Fitur 4: Mencari dokumen berdasarkan metadata
Jalankan kueri yang menargetkan bidang metadata, misalnya mencari dokumen di mana bahasa adalah English:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

- `search(query)` mencari melalui metadata yang diindeks dan mengembalikan dokumen yang cocok.

## Aplikasi Praktis
1. **Enterprise Document Management:** Mengambil kontrak berdasarkan tanggal kontrak atau nama penandatangan.  
2. **Digital Library Catalogs:** Membiarkan pengguna menelusuri buku berdasarkan genre, tahun publikasi, atau penulis.  
3. **CRM Systems:** Dengan cepat menemukan file klien menggunakan metadata khusus seperti ID pelanggan atau wilayah.  

## Pertimbangan Kinerja
- **Incremental Updates:** Gunakan `index.addOrUpdate()` untuk file baru atau yang berubah alih-alih membangun ulang seluruh indeks.  
- **Memory Tuning:** Sesuaikan ukuran heap JVM (`-Xmx`) berdasarkan volume metadata yang diindeks.  
- **Optimized Storage:** Secara berkala panggil `index.optimize()` untuk memadatkan indeks dan meningkatkan kecepatan kueri.

## Masalah Umum dan Solusinya

| Masalah | Solusi |
|-------|----------|
| **Tidak ada hasil yang dikembalikan** | Konfirmasi bahwa bidang metadata yang Anda harapkan memang ada dalam file sumber. |
| **Kesalahan izin** | Pastikan proses Java memiliki akses baca ke folder dokumen dan direktori indeks. |
| **Kesalahan out‑of‑memory** | Tingkatkan ukuran heap JVM atau proses batch operasi `add` untuk memproses file dalam kelompok yang lebih kecil. |

## Pertanyaan yang Sering Diajukan

**Q: Apa itu metadata indexing?**  
A: Metadata indexing menyimpan atribut dokumen (penulis, judul, tag khusus) dalam struktur yang dapat dicari, memungkinkan pencarian cepat tanpa memindai teks penuh.

**Q: Bagaimana cara mendapatkan lisensi sementara?**  
A: Kunjungi halaman pembelian GroupDocs dan ikuti langkah-langkah untuk memperoleh lisensi percobaan.

**Q: Bisakah saya mengindeks PDF dengan pengaturan ini?**  
A: Ya, GroupDocs.Search mendukung PDF, DOCX, PPT, dan banyak format lainnya.

**Q: Apa masalah umum saat menambahkan dokumen?**  
A: Verifikasi jalur file yang benar dan pastikan aplikasi memiliki izin baca untuk direktori.

**Q: Bagaimana cara mengoptimalkan kinerja pencarian?**  
A: Secara teratur perbarui indeks Anda, gunakan penambahan inkremental, dan sesuaikan pengaturan memori JVM.

## Sumber Daya

- **Documentation:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-01-06  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs