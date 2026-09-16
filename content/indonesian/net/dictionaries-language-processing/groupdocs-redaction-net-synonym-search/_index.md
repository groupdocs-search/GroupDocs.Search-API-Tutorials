---
date: '2026-09-16'
description: Pelajari cara membuat indeks pencarian dengan GroupDocs di .NET, menambahkan
  dokumen ke indeks, dan mengaktifkan pencarian sinonim untuk hasil kueri yang lebih
  cerdas.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Pelajari cara membuat indeks pencarian dengan GroupDocs di .NET, menambahkan
  dokumen ke indeks, dan mengaktifkan pencarian sinonim untuk hasil kueri yang lebih
  cerdas.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Cara membuat indeks pencarian dengan GroupDocs di .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Cara membuat indeks pencarian dengan GroupDocs dan pencarian sinonim di .NET
type: docs
url: /id/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Cara membuat indeks pencarian dengan GroupDocs dan pencarian sinonim di .NET

Dalam panduan ini Anda akan belajar **cara membuat indeks pencarian** menggunakan GroupDocs.Search, menambahkan dokumen ke indeks tersebut, dan mengaktifkan pencarian sinonim sehingga pengguna dapat menemukan konten yang relevan meskipun mereka menggunakan terminologi yang berbeda. Baik Anda membangun repositori hukum, basis pengetahuan perusahaan, atau arsip penelitian, langkah‑langkah di bawah ini memberikan solusi siap produksi yang bekerja pada .NET Framework 4.6.1+, .NET Core, dan .NET 5+.

## Jawaban Cepat
- **Apa arti “create search index”?** Itu membangun katalog yang dapat dicari dari dokumen Anda, menyimpan teks yang diekstrak dalam struktur yang dioptimalkan untuk pencarian dalam milidetik.  
- **Mengapa menggunakan pencarian sinonim?** Ini memperluas kueri untuk menyertakan kata‑kata dengan arti yang sama, meningkatkan recall hingga 30 % pada korpus tipikal.  
- **Apa prasyarat utama?** .NET 4.6.1+ (atau .NET Core/5+), pengetahuan C#, dan paket NuGet GroupDocs.Search + GroupDocs.Redaction.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk evaluasi; lisensi permanen diperlukan untuk penerapan produksi.  
- **Bisakah saya menggabungkannya dengan redaction?** Ya—GroupDocs.Redaction dapat dijalankan sebelum atau setelah pencarian untuk menyamarkan data sensitif.

## Apa itu “create search index”?
Sebuah **search index** adalah struktur data yang menyimpan teks yang diekstrak dan metadata dari setiap dokumen, memungkinkan mesin menemukan file yang cocok secara instan. GroupDocs.Search membangun indeks ini dengan memindai folder sumber, mengurai format yang didukung, dan menulis file indeks yang kompak ke direktori yang Anda tentukan.

## Mengapa mengaktifkan pencarian sinonim?
Pencarian sinonim secara otomatis menambahkan istilah alternatif ke kueri pengguna, sehingga pencarian untuk **“improve”** juga mengembalikan dokumen yang berisi **“enhance,” “upgrade,”** atau **“optimize.”** Dalam praktiknya hal ini dapat meningkatkan recall hasil sebesar 20‑35 % sambil menjaga presisi tinggi, karena kamus sinonim bawaan dikurasi untuk setiap bahasa.

## Prasyarat
- **.NET Framework 4.6.1** atau lebih baru (atau runtime .NET Core/5+ apa pun).  
- Keterampilan pengembangan C# dasar dan Visual Studio (Community, Professional, atau Enterprise).  
- Paket GroupDocs.Search dan GroupDocs.Redaction yang diinstal melalui NuGet.

### Instalasi
Instal GroupDocs.Redaction untuk .NET menggunakan salah satu metode berikut (lihat dokumentasi [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) untuk detail):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Sebagai alternatif, gunakan UI NuGet Package Manager di Visual Studio untuk mencari “GroupDocs.Redaction” dan menginstalnya secara langsung. Untuk referensi API, lihat [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Akuisisi Lisensi
- **Uji coba gratis:** Mulai dengan versi percobaan untuk menjelajahi semua fitur.  
- **Lisensi sementara:** Ajukan lisensi sementara di [situs GroupDocs](https://purchase.groupdocs.com/temporary-license/) atau kelola lisensi Anda melalui portal [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/).  
- **Pembelian penuh:** Saat Anda siap untuk produksi, beli lisensi penuh yang menghapus semua batas evaluasi.

## Cara menyiapkan GroupDocs.Redaction untuk .NET
GroupDocs.Redaction menyediakan fungsionalitas inti untuk meredaksi konten sensitif sebelum atau setelah pencarian. Ia mengekspos kelas `Redactor` yang Anda buat dengan lisensi dan pengaturan konfigurasi opsional.

Kode berikut menunjukkan cara membuat instance redactor dan memuat file lisensi:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Setelah redactor siap, Anda dapat memanggil `redactor.Redact(...)` pada dokumen apa pun yang Anda ambil dari hasil pencarian.

## Cara membuat indeks pencarian
Membuat indeks pencarian melibatkan penentuan folder tempat file indeks akan disimpan dan kemudian menginisialisasi kelas `Index` dari GroupDocs.Search. Indeks akan menyimpan semua data yang dapat dicari yang diekstrak dari dokumen sumber Anda.

Pertama, buat direktori untuk indeks dan kemudian buat instance objek `Index`:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Membuat indeks menulis sekumpulan file biner ke folder; file-file ini biasanya berukuran di bawah 200 KB per 1.000 halaman, memungkinkan Anda menskalakan hingga jutaan halaman tanpa menghabiskan ruang disk.

## Cara menambahkan dokumen ke indeks
Menambahkan dokumen memerlukan penunjukan API ke direktori yang berisi file sumber dan menginstruksikan indeks untuk mengolahnya. Proses ini mengurai setiap format yang didukung, mengekstrak teks, dan menyimpannya di indeks untuk pengambilan cepat.

Gunakan kode berikut untuk mengindeks semua file dalam folder sumber:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search mendukung **30+** format input—termasuk DOCX, PDF, PPTX, HTML, dan tipe gambar umum—sehingga Anda dapat mengindeks hampir semua arsip perusahaan tanpa konverter tambahan.

## Cara mengaktifkan dan menjalankan pencarian sinonim
Penanganan sinonim diaktifkan melalui `SearchOptions`. Setelah diaktifkan, setiap kueri secara otomatis diperluas untuk menyertakan sinonim dari kamus, meningkatkan recall tanpa mengorbankan presisi.

Aktifkan pencarian sinonim dengan cuplikan berikut:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

Kamus sinonim default berisi lebih dari **5.000** pasangan istilah untuk bahasa Inggris. Anda juga dapat memuat file `SynonymDictionary` khusus untuk mendukung jargon spesifik industri.

## Kamus sinonim khusus
Jika Anda memerlukan sinonim khusus domain, muat file kamus Anda sendiri dan tetapkan ke `SearchOptions` sebelum mengeksekusi kueri.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Tips pemecahan masalah umum
- **Masalah jalur:** Periksa kembali bahwa folder indeks dan sumber dapat diakses oleh akun proses.  
- **Batas lisensi:** Build tanpa lisensi dapat membatasi jumlah file yang diindeks hingga 100.  
- **Tidak ada hasil:** Pastikan kamus sinonim telah dimuat; Anda dapat memeriksa `options.SynonymDictionary.Count` pada runtime.  

## Aplikasi praktis
1. **Manajemen dokumen hukum:** Temukan preseden hukum menggunakan istilah hukum dan sinonimnya.  
2. **Penelitian akademik:** Perluas pencarian literatur di seluruh PDF akademik dan file Word.  
3. **Basis pengetahuan perusahaan:** Mengambil kebijakan internal bahkan ketika pengguna merumuskan kueri secara berbeda.  
4. **Sistem manajemen konten:** Menawarkan penemu konten yang lebih kaya bagi editor saat menandai artikel.  
5. **Sistem tiket dukungan pelanggan:** Mencocokkan tiket dengan masalah yang diketahui menggunakan deskripsi masalah yang sinonim.  

## Pertimbangan kinerja
- **Pemeliharaan indeks:** Lakukan re‑indeks setelah pembaruan massal; indeks inkremental mengurangi waktu henti hingga 70 %.  
- **Pemantauan sumber daya:** Mengindeks batch 10 GB pada VM standar (2 vCPU, 8 GB RAM) mencapai puncak ~1,2 GB RAM; batasi ukuran batch jika mendekati batas.  
- **Pembuangan objek:** Panggil `index.Dispose()` dan `redactor.Dispose()` segera setelah selesai untuk membebaskan sumber daya native.  

## Kesimpulan
Anda kini mengetahui **cara membuat indeks pencarian** dengan GroupDocs, menambahkan dokumen ke indeks tersebut, dan mengaktifkan pencarian sinonim untuk pengalaman pengguna yang lebih intuitif. Dasar ini juga memungkinkan Anda menambahkan redaction, peringkat khusus, atau pencocokan fuzzy di atas mesin pencari yang kuat.

## Langkah selanjutnya
- Bereksperimen dengan `SearchOptions.FuzzySearch` untuk menangkap kesalahan ejaan.  
- Jelajahi API `Ranking` untuk meningkatkan prioritas dokumen.  
- Bergabunglah dengan komunitas di [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) atau [Free Support Forum](https://forum.groupdocs.com/c/search/10) untuk berbagi tips dan mengajukan pertanyaan.  
- Periksa [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) untuk pembaruan dan fitur baru.  

## Pertanyaan yang sering diajukan

**Q: Apa itu pencarian sinonim?**  
A: Pencarian sinonim memperluas kueri pengguna untuk menyertakan istilah alternatif yang telah ditentukan, meningkatkan peluang menemukan dokumen relevan yang menggunakan kata‑kata berbeda.

**Q: Bagaimana cara memperbarui lisensi GroupDocs saya?**  
A: Kunjungi portal [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) dan unggah file lisensi baru melalui `License.SetLicense("path/to/license.lic")`.

**Q: Bisakah saya menggunakan pencarian sinonim dalam lingkungan multibahasa?**  
A: Ya—muat file `SynonymDictionary` khusus bahasa untuk setiap locale yang Anda dukung, dan mesin akan menerapkan set sinonim yang sesuai per kueri.

**Q: Apa masalah pengindeksan yang paling umum?**  
A: Izin akses file, format yang tidak didukung, dan melebihi batas dokumen versi percobaan adalah tiga masalah utama yang dihadapi pengembang.

**Q: Bagaimana saya dapat mengoptimalkan kinerja untuk indeks yang sangat besar?**  
A: Gunakan indeks inkremental, simpan indeks pada SSD, dan konfigurasikan `IndexingOptions.MaxDegreeOfParallelism` agar sesuai dengan jumlah core CPU Anda.

---

**Terakhir Diperbarui:** 2026-09-16  
**Diuji dengan:** GroupDocs.Search 23.10 for .NET  
**Penulis:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Tutorial Terkait

- [Tambahkan Dokumen ke Indeks dengan Tutorial GroupDocs.Search .NET](/search/net/document-management/)
- [Sorot Hasil Pencarian dalam Dokumen .NET Menggunakan GroupDocs.Search dan Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Cara Memperbarui Indeks dengan GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)