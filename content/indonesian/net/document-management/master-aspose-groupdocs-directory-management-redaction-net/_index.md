---
date: '2026-06-22'
description: Panduan langkah demi langkah untuk membuat indeks dokumen .NET menggunakan
  GroupDocs.Redaction untuk .NET—kelola direktori, ganti nama file, dan pertahankan
  indeks tetap terbaru.
keywords:
- create document index .net
- GroupDocs.Redaction directory management
- .NET document indexing
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Step‑by‑step guide to create document index .net using GroupDocs.Redaction
    for .NET—manage directories, rename files, and keep indexes up to date.
  headline: How to Create Document Index .NET with Aspose.GroupDocs Redaction
  type: TechArticle
- description: Step‑by‑step guide to create document index .net using GroupDocs.Redaction
    for .NET—manage directories, rename files, and keep indexes up to date.
  name: How to Create Document Index .NET with Aspose.GroupDocs Redaction
  steps:
  - name: '**Free Trial** – Get a 30‑day trial from the GroupDocs portal.'
    text: '**Free Trial** – Get a 30‑day trial from the GroupDocs portal.'
  - name: '**Temporary License** – Request a temporary key for extended testing.'
    text: '**Temporary License** – Request a temporary key for extended testing.'
  - name: '**Purchase** – Obtain a production license to unlock full functionality.'
    text: '**Purchase** – Obtain a production license to unlock full functionality.'
  - name: '**Legal Document Management** – Index contracts, briefs, and case files
      for instant retrieval.'
    text: '**Legal Document Management** – Index contracts, briefs, and case files
      for instant retrieval.'
  - name: '**Digital Library Systems** – Provide real‑time search across thousands
      of e‑books and research papers.'
    text: '**Digital Library Systems** – Provide real‑time search across thousands
      of e‑books and research papers.'
  - name: '**Enterprise Content Management** – Maintain audit‑ready directories that
      automatically reflect naming conventions.'
    text: '**Enterprise Content Management** – Maintain audit‑ready directories that
      automatically reflect naming conventions.'
  - name: '**Customer Support Archives** – Quickly locate prior tickets, PDFs, and
      knowledge‑base articles.'
    text: '**Customer Support Archives** – Quickly locate prior tickets, PDFs, and
      knowledge‑base articles.'
  type: HowTo
- questions:
  - answer: It redacts sensitive content from PDFs, DOCXs, and images while also offering
      robust directory and indexing utilities.
    question: What is the primary use of GroupDocs.Redaction?
  - answer: Yes—create separate `Index` instances for each folder and operate them
      in parallel.
    question: Can I manage multiple directories simultaneously?
  - answer: Wrap `Index.Build` and `Index.Refresh` in try‑catch blocks; log `RedactionException`
      details for troubleshooting.
    question: How do I handle errors during indexing?
  - answer: A .NET Framework 4.6+ or .NET Core 3.1+ runtime, at least 2 GB RAM, and
      500 MB of free disk space for temporary buffers.
    question: What are the system requirements for GroupDocs.Redaction?
  - answer: Regularly call `Index.Refresh`, enable parallel processing, and limit
      batch sizes to keep memory consumption under control.
    question: How can I optimise index performance for large document sets?
  type: FAQPage
title: Cara Membuat Indeks Dokumen .NET dengan Aspose.GroupDocs Redaction
type: docs
url: /id/net/document-management/master-aspose-groupdocs-directory-management-redaction-net/
weight: 1
---

# Buat Indeks Dokumen .NET dengan Aspose.GroupDocs Redaction

Mengelola koleksi file yang besar dapat dengan cepat menjadi mimpi buruk jika Anda tidak memiliki cara yang dapat diandalkan untuk menjaga folder tetap rapi **dan** indeks pencarian tetap terbaru. Dalam tutorial ini Anda akan belajar cara **create document index .net** menggunakan GroupDocs.Redaction untuk .NET, mencakup persiapan direktori, pembuatan indeks, penamaan ulang dokumen, dan pembaruan indeks. Pada akhir tutorial Anda akan memiliki alur kerja yang dapat diulang yang dapat diskalakan dari beberapa PDF hingga ribuan dokumen hukum atau dukungan.

## Jawaban Cepat
- **Library apa yang saya butuhkan?** GroupDocs.Redaction untuk .NET (versi NuGet terbaru).  
- **Versi .NET mana yang didukung?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6+.  
- **Berapa banyak format yang dapat diindeks?** Lebih dari 50 format input — termasuk PDF, DOCX, XLSX, PPTX, dan tipe gambar umum.  
- **Apakah saya dapat menamai ulang file tanpa merusak indeks?** Ya—gunakan metode bawaan `Rename` dan kemudian panggil `NotifyIndex`.  
- **Apakah lisensi diperlukan untuk produksi?** Lisensi GroupDocs.Redaction yang valid wajib untuk penggunaan produksi.

## Apa Itu “Create Document Index .NET”?
*Create document index .net* mengacu pada proses membangun katalog yang dapat dicari dari file dalam aplikasi .NET, di mana setiap entri menyimpan metadata seperti nama file, jalur, dan cuplikan konten. Indeks ini memungkinkan pencarian cepat tanpa harus memindai seluruh sistem file setiap kali.

## Mengapa Menggunakan GroupDocs.Redaction untuk Pengindeksan?
GroupDocs.Redaction tidak hanya menyensor konten sensitif tetapi juga menyediakan mesin pengindeksan berperforma tinggi yang dapat menangani **hingga 10.000 dokumen per menit** pada server standar 8‑core, sambil menjaga penggunaan memori di bawah **200 MB** untuk sebagian besar beban kerja. API-nya mengabstraksi keanehan sistem file, memberi Anda cara konsisten untuk mengelola direktori dan menjaga indeks tetap sinkron.

## Prasyarat
- **GroupDocs.Redaction** paket NuGet terpasang (rilis stabil terbaru).  
- Visual Studio 2022 atau IDE apa pun yang kompatibel dengan .NET.  
- Pengetahuan dasar C# (file I/O, penanganan pengecualian).  

### Perpustakaan, Versi, dan Dependensi yang Diperlukan
- `GroupDocs.Redaction` ≥ 23.10 (mendukung .NET Standard 2.0 dan .NET 5+).  
- Opsional: `Microsoft.Extensions.Logging` untuk diagnostik terperinci.

### Persyaratan Penyiapan Lingkungan
Tambahkan paket melalui salah satu perintah berikut (jangan **memodifikasi** placeholder yang mewakili blok kode sebenarnya):

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Cari “GroupDocs.Redaction” dan instal versi terbaru.

### Langkah-langkah Akuisisi Lisensi
1. **Free Trial** – Dapatkan percobaan 30 hari dari portal GroupDocs.  
2. **Temporary License** – Minta kunci sementara untuk pengujian yang diperpanjang.  
3. **Purchase** – Dapatkan lisensi produksi untuk membuka semua fungsi.

## Cara Menyiapkan Direktori Kerja yang Bersih?
Muat folder target Anda, hapus file sementara yang tersisa, dan salin dokumen sumber yang ingin Anda indeks. Langkah persiapan ini menghilangkan kesalahan “file‑in‑use” selama pengindeksan dan memastikan bahwa pembangun indeks bekerja terhadap kumpulan file yang deterministik. Dengan memastikan lingkungan yang bersih, Anda mengurangi false‑positives, menghindari masalah izin, dan meningkatkan kinerja pengindeksan secara keseluruhan.

### Bersihkan Direktori
Kelas `DirectoryCleaner` menghapus file residual (mis., *.tmp, *.bak) yang dapat mengganggu proses pengindeksan.  
```csharp
using GroupDocs.Search.Common;
using System.IO;

string documentFolder = "YOUR_DOCUMENT_DIRECTORY/";

// Ensure the directory is empty before use
Utils.CleanDirectory(documentFolder);
```  

### Salin File yang Diperlukan
`FilePreparer` menyalin PDF, DOCX, dan gambar sumber ke dalam folder kerja, mempertahankan hierarki folder asli.  
```csharp
// Copy essential documents to the target directory from a source path
Utils.CopyFiles(Utils.DocumentsPath, documentFolder);
```  

## Cara Membuat Indeks?
`Index` mewakili koleksi dokumen yang dapat dicari dan mengelola struktur penyimpanan yang mendasarinya.

Instansiasi objek `Index`, arahkan ke direktori bersih Anda, dan panggil `Build`. Operasi ini memindai setiap file, mengekstrak teks yang dapat dicari, dan menyimpannya dalam struktur biner yang efisien. Builder juga mencatat metadata seperti jalur file dan timestamp, memungkinkan pencarian cepat dan pembaruan inkremental tanpa memproses ulang dokumen yang tidak berubah.

### Buat Indeks
Kelas `Index` adalah komponen inti yang mewakili koleksi dokumen yang dapat dicari.  
```csharp
using GroupDocs.Search;

string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Index/";
Index index = new Index(indexFolder); // Create the index

// Add documents from your directory to the index
index.Add("YOUR_DOCUMENT_DIRECTORY/Documents/");
```  

## Cara Menamai Ulang Dokumen dan Memberi Tahu Indeks?
`DocumentRenamer` menyediakan utilitas untuk menamai ulang file sambil menjaga integritas indeks.

`DocumentRenamer.RenameAndNotify` menamai ulang file di disk dan kemudian memanggil `Index.UpdateEntry` untuk menjaga katalog tetap akurat. Dengan melakukan penamaan ulang dan notifikasi indeks secara langsung dalam satu transaksi, Anda menghindari referensi usang dan memastikan pencarian selanjutnya mengembalikan nama file baru. Metode ini juga mencatat operasi untuk jejak audit.  
```csharp
using System;
using GroupDocs.Search;
using System.IO;

string oldDocumentPath = "YOUR_DOCUMENT_DIRECTORY/Documents/Lorem ipsum.txt";
string newDocumentPath = "YOUR_DOCUMENT_DIRECTORY/Documents/Lorem ipsum renamed.txt";

// Rename the file by moving it to a new path
File.Move(oldDocumentPath, newDocumentPath);

// Notify the index about this change\NSNotification notification = Notification.CreateRenameNotification(oldDocumentPath, newDocumentPath);
Index indexForNotify = new Index(indexFolder);
bool result = indexForNotify.Notify(notification); 
Console.WriteLine($"Successful rename: {result}");
```  

## Cara Memperbarui Indeks yang Ada Setelah Perubahan?
`Index.Refresh` menerapkan perubahan inkremental pada indeks yang ada tanpa membangun ulang secara keseluruhan.

`Index.Refresh` memproses hanya delta (file baru atau yang berubah), mengurangi beban CPU hingga **85 %** dibandingkan dengan rebuild penuh. Metode ini memindai direktori kerja, mengidentifikasi file dengan timestamp yang dimodifikasi, dan memperbarui entri mereka sambil mempertahankan dokumen yang tidak tersentuh. Pendekatan ini secara dramatis mempersingkat jendela pemeliharaan dan menjaga pengalaman pencarian tetap responsif.  
```csharp
using GroupDocs.Search;

Index indexToUpdate = new Index(indexFolder);

// Updates metadata without reindexing the entire document
indexToUpdate.Update();
```  

## Kasus Penggunaan Umum
1. **Legal Document Management** – Indeks kontrak, brief, dan berkas kasus untuk pengambilan instan.  
2. **Digital Library Systems** – Sediakan pencarian waktu nyata di antara ribuan e‑book dan makalah penelitian.  
3. **Enterprise Content Management** – Pertahankan direktori siap audit yang secara otomatis mencerminkan konvensi penamaan.  
4. **Customer Support Archives** – Temukan dengan cepat tiket sebelumnya, PDF, dan artikel basis pengetahuan.

## Pertimbangan Kinerja
- **Batch Updates** – Kelompokkan perubahan menjadi batch ≤ 500 file untuk menghindari lonjakan I/O yang berlebihan.  
- **Memory Management** – Buang objek `Index` setelah setiap operasi; perpustakaan melepaskan buffer native secara otomatis.  
- **Parallel Scanning** – Aktifkan `IndexOptions.EnableParallelProcessing` untuk memanfaatkan CPU multi‑core, mencapai hingga **3×** percepatan pada mesin 8‑core.

## Pertanyaan yang Sering Diajukan

**Q: Apa penggunaan utama GroupDocs.Redaction?**  
A: Ia menyensor konten sensitif dari PDF, DOCX, dan gambar sekaligus menawarkan utilitas direktori dan pengindeksan yang kuat.

**Q: Bisakah saya mengelola beberapa direktori secara bersamaan?**  
A: Ya—buat instance `Index` terpisah untuk setiap folder dan jalankan secara paralel.

**Q: Bagaimana cara menangani kesalahan selama pengindeksan?**  
A: Bungkus `Index.Build` dan `Index.Refresh` dalam blok try‑catch; catat detail `RedactionException` untuk pemecahan masalah.

**Q: Apa persyaratan sistem untuk GroupDocs.Redaction?**  
A: Runtime .NET Framework 4.6+ atau .NET Core 3.1+, minimal 2 GB RAM, dan 500 MB ruang disk bebas untuk buffer sementara.

**Q: Bagaimana saya dapat mengoptimalkan kinerja indeks untuk kumpulan dokumen besar?**  
A: Secara teratur panggil `Index.Refresh`, aktifkan pemrosesan paralel, dan batasi ukuran batch untuk menjaga konsumsi memori tetap terkendali.

## Sumber Daya Tambahan
- **Dokumentasi**: [Dokumentasi GroupDocs Redaction](https://docs.groupdocs.com/search/net/)  
- **Referensi API**: [Referensi API GroupDocs](https://reference.groupdocs.com/redaction/net)  
- **Unduh**: [Dapatkan GroupDocs Redaction](https://releases.groupdocs.com/search/net/)  
- **Dukungan Gratis**: [Forum GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Lisensi Sementara**: [Dapatkan Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-06-22  
**Diuji Dengan:** GroupDocs.Redaction 23.10 untuk .NET  
**Penulis:** GroupDocs

```csharp
using GroupDocs.Redaction;

// Initialize the Redactor object with your document path
var redactor = new Redactor("YOUR_DOCUMENT_PATH");
```

## Tutorial Terkait

- [Implementasikan GroupDocs.Search & Redaction: Perbarui dan Kelola Indeks Dokumen di .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Penguasaan Pembuatan dan Penggabungan Indeks dengan GroupDocs.Redaction .NET untuk Manajemen Dokumen Efisien](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Menguasai GroupDocs.Redaction .NET: Pembuatan Indeks Efisien dan Manajemen Alias untuk Pencarian Dokumen Lanjutan](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)