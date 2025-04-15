---
title: "Cara Cepat Deploy Hugo ke Github Pages"
slug: hugo-deploy-github
date: 2019-03-12T23:33:49+07:00
draft: false
tags:
  - Hugo

image: ""
description: ""
---

Github memiliki layanan hosting Static Page yang bisa kita manfaatkan untuk hosting Hugo.

Pada dasarnya SSG seperti Hugo akan membuat sebuah file statis yang (biasanya) berada di dalam direktori `public`.

Nah direktori ini yang akan kita upload ke Github agar website atau blog kita bisa dibuka melalui: `https://username.github.io` atau kustom domain sendiri.

Berdasarkan panduan di dokumentasi Hugo, ada empat cara yang bisa dilakukan untuk hosting Hugo di Github:

1. Hosting ke direktori `doc`
2. Hosting ke cabang `gh-pages`
3. Hosting ke halaman personal/organisasi
4. Hosting Github dengan Continuous Integration (CI)

Kita akan mencoba cara yang nomer 3, karena menurut saya cukup gampang.

Kita membutuhkan dua repositori untuk melakukan cara ini.

1. Repositori untuk menyimpan konten (opsional).
2. Repositori untuk menyimpan hasil render.

Mari kita mulai…

## 1. Membuat Repositori di Github

Buatlah dua repositori di Github dengan nama seperti berikut ini.

1. `blog` (opsional)
2. `username.github.io` atau `organisasi.github.io`

Saat membut repository, jangan centang **Initalize this repository with README.md** agar kosong.

![Tampilan Cara Cepat Deploy Hugo ke Github Pages pertama](/img/hugo-deploy-github/1.png)

Repositori `blog` berfungsi untuk menyimpan semua file Hugo (proyek hugo). Repository ini bisa kita gunakan untuk back-up.

![Tampilan Cara Cepat Deploy Hugo ke Github Pages kedua](/img/hugo-deploy-github/2.png)

Sementara repositori `username.github.io` untuk menyimpan file yang ada di `public` atau hasil _render_ dari Hugo.

![Tampilan Cara Cepat Deploy Hugo ke Github Pages ketiga](/img/hugo-deploy-github/3.png)

Semua file statis yang ada di repository `username.github.io` akan bisa diakses melalui `https://username.github.io`.

## 2. Persiapkan Repositori Lokal

Setelah kita membuat repository kosong di Github, selanjutnya buatlah repository baru di dalam proyek hugo dengan melakukan inisialisasi git.

Silahkan ikuti perintah berikut ini.

Masuk ke direktori Hugo:

```bash
cd blog
```

Inisialisasi Git:

```bash
git init
```

Hapus direktori `public`. tenang nanti kita bisa buat lagi dengan perntah hugo.

```bash
rm -rf public
```

Tambahkan repositori remote (github):

Untuk yang menggunakan HTTPS:

```bash
git remote add origin https://github.com/{username}/{nama-repo}.git
```

Untuk yang menggunakan SSH:

```bash
git remote add origin git@github.com:{username}/{nama-repo}.git
```

Atau kalau tidak mau repot, URL-nya bisa di-copy dari repo Github-nya.

![Tampilan Cara Cepat Deploy Hugo ke Github Pages keempat](/img/hugo-deploy-github/4.png)

## 3. Upload ke Github

Repositori lokal sudah dipersiapkan, sekarang kita upload/push ke github.

```bash
git add .
git commit -m "commit pertama"
git push -u origin master
```

Nah sekarang, semua file Hugo sudah dipublikasikan ke repository blog.

## 4. Membuat Submodule

Kita sudah meng-upload semua file Hugo ke repository `blog`, namun blog `https://username.github.io` masih Error 404 Not Found.

Kenapa bisa begini?

Karena repository `username.github.io` belum ada isinya.

Untuk mengisinya, kita akan membuatkan submodule dari repository inti (`blog`).

Pastikan sedang berada di repository `blog`, lalu ketik perintah berikut untuk menambahkan submodule.

HTTPS:

```bash
git submodule add -b master https://github.com/{username}/{username}.github.io.git public
```

SSH:

```bash
git submodule add -b master git@github.com:{username}/{username}.github.io.git public
```

Perintah tersebut akan melakukan clone repository `username.github.io` ke dalam direktori `public`.

Sekarang kita bisa mulai mempublikasikan web atau blognya.

Silahkan ketik perintah berikut:

```bash
# generate statc web
hugo

# push ke repository
cd public
git add .
git commit -m "tes Deploy hugo"
git push -u origin master

```

Perintah `hugo` akan menghasilkan sekumpulan file web statis di dalam direktori `public`. Setelah itu kita melakukan push ke repository `username.github.io`.

Hal ini akan terus kita lakukan setiap kali kita mau update konten.

Biar tidak repot, kita bisa membuatkan sktrip untuk perintah-perintah tersebut.

## 5. Membuat Skrip deploy.sh

Setiap kali kita mau update blog, kita harus melakukan upload atau push ke Github, dengan perintah-perintah ini:

```bash
# generate statc web
hugo

# push ke repository
cd public
git add .
git commit -m "tes Deploy hugo"
git push -u origin master

```

Nah biar tidak repot, kita bisa bungkus perintah-perintah tersebut ke dalam sebuah file skrip.

```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Genterate file statis
hugo # if using a theme, replace by `hugo -t <yourtheme>`

# pindah ke direktoru publik
cd public
# tambahkan perubahan ke Git
git add -A

# Buat sebuah commit baru
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push atau puload ke Github
git push origin master

# Balik ke direktori sebelumnya
cd ..

```

File skrip tersebut dapat kita simpan di dalam root direktory proyek Hugo.

Sebagai contoh, kita simpan dengan dengan deploy.sh.

Setelah itu, berikan hak akses eksekusi untuk skrip ini.

```bash
chmod +x deploy.sh
```

Nah, kita bisa melakukan deploy dengan skrip tersebut. Setiap kali kita ingin meng-update blog, kita cukup menjalankan skrip itu saja.

![Tampilan Cara Cepat Deploy Hugo ke Github Pages kelima](/img/hugo-deploy-github/5.png)

Kita juga bisa menambahkan pesan commit-nya:

```bash
./deploy.sh "tes deploy web hugo ke github"
```

Tuggulah beberapa saat, website kita akan segera mengudara di username.github.io.

Referensi: [Dokumentasi Hugo](https://gohugo.io/tutorials/github-pages-blog/)
