---
date: '2026-08-15'
description: Pelajari cara mengatur lisensi dan menggunakan GroupDocs.Redaction untuk
  mencari serta menyorot konten HTML dalam aplikasi .NET.
keywords:
- how to set license
- search and highlight html
- GroupDocs.Redaction .NET
lastmod: '2026-08-15'
og_description: Temukan cara mengatur lisensi untuk GroupDocs.Redaction dan melakukan
  pencarian serta menyorot hasil HTML di .NET. Panduan lengkap dengan contoh praktis.
og_image_alt: Guide showing license setup and HTML search highlighting using GroupDocs.Redaction
  in .NET
og_title: Cara mengatur lisensi, menyorot pencarian dengan GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  headline: How to set license, highlight search with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  name: How to set license, highlight search with GroupDocs.Redaction
  steps:
  - name: '**Legal document analysis**: Quickly find and highlight key legal terms.'
    text: '**Legal document analysis**: Quickly find and highlight key legal terms.'
  - name: '**Customer support**: Highlight relevant customer feedback in support tickets.'
    text: '**Customer support**: Highlight relevant customer feedback in support tickets.'
  - name: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
    text: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
  - name: '**Financial reports**: Identify and highlight critical financial metrics.'
    text: '**Financial reports**: Identify and highlight critical financial metrics.'
  - name: '**Content management**: Improve content discoverability through keyword
      highlighting.'
    text: '**Content management**: Improve content discoverability through keyword
      highlighting.'
  type: HowTo
- questions:
  - answer: Visit [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)
      for more details.
    question: How do I obtain a GroupDocs license?
  - answer: Yes, after acquiring the appropriate license.
    question: Can I use GroupDocs in a commercial project?
  - answer: Use consistent directory structures and environment variables for flexibility.
    question: What is the best practice for managing document paths?
  - answer: Regularly update your index and optimize query parameters.
    question: How can I improve search performance?
  - answer: Yes, multiple language dictionaries are supported.
    question: Is there support for languages other than English in GroupDocs?
  type: FAQPage
tags:
- license setup
- HTML search highlighting
- GroupDocs.Redaction
- .NET document management
title: Cara mengatur lisensi, menyorot pencarian dengan GroupDocs.Redaction
type: docs
url: /id/net/document-management/mastering-document-management-groupdocs-redaction-net/
weight: 1
---

# Menguasai manajemen dokumen dengan GroupDocs.Redaction di .NET

## Pendahuluan

Di era digital saat ini, manajemen dokumen yang efisien sangat penting untuk menjaga privasi data dan meningkatkan fungsionalitas pencarian. Baik Anda seorang pengembang maupun bisnis yang ingin meningkatkan kemampuan pemrosesan dokumen, mengintegrasikan pustaka kuat seperti Aspose dan GroupDocs dapat menjadi transformasional. Tutorial ini akan memandu Anda dalam menyiapkan lisensi untuk pustaka-pustaka tersebut dan menyorot hasil pencarian dalam format HTML menggunakan pustaka GroupDocs.Redaction .NET.

**Apa yang Akan Anda Pelajari:**

- Cara mengatur lisensi untuk pustaka Aspose dan GroupDocs
- Menyiapkan jalur dan melakukan pencarian dengan GroupDocs.Search
- Menyorot istilah pencarian dalam dokumen HTML menggunakan GroupDocs.Viewer
- Menerapkan fitur-fitur ini ke dalam aplikasi .NET yang fungsional

Dengan contoh praktis dan instruksi langkah demi langkah, Anda akan siap untuk menyederhanakan proses manajemen dokumen Anda.

## Jawaban Cepat
- **Bagaimana cara mengatur lisensi untuk GroupDocs.Redaction?** Gunakan kelas `License` untuk memuat file `.lic` Anda sebelum panggilan API apa pun.
- **Apakah saya dapat mencari dan menyorot konten HTML?** Ya, gabungkan GroupDocs.Search dengan GroupDocs.Viewer untuk menemukan istilah dan menghasilkan HTML yang disorot.
- **Apakah saya juga memerlukan lisensi Aspose?** Hanya jika Anda menggunakan Aspose.HTML untuk rendering tambahan; jika tidak, GroupDocs.Redaction sudah cukup.
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Apakah lisensi percobaan cukup untuk pengujian?** Lisensi sementara memungkinkan Anda mengevaluasi semua fitur tanpa batasan waktu.

## Cara mengatur lisensi untuk GroupDocs.Redaction?

Kelas `License` mendaftarkan file lisensi dengan SDK GroupDocs. Muat file lisensi Anda dengan kelas `License` dan panggil `SetLicense` sebelum panggilan SDK lainnya. Ini membuka semua fitur, menghapus watermark evaluasi, dan mengaktifkan optimasi kinerja. Dengan memuat lisensi lebih awal, SDK dapat menerapkan pemeriksaan hak untuk setiap operasi berikutnya, memastikan semua fitur redaksi, pencarian, dan rendering berfungsi tanpa batasan.

```text
```bash
dotnet add package GroupDocs.Redaction
```
```

## Cara mengatur lisensi untuk Aspose.HTML?

Kelas `License` dalam Aspose.HTML mendaftarkan lisensi produk dan menonaktifkan batasan percobaan. Buat instance objek `License` Aspose dan arahkan ke file `.lic`. Ini memastikan semua fungsi rendering Aspose.HTML berjalan tanpa peringatan percobaan dan opsi rendering premium seperti dukungan CSS serta mesin tata letak lanjutan tersedia.

```text
```csharp
using Aspose.Html;

string licensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";
new License().SetLicense(licensePath);
```
```

- **Penjelasan**: `License.SetLicense` memuat file lisensi, membuka semua fitur.

## Cara mengatur lisensi untuk GroupDocs.Viewer?

Kelas `License` untuk GroupDocs.Viewer mendaftarkan lisensi viewer, memungkinkan rendering berkualitas tinggi dari PDF, DOCX, dan format lain ke HTML tanpa watermark. Buat instance `License` untuk GroupDocs.Viewer dan panggil `SetLicense`. Langkah ini diperlukan jika Anda ingin merender dokumen ke HTML dengan fidelitas penuh.

```text
```csharp
using GroupDocs.Viewer;

new License().SetLicense(licensePath);
```
```

## Mengapa menggunakan pencarian dan menyorot html dengan GroupDocs?

GroupDocs.Search mengindeks dokumen dalam struktur ringan, hanya-baca yang dapat mengkueri jutaan catatan dalam milidetik. Digabungkan dengan GroupDocs.Viewer, Anda dapat merender dokumen yang didukung menjadi HTML dan menambahkan sorotan pada istilah yang cocok dengan gaya CSS. Klaim terukur: mesin pencari dapat memproses PDF 500 halaman dalam kurang dari 2 detik pada server 2 GHz standar, dan viewer merender file yang sama ke HTML dalam kurang dari 1 detik.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Instalasi

Untuk mulai menggunakan GroupDocs.Redaction dalam proyek Anda, Anda dapat menginstalnya melalui berbagai pengelola paket:

**.NET CLI:**
```text
```powershell
Install-Package GroupDocs.Redaction
```
```

**Package Manager Console:**
```text
```csharp
// Set your license path
string redactionLicensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";

// Initialize the Redaction API with the license
new GroupDocs.Redaction.License().SetLicense(redactionLicensePath);
```
```

**NuGet Package Manager UI:**  
Cari "GroupDocs.Redaction" dan instal versi terbaru.

### Akuisisi Lisensi

Sebelum menggunakan kemampuan penuh GroupDocs.Redaction, dapatkan lisensi. Anda dapat memilih:

- **Uji coba gratis**: Unduh lisensi percobaan untuk menguji fitur.  
- **Lisensi sementara**: Dapatkan melalui [Lisensi Sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
- **Pembelian**: Beli lisensi permanen jika Anda berencana menggunakannya dalam produksi.

Untuk syarat lisensi detail, lihat [Dokumentasi GroupDocs](https://docs.groupdocs.com/search/net/).

### Inisialisasi dan Penyiapan Dasar

```text
```csharp
string basePath = @"./HighlightInHtml/HighlightExample";
string viewerCacheFolderPath = basePath + @"/ViewerCache";
string indexFolder = basePath + @"/Index";
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
string query = "\"dapibus diam\" OR lorem";
```
```

## Panduan Implementasi

### Menetapkan lisensi untuk pustaka Aspose dan GroupDocs

#### Gambaran Umum

Menetapkan lisensi memastikan Anda dapat memanfaatkan semua fitur Aspose.HTML dan GroupDocs.Viewer tanpa batasan.

#### Langkah-langkah

**1. Atur lisensi untuk Aspose.HTML**

```text
```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder); // Initialize index at specified path
index.Add(documentsFolder); // Add documents from directory to index
```
```

**2. Atur lisensi untuk GroupDocs.Viewer**

```text
```csharp
using GroupDocs.Search.Results;

SearchResult result = index.Search(query); // Execute the search
FoundDocument foundDocument = result.GetFoundDocument(0); // Retrieve first document
```
```

### Menyiapkan jalur dan kueri

#### Gambaran Umum

Tentukan jalur untuk dokumen Anda dan siapkan kueri pencarian untuk menemukan konten tertentu.

#### Langkah-langkah

**1. Tentukan jalur dasar**

```text
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Viewer.Options;

IndexedFileInfo fileInfo = new IndexedFileInfo(viewerCacheFolderPath, foundDocument.DocumentInfo.FilePath);
HighlightService highlightService = new HighlightService(fileInfo, null); // Prepare for highlighting

highlightService.Highlight(foundDocument, index.Dictionaries.Alphabet); // Perform highlighting
```
```

- **Penjelasan**: Mengatur jalur memastikan integrasi pencarian dan sorotan berjalan lancar.

### Membuat dan menambahkan ke indeks

#### Gambaran Umum

Buat indeks untuk memfasilitasi pencarian dokumen yang efisien.

**Langkah-langkah**

**1. Buat indeks**

```text
CODE_BLOCK_PLACEHOLDER_9_END
```

- **Penjelasan**: Objek `Index` mengelola data terindeks Anda, memungkinkan pengambilan cepat.

### Mencari dalam indeks

#### Gambaran Umum

Jalankan kueri pencarian pada indeks yang dibuat dan ambil hasilnya.

**Langkah-langkah**

**1. Lakukan pencarian**

```text
CODE_BLOCK_PLACEHOLDER_10_END
```

- **Penjelasan**: `index.Search` mengeksekusi kueri Anda, mengembalikan dokumen yang cocok.

### Menyorot hasil pencarian dalam HTML

#### Gambaran Umum

Gunakan GroupDocs.Viewer untuk menyorot istilah dalam representasi HTML sebuah dokumen.

**Langkah-langkah**

**1. Inisialisasi layanan sorotan**

```text
CODE_BLOCK_PLACEHOLDER_11_END
```

- **Penjelasan**: `HighlightService` memproses dan menyorot istilah pencarian dalam dokumen.

## Aplikasi Praktis

1. **Analisis dokumen hukum**: Temukan dan sorot istilah hukum utama dengan cepat.  
2. **Dukungan pelanggan**: Sorot umpan balik pelanggan yang relevan dalam tiket dukungan.  
3. **Makalah penelitian**: Mempermudah riset dengan menyorot istilah ilmiah tertentu.  
4. **Laporan keuangan**: Identifikasi dan sorot metrik keuangan penting.  
5. **Manajemen konten**: Tingkatkan penemuan konten melalui sorotan kata kunci.

## Pertimbangan Kinerja

- **Optimalkan pengindeksan**: Perbarui indeks Anda secara teratur untuk pencarian yang efisien.  
- **Manajemen memori**: Gunakan pemrosesan asynchronous bila memungkinkan untuk mengelola penggunaan memori.  
- **Penggunaan sumber daya**: Pantau kinerja aplikasi untuk menyesuaikan alokasi sumber daya.

## Masalah umum dan pemecahan masalah

- **Lisensi tidak dikenali** – Verifikasi bahwa jalur file `.lic` bersifat absolut atau relatif dengan benar terhadap assembly yang dijalankan.  
- **Pencarian tidak menghasilkan hasil** – Pastikan indeks dibangun kembali setelah menambahkan dokumen baru; indeks tidak secara otomatis mendeteksi perubahan file.  
- **Sorotan HTML tidak ada CSS** – Sertakan stylesheet default yang disediakan oleh GroupDocs.Viewer atau tambahkan CSS khusus untuk menata tag `<mark>`.  
- **PDF besar menyebabkan timeout** – Tingkatkan pengaturan `SearchOptions.MaxDegreeOfParallelism` untuk memanfaatkan prosesor multi‑core.

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara mendapatkan lisensi GroupDocs?**  
J: Kunjungi [Lisensi Sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/) untuk detail lebih lanjut.

**T: Bisakah saya menggunakan GroupDocs dalam proyek komersial?**  
J: Ya, setelah memperoleh lisensi yang sesuai.

**T: Apa praktik terbaik untuk mengelola jalur dokumen?**  
J: Gunakan struktur direktori yang konsisten dan variabel lingkungan untuk fleksibilitas.

**T: Bagaimana saya dapat meningkatkan kinerja pencarian?**  
J: Perbarui indeks secara teratur dan optimalkan parameter kueri.

**T: Apakah ada dukungan untuk bahasa selain Inggris di GroupDocs?**  
J: Ya, beberapa kamus bahasa didukung.

## Sumber Daya

- [Dokumentasi GroupDocs](https://docs.groupdocs.com/search/net/)
- [Dokumentasi GroupDocs](https://docs.groupdocs.com/search/net/)
- [Referensi API](https://reference.groupdocs.com/redaction/net)
- [Unduh GroupDocs Redaction](https://releases.groupdocs.com/search/net/)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Kesimpulan

Anda telah mempelajari cara mengatur lisensi, mengonfigurasi jalur pencarian, membuat indeks, melakukan pencarian, dan menyorot hasil menggunakan GroupDocs.Redaction di .NET. Saat Anda mengintegrasikan fitur-fitur ini ke dalam aplikasi, pertimbangkan untuk menjelajahi dokumentasi lebih lanjut untuk kemampuan lanjutan.

**Langkah selanjutnya:**

- Jelajahi [Dokumentasi GroupDocs](https://docs.groupdocs.com/search/net/) untuk mempelajari lebih dalam.  
- Bereksperimen dengan fitur tambahan seperti redaksi dan anotasi.

---

**Last Updated:** 2026-08-15  
**Tested With:** GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs

## Tutorial Terkait

- [Menguasai GroupDocs.Redaction .NET: Pembuatan Indeks Efisien dan Manajemen Alias untuk Pencarian Dokumen Lanjutan](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implementasi GroupDocs.Redaction .NET untuk Manajemen Penemu Dokumen dan Penyorotan](/search/net/document-management/groupdocs-redaction-net-finder-management-guide/)
- [Menguasai GroupDocs.Redaction .NET: Penyiapan & Penanganan Event untuk Manajemen Dokumen Aman](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}