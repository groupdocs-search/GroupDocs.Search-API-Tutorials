---
date: '2026-01-26'
description: Pelajari cara mencari frasa menggunakan pola wildcard di GroupDocs.Search
  untuk Java. Panduan ini mencakup pembuatan indeks pencarian, menambahkan dokumen
  ke indeks, dan melakukan pencarian wildcard di Java.
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: Cara Mencari Frasa dengan Wildcard di GroupDocs.Search Java
type: docs
url: /id/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Cara Mencari Frasa dengan Wildcard di GroupDocs.Search for Java

Di dunia manajemen dokumen yang bergerak cepat saat ini, **cara mencari frasa** secara efisien dapat menentukan keberhasilan kegunaan aplikasi. Baik Anda membangun sistem manajemen konten, katalog e‑commerce, atau repositori dokumen hukum, kemampuan menemukan frasa tepat—atau variasi fleksibel darinya—sangat penting. Dalam tutorial ini kami akan menjelaskan cara menyiapkan **GroupDocs.Search for Java**, membuat indeks pencarian, menambahkan dokumen ke indeks, dan menguasai pencarian frasa sederhana serta teknik pencarian wildcard Java yang kuat.

## Jawaban Cepat
- **Apa manfaat utama pencarian frasa?** Pencocokan tepat urutan kata dan kedekatannya.  
- **Apakah wildcard dapat digunakan di dalam frasa?** Ya, Anda dapat menggabungkan wildcard dengan kata tepat untuk pencocokan fleksibel.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis cukup untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Versi Maven mana yang harus saya gunakan?** Rilis terbaru GroupDocs.Search for Java (misalnya, 25.4 pada saat penulisan).  
- **Apakah pendekatan ini cocok untuk kumpulan dokumen besar?** Tentu—jaga indeks tetap dioptimalkan dan gunakan pola wildcard yang ditargetkan.

## Apa itu “cara mencari frasa”?
Mencari sebuah frasa berarti mencari urutan kata tertentu dalam sebuah dokumen. Ketika Anda menambahkan wildcard, Anda memungkinkan mesin pencari untuk melewatkan atau mengganti kata, memberi fleksibilitas untuk mencocokkan variasi tanpa mengorbankan relevansi.

## Mengapa Menggunakan GroupDocs.Search untuk Kuiri Frasa dan Wildcard?
- **Kinerja tinggi** pada koleksi besar berkat indeks terbalik yang dioptimalkan.  
- **Bahasa kuiri kaya** yang mendukung frasa tepat, wildcard sederhana, dan pola lanjutan.  
- **Integrasi mudah** dengan aplikasi berbasis Java apa pun melalui Maven atau unduhan langsung.  

## Prasyarat
- Java 8 atau yang lebih baru terpasang.  
- Maven 3 atau lebih baru (jika Anda lebih suka manajemen dependensi Maven).  
- Familiaritas dasar dengan sintaks Java dan struktur proyek.  

## Menyiapkan GroupDocs.Search untuk Java

### Menggunakan Maven
Add the repository and dependency to your `pom.xml` file:

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
Alternatively, download the latest JAR from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
- **Percobaan Gratis:** Ideal untuk percobaan cepat.  
- **Lisensi Sementara:** Minta melalui portal GroupDocs untuk pengujian yang diperpanjang.  
- **Pembelian Penuh:** Disarankan untuk penerapan produksi.

### Inisialisasi dan Penyiapan Dasar
Create a folder for the index and initialize it:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

Add the documents you want to make searchable:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## Cara Mencari Frasa dengan Wildcard di GroupDocs.Search
Berikut kami uraikan tiga skenario progresif: pencarian frasa tepat, penggunaan wildcard sederhana, dan pola wildcard lanjutan.

### Pencarian Frasa Sederhana

#### Gambaran Umum
Gunakan ini ketika Anda memerlukan kecocokan tepat urutan kata.

##### Langkah 1: Buat Indeks
```java
Index index = new Index(indexFolder);
```

##### Langkah 2: Tambahkan Dokumen ke Indeks
```java
index.add(documentsFolder);
```

##### Langkah 3: Cari Frasa Spesifik (Bentuk Teks)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Langkah 4: Kuiri Berbasis Objek (Cari Frasa Tepat)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Pencarian Frasa dengan Wildcard

#### Gambaran Umum
Placeholder wildcard memungkinkan Anda melewatkan sejumlah kata variabel di antara istilah tepat.

##### Langkah 1: Buat Indeks
*(Sama seperti langkah Pencarian Frasa Sederhana.)*

##### Langkah 2: Tambahkan Dokumen ke Indeks
*(Sama seperti di atas.)*

##### Langkah 3: Pencarian Bentuk Teks dengan Wildcard
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Langkah 4: Kuiri Berbasis Objek dengan Wildcard (Wildcard Search Java)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Pencarian Wildcard Lanjutan

#### Gambaran Umum
Gabungkan rentang numerik, karakter opsional, dan pola khusus untuk pencocokan yang canggih.

##### Langkah 1: Buat Indeks
*(Diulang untuk kejelasan.)*

##### Langkah 2: Tambahkan Dokumen ke Indeks
*(Diulang.)*

##### Langkah 3: Pencarian Bentuk Teks dengan Pola Wildcard Kompleks
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### Langkah 4: Kuiri Berbasis Objek dengan Wildcard Lanjutan
```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Aplikasi Praktis
- **Sistem Manajemen Konten:** Memungkinkan editor menemukan klausa tepat atau kutipan fleksibel.  
- **Katalog E‑commerce:** Membiarkan pembeli menemukan produk meskipun mereka melewatkan kata atau menggunakan sinonim.  
- **Legal & Kepatuhan:** Dengan cepat mengisolasi bahasa kontrak yang mungkin muncul dengan variasi kecil.

## Pertimbangan Kinerja
- **Buat Indeks Pencarian** hanya sekali per set dokumen, lalu gunakan kembali.  
- **Tambahkan Dokumen ke Indeks** secara inkremental ketika file baru datang—jangan membangun ulang seluruh indeks setiap kali.  
- Gunakan **pola wildcard yang tepat** untuk menghindari pemindaian yang tidak perlu; pola yang lebih luas meningkatkan beban CPU.  
- Secara periodik panggil `index.optimize()` (jika tersedia) untuk menjaga penggunaan memori tetap rendah.

## Masalah Umum & Solusi

| Masalah | Solusi |
|-------|----------|
| Tidak ada hasil yang dikembalikan untuk kuiri wildcard | Verifikasi sintaks wildcard (`*min~~max`) dan pastikan kata-kata ada dalam jarak yang ditentukan. |
| Indeks menjadi usang setelah pembaruan file | Jalankan kembali `index.add(updatedFolder)` atau gunakan API pembaruan inkremental. |
| Konsumsi memori tinggi pada dataset besar | Tingkatkan ukuran heap JVM dan pertimbangkan membagi indeks menjadi beberapa shard. |

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara wildcard dan pencarian frasa?**  
A: Pencarian frasa mencari urutan kata yang tepat, sementara wildcard memungkinkan Anda mengganti atau melewatkan kata dalam urutan tersebut.

**Q: Bisakah saya menggunakan wildcard dengan data numerik dalam pencarian?**  
A: Ya, parameter rentang wildcard berfungsi dengan angka maupun kata.

**Q: Bagaimana cara menangani koleksi dokumen yang sangat besar?**  
A: Jaga indeks tetap dioptimalkan, gunakan pembaruan inkremental, dan rancang pola wildcard Anda sespesifik mungkin.

**Q: Apakah GroupDocs.Search cocok untuk skenario pencarian waktu‑nyata?**  
A: Tentu—setelah indeks dibangun, kuiri dijalankan dalam milidetik, menjadikannya cocok untuk aplikasi interaktif.

**Q: Bisakah saya mengintegrasikan pustaka ini ke dalam proyek Java yang ada?**  
A: Ya. Tambahkan dependensi Maven atau JAR, inisialisasi indeks seperti yang ditunjukkan, dan Anda siap melanjutkan.

---

**Terakhir Diperbarui:** 2026-01-26  
**Diuji Dengan:** GroupDocs.Search 25.4 for Java  
**Penulis:** GroupDocs