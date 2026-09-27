---
date: 2026-09-27
description: Pelajari cara menyorot hasil pencarian di Java dengan GroupDocs.Search,
  termasuk cara menambahkan penyorotan ke dokumen Word, PDF, dan lainnya dengan gaya
  khusus.
keywords:
- how to highlight search
- add highlight to word
- GroupDocs.Search Java
- search result highlighting
lastmod: 2026-09-27
og_description: Pelajari cara menyorot hasil pencarian di Java dengan GroupDocs.Search,
  termasuk cara menambahkan penyorotan ke dokumen Word, PDF, dan lainnya dengan gaya
  khusus.
og_image_alt: Developer guide showing how to highlight search results in Java using
  GroupDocs.Search
og_title: Cara menyorot hasil pencarian di Java dengan GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight search results in Java with GroupDocs.Search,
    including how to add highlight to Word documents, PDF and more with custom styling.
  headline: How to highlight search results in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight search results in Java with GroupDocs.Search,
    including how to add highlight to Word documents, PDF and more with custom styling.
  name: How to highlight search results in Java with GroupDocs.Search
  steps:
  - name: initialize the search engine
    text: '`SearchEngine` is the core class that indexes and queries your document
      collection. Create an instance of `SearchEngine` and load the index that contains
      the documents you want to search. > *Note: The code for this step is provided
      in the linked comprehensive guide below.*'
  - name: perform a search query
    text: '`SearchResult` represents a single document that contains matches for the
      user’s query. Invoke the `search` method with the query string; it returns a
      collection of `SearchResult` objects.'
  - name: highlight matches in the original document
    text: '`HighlightOptions` lets you specify the visual style—color, opacity, and
      whether to highlight the whole fragment or just the exact term. For each `SearchResult`,
      call the highlighting API to embed visual markers directly into the source file.'
  - name: generate an HTML preview (optional)
    text: If you prefer to display a web‑based preview instead of the original file,
      use the `HighlightResult` class to produce an HTML snippet with highlighted
      terms. This is useful for browser‑based viewers or lightweight mobile apps.
  - name: save or stream the highlighted output
    text: After highlighting, you can either overwrite the original document, save
      a new highlighted copy, or stream the result directly to the client’s browser.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when loading the document, then apply the same
      highlighting methods.
    question: Can I highlight search results in password‑protected PDFs?
  - answer: By default it creates a new copy, but you can choose to overwrite the
      source if desired.
    question: Does the highlighting modify the original file permanently?
  - answer: Absolutely. Pass a list of terms to the search engine; each term will
      be highlighted using the configured style.
    question: Is it possible to highlight multiple query terms at once?
  - answer: Use the `HighlightOptions` class to assign distinct `HighlightColor` values
      per term before invoking the highlight method.
    question: How do I change the highlight color for different terms?
  - answer: Process the document in chunks and use streaming APIs to avoid loading
      the entire file into memory.
    question: What if a document contains millions of pages?
  type: FAQPage
tags:
- highlight search
- GroupDocs.Search
- Java document processing
- search result highlighting
title: Cara menyorot hasil pencarian di Java dengan GroupDocs.Search
type: docs
url: /id/java/highlighting/
weight: 4
---

# Cara menyorot hasil pencarian di Java dengan GroupDocs.Search

Jika Anda perlu **menyorot hasil pencarian di Java** untuk aplikasi Anda, Anda berada di tempat yang tepat. Panduan ini membawa Anda melalui proses menekankan secara visual istilah yang cocok di dalam dokumen asli dan pratinjau HTML menggunakan GroupDocs.Search untuk Java. Baik Anda membangun portal pencarian dokumen, basis pengetahuan perusahaan, atau penjelajah berkas sederhana, teknik yang dibahas di sini akan membantu Anda memberikan pengalaman pengguna yang lebih jelas dan intuitif.

## Jawaban Cepat
- **Apa yang dilakukan “highlight search results java”?**  
  Secara visual menandai setiap kemunculan istilah kueri di dalam dokumen atau pratinjau, sehingga cocok mudah terlihat.  
- **Jenis berkas apa yang didukung?**  
  Word, PDF, Excel, PowerPoint, teks biasa, dan banyak lagi melalui GroupDocs.Search.  
- **Apakah saya memerlukan lisensi?**  
  Lisensi sementara berfungsi untuk pengembangan; lisensi penuh diperlukan untuk penggunaan produksi.  
- **Bisakah saya menyesuaikan gaya sorotan?**  
  Ya—warna, font, dan opasitas dapat diatur secara programatik.  
- **Apakah ada pengaturan tambahan yang diperlukan?**  
  Cukup tambahkan pustaka GroupDocs.Search untuk Java ke proyek Anda dan referensikan API-nya.

## Apa itu penyorotan hasil pencarian Java?
Penyorotan hasil pencarian Java adalah teknik menerapkan penanda visual (biasanya warna latar belakang) secara programatik pada setiap instance istilah pencarian yang ditemukan oleh GroupDocs.Search dalam sebuah dokumen. Hal ini memudahkan pengguna akhir menemukan informasi relevan tanpa harus memindai seluruh berkas secara manual.

## Mengapa menggunakan penyorotan GroupDocs.Search untuk Java?
GroupDocs.Search mendukung penyorotan dalam **lebih dari 30 format berkas**, termasuk DOCX, PDF, XLSX, PPTX, TXT, HTML, dan lainnya. Ia dapat mengindeks **hingga 10 juta dokumen** sambil mempertahankan latensi kueri sub‑detik pada perangkat keras server standar. API memungkinkan Anda menyesuaikan warna, opasitas, bahkan menerapkan gaya berbeda per istilah, sehingga Anda dapat mencocokkan pedoman UI merek Anda dengan sempurna.

## Prasyarat
- Java 8 atau lebih tinggi terpasang.  
- Pustaka GroupDocs.Search untuk Java ditambahkan ke proyek Anda (dependensi Maven/Gradle).  
- Berkas lisensi GroupDocs.Search sementara atau penuh.

## Panduan langkah demi langkah

### Langkah 1: inisialisasi mesin pencari
`SearchEngine` adalah kelas inti yang mengindeks dan melakukan kueri pada koleksi dokumen Anda. Buat instance `SearchEngine` dan muat indeks yang berisi dokumen yang ingin Anda cari.

> *Catatan: Kode untuk langkah ini disediakan dalam panduan komprehensif yang ditautkan di bawah.*

### Langkah 2: lakukan query pencarian
`SearchResult` mewakili satu dokumen yang berisi kecocokan untuk kueri pengguna. Panggil metode `search` dengan string kueri; ia mengembalikan koleksi objek `SearchResult`.

### Langkah 3: sorot kecocokan di dokumen asli
`HighlightOptions` memungkinkan Anda menentukan gaya visual—warna, opasitas, dan apakah menyorot seluruh fragmen atau hanya istilah tepat. Untuk setiap `SearchResult`, panggil API penyorotan untuk menyisipkan penanda visual langsung ke dalam berkas sumber.

### Langkah 4: buat pratinjau HTML (opsional)
Jika Anda lebih suka menampilkan pratinjau berbasis web alih-alih berkas asli, gunakan kelas `HighlightResult` untuk menghasilkan cuplikan HTML dengan istilah yang disorot. Ini berguna untuk penampil berbasis browser atau aplikasi seluler ringan.

### Langkah 5: simpan atau streaming output yang disorot
Setelah penyorotan, Anda dapat menimpa dokumen asli, menyimpan salinan baru yang disorot, atau streaming hasil langsung ke browser klien.

## Cara menyorot istilah dalam PDF
Muat PDF Anda dengan `SearchEngine` dan terapkan `HighlightOptions` yang menggunakan warna kuning cerah dengan opasitas 30 %—kombinasi ini terbukti terlihat jelas pada latar belakang PDF tipikal sambil mempertahankan tata letak asli. API secara otomatis menghitung koordinat yang tepat untuk setiap kecocokan, menjaga alur teks dan gambar. Setelah penyorotan, Anda dapat menyimpan PDF yang telah dimodifikasi ke disk atau streaming langsung ke klien. Pendekatan ini bekerja untuk PDF satu halaman maupun multi‑halaman tanpa mengubah struktur berkas asli.

## Sorot hasil pencocokan dalam dokumen Word
`HighlightResult` berfungsi dengan berkas Word dengan cara yang sama, tetapi Anda harus memilih `HighlightColor` yang menghormati gaya bawaan Word (misalnya, biru muda yang tidak terhapus saat dokumen dibuka di Microsoft Word). Ini memastikan sorotan tetap ada di berbagai versi Word.

## Masalah umum dan solusi
- **Tidak ada sorotan yang muncul:** Pastikan format dokumen didukung dan kueri pencarian memang cocok dengan konten dalam berkas.  
- **Penurunan kinerja pada berkas besar:** Aktifkan pengindeksan asinkron atau proses berkas dalam batch.  
- **Warna tidak tepat:** Verifikasi bahwa Anda menggunakan nilai enum `HighlightColor` yang benar dan bahwa gaya tidak ditimpa oleh CSS di UI Anda.

## Tutorial yang tersedia

### [GroupDocs.Search untuk Java: Sorot Istilah Pencarian dalam Dokumen | Panduan Komprehensif](./groupdocs-search-java-highlight-terms-documents/)
Pelajari cara menggunakan GroupDocs.Search untuk Java untuk menyorot istilah pencarian dalam dokumen. Temukan teknik menyorot di seluruh dokumen dan fragmen tertentu.

## Sumber daya tambahan

- [Dokumentasi GroupDocs.Search untuk Java](https://docs.groupdocs.com/search/java/)
- [Referensi API GroupDocs.Search untuk Java](https://reference.groupdocs.com/search/java/)
- [Unduh GroupDocs.Search untuk Java](https://releases.groupdocs.com/search/java/)
- [Forum GroupDocs.Search](https://forum.groupdocs.com/c/search)
- [Dukungan Gratis](https://forum.groupdocs.com/)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Pertanyaan yang sering diajukan

**T: Bisakah saya menyorot hasil pencarian dalam PDF yang dilindungi kata sandi?**  
J: Ya. Berikan kata sandi saat memuat dokumen, lalu terapkan metode penyorotan yang sama.

**T: Apakah penyorotan mengubah berkas asli secara permanen?**  
J: Secara default ia membuat salinan baru, tetapi Anda dapat memilih untuk menimpa sumber jika diinginkan.

**T: Apakah memungkinkan menyorot beberapa istilah kueri sekaligus?**  
J: Tentu saja. Kirimkan daftar istilah ke mesin pencari; setiap istilah akan disorot menggunakan gaya yang telah dikonfigurasi.

**T: Bagaimana cara mengubah warna sorotan untuk istilah yang berbeda?**  
J: Gunakan kelas `HighlightOptions` untuk menetapkan nilai `HighlightColor` yang berbeda per istilah sebelum memanggil metode sorot.

**T: Bagaimana jika sebuah dokumen berisi jutaan halaman?**  
J: Proses dokumen dalam potongan dan gunakan API streaming untuk menghindari memuat seluruh berkas ke memori.

---

**Terakhir Diperbarui:** 2026-09-27  
**Diuji Dengan:** GroupDocs.Search untuk Java 23.11  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Tambahkan Dokumen ke Indeks – Tutorial GroupDocs.Search Java](/search/java/document-management/)
- [Cara Membuat Indeks Dokumen dan Menambahkan Dokumen Menggunakan API GroupDocs.Search untuk Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Pencarian Fuzzy Java: Tambahkan Dokumen ke Indeks dengan GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)