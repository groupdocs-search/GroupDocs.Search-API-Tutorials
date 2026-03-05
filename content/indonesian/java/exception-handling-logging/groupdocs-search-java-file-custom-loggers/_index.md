---
date: '2026-02-24'
description: Pelajari cara membuat logger kustom, mengatur ukuran maksimum log, dan
  mengonfigurasi logger konsol atau file di GroupDocs.Search untuk Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Cara membuat logger khusus dan membatasi ukuran file log dengan GroupDocs.Search
  Java
type: docs
url: /id/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Batasi ukuran file log dengan GroupDocs.Search Java Loggers

Dalam panduan ini Anda akan **membuat implementasi logger khusus** dan mempelajari cara **membatasi ukuran file log** saat menggunakan GroupDocs.Search untuk Java. Mengontrol pertumbuhan log sangat penting untuk pengindeksan dokumen skala besar, dan logger bawaan memungkinkan Anda **mengatur ukuran maksimum log**, **memutar ulang file log**, atau beralih ke **menggunakan console logger** untuk umpan balik instan. Mari kita jalani pengaturan lengkap, mulai dari konfigurasi Maven hingga menjalankan kueri pencarian, dan lihat cara **menambahkan dokumen ke indeks** dengan logger yang sudah diatur.

## Jawaban Cepat
- **Apa arti “membatasi ukuran file log”?** Itu membatasi ukuran maksimum sebuah file log, mencegah pertumbuhan yang tidak terkendali di disk.  
- **Logger mana yang memungkinkan Anda membatasi ukuran file log?** `FileLogger` bawaan menerima parameter ukuran maksimum.  
- **Bagaimana cara menggunakan console logger java?** Buat instance `ConsoleLogger` dan setel pada `IndexSettings`.  
- **Apakah saya memerlukan lisensi untuk GroupDocs.Search?** Versi percobaan dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Langkah pertama apa?** Tambahkan dependensi GroupDocs.Search ke proyek Maven Anda.  

## Apa itu pembatasan ukuran file log?
Membatasi ukuran file log berarti mengonfigurasi logger sehingga begitu file mencapai ambang batas yang telah ditentukan (mis., 4 MB), file tersebut tidak lagi tumbuh atau diputar ulang. Hal ini membuat jejak penyimpanan aplikasi Anda dapat diprediksi dan menghindari penurunan kinerja.

## Mengapa menggunakan file dan logger khusus dengan GroupDocs.Search?
- **Auditability:** Simpan catatan permanen tentang peristiwa pengindeksan dan pencarian.  
- **Debugging:** Dengan cepat mengidentifikasi masalah dengan meninjau log yang ringkas.  
- **Flexibility:** Pilih antara log file yang persisten dan output konsol instan (`use console logger`).  

## Prasyarat
- **GroupDocs.Search for Java** ≥ 25.4.  
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
Unduh JAR terbaru dari situs resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Perolehan Lisensi
Dapatkan lisensi percobaan atau beli lisensi melalui [licensing page](https://purchase.groupdocs.com/temporary-license/).

## Cara membuat logger khusus untuk GroupDocs.Search
GroupDocs.Search memungkinkan Anda menyambungkan implementasi apa pun dari antarmuka `ILogger`. Dengan memperluas `FileLogger` atau `ConsoleLogger`, Anda dapat menambahkan perilaku ekstra—seperti memutar ulang file log atau meneruskan pesan ke layanan pemantauan jarak jauh. Fleksibilitas ini menjadi alasan mengapa banyak tim **membuat logger khusus** yang sesuai dengan kebutuhan operasional mereka.

## Cara membatasi ukuran file log dengan File Logger
Berikut panduan langkah‑demi‑langkah yang menunjukkan cara **mengonfigurasi file logger** sehingga file log tidak pernah melebihi ukuran yang Anda tentukan.

### 1️⃣ Impor Paket yang Diperlukan
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Siapkan Index Settings dengan File Logger
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

### 5️⃣ Lakukan Kueri Pencarian
```java
SearchResult result = index.search(query);
```

**Poin penting:** Argumen kedua konstruktor `FileLogger` (`4.0`) menentukan **set max log size** dalam megabyte, secara langsung memenuhi kebutuhan **limit log file size**.

## Cara menggunakan console logger java
Jika Anda lebih suka umpan balik langsung di terminal, ganti file logger dengan console logger.

### 1️⃣ Impor Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Siapkan Index Settings dengan Console Logger
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

**Tip:** Console logger ideal selama pengembangan karena mencetak setiap entri log secara instan, membantu Anda memverifikasi bahwa pengindeksan dan pencarian berfungsi sebagaimana mestinya.

## Aplikasi Praktis
1. **Document Management Systems:** Simpan jejak audit setiap dokumen yang diindeks.  
2. **Enterprise Search Engines:** Pantau kinerja kueri dan tingkat kesalahan secara real time.  
3. **Legal & Compliance Software:** Catat istilah pencarian untuk pelaporan regulasi.  

## Pertimbangan Kinerja
- **Log Size:** Dengan **set max log size**, Anda menghindari penggunaan disk berlebih yang dapat memperlambat aplikasi.  
- **Asynchronous Logging:** Jika memerlukan throughput lebih tinggi, pertimbangkan membungkus logger dalam antrian async (di luar cakupan panduan ini).  
- **Memory Management:** Lepaskan objek `Index` yang besar ketika tidak lagi diperlukan untuk menjaga jejak memori JVM tetap rendah.

## Masalah Umum & Solusi
- **Log path not accessible:** Verifikasi direktori ada dan aplikasi memiliki izin menulis.  
- **Logger not firing:** Pastikan Anda memanggil `settings.setLogger(...)` *sebelum* membuat objek `Index`.  
- **Console output missing:** Pastikan Anda menjalankan aplikasi di terminal yang menampilkan `System.out`.

## Pertanyaan yang Sering Diajukan

**Q: Apa yang dikontrol oleh parameter kedua `FileLogger`?**  
A: Itu menetapkan ukuran maksimum file log dalam megabyte, memungkinkan Anda **set max log size**.

**Q: Bisakah saya menggabungkan file dan console logger?**  
A: Ya, dengan membuat logger khusus yang meneruskan pesan ke kedua tujuan.

**Q: Bagaimana cara menambahkan dokumen ke indeks setelah pembuatan awal?**  
A: Panggil `index.add(pathToNewDocs)` kapan saja; logger akan mencatat operasi tersebut.

**Q: Apakah `ConsoleLogger` thread‑safe?**  
A: Ia menulis langsung ke `System.out`, yang disinkronkan oleh JVM, sehingga aman untuk kebanyakan kasus penggunaan.

**Q: Apakah membatasi ukuran file log memengaruhi jumlah informasi yang disimpan?**  
A: Setelah batas ukuran tercapai, entri baru mungkin dibuang atau file dapat **roll over log file**, tergantung pada implementasi logger.

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/search/java/)
- [Referensi API](https://reference.groupdocs.com/search/java/)

---

**Terakhir Diperbarui:** 2026-02-24  
**Diuji Dengan:** GroupDocs.Search for Java 25.4  
**Penulis:** GroupDocs