---
date: '2026-02-27'
description: Pelajari cara menyorot teks Java menggunakan GroupDocs.Search untuk Java,
  mencakup pencarian dokumen Java, pengindeksan dokumen Java, dan penyorotan fragmen.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Sorot Teks Java dengan GroupDocs.Search
type: docs
url: /id/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Sorot Teks Java dengan GroupDocs.Search

Di lingkungan digital yang bergerak cepat saat ini, kemampuan untuk **highlight text java** di seluruh koleksi file yang besar merupakan fitur yang wajib dimiliki. Baik Anda sedang membangun platform peninjauan hukum, mesin riset akademik, atau konsol dukungan pelanggan, menemukan istilah yang dicari pengguna secara instan membuat pengalaman jauh lebih efisien. Tutorial ini memandu Anda menggunakan **GroupDocs.Search for Java** untuk **search documents java**, **index documents java**, dan menerapkan sorotan kaya—baik untuk seluruh dokumen maupun untuk fragmen terfokus.

## Jawaban Cepat
- **Apa arti “search and highlight text”?** Ini merujuk pada menemukan istilah kueri dalam dokumen dan menekankannya secara visual (misalnya, dengan warna latar belakang).  
- **Perpustakaan mana yang menyediakan kemampuan ini?** GroupDocs.Search for Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya menyesuaikan warna sorotan?** Ya—warna RGB apa pun dapat diatur melalui `HighlightOptions`.  
- **Apakah sorotan fragmen didukung?** Tentu saja; Anda dapat menentukan istilah sebelum/setelah kecocokan untuk membuat potongan singkat.

## Cara Menyorot Teks Java dalam Dokumen
Menyorot teks Java melibatkan tiga langkah inti:

1. **Indeks file sumber** sehingga dapat dicari dengan cepat.  
2. **Jalankan kueri** terhadap indeks untuk menemukan dokumen yang cocok.  
3. **Render hasil dengan petunjuk visual** menggunakan API highlighter.

Di bawah ini kami menjelajahi setiap langkah secara detail, pertama untuk output seluruh dokumen dan kemudian untuk potongan tingkat fragmen.

## Apa Itu Search and Highlight Text?
Search and highlight text adalah proses memindai indeks dokumen untuk kueri tertentu, mengambil dokumen yang cocok, dan kemudian menandai setiap kemunculan istilah kueri dalam output dokumen (HTML, PDF, dll.). Petunjuk visual ini membantu pengguna akhir menemukan informasi relevan secara instan.

## Mengapa Menggunakan GroupDocs.Search untuk Java?
- **Pengindeksan berperforma tinggi** dengan kompresi yang dapat dikonfigurasi (`index documents java`).  
- **API sorotan kaya** yang bekerja pada seluruh dokumen dan fragmen khusus (`highlight search terms java`).  
- **Dukungan lintas format** (DOCX, PDF, PPTX, TXT, dan lainnya).  
- **Integrasi Maven yang sederhana** dan desain yang berfokus pada Java.

## Prasyarat
- Java Development Kit (JDK) 8 atau yang lebih baru.  
- Maven untuk manajemen dependensi.  
- IDE seperti IntelliJ IDEA atau Eclipse.  
- Familiaritas dasar dengan sintaks Java.

## Menyiapkan GroupDocs.Search untuk Java

Tambahkan repositori GroupDocs dan dependensi ke `pom.xml` Anda:

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

Anda juga dapat mengunduh JAR terbaru secara langsung dari situs resmi: [Rilis GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Mulailah dengan percobaan gratis atau dapatkan lisensi sementara untuk evaluasi. Untuk penerapan produksi, beli lisensi penuh untuk membuka semua fitur.

## Panduan Implementasi

Implementasi dibagi menjadi dua bagian praktis: **menyorot dalam seluruh dokumen** dan **menyorot dalam fragmen**. Kedua bagian mencakup langkah penting untuk **cara menyorot Java** dokumen menggunakan GroupDocs.Search.

### Mengonfigurasi Pengaturan Indeks
Sebelum mengindeks, konfigurasikan penyimpanan untuk menggunakan kompresi tinggi—ini mengurangi penggunaan disk sambil mempertahankan kecepatan pencarian.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Menyorot dalam Seluruh Dokumen

#### Langkah 1: Buat dan Isi Indeks
Buat folder indeks dan tambahkan semua file sumber yang ingin Anda cari.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Langkah 2: Lakukan Pencarian dan Terapkan Sorotan
Cari istilah (misalnya `ipsum`) dan hasilkan file HTML dengan kecocokan yang disorot.

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

**Opsi utama dijelaskan**  
- **Compression** – kompresi tinggi menghemat penyimpanan.  
- **HighlightColor** – atur nilai RGB apa pun untuk menyesuaikan palet UI Anda.  
- **UseInlineStyles** – `false` menghasilkan HTML bersih yang dapat ditata secara global dengan CSS.  

### Menyorot dalam Fragmen

#### Langkah 1: Indeks dan Pencarian (sama seperti di atas)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Langkah 2: Tentukan Konteks Fragmen dan Sorot
Tentukan berapa banyak istilah sebelum dan setelah kecocokan yang harus muncul dalam setiap fragmen.

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

#### Langkah 3: Ambil dan Tulis Fragmen yang Disorot
Kumpulkan fragmen yang dihasilkan dan tulis ke file HTML.

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

## Aplikasi Praktis
1. **Peninjauan Dokumen Hukum** – secara instan menyorot undang‑undang, klausul, atau referensi kasus.  
2. **Penelitian Akademik** – menampilkan terminologi kunci di ratusan PDF dan file Word.  
3. **Dukungan Pelanggan** – menemukan nomor pesanan atau kode error dalam riwayat tiket.

## Pertimbangan Kinerja
- **Index Size** – kompresi tinggi (`Compression.High`) mengurangi jejak disk.  
- **Fragment Context** – nilai `termsBefore/After` yang lebih besar meningkatkan akurasi tetapi dapat memengaruhi kecepatan.  
- **Memory Management** – pantau heap JVM saat mengindeks korpus besar; pertimbangkan pengindeksan inkremental untuk set yang sangat besar.

## Masalah Umum dan Solusinya
- **Indexing Errors** – verifikasi jalur file dan pastikan aplikasi memiliki izin baca/tulis.  
- **No Highlights Appear** – pastikan `UseInlineStyles` sesuai dengan format output Anda (HTML vs. PDF).  
- **Color Not Applied** – pastikan nilai RGB berada dalam rentang 0‑255 dan penampil HTML mendukung gaya tersebut.

## Pertanyaan yang Sering Diajukan

**Q: Apa manfaat menggunakan GroupDocs.Search untuk Java?**  
A: Menawarkan pengindeksan cepat dan skalabel, sorotan yang dapat disesuaikan, serta dukungan untuk banyak format dokumen.

**Q: Bagaimana cara mengintegrasikan GroupDocs.Search dengan REST API?**  
A: Ekspose metode pencarian dan sorotan melalui controller Spring Boot, mengembalikan payload HTML atau JSON.

**Q: Apakah perpustakaan menangani file yang dilindungi kata sandi?**  
A: Ya—berikan kata sandi saat menambahkan dokumen ke indeks.

**Q: Bisakah saya menyesuaikan markup sorotan selain warna?**  
A: Tentu saja; Anda dapat menyuntikkan kelas CSS via `HighlightOptions` atau memodifikasi HTML setelah dibuat.

**Q: Versi apa yang diuji untuk panduan ini?**  
A: Kode telah divalidasi terhadap GroupDocs.Search 25.4.

**Q: Bagaimana cara set highlight options java untuk menggunakan kelas CSS alih-alih gaya inline?**  
A: Atur `options.setUseInlineStyles(false)` dan tambahkan aturan CSS untuk kelas yang Anda tetapkan via `options.setCssClass("myHighlight")`.

**Q: Apakah ada cara untuk highlight terms pdf java langsung ketika sumbernya PDF?**  
A: Ya—GroupDocs.Search bekerja dengan input PDF, dan highlighter akan menghasilkan HTML yang dapat Anda sematkan dalam penampil PDF atau konversi kembali ke PDF menggunakan GroupDocs.Conversion.

---

**Terakhir Diperbarui:** 2026-02-27  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs