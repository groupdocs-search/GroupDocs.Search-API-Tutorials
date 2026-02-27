---
date: '2026-01-08'
description: Pelajari cara menyorot hasil pencarian Java menggunakan GroupDocs.Search
  dalam aplikasi Java, mengonfigurasi pencarian yang dapat diskalakan, penyebaran
  jaringan, dan penyorotan hasil.
keywords:
- GroupDocs.Search Java
- distributed searching Java
- highlight search results Java
title: Sorot Hasil Pencarian Java Menggunakan GroupDocs.Search
type: docs
url: /id/java/licensing-configuration/groupdocs-search-java-implementation/
weight: 1
---

# Sorot Hasil Pencarian Java Menggunakan GroupDocs.Search

Jika Anda lelah menyaring dokumen tak berujung secara manual, **highlight search results java** menawarkan cara yang cepat dan andal untuk menampilkan tepat apa yang Anda butuhkan. Dalam tutorial ini kami akan membahas cara mengonfigurasi jaringan pencarian terdistribusi, mengindeks file Anda, menjalankan kueri, dan akhirnya menyorot kecocokan langsung di dalam dokumen. Pada akhir tutorial, Anda akan memiliki solusi siap produksi yang dapat diskalakan di beberapa node dan membuat istilah relevan langsung menonjol.

## Jawaban Cepat
- **Apa arti “highlight search results java”?** Itu merujuk pada penandaan secara programatik kata kunci yang ditemukan di dalam dokumen saat menggunakan pustaka Java seperti GroupDocs.Search.  
- **Bisakah saya menyorot beberapa istilah dalam dokumen yang sama?** Ya – gunakan `HighlightOptions` untuk menentukan berapa banyak istilah sebelum/setelah setiap kecocokan yang ditampilkan.  
- **Apakah saya memerlukan lisensi untuk menjalankan contoh ini?** Lisensi percobaan atau lisensi sementara cukup untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Versi Java apa yang dibutuhkan?** Java 8 atau lebih baru.  
- **Apakah pendekatan ini cocok untuk koleksi dokumen besar?** Tentu – jaringan pencarian mendistribusikan beban pengindeksan dan kueri ke seluruh node.

## Apa Itu Highlight Search Results Java?
**Highlight search results java** adalah proses mengambil kueri pencarian, menemukan fragmen yang cocok dalam dokumen Anda, dan menekankan secara visual fragmen tersebut (misalnya, dengan menambahkan penanda atau mengembalikannya sebagai potongan yang disorot). Hal ini memudahkan pengguna akhir melihat konteks setiap kecocokan tanpa harus membuka seluruh file.

## Mengapa Menggunakan GroupDocs.Search untuk Menyorot?
GroupDocs.Search menyediakan mesin siap pakai berperforma tinggi yang mendukung puluhan format file, pengindeksan terdistribusi, dan penyorot fragmen bawaan. Ini menghilangkan kebutuhan menulis parser khusus atau mengelola infrastruktur pencarian tingkat rendah, sehingga Anda dapat fokus pada memberikan pengalaman pengguna yang mulus.

## Prasyarat

- **Java Development Kit (JDK) 8+** – pastikan `java -version` menampilkan 1.8 atau lebih tinggi.  
- **Maven** – untuk manajemen dependensi.  
- **GroupDocs.Search for Java 25.4** – versi yang digunakan dalam panduan ini.  
- IDE seperti **IntelliJ IDEA** atau **Eclipse** (opsional namun disarankan).  
- Pengetahuan dasar tentang Java dan konsep jaringan.

## Menyiapkan GroupDocs.Search untuk Java

Anda dapat menambahkan pustaka ke proyek Anda melalui Maven atau dengan mengunduh JAR secara langsung.

### Pengaturan Maven
Tambahkan repositori dan dependensi ke `pom.xml` Anda:

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
Atau, unduh JAR terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Langkah Akuisisi Lisensi
- **Percobaan Gratis:** Mulai dengan percobaan untuk menjelajahi fitur inti.  
- **Lisensi Sementara:** Dapatkan lisensi uji lanjutan dari [halaman ini](https://purchase.groupdocs.com/temporary-license/).  
- **Pembelian:** Peroleh lisensi penuh untuk penyebaran produksi.

### Inisialisasi dan Pengaturan Dasar
Buat instance `Index` yang menunjuk ke folder tempat indeks pencarian akan disimpan:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an instance of Index
        Index index = new Index("path/to/index/directory");
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Panduan Implementasi

### Cara Menyorot Hasil Pencarian Java dalam Jaringan Terdistribusi

#### Mengonfigurasi Jaringan Pencarian
Pertama, tentukan di mana dokumen Anda berada dan port apa yang akan digunakan jaringan.

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/HighlightingResultsInNetwork/";
int basePort = 49116; // Change if port is busy

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **`basePath`** – folder root yang berisi file yang ingin Anda indeks.  
- **`basePort`** – port TCP untuk komunikasi node; pilih yang belum terpakai.

#### Menyebarkan Node Jaringan Pencarian
Sebarkan satu atau lebih node berdasarkan konfigurasi. Node pertama menjadi master.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```

- **`nodes`** – array semua node yang sedang berjalan.  
- **`masterNode`** – mengoordinasikan pengindeksan dan distribusi kueri.

#### Berlangganan ke Event Node Jaringan Pencarian
Lampirkan listener ke node master untuk menerima notifikasi waktu nyata (misalnya, saat pengindeksan selesai).

```java
import com.groupdocs.search.scaling.events.*;

SearchNetworkNodeEvents.subscribe(masterNode);
```

#### Mengindeks Direktori di Node Jaringan
Arahkan node ke folder(s) yang ingin Anda indeks. Kelas pembantu `Utils.DocumentsPath` mengarah ke folder data contoh.

```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.options.*;

IndexingDocuments.addDirectories(masterNode, Utils.DocumentsPath);
```

#### Mencari Teks di Seluruh Node Jaringan
Jalankan kueri terhadap **semua** node dan ambil dokumen yang cocok.

```java
import java.util.ArrayList;
import com.groupdocs.search.scaling.results.*;

ArrayList<NetworkFoundDocument> documents = TextSearchInNetwork.searchAll(masterNode, "ipsum", false);
highlightInDocument(masterNode, documents.get(0), 3); // Highlight results from the first found document.
```

- Ganti `"ipsum"` dengan istilah apa pun yang ingin Anda temukan.  
- Metode `highlightInDocument` (ditunjukkan berikutnya) akan menerapkan sorotan.

#### Menyorot Beberapa Istilah Dokumen – Highlighting Search Results
Metode berikut mendemonstrasikan cara menyorot fragmen di sekitar setiap kecocokan. Metode ini juga menunjukkan cara mengontrol jumlah istilah di sekitarnya, memenuhi kata kunci sekunder **highlight multiple terms document**.

```java
import com.groupdocs.search.highlighters.*;
import com.groupdocs.search.options.*;

public static void highlightInDocument(
    SearchNetworkNode node,
    NetworkFoundDocument document,
    int maxFragments) {
    
    Searcher searcher = node.getSearcher();
    FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.PlainText);

    HighlightOptions options = new HighlightOptions();
    options.setTermsAfter(5);
    options.setTermsBefore(5);
    options.setTermsTotal(15);

    searcher.highlight(document, highlighter, options); // Perform highlighting on the document.

    FragmentContainer[] result = highlighter.getResult();
    for (FragmentContainer container : result) {
        if (container.getCount() == 0) continue;

        String[] fragments = container.getFragments();
        int count = Math.min(fragments.length, maxFragments);
        for (int j = 0; j < count; j++) {
            // Print each fragment within the specified limit.
        }
    }
}
```

- **`OutputFormat.PlainText`** – mengembalikan potongan teks biasa; Anda dapat beralih ke HTML untuk UI yang lebih kaya.  
- **`HighlightOptions`** – mengontrol berapa banyak kata sebelum/setelah setiap kecocokan yang disertakan (`setTermsBefore`, `setTermsAfter`).  
- **`maxFragments`** – membatasi jumlah potongan yang ditampilkan per dokumen.

#### Menutup Node Jaringan
Setelah selesai, matikan setiap node untuk membebaskan sumber daya.

```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Aplikasi Praktis

- **Manajemen Dokumen Perusahaan:** Sentralisasi file korporat dan biarkan karyawan langsung menemukan kontrak atau kebijakan yang relevan.  
- **Berkas Kasus Hukum:** Cepat menampilkan dokumen preseden dengan menyorot istilah hukum utama.  
- **Basis Pengetahuan R&D:** Peneliti dapat mencari paten atau makalah teknis dan melihat kutipan yang disorot.  
- **Katalog E‑commerce:** Memungkinkan pembeli menemukan produk melalui kata kunci dengan sorotan pada deskripsi.  
- **Sistem Perpustakaan:** Pengguna dapat mencari di ribuan buku dan melihat bagian yang disorot tanpa membuka setiap file.

## Pertimbangan Kinerja

- **Jaga indeks tetap segar:** Lakukan pengindeksan ulang file yang berubah setiap malam atau gunakan pembaruan inkremental.  
- **Manfaatkan banyak node:** Distribusikan beban pengindeksan dan kueri untuk menghindari kemacetan.  
- **Sesuaikan `HighlightOptions`:** Mengurangi `termsBefore/After` menurunkan penggunaan memori untuk dokumen sangat besar.  

## Masalah Umum & Pemecahan Masalah

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|-------|
| Tidak ada hasil yang dikembalikan | Indeks belum dibangun atau mengarah ke folder yang salah | Verifikasi `Utils.DocumentsPath` dan jalankan kembali `IndexingDocuments.addDirectories` |
| Output sorotan kosong | `HighlightOptions` terlalu rendah atau masalah enkoding dokumen | Tingkatkan `termsTotal` atau pastikan enkoding dokumen didukung |
| Kesalahan konflik port | `basePort` sudah digunakan | Pilih nomor port lain (misalnya, 49117) |
| Pengecualian lisensi | File lisensi hilang atau kedaluwarsa | Tempatkan file `GroupDocs.Search.lic` yang valid di root aplikasi |

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menyebarkan beberapa node jaringan pencarian untuk load balancing?**  
J: Ya, menyebarkan beberapa node membagi pekerjaan pengindeksan dan kueri, meningkatkan skalabilitas dan waktu respons.

**T: Bagaimana cara menyorot beberapa istilah pencarian dalam dokumen yang sama?**  
J: Kirimkan daftar istilah ke metode `highlight` dan konfigurasikan `HighlightOptions` untuk menampilkan kata di sekitarnya untuk setiap kecocokan.

**T: Apakah memungkinkan berlangganan ke event pencarian waktu nyata?**  
J: Tentu. Gunakan `SearchNetworkNodeEvents.subscribe(masterNode)` untuk menerima callback tentang progres pengindeksan, eksekusi kueri, dan error.

**T: Format file apa saja yang didukung GroupDocs.Search untuk pengindeksan dan penyorotan?**  
J: Lebih dari 50 format, termasuk DOCX, PDF, HTML, TXT, PPTX, dan lainnya.

**T: Bagaimana cara meningkatkan kecepatan pencarian pada koleksi sangat besar?**  
J: Perbarui indeks secara rutin, distribusikan ke beberapa node, dan sesuaikan `HighlightOptions` untuk membatasi ukuran fragmen.

## Kesimpulan
Dengan mengikuti panduan ini Anda kini memiliki setup lengkap dan siap produksi untuk **highlight search results java** menggunakan GroupDocs.Search. Anda dapat menskalakan solusi di seluruh jaringan, mengindeks tipe dokumen apa pun yang didukung, menjalankan kueri cepat, dan mengembalikan potongan yang disorot yang membantu pengguna menemukan apa yang mereka butuhkan. Jelajahi langkah selanjutnya—mengintegrasikan hasil ke UI web, menambahkan pencarian berfaset, atau menggabungkan OCR untuk PDF yang dipindai.

---

**Terakhir Diperbarui:** 2026-01-08  
**Diuji Dengan:** GroupDocs.Search for Java 25.4  
**Penulis:** GroupDocs  

---