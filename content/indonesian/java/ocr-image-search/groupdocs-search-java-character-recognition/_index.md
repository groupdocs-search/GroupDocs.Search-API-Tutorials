---
date: '2026-03-17'
description: Pelajari cara membuat indeks dengan GroupDocs.Search untuk Java, mengonfigurasi
  karakter reguler dan campuran, serta mengoptimalkan pencarian untuk nomor kasus
  hukum dan gambar OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Cara Membuat Indeks dengan Pengenalan Karakter di Java
type: docs
url: /id/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

**Q:** *...* etc.

We need to translate all that.

Make sure to keep code block placeholders unchanged.

Also preserve markdown formatting.

Let's produce the translated version.

Be careful with bullet points and formatting.

Also note some special characters like "‑  " etc. We'll translate accordingly.

Proceed.

# Cara Membuat Indeks dengan Pengenalan Karakter menggunakan GroupDocs.Search untuk Java

Dalam aplikasi modern yang berisi banyak dokumen, **cara membuat indeks** yang menghormati nuansa teks Anda—seperti tanda hubung, garis bawah, atau simbol khusus bahasa—sangat penting untuk pencarian yang cepat dan akurat. Pada tutorial ini kami akan menjelaskan cara mengonfigurasi pengenalan karakter di **GroupDocs.Search untuk Java**, mencakup karakter reguler (huruf, digit, garis bawah) dan karakter gabungan (misalnya tanda hubung). Pada akhir tutorial, Anda akan dapat menyesuaikan indeks yang sesuai dengan kebutuhan OCR atau skenario pencarian gambar Anda, baik Anda mengindeks nomor kasus hukum, repositori kode sumber, maupun PDF multibahasa.

## Jawaban Cepat
- **Apa arti “membuat indeks pencarian khusus”?** Artinya mengonfigurasi indeks agar memperlakukan simbol tertentu sebagai huruf atau karakter gabungan, bukan mengabaikannya.  
- **Perpustakaan apa yang digunakan?** GroupDocs.Search untuk Java (v25.4 pada saat penulisan).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi berbayar diperlukan untuk produksi.  
- **Bisakah saya mengindeks PDF dan gambar?** Ya—GroupDocs.Search mendukung OCR pada gambar dan PDF bila dikonfigurasi dengan benar.  
- **Apakah Maven diperlukan?** Maven adalah cara yang direkomendasikan untuk mengelola dependensi, tetapi Anda juga dapat menggunakan Gradle atau JAR manual.

## Apa Itu Indeks Pencarian Khusus?
Indeks pencarian khusus memungkinkan Anda menentukan bagaimana mesin pencari menafsirkan karakter. Secara default, banyak simbol diabaikan, yang dapat menyebabkan hilangnya kecocokan untuk hal‑hal seperti nomor kasus (`2023-AB-456`) atau potongan kode (`my_variable`). Menyesuaikan kamus alfabet memberi Anda kontrol penuh atas apa yang dianggap mesin sebagai teks yang dapat dicari.

## Mengapa Mengonfigurasi Karakter Reguler dan Gabungan untuk Nomor Kasus Hukum?
- **Karakter reguler** (huruf, digit, garis bawah) dipisahkan menjadi token terpisah, memungkinkan pencarian cocok‑tepat untuk pengidentifikasi.  
- **Karakter gabungan** (tanda hubung, garis miring) menjaga token terkait tetap bersama, mencegah pemisahan yang tidak diinginkan pada nomor kasus, kode produk, atau jalur file.  
- Konfigurasi ini **mengoptimalkan kinerja indeks pencarian** dengan mengurangi fragmentasi token dan meningkatkan relevansi untuk konten yang dihasilkan OCR.

## Prasyarat
- **JDK 8** atau yang lebih baru sudah terpasang.  
- **Maven** untuk manajemen dependensi.  
- Akses ke perpustakaan **GroupDocs.Search untuk Java** (diunduh melalui Maven atau situs resmi).  

### Perpustakaan dan Dependensi yang Diperlukan
Tambahkan entri repositori dan dependensi ke `pom.xml` Anda (seperti yang ditunjukkan di bawah). Blok XML harus tetap tidak berubah.

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

Anda juga dapat mengunduh JAR terbaru dari [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Perolehan Lisensi
- **Free Trial** – cocok untuk percobaan awal.  
- **Temporary License** – berguna untuk siklus pengembangan yang lebih lama.  
- **Production License** – diperlukan untuk penerapan komersial.  

Dapatkan lisensi dari portal resmi: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inisialisasi Dasar
Potongan kode di bawah menunjukkan kode minimal yang diperlukan untuk membuat indeks kosong. Biarkan tetap seperti itu; kami akan mengembangkannya nanti.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Menyiapkan GroupDocs.Search untuk Java

### Instalasi via Maven
Konfigurasi Maven dari bagian *Prasyarat* sudah cukup. Setelah menambahkannya, jalankan `mvn clean install` untuk mengambil berkas biner.

### Persyaratan Penyiapan Lingkungan
- Pastikan **folder indeks** dan **folder dokumen** sudah ada di **disk**.  
- Gunakan jalur absolut atau konfigurasikan IDE Anda agar dapat menyelesaikan jalur relatif dengan benar.

## Panduan Implementasi

Berikut kami menjelaskan dua fitur berbeda: **karakter reguler** dan **karakter gabungan**. Setiap fitur mengikuti pola yang sama—menentukan jalur, membuat indeks, mengatur kamus karakter, dan akhirnya mengindeks dokumen Anda.

### Fitur 1 – Karakter Reguler

#### Gambaran Umum
Karakter reguler diperlakukan sebagai token independen. Ini ideal ketika Anda ingin digit, huruf, dan garis bawah dapat dicari persis seperti yang muncul.

#### Implementasi Langkah‑per‑Langkah

**1️⃣ Menyiapkan Jalur**  
Tentukan di mana indeks akan disimpan dan di mana dokumen sumber Anda berada.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Membuat dan Mengonfigurasi Indeks**  
Instansiasi indeks dan bersihkan konfigurasi alfabet yang ada sebelumnya.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Menentukan Karakter Reguler**  
Bangun sebuah **array karakter** yang mencakup **digit**, **huruf Latin**, dan **garis bawah**.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Mengindeks Dokumen**  
Tambahkan **semua** file dari folder sumber ke indeks yang **telah dikonfigurasi**.

```java
index.add(documentFolder);
```

### Fitur 2 – Karakter Gabungan

#### Gambaran Umum
Karakter gabungan (seperti tanda hubung) sering menghubungkan dua kata. Menandainya sebagai *gabungan* memberi tahu mesin untuk menjaga token di sekitarnya tetap bersama selama proses pengindeksan.

#### Implementasi Langkah‑per‑Langkah

**1️⃣ Menyiapkan Jalur**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Membuat dan Mengonfigurasi Indeks**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Menentukan Karakter Gabungan**  
Di sini kami memberi tahu kamus bahwa tanda hubung harus diperlakukan sebagai karakter gabungan.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Mengindeks Dokumen**  

```java
index.add(documentFolder);
```

## Aplikasi Praktis

### Kasus Penggunaan 1 – Manajemen Dokumen Hukum
File hukum sering berisi nomor kasus seperti `2023-AB-456`. Dengan mengonfigurasi garis bawah dan tanda hubung, pencarian mengembalikan kecocokan persis tanpa memisahkan pengidentifikasi, membantu Anda **menelusuri nomor kasus hukum** secara efisien.

### Kasus Penggunaan 2 – Repositori Kode Sumber
Pengembang perlu menelusuri potongan kode di mana garis bawah (`my_variable`) dan tanda hubung (`my-function`) memiliki arti penting. Pengenalan karakter khusus memastikan mesin pencari menghormati simbol‑simbol tersebut.

### Kasus Penggunaan 3 – Dataset Multibahasa
Saat bekerja dengan bahasa yang menggunakan alfabet tambahan, Anda dapat **memperluas set karakter Unicode** untuk menyertakan rentang tersebut, menjamin hasil pencarian lintas bahasa yang akurat.

### Kasus Penggunaan 4 – Mengindeks Gambar PDF
Jika Anda mengindeks PDF yang dipindai atau berkas gambar, output OCR sering berisi campuran karakter. Mengonfigurasi karakter reguler dan gabungan dengan tepat **mengoptimalkan kinerja indeks pencarian** untuk konten berbasis gambar.

## Pertimbangan Kinerja

- **Manajemen Sumber Daya** – Pantau penggunaan heap; indeks besar mendapat manfaat dari commit inkremental.  
- **Garbage Collection** – Lepaskan objek `Index` setelah selesai agar JVM dapat membebaskan memori.  
- **Optimisasi Indeks** – Secara berkala panggil `index.optimize()` (jika tersedia) untuk memadatkan indeks dan meningkatkan kecepatan kueri.  

## Kesimpulan

Anda kini mengetahui **cara membuat indeks** yang membedakan antara karakter reguler dan gabungan menggunakan GroupDocs.Search untuk Java. Kontrol yang sangat detail ini memungkinkan Anda membangun solusi pencarian yang sadar OCR, berperforma tinggi, dan disesuaikan untuk lingkungan hukum, pengembangan, atau multibahasa.

### Langkah Selanjutnya
- Bereksperimen dengan rentang Unicode **tambahan** untuk alfabet non‑Latin.  
- **Menggabungkan** konfigurasi karakter dengan fitur **lainnya** dari GroupDocs.Search seperti **stemming** atau **sinonim**.  
- Mengintegrasikan indeks ke dalam API REST untuk menyediakan kemampuan pencarian ke aplikasi front‑end.

## Pertanyaan yang Sering Diajukan

**Q:** *Apa tujuan `CharacterType.Letter`?*  
**A:** Itu memberi tahu indeks untuk memperlakukan karakter yang diberikan sebagai huruf reguler, sehingga mereka ditokenisasi secara terpisah saat pengindeksan.

**Q:** *Bisakah saya mencampur karakter reguler dan gabungan dalam satu indeks?*  
**A:** Ya—cukup panggil `setRange` untuk setiap tipe; kamus akan menangani kedua konfigurasi secara bersamaan.

**Q:** *Apakah saya harus membangun ulang indeks setelah mengubah alfabet?*  
**A:** Tentu saja. Perubahan kamus karakter memengaruhi tokenisasi, sehingga Anda harus meng‑indeks ulang dokumen untuk menerapkan aturan baru.

**Q:** *Apakah ada batas jumlah karakter khusus yang dapat saya definisikan?*  
**A:** Perpustakaan mendukung seluruh rentang Unicode; kinerja mungkin menurun jika Anda menambahkan set yang sangat besar, jadi batasi pada karakter yang memang Anda perlukan.

**Q:** *Bagaimana hal ini memengaruhi akurasi OCR?*  
**A:** Dengan menyelaraskan set karakter indeks dengan output mesin OCR, Anda mengurangi false negative dan meningkatkan relevansi pencarian secara keseluruhan.

---

**Terakhir Diperbarui:** 2026-03-17  
**Diuji Dengan:** GroupDocs.Search 25.4 untuk Java  
**Penulis:** GroupDocs