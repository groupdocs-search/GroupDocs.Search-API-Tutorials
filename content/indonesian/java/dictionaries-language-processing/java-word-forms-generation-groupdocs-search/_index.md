---
date: '2025-12-20'
description: Pelajari cara membuat penyedia bentuk kata di Java dengan GroupDocs.Search.
  Hasilkan bentuk tunggal dan jamak untuk pencarian, analisis teks, dan lainnya.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Buat Penyedia Formulir Word di Java Menggunakan API GroupDocs.Search
type: docs
url: /id/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Buat Penyedia Bentuk Kata dalam Java Menggunakan API GroupDocs.Search

Mengubah kata dari bentuk tunggal ke jamak—atau sebaliknya—adalah tantangan yang sering ditemui saat membangun aplikasi yang sadar bahasa. Dalam panduan ini Anda akan **membuat penyedia bentuk kata** menggunakan GroupDocs.Search Java API, memberikan mesin pencari atau alat analisis teks Anda kemampuan untuk memahami dan mencocokkan variasi kata yang berbeda secara otomatis.

Apakah Anda mengembangkan mesin pencari, sistem manajemen konten, atau aplikasi Java apa pun yang memproses bahasa alami, menguasai pembuatan bentuk kata akan membuat hasil Anda lebih akurat dan pengguna lebih puas. Mari kita jelajahi prasyarat yang diperlukan sebelum memulai.

## Jawaban Cepat
- **Apa yang dilakukan penyedia bentuk kata?** Ia menghasilkan bentuk alternatif (tunggal, jamak, dll.) dari sebuah kata sehingga pencarian dapat mencocokkan semua varian.  
- **Perpustakaan apa yang dibutuhkan?** GroupDocs.Search untuk Java (versi 25.4 atau lebih baru).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Versi Java apa yang didukung?** JDK 8 atau lebih tinggi.  
- **Berapa banyak baris kode yang dibutuhkan?** Sekitar 30 baris untuk implementasi penyedia sederhana.

## Apa itu fitur “Buat Penyedia Bentuk Kata”?
Komponen **create word forms provider** adalah kelas khusus yang mengimplementasikan `IWordFormsProvider`. Ia menerima sebuah kata dan mengembalikan array bentuk yang mungkin—tunggal, jamak, atau variasi linguistik lainnya—berdasarkan aturan yang Anda definisikan. Ini memungkinkan indeks pencarian memperlakukan “cat” dan “cats” sebagai setara, meningkatkan recall tanpa mengorbankan presisi.

## Mengapa menggunakan GroupDocs.Search untuk pembuatan bentuk kata?
- **Ekstensibilitas bawaan:** Anda dapat menyambungkan penyedia Anda langsung ke pipeline pengindeksan.  
- **Dioptimalkan untuk kinerja:** Perpustakaan menangani indeks besar secara efisien, dan Anda dapat menyimpan hasil dalam cache untuk kecepatan tambahan.  
- **Dukungan lintas bahasa:** Meskipun tutorial ini berfokus pada Java, konsep yang sama berlaku untuk .NET dan platform lainnya.

## Prasyarat

Sebelum mengimplementasikan **create word forms provider**, pastikan Anda memiliki:

- **Maven** terpasang dan JDK 8 atau lebih baru terpasang di mesin Anda.  
- Pemahaman dasar tentang pengembangan Java dan konfigurasi `pom.xml` Maven.  
- Akses ke perpustakaan GroupDocs.Search Java (versi 25.4 atau lebih baru).

## Menyiapkan GroupDocs.Search untuk Java

### Konfigurasi Maven

Tambahkan repositori dan dependensi ke file `pom.xml` Anda persis seperti yang ditunjukkan di bawah:

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

Atau, unduh JAR terbaru dari halaman rilis resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Langkah-langkah Akuisisi Lisensi

Untuk menggunakan GroupDocs.Search tanpa batasan:

1. **Free Trial:** Daftar untuk percobaan guna menjelajahi fitur inti.  
2. **Temporary License:** Minta kunci sementara untuk pengujian yang lebih lama.  
3. **Purchase:** Dapatkan lisensi komersial untuk penggunaan produksi tanpa batas.

### Inisialisasi dan Penyiapan Dasar

Potongan kode berikut menunjukkan cara membuat indeks—titik awal Anda untuk menambahkan dokumen dan logika bentuk kata:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Panduan Implementasi

Di bawah ini kami akan menjelaskan langkah-langkah untuk **create word forms provider** yang menangani transformasi sederhana tunggal‑ke‑jamak dan jamak‑ke‑tunggal.

### Mengimplementasikan SimpleWordFormsProvider

#### Gambaran Umum

Penyedia khusus kami akan:

- Menghapus akhiran “es” atau “s” untuk menebak bentuk tunggal.  
- Mengubah akhiran “y” menjadi “is” untuk menghasilkan bentuk jamak (misalnya, “city” → “citis”).  
- Menambahkan “s” dan “es” untuk menghasilkan kandidat jamak dasar.

#### Langkah 1 – Buat Kerangka Kelas

Mulailah dengan mendefinisikan kelas yang mengimplementasikan `IWordFormsProvider`. Biarkan pernyataan import tidak berubah:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Langkah 2 – Implementasikan `getWordForms`

Tambahkan metode yang membangun daftar bentuk yang mungkin. Blok ini berisi logika inti; Anda dapat memperluasnya nanti untuk mencakup aturan yang lebih kompleks.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Penjelasan Logika

- **Singularisasi:** Mendeteksi akhiran jamak umum (`es`, `s`) dan menghapusnya untuk memperkirakan kata dasar.  
- **Pluralisasi:** Menangani kata benda yang berakhiran `y` dengan menggantinya menjadi `is`, aturan sederhana yang berlaku untuk banyak kata bahasa Inggris.  
- **Penambahan Akhiran:** Menambahkan `s` dan `es` untuk mencakup bentuk jamak reguler yang mungkin tidak terdeteksi oleh pemeriksaan sebelumnya.

#### Tips Pemecahan Masalah

- **Sensitivitas Huruf:** Metode menggunakan `toLowerCase()` untuk perbandingan, memastikan “Cats” dan “cats” berperilaku sama.  
- **Kasus Tepi:** Kata yang lebih pendek dari panjang akhiran diabaikan untuk menghindari mengembalikan string kosong.  
- **Kinerja:** Untuk kosakata besar, pertimbangkan menyimpan hasil dalam `ConcurrentHashMap`.

## Aplikasi Praktis

Mengimplementasikan **create word forms provider** dapat meningkatkan beberapa skenario dunia nyata:

1. **Mesin Pencari:** Pengguna yang mengetik “mouse” juga harus menemukan dokumen yang berisi “mice”. Penyedia dapat menghasilkan bentuk tidak teratur tersebut.  
2. **Alat Analisis Teks:** Analisis sentimen atau ekstraksi entitas menjadi lebih dapat diandalkan ketika semua varian kata dikenali.  
3. **Sistem Manajemen Konten:** Pembuatan tag otomatis dapat mencakup sinonim jamak, meningkatkan SEO dan tautan internal.

## Pertimbangan Kinerja

Saat Anda menyematkan penyedia ke dalam sistem produksi, ingatlah tips berikut:

- **Cache Bentuk yang Sering Digunakan:** Simpan hasil di memori untuk menghindari perhitungan ulang kata yang sama secara berulang.  
- **Pantau Heap JVM:** Indeks besar dapat meningkatkan tekanan memori; sesuaikan `-Xmx` secara tepat.  
- **Gunakan Koleksi Efisien:** `ArrayList` cocok untuk set kecil, tetapi untuk ribuan bentuk pertimbangkan `HashSet` untuk menghilangkan duplikat dengan cepat.

**Praktik Terbaik**

- Jaga perpustakaan tetap terbaru untuk mendapatkan perbaikan kinerja.  
- Profilkan penyedia dengan beban kueri realistis untuk menemukan bottleneck lebih awal.

## Kesimpulan

Anda kini telah mempelajari cara **create word forms provider** menggunakan GroupDocs.Search untuk Java. Komponen ringan ini dapat secara dramatis meningkatkan relevansi hasil pencarian dan akurasi analisis linguistik di banyak aplikasi.  

**Langkah Selanjutnya:**  
- Bereksperimen dengan aturan linguistik yang lebih canggih (jamak tidak teratur, stemming).  
- Integrasikan penyedia ke dalam pipeline pengindeksan dan ukur peningkatan recall.  
- Jelajahi fitur GroupDocs.Search lainnya seperti kamus sinonim dan analyzer khusus.

**Ajakan:** Coba tambahkan `SimpleWordFormsProvider` ke proyek Anda hari ini dan lihat bagaimana itu memperkaya pengalaman pencarian Anda!

## Bagian FAQ

**1. Apa itu GroupDocs.Search untuk Java?**  
Ini adalah perpustakaan kuat yang menawarkan pencarian full‑text, pengindeksan, dan fitur linguistik—termasuk kemampuan untuk menyambungkan penyedia bentuk kata khusus.

**2. Bagaimana cara kerja SimpleWordFormsProvider?**  
Ia menghasilkan bentuk alternatif dengan menerapkan aturan berbasis akhiran sederhana (menghapus “s/es”, mengubah “y” menjadi “is”, dan menambahkan “s/es”).

**3. Bisakah saya menyesuaikan aturan pembuatan bentuk kata?**  
Tentu saja. Modifikasi metode `getWordForms` untuk menyertakan bentuk tidak teratur, aturan spesifik locale, atau integrasi dengan kamus eksternal.

**4. Apa saja aplikasi umum untuk fitur ini?**  
Mesin pencari, pipeline analisis teks, dan platform CMS mendapat manfaat dari pengenalan varian tunggal/jamak.

**5. Apakah saya memerlukan lisensi komersial untuk penggunaan produksi?**  
Ya—meskipun percobaan memungkinkan Anda menjelajahi API, lisensi yang dibeli menghilangkan batas penggunaan dan memberikan dukungan.

---

**Terakhir Diperbarui:** 2025-12-20  
**Diuji Dengan:** GroupDocs.Search 25.4 (Java)  
**Penulis:** GroupDocs  

---