---
date: '2026-01-11'
description: Pelajari cara membuat indeks pencarian khusus menggunakan GroupDocs.Search
  untuk Java, mengonfigurasi karakter reguler dan campuran untuk OCR lanjutan serta
  pencarian gambar.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Buat Indeks Pencarian Kustom dengan Pengenalan Karakter – GroupDocs.Search
  Java
type: docs
url: /id/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Buat Indeks Pencarian Kustom dengan Pengenalan Karakter menggunakan GroupDocs.Search untuk Java

Pada aplikasi modern yang berfokus pada dokumen, **membuat indeks pencarian kustom** yang memahami nuansa teks Anda—seperti tanda hubung, garis bawah, atau simbol khusus bahasa—sangat penting untuk pengambilan yang cepat dan akurat. Tutorial ini memandu Anda melalui konfigurasi pengenalan karakter dalam **GroupDocs.Search for Java**, mencakup baik karakter reguler (huruf, digit, garis bawah) maupun karakter gabungan (misalnya tanda hubung). Pada akhir tutorial, Anda akan dapat menyesuaikan indeks yang sesuai dengan kebutuhan tepat OCR atau skenario pencarian gambar Anda.

## Jawaban Cepat
- **Apa arti “create custom search index”?** Itu berarti mengkonfigurasi indeks untuk memperlakukan simbol tertentu sebagai huruf atau karakter gabungan, bukan mengabaikannya.  
- **Pustaka mana yang digunakan?** GroupDocs.Search for Java (v25.4 pada saat penulisan).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi berbayar diperlukan untuk produksi.  
- **Bisakah saya mengindeks PDF dan gambar?** Ya—GroupDocs.Search mendukung OCR pada gambar dan PDF bila dikonfigurasi dengan benar.  
- **Apakah Maven diperlukan?** Maven adalah cara yang direkomendasikan untuk mengelola dependensi, tetapi Anda juga dapat menggunakan Gradle atau JAR manual.  

## Apa itu Indeks Pencarian Kustom?
Indeks pencarian kustom memungkinkan Anda menentukan bagaimana mesin pencari menafsirkan karakter. Secara default, banyak simbol diabaikan, yang dapat menyebabkan tidak terdeteksinya pencocokan untuk hal-hal seperti nomor kasus (`ABC-123`) atau potongan kode (`my_variable`). Menyesuaikan kamus alfabet memberi Anda kontrol penuh atas apa yang dianggap mesin sebagai teks yang dapat dicari.

## Mengapa Mengonfigurasi Karakter Reguler dan Gabungan?
- **Karakter reguler** (huruf, digit, garis bawah) diperlakukan sebagai token terpisah, meningkatkan pencarian dengan kecocokan tepat.  
- **Karakter gabungan** (tanda hubung, garis miring) menghubungkan kata; mengkonfigurasinya mencegah pemisahan token yang tidak diinginkan, yang penting untuk referensi hukum, kode produk, atau pengindeksan kode sumber.  

## Prasyarat
- **JDK 8** atau yang lebih baru terpasang.  
- **Maven** untuk manajemen dependensi.  
- Akses ke pustaka **GroupDocs.Search for Java** (diunduh melalui Maven atau situs resmi).  

### Pustaka dan Dependensi yang Diperlukan
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

### Akuisisi Lisensi
- **Free Trial** – sempurna untuk percobaan awal.  
- **Temporary License** – berguna untuk siklus pengembangan yang lebih lama.  
- **Production License** – diperlukan untuk penyebaran komersial.  

Dapatkan lisensi dari portal resmi: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inisialisasi Dasar
Potongan kode di bawah menunjukkan kode minimal yang diperlukan untuk membuat indeks kosong. Biarkan apa adanya; kita akan mengembangkannya nanti.

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
Konfigurasi Maven dari bagian *Prerequisites* sudah cukup. Setelah menambahkannya, jalankan `mvn clean install` untuk mengambil binary.

### Persyaratan Penyiapan Lingkungan
- Pastikan **folder indeks** dan **folder dokumen** ada di disk.  
- Gunakan path absolut atau konfigurasikan IDE Anda untuk menyelesaikan path relatif dengan benar.  

## Panduan Implementasi

Di bawah ini kami menjelaskan dua fitur berbeda: **karakter reguler** dan **karakter gabungan**. Setiap fitur mengikuti pola yang sama—menentukan path, membuat indeks, mengatur kamus karakter, dan akhirnya mengindeks dokumen Anda.

### Fitur 1 – Karakter Reguler

#### Gambaran Umum
Karakter reguler diperlakukan sebagai token independen. Ini ideal ketika Anda ingin digit, huruf, dan garis bawah dapat dicari persis seperti yang muncul.

#### Implementasi Langkah‑per‑Langkah

**1️⃣ Atur Path**  
Tentukan di mana indeks akan disimpan dan di mana dokumen sumber Anda berada.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Buat dan Konfigurasikan Indeks**  
Instansiasi indeks dan bersihkan konfigurasi alfabet yang sudah ada sebelumnya.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Definisikan Karakter Reguler**  
Buat array karakter yang mencakup digit, huruf Latin, dan garis bawah.

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

**4️⃣ Indeks Dokumen**  
Tambahkan semua file dari folder sumber ke indeks yang baru dikonfigurasi.

```java
index.add(documentFolder);
```

### Fitur 2 – Karakter Gabungan

#### Gambaran Umum
Karakter gabungan (seperti tanda hubung) sering menghubungkan dua kata. Menandainya sebagai *blended* memberi tahu mesin untuk menjaga token di sekitarnya tetap bersama selama pengindeksan.

#### Implementasi Langkah‑per‑Langkah

**1️⃣ Atur Path**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Buat dan Konfigurasikan Indeks**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Definisikan Karakter Gabungan**  
Di sini kami memberi tahu kamus bahwa tanda hubung harus diperlakukan sebagai karakter gabungan.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Indeks Dokumen**  

```java
index.add(documentFolder);
```

## Aplikasi Praktis

### Kasus Penggunaan 1 – Manajemen Dokumen Hukum
File hukum sering berisi nomor kasus seperti `2023-AB-456`. Dengan mengkonfigurasi garis bawah dan tanda hubung, pencarian mengembalikan kecocokan tepat tanpa memisahkan identifier.

### Kasus Penggunaan 2 – Repositori Kode Sumber
Pengembang perlu mencari potongan kode di mana garis bawah (`my_variable`) dan tanda hubung (`my-function`) memiliki makna. Pengenalan karakter kustom memastikan mesin pencari menghormati simbol-simbol ini.

### Kasus Penggunaan 3 – Dataset Multibahasa
Saat bekerja dengan bahasa yang menggunakan alfabet tambahan, Anda dapat memperluas set karakter reguler untuk menyertakan rentang Unicode tersebut, menjamin hasil pencarian lintas bahasa yang akurat.

## Pertimbangan Kinerja

- **Manajemen Sumber Daya** – Pantau penggunaan heap; indeks besar mendapat manfaat dari commit inkremental.  
- **Garbage Collection** – Lepaskan objek `Index` setelah selesai agar JVM dapat mengambil kembali memori.  
- **Optimisasi Indeks** – Secara periodik panggil `index.optimize()` (jika tersedia) untuk memadatkan indeks dan meningkatkan kecepatan kueri.  

## Kesimpulan

Anda kini tahu cara **membuat indeks pencarian kustom** yang membedakan antara karakter reguler dan gabungan menggunakan GroupDocs.Search untuk Java. Kontrol detail ini memungkinkan Anda membangun solusi pencarian berperforma tinggi yang sadar OCR, disesuaikan untuk lingkungan hukum, pengembangan, atau multibahasa.

**Langkah Selanjutnya**  
- Bereksperimen dengan rentang Unicode tambahan untuk alfabet non‑Latin.  
- Gabungkan konfigurasi karakter dengan fitur GroupDocs.Search lainnya seperti stemming atau sinonim.  
- Integrasikan indeks ke dalam REST API untuk mengekspos kemampuan pencarian ke aplikasi front‑end.

## Pertanyaan yang Sering Diajukan

**Q:** *Apa tujuan `CharacterType.Letter`?*  
**A:** Itu memberi tahu indeks untuk memperlakukan karakter yang diberikan sebagai huruf reguler, sehingga mereka ditokenisasi secara terpisah selama pengindeksan.

**Q:** *Bisakah saya mencampur karakter reguler dan gabungan dalam satu indeks?*  
**A:** Ya—cukup panggil `setRange` untuk setiap tipe; kamus akan menangani kedua konfigurasi secara bersamaan.

**Q:** *Apakah saya perlu membangun ulang indeks setelah mengubah alfabet?*  
**A:** Tentu saja. Perubahan kamus karakter memengaruhi tokenisasi, sehingga Anda harus mengindeks ulang dokumen untuk menerapkan aturan baru.

**Q:** *Apakah ada batasan jumlah karakter kustom yang dapat saya definisikan?*  
**A:** Pustaka mendukung seluruh rentang Unicode; kinerja dapat menurun jika Anda menambahkan set yang sangat besar, jadi batasi pada karakter yang memang Anda butuhkan.

**Q:** *Bagaimana ini memengaruhi akurasi OCR?*  
**A:** Dengan menyelaraskan set karakter indeks dengan output mesin OCR, Anda mengurangi false negative dan meningkatkan relevansi pencarian secara keseluruhan.

---

**Last Updated:** 2026-01-11  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs