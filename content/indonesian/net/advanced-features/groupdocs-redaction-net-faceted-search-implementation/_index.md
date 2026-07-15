---
date: '2026-04-02'
description: Pelajari cara membuat indeks pencarian GroupDocs dan menambahkan dokumen
  ke indeks sambil menerapkan pencarian berfaset menggunakan GroupDocs.Search dan
  GroupDocs.Redaction di .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Buat Indeks Pencarian GroupDocs dengan Redaksi .NET dan Pencarian Berfasilitas
type: docs
url: /id/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Buat Indeks Pencarian GroupDocs dengan Redaction .NET Pencarian Berfaset

Pada aplikasi modern, **membuat indeks pencarian dengan GroupDocs** sangat penting untuk pengambilan dokumen yang cepat dan akurat. Baik Anda menangani kontrak hukum, katalog produk, atau basis pengetahuan yang besar, indeks yang dibangun dengan baik memungkinkan Anda **menambahkan dokumen ke indeks** dan menjalankan pencarian berfaset yang kuat dalam hitungan detik. Tutorial ini memandu Anda melalui seluruh proses—dari menyiapkan GroupDocs.Redaction hingga membuat kueri berfaset sederhana dan kompleks—sehingga Anda dapat memberikan pengalaman pencarian yang responsif dalam proyek .NET Anda.

## Jawaban Cepat
- **Apa tujuan utama?** Untuk membuat indeks pencarian dengan GroupDocs dan mengaktifkan pencarian berfaset.  
- **Perpustakaan apa yang diperlukan?** GroupDocs.Redaction dan GroupDocs.Search untuk .NET.  
- **Bagaimana cara menambahkan dokumen ke indeks?** Gunakan `index.Add(documentsFolder)` setelah menginisialisasi indeks.  
- **Bisakah saya menjalankan kueri kompleks?** Ya, gabungkan kueri objek dengan operator logika untuk penyaringan lanjutan.  
- **Apakah lisensi diperlukan?** Versi percobaan gratis berfungsi untuk pengembangan; lisensi komersial diperlukan untuk produksi.

## Apa itu pencarian berfaset dan mengapa menggunakannya dengan GroupDocs?
Pencarian berfaset memungkinkan pengguna mempersempit hasil dengan menerapkan beberapa filter—seperti kategori, tanggal, atau penulis—secara bersamaan. Ketika digabungkan dengan **GroupDocs.Redaction**, Anda mendapatkan konten yang aman dan dapat dicari yang menghormati aturan redaksi, menjadikannya ideal untuk lingkungan yang sangat mematuhi regulasi.

## Prasyarat

### Perpustakaan yang Diperlukan, Versi, dan Ketergantungan
- **GroupDocs.Redaction .NET** – rilis stabil terbaru.  
- **GroupDocs.Search .NET** – bekerja beriringan dengan Redaction untuk pengindeksan.

### Persyaratan Penyiapan Lingkungan
- **IDE**: Visual Studio 2019 atau lebih baru.  
- **Framework**: .NET Core 3.1, .NET 5, atau .NET 6.  
- **Kompatibilitas OS**: Windows, Linux, macOS.

### Prasyarat Pengetahuan
Keterampilan dasar C# dan pemahaman tingkat tinggi tentang konsep pencarian berfaset akan membantu, tetapi panduan langkah‑demi‑langkah ini ramah bagi pemula juga.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Informasi Instalasi
Anda dapat menambahkan paket GroupDocs.Redaction menggunakan salah satu metode berikut:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Cari "GroupDocs.Redaction" dan instal versi terbaru.

### Langkah-langkah Akuisisi Lisensi
Untuk membuka semua fitur, mulailah dengan percobaan gratis atau dapatkan lisensi permanen:

1. Kunjungi [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) untuk menjelajahi opsi lisensi.  
2. Ikuti petunjuk di layar untuk menerima file lisensi percobaan atau yang dibeli.

### Inisialisasi dan Penyiapan Dasar
Setelah paket diinstal, inisialisasi Redactor dalam aplikasi Anda:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Cara membuat indeks pencarian groupdocs

Di bawah ini kami membagi implementasi menjadi dua bagian: **Pencarian Berfaset Sederhana** dan **Kuery Kompleks**. Setiap bagian menunjukkan cara **membuat indeks pencarian groupdocs**, menambahkan dokumen, dan menjalankan kueri.

### Fitur 1: Pencarian Berfaset Sederhana

**Overview**  
Pencarian berfaset memungkinkan pengguna mempersempit hasil dengan memilih beberapa kriteria. Bagian ini mendemonstrasikan pendekatan langsung menggunakan GroupDocs.Search.

#### Langkah 1: Tentukan Folder Indeks dan Dokumen
Siapkan jalur folder tempat indeks akan disimpan dan tempat dokumen sumber Anda berada.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Langkah 2: Buat Indeks
Inisialisasi indeks pencarian di folder yang telah Anda tentukan.

```csharp
Index index = new Index(indexFolder);
```

#### Langkah 3: Tambahkan Dokumen ke Indeks
Muat dokumen Anda sehingga menjadi dapat dicari.

```csharp
index.Add(documentsFolder);
```

#### Langkah 4: Lakukan Pencarian Kuery Teks
Jalankan kueri teks dasar terhadap bidang **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Langkah 5: Jalankan Pencarian Kuery Objek
Gunakan kueri berorientasi objek untuk kontrol yang lebih halus.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Fitur 2: Kuery Kompleks

**Overview**  
Ketika Anda perlu menggabungkan beberapa filter—seperti pola nama file dan pencocokan frasa—Anda dapat membangun kueri kompleks menggunakan operator logika.

#### Langkah 1: Tentukan Folder Indeks dan Dokumen
Gunakan kembali struktur folder yang sama untuk skenario yang lebih maju.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Langkah 2: Buat Indeks dan Tambahkan Dokumen
(Lihat langkah 2‑3 dari contoh sederhana; tetap sama.)

#### Langkah 3: Jalankan Pencarian Kuery Teks
Jalankan kueri teks gabungan yang mencampur kriteria nama file dan konten.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Langkah 4: Bangun dan Jalankan Kuery Objek
Bangun logika yang sama secara programatis.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Lanjutkan menggabungkan frasa, rentang, dan operator boolean untuk mencocokkan aturan bisnis Anda secara tepat.

## Aplikasi Praktis

1. **Platform E‑Commerce** – Filter produk berdasarkan kategori, harga, dan rating.  
2. **Sistem Manajemen Dokumen** – Temukan kontrak berdasarkan penulis, tanggal, atau tingkat kerahasiaan.  
3. **Portal Konten** – Biarkan pembaca menelusuri lebih dalam berdasarkan tag, topik, dan tanggal publikasi.

## Pertimbangan Kinerja

- **Penyegaran Indeks**: Secara rutin indeks ulang file baru atau yang diperbarui untuk menjaga pencarian tetap cepat.  
- **Manajemen Memori**: Buang objek `Index` setelah selesai, terutama untuk kumpulan data besar.  
- **Pengindeksan Asinkron**: Gunakan `Task.Run` atau layanan latar belakang untuk menghindari pembekuan UI selama pengindeksan berat.

## Masalah Umum dan Solusi

| Masalah | Solusi |
|-------|----------|
| **Indeks tidak ditemukan** | Verifikasi jalur `indexFolder` dan pastikan folder memiliki izin menulis. |
| **Tidak ada hasil yang dikembalikan** | Periksa bahwa bidang yang Anda kueri (mis., `Content`, `Filename`) telah diindeks. |
| **Kesalahan out‑of‑memory** | Proses dokumen secara batch dan pertimbangkan meningkatkan ukuran heap .NET GC. |

## Pertanyaan yang Sering Diajukan

**Q: Apa itu pencarian berfaset?**  
A: Pencarian berfaset memungkinkan pengguna memperhalus hasil menggunakan beberapa filter independen seperti kategori, tanggal, atau penulis.

**Q: Bagaimana cara menangani dataset besar dengan GroupDocs.Search?**  
A: Gunakan pengindeksan inkremental, pemrosesan batch, dan operasi asinkron untuk menjaga penggunaan memori rendah dan kinerja tinggi.

**Q: Bisakah saya mengintegrasikan fungsionalitas GroupDocs ke dalam aplikasi .NET yang ada?**  
A: Ya, perpustakaan dirancang untuk integrasi mulus dengan proyek .NET apa pun.

**Q: Apa saja masalah umum dengan pencarian berfaset?**  
A: Sintaks kueri kompleks dan memastikan semua bidang relevan diindeks merupakan tantangan umum; pengujian yang tepat dan pemeliharaan indeks dapat menguranginya.

**Q: Bagaimana cara memperoleh lisensi sementara untuk GroupDocs?**  
A: Kunjungi [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) untuk mengajukan lisensi percobaan yang membuka semua fungsi selama evaluasi.

## Sumber Daya
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Last Updated:** 2026-04-02  
**Tested With:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Author:** GroupDocs