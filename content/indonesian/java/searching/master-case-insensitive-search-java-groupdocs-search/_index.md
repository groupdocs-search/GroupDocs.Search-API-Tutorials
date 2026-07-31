---
date: '2026-07-31'
description: Pelajari cara mengimplementasikan pencarian tidak sensitif huruf di Java
  dengan menambahkan dokumen ke indeks menggunakan GroupDocs.Search, serta menggunakan
  penggantian karakter untuk menormalkan teks selama proses pengindeksan.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Pencarian tidak sensitif huruf di Java memungkinkan Anda menambahkan
  dokumen ke indeks dan melakukan kueri tanpa khawatir tentang huruf besar/kecil.
  Panduan ini menunjukkan bagaimana GroupDocs.Search menormalkan teks selama pengindeksan
  untuk hasil yang cepat dan dapat diandalkan.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Pencarian Tidak Sensitif Huruf Java – Indeks Dokumen dengan GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Tambahkan Dokumen ke Indeks untuk Pencarian Tidak Sensitif Huruf di Java
type: docs
url: /id/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Tambah Dokumen ke Indeks untuk Pencarian Tidak Sensitif Huruf Besar/Kecil di Java

Ketika Anda membutuhkan **case insensitive search java** yang dapat menemukan informasi secara andal terlepas dari cara pengguna mengetiknya, kuncinya adalah menambahkan dokumen ke indeks sambil menormalkan teks. Dalam tutorial ini kami menjelaskan cara mengonfigurasi GroupDocs.Search untuk Java sehingga setiap dokumen yang Anda indeks secara otomatis diubah menjadi huruf kecil (atau transformasi lain) selama proses pengindeksan, menjamin hasil yang tidak sensitif huruf besar/kecil tanpa logika tambahan pada waktu kueri.

## Jawaban Cepat
- **Apa arti “add documents to index”?** Artinya memuat file sumber ke dalam struktur data yang dapat dicari sehingga dapat dipertanyakan nanti.  
- **Mengapa menggunakan penggantian karakter?** Ini menormalkan setiap karakter—biasanya menjadi huruf kecil—sehingga pencarian mengabaikan perbedaan huruf secara otomatis.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi penuh diperlukan untuk penerapan produksi.  
- **Versi Java mana yang diperlukan?** Java 8 atau yang lebih baru; perpustakaan menargetkan Java 11+ untuk kinerja optimal.  
- **Bisakah saya beralih ke pencarian sensitif huruf besar/kecil bila diperlukan?** Ya—opsi pencarian memungkinkan Anda mengaktifkan atau menonaktifkan sensitivitas huruf per kueri.

## Apa itu “add documents to index” dalam GroupDocs.Search?
Muat file sumber Anda (PDF, DOCX, TXT, dll.) ke dalam indeks yang dapat dicari sehingga mesin dapat mengambilnya dengan cepat. Menambahkan dokumen ke indeks mem-parsing setiap file, mengekstrak teks polos, dan menyimpannya dalam struktur data yang dioptimalkan untuk pencarian cepat.

## Mengapa mengaktifkan penggantian karakter selama pengindeksan?
Penggantian karakter mengubah setiap karakter menjadi padanan yang telah ditentukan—biasanya huruf kecil—sementara indeks dibangun. Hal ini memastikan variasi kapitalisasi, diakritik, atau simbol khusus lokal tidak memengaruhi hasil pencarian. Dengan menormalkan teks pada saat pengindeksan, mesin dapat mencocokkan kueri terhadap set token yang konsisten, memberikan perilaku tidak sensitif huruf besar/kecil yang cepat dan dapat diandalkan tanpa pemrosesan tambahan pada setiap pencarian.

## Prasyarat
- **GroupDocs.Search for Java** versi 25.4 atau yang lebih baru (perpustakaan mendukung lebih dari 30 format file dan dapat mengindeks dokumen ratusan halaman tanpa memuat seluruh file ke memori).  
- **Java Development Kit (JDK)** 8 atau yang lebih baru terpasang.  
- Familiaritas dasar dengan **Maven** (atau kemampuan menambahkan JAR secara manual).  

## Menyiapkan GroupDocs.Search untuk Java

### Pengaturan Maven
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

### Unduhan Langsung
Jika Anda lebih memilih tidak menggunakan Maven, unduh JAR terbaru dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Free Trial** – unduh lisensi percobaan untuk mulai bereksperimen.  
- **Temporary License** – minta lisensi pengujian tambahan melalui portal GroupDocs.  
- **Full License** – beli lisensi produksi saat Anda siap meluncurkan.

### Inisialisasi Dasar (Buat indeks)
Cuplikan berikut membuat folder indeks dan mengaktifkan penggantian karakter:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Panduan Implementasi

### Aktifkan Penggantian Karakter dalam Pengaturan Indeks
Mengaktifkan fitur ini memberi tahu mesin untuk mengganti karakter saat mengindeks, yang merupakan langkah inti untuk perilaku tidak sensitif huruf besar/kecil.

#### Langkah 1: Konfigurasikan `IndexSettings`
`IndexSettings` adalah objek konfigurasi yang mengontrol bagaimana indeks menyimpan dan memproses teks. Dengan menyetel `useCharacterReplacements` ke **true**, Anda mengaktifkan pengubahan otomatis menjadi huruf kecil (atau pemetaan khusus apa pun yang Anda sediakan).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Konfigurasikan Penggantian Karakter
Petakan setiap karakter ke padanan huruf kecilnya (atau pemetaan khusus apa pun yang Anda perlukan).

#### Langkah 2: Definisikan dan Tambahkan Pasangan Penggantian
Kamus penggantian berisi pasangan seperti `'A' → 'a'`, `'É' → 'e'`, dll. Menambahkan pasangan ini sebelum pengindeksan memastikan setiap token dinormalkan.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Mengindeks Dokumen
Sekarang indeks sudah siap, Anda dapat **add documents to index** dari folder mana pun.

#### Langkah 3: Tambahkan Dokumen untuk Pengindeksan
GroupDocs.Search memindai direktori target, mengekstrak teks dari setiap tipe file yang didukung, menerapkan peta penggantian, dan menulis token ke penyimpanan indeks.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Lakukan Pencarian Sensitif Huruf Besar/Kecil (Opsional)

#### Langkah 4: Jalankan Pencarian Sensitif Huruf Besar/Kecil
`SearchOptions` mengonfigurasi perilaku kueri, seperti mengaktifkan atau menonaktifkan sensitivitas huruf, memungkinkan kontrol halus atas cara pencarian dilakukan.  
`SearchOptions.setUseCaseSensitiveSearch(true)` memaksa mesin memperlakukan karakter huruf besar dan kecil sebagai berbeda selama kueri tertentu, menimpa perilaku default yang tidak sensitif huruf besar/kecil.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Aplikasi Praktis
1. **Kampanye Pemasaran** – Normalisasi nama produk sehingga tim penjualan dapat menemukan aset tanpa memperhatikan huruf.  
2. **Dukungan Pelanggan** – Dukung kotak pencarian help‑desk yang mengembalikan artikel yang tepat apakah pengguna mengetik “login” atau “Login”.  
3. **Katalog E‑commerce** – Pastikan pembeli menemukan barang terlepas dari cara mereka mengetik judul produk, meningkatkan tingkat konversi.

## Pertimbangan Kinerja
- **Atur File Sumber** – Hierarki folder yang rapi mengurangi waktu pemindaian selama langkah **add documents to index**.  
- **Pantau Memori** – Pengindeksan korpus besar dapat mengonsumsi RAM signifikan; memproses file dalam batch 500 – 1 000 item menjaga penggunaan heap tetap terkendali.  
- **Pengindeksan Asinkron** – Bila didukung, jalankan pengindeksan pada thread latar belakang agar UI tetap responsif dan tidak memblokir operasi pengguna.

## Masalah Umum & Pemecahan Masalah
| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Tidak ada hasil yang dikembalikan untuk istilah yang dikenal | Penggantian karakter tidak diaktifkan | Verifikasi `settings.setUseCharacterReplacements(true)` dan pastikan peta penggantian berisi karakter yang diperlukan. |
| Kesalahan out‑of‑memory saat pengindeksan | Mengindeks terlalu banyak file besar sekaligus | Indeks dalam batch lebih kecil atau tingkatkan heap JVM (`-Xmx4g`). |
| Pencarian mengembalikan hasil sensitif huruf secara tak terduga | `SearchOptions.setUseCaseSensitiveSearch(true)` telah disetel | Hapus atau set ke `false` untuk perilaku default yang tidak sensitif huruf. |
| Waktu muat indeks melebihi harapan | Tata letak folder tidak efisien atau SSD tidak digunakan | Atur ulang file, hapus dokumen yang tidak dipakai, dan simpan indeks pada SSD cepat. |
| Karakter khusus diabaikan | Peta penggantian tidak mencakup entri Unicode | Tambahkan pemetaan untuk karakter seperti “é”, “ß”, “ø” ke padanan yang diinginkan. |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara menangani karakter khusus (mis., “é”, “ß”) selama pengindeksan?**  
J: Sertakan karakter tersebut dalam peta penggantian Anda, memetakannya ke padanan ASCII atau membiarkannya tidak berubah sesuai kebutuhan pencarian.

**T: Apakah saya dapat membatasi penggantian karakter pada bahasa tertentu?**  
J: Ya. Buat array penggantian khusus yang hanya berisi karakter untuk bahasa target sebelum menambahkannya ke kamus.

**T: Apa yang harus saya lakukan jika indeks membutuhkan waktu lama untuk dimuat?**  
J: Optimalkan struktur folder, hapus file yang tidak diperlukan, dan simpan indeks pada SSD berkecepatan tinggi. Pengindeksan inkremental juga mengurangi beban muat.

**T: Apakah memungkinkan untuk mengembalikan penggantian karakter setelah pengindeksan?**  
J: Tidak. Penggantian sudah tertanam dalam data yang diindeks; Anda harus membangun ulang indeks dengan pengaturan baru untuk mengubahnya.

**T: Di mana saya dapat menemukan dokumentasi API yang lebih detail?**  
J: Dokumen resmi dan referensi API menyediakan detail lengkap (lihat Sumber Daya di bawah).

## Sumber Daya
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/) 

---

**Terakhir Diperbarui:** 2026-07-31  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs  

## Tutorial Terkait

- [Penggantian Karakter dalam GroupDocs.Search Java: Panduan Komprehensif untuk Meningkatkan Pencarian Teks dan Pengindeksan](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Add documents to index: pencarian Java sensitif huruf dengan GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Cara Menambahkan Dokumen ke Indeks dengan GroupDocs.Search untuk Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)