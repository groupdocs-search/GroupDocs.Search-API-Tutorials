---
date: '2026-02-21'
description: Pelajari cara menghasilkan bentuk tunggal dan jamak dalam Java menggunakan
  API GroupDocs.Search. Buat penyedia bentuk kata khusus untuk pencarian dan analisis
  teks yang akurat.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Hasilkan Bentuk Tunggal Jamak dalam Java dengan GroupDocs.Search
type: docs
url: /id/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

 translations.

Check for any missing elements: code block placeholders remain unchanged. No other shortcodes. Ensure we didn't translate URLs.

All good.

Now output only the translated content.# Hasilkan Bentuk Tunggal Jamak dalam Java dengan GroupDocs.Search

Jika Anda perlu **menghasilkan bentuk tunggal jamak dalam Java**, penyedia bentuk kata khusus adalah kunci agar mesin pencarian atau analisis teks Anda memahami setiap variasi istilah. Dalam tutorial ini kami akan memandu Anda membangun penyedia tersebut dengan GroupDocs.Search Java API, sehingga aplikasi Anda dapat secara otomatis mencocokkan “cat”, “cats”, “city”, dan “citis” tanpa usaha tambahan.

## Jawaban Cepat
- **Apa yang dilakukan penyedia bentuk kata?** Ia menghasilkan bentuk alternatif (tunggal, jamak, dll.) dari sebuah kata sehingga pencarian dapat mencocokkan semua varian.  
- **Perpustakaan apa yang diperlukan?** GroupDocs.Search untuk Java (versi 25.4 atau lebih baru).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Versi Java apa yang didukung?** JDK 8 atau lebih tinggi.  
- **Berapa banyak baris kode yang diperlukan?** Sekitar 30 baris untuk implementasi penyedia sederhana.

## Apa itu fitur “Create Word Forms Provider”?
Komponen **create word forms provider** adalah kelas khusus yang mengimplementasikan `IWordFormsProvider`. Ia menerima sebuah kata dan mengembalikan array bentuk yang mungkin—tunggal, jamak, atau variasi linguistik lainnya—berdasarkan aturan yang Anda tentukan. Ini memungkinkan indeks pencarian memperlakukan “cat” dan “cats” sebagai setara, meningkatkan recall tanpa mengorbankan presisi.

## Mengapa menggunakan GroupDocs.Search untuk menghasilkan bentuk kata?
- **Ekstensibilitas bawaan:** Sambungkan penyedia Anda langsung ke pipeline pengindeksan.  
- **Dioptimalkan untuk kinerja:** Menangani indeks besar secara efisien, dan Anda dapat menyimpan hasil dalam cache untuk kecepatan tambahan.  
- **Dukungan lintas bahasa:** Konsep ini juga berlaku untuk .NET dan platform lainnya.

## Prasyarat
Sebelum mengimplementasikan **create word forms provider**, pastikan Anda memiliki:

- **Maven** terpasang dan JDK 8 atau lebih baru sudah diatur di mesin Anda.  
- Familiaritas dasar dengan pengembangan Java dan konfigurasi `pom.xml` Maven.  
- Akses ke perpustakaan GroupDocs.Search Java (versi 25.4 atau lebih baru).  

## Menyiapkan GroupDocs.Search untuk Java

### Konfigurasi Maven

Add the repository and dependency to your `pom.xml` file exactly as shown below:

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

Sebagai alternatif, unduh JAR terbaru dari halaman rilis resmi: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Langkah-langkah Akuisisi Lisensi

1. **Free Trial:** Daftar untuk percobaan guna menjelajahi fitur inti.  
2. **Temporary License:** Minta kunci sementara untuk pengujian yang diperpanjang.  
3. **Purchase:** Dapatkan lisensi komersial untuk penggunaan produksi tanpa batas.

### Inisialisasi dan Penyiapan Dasar

The following snippet demonstrates how to create an index—your starting point for adding documents and word‑form logic:

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

Berikut kami menjelaskan langkah-langkah untuk **create word forms provider** yang menangani transformasi sederhana tunggal‑ke‑jamak dan jamak‑ke‑tunggal.

### Mengimplementasikan SimpleWordFormsProvider

#### Gambaran Umum
Penyedia khusus kami akan:

- Menghapus akhiran “es” atau “s” untuk menebak bentuk tunggal.  
- Mengubah akhiran “y” menjadi “is” untuk menghasilkan bentuk jamak (mis., “city” → “citis”).  
- Menambahkan “s” dan “es” untuk menghasilkan kandidat jamak dasar.

#### Langkah 1 – Buat Kerangka Kelas

Start by defining a class that implements `IWordFormsProvider`. Keep the import statements unchanged:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Langkah 2 – Implementasikan `getWordForms`

Add the method that builds the list of possible forms. This block contains the core logic; you can extend it later to cover more complex rules.

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
- **Singularization:** Mendeteksi akhiran jamak umum (`es`, `s`) dan menghapusnya untuk memperkirakan kata dasar.  
- **Pluralization:** Menangani kata benda yang berakhiran `y` dengan menggantinya menjadi `is`, aturan sederhana yang berlaku untuk banyak kata bahasa Inggris.  
- **Suffix Appending:** Menambahkan `s` dan `es` untuk mencakup bentuk jamak reguler yang mungkin tidak terdeteksi oleh pemeriksaan sebelumnya.

#### Tips Pemecahan Masalah
- **Case Sensitivity:** Metode ini menggunakan `toLowerCase()` untuk perbandingan, memastikan “Cats” dan “cats” berperilaku sama.  
- **Edge Cases:** Kata yang lebih pendek dari panjang akhiran diabaikan untuk menghindari mengembalikan string kosong.  
- **Performance:** Untuk kosakata besar, pertimbangkan menyimpan hasil dalam `ConcurrentHashMap`.

## Aplikasi Praktis

Mengimplementasikan **create word forms provider** dapat meningkatkan beberapa skenario dunia nyata:

1. **Search Engines:** Pengguna yang mengetik “mouse” juga harus menemukan dokumen yang berisi “mice”. Penyedia dapat menghasilkan bentuk tidak teratur tersebut.  
2. **Text Analysis Tools:** Analisis sentimen atau ekstraksi entitas menjadi lebih dapat diandalkan ketika semua varian kata dikenali.  
3. **Content Management Systems:** Pembuatan tag otomatis dapat menyertakan sinonim jamak, meningkatkan SEO dan penautan internal.

## Pertimbangan Kinerja

Saat Anda menyematkan penyedia ke dalam sistem produksi, perhatikan tips berikut:

- **Cache Frequently Used Forms:** Simpan hasil di memori untuk menghindari perhitungan ulang kata yang sama secara berulang.  
- **Monitor JVM Heap:** Indeks besar dapat meningkatkan tekanan memori; sesuaikan `-Xmx` sesuai kebutuhan.  
- **Use Efficient Collections:** `ArrayList` cocok untuk kumpulan kecil, tetapi untuk ribuan bentuk pertimbangkan `HashSet` untuk menghilangkan duplikat dengan cepat.

**Praktik Terbaik**
- Pertahankan perpustakaan tetap terbaru untuk mendapatkan perbaikan kinerja.  
- Profilkan penyedia dengan beban kueri realistis untuk menemukan bottleneck lebih awal.  

## Kesimpulan

Anda kini telah mempelajari cara **menghasilkan bentuk tunggal jamak dalam Java** menggunakan `SimpleWordFormsProvider` khusus dengan GroupDocs.Search. Komponen ringan ini dapat secara dramatis meningkatkan relevansi hasil pencarian dan akurasi analisis linguistik di banyak aplikasi.

**Langkah selanjutnya:**  
- Bereksperimen dengan aturan linguistik yang lebih canggih (jamak tidak teratur, stemming).  
- Integrasikan penyedia ke dalam pipeline pengindeksan dan ukur peningkatan recall.  
- Jelajahi fitur GroupDocs.Search lainnya seperti kamus sinonim dan analyzer khusus.

**Ajakan:** Cobalah menambahkan `SimpleWordFormsProvider` ke proyek Anda hari ini dan lihat bagaimana itu memperkaya pengalaman pencarian Anda!

## Bagian FAQ

**1. Apa itu GroupDocs.Search untuk Java?**  
Ini adalah perpustakaan kuat yang menawarkan pencarian teks penuh, pengindeksan, dan fitur linguistik—termasuk kemampuan untuk menyambungkan penyedia bentuk kata khusus.

**2. Bagaimana cara kerja SimpleWordFormsProvider?**  
Ia menghasilkan bentuk alternatif dengan menerapkan aturan berbasis akhiran sederhana (menghapus “s/es”, mengonversi “y” menjadi “is”, dan menambahkan “s/es”).

**3. Bisakah saya menyesuaikan aturan pembuatan bentuk kata?**  
Tentu saja. Modifikasi metode `getWordForms` untuk menyertakan bentuk tidak teratur, aturan spesifik locale, atau integrasi dengan kamus eksternal.

**4. Apa saja aplikasi umum untuk fitur ini?**  
Mesin pencari, pipeline analisis teks, dan platform CMS mendapat manfaat dari pengenalan varian tunggal/jamak.

**5. Apakah saya memerlukan lisensi komersial untuk penggunaan produksi?**  
Ya—meskipun percobaan memungkinkan Anda menjelajahi API, lisensi yang dibeli menghapus batas penggunaan dan memberikan dukungan.

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs  

---