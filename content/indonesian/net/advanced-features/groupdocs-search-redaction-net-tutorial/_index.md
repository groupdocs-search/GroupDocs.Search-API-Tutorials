---
date: '2026-04-04'
description: Pelajari cara mencari dokumen hukum dan mengelola indeks menggunakan
  GroupDocs.Search, serta mengintegrasikan penyensoran untuk rekam medis dengan GroupDocs.Redaction
  di .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Cari Dokumen Hukum dengan GroupDocs Search & Redaction untuk .NET
type: docs
url: /id/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Cari Dokumen Hukum dengan GroupDocs Search & Redaction di .NET

Di lingkungan yang didorong oleh data saat ini, **mencari dokumen hukum** dengan cepat dan aman merupakan kebutuhan kritis bagi setiap organisasi. Baik Anda menangani kontrak, pengajuan pengadilan, atau laporan kepatuhan, GroupDocs.Search memberikan indeks yang cepat dan skalabel, sementara GroupDocs.Redaction memastikan informasi sensitif tetap tersembunyi. Tutorial ini memandu Anda melalui penyiapan indeks yang dapat dicari, menambahkan dokumen dari beberapa folder, dan mengonfigurasi redaction sehingga Anda dapat mencari rekam medis dan file rahasia lainnya dengan aman.

## Jawaban Cepat
- **Apa yang dilakukan GroupDocs.Search?** Ia membuat indeks pencarian full‑text untuk berbagai format dokumen.  
- **Bisakah saya men-redact informasi sebelum pencarian?** Ya – gunakan GroupDocs.Redaction untuk menyamarkan atau menghapus data sensitif.  
- **Bagaimana cara menambahkan dokumen ke indeks?** Panggil `index.Add("folderPath")` untuk setiap folder yang ingin Anda sertakan.  
- **Jenis file apa yang didukung?** PDF, DOCX, PPTX, TXT, dan banyak lagi.  
- **Apakah saya memerlukan lisensi untuk produksi?** Versi percobaan sementara tersedia; lisensi permanen diperlukan untuk penggunaan komersial.

## Prasyarat
Untuk mengikuti tutorial ini, pastikan Anda memiliki:
- .NET Core SDK (3.1 atau lebih baru) terpasang.
- Visual Studio Code, Visual Studio, atau IDE lain yang mendukung .NET.
- Familiaritas dasar dengan pemrograman C#.

### Akuisisi Lisensi
Anda dapat memulai dengan percobaan gratis untuk kedua pustaka. Untuk penggunaan jangka panjang, pertimbangkan memperoleh lisensi sementara atau membeli satu dari [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

## Menginstal Paket yang Diperlukan

**Instalasi GroupDocs.Search:**  
Menggunakan **.NET CLI**, jalankan:
```bash
dotnet add package GroupDocs.Search
```
Sebagai alternatif, gunakan Package Manager Console di Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**Instalasi GroupDocs.Redaction:**  
- Gunakan .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Atau, melalui Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Kunjungi UI NuGet Package Manager dan cari "GroupDocs.Redaction" untuk menginstalnya jika Anda lebih suka GUI.

## Konfigurasi Pengaturan Redaktor
Sebelum Anda mulai melakukan redaction, Anda mungkin ingin menyesuaikan perilaku redaktor (mis., mengatur warna redaction atau mendefinisikan pola khusus). Potongan kode berikut menunjukkan inisialisasi dasar:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Tips pro:** Sesuaikan `redactorSettings` agar sesuai dengan kebijakan kepatuhan organisasi Anda (mis., mengganti teks dengan kotak hitam, menerapkan OCR sebelum redaction, dll.).

## Panduan Implementasi

### Cara Mencari Dokumen Hukum?
Membuat indeks yang dapat dicari adalah dasar untuk pengambilan dokumen hukum yang cepat. GroupDocs.Search memungkinkan Anda menunjuk ke folder mana pun, membangun indeks, dan kemudian mengeksekusi kueri kompleks di ribuan file.

### Cara Menambahkan Dokumen ke Indeks
Menambahkan dokumen sangat mudah—cukup arahkan pustaka ke direktori yang menyimpan file Anda. Anda dapat menambahkan beberapa folder, yang berguna ketika korpus hukum Anda tersebar di lokasi yang berbeda.

#### Membuat dan Mengelola Indeks
**Gambaran Umum:**  
Membuat indeks adalah langkah pertama menuju operasi pencarian dokumen yang efisien. GroupDocs.Search memungkinkan Anda membuat indeks yang dapat dicari di direktori mana pun pilihan Anda, memungkinkan pengambilan dokumen yang cepat.

##### Langkah 1: Buat Indeks
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Penjelasan:* `Index` menginisialisasi indeks pencarian pada direktori yang ditentukan. Pastikan jalur mencerminkan struktur folder proyek Anda.

##### Langkah 2: Menambahkan Dokumen ke Indeks
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Penjelasan:* Metode `Add` memindai folder yang diberikan dan memasukkan setiap dokumen yang didukung ke dalam indeks. Gunakan ini untuk **menambahkan dokumen ke indeks** dari berbagai sumber, seperti kontrak, berkas kasus, atau rekam medis.

### Mengambil dan Menampilkan Laporan Pengindeksan
**Gambaran Umum:**  
Laporan pengindeksan memberi Anda wawasan tentang berapa banyak dokumen yang diproses, total jumlah istilah, dan ukuran penyimpanan—metrik penting untuk penyetelan kinerja.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Penjelasan:* `GetIndexingReports` mengembalikan array laporan yang merinci proses pengindeksan, membantu Anda memantau dan mengoptimalkan kinerja.

## Aplikasi Praktis
1. **Manajemen Dokumen Hukum:** Mengotomatiskan pengindeksan berkas kasus untuk pengambilan instan undang‑undang, brief, dan putusan.  
2. **Sistem Rekam Medis:** Mencari rekam pasien sambil menjaga privasi menggunakan GroupDocs.Redaction untuk menyamarkan PHI.  
3. **Portal HR Korporat:** Menggabungkan file karyawan yang dapat dicari dengan redaction untuk melindungi data pribadi.

## Pertimbangan Kinerja
- **Mengoptimalkan Ukuran Indeks:** Secara berkala memangkas entri usang dan membangun ulang indeks agar tetap ramping.  
- **Manajemen Memori:** Manfaatkan garbage collector .NET; dispose objek `Index` ketika tidak lagi diperlukan.  
- **Praktik Terbaik Skalabilitas:** Simpan indeks pada penyimpanan SSD cepat dan pertimbangkan sharding korpus besar di beberapa indeks.

## Pertanyaan yang Sering Diajukan

**Q: Apa penggunaan utama GroupDocs.Search?**  
A: Ideal untuk membuat indeks yang dapat dicari dari koleksi dokumen besar, memungkinkan pengambilan cepat file hukum dan medis.

**Q: Bagaimana GroupDocs.Redaction memastikan privasi data?**  
A: Memungkinkan Anda mendefinisikan pola redaction yang secara permanen menghapus atau menyamarkan informasi sensitif sebelum dokumen diindeks atau dibagikan.

**Q: Bisakah saya menggunakan pustaka ini di lingkungan cloud?**  
A: Ya—kedua pustaka bekerja di Azure, AWS, atau deployment .NET berbasis kontainer dengan lisensi yang tepat.

**Q: Format file apa yang didukung oleh GroupDocs.Search?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML, dan banyak lagi format perusahaan.

**Q: Bagaimana cara mengatasi kesalahan pengindeksan?**  
A: Verifikasi jalur folder, periksa izin file, dan tinjau output konsol dari `IndexingReport` untuk kode kesalahan spesifik.

## Sumber Daya
- **Dokumentasi:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **Referensi API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Unduh:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Dukungan Gratis:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Lisensi Sementara:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Terakhir Diperbarui:** 2026-04-04  
**Diuji Dengan:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 untuk .NET  
**Penulis:** GroupDocs