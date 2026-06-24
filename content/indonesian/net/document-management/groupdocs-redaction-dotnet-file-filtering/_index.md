---
date: '2026-04-21'
description: Pelajari cara memfilter file menggunakan GroupDocs.Redaction untuk .NET,
  termasuk memfilter berdasarkan tanggal pembuatan, ukuran file, tanggal modifikasi,
  dan cara menerapkan filter NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Cara Menyaring File dengan GroupDocs.Redaction untuk .NET
type: docs
url: /id/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Cara Memfilter File dengan GroupDocs.Redaction untuk .NET

Dalam lingkungan digital yang bergerak cepat saat ini, **cara memfilter file** secara efisien dapat menentukan produktivitas Anda. Baik Anda perlu mengisolasi dokumen berdasarkan ekstensi, tanggal pembuatan, ukuran, atau tanggal modifikasi, strategi pemfilteran yang solid menghemat waktu, mengurangi biaya penyimpanan, dan menjaga indeks pencarian tetap rapi. Dalam tutorial ini kami akan membahas contoh dunia nyata menggunakan GroupDocs.Redaction untuk .NET, menunjukkan secara tepat cara memfilter file untuk memenuhi kebutuhan bisnis umum.

## Jawaban Cepat
- **Library apa yang saya butuhkan?** GroupDocs.Redaction for .NET (install via NuGet).  
- **Bisakah saya memfilter berdasarkan tanggal pembuatan?** Ya – gunakan `CreateCreationTimeRange`.  
- **Bagaimana cara mengecualikan tipe tertentu?** Terapkan filter NOT dengan `DocumentFilter.CreateNot`.  
- **Apakah pemfilteran ukuran file didukung?** Tentu saja, melalui `CreateFileLengthRange` atau batas atas/bawah.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan atau penuh diperlukan untuk penggunaan produksi.

## Apa itu pemfilteran file dengan GroupDocs.Redaction?
Pemfilteran file memungkinkan Anda memberi tahu mesin pengindeksan dokumen mana yang harus disertakan atau diabaikan berdasarkan metadata seperti ekstensi, tanggal, pola jalur, atau ukuran. Dengan mendefinisikan aturan `DocumentFilter` yang tepat, Anda menjaga indeks tetap ramping dan pencarian menjadi cepat.

## Mengapa menggunakan GroupDocs.Redaction untuk .NET?
- **Pembantu filter bawaan** – tidak perlu menulis kode sistem file khusus.  
- **Operator logika** – gabungkan beberapa kriteria dengan AND, OR, dan NOT.  
- **Dioptimalkan untuk kinerja** – filter diterapkan selama proses pengindeksan, bukan setelahnya.  
- **Lintas platform** – bekerja dengan .NET Framework, .NET Core, dan .NET 5/6+.

## Prasyarat
- .NET Framework 4.6+ atau .NET Core 3.1+ terinstal.  
- Visual Studio atau IDE C# pilihan Anda.  
- Pengetahuan dasar C#.

### Perpustakaan & Penyiapan yang Diperlukan
Instal paket NuGet menggunakan metode pilihan Anda:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Pro tip:** Setelah menginstal, tambahkan file lisensi Anda ke root proyek dan panggil `License.SetLicense("license-file-path")` sebelum membuat objek Redactor atau Index apa pun.

## Menyiapkan GroupDocs.Redaction untuk .NET

Pertama, buat instance `Redactor` yang mengarah ke dokumen yang ingin Anda kerjakan:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Mengapa ini penting:** Menginisialisasi Redactor menjamin perpustakaan siap menerapkan filter dan aturan redaksi nanti dalam alur kerja.

## Cara memfilter file berdasarkan ekstensi

Memfilter berdasarkan ekstensi file adalah cara paling umum untuk mempersempit kumpulan dokumen. Di bawah ini kami hanya mempertahankan file FB2, EPUB, dan TXT.

### Memfilter berdasarkan ekstensi file

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cara menerapkan filter NOT untuk mengecualikan tipe yang tidak diinginkan

Jika Anda perlu **menerapkan filter NOT**—misalnya, mengecualikan file HTML dan PDF—gunakan `CreateNot`.

### Mengecualikan file HTM, HTML, dan PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cara memfilter file berdasarkan tanggal pembuatan

Ketika Anda perlu **memfilter berdasarkan tanggal pembuatan**, tentukan `DateTime` mulai dan akhir.

### Memfilter berdasarkan rentang tanggal pembuatan

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cara memfilter file berdasarkan tanggal modifikasi

Mirip dengan tanggal pembuatan, Anda dapat membatasi hasil ke file yang dimodifikasi sebelum titik tertentu.

### Memfilter berdasarkan tanggal modifikasi

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cara memfilter file berdasarkan jalur menggunakan ekspresi reguler

Jika struktur folder Anda mengikuti konvensi penamaan, regex dapat menargetkan jalur tertentu.

### Memfilter berdasarkan pola jalur file

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cara memfilter file berdasarkan ukuran

Mengontrol ukuran dokumen penting saat menangani batas bandwidth atau penyimpanan.

### Memfilter berdasarkan ukuran file (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cara menggabungkan beberapa kondisi dengan AND

Ketika Anda perlu **memfilter file** menggunakan beberapa kriteria sekaligus, gabungkan mereka dengan `CreateAnd`.

### Contoh AND logis

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cara menggabungkan beberapa kondisi dengan OR

Gunakan `CreateOr` ketika salah satu dari beberapa aturan harus lolos.

### Contoh OR logis

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Masalah Umum dan Solusinya
- **Filter tidak diterapkan:** Pastikan Anda menetapkan `settings.DocumentFilter` **sebelum** membuat instance `Index`.  
- **File tidak terduga muncul:** Periksa kembali ekstensi file termasuk titik di depannya (`.txt`).  
- **Penurunan kinerja:** Gabungkan filter dengan AND untuk mengurangi jumlah file yang dipindai pada tahap awal pipeline pengindeksan.  
- **Kesalahan regex:** Escape karakter khusus dalam pola jalur Anda atau gunakan `RegexOptions.IgnoreCase` untuk pencocokan tidak sensitif huruf besar/kecil.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggabungkan filter NOT dengan filter AND?**  
A: Ya. Bangun filter NOT terlebih dahulu (`DocumentFilter.CreateNot`) dan kemudian sertakan sebagai salah satu argumen ke `DocumentFilter.CreateAnd`.

**Q: Bagaimana cara memfilter file yang lebih besar dari 10 MB?**  
A: Gunakan `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` untuk hanya menyertakan file yang melebihi ukuran tersebut.

**Q: Apakah memungkinkan memfilter berdasarkan tanggal pembuatan dan modifikasi secara bersamaan?**  
A: Tentu saja. Buat masing‑masing filter secara terpisah dan gabungkan dengan `CreateAnd`.

**Q: Apakah filter ini bekerja dengan jalur penyimpanan cloud?**  
A: Filter beroperasi pada sistem file lokal. Untuk sumber cloud, unduh file ke folder sementara terlebih dahulu, lalu terapkan filter yang sama.

**Q: Apakah mengubah filter memerlukan re‑indeksasi?**  
A: Ya. Filter dievaluasi saat Anda memanggil `index.Add`. Mengubah filter berarti Anda perlu membangun kembali indeks untuk mencerminkan kriteria baru.

## Kesimpulan

Dengan menguasai **cara memfilter file** dengan GroupDocs.Redaction untuk .NET—baik berdasarkan ekstensi, tanggal pembuatan, tanggal modifikasi, ukuran file, atau menggunakan logika NOT—Anda dapat menyederhanakan manajemen dokumen, menjaga indeks tetap berperforma, dan fokus pada konten yang benar‑benar penting. Bereksperimenlah dengan operator logika untuk menyesuaikan pemfilteran dengan aturan bisnis Anda secara tepat, dan Anda akan melihat peningkatan langsung dalam kecepatan dan efisiensi penyimpanan.

---

**Terakhir Diperbarui:** 2026-04-21  
**Diuji Dengan:** GroupDocs.Redaction 24.11 untuk .NET  
**Penulis:** GroupDocs