---
date: '2026-02-21'
description: Pelajari cara mengimplementasikan filter ekstensi file Java menggunakan
  GroupDocs.Search untuk Java, mencakup operator logika, tanggal pembuatan/modifikasi,
  dan filter jalur.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: Filter ekstensi file Java dengan GroupDocs.Search – Panduan
type: docs
url: /id/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

Tested With" and "Author". Keep as is? The instruction: translate all text. So translate.

**Last Updated:** 2026-02-21 -> "**Terakhir Diperbarui:** 2026-02-21"

**Tested With:** GroupDocs.Search 25.4 for Java -> "**Diuji Dengan:** GroupDocs.Search 25.4 for Java"

**Author:** GroupDocs -> "**Penulis:** GroupDocs"

Now ensure all markdown formatting preserved.

Check for any shortcodes: none.

Check code block placeholders: keep.

Check links: only one, kept.

Now produce final content.# Menguasai java file extension filter dengan GroupDocs.Search

Mengelola repositori dokumen yang terus bertambah dapat dengan cepat menjadi sangat membebani, terutama ketika Anda hanya perlu mengindeks tipe file tertentu. **The java file extension filter** memungkinkan Anda memberi tahu GroupDocs.Search secara tepat ekstensi mana yang harus disertakan atau dikecualikan, memberikan kontrol yang presisi atas pipeline pengindeksan Anda. Dalam panduan ini kami akan menjelaskan cara menyiapkan GroupDocs.Search untuk Java dan menunjukkan cara menggabungkan penyaringan ekstensi file dengan operator logika AND, OR, dan NOT, serta filter rentang tanggal dan jalur.

## Jawaban Cepat
- **Apa itu java file extension filter?** Sebuah konfigurasi yang memberi tahu GroupDocs.Search ekstensi file mana yang harus disertakan atau dikecualikan selama pengindeksan.  
- **Library mana yang menyediakan fitur ini?** GroupDocs.Search for Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya menggabungkan filter?** Ya – Anda dapat menghubungkan filter ekstensi, tanggal, ukuran, dan jalur dengan logika AND, OR, NOT.  
- **Apakah kompatibel dengan Maven?** Tentu – tambahkan dependensi GroupDocs.Search ke `pom.xml` Anda.

## Apa itu java file extension filter?
Sebuah **java file extension filter** adalah sekumpulan aturan yang mengevaluasi ekstensi setiap file sebelum dikirim ke mesin pengindeksan. Dengan menentukan ekstensi seperti `.txt`, `.pdf`, atau `.epub`, Anda dapat **include files by extension** atau **exclude files by extension** untuk menjaga indeks tetap terfokus dan hasil pencarian relevan.

## Mengapa menggunakan file‑extension filtering dengan GroupDocs.Search?
- **Performance:** Melewatkan file yang tidak diinginkan mengurangi I/O dan mempercepat pengindeksan.  
- **Storage savings:** Hanya dokumen yang relevan yang disimpan dalam indeks, mengurangi penggunaan disk.  
- **Compliance:** Mencegah pengindeksan tidak sengaja dari file rahasia atau tipe file yang tidak didukung.  
- **Flexibility:** Gabungkan dengan fitur **date range filter java** untuk menargetkan file yang dibuat atau dimodifikasi dalam periode tertentu.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal berikut:

### Perpustakaan dan Dependensi yang Diperlukan
- **GroupDocs.Search for Java**: Versi 25.4 atau lebih baru  
- **Java Development Kit (JDK)**: Versi yang kompatibel terpasang  

### Penyiapan Lingkungan
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse, atau IDE yang kompatibel dengan Maven apa pun.

### Prasyarat Pengetahuan
- Pemrograman Java dasar  
- Familiaritas dengan file I/O di Java  
- Pemahaman tentang regular expressions dan penanganan date‑time  

## Menyiapkan GroupDocs.Search untuk Java
Untuk mulai menggunakan GroupDocs.Search, Anda perlu menyertakannya sebagai dependensi dalam proyek Anda.

### Konfigurasi Maven
Tambahkan konfigurasi repositori dan dependensi berikut ke file `pom.xml` Anda:

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
Atau, unduh versi terbaru secara langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Akuisisi Lisensi
1. **Free Trial** – jelajahi fitur tanpa biaya.  
2. **Temporary License** – dapatkan fungsionalitas penuh untuk periode terbatas.  
3. **Purchase** – peroleh lisensi permanen untuk penggunaan produksi.  

### Inisialisasi dan Penyiapan Dasar
Setelah perpustakaan ditambahkan, inisialisasi lingkungan pengindeksan Anda:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Panduan Implementasi
Di bawah ini kami membahas setiap tipe filter, menjelaskan **mengapa penting** dan menyediakan kode langkah demi langkah yang dapat Anda salin ke proyek Anda.

### Penyaringan Ekstensi File
Filter file berdasarkan ekstensi mereka selama pengindeksan. Ini sempurna ketika Anda hanya ingin memproses e‑book (`.fb2`, `.epub`) dan file teks biasa (`.txt`).

#### Gambaran Umum
Gunakan `DocumentFilter.createFileExtension` untuk membuat daftar putih ekstensi.

#### Langkah Implementasi
1. **Create Filter**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter NOT Logika
Kecualikan ekstensi tertentu, seperti halaman web dan PDF, ketika tidak diperlukan untuk skenario pencarian Anda.

#### Langkah Implementasi
1. **Create Exclusion Filter**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to Index Settings**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add Documents**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter AND Logika
Gabungkan beberapa kondisi—tanggal pembuatan, ekstensi, dan ukuran file—sehingga **hanya file yang memenuhi semua kriteria** yang diindeks.

#### Gambaran Umum
`DocumentFilter.createAnd` menggabungkan beberapa filter menjadi satu aturan.

#### Langkah Implementasi
1. **Define Filters**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine Filters**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index Documents**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter OR Logika
Sertakan file yang memenuhi **any** dari kondisi yang ditentukan—berguna ketika Anda ingin menangkap baik file teks kecil maupun file non‑teks yang lebih besar.

#### Langkah Implementasi
1. **Define Filters**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine Filters with Logical Conditions**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR Filter**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter Waktu Pembuatan
Target file yang dibuat dalam periode tertentu—skenario klasik **date range filter java**.

#### Langkah Implementasi
1. **Define Date Range Filter**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index Documents**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter Waktu Modifikasi
Kecualikan file yang dimodifikasi setelah tanggal batas tertentu.

#### Langkah Implementasi
1. **Define Filter**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index Documents**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Penyaringan Jalur File
Batasi pengindeksan ke file yang berada di folder tertentu atau yang cocok dengan pola—ideal untuk **include files by extension** dalam hierarki direktori tertentu.

#### Langkah Implementasi
1. **Define File Path Filter**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Kesalahan Umum & Tips
- **Never mix absolute and relative paths** dalam konfigurasi filter yang sama – dapat menyebabkan pengecualian yang tidak terduga.  
- **Reset the `IndexSettings`** saat beralih set filter; jika tidak, filter sebelumnya dapat tetap ada.  
- **Combine a length upper bound with an extension filter** untuk koleksi besar agar penggunaan memori tetap rendah.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) untuk melihat mengapa sebuah file ditolak.  

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya mengubah kriteria filter setelah indeks dibuat?**  
A: Ya. Bangun kembali indeks dengan `DocumentFilter` baru atau gunakan pengindeksan inkremental dengan pengaturan yang diperbarui.

**Q: Apakah java file extension filter bekerja pada arsip terkompresi (mis., ZIP)?**  
A: GroupDocs.Search dapat mengindeks format arsip yang didukung, tetapi filter ekstensi diterapkan pada arsip itu sendiri, bukan pada file di dalamnya. Gunakan filter bersarang untuk kontrol yang lebih dalam.

**Q: Bagaimana cara saya men-debug mengapa file tertentu dikecualikan?**  
A: Aktifkan logging perpustakaan (`LoggingOptions.setEnabled(true)`) dan periksa log – log akan melaporkan filter mana yang menolak setiap file.

**Q: Apakah memungkinkan menggabungkan java file extension filter dengan filter regex khusus?**  
A: Tentu saja. Bungkus filter regex di dalam `DocumentFilter.createAnd()` bersama filter ekstensi.

**Q: Apa dampak kinerja menambahkan banyak filter?**  
A: Setiap filter menambah overhead yang wajar selama pengindeksan, tetapi pengurangan data yang diindeks biasanya melebihi biaya tersebut. Uji dengan sampel representatif untuk menemukan keseimbangan optimal.

---

**Terakhir Diperbarui:** 2026-02-21  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs