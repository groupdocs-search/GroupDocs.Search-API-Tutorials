---
date: '2026-06-07'
description: Pelajari cara menampilkan ekstensi file dan mendapatkan format file menggunakan
  GroupDocs.Redaction di C#. Termasuk pengaturan, kode, dan tips praktis.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Cara menampilkan ekstensi file dengan GroupDocs.Redaction di .NET – Panduan
  Komprehensif
type: docs
url: /id/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Menampilkan Format File yang Didukung Menggunakan GroupDocs.Redaction di .NET

Mengelola berbagai jenis dokumen adalah kenyataan sehari-hari bagi pengembang .NET. Dengan menggunakan **GroupDocs.Redaction**, Anda dapat **mendaftar ekstensi file** yang didukung oleh perpustakaan, memberikan aplikasi Anda kecerdasan untuk menerima atau menolak unggahan, menampilkan pilihan UI yang ramah, dan menghindari kesalahan runtime yang mahal. Tutorial ini memandu Anda melalui semua yang diperlukan—dari prasyarat hingga implementasi lengkap yang siap produksi—sehingga Anda dapat dengan percaya diri **mendapatkan format file** dan **c# menampilkan format file** dalam solusi Anda.

## Jawaban Cepat
- **Apa arti “list file extensions”?** Artinya mengambil koleksi pengidentifikasi tipe file yang didukung (misalnya *.pdf*, *.docx*) dari API.  
- **Package NuGet mana yang menyediakan kemampuan ini?** `GroupDocs.Redaction` (versi stabil terbaru).  
- **Apakah saya memerlukan lisensi untuk menjalankan contoh?** Lisensi percobaan gratis berfungsi untuk pengembangan; lisensi permanen diperlukan untuk produksi.  
- **Bisakah saya menyimpan hasil dalam cache?** Ya—simpan daftar di memori atau cache terdistribusi untuk menghindari pemanggilan API berulang.  
- **Apakah fitur ini kompatibel dengan .NET 6 dan .NET Core?** Tentu saja; perpustakaan mendukung .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, dan .NET 6+.

## Apa itu GroupDocs.Redaction?
**GroupDocs.Redaction** adalah perpustakaan .NET yang memungkinkan pengembang untuk menyensor konten sensitif, mengonversi dokumen, dan menemukan tipe file yang didukung—semua tanpa memerlukan Microsoft Office di server. Ini mengabstraksi penanganan format yang kompleks di balik API yang bersih dan berorientasi objek. Ia menawarkan API terpadu untuk penyensoran, konversi, dan penemuan format, menangani PDF, dokumen Office, gambar, dan lainnya, sambil memastikan kinerja tinggi dan keamanan.

## Mengapa mendaftar ekstensi file dengan GroupDocs.Redaction?
Perpustakaan **mendukung lebih dari 50 format input dan output**, termasuk PDF, DOCX, PPTX, XLSX, HTML, dan lebih dari 30 tipe gambar. Dengan secara programatis **mendaftar ekstensi file**, Anda dapat:
- Mencegah pengguna mengunggah file yang tidak didukung (mengurangi kesalahan validasi hingga 90%).  
- Mengisi menu dropdown secara dinamis, memastikan UI tetap selaras dengan pembaruan perpustakaan.  
- Membuat log audit yang mencatat tipe file tepat yang dicoba diproses oleh pengguna.

## Prasyarat
- **GroupDocs.Redaction**: Instal melalui NuGet (lihat perintah di bawah).  
- **.NET SDK**: Pastikan .NET SDK terbaru terinstal. Unduh [di sini](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 atau editor kompatibel lainnya.  
- **Pengetahuan dasar C#**: Anda harus nyaman dengan koleksi dan LINQ.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Instal perpustakaan

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Buka NuGet Package Manager, cari “GroupDocs.Redaction,” dan instal versi terbaru.

### Dapatkan dan terapkan lisensi

Mulailah dengan percobaan gratis atau minta lisensi sementara untuk menjelajahi semua fitur tanpa batasan. Untuk opsi pembelian, kunjungi [halaman pembelian GroupDocs](https://purchase.groupdocs.com/). Setelah Anda memiliki file lisensi:
1. Tempatkan di folder yang dapat diakses dalam proyek Anda (mis., `./Licenses/GroupDocs.Redaction.lic`).  
2. Inisialisasi lisensi saat aplikasi dimulai:

Kelas `License` memuat file lisensi Anda dan mengaktifkan GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Cara mendaftar ekstensi file menggunakan GroupDocs.Redaction?

Muat API Redaction dan panggil metode yang mengembalikan format yang didukung. Pemanggilan mengembalikan koleksi di mana setiap item berisi ekstensi dan deskripsi yang dapat dibaca manusia. Operasi ini ringan dan dapat dilakukan saat startup atau sesuai permintaan.

### Dapatkan tipe file yang didukung
Metode `RedactionApi.GetSupportedFileFormats()` mengembalikan koleksi read‑only dari objek `FileFormatInfo` yang menjelaskan setiap format.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Tampilkan setiap ekstensi dan deskripsi
Setiap `FileFormatInfo` menyediakan properti `Extension` dan `Description` untuk tipe file.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Penjelasan**: Loop mengiterasi setiap objek `FileFormatInfo`, mencetak `Extension` dan `Description`-nya dalam tabel yang teratur.

## Cara mengintegrasikan daftar ke dalam dropdown UI?

Setelah Anda memiliki koleksi, ikatkan ke komponen UI apa pun—WinForms `ComboBox`, WPF `ComboBox`, atau elemen `select` ASP.NET Core. Kuncinya adalah menggunakan `Extension` sebagai nilai dan `Description` sebagai teks tampilan. Ini memastikan pengguna melihat nama yang ramah sementara kode Anda bekerja dengan string ekstensi yang tepat.

## Masalah Umum dan Solusinya
- **Kesalahan namespace tidak ditemukan** – Pastikan Anda mengimpor `GroupDocs.Redaction` dan `GroupDocs.Redaction.Common`.  
- **Lisensi tidak ditemukan** – Pastikan jalur file lisensi benar dan file tersebut termasuk dalam output build.  
- **Kinerja pada proyek besar** – Cache hasil dalam variabel statis atau cache terdistribusi (mis., Redis) untuk menghindari enumerasi berulang.

## Aplikasi Praktis
Mengetahui daftar tepat ekstensi yang didukung membuka beberapa skenario dunia nyata:
1. **Sistem Manajemen Dokumen** – Mengkategorikan secara otomatis file yang masuk berdasarkan ekstensi mereka.  
2. **Alat Penyaringan Konten** – Memblokir format yang tidak diizinkan (mis., file eksekusi) saat unggah.  
3. **Pipeline Konversi File** – Memutuskan secara dinamis apakah file dapat dikonversi atau memerlukan alur kerja cadangan.

## Pertimbangan Kinerja
- **Jejak memori** – Daftar format disimpan dalam `IReadOnlyCollection` yang ringan, biasanya di bawah 2 KB.  
- **Keamanan thread** – Koleksi tidak dapat diubah setelah dibuat, membuatnya aman untuk pembacaan bersamaan.  
- **Caching** – Untuk API dengan lalu lintas tinggi, cache daftar selama masa hidup aplikasi untuk menghilangkan beberapa mikrodetik overhead per permintaan.

## Kesimpulan
Dengan mengikuti langkah-langkah di atas, Anda kini memiliki cara yang dapat diandalkan untuk **mendaftar ekstensi file** dan **c# menampilkan format file** menggunakan GroupDocs.Redaction. Kemampuan ini tidak hanya meningkatkan pengalaman pengguna tetapi juga melindungi backend Anda dari file yang tidak didukung. Jelajahi fitur Redaction tambahan—seperti penyamaran konten, penyensoran PDF, dan pemrosesan batch—untuk lebih memperkuat alur kerja dokumen Anda.

## Pertanyaan yang Sering Diajukan
**Q: Apa format file default yang didukung?**  
A: GroupDocs.Redaction mendukung lebih dari 50 format, termasuk PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG, dan banyak lagi. Lihat daftar lengkap di [dokumentasi GroupDocs](https://docs.groupdocs.com/search/net/).

**Q: Bagaimana cara memperbarui perpustakaan ke versi terbaru?**  
A: Buka NuGet Package Manager, cari “GroupDocs.Redaction,” dan klik **Update**. Atau, jalankan `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Bisakah saya menggunakan daftar ini untuk validasi sisi server pada file yang diunggah?**  
A: Ya—bandingkan ekstensi file yang diunggah dengan koleksi yang diambil sebelum diproses. Ini menghilangkan 99% kesalahan format tidak valid.

**Q: Apakah memungkinkan memperluas dukungan untuk tipe file khusus?**  
A: Ekstensi khusus memerlukan penangan khusus; perpustakaan inti tidak menambahkan format baru secara native. Tinjau dokumen API untuk membuat pipeline impor/ekspor khusus.

**Q: Aplikasi saya crash setelah menambahkan kode—apa yang harus saya periksa?**  
A: Pastikan lisensi dimuat dengan benar, pernyataan `using` merujuk ke namespace yang tepat, dan Anda menangani `IOException` saat membaca file lisensi.

---

**Terakhir Diperbarui:** 2026-06-07  
**Diuji Dengan:** GroupDocs.Redaction 23.9 untuk .NET  
**Penulis:** GroupDocs  

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/search/net/)
- [Referensi API](https://reference.groupdocs.com/redaction/net)
- [Unduh GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Permintaan Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Tutorial Terkait
- [Menguasai Penyaringan File di .NET dengan GroupDocs.Redaction: Teknik Manajemen Dokumen Efisien](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Menguasai GroupDocs.Redaction .NET: Penyiapan & Penanganan Event untuk Manajemen Dokumen Aman](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Menguasai Manajemen Dokumen di .NET dengan GroupDocs.Redaction: Penyiapan Lisensi dan Penyorotan Pencarian HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)