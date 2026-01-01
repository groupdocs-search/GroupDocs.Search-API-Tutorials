---
date: '2025-12-24'
description: Pelajari cara membatasi ukuran file log dan menggunakan console logger
  java dengan GroupDocs.Search untuk Java. Panduan ini mencakup konfigurasi logging,
  tips pemecahan masalah, dan optimasi kinerja.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Batasi ukuran file log dengan Logger GroupDocs.Search Java
type: docs
url: /id/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Batasi ukuran file log dengan GroupDocs.Search Java Loggers

Pencatatan yang efisien sangat penting saat mengelola koleksi dokumen besar, terutama ketika Anda perlu **membatasi ukuran file log** agar penyimpanan tetap terkendali. **GroupDocs.Search untuk Java** menawarkan solusi kuat untuk menangani log melalui kemampuan pencarian yang kuat. Tutorial ini memandu Anda dalam mengimplementasikan file logger dan custom logger menggunakan GroupDocs.Search, meningkatkan kemampuan aplikasi Anda untuk melacak peristiwa dan men-debug masalah.

## Jawaban Cepat
- **Apa arti “membatasi ukuran file log”?** Itu membatasi ukuran maksimum sebuah file log, mencegah pertumbuhan tak terkendali di disk.  
- **Logger mana yang memungkinkan Anda membatasi ukuran file log?** `FileLogger` bawaan menerima parameter ukuran maksimum.  
- **Bagaimana cara menggunakan console logger java?** Buat instance `ConsoleLogger` dan tetapkan pada `IndexSettings`.  
- **Apakah saya memerlukan lisensi untuk GroupDocs.Search?** Versi percobaan dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Langkah pertama apa?** Tambahkan dependensi GroupDocs.Search ke proyek Maven Anda.

## Apa itu membatasi ukuran file log?
Membatasi ukuran file log berarti mengonfigurasi logger sehingga setelah file mencapai ambang batas yang telah ditentukan (misalnya, 4 MB), file tersebut tidak lagi tumbuh atau melakukan rollover. Hal ini menjaga jejak penyimpanan aplikasi Anda tetap dapat diprediksi dan menghindari penurunan kinerja.

## Mengapa menggunakan file dan custom logger dengan GroupDocs.Search?
- **Auditabilitas:** Simpan catatan permanen tentang peristiwa pengindeksan dan pencarian.  
- **Debugging:** Cepat mengidentifikasi masalah dengan meninjau log yang ringkas.  
- **Fleksibilitas:** Pilih antara log file yang persisten dan output konsol instan (`use console logger java`).  

## Prasyarat
- **GroupDocs.Search untuk Java** ≥ 25.4.  
- JDK 8 atau lebih baru, IDE (IntelliJ IDEA, Eclipse, dll.).  
- Pengetahuan dasar tentang Java dan Maven.  

## Menyiapkan GroupDocs.Search untuk Java

Tambahkan pustaka ke proyek Anda menggunakan salah satu metode di bawah ini.

**Pengaturan Maven:**

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

**Unduhan Langsung:**  
Unduh JAR terbaru dari situs resmi: [rilisan GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/).

### Akuisisi Lisensi
Dapatkan lisensi percobaan atau beli lisensi melalui [halaman lisensi](https://purchase.groupdocs.com/temporary-license/).

## Cara membatasi ukuran file log dengan File Logger
Berikut panduan langkah‑demi‑langkah yang menunjukkan cara mengonfigurasi `FileLogger` sehingga file log tidak pernah melebihi ukuran yang Anda tentukan.

### 1️⃣ Impor Paket yang Diperlukan
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Atur Index Settings dengan File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Buat atau Muat Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Tambahkan Dokumen ke Index
```java
index.add(documentsFolder);
```

### 5️⃣ Lakukan Query Pencarian
```java
SearchResult result = index.search(query);
```

**Poin penting:** Argumen kedua konstruktor `FileLogger` (`4.0`) menentukan ukuran maksimum file log dalam megabyte, secara langsung memenuhi kebutuhan **membatasi ukuran file log**.

## Cara menggunakan console logger java
Jika Anda lebih suka umpan balik langsung di terminal, ganti file logger dengan console logger.

### 1️⃣ Impor Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Atur Index Settings dengan Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Buat atau Muat Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Tambahkan Dokumen dan Lakukan Pencarian
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** Console logger ideal selama pengembangan karena mencetak setiap entri log secara langsung, membantu Anda memverifikasi bahwa pengindeksan dan pencarian berfungsi seperti yang diharapkan.

## Aplikasi Praktis
1. **Sistem Manajemen Dokumen:** Simpan jejak audit setiap dokumen yang diindeks.  
2. **Mesin Pencarian Enterprise:** Pantau kinerja kueri dan tingkat kesalahan secara real time.  
3. **Perangkat Lunak Hukum & Kepatuhan:** Catat istilah pencarian untuk pelaporan regulasi.

## Pertimbangan Kinerja
- **Ukuran Log:** Dengan membatasi ukuran file log, Anda menghindari penggunaan disk berlebih yang dapat memperlambat aplikasi.  
- **Logging Asinkron:** Jika Anda memerlukan throughput lebih tinggi, pertimbangkan membungkus logger dalam antrian async (di luar cakupan panduan ini).  
- **Manajemen Memori:** Lepaskan objek `Index` yang besar ketika tidak lagi diperlukan untuk menjaga jejak memori JVM tetap rendah.

## Masalah Umum & Solusi
- **Path log tidak dapat diakses:** Pastikan direktori ada dan aplikasi memiliki izin menulis.  
- **Logger tidak berjalan:** Pastikan Anda memanggil `settings.setLogger(...)` *sebelum* membuat objek `Index`.  
- **Output konsol tidak muncul:** Pastikan Anda menjalankan aplikasi di terminal yang menampilkan `System.out`.

## Pertanyaan yang Sering Diajukan

**T: Apa yang dikontrol oleh parameter kedua `FileLogger`?**  
J: Itu menentukan ukuran maksimum file log dalam megabyte, memungkinkan Anda membatasi ukuran file log.

**T: Bisakah saya menggabungkan file dan console logger?**  
J: Ya, dengan membuat custom logger yang meneruskan pesan ke kedua tujuan.

**T: Bagaimana cara menambahkan dokumen ke indeks setelah pembuatan awal?**  
J: Panggil `index.add(pathToNewDocs)` kapan saja; logger akan mencatat operasi tersebut.

**T: Apakah `ConsoleLogger` thread‑safe?**  
J: Ia menulis langsung ke `System.out`, yang disinkronkan oleh JVM, sehingga aman untuk kebanyakan kasus penggunaan.

**T: Apakah membatasi ukuran file log memengaruhi jumlah informasi yang disimpan?**  
J: Setelah batas ukuran tercapai, entri baru mungkin dibuang atau file dapat melakukan rollover, tergantung pada implementasi logger.

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/search/java/)
- [Referensi API](https://reference.groupdocs.com/search/java/)

---

**Terakhir Diperbarui:** 2025-12-24  
**Diuji Dengan:** GroupDocs.Search untuk Java 25.4  
**Penulis:** GroupDocs