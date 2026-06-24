---
date: '2026-04-27'
description: Pelajari cara menyensor data sensitif di .NET menggunakan GroupDocs.Search
  dan Redaction, serta temukan cara menambahkan dokumen ke indeks untuk mencari dokumen
  berukuran besar.
keywords:
- redact sensitive data
- add documents to index
- search large documents
title: GroupDocs.Search & Redaction di .NET – menyensor data sensitif
type: docs
url: /id/net/document-management/groupdocs-search-redaction-net-guide/
weight: 1
---

# GroupDocs.Search & Redaction di .NET – menghapus data sensitif

Mengelola sejumlah besar dokumen dapat menjadi menakutkan, terutama ketika Anda perlu **menghapus data sensitif** sambil tetap menyediakan kemampuan pencarian cepat. Dalam panduan ini kami akan menjelaskan cara menyiapkan GroupDocs.Search bersama dengan GroupDocs.Redaction, menunjukkan cara **menambahkan dokumen ke indeks**, melakukan operasi **pencarian dokumen besar** secara efisien, dan memastikan semuanya mematuhi persyaratan privasi.

## Jawaban Cepat
- **Apa arti “redact sensitive data”?** Itu berarti menghapus secara permanen atau menyamarkan informasi rahasia dari dokumen.
- **Perpustakaan apa yang saya perlukan?** GroupDocs.Search dan GroupDocs.Redaction untuk .NET (tersedia melalui NuGet).
- **Bisakah saya mengindeks proyek .NET secara otomatis?** Ya – lihat bagian “How to index .NET” untuk panduan langkah demi langkah.
- **Bagaimana saya menangani file besar?** Gunakan pencarian berbasis chunk untuk memproses data dalam bagian yang dapat dikelola.
- **Apakah lisensi diperlukan untuk produksi?** Lisensi GroupDocs yang valid diperlukan untuk penggunaan produksi; percobaan gratis tersedia.

## Apa itu menghapus data sensitif?
Menghapus data sensitif adalah proses menghapus secara permanen atau menyamarkan informasi pribadi, keuangan, atau rahasia dari sebuah dokumen sehingga tidak dapat dipulihkan atau dilihat oleh pengguna yang tidak berwenang.

## Mengapa menggabungkan GroupDocs.Search dengan Redaction?
- **Kecepatan:** Membuat indeks yang dapat dicari yang mengembalikan hasil dalam milidetik.  
- **Keamanan:** Terapkan aturan redaksi sebelum dokumen dibagikan atau disimpan.  
- **Skalabilitas:** Pencarian chunk memungkinkan Anda bekerja dengan terabyte teks tanpa menghabiskan memori.  
- **Kepatuhan:** Memenuhi GDPR, HIPAA, dan regulasi lainnya dengan memastikan data rahasia tidak pernah bocor.

## Prasyarat
- Lingkungan pengembangan .NET (Visual Studio disarankan).  
- Pengetahuan dasar C#.  
- Akses ke NuGet untuk menginstal paket yang diperlukan.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Instalasi via .NET CLI
```bash
dotnet add package GroupDocs.Redaction
```

### Instalasi Package Manager
```powershell
Install-Package GroupDocs.Redaction
```

### UI NuGet Package Manager
Cari **"GroupDocs.Redaction"** dan instal versi terbaru.

### Langkah-langkah Akuisisi Lisensi
- **Percobaan Gratis:** Mulai dengan percobaan gratis untuk menjelajahi fitur.  
- **Lisensi Sementara:** Minta lisensi sementara untuk akses yang lebih lama.  
- **Pembelian:** Pertimbangkan membeli untuk penggunaan produksi jangka panjang.

### Inisialisasi dan Penyiapan Dasar
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## Panduan Implementasi

### Cara mengindeks proyek .NET dengan GroupDocs.Search
Di bawah ini kami membagi implementasi menjadi langkah‑langkah berurutan yang jelas sehingga Anda dapat mengikutinya dengan mudah.

#### Langkah 1: Tentukan Folder Indeks
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*Mengapa?* Menentukan folder khusus menjaga indeks Anda tetap terorganisir dan terpisah dari dokumen mentah.

#### Langkah 2: Buat dan Konfigurasikan Indeks
```csharp
Index index = new Index(indexFolder);
```
*Tujuan:* Membuat indeks yang dapat dicari baru di lokasi yang Anda tentukan.

#### Langkah 3: **Tambahkan dokumen ke indeks**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*Penjelasan:* Setiap pemanggilan menambahkan file (atau folder) ke indeks, membuat isinya dapat dicari.

### Cari dokumen besar dengan Chunk Search
Chunk search memungkinkan Anda memecah file besar menjadi potongan‑potongan lebih kecil, menjaga penggunaan memori tetap rendah.

#### Langkah 1: Tentukan Kuery Pencarian
```csharp
string query = "invitation";
```
*Tujuan:* Istilah yang Anda cari di semua file yang diindeks.

#### Langkah 2: Konfigurasikan Opsi Chunk Search
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*Penjelasan:* Mengaktifkan `IsChunkSearch` memberi tahu mesin untuk memproses data dalam chunk.

#### Langkah 3: Jalankan Pencarian Awal
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*Hasil:* Menunjukkan berapa banyak dokumen yang mengandung istilah tersebut dan berapa total kemunculan yang ditemukan.

#### Langkah 4: Lanjutkan dengan Chunk Berikutnya
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*Mengapa loop ini?* Ini memastikan Anda mengambil hasil dari setiap chunk hingga seluruh dataset diproses.

### Cara menghapus data sensitif dengan GroupDocs.Redaction
Setelah Anda menemukan informasi yang perlu dilindungi, terapkan aturan redaksi.

#### Langkah 1: Inisialisasi Pengaturan Redaksi
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### Langkah 2: Terapkan Redaksi
Gunakan kelas `Redactor` (tidak ditampilkan di sini untuk menjaga kode asli tetap utuh) untuk mendefinisikan pola, teks, atau gambar yang ingin Anda sembunyikan.  
*Tip profesional:* Uji aturan redaksi Anda pada salinan dokumen terlebih dahulu untuk menghindari kehilangan data secara tidak sengaja.

## Aplikasi Praktis
Kemampuan ini bersinar di banyak industri:

1. **Manajemen Dokumen Hukum** – Cari berkas kasus dengan cepat sambil menghapus detail rahasia klien.  
2. **Penanganan Data Kesehatan** – Lindungi PHI pasien sambil memungkinkan klinisi menemukan catatan yang relevan.  
3. **Audit Keuangan** – Indeks log transaksi besar dan hapus nomor akun atau pengidentifikasi pribadi.

## Pertimbangan Kinerja
- **Optimalkan Pengindeksan:** Lakukan re‑indeks hanya pada file yang berubah untuk menjaga indeks tetap segar tanpa pekerjaan yang tidak perlu.  
- **Kelola Sumber Daya:** Sesuaikan ukuran chunk (`options.ChunkSize`) berdasarkan RAM server Anda.  
- **Operasi Async:** Untuk batch besar, gunakan pengindeksan asynchronous untuk menjaga UI tetap responsif.

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana saya menangani file besar secara efisien?**  
A: Gunakan pencarian berbasis chunk (`IsChunkSearch = true`) untuk memproses data dalam potongan lebih kecil, mengurangi tekanan memori.

**Q: Bisakah GroupDocs.Redaction bekerja dengan dokumen terenkripsi?**  
A: Ya – dekripsi file terlebih dahulu, terapkan redaksi, lalu enkripsi kembali jika diperlukan.

**Q: Opsi lisensi apa yang tersedia?**  
A: Percobaan gratis, lisensi sementara untuk evaluasi, dan lisensi komersial penuh untuk produksi.

**Q: Bagaimana saya dapat memecahkan masalah kesalahan indeks?**  
A: Verifikasi bahwa path folder indeks benar, pastikan aplikasi memiliki izin baca/tulis, dan periksa bahwa semua format dokumen didukung.

**Q: Apakah memungkinkan untuk menyesuaikan kueri pencarian lebih lanjut?**  
A: Tentu saja. Anda dapat menggabungkan operator Boolean, wildcard, dan pencarian proksimitas menggunakan API `SearchOptions`.

## Sumber Daya
- **Dokumentasi:** [GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **Referensi API:** [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)  
- **Unduh:** [Latest Releases](https://releases.groupdocs.com/search/net/)  
- **Dukungan Gratis:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Lisensi Sementara:** [Request Here](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-04-27  
**Diuji Dengan:** GroupDocs.Search 23.9 dan GroupDocs.Redaction 23.9 untuk .NET  
**Penulis:** GroupDocs