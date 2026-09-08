---
date: '2026-07-26'
description: Pelajari cara membuat indeks di .NET menggunakan GroupDocs.Search dan
  mengintegrasikan redaction dengan GroupDocs.Redaction, memungkinkan pencarian dokumen
  yang cepat dan penanganan data.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: Pelajari cara membuat indeks di .NET menggunakan GroupDocs.Search
  dan mengintegrasikan redaction dengan GroupDocs.Redaction, memungkinkan pencarian
  dokumen yang cepat dan penanganan data.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: Cara Membuat Indeks di .NET dengan GroupDocs Search API
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: Cara Membuat Indeks di .NET dengan GroupDocs Search API
type: docs
url: /id/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# Cara Membuat Indeks di .NET dengan GroupDocs Search API

Dalam tutorial ini Anda akan menemukan **cara membuat indeks** untuk aplikasi .NET Anda menggunakan GroupDocs.Search dan kemudian melindungi konten sensitif dengan GroupDocs.Redaction. Pada akhir panduan Anda akan dapat membangun, memperbarui, dan memangkas indeks yang dapat dicari, serta memahami mengapa menggabungkan pencarian dan redaksi merupakan praktik terbaik untuk manajemen dokumen yang aman.

## Jawaban Cepat
- **Apa arti “cara membuat indeks”?** Itu berarti membangun struktur data yang dapat dicari yang memetakan konten dokumen ke kunci pencarian cepat.  
- **Perpustakaan apa yang diperlukan?** GroupDocs.Search dan GroupDocs.Redaction untuk .NET (paket NuGet).  
- **Apakah saya dapat mengindeks PDF, Word, dan gambar?** Ya—lebih dari 150 format didukung secara bawaan.  
- **Bagaimana cara menghapus dokumen dari indeks?** Panggil metode `Delete` dengan path atau ID dokumen.  
- **Apakah redaksi dilakukan sebelum atau setelah pengindeksan?** Redaksi harus dilakukan terlebih dahulu sehingga data yang dilindungi tidak pernah masuk ke indeks.

## Apa itu “cara membuat indeks”?
Frasa **cara membuat indeks** merujuk pada proses menghasilkan struktur data yang dapat dicari yang menyimpan pemetaan istilah‑ke‑dokumen untuk pengambilan cepat. Di GroupDocs, struktur ini berada di disk dan dapat diperbarui secara inkremental tanpa harus membangun ulang seluruh koleksi.

## Mengapa menggunakan GroupDocs.Search dan GroupDocs.Redaction bersama-sama?
GroupDocs.Search mendukung pengindeksan **lebih dari 150 format file** dan dapat menangani indeks yang lebih besar dari **10 GB** sambil menjaga penggunaan memori di bawah 200 MB karena ia melakukan streaming file alih-alih memuat seluruhnya. Menambahkan GroupDocs.Redaction memastikan bahwa teks, gambar, atau metadata rahasia dihapus sebelum konten pernah mencapai indeks, menjamin kepatuhan terhadap GDPR, HIPAA, dan regulasi lainnya.

## Prasyarat

- **Perpustakaan & Versi** – Instal paket NuGet **GroupDocs.Search** dan **GroupDocs.Redaction** terbaru yang kompatibel dengan .NET 6 atau yang lebih baru.  
- **IDE** – Visual Studio 2022 (atau IDE apa pun yang mendukung .NET 6).  
- **Pengetahuan** – Keterampilan dasar C#, familiaritas dengan I/O file, dan pemahaman tentang konsep pengindeksan.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Instalasi

**Menggunakan .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Using Package Manager Console in Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Anda juga dapat menemukan “GroupDocs.Redaction” di UI NuGet Package Manager dan menginstal versi stabil terbaru.

### Akuisisi Lisensi

Anda dapat memperoleh percobaan gratis atau meminta lisensi sementara untuk menjelajahi semua fitur tanpa batasan. Kunjungi [Halaman Pembelian GroupDocs](https://purchase.groupdocs.com/temporary-license/) untuk detail lebih lanjut tentang cara memperoleh lisensi.

### Inisialisasi Dasar

Redactor adalah kelas utama yang melakukan operasi redaksi pada dokumen.  
Potongan kode berikut menunjukkan kode minimal yang diperlukan untuk mulai menggunakan GroupDocs.Redaction:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

Pengaturan sederhana ini adalah semua yang Anda butuhkan untuk mulai menggunakan GroupDocs.Redaction.

## Panduan Implementasi

### Cara membuat indeks?

`Index` mewakili kontainer yang dapat dicari yang menyimpan kamus istilah dan metadata dokumen.  
Muat atau buat objek `Index`, arahkan ke folder tempat file indeks akan disimpan, dan panggil `Create`. Operasi ini menulis file metadata yang diperlukan dan menyiapkan mesin untuk ingest dokumen.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### Langkah 1: Buat Indeks
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### Cara menambahkan dokumen ke indeks?

`Add` menyisipkan satu dokumen ke dalam indeks, sementara `AddFolder` memproses semua file dalam sebuah direktori.  
Anda menambahkan file dengan memanggil `Add` atau `AddFolder`. Mesin membaca setiap file yang didukung, mengekstrak teks, dan memperbarui kamus istilah.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### Langkah 2: Tambahkan Folder Dokumen
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### Cara mengambil jalur yang diindeks?

`GetIndexedPaths` mengembalikan koleksi semua path dokumen yang disimpan dalam indeks.  
Mengambil daftar jalur file yang diindeks memungkinkan Anda memverifikasi dokumen mana yang saat ini dapat dicari.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### Langkah 3: Tampilkan Jalur yang Diindeks
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### Cara menghapus dokumen dari indeks?

`Delete` menghapus dokumen dari indeks berdasarkan path atau identifier-nya.  
Ketika sebuah file dihapus atau menjadi usang, Anda harus menghapus entri tersebut untuk menjaga akurasi hasil pencarian.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### Langkah 4: Hapus Path Spesifik
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### Cara memverifikasi jalur yang tersisa setelah penghapusan?

Setelah penghapusan, Anda dapat menjalankan kembali metode pengambilan untuk memastikan indeks mencerminkan keadaan saat ini.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### Langkah 5: Verifikasi Jalur yang Tersisa
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## Aplikasi Praktis

1. **Sistem Manajemen Dokumen** – Dengan cepat menemukan kontrak, faktur, atau manual di antara jutaan file.  
2. **Tinjauan Dokumen Hukum** – Redaksi informasi yang bersifat istimewa sebelum pengindeksan untuk menghindari paparan tidak sengaja.  
3. **Solusi Arsip** – Mempertahankan metadata yang dapat dicari untuk catatan historis tanpa memuat seluruh arsip ke memori.  
4. **Platform Manajemen Konten** – Menyediakan pencarian seluruh situs untuk blog, basis pengetahuan, dan perpustakaan multimedia.  
5. **Audit Kepatuhan Data** – Memastikan hanya konten yang telah dibersihkan yang dapat dicari, memenuhi persyaratan regulasi.

## Pertimbangan Kinerja

- **Optimalkan Pengindeksan** – Jadwalkan pengindeksan inkremental setiap malam; gunakan `AddFolder` dengan ukuran batch 100 file untuk mengurangi lonjakan I/O.  
- **Manajemen Sumber Daya** – Pantau CPU dan RAM; GroupDocs.Search memproses file secara streaming, menjaga memori puncak di bawah 200 MB bahkan untuk indeks 10 GB.  
- **Praktik Terbaik** – Simpan indeks pada SSD untuk respons kueri sub‑detik, dan aktifkan kompresi (`index.Compression = true`) untuk mengurangi penggunaan disk setengahnya.

## Pertanyaan yang Sering Diajukan

**T: Apakah saya dapat mengindeks file non‑teks dengan GroupDocs?**  
**J:** Ya, GroupDocs.Search dapat mengindeks lebih dari 150 format—termasuk PDF, DOCX, PPTX, XLSX, dan tipe gambar—dengan mengekstrak teks tersemat melalui OCR bila diperlukan.

**T: Bagaimana cara menangani volume dokumen yang besar?**  
**J:** Gunakan `AddFolder` dengan ukuran batch yang dapat dikonfigurasi, jalankan pengindeksan dalam layanan latar belakang, dan secara berkala panggil `Optimize()` untuk menggabungkan segmen indeks kecil.

**T: Apa manfaat menggunakan redaksi bersama pengindeksan?**  
**J:** Redaksi menghapus informasi pribadi yang dapat diidentifikasi sebelum pernah mencapai indeks, menjamin bahwa hasil pencarian tidak pernah menampilkan data yang dilindungi.

**T: Apakah memungkinkan menyesuaikan algoritma pencarian?**  
**J:** GroupDocs.Search menyediakan kamus sinonim, tokenizer khusus, dan filter ekspresi reguler, memungkinkan Anda menyesuaikan skor relevansi secara detail.

**T: Bagaimana cara memecahkan masalah umum pada pengindeksan?**  
**J:** Verifikasi izin folder, pastikan runtime .NET cocok dengan target perpustakaan, dan periksa file log yang dihasilkan di folder indeks untuk pesan kesalahan terperinci.

## Sumber Daya

- **Dokumentasi**: [Dokumen GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **Referensi API**: [Referensi API GroupDocs Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Unduhan**: [Rilis Terbaru GroupDocs](https://releases.groupdocs.com/search/net/)  
- **Dukungan Gratis**: [Forum GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Lisensi Sementara**: [Minta Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)  

Jelajahi sumber daya ini untuk memperdalam pemahaman Anda dan meningkatkan implementasi GroupDocs.Search dan Redaction di .NET. Selamat coding!

---

**Terakhir Diperbarui:** 2026-07-26  
**Diuji Dengan:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 untuk .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Membuat dan Menggabungkan Indeks dengan GroupDocs.Redaction .NET untuk Manajemen Dokumen Efisien](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)  
- [Menguasai GroupDocs.Redaction .NET: Pembuatan Indeks Efisien dan Manajemen Alias untuk Pencarian Dokumen Lanjutan](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)  
- [Menguasai GroupDocs Search dan Redaction di .NET: Panduan Komprehensif untuk Manajemen Dokumen](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)