---
date: '2026-04-02'
description: Pelajari cara membuat repositori indeks Java, menambahkan dokumen ke
  indeks, menangani peristiwa pengindeksan waktu nyata, dan mencari di seluruh beberapa
  indeks menggunakan GroupDocs.Search untuk Java.
keywords:
- create index repository java
- add documents to index
- search across multiple indices
title: 'Cara membuat repositori indeks Java dengan GroupDocs.Search: Pengindeksan
  & Pencarian Dokumen yang Efisien'
type: docs
url: /id/java/searching/master-groupdocs-search-java-indexing-search/
weight: 1
---

# buat repositori indeks java dengan GroupDocs.Search: Pengindeksan & Pencarian Dokumen yang Efisien

Dalam lanskap digital saat ini, mengelola dataset besar secara efisien adalah tantangan yang dihadapi pengembang di seluruh dunia. **Tutorial ini menunjukkan cara membuat repositori indeks java** menggunakan GroupDocs.Search untuk Java, sehingga Anda dapat menambahkan dokumen ke indeks, merespons peristiwa pengindeksan waktu nyata, dan melakukan pencarian cepat di seluruh beberapa indeks. Kami akan memandu Anda melalui penyiapan lingkungan, membangun repositori indeks, berlangganan ke peristiwa, dan mengeksekusi kueri kuat—semua dengan contoh kode langkah demi langkah yang jelas.

## Jawaban Cepat
- **Apa langkah pertama?** Tambahkan repositori Maven GroupDocs.Search dan dependensinya ke proyek Anda.  
- **Bagaimana cara membuat repositori indeks?** Buat instance `IndexRepository` dan tambahkan objek `Index` untuk setiap folder.  
- **Apakah saya dapat memantau kemajuan pengindeksan?** Ya—berlangganan ke peristiwa `OperationProgressChanged` untuk pembaruan waktu nyata.  
- **Bagaimana cara mencari di seluruh beberapa indeks?** Panggil `indexRepository.search(query)` setelah menambahkan semua indeks.  
- **Versi Java apa yang dibutuhkan?** JDK 8 atau lebih tinggi.

## Apa yang Akan Anda Pelajari
- Menyiapkan dan mengkonfigurasi lingkungan pengembangan Anda dengan GroupDocs.Search.  
- **Cara membuat repositori indeks java** dan memelihara beberapa indeks secara efisien.  
- Berlangganan ke **peristiwa pengindeksan waktu nyata** untuk umpan balik instan.  
- **Cara menambahkan dokumen ke indeks** dan menjaga mereka tetap terbaru.  
- Melakukan **pencarian di seluruh beberapa indeks** dengan satu kueri.  
- Aplikasi praktis dan tips penyetelan kinerja.

### Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki hal berikut:
- **Java Development Kit (JDK)**: Versi 8 atau lebih tinggi.  
- **Integrated Development Environment (IDE)**: Seperti IntelliJ IDEA atau Eclipse.  
- **Maven**: Untuk mengelola dependensi (opsional tetapi disarankan).

#### Perpustakaan dan Dependensi yang Diperlukan
Untuk menggunakan GroupDocs.Search untuk Java, tambahkan konfigurasi Maven berikut ke file `pom.xml` Anda:

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

Sebagai alternatif, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Akuisisi Lisensi
Anda dapat memperoleh lisensi percobaan gratis atau membeli lisensi penuh untuk menjelajahi semua fitur tanpa batasan. Untuk detail lisensi dan lisensi sementara, kunjungi [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## Menyiapkan GroupDocs.Search untuk Java

Untuk memulai dengan GroupDocs.Search dalam proyek Java Anda, pastikan Maven terinstal (jika tidak menggunakan Maven, atur pustaka secara manual). Ikuti langkah-langkah berikut:

1. **Tambahkan Repository dan Dependensi**: Gunakan konfigurasi Maven yang disediakan untuk menyertakan GroupDocs.Search.  
2. **Inisialisasi Dasar**:

```java
import com.groupdocs.search.Index;

// Initialize an index repository instance
IndexRepository indexRepository = new IndexRepository();
```

## Cara membuat repositori indeks java dan mengelola beberapa indeks

Membuat sistem terstruktur untuk pengindeksan memungkinkan manajemen dokumen yang efisien dan kemampuan pencarian. Ikuti langkah-langkah bernomor ini; setiap langkah menyertakan penjelasan singkat sebelum blok kode sehingga Anda tahu persis apa yang terjadi.

### Langkah 1: Tentukan Jalur untuk Indeks dan Dokumen
```java
String indexFolder1 = "YOUR_DOCUMENT_DIRECTORY\\Index1";
String indexFolder2 = "YOUR_DOCUMENT_DIRECTORY\\Index2";
String documentFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentFolder2 = "YOUR_DOCUMENT_DIRECTORY";
```

### Langkah 2: Buat Instance `IndexRepository`
```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexRepository;

// Initialize the index repository
IndexRepository indexRepository = new IndexRepository();
```

### Langkah 3: Buat atau Muat Indeks dan Tambahkan ke Repository
```java
// Load or create indices
Index index1 = new Index(indexFolder1);
indexRepository.addToRepository(index1);

Index index2 = new Index(indexFolder2);
indexRepository.addToRepository(index2);
```
Konfigurasi ini memungkinkan Anda **mengelola beberapa indeks** dengan mulus.

### Langkah 4: **Tambahkan dokumen ke indeks** – Isi Setiap Indeks
```java
// Add documents to the first index
index1.add(documentFolder1);

// Add documents to the second index
index2.add(documentFolder2);
```

### Langkah 5: Perbarui Semua Indeks di Repository
```java
// Synchronize all indices with new document data
indexRepository.update();
```
Menjalankan `update()` memastikan hasil pencarian Anda selalu mencerminkan perubahan terbaru.

## Berlangganan ke peristiwa pengindeksan waktu nyata

Memantau peristiwa pengindeksan dapat meningkatkan responsivitas aplikasi dan memberi Anda umpan balik instan. Berikut cara menghubungkan ke peristiwa tersebut.

### Langkah 1: Tentukan Jalur untuk Folder Indeks
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\Index";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

### Langkah 2: Buat Instance `IndexRepository` dan Berlangganan ke Peristiwa
```java
import com.groupdocs.search.events.EventHandler;
import com.groupdocs.search.events.OperationProgressEventArgs;

// Initialize the index repository
IndexRepository indexRepository = new IndexRepository();

// Load or create an index
Index index = new Index(indexFolder);
indexRepository.addToRepository(index);

// Subscribe to indexing progress events
indexRepository.getEvents().OperationProgressChanged.add(new EventHandler<OperationProgressEventArgs>() {
    @Override
    public void invoke(Object sender, OperationProgressEventArgs args) {
        System.out.println("Document indexed: " + args.getIndexedDocumentName());
    }
});
```
Handler ini mencetak pesan setiap kali dokumen diindeks, memberi Anda **peristiwa pengindeksan waktu nyata**.

### Langkah 3: Tambahkan Dokumen untuk Memicu Peristiwa
```java
// Start adding documents to trigger events
index.add(documentFolder);
```

## Mencari di seluruh beberapa indeks

Menjalankan pencarian yang mencakup semua indeks Anda penting untuk pengambilan informasi yang cepat.

### Langkah 1: Tentukan Jalur dan Inisialisasi Repository
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\Index";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Create or load the index repository
IndexRepository indexRepository = new IndexRepository();
indexRepository.addToRepository(new com.groupdocs.search.Index(indexFolder));
```

### Langkah 2: Tambahkan Dokumen dan Lakukan Pencarian
```java
new com.groupdocs.search.Index(indexFolder).add(documentFolder);

String query = "decisively";
SearchResult result = indexRepository.search(query);
// Process search results (implement as needed)
```
Dengan pengaturan ini Anda dapat **mencari di seluruh beberapa indeks** menggunakan satu string kueri.

## Aplikasi Praktis
1. **Manajemen Dokumen Perusahaan** – Indeks perpustakaan korporat besar untuk pengambilan instan.  
2. **Sistem Pengambilan Kasus Hukum** – Temukan berkas kasus yang relevan dengan cepat.  
3. **Dukungan Pelanggan** – Ambil tiket atau email lama dengan kata kunci tertentu.  
4. **Platform Agregasi Konten** – Kelola jutaan artikel dari berbagai sumber.

## Pertimbangan Kinerja
- Jalankan `indexRepository.update()` secara teratur untuk menjaga indeks tetap segar.  
- Pantau penggunaan memori; dataset besar mungkin memerlukan pemisahan menjadi indeks terpisah.  
- Manfaatkan **peristiwa pengindeksan waktu nyata** untuk menghindari pengindeksan ulang penuh yang tidak perlu.  

## Kesimpulan
Dengan mengikuti panduan ini, Anda telah mempelajari cara **membuat repositori indeks java** dengan GroupDocs.Search, **menambahkan dokumen ke indeks**, mendengarkan **peristiwa pengindeksan waktu nyata**, dan melakukan **pencarian cepat di seluruh beberapa indeks**. Sebagai langkah selanjutnya, jelajahi fitur lanjutan di [dokumentasi GroupDocs](https://docs.groupdocs.com/search/java/).

## Pertanyaan yang Sering Diajukan

**Q: Apakah saya dapat menggunakan GroupDocs.Search dengan kerangka kerja Java lainnya?**  
A: Ya, ia terintegrasi dengan mulus dengan Spring Boot, Jakarta EE, dan kerangka kerja populer lainnya.

**Q: Bagaimana saya harus menangani koleksi dokumen yang sangat besar?**  
A: Gunakan pengindeksan batch dan pertimbangkan memecah data menjadi beberapa indeks, kemudian cari di antaranya seperti yang ditunjukkan di atas.

**Q: Opsi lisensi apa yang tersedia?**  
A: Mulailah dengan lisensi percobaan gratis untuk mengevaluasi produk; lisensi penuh diperlukan untuk penggunaan produksi.

**Q: Apakah memungkinkan menyesuaikan peringkat relevansi hasil pencarian?**  
A: Tentu – Anda dapat menyesuaikan kriteria peringkat melalui API `SearchSettings`.

**Q: Di mana saya dapat menemukan tips pemecahan masalah untuk kegagalan pengindeksan?**  
A: Aktifkan logging terperinci dan berlangganan ke peristiwa `OperationProgressChanged` untuk mengidentifikasi file yang bermasalah.

## Sumber Daya
- **Dokumentasi**: [Dokumentasi GroupDocs](https://docs.groupdocs.com/search/java/)  
- **Referensi API**: [GroupDocs API](https://apireference.groupdocs.com/search/java/)

---

**Terakhir Diperbarui:** 2026-04-02  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs  

---