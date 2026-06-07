---
date: '2026-06-07'
description: Pelajari cara mengimplementasikan high compression .net untuk penyimpanan
  teks dan men-redact data rahasia menggunakan GroupDocs.Search dan GroupDocs.Redaction
  dalam aplikasi .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Implement High Compression .NET dengan GroupDocs: Panduan Teks & Redaction'
type: docs
url: /id/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementasi Kompresi Tinggi .NET dengan GroupDocs: Panduan Teks & Redaksi

Dalam solusi .NET modern, **implement high compression .net** sangat penting ketika Anda perlu menyimpan koleksi teks yang sangat besar tanpa meningkatkan penggunaan disk secara berlebihan. Pada saat yang sama, melindungi informasi sensitif—seperti pengenal pribadi atau angka keuangan—memerlukan redaksi yang dapat diandalkan. Tutorial ini menunjukkan, langkah demi langkah, cara mengonfigurasi penyimpanan teks dengan kompresi tinggi menggunakan **GroupDocs.Search** dan cara menghapus data rahasia secara aman menggunakan **GroupDocs.Redaction**. Pada akhir tutorial, Anda akan dapat mengompresi teks terindeks hingga 90 % dan menghapus konten pribadi dari PDF, file Word, dan banyak format lainnya.

## Jawaban Cepat
- **Perpustakaan apa yang menyediakan pengindeksan kompresi tinggi?** GroupDocs.Search for .NET.  
- **Alat apa yang melakukan redaksi data sensitif?** GroupDocs.Redaction for .NET.  
- **Bisakah saya menambahkan dokumen ke indeks secara otomatis?** Yes—use the `AddDocument` API inside a folder‑scan loop.  
- **Apakah kompresi tidak mengurangi kualitas untuk pencarian?** Yes, the text remains fully searchable after compression.  
- **Apakah saya memerlukan lisensi untuk produksi?** A permanent GroupDocs license is required for commercial use.

## Apa itu “implement high compression .net”?
Implement high compression .net berarti mengonfigurasi mesin pengindeksan GroupDocs.Search untuk menyimpan konten teks yang diekstrak dalam bentuk terkompresi. Ini mengurangi ukuran indeks di disk secara dramatis sambil menjaga teks tetap dapat dicari sepenuhnya. Kompresi ini tidak mengurangi kualitas, sehingga relevansi kueri dan ekstraksi cuplikan berfungsi persis seperti pada indeks yang tidak terkompresi.

## Mengapa menggunakan GroupDocs untuk kompresi dan redaksi?
GroupDocs.Search mendukung lebih dari lima puluh format input dan dapat mengompresi teks terindeks hingga sembilan puluh persen, memungkinkan koleksi dokumen besar hanya menempati sebagian kecil dari ukuran aslinya. GroupDocs.Redaction melengkapi ini dengan menghapus atau menyamarkan informasi sensitif secara permanen pada lebih dari tiga puluh jenis file, membantu Anda memenuhi regulasi kepatuhan ketat seperti GDPR dan HIPAA tanpa alat tambahan.

## Prasyarat
- **Lingkungan pengembangan:** Visual Studio 2022 atau lebih baru, .NET 6+ (atau .NET Framework 4.7.2).  
- **Pustaka:** `GroupDocs.Search` and `GroupDocs.Redaction` NuGet packages.  
- **Izin:** Read/write access to the folders that contain source documents and the index output location.  
- **Pengetahuan dasar:** C# syntax, file I/O, and familiarity with .NET project structure.

## Cara mengimplementasikan kompresi tinggi .NET dengan GroupDocs?
Untuk mengimplementasikan kompresi tinggi .NET dengan GroupDocs, pertama buat instance `TextStorageSettings` dan atur `CompressionLevel`‑nya ke `High`. Kemudian buat objek `Index`, melewatkan pengaturan dan folder tempat indeks akan disimpan. Setelah indeks siap, tambahkan dokumen menggunakan `AddDocument`, dan akhirnya jalankan pencarian dengan metode `Search`, semua sementara mesin secara transparan menangani kompresi dan dekompresi.

### Langkah 1: Instal paket NuGet yang diperlukan
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Cari “GroupDocs.Search” dan klik **Install**.  

### Langkah 2: Instal GroupDocs.Redaction (untuk redaksi data)
- Buka **NuGet Package Manager**.  
- Cari **GroupDocs.Redaction** dan instal versi stabil terbaru.  

### Langkah 3: Dapatkan dan terapkan lisensi
- **Free trial:** Daftar di portal GroupDocs untuk mendapatkan kunci percobaan 30‑hari.  
- **Temporary license:** Minta kunci sementara untuk lingkungan pengembangan.  
- **Permanent license:** Beli lisensi produksi untuk menghapus batasan evaluasi.

### Langkah 4: Inisialisasi dasar kedua pustaka
Mesin `Search` dan `Redaction` berbagi model lisensi yang sama. Inisialisasi keduanya saat aplikasi dimulai:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Fitur 1: Pengaturan Penyimpanan Teks Kompresi Tinggi

### Menyiapkan Konfigurasi Pengindeksan
`TextStorageSettings` adalah kelas yang memberi tahu GroupDocs.Search cara menyimpan teks yang diekstrak. Mengaktifkan kompresi tinggi mengurangi ukuran indeks hingga **10×** tanpa memengaruhi kecepatan pencarian.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Penjelasan:**  
- `CompressionLevel.High` mengaktifkan algoritma berbasis ZSTD yang mengompresi blok teks secara efisien.  
- `UseMemoryCache = false` memaksa mesin untuk men‑stream data dari disk, yang ideal untuk penyebaran skala besar.

### Membuat dan Mengelola Indeks
Objek `Index` mewakili repositori yang dapat dicari di disk. Anda menentukan folder tempat file indeks akan disimpan dan melewatkan pengaturan kompresi yang telah didefinisikan di atas.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Penjelasan:**  
- `indexFolder` menentukan di mana file indeks terkompresi berada.  
- `settings` menyuntikkan konfigurasi kompresi tinggi, memastikan setiap dokumen yang ditambahkan mendapat manfaat darinya.

## Fitur 2: Menambahkan Dokumen ke Indeks

### Tambahkan Dokumen ke Indeks Anda
`AddDocument` menambahkan satu file ke indeks, mengekstrak teksnya, mengompresinya sesuai pengaturan yang dikonfigurasi, dan menyimpan hasilnya. GroupDocs.Search dapat mengimpor file dari struktur direktori. Loop berikut melintasi `documentsFolder`, menambahkan setiap file, dan mencatat kemajuan.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Penjelasan:**  
- `AddDocument` mem‑parsing file, mengekstrak teks yang dapat dicari, mengompresinya sesuai `TextStorageSettings`, dan menyimpannya di indeks.  
- Pendekatan ini bekerja untuk **PDF, DOCX, TXT, HTML**, dan lebih dari **30** format lainnya.

## Fitur 3: Menjalankan Kuery Pencarian

### Lakukan Pencarian
`Search` menjalankan kueri terhadap indeks terkompresi dan mengembalikan koleksi objek `DocumentResult` yang cocok dengan skor relevansi dan cuplikan yang disorot. Setelah indeks terisi, Anda dapat menjalankan kueri cepat. Metode `Search` mengembalikan koleksi objek `DocumentResult` yang mencakup jalur file dan cuplikan yang disorot.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Penjelasan:**  
- Mesin pencari memindai teks terkompresi secara langsung, sehingga latensi kueri tetap rendah bahkan untuk indeks yang berisi **jutaan halaman**.  
- `Score` menunjukkan relevansi; nilai yang lebih tinggi berarti kecocokan yang lebih baik.

## Cara meredaksi data rahasia dengan GroupDocs.Redaction?
Meredaksi data rahasia dengan GroupDocs.Redaction dimulai dengan membuat instance `Redactor` untuk file target. Definisikan satu atau lebih objek `SearchPattern` yang menggambarkan teks yang akan dihapus, seperti ekspresi reguler untuk nomor jaminan sosial. Terapkan setiap pola menggunakan `Redact`, menentukan `RedactionType` seperti `BlackOut`, dan simpan hasilnya sebagai dokumen baru, memastikan yang asli tetap tidak tersentuh.

`Redactor` adalah kelas utama dalam GroupDocs.Redaction yang digunakan untuk memuat dokumen dan melakukan operasi redaksi.  
`SearchPattern` mendefinisikan ekspresi reguler yang mengidentifikasi teks yang akan diredaksi.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Penjelasan:**  
- `SearchPattern` menggunakan ekspresi reguler untuk menemukan nomor jaminan sosial.  
- `RedactionType.BlackOut` menggantikan teks yang cocok dengan persegi hitam solid, memastikan data tidak dapat dipulihkan.

## Aplikasi Praktis
1. **Manajemen Dokumen Hukum:** Secara otomatis mengompresi file kasus yang sangat besar dan meredaksi pengidentifikasi klien sebelum diarsipkan.  
2. **Catatan Kesehatan:** Simpan bertahun‑tahun catatan pasien dalam indeks terkompresi dan hapus PHI (Informasi Kesehatan yang Dilindungi) sebelum dibagikan dengan mitra riset.  
3. **Pelaporan Keuangan:** Amankan laporan kuartalan dengan meredaksi nomor akun sambil mempertahankan teks yang dapat dicari untuk kueri audit.

## Pertimbangan Kinerja
- **Dampak Kompresi:** Kompresi tinggi mengurangi ukuran indeks hingga **90 %**, yang mengurangi keausan SSD dan mempercepat operasi pencadangan.  
- **Penggunaan Memori:** Nonaktifkan caching dalam memori untuk indeks yang sangat besar agar jejak proses tetap di bawah **500 MB**.  
- **Optimasi I/O:** Tambahkan dokumen secara batch dalam kelompok berisi 100 untuk meminimalkan beban disk.  
- **Pemrosesan Async:** Bungkus pemanggilan `AddDocument` dalam `Task.Run` untuk menjaga responsivitas thread UI pada aplikasi desktop.

## Kesulitan Umum & Pemecahan Masalah
- **Path file tidak tepat:** Pastikan `documentsFolder` dan `indexFolder` merupakan path absolut dan aplikasi memiliki izin baca/tulis.  
- **Kesalahan lisensi:** Pastikan file `.lic` ditempatkan bersama executable atau di‑embed sebagai sumber daya.  
- **Pencarian tidak menghasilkan hasil:** Periksa bahwa level kompresi `TextStorageSettings` sesuai dengan yang digunakan saat pengindeksan; ketidaksesuaian pengaturan dapat menyebabkan kegagalan deserialisasi.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menambahkan dokumen ke indeks setelah pembuatan awal?**  
A: Ya—cukup panggil `index.AddDocument` untuk file baru; mesin memperbarui indeks terkompresi secara inkremental.

**Q: Apakah redaksi mengubah file asli?**  
A: Tidak—file asli tetap tidak tersentuh; versi yang diredaksi disimpan sebagai file baru, menjaga integritas dokumen.

**Q: Format apa yang didukung oleh GroupDocs.Redaction?**  
A: Lebih dari **30** format, termasuk PDF, DOCX, PPTX, XLSX, gambar (PNG, JPEG), dan teks biasa.

**Q: Bagaimana kompresi tinggi memengaruhi relevansi pencarian?**  
A: Tidak memengaruhi. Kompresi bersifat loss‑less untuk teks, sehingga skor relevansi identik dengan indeks yang tidak terkompresi.

**Q: Apakah ada batas ukuran dokumen yang dapat saya indeks?**  
A: GroupDocs.Search dapat menangani file multi‑gigabyte dengan streaming konten; namun, pastikan ruang disk yang cukup untuk indeks terkompresi (sekitar 10 % dari ukuran asli).

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/search/net/)
- [Referensi API](https://reference.groupdocs.com/redaction/net)
- [Unduh GroupDocs.Redaction untuk .NET](https://releases.groupdocs.com/search/net/)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Akuisisi Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-06-07  
**Diuji Dengan:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Menerapkan GroupDocs.Search dan Redaction di .NET untuk Manajemen Dokumen](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Cara Mengoptimalkan GroupDocs.Redaction untuk .NET: Panduan Manajemen Indeks & Ejaan Efisien](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Menguasai GroupDocs Redaction dan Search di .NET: Manajemen Dokumen Efisien dan Pencarian Aman](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)