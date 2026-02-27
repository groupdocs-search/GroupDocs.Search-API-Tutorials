---
date: '2026-01-14'
description: Pelajari cara membuat indeks Java dan mengekstrak teks Java secara efisien
  menggunakan GroupDocs.Search untuk Java. Optimalkan pencarian dokumen, output teks
  ke file, dan tangani ekstraksi teks terstruktur.
keywords:
- GroupDocs.Search for Java
- efficient document search
- index creation in Java
title: Cara membuat indeks Java dengan GroupDocs.Search untuk Java
type: docs
url: /id/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# Menguasai Pencarian Dokumen Efisien dengan GroupDocs.Search untuk Java

Dalam dunia manajemen dokumen, menemukan konten spesifik di antara banyak dokumen dengan cepat sangat penting. Baik Anda mengelola kontrak hukum maupun makalah akademik, kemampuan **create index java** dapat menghemat jam kerja manual. Tutorial ini membahas penggunaan **GroupDocs.Search for Java**, sebuah **java search library** yang kuat yang membantu Anda membuat indeks, **add documents to index**, dan **extract text java** dari file secara efisien. Pada akhir panduan ini, Anda akan tahu cara menyiapkan pengindeksan dengan pengaturan khusus dan mengeluarkan teks dokumen dalam berbagai format, termasuk ekstraksi teks terstruktur.

## Jawaban Cepat
- **Apa tujuan utama?** Untuk **create index java** dan mengambil konten dokumen dengan cepat.  
- **Library mana yang harus saya gunakan?** **GroupDocs.Search for Java** **java search library**.  
- **Bisakah saya mengeluarkan teks ke file?** Ya, gunakan adaptor **output text to file** yang disediakan.  
- **Apakah ekstraksi terstruktur didukung?** Tentu – gunakan adaptor **structured text extraction**.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan atau permanen diperlukan untuk penggunaan produksi.

## Apa yang Akan Anda Pelajari
- Cara **create index java** dan **add documents to index** menggunakan GroupDocs.Search untuk Java.  
- Teknik untuk **output text to file**, aliran, string, dan data terstruktur.  
- Tips optimalisasi kinerja untuk pencarian yang efisien dan manajemen memori.  
- Aplikasi dunia nyata dari fitur-fitur ini.

### Prasyarat
Sebelum menyelam ke tutorial, pastikan hal‑hal berikut sudah tersedia:
- **Java Development Kit (JDK)**: Versi 8 atau lebih tinggi disarankan.  
- Library **GroupDocs.Search for Java**.  
- **Maven** untuk manajemen dependensi dan membangun proyek Anda.  
- Pengetahuan dasar pemrograman Java, khususnya operasi I/O file.

### Menyiapkan GroupDocs.Search untuk Java
Untuk mulai menggunakan GroupDocs.Search untuk Java, Anda perlu menambahkan dependensi yang diperlukan ke proyek Anda. Berikut cara menyiapkannya menggunakan Maven:

**Pengaturan Maven**  
Tambahkan konfigurasi repositori dan dependensi berikut ke file `pom.xml` Anda:

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

Bagi yang lebih suka mengunduh langsung, Anda dapat memperoleh versi terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Perolehan Lisensi**  
Untuk menggunakan GroupDocs.Search, pertimbangkan memperoleh lisensi percobaan gratis atau lisensi sementara. Untuk pembelian penuh, kunjungi situs resmi mereka untuk memperoleh lisensi permanen.

## Cara create index java dengan pengaturan khusus
Bagian ini memandu Anda membuat indeks, menambahkan dokumen, dan mengonfigurasi kompresi untuk penyimpanan optimal.

### Pembuatan Indeks dan Pengindeksan Dokumen

#### Gambaran Umum
Membuat indeks memungkinkan Anda mencari dokumen secara efisien. Contoh di bawah menunjukkan cara **create index java** dengan kompresi tinggi dan kemudian **add documents to index**.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**Penjelasan**  
- **Index Settings**: Kami mengaktifkan kompresi tinggi untuk penyimpanan teks, mengoptimalkan penggunaan ruang disk.  
- **Adding Documents**: Metode `index.add()` **adds documents to index**, memindai folder secara rekursif.

## Cara output text to file, stream, string, dan format terstruktur
Berikut empat cara umum untuk mengambil dan menyimpan konten yang diekstrak setelah Anda **created index java**.

### Output Teks Dokumen ke File

#### Gambaran Umum
Contoh ini menunjukkan cara **output text to file** dalam format HTML, yang berguna untuk inspeksi visual atau pemrosesan lanjutan.

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**Penjelasan**  
- **FileOutputAdapter**: Mengonversi teks dokumen yang diindeks menjadi HTML dan menuliskannya ke jalur file yang ditentukan.

### Output Teks Dokumen ke Stream

#### Gambaran Umum
Ketika Anda memerlukan pemrosesan dalam memori—seperti menghasilkan konten web dinamis—output ke stream adalah pilihan ideal.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**Penjelasan**  
- **StreamOutputAdapter**: Menyalurkan teks dokumen ke `ByteArrayOutputStream`, memungkinkan penanganan fleksibel tanpa menyentuh sistem file.

### Output Teks Dokumen ke String

#### Gambaran Umum
Jika Anda hanya perlu mencatat atau menampilkan konten, mengonversi hasil ke `String` adalah cara tercepat.

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**Penjelasan**  
- **StringOutputAdapter**: Menangkap teks dokumen dalam sebuah `String`, memudahkan penyisipan ke log atau komponen UI.

### Output Teks Dokumen ke Format Terstruktur

#### Gambaran Umum
Untuk parsing lanjutan—seperti mengekstrak bidang, tabel, atau metadata khusus—gunakan adaptor output terstruktur.

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**Penjelasan**  
- **StructuredOutputAdapter**: Mengekstrak teks dokumen ke format **structured text extraction**, memungkinkan analisis detail atau pipeline data downstream.

## Masalah Umum dan Solusinya
| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Indeks tidak dibuat** | Jalur folder salah atau izin menulis tidak ada | Pastikan `indexFolder` ada dan aplikasi memiliki akses menulis |
| **Tidak ada dokumen yang dikembalikan** | `index.add()` tidak dipanggil atau folder sumber salah | Pastikan `documentsFolder` mengarah ke direktori yang tepat dan berisi tipe file yang didukung |
| **File output kosong** | Jalur adaptor output tidak valid atau direktori hilang | Buat direktori target (`YOUR_OUTPUT_DIRECTORY`) sebelum menjalankan |
| **Lonjakan memori dengan file besar** | Memuat seluruh file ke memori | Gunakan adaptor stream (`StreamOutputAdapter`) untuk memproses data secara bertahap |

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menggunakan GroupDocs.Search dengan bahasa JVM lain seperti Kotlin atau Scala?**  
J: Ya, library ini murni Java dan bekerja mulus dengan bahasa JVM apa pun.

**T: Bagaimana kompresi memengaruhi kecepatan pencarian?**  
J: Kompresi tinggi mengurangi penggunaan disk tetapi dapat menambah beban CPU sedikit saat pengindeksan. Kinerja pencarian tetap cepat karena library mendekompresi secara langsung.

**T: Apakah memungkinkan memperbarui indeks yang ada tanpa membangunnya kembali?**  
J: Tentu. Gunakan `index.add()` untuk file baru dan `index.remove()` untuk menghapus yang usang.

**T: Format output mana yang terbaik untuk pemrosesan bahasa alami lebih lanjut?**  
J: `PlainText` melalui adaptor **structured text extraction** memberikan konten bersih yang tidak bergantung bahasa, ideal untuk pipeline NLP.

**T: Apakah saya memerlukan lisensi untuk pengembangan dan pengujian?**  
J: Lisensi percobaan gratis cukup untuk pengembangan dan evaluasi. Deploymen produksi memerlukan lisensi berbayar.

---

**Terakhir Diperbarui:** 2026-01-14  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs