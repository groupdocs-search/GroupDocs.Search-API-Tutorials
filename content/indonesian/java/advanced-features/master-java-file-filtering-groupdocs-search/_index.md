---
date: '2026-09-06'
description: Pelajari cara memfilter ekstensi file java menggunakan GroupDocs.Search
  untuk Java, mencakup operator logika AND, OR, NOT, filter rentang tanggal, dan filter
  jalur.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Filter ekstensi file java menggunakan GroupDocs.Search. Pelajari cara
  menggabungkan filter ekstensi, rentang tanggal, dan jalur dengan operator logika
  di Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Filter ekstensi file java dengan GroupDocs.Search – Panduan Lengkap
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Cara memfilter ekstensi file java dengan GroupDocs.Search
type: docs
url: /id/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filter ekstensi file java dengan GroupDocs.Search

Dalam tutorial komprehensif ini Anda akan belajar cara **filter file extensions java** saat mengindeks dokumen dengan GroupDocs.Search. Pada akhir panduan Anda akan dapat menyertakan hanya jenis file yang Anda butuhkan, mengecualikan format yang tidak diinginkan, dan menggabungkan aturan tersebut dengan filter rentang tanggal dan jalur menggunakan operator logika AND, OR, dan NOT. Pendekatan ini membuat indeks Anda lebih ramping, mempercepat pencarian, dan membantu Anda tetap mematuhi kebijakan penanganan data.

## Jawaban cepat
- **Apa itu filter ekstensi file java?** Ini adalah aturan yang memberi tahu GroupDocs.Search ekstensi file mana yang harus disertakan atau dikecualikan selama pengindeksan.  
- **Library mana yang menyediakan fitur ini?** GroupDocs.Search for Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya menggabungkan filter?** Ya – Anda dapat menghubungkan filter ekstensi, tanggal, ukuran, dan jalur dengan logika AND, OR, NOT.  
- **Apakah kompatibel dengan Maven?** Tentu – tambahkan dependensi GroupDocs.Search ke `pom.xml` Anda.

## Apa itu filter ekstensi file java?
Sebuah **java file extension filter** adalah sekumpulan aturan yang mengevaluasi ekstensi setiap file sebelum dikirim ke mesin pengindeksan. Dengan menentukan ekstensi seperti `.txt`, `.pdf`, atau `.epub`, Anda dapat **include files by extension** atau **exclude files by extension** untuk menjaga indeks tetap terfokus dan hasil pencarian relevan.

## Mengapa menggunakan filter ekstensi file dengan GroupDocs.Search?
Filter ekstensi file meningkatkan efisiensi pengindeksan dengan mengecualikan format yang tidak relevan, mengurangi kebutuhan penyimpanan, dan membantu memenuhi aturan kepatuhan dengan mencegah konten yang tidak diinginkan masuk ke indeks. Ini juga memungkinkan respons kueri yang lebih cepat karena mesin pencari memproses dataset yang lebih kecil dan lebih relevan.

- **Performance:** Melewatkan file yang tidak diinginkan mengurangi I/O dan mempercepat pengindeksan hingga 40 % pada repositori besar.  
- **Storage savings:** Hanya dokumen yang relevan yang disimpan dalam indeks, mengurangi penggunaan disk rata‑rata sebesar 30 %.  
- **Compliance:** Mencegah pengindeksan tidak sengaja terhadap tipe file yang rahasia atau tidak didukung.  
- **Flexibility:** Gabungkan dengan fitur **date range filter java** untuk menargetkan file yang dibuat atau dimodifikasi dalam periode tertentu.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal berikut:

### Perpustakaan dan dependensi yang diperlukan
- **GroupDocs.Search for Java** – versi 25.4 atau lebih baru (mendukung lebih dari 60 format input).  
- **Java Development Kit (JDK)** – versi yang kompatibel apa pun (8 atau lebih baru).

### Pengaturan lingkungan
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse, atau IDE yang kompatibel dengan Maven apa pun.

### Prasyarat pengetahuan
- Pemrograman Java dasar.  
- Familiaritas dengan file I/O di Java.  
- Pemahaman tentang ekspresi reguler dan penanganan tanggal‑waktu.

## Menyiapkan GroupDocs.Search untuk Java
Untuk mulai menggunakan GroupDocs.Search, Anda perlu menyertakannya sebagai dependensi dalam proyek Anda.

### Konfigurasi Maven
Tambahkan repositori dan konfigurasi dependensi berikut ke file `pom.xml` Anda:

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

### Unduhan langsung
Sebagai alternatif, unduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Perolehan lisensi
1. **Free trial** – jelajahi fitur tanpa biaya.  
2. **Temporary license** – dapatkan fungsionalitas penuh untuk periode terbatas.  
3. **Purchase** – peroleh lisensi permanen untuk penggunaan produksi.

### Inisialisasi dan pengaturan dasar
Setelah perpustakaan ditambahkan, inisialisasi lingkungan pengindeksan Anda. Kelas `IndexSettings` menyimpan semua opsi konfigurasi, termasuk filter.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Panduan implementasi
Di bawah ini kami membahas setiap tipe filter, menjelaskan **why it matters** dan memberikan instruksi langkah‑demi‑langkah yang dapat Anda salin ke dalam proyek Anda.

### Filter ekstensi file
Filter file berdasarkan ekstensi mereka selama pengindeksan. Ini sempurna ketika Anda hanya ingin memproses e‑book (`.fb2`, `.epub`) dan file teks biasa (`.txt`).

#### Gambaran umum
`DocumentFilter.createFileExtension` membuat daftar putih ekstensi.

#### Langkah‑langkah implementasi
1. **Create filter** – tentukan ekstensi yang ingin Anda pertahankan.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – terapkan filter saat membangun `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter NOT logika
Kecualikan ekstensi tertentu, seperti halaman web dan PDF, ketika tidak diperlukan untuk skenario pencarian Anda.

#### Langkah‑langkah implementasi
1. **Create exclusion filter** – tentukan ekstensi yang akan ditolak.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – gabungkan filter NOT dengan aturan lain.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – hanya file yang lolos filter gabungan yang diindeks.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter AND logika
Gabungkan beberapa kondisi—tanggal pembuatan, ekstensi, dan ukuran file—sehingga **only files that meet all criteria** diindeks.

#### Gambaran umum
`DocumentFilter.createAnd` menggabungkan beberapa filter menjadi satu aturan.

#### Langkah‑langkah implementasi
1. **Define filters** – buat filter individu untuk setiap kondisi.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – gunakan operator AND untuk memerlukan semua kondisi.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – berikan filter gabungan ke pipeline pengindeksan.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter OR logika
Sertakan file yang memenuhi **any** dari kondisi yang ditentukan—berguna ketika Anda ingin menangkap baik file teks kecil maupun file non‑teks yang lebih besar.

#### Langkah‑langkah implementasi
1. **Define filters** – buat filter terpisah untuk setiap kondisi alternatif.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – gunakan operator OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – lampirkan filter gabungan ke konfigurasi indeks.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter waktu pembuatan
Target file yang dibuat dalam periode tertentu—skenario klasik **date range filter java**.

#### Langkah‑langkah implementasi
1. **Define date‑range filter** – tentukan tanggal mulai dan akhir.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – hanya file yang timestamp pembuatannya berada dalam rentang tersebut yang diindeks.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter waktu modifikasi
Kecualikan file yang dimodifikasi setelah tanggal batas tertentu.

#### Langkah‑langkah implementasi
1. **Define filter** – tetapkan timestamp modifikasi maksimum.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – file yang lebih baru dari batas diabaikan.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Filter jalur file
Batasi pengindeksan ke file yang berada di folder tertentu atau yang cocok dengan pola—ideal untuk **include files by extension** dalam hierarki direktori tertentu.

#### Langkah‑langkah implementasi
1. **Define file‑path filter** – gunakan pola glob atau regex untuk mencocokkan direktori.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – terapkan filter jalur bersama aturan lain.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Jebakan umum & tips

- **Never mix absolute and relative paths** dalam konfigurasi filter yang sama – dapat menyebabkan pengecualian yang tidak terduga.  
- **Reset the `IndexSettings`** saat beralih set filter; jika tidak, filter sebelumnya dapat tetap ada.  
- **Combine a length upper bound with an extension filter** untuk koleksi besar agar penggunaan memori tetap rendah.  
- LoggingOptions mengontrol konfigurasi logging untuk GroupDocs.Search.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) untuk melihat mengapa sebuah file ditolak.  

## Pertanyaan yang sering diajukan

**Q: Bisakah saya mengubah kriteria filter setelah indeks dibuat?**  
A: Ya. Bangun kembali indeks dengan `DocumentFilter` baru atau gunakan pengindeksan inkremental dengan pengaturan yang diperbarui.

**Q: Apakah filter ekstensi file java bekerja pada arsip terkompresi (mis., ZIP)?**  
A: GroupDocs.Search dapat mengindeks format arsip yang didukung, tetapi filter ekstensi berlaku pada arsip itu sendiri, bukan pada file di dalamnya. Gunakan filter bersarang untuk kontrol yang lebih mendalam.

**Q: Bagaimana cara saya men-debug mengapa file tertentu dikecualikan?**  
A: Aktifkan logging library (`LoggingOptions.setEnabled(true)`) dan periksa log – log akan melaporkan filter mana yang menolak setiap file.

**Q: Apakah memungkinkan menggabungkan filter ekstensi file java dengan filter regex khusus?**  
A: Tentu. Bungkus filter regex di dalam `DocumentFilter.createAnd()` bersama filter ekstensi.

**Q: Apa dampak kinerja menambahkan banyak filter?**  
A: Setiap filter menambahkan overhead yang wajar selama pengindeksan, tetapi pengurangan data yang diindeks biasanya melebihi biaya tersebut. Uji dengan sampel representatif untuk menemukan keseimbangan optimal.

---

**Terakhir Diperbarui:** 2026-09-06  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Format Tanggal Kustom Java | Pencarian Rentang Tanggal dengan GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Menguasai Pencarian Boolean dengan GroupDocs.Search untuk Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Optimalkan Kinerja Pencarian dengan Teknik Pengindeksan Lanjutan di GroupDocs.Search untuk Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}