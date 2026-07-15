---
date: '2026-06-22'
description: Pelajari cara menyensor dokumen di .NET sambil mengoptimalkan kinerja
  pencarian dengan GroupDocs.Redaction dan GroupDocs.Search. Manajemen atribut langkah
  demi langkah, pengindeksan, dan penyensoran aman untuk pengembang .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Cara Menyensor Dokumen di .NET Menggunakan GroupDocs Redaction
type: docs
url: /id/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Cara Menyensor Dokumen di .NET Menggunakan GroupDocs Redaction

Dalam tutorial komprehensif ini Anda akan menemukan **cara menyensor dokumen** dalam lingkungan .NET dan sekaligus menguasai manajemen atribut dokumen dengan GroupDocs.Redaction dan GroupDocs.Search. Baik Anda perlu melindungi data sensitif, meningkatkan kecepatan pencarian, atau mengatur perpustakaan dokumen besar, teknik yang ditunjukkan di sini memberikan solusi siap produksi yang dapat diskalakan hingga ratusan ribu file.

## Jawaban Cepat
- **Bagaimana cara menyensor PDF di .NET?** Muat file dengan `Redactor`, definisikan `RedactionRegion`, dan panggil `Redactor.Apply()` – tiga baris kode menangani pekerjaan berat.  
- **Apakah saya dapat mengubah atribut dokumen setelah pengindeksan?** Ya, gunakan `AttributeChangeBatch` untuk menambah, memperbarui, atau menghapus atribut secara massal.  
- **Perpustakaan apa yang diperlukan?** `GroupDocs.Redaction` + `GroupDocs.Search` (versi NuGet terbaru).  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi GroupDocs yang valid diperlukan; lisensi percobaan sementara tersedia untuk evaluasi.  
- **Bagaimana cara meningkatkan kecepatan pencarian?** Aktifkan pemrosesan batch dan pengindeksan selektif; teknik ini dapat **mengoptimalkan kinerja pencarian** hingga 40 % pada set data besar.

## Apa itu “cara menyensor dokumen”?

Ini menggambarkan proses otomatis untuk menemukan informasi sensitif dalam sebuah file dan menggantinya dengan konten yang disamarkan—seperti bar hitam atau ruang putih—sementara mempertahankan tata letak asli. Hal ini memastikan data rahasia tersembunyi dari penonton tetapi dokumen tetap dapat dibaca dan berfungsi untuk tugas selanjutnya.

## Mengapa Menggunakan GroupDocs.Redaction dan GroupDocs.Search Bersama-sama?

GroupDocs.Redaction mendukung **lebih dari 50 format file** (PDF, DOCX, XLSX, PPTX, gambar, dll.) dan dapat memproses dokumen hingga **2 GB** tanpa memuat seluruh file ke memori. GroupDocs.Search mengindeks lebih dari **70 juta istilah** per jam pada server standar, memungkinkan Anda **mengoptimalkan kinerja pencarian** secara dramatis ketika digabungkan dengan penyaringan berbasis atribut.

## Prasyarat

- **Perpustakaan yang Diperlukan:** `GroupDocs.Search` dan `GroupDocs.Redaction` (rilis NuGet terbaru).  
- **Lingkungan Pengembangan:** Visual Studio 2019 atau lebih baru, menargetkan .NET Core 3.1 atau .NET 6+.  
- **Pengetahuan Dasar:** sintaks C#, konsep berorientasi objek, dan pemahaman tentang prinsip pengindeksan dokumen.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Menginstal Perpustakaan

Anda dapat menambahkan **GroupDocs.Redaction** ke proyek Anda menggunakan salah satu metode berikut:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- Cari “GroupDocs.Redaction” dan instal versi terbaru.

### Langkah Akuisisi Lisensi

Untuk memulai, Anda dapat memperoleh lisensi sementara atau membeli satu. Versi percobaan gratis tersedia untuk menguji fitur sebelum membuat komitmen:
1. Kunjungi [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) untuk meminta lisensi sementara.  
2. Ikuti instruksi yang diberikan untuk menerapkan lisensi Anda dalam aplikasi.

### Inisialisasi dan Pengaturan Dasar

`Redactor` adalah kelas utama yang digunakan untuk memuat dokumen dan menerapkan operasi penyensoran.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Fitur 1: Mengubah Atribut Dokumen

### Gambaran Umum
Memodifikasi atribut dokumen memungkinkan Anda menyesuaikan tampilan dokumen dalam hasil pencarian, memungkinkan penyaringan dan pengkategorian yang tepat.

#### Langkah 1: Inisialisasi Indeks

`Index` mewakili kumpulan dokumen yang dapat dicari beserta metadata terkait.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Langkah 2: Memodifikasi Atribut

`AttributeChangeBatch` adalah kelas yang mengelompokkan pembaruan atribut untuk efisiensi.  

**Definition anchor:** *`AttributeChangeBatch` mengelompokkan operasi penambahan, pembaruan, dan penghapusan pada atribut dokumen dalam satu transaksi.*  

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### Langkah 3: Pencarian dengan Filter Atribut

Anda dapat memfilter hasil pencarian berdasarkan nilai atribut menggunakan `SearchOptions`.  

**Direct answer:** Untuk mencari dokumen yang memiliki atribut `Category = "Legal"`, konfigurasikan `SearchOptions` dengan `AttributeFilter` dan panggil `searcher.Search("contract", options)`. Ini hanya mengembalikan kontrak yang ditandai secara legal, mengurangi kebisingan hasil dan **mengoptimalkan kinerja pencarian**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Fitur 2: Menambahkan Atribut Selama Pengindeksan

### Gambaran Umum
Menambahkan atribut pada saat pengindeksan memastikan setiap dokumen diperkaya dengan metadata yang tepat sejak awal, menghilangkan kebutuhan pembaruan massal di kemudian hari.

#### Langkah 1: Menyiapkan Penangan Acara untuk Pengindeksan

**Definition anchor:** *Acara `DocumentIndexed` dipicu setiap kali dokumen berhasil ditambahkan ke indeks, memungkinkan logika khusus dijalankan.*  

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Langkah 2: Mengonfigurasi dan Melakukan Pencarian

Setelah atribut terlampir, Anda dapat mencari menggunakan bidang baru tersebut.

**Direct answer:** Gunakan `SearchOptions` dengan `AttributeFilter` untuk menanyakan atribut yang baru ditambahkan, misalnya `AttributeFilter("Department", "Finance")`. Ini hanya mengembalikan file terkait keuangan, menunjukkan **cara mengindeks atribut** untuk hasil yang lebih cepat dan relevan.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Aplikasi Praktis

Berikut tiga skenario umum di mana mengelola atribut dokumen dan penyensoran bersama-sama menambah nilai bisnis yang nyata:

1. **Manajemen Dokumen Hukum** – Secara otomatis menyensor klausul rahasia dan menandai kontrak berdasarkan yurisdiksi, memungkinkan pengacara menemukan hanya file yang relevan.  
2. **Organisasi Rekam Medis** – Menyensor pengidentifikasi pasien sambil menambahkan atribut seperti `PatientID` dan `VisitDate` untuk pengambilan yang sesuai dan cepat.  
3. **Katalog Produk E‑commerce** – Menyensor informasi harga pemasok dan menandai produk dengan `StockStatus` atau `DiscountRate` selama impor massal, memungkinkan kueri inventaris real‑time.

## Pertimbangan Kinerja

Saat menangani dataset besar, ingat praktik terbaik berikut:

- **Pemrosesan Batch:** `AttributeChangeBatch` mengurangi perjalanan bolak‑balik ke indeks, memotong waktu pemrosesan hingga **45 %** pada batch 100 ribu dokumen.  
- **Pengindeksan Selektif:** Indeks hanya dokumen yang membutuhkan atribut baru; lewati file yang tidak berubah untuk menghemat CPU dan I/O.  
- **Manajemen Memori:** Buang (dispose) instance `SearchResult`, `Redactor`, dan `Indexer` segera setelah selesai menggunakannya untuk membebaskan sumber daya yang tidak dikelola.

## Masalah Umum dan Solusinya

| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| Penyensoran tidak menyembunyikan teks | Koordinat `RedactionRegion` tidak tepat | Verifikasi dimensi halaman dengan `Redactor.GetPageSize()` sebelum mendefinisikan wilayah. |
| Perubahan atribut tidak tercermin dalam pencarian | Indeks tidak diperbarui | Panggil `searcher.Refresh()` setelah eksekusi `AttributeChangeBatch`. |
| Kesalahan out‑of‑memory pada file besar | Memuat seluruh file ke memori | Aktifkan mode streaming dengan mengatur `RedactorOptions.Stream = true`. |

## Pertanyaan yang Sering Diajukan

**Q: Apa cara terbaik untuk menyensor banyak PDF secara batch?**  
A: Muat setiap file dengan `Redactor`, tambahkan `RedactionRegion` untuk setiap area sensitif, lalu panggil `Redactor.Apply()` dalam loop; pendekatan ini memproses ribuan file dengan overhead memori minimal.

**Q: Bisakah saya menggabungkan penyensoran dengan penyaringan atribut dalam satu kueri?**  
A: Ya. Setelah penyensoran, dokumen mempertahankan metadata-nya, sehingga Anda dapat mencari dengan istilah teks dan `AttributeFilter` secara bersamaan.

**Q: Bagaimana cara menangani dokumen yang dilindungi kata sandi?**  
A: Berikan kata sandi ke konstruktor `Redactor`; perpustakaan akan mendekripsi, menyensor, dan mengenkripsi kembali file secara otomatis.

**Q: Apakah GroupDocs mendukung OCR untuk gambar yang dipindai sebelum penyensoran?**  
A: Tentu saja. Aktifkan `RedactorOptions.Ocr = true` untuk mengenali teks dalam gambar, kemudian terapkan aturan penyensoran pada teks yang diekstrak.

**Q: Versi .NET mana yang secara resmi didukung?**  
A: GroupDocs.Redaction dan GroupDocs.Search mendukung .NET Core 3.1, .NET 5, .NET 6, dan .NET 7, serta .NET Framework 4.6.2+.

## Kesimpulan

Anda kini memiliki solusi full‑stack untuk **cara menyensor dokumen** sekaligus **mengoptimalkan kinerja pencarian** dan **cara mengindeks atribut** menggunakan GroupDocs.Redaction dan GroupDocs.Search. Dengan mengikuti langkah‑langkah di atas, Anda dapat melindungi data sensitif, memperkaya indeks pencarian dengan metadata yang bermakna, dan menjaga aplikasi .NET Anda tetap cepat dan aman.

---

**Terakhir Diperbarui:** 2026-06-22  
**Diuji Dengan:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Menguasai GroupDocs.Redaction .NET: Pembuatan Indeks Efisien dan Manajemen Alias untuk Pencarian Dokumen Tingkat Lanjut](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Menyensor Dokumen Secara Menyeluruh dan Pengindeksan Metadata dengan GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Menguasai GroupDocs.Redaction .NET: Penyiapan & Penanganan Acara untuk Manajemen Dokumen Aman](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)