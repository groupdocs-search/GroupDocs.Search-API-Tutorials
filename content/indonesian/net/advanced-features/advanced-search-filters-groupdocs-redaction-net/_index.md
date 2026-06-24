---
date: '2026-04-02'
description: Pelajari cara memfilter berdasarkan ekstensi file dan mencari hanya file
  txt dengan GroupDocs.Redaction untuk .NET—tingkatkan efisiensi manajemen dokumen.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filter berdasarkan ekstensi file di .NET menggunakan GroupDocs.Redaction
type: docs
url: /id/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filter berdasarkan ekstensi file di .NET menggunakan GroupDocs.Redaction

Mencari melalui koleksi file yang sangat besar dapat terasa menakutkan, terutama ketika Anda hanya membutuhkan hasil dari tipe file tertentu. Dalam tutorial ini Anda akan menemukan **cara memfilter berdasarkan ekstensi file** dengan GroupDocs.Redaction untuk .NET, memungkinkan Anda mencari hanya file txt atau ekstensi lain yang Anda pilih. Kami akan menjelaskan cara menyiapkan filter berbasis tipe file dan jalur, sehingga Anda dapat dengan cepat menemukan dokumen yang tepat.

## Jawaban Cepat
- **Apa yang dilakukan “filter berdasarkan ekstensi file”?** Ini membatasi pencarian ke dokumen yang cocok dengan ekstensi file tertentu (mis., *.txt).  
- **Mengapa menggunakan GroupDocs.Redaction untuk ini?** Ini menyediakan API filter bawaan yang cepat dan mudah diintegrasikan.  
- **Apakah saya memerlukan lisensi?** Percobaan gratis berfungsi untuk pengujian; lisensi berbayar diperlukan untuk produksi.  
- **Versi .NET mana yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Bisakah saya menggabungkan filter tipe file dan jalur?** Ya—terapkan beberapa filter untuk pencarian yang sangat tepat.

## Apa yang akan Anda pelajari
- Cara **filter berdasarkan ekstensi file** sehingga hanya file teks yang dicari.  
- Cara menyiapkan **filter jalur file** untuk mempersempit hasil ke folder tertentu atau pola penamaan.  
- Tips untuk menjaga indeks tetap cepat dan efisien memori.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- **GroupDocs.Redaction Library** terinstal dan kompatibel dengan proyek .NET Anda.  
- Lingkungan pengembangan seperti Visual Studio atau VS Code.  
- Pengetahuan dasar C# dan familiaritas dengan struktur proyek .NET.

## Menyiapkan GroupDocs.Redaction untuk .NET

Pertama, tambahkan pustaka ke proyek Anda.

**Menggunakan .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Menggunakan Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Atau temukan “GroupDocs.Redaction” di UI NuGet Package Manager dan instal versi terbaru.

### Akuisisi Lisensi

Anda dapat memulai dengan percobaan gratis atau meminta lisensi sementara. Untuk proyek jangka panjang, beli lisensi dari situs resmi.

### Inisialisasi Dasar

Setelah paket terinstal, buat indeks yang akan menyimpan referensi ke dokumen Anda:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Panduan Implementasi

### Fitur 1: Menetapkan filter untuk dokumen teks (.txt)

#### Cara memfilter berdasarkan ekstensi file untuk dokumen teks

1. **Tentukan indeks dan folder dokumen**  
   Atur jalur tempat file sumber Anda berada:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Buat Indeks**  
   Muat semua file dari folder sumber ke dalam indeks:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Konfigurasikan Opsi Pencarian dengan filter ekstensi file**  
   Beritahu mesin untuk hanya mempertimbangkan file *.txt:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Lakukan pencarian**  
   Jalankan kueri; filter memastikan file non‑teks diabaikan:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Penjelasan*: Metode `Search` mengembalikan hasil yang memenuhi filter, secara dramatis mengurangi kebisingan dan meningkatkan kinerja.

### Fitur 2: Filter Jalur File

#### Mengapa menggunakan filter jalur file?

Kadang-kadang Anda perlu membatasi pencarian ke folder departemen tertentu atau sekumpulan file yang memiliki konvensi penamaan yang sama. Filter jalur memungkinkan Anda melakukan hal itu.

1. **Tentukan indeks dan folder dokumen**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Buat Indeks**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Konfigurasikan Opsi Pencarian dengan ekspresi reguler berbasis jalur**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Ekspresi reguler ini mencocokkan setiap file yang jalur lengkapnya mengandung kata “Lorem”, memungkinkan Anda menargetkan sub‑folder tertentu.

4. **Jalankan pencarian berbasis jalur**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Aplikasi Praktis
- **Manajemen Dokumen Hukum** – Cepat menemukan kontrak relevan yang disimpan sebagai file teks biasa.  
- **Penelitian Akademik** – Ambil hanya catatan penelitian *.txt yang berada di folder proyek tertentu.  
- **Pelaporan Korporat** – Filter laporan internal berdasarkan jalur departemen (mis., `/Finance/2025/`).  

## Pertimbangan Kinerja
- Indeks hanya tipe dokumen yang benar‑benar Anda butuhkan; file yang tidak diperlukan meningkatkan ukuran indeks dan waktu pencarian.  
- Jaga indeks Anda tetap terbaru dengan pekerjaan terjadwal yang memanggil `index.Add()` untuk file baru atau yang berubah.  
- Gunakan ekspresi reguler sederhana; pola yang terlalu kompleks dapat memperlambat mesin pencari.  
- Hapus objek `Index` ketika tidak lagi diperlukan untuk membebaskan memori.

## Kesimpulan
Anda sekarang tahu cara **memfilter berdasarkan ekstensi file** dan menerapkan **filter jalur file** menggunakan GroupDocs.Redaction untuk .NET. Teknik ini memberi Anda kontrol detail atas koleksi dokumen besar, membuat pencarian lebih cepat dan lebih relevan. Selanjutnya, coba menggabungkan beberapa filter atau mengintegrasikan pencarian ke dalam alur kerja aplikasi yang lebih besar.

## Bagian FAQ

**Q1: Bisakah saya memfilter dokumen selain file teks?**  
A1: Ya, GroupDocs.Redaction mendukung banyak format. Ubah argumen dalam `CreateFileExtension` ke ekstensi yang diinginkan (mis., ".pdf").

**Q2: Bagaimana cara memperbarui indeks pencarian saya secara teratur?**  
A2: Jadwalkan layanan latar belakang atau pekerjaan cron yang menjalankan `index.Add()` pada direktori yang ingin Anda perbarui.

**Q3: Apakah ada dampak kinerja saat memfilter berdasarkan jalur file?**  
A3: Ekspresi reguler yang dioptimalkan dengan baik memiliki dampak minimal, tetapi selalu lakukan benchmark dengan dataset Anda sendiri.

**Q4: Bisakah saya menggabungkan beberapa filter untuk pencarian yang lebih halus?**  
A4: Tentu saja. Anda dapat menautkan filter atau membuat filter komposit untuk menargetkan tipe file dan jalur secara bersamaan.

**Q5: Di mana saya dapat menemukan lebih banyak sumber tentang GroupDocs.Redaction?**  
A5: Kunjungi dokumentasi resmi di [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) untuk panduan detail dan referensi API.

## Pertanyaan yang Sering Diajukan

**Q: Apakah `SearchDocumentFilter` bekerja dengan file terenkripsi?**  
A: Filter itu sendiri beroperasi pada metadata file, sehingga file terenkripsi tetap diindeks jika Anda menyediakan kredensial dekripsi yang diperlukan selama proses pengindeksan.

**Q: Bisakah saya menggunakan wildcard alih-alih ekspresi reguler untuk filter jalur?**  
A: API saat ini memerlukan ekspresi reguler, tetapi Anda dapat mensimulasikan wildcard sederhana (mis., `.*` untuk karakter apa pun).

**Q: Seberapa besar indeks dapat sebelum saya perlu mempertimbangkan sharding?**  
A: Indeks berukuran beberapa ratus gigabyte mungkin mendapat manfaat dari pemisahan menjadi beberapa indeks logis; uji kinerja saat koleksi Anda berkembang.

**Q: Apakah ada metode bawaan untuk menghapus dokumen dari indeks?**  
A: Ya—panggil `index.Delete(documentId)` atau `index.DeleteAll()` untuk mengelola entri usang.

**Q: Apakah ada cara untuk menampilkan pratinjau hasil pencarian sebelum memuat dokumen penuh?**  
A: Objek `SearchResult` menyertakan informasi cuplikan yang dapat Anda tampilkan di UI tanpa membuka seluruh file.

## Sumber Daya
- **Dokumentasi**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **Referensi API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Unduhan**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Dukungan Gratis**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Lisensi Sementara**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Terakhir Diperbarui:** 2026-04-02  
**Diuji Dengan:** GroupDocs.Redaction 23.12 for .NET  
**Penulis:** GroupDocs