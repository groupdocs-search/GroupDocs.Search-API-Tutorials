---
date: '2026-09-27'
description: Pelajari cara menyorot teks Java menggunakan GroupDocs.Search untuk Java,
  mencakup search documents java, index documents java, dan fragment highlighting.
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: Pelajari cara menyorot teks Java menggunakan GroupDocs.Search untuk
  Java. Dapatkan panduan langkah demi langkah tentang pengindeksan, pencarian, dan
  fragment highlighting untuk hasil cepat.
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: Sorot teks Java dengan GroupDocs.Search – Penyorotan dokumen cepat
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: Sorot teks Java dengan GroupDocs.Search
type: docs
url: /id/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Sorot teks java dengan GroupDocs.Search

Dalam aplikasi perusahaan modern, **highlight text java** penting untuk mengubah hasil pencarian mentah menjadi wawasan yang dapat dibaca secara instan. Baik Anda membangun portal peninjauan hukum, mesin riset akademik, atau dasbor dukungan pelanggan, kemampuan untuk menemukan dan menekankan istilah kueri secara visual menghemat banyak detik pemindaian manual bagi pengguna. Tutorial ini menunjukkan cara menggunakan **GroupDocs.Search for Java** untuk **search documents java**, **index documents java**, dan menerapkan penyorotan baik pada dokumen penuh maupun level fragmen, semuanya dengan hanya beberapa baris kode.

## Jawaban Cepat
- **Apa arti “search and highlight text”?** Artinya menemukan istilah kueri di dalam dokumen dan menekankannya secara visual (misalnya, dengan latar belakang berwarna).  
- **Perpustakaan mana yang menyediakan kemampuan ini?** GroupDocs.Search for Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk penggunaan produksi.  
- **Bisakah saya menyesuaikan warna sorotan?** Ya—warna RGB apa pun dapat diatur melalui `HighlightOptions`.  
- **Apakah sorotan fragmen didukung?** Tentu; Anda dapat menentukan istilah sebelum/setelah kecocokan untuk membuat potongan singkat.

## Cara menyorot teks java dalam dokumen

Untuk menyorot teks java dalam dokumen, pertama bangun indeks file sumber menggunakan pengaturan kompresi yang tepat, kemudian jalankan kueri pencarian untuk menemukan istilah yang diinginkan, dan akhirnya ekspor hasil ke HTML, PDF, atau teks biasa dengan setiap kecocokan dibungkus dalam tag sorotan. Proses tiga langkah ini memastikan sorotan yang cepat dan akurat pada koleksi besar.

1. **Buat indeks** dengan pengaturan kompresi yang menjaga jejak penyimpanan tetap rendah.  
2. **Jalankan pencarian** menggunakan string kueri yang ingin Anda sorot.  
3. **Hasilkan output** (HTML, PDF, atau teks biasa) di mana setiap kemunculan istilah kueri dibungkus dalam tag sorotan.

## Apa itu pencarian dan penyorotan teks?

Pencarian dan penyorotan teks adalah proses memindai koleksi terindeks untuk kueri tertentu, mengambil dokumen yang cocok, dan kemudian menandai setiap kemunculan istilah kueri dalam output (HTML, PDF, dll.). Petunjuk visual ini membantu pengguna akhir menemukan informasi relevan secara instan.

## Mengapa menggunakan GroupDocs.Search untuk Java?

GroupDocs.Search untuk Java menyediakan **indeksasi berperforma tinggi** (hingga 50 GB per indeks dengan `Compression.High`), **penyorotan kaya** yang berfungsi pada seluruh dokumen dan fragmen khusus, serta **dukungan lintas format** untuk lebih dari 30 tipe file—termasuk DOCX, PDF, PPTX, dan TXT. Perpustakaan ini juga menawarkan **indeksasi inkremental**, memungkinkan Anda menambahkan file baru tanpa membangun ulang seluruh indeks, yang mengurangi waktu henti hingga 80 % pada penyebaran skala besar.

## Prasyarat
- Java Development Kit (JDK) 8 atau yang lebih baru.  
- Maven untuk manajemen dependensi.  
- IDE seperti IntelliJ IDEA atau Eclipse.  
- Familiaritas dasar dengan sintaks Java.

## Menyiapkan GroupDocs.Search untuk Java

Add the GroupDocs repository and dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

Anda juga dapat mengunduh JAR terbaru langsung dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Mulailah dengan percobaan gratis atau dapatkan lisensi sementara untuk evaluasi. Untuk penyebaran produksi, beli lisensi penuh untuk membuka semua fitur.

## Panduan Implementasi

Implementasi dibagi menjadi dua bagian praktis: **penyorotan dalam seluruh dokumen** dan **penyorotan dalam fragmen**. Kedua bagian mencakup langkah-langkah penting untuk **cara menyorot dokumen Java** menggunakan GroupDocs.Search.

### Mengonfigurasi pengaturan indeks

Sebelum mengindeks, konfigurasikan penyimpanan untuk menggunakan kompresi tinggi—ini mengurangi penggunaan disk hingga 70 % sambil mempertahankan kecepatan pencarian.

`IndexSettings` adalah objek konfigurasi yang mengontrol cara indeks disimpan di disk. Atur `Compression` ke `Compression.High` untuk mengaktifkan optimisasi ini.  
`Compression` menentukan tingkat kompresi data yang diterapkan pada file indeks, dengan `Compression.High` memberikan pengurangan ukuran maksimum.

## Penyorotan dalam seluruh dokumen

### Langkah 1: buat dan isi indeks

Buat folder indeks dan tambahkan semua file sumber yang ingin Anda cari. Kelas `Index` mewakili kontainer yang dapat dicari.

### Langkah 2: lakukan pencarian dan terapkan penyorotan

Cari istilah (mis., `ipsum`) dan hasilkan file HTML dengan kecocokan yang disorot. Gunakan `HighlightOptions` untuk menentukan warna sorotan dan apakah akan menggunakan gaya inline.

`HighlightOptions` memungkinkan Anda menentukan warna latar depan dan latar belakang, serta kelas CSS yang akan diterapkan pada setiap istilah yang disorot.

`HtmlHighlighter` menghasilkan output HTML dengan istilah yang disorot berdasarkan opsi yang diberikan.  
`SearchResult` berisi daftar dokumen yang cocok dan posisi setiap istilah yang ditemukan.

**Jawaban langsung:** Muat indeks Anda, panggil `search("ipsum")`, dan berikan `SearchResult` yang dihasilkan bersama dengan instance `HighlightOptions` yang telah dikonfigurasi ke `HtmlHighlighter`. Highlighter mengembalikan HTML di mana setiap kemunculan “ipsum” dibungkus dalam `<span>` dengan warna latar belakang yang dipilih.

Penjelasan opsi utama  
- **Compression** – kompresi tinggi menghemat penyimpanan.  
- **HighlightColor** – atur nilai RGB apa pun untuk mencocokkan palet UI Anda.  
- **UseInlineStyles** – `false` menghasilkan HTML bersih yang dapat ditata secara global dengan CSS.  

## Penyorotan dalam fragmen

### Langkah 1: indeks dan pencarian (sama seperti di atas)

Langkah indeks dan pencarian yang sama berlaku; Anda menggunakan kembali objek `Index` dan `SearchResult`.

### Langkah 2: definisikan konteks fragmen dan sorot

Tentukan berapa banyak istilah sebelum dan setelah kecocokan yang harus muncul di setiap fragmen dengan `FragmentOptions`.

`FragmentOptions` mengontrol jumlah kata di sekitar (`termsBefore` dan `termsAfter`) yang termasuk dalam setiap potongan, memungkinkan Anda menyeimbangkan konteks dengan panjang potongan.

### Langkah 3: ambil dan tulis fragmen yang disorot

Kumpulkan fragmen yang dihasilkan dan tulis ke file HTML. Setiap fragmen sudah disorot sesuai dengan `HighlightOptions` yang Anda konfigurasikan.

`fragmentHighlighter` adalah utilitas yang membuat potongan yang disorot dari `SearchResult` menggunakan opsi fragmen dan sorotan yang ditentukan.

**Jawaban langsung:** Setelah memperoleh `SearchResult`, panggil `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)`. Metode ini mengembalikan daftar potongan HTML, masing-masing berisi istilah yang cocok dikelilingi oleh jumlah kata konteks yang dikonfigurasi dan disorot dengan warna yang dipilih.

## Aplikasi Praktis
1. **Peninjauan dokumen hukum** – secara instan menyorot undang‑undang, klausul, atau referensi kasus di seluruh ribuan kontrak.  
2. **Riset akademik** – menampilkan terminologi kunci di puluhan file PDF dan Word, mengurangi waktu tinjauan literatur hingga 60 %.  
3. **Dukungan pelanggan** – menandai nomor pesanan atau kode error dalam riwayat tiket, memungkinkan agen menyelesaikan masalah lebih cepat.

## Pertimbangan Kinerja
- **Ukuran indeks** – kompresi tinggi (`Compression.High`) mengurangi jejak disk hingga 70 % tanpa dampak latensi yang terlihat.  
- **Konteks fragmen** – nilai `termsBefore/After` yang lebih besar meningkatkan keterbacaan potongan tetapi dapat menambah 10–15 ms per kueri.  
- **Manajemen memori** – pantau heap JVM saat mengindeks korpus besar; pertimbangkan indeksasi inkremental untuk dataset yang melebihi 2 GB agar penggunaan memori tetap di bawah 1 GB.

## Masalah Umum dan Solusinya
- **Kesalahan pengindeksan** – verifikasi jalur file dan pastikan aplikasi memiliki izin baca/tulis pada folder indeks.  
- **Tidak ada sorotan yang muncul** – pastikan `UseInlineStyles` sesuai dengan format output Anda (HTML vs. PDF).  
- **Warna tidak diterapkan** – pastikan nilai RGB berada dalam rentang 0‑255 dan bahwa penampil menghormati CSS inline atau kelas CSS yang disediakan.

## Pertanyaan yang Sering Diajukan

**Q: Apa manfaat menggunakan GroupDocs.Search untuk Java?**  
A: Menawarkan indeksasi cepat dan skalabel, penyorotan yang dapat disesuaikan, serta dukungan untuk lebih dari 30 format dokumen, memproses file 500‑halaman dalam kurang dari 2 detik pada server tipikal.

**Q: Bagaimana saya dapat mengintegrasikan GroupDocs.Search dengan REST API?**  
A: Ekspose metode pencarian dan penyorotan melalui controller Spring Boot, mengembalikan potongan HTML atau payload JSON yang berisi fragmen yang disorot.

**Q: Apakah perpustakaan ini menangani file yang dilindungi password?**  
A: Ya—berikan password saat menambahkan dokumen ke indeks melalui `addDocument(filePath, password)`.

**Q: Bisakah saya menyesuaikan markup sorotan selain warna?**  
A: Tentu; Anda dapat menetapkan kelas CSS dengan `options.setCssClass("myHighlight")` dan menata secara global, atau memodifikasi HTML yang dihasilkan setelah penyorotan.

**Q: Versi apa yang diuji untuk panduan ini?**  
A: Kode telah divalidasi terhadap GroupDocs.Search 25.4.

**Q: Bagaimana cara mengatur highlight options java untuk menggunakan kelas CSS alih-alih gaya inline?**  
A: Panggil `options.setUseInlineStyles(false)` dan definisikan aturan CSS untuk kelas yang Anda tetapkan melalui `options.setCssClass("myHighlight")`.

**Q: Apakah ada cara untuk menyorot istilah dalam output PDF secara langsung?**  
A: Ya—GroupDocs.Search bekerja dengan input PDF, dan highlighter menghasilkan HTML yang dapat disematkan dalam penampil PDF atau dikonversi kembali ke PDF menggunakan GroupDocs.Conversion.

**Terakhir diperbarui:** 2026-09-27  
**Diuji dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Tutorial Terkait

- [Cara mengimplementasikan pencarian teks penuh java: buat direktori indeks dengan GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Pelajari Cara Mengelola Indeks Pencarian dengan GroupDocs.Search untuk Java](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [Tambahkan dokumen ke indeks dengan pencarian berbasis chunk dalam Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)