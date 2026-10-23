---
date: '2026-10-22'
description: Pelajari cara melakukan pencarian metadata dengan GroupDocs di Java,
  mengonfigurasi index settings, menambahkan documents, dan query by metadata fields
  secara efisien.
keywords:
- metadata search with groupdocs
- metadata indexing java
- groupdocs search java
lastmod: '2026-10-22'
og_description: Pelajari cara melakukan pencarian metadata dengan GroupDocs di Java,
  mengonfigurasi index settings, menambahkan documents, dan query by metadata fields
  secara efisien.
og_image_alt: Guide showing Java code for metadata indexing using GroupDocs.Search
og_title: Cara melakukan pencarian metadata dengan GroupDocs di Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-22'
  description: Learn how to perform metadata search with GroupDocs in Java, configure
    index settings, add documents, and query by metadata fields efficiently.
  headline: How to do metadata search with GroupDocs in Java
  type: TechArticle
- description: Learn how to perform metadata search with GroupDocs in Java, configure
    index settings, add documents, and query by metadata fields efficiently.
  name: How to do metadata search with GroupDocs in Java
  steps:
  - name: Visit the GroupDocs website and go to the **Purchase** section.
    text: Visit the GroupDocs website and go to the **Purchase** section.
  - name: Choose a **temporary license** plan that matches your evaluation needs.
    text: Choose a **temporary license** plan that matches your evaluation needs.
  - name: '**Enterprise document management:** Retrieve contracts by contract date
      or signatory name.'
    text: '**Enterprise document management:** Retrieve contracts by contract date
      or signatory name.'
  - name: '**Digital library catalogs:** Let users browse books by genre, publication
      year, or author.'
    text: '**Digital library catalogs:** Let users browse books by genre, publication
      year, or author.'
  - name: '**CRM systems:** Quickly locate client files using custom metadata like
      customer ID or region.'
    text: '**CRM systems:** Quickly locate client files using custom metadata like
      customer ID or region.'
  type: HowTo
- questions:
  - answer: Metadata indexing stores document attributes (author, title, custom tags)
      in a searchable structure, enabling fast look‑ups without scanning full text.
    question: What is metadata indexing?
  - answer: Visit the GroupDocs purchase page and follow the steps to acquire a trial
      license.
    question: How do I obtain a temporary license?
  - answer: Yes, GroupDocs.Search supports PDF, DOCX, PPT, and many other formats.
    question: Can I index PDFs with this setup?
  - answer: Verify correct file paths and ensure the application has read permissions
      for the directories.
    question: What are common issues when adding documents?
  - answer: Regularly update your index, use incremental adds, and tune JVM memory
      settings.
    question: How do I optimize search performance?
  type: FAQPage
tags:
- metadata search
- GroupDocs
- Java indexing
title: Cara melakukan pencarian metadata dengan GroupDocs di Java
type: docs
url: /id/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Cara melakukan pencarian metadata dengan GroupDocs di Java

Menambahkan dokumen ke indeks dengan cepat dan andal adalah tulang punggung setiap aplikasi modern yang didorong oleh pencarian. Baik Anda membangun repositori hukum, basis pengetahuan dukungan pelanggan, atau portal dokumen internal, **metadata search with GroupDocs** memungkinkan Anda menemukan file berdasarkan penulis, judul, atau tag khusus apa pun tanpa memindai konten teks penuh. Dalam tutorial ini Anda akan belajar cara mengonfigurasi pengaturan indeks, membuat indeks yang berfokus pada metadata, menambahkan file Anda, dan menjalankan pencarian yang tepat—semua dengan GroupDocs.Search untuk Java.

## Jawaban Cepat
- **Apa tujuan utama pengindeksan metadata?** Itu memungkinkan pencarian cepat berdasarkan properti dokumen daripada konten teks penuh.  
- **Metode mana yang menambahkan file ke indeks?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Apakah saya dapat mencari berdasarkan bidang metadata khusus?** Ya, setelah bidang tersebut diindeks Anda dapat menanyakan mereka secara langsung.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi percobaan sementara cukup untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi disarankan.

## Apa itu pengindeksan metadata di GroupDocs.Search?
Pengindeksan metadata mengekstrak dan menyimpan atribut dokumen (mis., penulis, tanggal pembuatan, tag khusus) dalam struktur yang dapat dicari. Ketika Anda **menambahkan dokumen ke indeks**, mesin mencatat atribut-atribut ini, memungkinkan Anda menjalankan kueri yang tepat seperti “temukan semua PDF yang ditulis oleh *John Doe*” atau “cari PDF berdasarkan penulis”.

## Mengapa menggunakan GroupDocs.Search untuk pengindeksan metadata?
Pencarian metadata dengan GroupDocs memberikan waktu respons ringan, kurang dari satu detik bahkan ketika indeks berisi jutaan catatan. Ini mendukung **lebih dari 30 format input dan output**—termasuk PDF, DOCX, PPTX, HTML, dan file gambar—dan menggunakan kurang dari 200 MB memori heap untuk indeks 100 000 dokumen pada server tipikal.

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

Anda juga dapat mengunduh binari terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Untuk mendapatkan lisensi sementara untuk pengujian:

1. Kunjungi situs web GroupDocs dan buka bagian **Purchase**.  
2. Pilih paket **temporary license** yang sesuai dengan kebutuhan evaluasi Anda.  

## Cara mengonfigurasi pengaturan indeks untuk metadata?
Mengonfigurasi pengaturan indeks memberi tahu mesin informasi apa yang akan diekstrak dan disimpan. Dengan mengatur tipe indeks ke `MetadataIndex`, Anda menginstruksikan GroupDocs.Search untuk fokus pada bidang metadata daripada konten teks penuh, yang mengurangi ukuran indeks dan mempercepat kueri. Konfigurasi ini diterapkan melalui objek `IndexSettings`, di mana Anda juga dapat menentukan bidang metadata khusus yang akan diindeks.

```text
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);
```

## Fitur 1: konfigurasi pengaturan indeks
Pemanggilan `setIndexType(IndexType.MetadataIndex)` memberi tahu mesin untuk fokus pada metadata daripada konten teks penuh. **`IndexType.MetadataIndex`** adalah nilai enumerasi yang memilih mode pengindeksan hanya metadata.

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

## Fitur 2: membuat indeks di folder yang ditentukan
Buat direktori indeks fisik di mana semua metadata akan disimpan:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Ganti `YOUR_DOCUMENT_DIRECTORY` dengan jalur yang sesuai dengan tata letak proyek Anda.

## Fitur 3: Cara menambahkan dokumen ke indeks
Metode `index.add` menambahkan file dari folder ke indeks dan mengekstrak metadata mereka. **`index.add`** memindai setiap dokumen, membaca bidang metadata yang didukung, dan menyimpannya di indeks untuk pengambilan cepat.

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tips:**  
- Pastikan jalur folder benar dan aplikasi memiliki izin baca.  
- GroupDocs.Search secara otomatis mengekstrak metadata yang didukung dari setiap file.

## Fitur 4: Mencari dokumen berdasarkan metadata
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

Metode `search(query)` mencari melalui metadata yang diindeks dan mengembalikan dokumen yang cocok. Anda juga dapat **search pdf by author** dengan menggunakan nama penulis sebagai string kueri.

## Aplikasi Praktis
1. **Manajemen dokumen perusahaan:** Mengambil kontrak berdasarkan tanggal kontrak atau nama penandatangan.  
2. **Katalog perpustakaan digital:** Membiarkan pengguna menelusuri buku berdasarkan genre, tahun publikasi, atau penulis.  
3. **Sistem CRM:** Dengan cepat menemukan file klien menggunakan metadata khusus seperti ID pelanggan atau wilayah.  

## Tips dan praktik terbaik
- **Pembaruan inkremental:** Gunakan `index.addOrUpdate()` untuk file baru atau yang berubah alih-alih membangun ulang seluruh indeks.  
- **Pemrosesan batch:** Saat menangani ribuan file, tambahkan mereka dalam batch lebih kecil untuk menjaga penggunaan memori tetap rendah.  
- **Validasi metadata:** Pastikan dokumen sumber benar-benar berisi metadata yang ingin Anda kueri (mis., bidang penulis dalam PDF).  

## Pertimbangan Kinerja
- **Penyesuaian memori:** Sesuaikan ukuran heap JVM (`-Xmx`) berdasarkan volume metadata yang diindeks.  
- **Penyimpanan teroptimasi:** Secara periodik panggil `index.optimize()` untuk memadatkan indeks dan meningkatkan kecepatan kueri.  

## Masalah umum dan solusi
| Masalah | Solusi |
|-------|----------|
| **Tidak ada hasil yang dikembalikan** | Pastikan bahwa bidang metadata yang Anda harapkan memang ada dalam file sumber. |
| **Kesalahan izin** | Pastikan proses Java memiliki akses baca ke folder dokumen dan direktori indeks. |
| **Kesalahan out‑of‑memory** | Tingkatkan ukuran heap JVM atau lakukan batch pada operasi `add` untuk memproses file dalam grup yang lebih kecil. |

## Pertanyaan yang sering diajukan

**Q: Apa itu pengindeksan metadata?**  
A: Pengindeksan metadata menyimpan atribut dokumen (penulis, judul, tag khusus) dalam struktur yang dapat dicari, memungkinkan pencarian cepat tanpa memindai teks penuh.

**Q: Bagaimana cara mendapatkan lisensi sementara?**  
A: Kunjungi halaman pembelian GroupDocs dan ikuti langkah-langkah untuk memperoleh lisensi percobaan.

**Q: Bisakah saya mengindeks PDF dengan pengaturan ini?**  
A: Ya, GroupDocs.Search mendukung PDF, DOCX, PPT, dan banyak format lainnya.

**Q: Apa masalah umum saat menambahkan dokumen?**  
A: Verifikasi jalur file yang benar dan pastikan aplikasi memiliki izin baca untuk direktori.

**Q: Bagaimana cara mengoptimalkan kinerja pencarian?**  
A: Secara teratur perbarui indeks Anda, gunakan penambahan inkremental, dan sesuaikan pengaturan memori JVM.

## Sumber Daya

- **Dokumentasi:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **Referensi API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Unduh:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **Repositori GitHub:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Forum dukungan gratis:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Lisensi sementara:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-10-22  
**Diuji Dengan:** GroupDocs.Search Java 25.4  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara menambahkan dokumen ke indeks dengan Metadata Indexing di Java menggunakan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Cara Membuat Indeks Dokumen dan Menambahkan Dokumen Menggunakan API GroupDocs.Search untuk Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Panduan Manajemen Indeks Groupdocs Search Java](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)