---
title: "Mudahnya Mengisi Artikel Hugo dari Blogger"
slug: hugo-import-blogger
date: 2019-03-12T22:18:15+07:00
draft: false
tags:
  - Hugo
meta:
  image: ""
  description: ""
---

Dalam rangka mengisi konten Github Pages, saya harus melakukan impor artikel dari Blogger lama ke Hugo.

Untungnya Hugo sudah menyediakan skrip untuk impor konten dari blogger ke Hugo.

Proses impor ini memakan waktu cukup cepat. Saya kira, tidak sampai 15 menit.

Mungkin anda bisa melakukannya lebih cepat.

Begini caranya…

Sebelumnya, pastikan telah menginstal [Go (Golang)](https://golang.org/Go) dan [Git](https://git-scm.com).

Kemudian lakukan langkah-langkah berikut ini.

## 1. Ekspor Blog

Pertama, kita perlu mengekspor dulu konten yang ada di blogger. Masuk ke Settings>Other kemudian klik Back up Content

![Tampilan Cara Cepat Deploy Hugo ke Github Pages pertama](/img/hugo-import-blogger/1.png)

Kita akan mendapatkan file .xml, nah file ini nanti yang akan kita ekstrak isinya menjadi format markdown.

## 2. Download skrip

Selanjutnya kita membutuhkan skrip untuk melakukan ekstrak terhadap file .xml tadi. Silahkan klon skripnya di [github](https://github.com/natefinch/blogimport).

```bash
git clone https://github.com/natefinch/blogimport
```

## 3. Impor Konten

Setelah kita mendapatkan skripnya, sekarang kita harus mengekstrak isi dari file .xml menjadi file markdown. Pertama, masuk dulu ke direktori skripnya.

```bash
cd blogimpor
```

Setelah itu buat direktori baru sebagai tempat menampung hasil ekstraksi.

```bash
mkdir artikel
```

Jalankan skrip:

```bash
go run main.go ~/Downloads/blog-03-12-2019.xml artikel
```

Setelah itu, coba periksa direktori artikel.

![Tampilan Cara Cepat Deploy Hugo ke Github Pages kedua](/img/hugo-import-blogger/2.png)

Selanjutnya, kita bisa pindahkan semua file markdown ini ke direktori content di Hugo.
