---
date: '2026-10-17'
description: Pelajari cara menggunakan sinonim di Java dengan GroupDocs.Search, mengimpor
  kamus sinonim, mengelola grup sinonim, dan mengoptimalkan indeks pencarian Anda
  untuk relevansi yang lebih baik.
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: Pelajari cara menggunakan sinonim di Java dengan GroupDocs.Search,
  mengimpor kamus sinonim, mengelola grup sinonim, dan mengoptimalkan indeks pencarian
  Anda untuk relevansi yang lebih baik.
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: Cara menggunakan sinonim di Java dengan GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: Cara menggunakan sinonim di Java dengan GroupDocs.Search
type: docs
url: /id/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

# Cara menggunakan sinonim di Java dengan GroupDocs.Search

Jika Anda ingin pengguna menemukan konten yang tepat bahkan ketika mereka mengetik kata yang berbeda, **search with synonyms** adalah jawabannya. Dalam panduan ini Anda akan belajar cara membuat kamus sinonim, mengimpor atau mengekspornya, mengelola grup sinonim, dan menjalankan pencarian yang secara otomatis memperluas kueri menggunakan sinonim tersebut. Baik Anda membangun CMS, katalog e‑commerce, atau repositori dokumen hukum, menambahkan dukungan sinonim dapat secara dramatis meningkatkan relevansi dan tingkat konversi.

## Jawaban cepat
- **Apa langkah pertama untuk menambahkan sinonim?** Create an `Index` instance and work with the `SynonymDictionary` API.  
- **Bisakah saya mengimpor kamus sinonim yang sudah jadi?** Yes – call `importDictionary(path)` with the file location.  
- **Bagaimana cara mengaktifkan pencarian yang sadar sinonim?** Enable `SearchOptions.setUseSynonymSearch(true)`.  
- **Apakah memungkinkan mengedit grup sinonim saat runtime?** Absolutely – you can clear, add, or retrieve groups via the dictionary API.  
- **Apa yang harus saya pantau saat memperbesar indeks?** Regularly prune unused entries and tune the JVM heap for large synonym files.

## Apa itu search with synonyms?
**Search with synonyms** berarti mesin memperlakukan sekumpulan kata atau frasa sebagai dapat dipertukarkan. Ketika pengguna mengetik **“better”**, mesin juga mencari **“improve”**, **“enhance”**, atau istilah lain yang Anda definisikan dalam grup sinonim yang sama, memberikan hasil yang lebih kaya tanpa mengubah kueri pengguna.

## Mengapa mengaktifkan dukungan sinonim di GroupDocs.Search?
Mengaktifkan dukungan sinonim memungkinkan mesin secara otomatis memperluas kueri untuk menyertakan istilah yang setara, yang meningkatkan relevansi hasil, meningkatkan kepuasan pengguna, dan dapat meningkatkan tingkat konversi untuk situs e‑commerce atau berbasis konten. Ini juga memusatkan manajemen terminologi, mengurangi beban pemeliharaan di banyak aplikasi.

## Prasyarat
- GroupDocs.Search for Java versi **25.4** atau lebih baru.  
- IDE Java (IntelliJ IDEA, Eclipse, dll.) dengan dukungan Maven.  
- Pengetahuan dasar Java dan familiaritas dengan struktur proyek Maven.

### Perpustakaan dan versi yang diperlukan
- GroupDocs.Search for Java **25.4** atau lebih tinggi.

### Pengaturan lingkungan
- IDE pilihan Anda (IntelliJ IDEA, Eclipse, dll.).  
- Maven untuk manajemen dependensi.

### Persyaratan pengetahuan
- Pemrograman berorientasi objek di Java.  
- Operasi file I/O dasar.

## Menyiapkan GroupDocs.Search untuk Java

### Informasi instalasi
Add the repository and dependency to your `pom.xml`:

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

**Direct download** – Anda juga dapat mengunduh JAR terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Perolehan lisensi
- **Free trial:** Uji fitur inti tanpa lisensi.  
- **Temporary license:** Perpanjang kemampuan percobaan selama evaluasi.  
- **Purchase:** Diperlukan untuk penggunaan produksi dan set fitur lengkap.

#### Inisialisasi dan pengaturan dasar
Create an `Index` instance, then add documents to be searchable:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## Cara menambahkan sinonim ke indeks pencarian Anda

### Fitur 1: membuat dan mengindeks sebuah indeks
The `Index` class represents a searchable collection of documents stored on disk or in memory.  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### Fitur 2: mengambil sinonim untuk sebuah kata
`SynonymDictionary` manages synonym groups and provides methods to query synonyms for a term.  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Fitur 3: mengambil grup sinonim
`SynonymDictionary.getGroups()` returns a list of all defined synonym groups with their identifiers.  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### Fitur 4: mengelola entri kamus sinonim
`add(word, synonym)` inserts a new synonym relationship into the dictionary. `clear()` removes all entries, and `remove(word)` deletes a specific term from the dictionary.  

```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### Fitur 5: mengekspor sinonim ke file
`exportDictionary(path)` writes the current synonym dictionary to a binary .dat file at the specified location.  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### Fitur 6: mengimpor sinonim dari file
`importDictionary(path)` loads a previously exported .dat file into the synonym dictionary.  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### Fitur 7: melakukan pencarian dengan dukungan sinonim
`SearchOptions` configures query behavior, including whether synonym expansion is enabled. `setUseSynonymSearch(true)` turns on synonym‑aware searching for the upcoming query.  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## Cara mencari dengan sinonim
Load your `Index`, enable synonym search, and execute a query. The engine automatically expands the query using the synonym dictionary you built or imported, returning matches for all related terms.

## Cara mengimpor kamus sinonim
If you already have a `.dat` file prepared by another environment, simply call `importDictionary(path)`. This is ideal for synchronizing dictionaries across development, staging, and production servers.

## Cara mengelola grup sinonim
Synonym groups let you treat a set of terms as a single logical entity. Adding, clearing, or retrieving groups is done through the `SynonymDictionary` API, as shown in the code snippets above.

## Cara mengoptimalkan indeks pencarian
- **Regularly prune unused entries:** Gunakan `clear()` sebelum pembaruan massal.  
- **Adjust JVM heap:** Kamus besar mungkin memerlukan lebih banyak memori; tingkatkan parameter `-Xmx` sesuai.  
- **Keep the library up‑to‑date:** Rilis baru berisi perbaikan kinerja dan perbaikan bug.

## Aplikasi praktis
1. **Content management systems (CMS):** Pengguna menemukan artikel bahkan ketika mereka menggunakan terminologi alternatif.  
2. **E‑commerce platforms:** Pencarian produk menjadi toleran terhadap sinonim seperti “laptop” vs. “notebook”.  
3. **Document repositories:** Arsip hukum atau medis mendapat manfaat dari grup sinonim khusus domain, meningkatkan kemampuan penemuan bagi profesional.

## Pertimbangan kinerja
- **Optimize index storage:** Secara berkala bangun kembali indeks untuk menghapus data usang.  
- **Manage memory usage:** Pantau konsumsi heap saat memuat file sinonim besar; kamus 500 MB biasanya memerlukan heap 2 GB pada JVM 64‑bit.  
- **Regular updates:** Tetap gunakan versi GroupDocs.Search terbaru untuk perbaikan bug dan peningkatan kecepatan.

## Masalah umum dan solusi
| Issue | Likely cause | Fix |
|-------|--------------|-----|
| Tidak ada hasil sinonim yang muncul | `setUseSynonymSearch(true)` tidak diatur atau kamus tidak diimpor | Verifikasi opsi diaktifkan dan file kamus ada. |
| Kesalahan out‑of‑memory saat impor | File `.dat` yang sangat besar melebihi heap JVM | Tingkatkan ukuran heap `-Xmx` atau impor dalam batch yang lebih kecil. |
| Entri duplikat dalam hasil | Istilah yang sama muncul di beberapa grup sinonim | Konsolidasikan grup yang tumpang tindih menggunakan `clear()` lalu `addRange()`. |

## Pertanyaan yang sering diajukan

**Q: Apa persyaratan sistem minimum untuk menggunakan GroupDocs.Search?**  
A: Sistem operasi modern apa pun dengan JDK yang kompatibel (Java 8 atau lebih baru) sudah cukup.

**Q: Seberapa sering saya harus memperbarui kamus sinonim saya?**  
A: Perbarui setiap kali terminologi baru muncul—gunakan `clear()` diikuti `addRange()` untuk penyegaran bersih.

**Q: Bisakah saya menjalankan GroupDocs.Search tanpa membeli lisensi?**  
A: Versi percobaan gratis berfungsi untuk evaluasi, tetapi lisensi diperlukan untuk penerapan produksi.

**Q: Apa praktik terbaik untuk mengindeks kumpulan data besar?**  
A: Bagi data menjadi batch logis, pantau penggunaan heap, dan jadwalkan pemeliharaan indeks secara rutin.

**Q: Saya tidak melihat hasil sinonim yang diharapkan—apa yang harus saya periksa?**  
A: Verifikasi bahwa kamus telah diimpor dengan benar, bahwa `setUseSynonymSearch(true)` aktif, dan bahwa istilah ada dalam grup sinonim.

**Sumber daya**  
- [Dokumentasi](https://docs.groupdocs.com/search/java/)  
- [Referensi API](https://reference.groupdocs.com/search/java)  
- [Unduh GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/)  
- [Repositori GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/search/10)  
- [Perolehan Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/) 

---

**Terakhir Diperbarui:** 2026-10-17  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Buat Kelola Indeks Groupdocs Search Java](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Perpustakaan Pencarian Teks Penuh Java – Optimalkan Indeks dengan GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Pencarian Fuzzy Java: Tambahkan Dokumen ke Indeks dengan GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)
