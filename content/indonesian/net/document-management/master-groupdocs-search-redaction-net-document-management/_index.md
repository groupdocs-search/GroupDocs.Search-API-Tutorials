---
date: '2026-07-16'
description: Pelajari cara menyensor dokumen di .NET menggunakan GroupDocs Search
  dan Redaction, serta menyorot hasil pencarian untuk manajemen dokumen yang lebih
  cepat.
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: Pelajari cara menyensor dokumen di .NET menggunakan GroupDocs Search
  dan Redaction, serta menyorot hasil pencarian untuk manajemen dokumen yang lebih
  cepat.
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: Cara Menyensor Dokumen dengan GroupDocs Search di .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: Cara Menyensor Dokumen dengan GroupDocs Search di .NET
type: docs
url: /id/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# Cara Menyensor Dokumen dengan GroupDocs Search di .NET

Di perusahaan modern, **cara menyensor dokumen** dengan cepat dan aman merupakan tantangan harian. Menggunakan GroupDocs.Search bersama dengan GroupDocs.Redaction untuk .NET memberi Anda solusi kuat yang siap pakai yang tidak hanya menyensor konten sensitif tetapi juga memungkinkan Anda melakukan pencarian fuzzy dan **menyorot hasil pencarian** dalam HTML. Tutorial ini memandu Anda melalui instalasi pustaka, pembuatan indeks, menjalankan kueri fuzzy, dan menghasilkan output yang disorot—semua dengan potongan kode siap produksi yang jelas.

## Jawaban Cepat
- **Apa langkah pertama?** Instal paket NuGet GroupDocs.Search dan GroupDocs.Redaction.  
- **Bisakah saya menyensor PDF dan file Word?** Ya, kedua format didukung secara langsung.  
- **Apakah pencarian fuzzy tersedia?** Tentu – Anda dapat mengatur akurasi dari 0 % hingga 100 %.  
- **Apakah saya membutuhkan lisensi untuk pengembangan?** Lisensi percobaan gratis dapat digunakan untuk pengujian; lisensi berbayar diperlukan untuk produksi.  
- **Apakah solusi ini bekerja pada .NET 6?** Ya, pustaka kompatibel dengan .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, dan .NET 6+.

## Apa itu GroupDocs.Search?
GroupDocs.Search adalah pustaka .NET yang menyediakan pengindeksan cepat dan pencarian full‑text di lebih dari 100 format file. Ia dapat memproses dokumen hingga 2 GB tanpa memuat seluruh file ke memori, menjadikannya ideal untuk repositori berskala besar. Ia mendukung pengindeksan inkremental, analisis multibahasa, dan terintegrasi mulus dengan aplikasi .NET, memungkinkan pengembang membangun pengalaman pencarian yang kuat dengan kode minimal.

## Mengapa menggunakan GroupDocs.Redaction untuk penyensoran dokumen?
GroupDocs.Redaction menawarkan lebih dari 30 pola penyensoran bawaan dan mendukung pemrosesan batch, memastikan data pribadi, klausul rahasia, atau penandaan regulasi dihapus secara permanen. Dalam pengujian benchmark, menyensor PDF 500 halaman memakan waktu kurang dari 2 detik pada server standar. Mesin bekerja pada aliran konten dokumen, memastikan area yang disensor tidak dapat dipulihkan, dan mempertahankan format serta tata letak asli.

## Prasyarat
- **Pustaka yang Diperlukan:** GroupDocs.Search, GroupDocs.Redaction  
- **Platform yang Didukung:** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE:** Visual Studio 2022 atau lebih baru (semua edisi)  
- **Keterampilan Dasar:** Familiaritas dengan C#, file I/O, dan konsep OOP  

## Bagaimana cara menyiapkan GroupDocs.Search dan GroupDocs.Redaction dalam proyek .NET?
Instal paket NuGet melalui .NET CLI, Package Manager Console, atau UI, kemudian tambahkan file lisensi ke proyek Anda. Penyiapan dua langkah ini adalah semua yang Anda butuhkan sebelum menulis kode pengindeksan atau penyensoran. Setelah menambahkan paket, letakkan file lisensi di root aplikasi dan referensikan namespace dalam file kode Anda.

## Menyiapkan GroupDocs.Redaction untuk .NET
Untuk mulai menggunakan GroupDocs.Search dan GroupDocs.Redaction dalam aplikasi .NET Anda, ikuti langkah instalasi berikut:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Cari "GroupDocs.Redaction" dan instal versi terbaru.

### Langkah Akuisisi Lisensi
1. **Free Trial**: Daftar di [GroupDocs](https://www.groupdocs.com) untuk mendapatkan lisensi sementara.  
2. **Purchase**: Untuk akses penuh, beli lisensi dari situs web GroupDocs.  
3. **Temporary License**: Dapatkan untuk tujuan evaluasi melalui tautan yang disediakan.

#### Inisialisasi dan Penyiapan Dasar
Kelas `Index` mewakili indeks yang dapat dicari yang disimpan di disk dan menyediakan metode untuk menambah, memperbarui, dan mengkueri dokumen. Setelah instalasi, inisialisasi proyek Anda dengan konfigurasi yang diperlukan:  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## Panduan Implementasi

### Membuat dan Mengindeks Dokumen
**Overview**  
Fitur ini menunjukkan cara mengatur dokumen secara efisien dengan membuat indeks untuk folder yang berisi banyak file.

#### Langkah 1: Tentukan Jalur  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### Penyiapan dan Eksekusi Pencarian Fuzzy
**Overview**  
Pencarian fuzzy memungkinkan Anda menemukan dokumen meskipun ada perbedaan kecil pada istilah pencarian. Fitur ini menampilkan cara menyiapkan pencarian fuzzy dengan akurasi yang dapat disesuaikan.

#### Langkah 1: Aktifkan Pencarian Fuzzy  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### Sorot Hasil Pencarian dalam Format HTML
**Overview**  
Menyorot hasil pencarian secara visual menandai bagian relevan dalam file, memudahkan analisis cepat.

#### Langkah 1: Siapkan Kompresi Tinggi  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### Langkah 2: Sorot dan Output  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### Tips Pemecahan Masalah
- Pastikan jalur ditentukan dengan benar untuk menghindari kesalahan file‑not‑found.  
- Verifikasi bahwa semua izin yang diperlukan untuk operasi baca/tulis pada direktori telah diatur.  

## Aplikasi Praktis
1. **Legal Document Review** – Dengan cepat menemukan istilah terkait kasus dalam korpus hukum yang besar.  
2. **Academic Research** – Cari di antara ribuan makalah untuk metodologi spesifik.  
3. **Business Intelligence** – Ambil metrik kunci dari laporan kuartalan tanpa penelusuran manual.  
4. **Customer Support** – Pindai tiket dukungan untuk masalah berulang dan sensor data pribadi sebelum analisis.  
5. **Content Management Systems (CMS)** – Tingkatkan pengambilan konten dengan pencarian fuzzy dan sensor otomatis potongan sensitif.  

## Pertimbangan Kinerja
- Optimalkan pengaturan penyimpanan indeks untuk menyeimbangkan kecepatan dan penggunaan disk.  
- Secara rutin perbarui indeks untuk menjaga data tetap terbaru, mengurangi pemrosesan yang tidak perlu.  
- Buang objek yang tidak terpakai dengan cepat untuk mencegah kebocoran memori, terutama saat menangani batch besar.  

## Cara menyensor informasi sensitif dari PDF menggunakan GroupDocs Redaction?
`Redactor` adalah kelas utama yang digunakan untuk menerapkan pola penyensoran pada format dokumen yang didukung. Muat PDF target dengan `Redactor redactor = new Redactor("file.pdf")`, definisikan pola penyensoran (mis., `redactor.AddRedaction(new RedactionPhrase("confidential"))`), dan panggil `redactor.Apply()` – pustaka menimpa file asli dengan konten yang disensor sambil mempertahankan tata letak. Alur kerja satu‑langkah ini menjamin tidak ada jejak frasa yang dilindungi yang tersisa.

## Cara menyorot hasil pencarian dalam HTML setelah kueri fuzzy?
`SearchResultHighlighter` menyediakan utilitas untuk menghasilkan potongan HTML yang disorot dari hasil pencarian. Jalankan kueri fuzzy, ambil fragmen yang cocok, dan berikan ke `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")`. Metode ini membungkus setiap kemunculan dengan tag yang diberikan, menghasilkan potongan HTML dimana setiap istilah relevan ditandai secara visual. HTML yang disorot dapat disematkan langsung ke halaman web atau disimpan sebagai laporan, memudahkan pengguna akhir melihat konteks setiap kecocokan.

## Pertanyaan yang Sering Diajukan

**Q: Apa itu pencarian fuzzy?**  
A: Pencarian fuzzy menemukan kecocokan perkiraan, mentoleransi kesalahan ejaan atau variasi kecil pada istilah kueri.

**Q: Bisakah saya menggunakan pustaka ini dalam proyek komersial?**  
A: Ya, lisensi GroupDocs yang valid memberikan hak penggunaan komersial.

**Q: Bagaimana cara menangani kumpulan dokumen besar secara efisien?**  
A: Gunakan pengindeksan inkremental, sesuaikan `IndexingOptions` untuk ukuran batch, dan jadwalkan rebuild indeks secara reguler untuk menjaga kinerja optimal.

**Q: Format file apa yang didukung oleh GroupDocs.Search?**  
A: Lebih dari 100 format didukung, termasuk PDF, DOCX, XLSX, PPTX, HTML, TXT, dan tipe gambar seperti JPEG dan PNG.

**Q: Apakah ada dukungan multibahasa untuk pencarian dan penyensoran?**  
A: Ya, pustaka mencakup analis bahasa untuk lebih dari 30 bahasa, memungkinkan pencarian dan penyensoran yang akurat pada konten global.

## Sumber Daya
- [dokumentasi](https://docs.groupdocs.com/search/net/)  
- [Dokumentasi](https://docs.groupdocs.com/search/net/)  
- [forum dukungan](https://forum.groupdocs.com/c/search/10)  
- [Referensi API](https://reference.groupdocs.com/redaction/net)  
- [Unduh](https://www.groupdocs.com/products/search-net)

---

**Terakhir Diperbarui:** 2026-07-16  
**Diuji Dengan:** GroupDocs.Search 2.0.0 and GroupDocs.Redaction 2.0.0 for .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Highlight Search Results in .NET Documents Using GroupDocs.Search and Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Master GroupDocs Redaction and Search in .NET: Efficient Document Management and Secure Searching](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
- [Master Document Redaction with GroupDocs.Redaction .NET: Indexing and Managing Aliases for Secure Document Management](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)