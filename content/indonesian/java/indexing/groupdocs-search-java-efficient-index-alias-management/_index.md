---
date: '2026-03-06'
description: Pelajari cara menambahkan beberapa alias, menambahkan dokumen ke indeks,
  dan mengelola indeks yang dapat dicari secara efisien dengan GroupDocs.Search untuk
  Java.
keywords:
- GroupDocs.Search Java
- index management
- alias dictionary
title: Cara Menambahkan Beberapa Alias dan Menambahkan Dokumen ke Indeks di GroupDocs.Search
  untuk Java
type: docs
url: /id/java/indexing/groupdocs-search-java-efficient-index-alias-management/
weight: 1
---

# Tambahkan Banyak Alias dan Tambahkan Dokumen ke Indeks di GroupDocs.Search Java: Panduan Komprehensif

Di dunia yang didorong oleh data saat ini, kemampuan untuk **menambahkan banyak alias** sambil **menambahkan dokumen ke indeks** memberi solusi pencarian Anda keunggulan kinerja yang jelas. Baik Anda mengindeks ribuan kontrak, katalog produk, atau makalah penelitian, GroupDocs.Search untuk Java memungkinkan Anda **membuat indeks yang dapat dicari** dan menyesuaikan kueri dengan kamus alias—semua sambil menjaga implementasi tetap sederhana dan cepat.

## Jawaban Cepat
- **Apa langkah pertama untuk mulai menggunakan GroupDocs.Search?** Tambahkan dependensi Maven dan inisialisasi objek `Index`.  
- **Bagaimana cara menambahkan dokumen ke indeks?** Panggil `index.add("<folder_path>")` dengan folder yang berisi file Anda.  
- **Apakah saya dapat membuat alias untuk kueri kompleks?** Ya—gunakan kamus alias untuk memetakan token pendek ke ekspresi kueri lengkap, dan Anda juga dapat **menambahkan banyak alias** secara massal.  
- **Apakah memungkinkan mengekspor dan mengimpor kamus alias?** Tentu—gunakan metode `exportDictionary` dan `importDictionary`.  
- **Versi GroupDocs.Search apa yang diperlukan?** Versi 25.4 atau lebih baru (tutorial ini menggunakan 25.4).  

## Apa itu “menambahkan dokumen ke indeks”?
Menambahkan dokumen ke indeks berarti memasukkan file mentah (PDF, DOCX, TXT, dll.) ke dalam GroupDocs.Search sehingga perpustakaan dapat menganalisis kontennya dan membangun **indeks yang dapat dicari**. Setelah diindeks, Anda dapat menjalankan kueri teks lengkap yang cepat pada semua dokumen tersebut.

## Mengapa Mengelola Alias?
Alias memungkinkan Anda mengganti fragmen kueri yang panjang dan berulang dengan token pendek yang mudah diingat (mis., `@t` → `(gravida OR promotion)`). Ini tidak hanya mempersingkat string pencarian Anda tetapi juga meningkatkan keterbacaan, pemeliharaan, dan **mengoptimalkan kinerja pencarian**, terutama ketika kueri menjadi kompleks.

## Bagaimana cara menambahkan banyak alias?
GroupDocs.Search menyediakan metode `addRange` yang nyaman yang memungkinkan Anda menyisipkan banyak pasangan pengganti alias sekaligus. Operasi massal ini mengurangi beban dibandingkan menambahkan setiap alias secara terpisah.

## Prasyarat

- **GroupDocs.Search untuk Java** ≥ 25.4.  
- **JDK** (versi terbaru apa pun, mis., 11+).  
- Sebuah IDE seperti **IntelliJ IDEA** atau **Eclipse**.  
- Pengetahuan dasar Java dan Maven.  

## Menyiapkan GroupDocs.Search untuk Java

### Menggunakan Maven
Tambahkan repositori dan dependensi ke `pom.xml` Anda:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

### Unduhan Langsung
Sebagai alternatif, unduh JAR terbaru dari situs resmi:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Langkah-langkah Akuisisi Lisensi
1. **Free Trial** – jelajahi semua fitur tanpa komitmen.  
2. **Temporary License** – minta kunci jangka pendek untuk evaluasi.  
3. **Full Purchase** – dapatkan lisensi permanen untuk penggunaan produksi.  

### Inisialisasi dan Pengaturan Dasar

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        // Specify the directory to store indices
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
        
        // Create or open an index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## Panduan Implementasi

Berikut adalah panduan lengkap untuk setiap fitur. Baca penjelasan terlebih dahulu, kemudian salin blok kode yang sesuai.

### Membuat atau Membuka Indeks

**Cara menambahkan dokumen ke indeks – pertama Anda memerlukan instance Index yang aktif.**

#### Langkah 1: Impor kelas Index
```java
import com.groupdocs.search.Index;
```

#### Langkah 2: Tentukan lokasi file indeks
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
```

#### Langkah 3: Buat indeks baru atau buka yang sudah ada
```java
Index index = new Index(indexFolder);
```

### Menambahkan Dokumen ke Indeks

Sekarang indeks sudah ada, mari **menambahkan dokumen ke indeks**.

#### Langkah 1: Arahkan ke folder sumber Anda
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/Documents";
```

#### Langkah 2: Tambahkan setiap file yang didukung dari folder tersebut
```java
index.add(documentsFolder);
```

> **Tip Pro:** Jalankan langkah ini setiap kali file baru tiba. GroupDocs.Search hanya akan mengindeks konten baru, meninggalkan entri yang ada tidak tersentuh. Inilah esensi dari **incremental indexing java**.

### Mengelola Kamus Alias

Alias memungkinkan Anda memetakan token pendek ke string kueri kompleks. Kami akan membahas cara menghapus entri lama, menambahkan alias tunggal, dan **menambahkan banyak alias** secara massal.

#### Menghapus Alias yang Ada
```java
if (index.getDictionaries().getAliasDictionary().getCount() > 0) {
    index.getDictionaries().getAliasDictionary().clear();
}
```

#### Menambahkan Alias Tunggal
```java
index.getDictionaries().getAliasDictionary().add("t", "(gravida OR promotion)");
index.getDictionaries().getAliasDictionary().add("e", "(viverra OR farther)");
```

#### Menambahkan Banyak Alias
```java
AliasReplacementPair[] pairs = new AliasReplacementPair[] {
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};
index.getDictionaries().getAliasDictionary().addRange(pairs);
```

### Menanyakan Penggantian Alias

Anda dapat mengambil teks lengkap untuk setiap alias yang telah Anda definisikan:

```java
if (index.getDictionaries().getAliasDictionary().contains("e")) {
    String replacement = index.getDictionaries().getAliasDictionary().getText("e");
}
```

### Mengekspor dan Mengimpor Kamus Alias

Mengekspor berguna untuk pencadangan atau berbagi antar lingkungan.

#### Mengekspor Alias
```java
String fileName = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.getDictionaries().getAliasDictionary().exportDictionary(fileName);
```

#### Mengimpor Alias
```java
index.getDictionaries().getAliasDictionary().importDictionary(fileName);
```

### Mencari Menggunakan Kueri Alias

Dengan alias yang ada, string pencarian Anda menjadi jauh lebih bersih:

```java
String query = "@t OR @e";
SearchResult result = index.search(query);
```

Simbol `@` memberi tahu GroupDocs.Search untuk mengganti token dengan ekspresi lengkapnya sebelum mengeksekusi pencarian.

## Aplikasi Praktis

| Skenario | Bagaimana Alias Membantu |
|----------|--------------------------|
| **Manajemen Dokumen Hukum** | Pemetaan nomor kasus (`@case123`) ke klausa Boolean kompleks, mempercepat pengambilan. |
| **Pencarian Produk E‑commerce** | Ganti kombinasi atribut umum (`@sale`) dengan `(discounted OR clearance)`. |
| **Basis Data Penelitian** | Gunakan `@year2020` untuk memperluas menjadi filter rentang tanggal pada banyak makalah. |

## Pertimbangan Kinerja

- **Incremental Indexing:** Tambahkan hanya file baru atau yang berubah; hindari pengindeksan ulang penuh.  
- **JVM Tuning:** Alokasikan memori heap yang cukup (`-Xmx4g` untuk korpus besar).  
- **Batch Alias Updates:** Gunakan `addRange` untuk menyisipkan banyak alias sekaligus, mengurangi beban.  
- **Optimize Search Performance:** Jaga kamus alias tetap ramping dan gunakan kembali token secara bijak untuk meminimalkan waktu parsing kueri.

## Masalah Umum dan Solusinya

| Masalah | Solusi |
|---------|--------|
| File baru tidak dapat dicari | Jalankan `index.add(newFolder)` lagi; GroupDocs.Search hanya mengindeks file yang belum terlihat. |
| Alias mengembalikan hasil kosong | Verifikasi bahwa kunci alias (`@`) memiliki prefiks yang benar dan kamus berisi token tersebut. |
| Penggunaan memori tinggi selama pengindeksan massal | Tingkatkan heap JVM (`-Xmx`) dan pertimbangkan mengindeks dalam batch yang lebih kecil. |

## Pertanyaan yang Sering Diajukan

**Q: Apa manfaat utama menggunakan GroupDocs.Search untuk Java?**  
A: Ini menyediakan kemampuan pengindeksan dan pencarian teks lengkap yang kuat, siap pakai, memungkinkan Anda **menambahkan dokumen ke indeks** dengan cepat dan menanyakan mereka dengan kinerja tinggi.

**Q: Bisakah saya menggunakan GroupDocs.Search dengan basis data?**  
A: Ya—ekstrak data dari sumber apa pun (SQL, NoSQL, CSV) dan masukkan ke indeks menggunakan metode `add` yang sama.

**Q: Bagaimana alias meningkatkan efisiensi pencarian?**  
A: Alias memungkinkan Anda menyimpan logika kueri kompleks sekali dan menggunakannya kembali dengan token pendek, mengurangi waktu parsing kueri dan meminimalkan kesalahan manusia ketika Anda **mencari dengan alias**.

**Q: Apakah memungkinkan memperbarui alias yang ada tanpa membangun ulang seluruh kamus?**  
A: Tentu—cukup panggil `add` dengan kunci yang sama; perpustakaan akan menimpa nilai sebelumnya.

**Q: Apa yang harus saya lakukan jika pencarian saya menghasilkan hasil yang tidak terduga?**  
A: Verifikasi bahwa definisi alias sudah benar, lakukan pengindeksan ulang pada dokumen yang baru ditambahkan, dan periksa pengaturan analyzer untuk masalah tokenisasi.

---

**Terakhir Diperbarui:** 2026-03-06  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs