---
date: '2026-07-02'
description: Pelajari cara menyensor dokumen dan mengoptimalkan kinerja pencarian
  dengan menambahkan dokumen ke indeks menggunakan GroupDocs.Redaction dan GroupDocs.Search
  untuk .NET.
keywords:
- how to redact documents
- optimize search performance
- add documents to index
- redact pdf c#
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  headline: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  type: TechArticle
- description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  name: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  steps:
  - name: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
    text: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
  - name: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
    text: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
  - name: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
    text: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
  type: HowTo
- questions:
  - answer: Yes—`RedactionEngine` works natively with PDF streams, so you can load
      a PDF, apply redaction objects, and save the result without any format conversion.
    question: Can I redact PDF C# files directly without converting them first?
  - answer: Incremental indexing adds only the new files, keeping the index size stable
      and query latency under 200 ms for typical workloads.
    question: How does adding documents to index affect search speed?
  - answer: Absolutely. Use a Windows Service or Azure Function to call `Index.AddDocument`
      on a timer, feeding newly uploaded files into the index.
    question: Is it possible to schedule automatic re‑indexing?
  - answer: Yes—redaction overwrites the original bytes, making recovery impossible
      even with forensic tools.
    question: Does redaction permanently remove the hidden data?
  - answer: Both .NET Framework 4.6.1+ and .NET Core 3.1+ (including .NET 5/6) are
      officially supported.
    question: What .NET versions are fully supported?
  type: FAQPage
title: Cara Menyensor Dokumen & Mengoptimalkan Indeks Pencarian di .NET dengan GroupDocs
type: docs
url: /id/net/document-management/master-document-redaction-groupdocs-net/
weight: 1
---

# Menguasai Redaksi Dokumen dan Manajemen Indeks Pencarian di .NET dengan GroupDocs

## Pendahuluan

Jika Anda perlu **cara meredaksi dokumen** sambil tetap membuatnya dapat dicari, Anda berada di tempat yang tepat. Tutorial ini memandu Anda menggabungkan **GroupDocs.Redaction** dan **GroupDocs.Search** untuk menyembunyikan data sensitif secara aman dan kemudian **menambahkan dokumen ke indeks** untuk pengambilan cepat. Pada akhir tutorial Anda akan memahami cara **mengoptimalkan kinerja pencarian**, meredaksi file PDF dalam C#, dan membangun pipeline indeksasi yang kuat yang dapat diskalakan dengan data Anda.

## Jawaban Cepat
- **Bagaimana cara saya meredaksi PDF di C#?** Gunakan `RedactionEngine` untuk memuat file, menentukan area redaksi, dan panggil `Save`.  
- **Kelas apa yang membuat indeks pencarian?** Kelas `Index` dari GroupDocs.Search mengelola semua operasi indeksasi.  
- **Bisakah saya menambahkan file baru tanpa membangun ulang seluruh indeks?** Ya—panggil `Index.AddDocument` untuk pembaruan inkremental.  
- **Apakah redaksi memengaruhi hasil pencarian?** Konten yang diredaksi dikecualikan dari indeks, menjaga pencarian tetap bersih.  
- **Versi .NET apa yang didukung?** .NET Framework 4.6.1+, .NET Core 3.1+, dan .NET 5/6.

## Apa itu “cara meredaksi dokumen”?
**“Cara meredaksi dokumen”** mengacu pada proses menghapus atau menyamarkan informasi rahasia dari file secara programatis sehingga data yang disembunyikan tidak dapat dipulihkan atau ditampilkan. Redaksi penting untuk kepatuhan, privasi, dan alur kerja hukum di mana paparan data harus dicegah.

## Mengapa menggunakan GroupDocs untuk redaksi dan pencarian?
GroupDocs mendukung **lebih dari 50 format file** (termasuk PDF, DOCX, PPTX, dan tipe gambar) dan dapat memproses dokumen ratusan halaman tanpa memuat seluruh file ke memori, mencapai **hingga 30 % lebih cepat dalam indeksasi** dibandingkan dengan perpustakaan umum. Suite gabungan Redaction + Search memungkinkan Anda **meredaksi file PDF C#** dan langsung mengindeks versi bersihnya, menghilangkan kebutuhan langkah pra‑pemrosesan terpisah.

## Prasyarat

- **GroupDocs.Search** untuk .NET (v20.11 atau lebih baru)  
- **GroupDocs.Redaction** untuk .NET (v20.10 atau lebih baru)  
- Visual Studio 2017 atau lebih baru  
- .NET Framework 4.6.1 atau lebih baru (atau .NET Core 3.1+)

### Prasyarat Pengetahuan
Anda sebaiknya nyaman dengan sintaks dasar C#, referensi proyek, dan operasi sistem file.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Instalasi pustaka

**.NET CLI**  
`dotnet add package` adalah perintah .NET CLI yang menginstal paket NuGet ke dalam proyek Anda.  

```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
`Install-Package` adalah perintah PowerShell yang digunakan oleh NuGet Package Manager Console untuk menambahkan pustaka.  

```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Cari “GroupDocs.Redaction” dan klik **Install** untuk mengambil rilis stabil terbaru.

### Akuisisi Lisensi
- **Free Trial** – percobaan fitur lengkap selama 30 hari.  
- **Temporary License** – akses perpanjangan 15 hari untuk evaluasi.  
- **Purchase** – lisensi produksi permanen.

#### Inisialisasi Dasar
`RedactionEngine` adalah kelas inti yang digunakan untuk memuat, memodifikasi, dan menyimpan dokumen setelah redaksi.  

```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Further configuration and initialization...
```

## Panduan Implementasi

Mari kita bagi solusi menjadi tiga bagian logis: membuat indeks, menambahkan dokumen (termasuk yang telah diredaksi), dan mencari dalam indeks.

### Cara membuat indeks pencarian dengan GroupDocs.Search?

`Index` adalah kelas utama yang mewakili indeks yang dapat dicari dalam GroupDocs.Search. Anda memuat atau membuat instance `Index` dengan menunjuk ke folder di disk; perpustakaan kemudian mengelola semua file internal untuk Anda. Langkah ini merupakan dasar untuk **mengoptimalkan kinerja pencarian** karena indeks yang terstruktur dengan baik mengurangi latensi kueri.

```csharp
using GroupDocs.Search;

string indexFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldIndex";
```

**Penjelasan:** Kode mendefinisikan direktori yang akan menyimpan file indeks. Menggunakan folder khusus menjaga data indeks terisolasi dari dokumen sumber Anda.

```csharp
Index index = new Index(indexFolder);
```

**Penjelasan:** Menginstansiasi `Index` akan membuka indeks yang ada atau membuat yang baru jika path kosong.

### Cara menambahkan dokumen ke indeks setelah redaksi?

Pertama, redaksi setiap bagian rahasia, kemudian masukkan file bersih ke dalam indeks. Alur dua langkah ini menjamin bahwa hanya konten aman yang dapat dicari.

#### Tentukan folder sumber
`documentsFolder` adalah path tempat PDF asli Anda berada.  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldDocuments";
```

`AddDocument` adalah metode dari kelas `Index` yang menambahkan satu dokumen ke indeks.  

```csharp
index.Add(documentsFolder);
```

### Cara mencari dalam indeks yang dibuat?

Tentukan string kueri, jalankan pencarian, dan iterasi melalui hasil. API mengembalikan nomor halaman, cuplikan, dan pengidentifikasi dokumen, memudahkan penyajian hasil dalam UI.

`SearchResult` menyimpan hasil yang dikembalikan oleh kueri, termasuk dokumen yang cocok dan cuplikan.  

```csharp
string query = "Lorem";
```

```csharp
SearchResult result = index.Search(query);
```

## Aplikasi Praktis

Kemampuan ini menyelesaikan masalah dunia nyata:

1. **Manajemen Dokumen Hukum** – Redaksi nama klien sebelum mengindeks berkas kasus, memastikan privasi sementara pengacara tetap dapat mencari yurisprudensi.  
2. **Rekam Medis** – Menghapus identifikasi pasien dari PDF medis, lalu mengindeks versi yang disanitasi untuk kueri audit cepat.  
3. **Kepatuhan Korporat** – Mengotomatiskan redaksi laporan keuangan dan segera membuat versi bersih dapat dicari untuk penyelidikan internal.

## Pertimbangan Kinerja

Untuk **mengoptimalkan kinerja pencarian** saat menangani volume besar:

- Jalankan indeksasi sebagai pekerjaan latar belakang dan komit perubahan dalam batch.  
- Segera dispose objek `Index` untuk membebaskan sumber daya tak terkelola.  
- Pantau penggunaan memori; GroupDocs.Search men‑stream data dan tidak pernah memuat seluruh dokumen ke RAM.  
- Jadwalkan penggabungan indeks secara berkala untuk menjaga indeks tetap kompak dan cepat dalam kueri.

## Masalah Umum dan Solusinya

| Issue | Solution |
|-------|----------|
| **Kesalahan out‑of‑memory pada PDF besar** | Gunakan `RedactionEngine` dengan `RedactionOptions` yang mengaktifkan mode streaming. |
| **Pencarian mengembalikan istilah yang diredaksi** | Pastikan Anda menjalankan redaksi **sebelum** memanggil `Index.AddDocument`. |
| **Format file tidak didukung** | Verifikasi ekstensi file termasuk dalam 50+ format yang didukung; konversi file yang tidak didukung ke PDF terlebih dahulu. |
| **Lisensi tidak dikenali** | Letakkan file lisensi di root aplikasi dan panggil `License.SetLicense("license.json")` sebelum penggunaan API apa pun. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya meredaksi file PDF C# secara langsung tanpa mengonversinya terlebih dahulu?**  
A: Ya—`RedactionEngine` bekerja secara native dengan aliran PDF, sehingga Anda dapat memuat PDF, menerapkan objek redaksi, dan menyimpan hasilnya tanpa konversi format apa pun.

**Q: Bagaimana penambahan dokumen ke indeks memengaruhi kecepatan pencarian?**  
A: Indeksasi inkremental menambahkan hanya file baru, menjaga ukuran indeks stabil dan latensi kueri di bawah 200 ms untuk beban kerja tipikal.

**Q: Apakah memungkinkan menjadwalkan re‑indeks otomatis?**  
A: Tentu saja. Gunakan Windows Service atau Azure Function untuk memanggil `Index.AddDocument` berdasarkan timer, memasukkan file yang baru diunggah ke dalam indeks.

**Q: Apakah redaksi secara permanen menghapus data tersembunyi?**  
A: Ya—redaksi menimpa byte asli, membuat pemulihan tidak mungkin bahkan dengan alat forensik.

**Q: Versi .NET apa yang sepenuhnya didukung?**  
A: Baik .NET Framework 4.6.1+ maupun .NET Core 3.1+ (termasuk .NET 5/6) secara resmi didukung.

## Sumber Daya
- [Documentation](https://docs.groupdocs.com/search/net/)
- [Referensi API](https://reference.groupdocs.com/redaction/net)
- [Unduh](https://releases.groupdocs.com/search/net/)
- [Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-07-02  
**Diuji Dengan:** GroupDocs.Search 21.2 dan GroupDocs.Redaction 21.1 untuk .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Menguasai GroupDocs.Redaction .NET: Pembuatan Indeks Efisien dan Manajemen Alias untuk Pencarian Dokumen Lanjutan](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Cara Mengindeks dan Mencari Dokumen PDF/Word berdasarkan Subjek Menggunakan GroupDocs.Redaction di .NET](/search/net/indexing/index-search-pdf-word-subject-groupdocs-redaction/)
- [Menguasai GroupDocs Search dan Redaction di .NET: Manajemen Dokumen Lanjutan](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)