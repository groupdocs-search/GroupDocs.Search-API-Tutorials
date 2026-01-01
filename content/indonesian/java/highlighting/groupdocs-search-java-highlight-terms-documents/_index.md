---
date: '2025-12-26'
description: Pelajari cara mencari dan menyorot teks dalam dokumen menggunakan GroupDocs.Search
  untuk Java. Jelajahi teknik untuk penyorotan dokumen penuh dan fragmen.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Cari dan Sorot Teks dengan GroupDocs.Search untuk Java
type: docs
url: /id/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Cari dan Sorot Teks dalam Dokumen Menggunakan GroupDocs.Search untuk Java

Di era digital saat ini, **search and highlight text** di seluruh koleksi dokumen besar merupakan kebutuhan umum. Baik Anda sedang membangun alat tinjauan hukum, portal riset akademik, atau dasbor dukungan pelanggan, kemampuan untuk langsung menemukan dan menekankan istilah kunci secara signifikan meningkatkan kegunaan. Dalam panduan komprehensif ini, Anda akan menemukan cara mengimplementasikan **search and highlight text** dengan GroupDocs.Search untuk Java—mencakup sorotan seluruh dokumen dan sorotan tingkat fragmen untuk konteks yang terfokus.

## Jawaban Cepat
- **Apa arti “search and highlight text”?** Ini merujuk pada menemukan istilah kueri dalam dokumen dan menekankannya secara visual (misalnya, dengan warna latar belakang).  
- **Library mana yang menyediakan kemampuan ini?** GroupDocs.Search untuk Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Apakah saya dapat menyesuaikan warna sorotan?** Ya—warna RGB apa pun dapat diatur melalui `HighlightOptions`.  
- **Apakah sorotan fragmen didukung?** Tentu; Anda dapat menentukan istilah sebelum/setelah kecocokan untuk membuat potongan singkat.

## Apa Itu Search and Highlight Text?
Search and highlight text adalah proses memindai indeks dokumen untuk kueri tertentu, mengambil dokumen yang cocok, dan kemudian menandai setiap kemunculan istilah kueri dalam output dokumen (HTML, PDF, dll.). Petunjuk visual ini membantu pengguna akhir menemukan informasi yang relevan secara instan.

## Mengapa Menggunakan GroupDocs.Search untuk Java?
- **High‑performance indexing** dengan kompresi yang dapat dikonfigurasi.  
- **Rich highlighting API** yang bekerja pada seluruh dokumen dan fragmen khusus.  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT, dan lainnya).  
- **Easy Maven integration** dan API berorientasi Java yang jelas.

## Prasyarat
- Java Development Kit (JDK) 8 atau lebih baru.  
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

Anda juga dapat mengunduh JAR terbaru secara langsung dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Mulailah dengan percobaan gratis atau dapatkan lisensi sementara untuk evaluasi. Untuk penerapan produksi, beli lisensi penuh untuk membuka semua fitur.

## Panduan Implementasi

Implementasi dibagi menjadi dua bagian praktis: **highlighting in entire documents** dan **highlighting in fragments**. Kedua bagian mencakup langkah-langkah penting untuk **how to highlight Java** dokumen menggunakan GroupDocs.Search.

### Mengonfigurasi Pengaturan Indeks
Sebelum mengindeks, konfigurasikan penyimpanan untuk menggunakan kompresi tinggi—ini mengurangi penggunaan disk sambil mempertahankan kecepatan pencarian.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Highlighting in Entire Documents

#### Langkah 1: Buat dan Isi Indeks
Buat folder indeks dan tambahkan semua file sumber yang ingin Anda cari.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Langkah 2: Lakukan Pencarian dan Terapkan Sorotan
Cari istilah (mis., `ipsum`) dan hasilkan file HTML dengan kecocokan yang disorot.

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

### Highlighting in Fragments

#### Langkah 1: Indeks dan Cari (sama seperti di atas)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Langkah 2: Tentukan Konteks Fragmen dan Sorot
Tentukan berapa banyak istilah sebelum dan sesudah kecocokan yang harus muncul di setiap fragmen.

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
1. **Legal Document Review** – secara instan menyorot undang‑undang, klausul, atau referensi kasus.  
2. **Academic Research** – menampilkan terminologi kunci di ratusan PDF dan file Word.  
3. **Customer Support** – menemukan nomor pesanan atau kode error dalam riwayat tiket.

## Pertimbangan Kinerja
- **Index Size** – kompresi tinggi (`Compression.High`) mengurangi jejak disk.  
- **Fragment Context** – nilai `termsBefore/After` yang lebih besar meningkatkan akurasi tetapi dapat memengaruhi kecepatan.  
- **Memory Management** – pantau heap JVM saat mengindeks korpus besar; pertimbangkan indeks inkremental untuk set yang sangat besar.

## Masalah Umum dan Solusinya
- **Indexing Errors** – verifikasi jalur file dan pastikan aplikasi memiliki izin baca/tulis.  
- **No Highlights Appear** – pastikan `UseInlineStyles` sesuai dengan format output Anda (HTML vs. PDF).  
- **Color Not Applied** – pastikan nilai RGB berada dalam rentang 0‑255 dan penampil HTML mendukung gaya tersebut.

## Pertanyaan yang Sering Diajukan

**Q: Apa manfaat menggunakan GroupDocs.Search untuk Java?**  
A: Ia menawarkan pengindeksan cepat dan skalabel, sorotan yang dapat disesuaikan, serta dukungan untuk banyak format dokumen.

**Q: Bagaimana saya dapat mengintegrasikan GroupDocs.Search dengan REST API?**  
A: Ekspose metode pencarian dan sorotan melalui kontroler Spring Boot, mengembalikan payload HTML atau JSON.

**Q: Apakah perpustakaan ini menangani file yang dilindungi password?**  
A: Ya—berikan password saat menambahkan dokumen ke indeks.

**Q: Bisakah saya menyesuaikan markup sorotan selain warna?**  
A: Tentu; Anda dapat menyuntikkan kelas CSS melalui `HighlightOptions` atau memodifikasi HTML setelah dibuat.

**Q: Versi apa yang diuji untuk panduan ini?**  
A: Kode telah divalidasi terhadap GroupDocs.Search 25.4.

---

**Terakhir Diperbarui:** 2025-12-26  
**Diuji Dengan:** GroupDocs.Search 25.4  
**Penulis:** GroupDocs