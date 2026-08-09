---
date: '2026-06-12'
description: Pelajari cara mencari dan menyunting dokumen di .NET dengan GroupDocs.Search
  dan GroupDocs.Redaction, mengoptimalkan kinerja pencarian dan menangani kesalahan
  pengindeksan.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Cara Mencari dan Menyunting Dokumen di .NET Menggunakan GroupDocs.Search dan
  GroupDocs.Redaction
type: docs
url: /id/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Cari dan Redaksi Dokumen di .NET dengan GroupDocs.Search & GroupDocs.Redaction

Di lingkungan perusahaan modern, kemampuan **search and redact** sangat penting untuk melindungi informasi sensitif sambil menjaga dokumen mudah ditemukan. Tutorial ini memandu Anda membangun solusi .NET yang kuat yang menggabungkan GroupDocs.Search untuk pencarian full‑text cepat dengan GroupDocs.Redaction untuk menghapus data rahasia secara aman. Pada akhir tutorial, Anda akan mengetahui cara menyiapkan pustaka, membuat segmenter teks khusus, menjalankan pencarian berperforma tinggi, dan menerapkan redaksi dengan aman.

## Jawaban Cepat
- **Apa arti “search and redact”?** Itu berarti menemukan teks dalam dokumen dan menutupinya secara permanen.  
- **Pustaka apa yang diperlukan?** GroupDocs.Search dan GroupDocs.Redaction untuk .NET.  
- **Bisakah saya menangani konten multibahasa?** Ya—gunakan segmenter teks khusus untuk memisahkan kata dengan benar.  
- **Bagaimana cara meningkatkan kecepatan pencarian?** Lakukan indexing sekali, gunakan kembali indeks, dan aktifkan pengaturan `optimize search performance`.  
- **Bagaimana jika indexing gagal?** Ikuti panduan “handle indexing errors” di bagian pemecahan masalah.

## Apa itu “search and redact”?

Search and redact adalah proses menemukan istilah tertentu dalam kumpulan dokumen dan kemudian secara permanen menyembunyikan atau menghapus istilah tersebut untuk melindungi privasi atau memenuhi kepatuhan regulasi. Ini menggabungkan pencarian full‑text untuk menemukan informasi sensitif dengan alat redaksi yang mengganti konten sambil mempertahankan tata letak asli dokumen.

## Mengapa Menggunakan GroupDocs.Search dan GroupDocs.Redaction Bersama-sama?

GroupDocs.Search mendukung **50+ format file** dan dapat mengindeks **100.000+ dokumen** dalam kurang dari satu menit pada perangkat keras server tipikal, sementara GroupDocs.Redaction dapat menerapkan redaksi pada **PDF, DOCX, PPTX, dan lainnya** tanpa mengubah tata letak asli. Menggabungkan keduanya memberi Anda solusi satu‑tumpukan yang **mengoptimalkan kinerja pencarian** dan **menangani kesalahan indexing** dengan elegan.

## Prasyarat

- Visual Studio 2022 atau yang lebih baru dengan dukungan .NET 6+.  
- Paket NuGet: **GroupDocs.Search** dan **GroupDocs.Redaction** (versi stabil terbaru).  
- Lisensi GroupDocs yang valid (percobaan atau dibeli).  

### Pustaka yang Diperlukan
- **GroupDocs.Search** – Menyediakan indexing, querying, dan segmentasi khusus.  
- **GroupDocs.Redaction** – Menawarkan redaksi teks, gambar, dan metadata pada format yang didukung.

### Persyaratan Penyiapan Lingkungan
Pastikan mesin pengembangan Anda memiliki izin menulis ke folder tempat indeks akan disimpan.

### Prasyarat Pengetahuan
- Familiaritas dengan C# dan struktur proyek .NET.  
- Pemahaman dasar tentang konsep pemrosesan dokumen (opsional tetapi membantu).

## Bagaimana Cara Menginstal GroupDocs.Redaction untuk .NET?

Anda dapat menambahkan paket Redaction ke proyek Anda menggunakan .NET CLI atau NuGet Package Manager. Perintah tersebut mengunduh versi stabil terbaru dan mendaftarkannya dalam file proyek Anda, sehingga API tersedia untuk langsung digunakan.  

```bash
dotnet add package GroupDocs.Redaction
```  

## Bagaimana Cara Mendapatkan Lisensi untuk GroupDocs?

GroupDocs menawarkan tiga opsi lisensi: percobaan gratis untuk evaluasi, lisensi sementara untuk pengujian pengembangan yang diperpanjang, dan lisensi komersial penuh untuk penggunaan produksi. Versi percobaan menyediakan fungsionalitas terbatas, sementara kunci sementara memperpanjang periode evaluasi, dan lisensi yang dibeli membuka semua fitur serta dukungan prioritas.

## Bagaimana Cara Menginisialisasi GroupDocs.Redaction dalam Aplikasi Saya?

Kelas `Redaction` adalah titik masuk utama untuk menerapkan redaksi pada dokumen yang didukung. Ia memuat file, menyiapkan objek redaksi, dan mengeksekusi proses redaksi, mengembalikan dokumen yang dimodifikasi sambil mempertahankan tata letak asli. Anda juga dapat mengonfigurasi opsi redaksi seperti warna, overlay, dan penghapusan metadata untuk memenuhi persyaratan kepatuhan tertentu.  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Bagaimana Cara Menyiapkan Indeks Menggunakan GroupDocs.Search?

Kelas `Index` mewakili repositori yang dapat dicari yang disimpan di disk. Ia mengelola pembuatan, pembaruan, dan kueri indeks, memungkinkan Anda menambahkan dokumen, membangun ulang indeks, dan menjalankan pencarian cepat pada koleksi besar. Folder indeks dapat berada di penyimpanan lokal atau jaringan, dan Anda dapat mengonfigurasi pengaturan kompresi serta enkripsi untuk melindungi data yang diindeks.  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Apa Itu Segmenter Teks Kustom dan Mengapa Saya Harus Menggunakannya?

Segmenter teks kustom menentukan bagaimana teks mentah dibagi menjadi token yang dapat dicari. Dengan menyesuaikan aturan segmentasi untuk bahasa atau domain tertentu, Anda meningkatkan akurasi tokenisasi, menghasilkan recall dan relevansi yang lebih tinggi dalam hasil pencarian. Ini sangat berguna untuk bahasa dengan batas kata yang kompleks, seperti Jepang atau Arab, di mana tokenizer default mungkin memisahkan kata secara tidak tepat.  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Bagaimana Cara Melakukan Pencarian Full‑Text dengan Segmenter Kustom?

Objek `SearchQuery` mengenkapsulasi kueri pengguna dan bekerja dengan segmenter kustom untuk menemukan kecocokan. Ia mendukung pencocokan fuzzy, kueri frasa, dan pemberian bobot, mengembalikan set hasil dengan ID dokumen, posisi hit, dan skor relevansi. Anda juga dapat menerapkan filter seperti tipe file atau rentang tanggal untuk mempersempit hasil demi penargetan yang lebih tepat.  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Bagaimana Cara Menerapkan Redaksi Setelah Menemukan Teks Sensitif?

API `Redaction` memungkinkan Anda mengganti atau menghapus teks, gambar, dan metadata dalam dokumen yang didukung. Setelah mengidentifikasi istilah sensitif, Anda membuat objek redaksi, menerapkannya, dan menyimpan file yang telah diredaksi, memastikan informasi rahasia tersembunyi secara permanen. Opsi redaksi meliputi menambahkan kotak hitam, menerapkan warna kustom, atau menghapus seluruh objek sambil mempertahankan struktur dokumen.  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## Masalah Umum dan Cara Menangani Kesalahan Indexing

- **Index Not Found:** Verifikasi bahwa jalur indeks ada dan aplikasi memiliki izin baca/tulis.  
- **Search Returns No Results:** Jalankan kembali proses indexing dan pastikan segmenter kustom terdaftar dengan benar.  
- **Redaction Fails on Certain Formats:** Pastikan tipe file didukung; untuk PDF, gunakan versi Redaction terbaru untuk menangani fitur PDF 2.0.

## Aplikasi Praktis

1. **Manajemen Dokumen Hukum:** Cari kontrak untuk “non‑disclosure” dan secara otomatis redaksi klausa sebelum dibagikan ke pihak luar.  
2. **Penelitian Akademik:** Temukan data yang belum dipublikasikan dalam naskah dan sembunyikan untuk proses peer‑review.  
3. **Kontrak Bisnis:** Proses batch ribuan perjanjian, meredaksi pengidentifikasi pribadi sambil mempertahankan bahasa hukum.

## Bagaimana Saya Dapat Mengoptimalkan Kinerja Pencarian untuk Set Dokumen Besar?

Untuk memaksimalkan kinerja, indeks dokumen sekali dan gunakan kembali indeks yang sama untuk kueri berikutnya. Aktifkan pemrosesan paralel, konfigurasikan caching, dan sesuaikan pengaturan indeks untuk mengurangi latensi serta meningkatkan throughput pada server multi‑core. Selain itu, atur flag `EnableMemoryMapping` untuk memungkinkan indeks dimapping ke memori, yang mempercepat operasi baca untuk dataset besar.

## Bagaimana Cara Mengelola Memori .NET Saat Bekerja dengan File Besar?

Manajemen memori yang efisien sangat penting saat menangani dokumen besar. Bungkus objek `Index` dan `Redaction` dalam pernyataan `using` untuk memastikan pembuangan deterministik, dan proses file sebagai stream alih-alih memuat seluruh dokumen ke memori. Memantau performance counter membantu mendeteksi lonjakan memori secara dini, memungkinkan Anda menyesuaikan ukuran batch atau mengaktifkan penyetelan garbage collection.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan GroupDocs.Search dengan metadata non‑teksual?**  
A: Ya—field metadata dapat diindeks bersama konten dokumen, memungkinkan pencarian seperti “author:JohnDoe”.

**Q: Apakah GroupDocs.Redaction mendukung redaksi waktu nyata dalam API web?**  
A: Ya; Anda dapat memanggil API Redaction secara sinkron untuk file kecil atau menempatkan pekerjaan yang lebih besar dalam antrian untuk pemrosesan asinkron.

**Q: Apa yang harus saya lakukan jika indeks menjadi korup?**  
A: Hapus folder indeks yang korup dan bangun kembali menggunakan rutinitas indexing yang sama; pustaka mencatat pesan kesalahan terperinci untuk membantu Anda menemukan penyebabnya.

**Q: Apakah memungkinkan untuk meninjau dokumen yang telah diredaksi sebelum disimpan?**  
A: Tentu saja—panggil `redaction.Apply()` dengan flag `preview` untuk menghasilkan versi sementara untuk ditinjau.

**Q: Versi .NET mana yang secara resmi didukung?**  
A: GroupDocs.Search dan GroupDocs.Redaction mendukung .NET 6, .NET 5, .NET Core 3.1, dan .NET Framework 4.6.2+.

## Sumber Daya

- **Dokumentasi:** [Dokumentasi GroupDocs Redaction](https://docs.groupdocs.com/search/net/)
- **Referensi API:** [Referensi API GroupDocs](https://reference.groupdocs.com/redaction/net)
- **Unduh:** [Rilis GroupDocs](https://releases.groupdocs.com/search/net/)
- **Dukungan Gratis:** [Forum GroupDocs](https://forum.groupdocs.com/c/search/10)
- **Lisensi Sementara:** [Lisensi Sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-06-12  
**Diuji Dengan:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Penulis:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Tutorial Terkait

- [Menguasai GroupDocs Search dan Redaction di .NET: Manajemen Dokumen Lanjutan](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [Implementasikan GroupDocs.Search & Redaction: Perbarui dan Kelola Indeks Dokumen di .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Optimalkan Pengindeksan Dokumen di .NET dengan GroupDocs.Redaction: Pembatalan, Async, dan Thread](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)