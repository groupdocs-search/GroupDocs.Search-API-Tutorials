---
date: '2026-06-07'
description: Pelajari cara memperbarui indeks secara efisien dengan GroupDocs.Search
  dan Redaction untuk .NET, meningkatkan sistem manajemen dokumen Anda.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Cara Memperbarui Indeks dengan GroupDocs.Search & Redaction (.NET)
type: docs
url: /id/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Cara Memperbarui Indeks dengan GroupDocs.Search & Redaction (.NET)

Dalam perusahaan modern yang berbasis data, **cara memperbarui indeks** dengan cepat dan dapat diandalkan dapat menentukan keberhasilan pengalaman pencarian Anda. Baik Anda menangani ribuan kontrak atau basis pengetahuan yang luas, menjaga indeks pencarian tetap sinkron dengan perubahan dokumen terbaru sangat penting untuk hasil yang cepat dan akurat. Tutorial ini memandu Anda menggunakan GroupDocs.Search untuk .NET bersama dengan GroupDocs.Redaction untuk **memperbarui file indeks**, mengelola indeks berversi, dan melindungi konten sensitif—semua dalam proyek .NET yang bersih.

## Jawaban Cepat
- **Apa arti “cara memperbarui indeks”?** Ini adalah proses memodifikasi indeks pencarian yang ada sehingga dokumen baru atau yang berubah menjadi dapat dicari tanpa harus membangun ulang dari awal.  
- **Perpustakaan mana yang diperlukan?** GroupDocs.Search dan GroupDocs.Redaction untuk .NET (keduanya tersedia via NuGet).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengujian; lisensi produksi membuka semua fungsi.  
- **Bisakah saya menjalankannya di .NET Core?** Ya, perpustakaan mendukung .NET Framework 4.5+, .NET Core 3.1+, dan .NET 5/6+.  
- **Kinerja apa yang dapat saya harapkan?** Memperbarui indeks 1 GB dengan 2 thread selesai dalam kurang dari satu menit pada server 4‑core tipikal.

## Apa itu “cara memperbarui indeks”?
**Cara memperbarui indeks** mengacu pada teknik menerapkan perubahan inkremental pada indeks pencarian yang sudah ada alih‑alih membuatnya kembali secara keseluruhan. Pendekatan ini mengurangi waktu henti, menghemat siklus CPU, dan menjaga hasil pencarian tetap segar saat dokumen ditambahkan, diedit, atau dihapus.

## Mengapa menggunakan GroupDocs.Search & Redaction untuk pembaruan indeks?
GroupDocs.Search mendukung **lebih dari 50 format file** (PDF, DOCX, XLSX, PPTX, HTML, gambar, dll.) dan dapat memproses dokumen ratusan halaman tanpa memuat seluruh file ke memori. Digabungkan dengan GroupDocs.Redaction, Anda dapat secara otomatis menghapus atau menyamarkan data sensitif sebelum pengindeksan, memastikan kepatuhan sambil mempertahankan relevansi pencarian.

## Prasyarat

- **GroupDocs.Search** – instal via NuGet.  
- **GroupDocs.Redaction untuk .NET** – diperlukan untuk kemampuan redaksi.  
- Visual Studio (atau IDE .NET apa pun) dengan .NET 6+ terpasang.  
- Pengetahuan dasar C# dan pemahaman tentang konsep pengindeksan.

### Perpustakaan dan Versi yang Diperlukan
- **GroupDocs.Search** – rilis stabil terbaru dari NuGet.  
- **GroupDocs.Redaction untuk .NET** – rilis stabil terbaru dari NuGet.

### Persyaratan Penyiapan Lingkungan
- Mesin Windows atau Linux dengan .NET SDK terpasang.  
- Akses ke folder tempat file indeks akan disimpan.

### Prasyarat Pengetahuan
- Memahami dasar‑dasar pengindeksan dokumen dan pencarian.  
- Menyadari manajemen siklus hidup dokumen dalam sistem perusahaan.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Instal Paket-paket

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Cari “GroupDocs.Redaction” dan instal versi terbaru.

### Langkah-langkah Akuisisi Lisensi
1. **Free Trial** – mulai dengan percobaan untuk menjelajahi semua fitur.  
2. **Temporary License** – minta kunci sementara untuk pengujian yang lebih lama.  
3. **Purchase** – dapatkan lisensi penuh untuk penerapan produksi.

### Inisialisasi dan Penyiapan Dasar
`Redactor` adalah kelas inti yang menerapkan aturan redaksi pada dokumen.  
Untuk memulai, referensikan namespace Redaction dan buat instance `Redactor`:

```csharp
using GroupDocs.Redaction;
```

Ini mempersiapkan Anda untuk menerapkan aturan redaksi sebelum memasukkan dokumen ke indeks pencarian.

## Panduan Implementasi

Kami akan membahas dua kemampuan inti: memperbarui dokumen yang diindeks dan menjaga kontrol versi indeks.

### Cara memperbarui indeks menggunakan GroupDocs.Search?

`Index` mewakili koleksi yang dapat dicari yang disimpan di disk.  
`UpdateOptions` mengonfigurasi bagaimana pembaruan inkremental dilakukan (misalnya, jumlah thread).  
`UpdateDocument` menerapkan perubahan pada satu dokumen, dan `Commit` menyelesaikan semua pembaruan yang tertunda.

**Jawaban langsung (40‑70 kata):**  
Buat objek `Index` yang menunjuk ke folder indeks Anda, gunakan `UpdateOptions` untuk menentukan jumlah thread, panggil `UpdateDocument` untuk setiap file yang berubah, dan akhirnya panggil `Commit` untuk menyimpan perubahan. Pendekatan inkremental ini memperbarui hanya bagian yang dimodifikasi, menjaga indeks tetap terkini tanpa pembangunan ulang penuh.

#### Fitur 1: Memperbarui Dokumen yang Diindeks

##### Gambaran Umum
Memperbarui dokumen yang diindeks memastikan hasil pencarian Anda mencerminkan konten terbaru, bahkan ketika dokumen diedit atau diganti.

##### Langkah 1: Buat Indeks  
Kelas `Index` adalah objek tingkat atas yang mewakili koleksi yang dapat dicari di disk.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Langkah 2: Tambahkan Dokumen ke Indeks  
Tambahkan file dari sebuah direktori; perpustakaan secara otomatis mengekstrak teks yang dapat dicari.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Langkah 3: Cari dan Perbarui  
Jalankan kueri, ubah file sumber, lalu panggil `UpdateDocument` dengan `UpdateOptions` yang sama seperti saat pengindeksan.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Mengapa Ini Berhasil:** Dengan mengatur `Threads = 2`, pembaruan memanfaatkan dua inti CPU, memotong waktu pemrosesan hampir setengah pada mesin quad‑core.

### Cara menjaga kontrol versi indeks?

`IndexUpdater` adalah kelas utilitas yang memperbarui format indeks lama ke versi terbaru yang didukung oleh perpustakaan.  

**Jawaban langsung (40‑70 kata):**  
Instansiasi `IndexUpdater` dengan path ke indeks yang ada, panggil `CanUpdateVersion()` untuk memverifikasi kompatibilitas, lalu jalankan `UpdateVersion()` jika diperlukan. Setelah upgrade, muat kembali indeks dengan format baru dan lakukan pencarian untuk memastikan semuanya berfungsi. Ini memastikan migrasi mulus antar rilis perpustakaan.

#### Fitur 2: Menjaga Kontrol Versi Indeks

##### Gambaran Umum
Kontrol versi menjamin bahwa indeks lama tetap dapat dicari setelah upgrade perpustakaan.

##### Langkah 1: Periksa Kompatibilitas  
`IndexUpdater` memeriksa apakah indeks saat ini dapat ditingkatkan ke format terbaru.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Langkah 2: Muat dan Cari  
Setelah upgrade, muat indeks yang telah diperbarui dan jalankan kueri untuk memverifikasi integritas.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Mengapa Ini Berhasil:** Guard `CanUpdateVersion` mencegah pengecualian runtime yang disebabkan oleh skema indeks yang tidak cocok, menyediakan jalur upgrade yang aman.

## Aplikasi Praktis

Skenario dunia nyata di mana **cara memperbarui indeks** penting:

1. **Manajemen Dokumen Hukum** – Cepat mengindeks ulang kontrak setelah amandemen sambil meredaksi klausa rahasia.  
2. **Arsip Korporat** – Menjaga catatan historis dapat dicari tanpa memproses ulang jutaan file.  
3. **Sistem Manajemen Konten (CMS)** – Mendorong pembaruan inkremental ke indeks pencarian saat penulis mempublikasikan artikel baru.

## Pertimbangan Kinerja

- **Threading Options:** Sesuaikan `UpdateOptions.Threads` berdasarkan inti CPU; lebih banyak thread meningkatkan throughput tetapi menambah penggunaan memori.  
- **Resource Usage:** Pantau RAM; perpustakaan melakukan streaming file, sehingga lonjakan memori minimal bahkan untuk PDF 500 halaman.  
- **Best Practices:** Jadwalkan pembaruan inkremental secara rutin dan bersihkan versi indeks yang usang untuk menjaga kinerja optimal.

## Masalah Umum dan Solusinya

| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| **Index tidak ditemukan** | Path folder salah | Pastikan konstruktor `Index` menunjuk ke direktori yang benar. |
| **Kesalahan ketidakcocokan versi** | Menggunakan indeks lama dengan perpustakaan baru | Jalankan alur `IndexUpdater` sebelum pengindeksan normal. |
| **Redaksi tidak diterapkan** | Aturan redaksi dimuat setelah pengindeksan | Terapkan redaksi **sebelum** menambahkan dokumen ke indeks. |

## Pertanyaan yang Sering Diajukan

**T: Apa perbedaan antara `UpdateDocument` dan `Rebuild`?**  
J: `UpdateDocument` hanya memodifikasi file yang berubah, sedangkan `Rebuild` membuat ulang seluruh indeks dari awal, memakan lebih banyak waktu dan sumber daya.

**T: Bisakah saya memperbarui beberapa dokumen secara paralel?**  
J: Ya, atur `UpdateOptions.Threads` ke jumlah inti yang ingin Anda gunakan; perpustakaan menangani pemrosesan paralel secara internal.

**T: Apakah GroupDocs.Search mendukung PDF terenkripsi?**  
J: Tentu. Berikan kata sandi melalui `SearchOptions.Password` saat memuat dokumen.

**T: Bagaimana saya memverifikasi bahwa redaksi berhasil sebelum pengindeksan?**  
J: Panggil `Redactor.Apply()` dan periksa ukuran file output; ukuran yang berkurang biasanya menandakan redaksi berhasil.

**T: Versi .NET apa yang secara resmi didukung?**  
J: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, dan .NET 6+.

## Kesimpulan

Anda kini memiliki panduan lengkap dan siap produksi tentang **cara memperbarui indeks** menggunakan GroupDocs.Search dan cara menjaga indeks tetap kompatibel versi dengan GroupDocs.Redaction untuk .NET. Dengan mengikuti langkah‑langkah di atas, Anda dapat memastikan lapisan pencarian tetap cepat, akurat, dan mematuhi regulasi privasi data.

**Langkah Selanjutnya:**  
- Bereksperimen dengan pengaturan `Threads` yang berbeda untuk menemukan titik optimal bagi perangkat keras Anda.  
- Jelajahi pola redaksi lanjutan (misalnya, penghapusan SSN berbasis regex) sebelum pengindeksan.  
- Integrasikan rutinitas pembaruan indeks ke dalam pipeline CI/CD Anda untuk manajemen dokumen yang sepenuhnya otomatis.

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs  

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/search/net/)
- [Referensi API](https://reference.groupdocs.com/redaction/net)
- [Unduh GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Tutorial Terkait

- [Menguasai GroupDocs.Redaction .NET: Pembuatan Indeks Efisien dan Manajemen Alias untuk Pencarian Dokumen Lanjutan](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implementasi Pencarian Sinonim dengan GroupDocs.Redaction .NET untuk Manajemen Dokumen yang Ditingkatkan](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Menguasai GroupDocs Search dan Redaction di .NET: Manajemen Dokumen Lanjutan](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)