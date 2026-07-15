---
date: '2026-04-05'
description: Pelajari cara membuat kamus kata sandi .NET menggunakan GroupDocs.Redaction
  dan juga menghapus kata sandi dari kamus untuk penanganan dokumen yang aman.
keywords:
- create password dictionary .net
- remove password from dictionary
- GroupDocs Redaction password management
title: Buat Kamus Kata Sandi .NET dengan GroupDocs Redaction
type: docs
url: /id/net/advanced-features/master-document-password-management-net-groupdocs/
weight: 1
---

# Buat Kamus Kata Sandi .NET dengan GroupDocs Redaction

Di dunia digital saat ini, melindungi dokumen sensitif sangat penting, dan **Anda akan belajar cara membuat kamus kata sandi .NET** menggunakan GroupDocs.Redaction. Baik Anda seorang profesional bisnis yang melindungi laporan perusahaan maupun individu yang melindungi file pribadi, kamus kata sandi yang kuat memungkinkan Anda mengontrol akses dan menyederhanakan pengindeksan yang aman.

**Apa yang Akan Anda Pelajari**
- Cara **membuat kamus kata sandi .NET** dengan GroupDocs
- Teknik untuk **menghapus kata sandi dari kamus** ketika tidak lagi diperlukan
- Langkah-langkah untuk mengindeks dokumen secara aman dengan kata sandi yang disematkan
- Cara mencari file yang dilindungi kata sandi secara efisien

## Jawaban Cepat
- **Apa itu kamus kata sandi?** Sebuah penyimpanan kunci‑nilai yang memetakan jalur file ke kata sandi mereka.  
- **Mengapa menggunakan GroupDocs.Redaction?** Ia mengintegrasikan redaksi dan manajemen kata sandi dalam satu API.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan dapat digunakan untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya mengindeks folder besar?** Ya – pastikan Anda mengelola ukuran kamus.  
- **Apakah .NET Core didukung?** Tentu saja, GroupDocs.Redaction bekerja dengan .NET Core dan versi selanjutnya.

## Apa itu kamus kata sandi di GroupDocs?
Kamus kata sandi adalah kumpulan sederhana dalam memori atau di disk yang menghubungkan lokasi setiap dokumen dengan kata sandi pembukanya. GroupDocs.Search membaca kamus ini selama proses pengindeksan, memungkinkan ia membuka file terenkripsi secara otomatis.

## Mengapa membuat kamus kata sandi .NET?
Membuat kamus kata sandi memusatkan manajemen kredensial, mengurangi kode yang berulang, dan memungkinkan operasi massal seperti pencarian di banyak file yang dilindungi tanpa harus menentukan kata sandi secara manual setiap kali.

## Prasyarat
- **Pustaka**: paket NuGet `GroupDocs.Search` dan `GroupDocs.Redaction`.  
- **Lingkungan**: .NET Core 3.1+ (atau .NET 6/7).  
- **Pengetahuan**: Konsep dasar C# dan I/O file.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Instal paket
**Menggunakan .NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Konsol Pengelola Paket (Visual Studio)**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Cari "GroupDocs.Redaction" dan instal versi terbaru.

### Akuisisi Lisensi
- **Percobaan Gratis:** Mulai dengan lisensi percobaan sementara untuk menjelajahi fitur.  
- **Pembelian:** Untuk penggunaan berkelanjutan setelah percobaan, pertimbangkan membeli lisensi penuh. Instruksi detail dapat ditemukan di [halaman pembelian](https://purchase.groupdocs.com/temporary-license/).

### Inisialisasi dan Penyiapan
```csharp
using GroupDocs.Redaction;

// Basic initialization of the Redactor
RedactorSettings settings = new RedactorSettings();
var redactor = new Redactor("path/to/document.pdf", settings);
```

Sekarang lingkungan siap, mari kita selami implementasi inti.

## Cara membuat kamus kata sandi .NET

### Langkah 1: Inisialisasi Indeks
```csharp
using GroupDocs.Search;
using System.IO;

string indexFolder = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Index");
Index index = new Index(indexFolder);
```
*Penjelasan:* Kami membuat objek `Index` yang akan menyimpan kamus kata sandi kami dan metadata pencarian lainnya.

### Langkah 2: Hapus Kata Sandi yang Ada (Jika Ada)
```csharp
if (index.Dictionaries.DocumentPasswords.Count > 0)
{
    index.Dictionaries.DocumentPasswords.Clear();
}
```
*Penjelasan:* Menghapus entri usang menjamin awal yang bersih, mencegah penggunaan kata sandi lama secara tidak sengaja.

### Langkah 3: Tambahkan Kata Sandi ke Kamus
```csharp
string key1 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "English.docx"));
index.Dictionaries.DocumentPasswords.Add(key1, "123456");
```
*Penjelasan:* Ini memetakan jalur dokumen (`key1`) ke kata sandinya (`"123456"`). Ulangi langkah ini untuk setiap file yang dilindungi.

### Langkah 4: Ambil dan Hapus Kata Sandi
```csharp
if (index.Dictionaries.DocumentPasswords.Contains(key1))
{
    string password = index.Dictionaries.DocumentPasswords.GetPassword(key1);
    index.Dictionaries.DocumentPasswords.Remove(key1);
}
```
*Penjelasan:* Anda dapat mengambil kata sandi yang disimpan saat diperlukan dan **menghapus kata sandi dari kamus** setelah dokumen tidak lagi perlu diakses.

## Cara menambahkan banyak kata sandi ke kamus
```csharp
string key2 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "English.docx"));
index.Dictionaries.DocumentPasswords.Add(key2, "123456");
string key3 = Path.GetFullPath(Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Lorem ipsum.docx"));
index.Dictionaries.DocumentPasswords.Add(key3, "123456");
```
*Penjelasan:* Menambahkan beberapa entri sekaligus memungkinkan Anda mengelola akses massal untuk banyak file.

## Cara mengindeks dokumen dengan kata sandi
```csharp
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
index.Add(documentsFolder);
```
*Penjelasan:* Metode `Add` membaca setiap file, secara otomatis menerapkan kata sandi dari kamus, dan membangun indeks yang dapat dicari.

## Cara mencari dalam dokumen yang diindeks dan dilindungi kata sandi
```csharp
string query = "ipsum OR increasing";
SearchResult result = index.Search(query);
```
*Penjelasan:* Setelah pengindeksan, Anda dapat menjalankan kueri pencarian biasa di semua dokumen, terlepas dari status enkripsinya.

## Masalah Umum dan Solusinya
- **Kata sandi tidak diterapkan** – Pastikan jalur file yang digunakan sebagai kunci kamus cocok persis dengan lokasi file sebenarnya (gunakan `Path.GetFullPath`).  
- **Kamus besar memengaruhi kinerja** – Secara berkala hapus entri yang tidak terpakai dan pertimbangkan menyimpan kamus ke basis data ringan jika ukurannya sangat besar.  
- **Kesalahan lisensi** – Pastikan file lisensi percobaan atau penuh Anda direferensikan dengan benar pada startup aplikasi.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan GroupDocs.Redaction secara gratis?**  
A: Anda dapat memulai dengan lisensi percobaan sementara. Untuk penggunaan yang lebih lama, pembelian lisensi penuh diperlukan.

**Q: Bagaimana cara menangani kumpulan dokumen besar secara efisien?**  
A: Gunakan praktik pengindeksan dan manajemen memori yang efisien untuk menangani dataset yang lebih besar secara efektif.

**Q: Apakah GroupDocs.Redaction kompatibel dengan semua versi .NET?**  
A: Ya, ia mendukung versi .NET Core terbaru. Selalu periksa pembaruan kompatibilitas.

**Q: Bisakah saya mencari dalam dokumen yang dilindungi kata sandi secara mulus?**  
A: Ya, setelah diindeks dengan kata sandi, Anda dapat melakukan pencarian menggunakan GroupDocs.Search tanpa masalah.

**Q: Apa saja tips pemecahan masalah umum saat menyiapkan GroupDocs.Redaction?**  
A: Pastikan lisensi Anda aktif dan jalur ke direktori dokumen ditentukan dengan benar. Lihat [forum dukungan](https://forum.groupdocs.com/) untuk bantuan lebih lanjut.

## Kesimpulan
Dengan mengikuti langkah-langkah di atas, Anda kini tahu cara **membuat kamus kata sandi .NET** dan juga **menghapus kata sandi dari kamus** bila diperlukan. Pendekatan ini memusatkan penanganan kredensial, meningkatkan keamanan, dan memungkinkan pencarian kuat di seluruh file terenkripsi. Jelajahi integrasi lebih lanjut dengan penyimpanan cloud atau sistem manajemen dokumen untuk memperluas solusi Anda.

---

**Terakhir Diperbarui:** 2026-04-05  
**Diuji Dengan:** GroupDocs.Redaction 23.2 for .NET  
**Penulis:** GroupDocs