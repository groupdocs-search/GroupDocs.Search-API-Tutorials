---
date: '2026-06-12'
description: Pelajari cara membuat indeks pencarian .NET dan menerapkan redaction
  pada PDF menggunakan GroupDocs.Search dan GroupDocs.Redaction. Penyiapan, penyebaran,
  pengindeksan, dan pencarian lanjutan dijelaskan.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Buat Indeks Pencarian .NET dengan GroupDocs Search dan Redaction – Panduan
  Komprehensif
type: docs
url: /id/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Buat Indeks Pencarian .NET dengan GroupDocs Search dan Redaction – Panduan Komprehensif

Dalam lanskap digital saat ini, solusi **creating a search index .NET** yang dapat menemukan informasi dengan cepat dan melindungi data sensitif menjadi prioritas utama bagi setiap organisasi. Tutorial ini memandu Anda melalui konfigurasi jaringan GroupDocs.Search yang skalabel, penyebaran node, pengindeksan dokumen, dan penggunaan GroupDocs.Redaction untuk **apply redaction to PDF** file—semua dalam lingkungan .NET.

## Jawaban Cepat
- **What is the first step to create a search index .NET?** Tentukan jalur dasar dan port, lalu sebarkan node jaringan.  
- **How do I apply redaction to PDF with GroupDocs?** Inisialisasi instance `Redactor`, muat PDF, dan panggil `Redact` dengan pola yang diinginkan.  
- **Can I run the search network on multiple machines?** Ya—sebar node pada server terpisah dan biarkan node master mengoordinasikan pengindeksan dan kueri.  
- **Do I need a license for production use?** Lisensi GroupDocs yang valid diperlukan untuk produksi; lisensi percobaan sementara tersedia untuk evaluasi.  
- **What .NET versions are supported?** .NET Framework 4.7.2+, .NET Core 3.1+, dan .NET 5/6/7 didukung sepenuhnya.

## Apa itu “create search index .net”?
*Creating a search index .NET* mengacu pada pembuatan repositori yang dapat dicari berisi metadata dokumen dan konten menggunakan pustaka .NET, yang mengekstrak teks, mem-tokenisasi istilah, dan menyimpannya dalam struktur indeks yang dioptimalkan. Ini memungkinkan respons kueri instan di seluruh node terdistribusi, mendukung berbagai format file, dan memungkinkan pengambilan dokumen yang skalabel serta berperforma tinggi dalam aplikasi perusahaan.

## Mengapa menggunakan GroupDocs Search dan Redaction bersama-sama?
GroupDocs.Search mendukung **50+ file formats**—termasuk DOCX, PDF, PPTX, dan HTML—dan dapat mengindeks dokumen ratusan halaman tanpa memuat seluruh file ke memori. Dikombinasikan dengan GroupDocs.Redaction, yang dapat **apply redaction to PDF** dalam kurang dari 200 ms per halaman, Anda mendapatkan alur manajemen dokumen yang aman dan berperforma tinggi.

## Prasyarat

### Perpustakaan & Ketergantungan yang Diperlukan
Untuk mengikuti tutorial ini, instal paket-paket berikut:
- **GroupDocs.Search** for .NET
- **GroupDocs.Redaction** for .NET  

Anda dapat menggunakan salah satu metode berikut untuk menginstal perpustakaan yang diperlukan:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Cari "GroupDocs.Search" dan "GroupDocs.Redaction" lalu instal versi terbaru.

### Persyaratan Penyiapan Lingkungan
- .NET Framework 4.7.2 atau lebih tinggi (atau .NET Core 3.1+)
- Visual Studio IDE (Community, Professional, atau Enterprise)

### Prasyarat Pengetahuan
- Pemrograman C# dasar
- Konsep berorientasi objek
- Familiaritas dengan konfigurasi jaringan dan sistem manajemen dokumen

## Menyiapkan GroupDocs.Redaction untuk .NET

### Informasi Instalasi
Untuk mengintegrasikan fitur redaction ke dalam aplikasi Anda, mulailah dengan menambahkan pustaka GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Cari "GroupDocs.Redaction" dan instal.

### Akuisisi Lisensi
Untuk memulai dengan percobaan gratis atau lisensi sementara, ikuti langkah-langkah berikut:
- Kunjungi [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) untuk meminta lisensi sementara.  
- Untuk opsi pembelian, buka [pricing page](https://groupdocs.com/pricing).

Setelah Anda memiliki file lisensi, terapkan dalam pengaturan aplikasi Anda:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Inisialisasi Dasar
Untuk menginisialisasi GroupDocs.Redaction untuk operasi dasar, gunakan potongan kode berikut:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Panduan Implementasi

### Penyiapan Konfigurasi

#### Ikhtisar
Fitur ini mengkonfigurasi jaringan pencarian Anda menggunakan jalur dasar dan nomor port, membentuk fondasi sistem manajemen dokumen Anda.

#### Definisi Anchor
`SearchNetworkDeployment` adalah kelas yang mengatur penyebaran node pencarian di seluruh jaringan.

#### Langkah 1: Tentukan Jalur Dasar dan Port  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Langkah 2: Konfigurasikan Jaringan
Gunakan metode `Configure` untuk menyiapkan jaringan pencarian dengan jalur dan port yang ditentukan:
```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Penyebaran Node Jaringan

#### Ikhtisar
Sebarkan node dalam jaringan pencarian yang telah dikonfigurasi untuk pencarian dokumen terdistribusi.

#### Definisi Anchor
`SearchNetworkNode` mewakili node pencarian individual yang berkomunikasi dengan node master.

#### Langkah 1: Inisialisasi Penyebaran  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Langganan Event untuk Node Master

#### Ikhtisar
Langganan ke event pada node master untuk memantau dan mengelola operasi jaringan secara efektif.

#### Definisi Anchor
`SearchNetworkNodeEvents` menyediakan callback untuk pengindeksan, eksekusi kueri, dan penanganan error.

#### Langkah 1: Identifikasi Node Master
Pilih node pertama sebagai master Anda:
```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Langkah 2: Langganan ke Event
Langganan ke event menggunakan:
```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Mengindeks Dokumen

#### Ikhtisar
Indeks dokumen untuk operasi pencarian yang efisien. Langkah ini penting untuk memastikan jaringan Anda dapat dengan cepat mengambil data yang diperlukan.

#### Definisi Anchor
`SearchIndex` adalah objek inti yang menyimpan token yang dapat dicari dan metadata untuk setiap file yang diindeks.

#### Langkah 1: Tambahkan Direktori ke Indeks
Tentukan direktori yang berisi dokumen Anda:
```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Fungsionalitas Pencarian – Penggunaan Dasar

#### Ikhtisar
Lakukan operasi pencarian dasar di seluruh node dalam jaringan.

#### Jawaban Langsung
Panggil `SearchNetwork.Query("your term")` pada node master untuk mengambil dokumen yang cocok secara instan. Metode ini mengembalikan koleksi objek `SearchResult` yang mencakup jalur file dan skor relevansi.  
`SearchNetwork.Query` adalah metode yang mengeksekusi kueri pencarian di seluruh jaringan dan mengembalikan hasil yang cocok.

#### Langkah 1: Tentukan Parameter Pencarian  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Fungsionalitas Pencarian Lanjutan

#### Ikhtisar
Manfaatkan teknik pencarian lanjutan dengan parameter yang dapat disesuaikan untuk hasil yang lebih tepat.

#### Jawaban Langsung
Implementasikan metode yang membangun objek `SearchOptions`, mengatur properti `UseFuzzySearch`, `Highlight`, dan `PageSize`, lalu mengirimkannya ke `SearchNetwork.QueryAdvanced`. Ini menghasilkan hasil berhalaman, disorot, dengan pencocokan fuzzy diaktifkan.  
`SearchNetwork.QueryAdvanced` adalah metode yang menjalankan kueri dengan opsi lanjutan seperti pencocokan fuzzy dan paginasi.

#### Langkah 1: Implementasikan Metode Pencarian Lanjutan  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Menerapkan Redaction pada File PDF

#### Ikhtisar
Amankan informasi sensitif dengan meredaksi konten PDF sebelum disimpan atau dibagikan.

#### Jawaban Langsung
Buat instance `Redactor`, muat PDF target, definisikan `RedactionPattern` (mis., regex SSN), panggil `redactor.Apply(pattern)`, dan akhirnya simpan dokumen yang telah diredaksi. Proses ini memastikan data pribadi dihapus secara permanen.

#### Definisi Anchor
`Redactor` adalah kelas utama di GroupDocs.Redaction yang memproses dokumen dan menerapkan aturan redaction.

#### Contoh Alur Kerja (tanpa blok kode baru)
1. Inisialisasi `Redactor` dengan lisensi Anda.  
2. Muat PDF menggunakan `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` mewakili aturan yang menentukan teks atau pola yang akan diredaksi. Definisikan pola seperti `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Jalankan `redactor.Apply(pattern)`.  
5. Simpan output dengan `redactor.Save("sample_redacted.pdf")`.

### Aplikasi Praktis

#### Kasus Penggunaan Dunia Nyata
1. **Legal Document Management** – Cari kontrak secara efisien dan secara otomatis meredaksi pengidentifikasi klien.  
2. **Healthcare Records** – Temukan catatan pasien sambil memastikan redaksi PHI yang sesuai dengan HIPAA.  
3. **Corporate Compliance** – Pindai komunikasi internal untuk istilah terlarang dan redaksi sebelum diarsipkan.

## Kesimpulan 
Panduan ini menyediakan jalur komprehensif untuk **creating a search index .NET** solusi yang skalabel, mengindeks dengan cepat, dan melindungi data melalui redaction. Dengan mengkonfigurasi node, mengindeks dokumen, memanfaatkan fitur pencarian lanjutan, dan menerapkan redaction, pengembang dapat secara dramatis meningkatkan alur kerja manajemen dokumen sambil mempertahankan standar keamanan yang ketat.

## Pertanyaan yang Sering Diajukan

**Q: How do I set up a distributed search network in .NET with GroupDocs?**  
A: Tentukan jalur dasar dan port, lalu panggil `SearchNetworkDeployment.Deploy()` untuk meluncurkan node master dan worker di seluruh mesin.

**Q: Can I perform advanced searches with multiple parameters in GroupDocs?**  
A: Ya—gunakan `SearchOptions` untuk menggabungkan pencocokan fuzzy, dukungan wildcard, dan penyorotan hasil dalam satu kueri.

**Q: Is it possible to monitor network activity on the master node?**  
A: Tentu—langganan ke `SearchNetworkNodeEvents` seperti `IndexingCompleted` dan `QueryExecuted` untuk wawasan waktu nyata.

**Q: How do I apply redaction to PDF files using GroupDocs?**  
A: Inisialisasi `Redactor`, muat PDF, definisikan objek `RedactionPattern` (regex atau string literal), panggil `Apply`, dan simpan dokumen yang telah disanitasi.

**Q: What's the easiest way to improve search performance in a networked environment?**  
A: Indeks seluruh set dokumen Anda sepenuhnya sebelum kueri, sebarkan node untuk memanfaatkan pemrosesan paralel, dan sesuaikan `SearchOptions` untuk caching dan paging.

---

**Last Updated:** 2026-06-12  
**Tested With:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Author:** GroupDocs

## Tutorial Terkait

- [Master .NET Document Indexing with GroupDocs.Search&#58; Panduan Komprehensif](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Pengindeksan Dokumen Master dan Kuery Pencarian Lanjutan dengan GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Menguasai GroupDocs Search dan Redaction di .NET&#58; Manajemen Dokumen Lanjutan](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)