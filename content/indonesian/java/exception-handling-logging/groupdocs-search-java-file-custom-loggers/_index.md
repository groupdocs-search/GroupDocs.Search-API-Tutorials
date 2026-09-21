---
date: '2026-09-21'
description: Pelajari cara membuat logger, mengatur ukuran maksimum log, dan menggunakan
  console logger di GroupDocs.Search untuk Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Pelajari cara membuat logger, mengatur ukuran maksimum log, dan menggunakan
  console logger di GroupDocs.Search untuk Java. Ikuti petunjuk langkah‑by‑step dan
  tips best‑practice.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Cara membuat logger dan membatasi ukuran log di GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Cara membuat logger dan membatasi ukuran log di GroupDocs.Search untuk Java
type: docs
url: /id/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Cara membuat logger dan membatasi ukuran file log di GroupDocs.Search untuk Java

Dalam tutorial ini Anda akan **cara membuat logger** implementasi untuk GroupDocs.Search, mengonfigurasi ukuran maksimum file log, dan beralih antara logging berbasis file dan konsol. Manajemen log yang tepat mencegah disk penuh selama pekerjaan pengindeksan besar, meningkatkan pemecahan masalah, dan memberi Anda umpan balik instan saat mengembangkan. Kami akan memulai dengan pengaturan Maven, menelusuri konfigurasi logger, dan mengakhiri dengan kueri pencarian sederhana yang menunjukkan logger beraksi.

## Jawaban Cepat
- **Apa arti “limit log file size”?** Itu membatasi ukuran maksimum file log, mencegah pertumbuhan yang tidak terkendali di disk.  
- **Logger mana yang memungkinkan Anda membatasi ukuran file log?** `FileLogger` bawaan menerima parameter ukuran maksimum.  
- **Bagaimana cara menggunakan console logger java?** Buat instance `ConsoleLogger` dan setel pada `IndexSettings`.  
- **Apakah saya memerlukan lisensi untuk GroupDocs.Search?** Versi percobaan dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Langkah pertama apa?** Tambahkan dependensi GroupDocs.Search ke proyek Maven Anda.  

## Apa itu limit log file size?
Pengaturan **limit log file size** memberi tahu logger untuk berhenti menulis entri baru setelah file mencapai ambang batas yang ditentukan (misalnya, 4 MB). Ketika batas tercapai, logger akan membuang pesan selanjutnya atau membuat file baru, sehingga penggunaan disk menjadi dapat diprediksi.

## Mengapa menggunakan file dan custom logger dengan GroupDocs.Search?
File dan custom logger memberikan auditabilitas, wawasan debugging, dan fleksibilitas. Di lingkungan produksi, log file menyediakan catatan permanen setiap operasi pengindeksan dan pencarian, sementara log konsol memberikan umpan balik instan selama pengembangan. Log ini membantu tim memantau kinerja, melacak kesalahan, dan memenuhi persyaratan kepatuhan dengan menyimpan jejak aktivitas yang detail.

## Prasyarat
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 atau lebih baru, dengan IDE seperti IntelliJ IDEA atau Eclipse.  
- Pemahaman dasar tentang Maven dan pemrograman Java.  

## Menyiapkan GroupDocs.Search untuk Java

Tambahkan pustaka ke proyek Anda menggunakan salah satu metode di bawah ini.

**Pengaturan Maven:**  

```text
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
```

**Unduh langsung:**  
Unduh JAR terbaru dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Perolehan Lisensi
Dapatkan versi percobaan atau beli lisensi melalui [halaman lisensi](https://purchase.groupdocs.com/temporary-license/).

## Cara membuat custom logger untuk GroupDocs.Search
Membuat custom logger cukup sederhana karena GroupDocs.Search bergantung pada antarmuka `ILogger`. Dengan mengimplementasikan antarmuka ini—atau dengan memperluas `FileLogger` atau `ConsoleLogger` yang disediakan—Anda dapat menyuntikkan perilaku tambahan seperti penerusan jarak jauh atau rotasi log. Anda juga dapat menambahkan logika inisialisasi, seperti membuka koneksi jaringan, dan memastikan sumber daya ditutup dalam metode shutdown logger. Pendekatan ini memungkinkan Anda mengintegrasikan dengan platform pemantauan seperti ELK atau Splunk.

### Anchor definisi
`ILogger` adalah kontrak logging inti di GroupDocs.Search; setiap kelas yang mengimplementasikan metode `log(Level, String)`-nya dapat menjadi logger.

### Contoh pendekatan (tanpa blok kode)
1. Buat kelas yang mengimplementasikan `ILogger`.  
2. Override metode `log` untuk menulis pesan ke tujuan pilihan Anda (file, basis data, endpoint HTTP).  
3. Dalam konfigurasi indeks, panggil `settings.setLogger(new YourCustomLogger())`.  

## Cara membatasi ukuran file log dengan File Logger
`FileLogger` menulis entri log ke file di disk dan menerima argumen ukuran maksimum. Dengan menentukan batas ukuran, logger secara otomatis berhenti menambahkan entri baru atau membuat file baru ketika ambang tercapai, mencegah pertumbuhan disk yang tidak terkendali. Perilaku ini memastikan logging tidak mengganggu kinerja pengindeksan sambil menjaga catatan peristiwa yang ringkas.

### Anchor definisi
`FileLogger` adalah logger bawaan yang menyimpan pesan ke file teks dan mendukung ukuran file maksimum yang dapat dikonfigurasi.

### Panduan langkah‑demi‑langkah
1️⃣ **Impor paket yang diperlukan**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Siapkan pengaturan indeks dengan File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Buat atau muat indeks**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Tambahkan dokumen ke indeks**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Lakukan kueri pencarian**  
```text
```java
SearchResult result = index.search(query);
```
```

**Poin penting:** Argumen kedua konstruktor `FileLogger` (`4.0`) menentukan **set max log size** dalam megabyte, secara langsung memenuhi kebutuhan **limit log file size**.

## Cara menggunakan console logger java
Ketika Anda membutuhkan visibilitas instan dari peristiwa log, `ConsoleLogger` menulis setiap pesan ke `System.out`. Logger ini ringan dan thread‑safe, sehingga cocok untuk sesi pengembangan dan debugging. Ia memberikan umpan balik langsung tentang kemajuan pengindeksan, kueri pencarian, dan kondisi error tanpa memerlukan I/O file, yang dapat mempercepat pengujian iteratif.

### Anchor definisi
`ConsoleLogger` adalah logger ringan yang mengeluarkan entri log ke aliran konsol standar, menjadikannya ideal untuk sesi debugging.

### Langkah konfigurasi
1️⃣ **Impor console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Siapkan pengaturan indeks dengan Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Buat atau muat indeks**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Tambahkan dokumen dan lakukan pencarian**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Tip:** Console logger ideal selama pengembangan karena mencetak setiap entri log secara instan, membantu Anda memverifikasi bahwa pengindeksan dan pencarian berperilaku sesuai harapan.

## Aplikasi praktis
1. **Sistem manajemen dokumen:** Menjaga jejak audit setiap dokumen yang diindeks, memenuhi persyaratan kepatuhan.  
2. **Mesin pencarian perusahaan:** Memantau kinerja kueri dan tingkat error secara real time, memungkinkan pemeriksaan kepatuhan SLA yang cepat.  
3. **Perangkat lunak hukum & kepatuhan:** Mencatat istilah pencarian dan cap waktu untuk pelaporan regulasi, dengan log disimpan selama periode retensi yang diwajibkan.

## Pertimbangan kinerja
- **Ukuran log:** Dengan **set max log size**, Anda menghindari penggunaan disk berlebih yang dapat memperlambat garbage collector JVM.  
- **Logging asynchronous:** Untuk skenario throughput tinggi, bungkus logger Anda dalam antrian asynchronous untuk memisahkan I/O dari thread pengindeksan (implementasi di luar cakupan panduan ini).  
- **Manajemen memori:** Lepaskan objek `Index` besar dengan `index.close()` ketika tidak lagi diperlukan untuk menjaga jejak memori JVM tetap rendah.

## Masalah umum & solusi
- **Path log tidak dapat diakses:** Pastikan direktori ada dan aplikasi memiliki izin menulis untuk akun pengguna yang menjalankan JVM.  
- **Logger tidak aktif:** Pastikan Anda memanggil `settings.setLogger(...)` *sebelum* membuat objek `Index`; jika tidak, logger default yang digunakan.  
- **Output konsol tidak muncul:** Pastikan Anda menjalankan aplikasi di terminal yang menampilkan `System.out`, dan tidak ada kerangka kerja logging (misalnya, SLF4J) yang menyaring output.

## Pertanyaan yang sering diajukan

**Q: Apa yang dikontrol oleh parameter kedua `FileLogger`?**  
A: Itu menentukan ukuran maksimum file log dalam megabyte, memungkinkan Anda **set max log size** dan mencegah pertumbuhan yang tidak terkendali.

**Q: Bisakah saya menggabungkan file dan console logger?**  
A: Ya. Buat custom logger yang meneruskan setiap panggilan `log` ke both `FileLogger` dan `ConsoleLogger`, lalu daftarkan logger komposit tersebut dengan `IndexSettings`.

**Q: Bagaimana cara menambahkan dokumen ke indeks setelah pembuatan awal?**  
A: Panggil `index.add(pathToNewDocs)` kapan saja; logger yang dikonfigurasi akan secara otomatis mencatat penambahan tersebut.

**Q: Apakah `ConsoleLogger` thread‑safe?**  
A: Ia menulis langsung ke `System.out`, yang disinkronkan secara internal oleh JVM, sehingga aman untuk kasus penggunaan multi‑threaded umum.

**Q: Apakah membatasi ukuran file log akan memengaruhi jumlah informasi yang disimpan?**  
A: Setelah batas ukuran tercapai, entri baru akan dibuang atau logger akan beralih ke file baru, tergantung pada implementasi yang Anda pilih.

## Sumber daya
- [Dokumentasi](https://docs.groupdocs.com/search/java/)
- [Referensi API](https://reference.groupdocs.com/search/java/)

---

**Terakhir Diperbarui:** 2026-09-21  
**Diuji Dengan:** GroupDocs.Search for Java 25.4  
**Penulis:** GroupDocs  

---

## Tutorial Terkait

- [Cara Menerapkan Logging - Tutorial Penanganan Pengecualian dan Logging untuk GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Menerapkan Logging Asynchronous di Java dengan GroupDocs.Search – Panduan Custom Logger](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Buat Indeks Pencarian Java – Tutorial GroupDocs.Search](/search/java/indexing/)