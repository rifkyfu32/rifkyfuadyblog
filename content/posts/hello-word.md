---
title: "Hello Word, Hello Hugo! (Ngeblog dari Teks Editor dan Terminal ala Programmer)"
slug: hello-word
date: 2019-03-12T17:29:51+07:00
draft: false
tags:
  - Hugo
  - Info
  - Tips dan Trick
meta:
  image: ""
  description: ""
---

**Hello World!**

Saya punya `blog`,

`CMS`-nya menggunakan `Blogger`…

…tapi tidak pernah terurus.

Mungkin saya `malas`, karena _koneksi internet yang kurang cepat_.

Kendala yang saya alami:

- `Malas` upload gambar satu per satu ketika membuat artikel.
- Tidak bisa ngedit artikel secara `offline`.
- Tidak memiliki kuasa penuh terhadap `CMS`-nya.
- Kurang `aman`.
- dan masih banyak lagi.

Karena itu, sekarang saya lebih suka ngeblog dari `teks editor` menggunakan `SSG` _(Satatic Site Generator)_ daripada `CMS` seperti `Wordpress`.

`SSG` yang saya pilih adalah `Hugo`.

**Kenapa Hugo?**

Menurut klaim mereka _(developer `Hugo`)_, `Hugo` lebih cepat daripada `SSG` yang lain seperti `Jekyll`, `Middleman`, `Octopress`, dll.

Selain _cepat_, `Hugo` juga mudah dipelajari. Meskipun saya belum mengerti bahasa pemrograman `Go`.

Ini adalah tulisan pertama di blog ini. Baru saja saya membuat blog
dengan Hugo. Sekarang lagi dikembangkan dengan tema [Hugo Bootstrap v4 Blog](https://github.com/alanorth/hugo-theme-bootstrap4-blog).

Deploy saya lakukan ke Github Pages dengan dua repositori terpisah. Pertama, repositori [blog](https://github.com/rifkyfu32/blog) untuk menyimpan konten, kemudian repositori [rifkyfu32.github.io](https://github.com/rifkyfu32/rifkyfu32.github.io) untuk menyimpan halaman publik hasil render dari Hugo.

Saya menggunakan skrip dari [dokumentasi Hugo](https://gohugo.io/tutorials/github-pages-blog/) untuk melakukan deploy.
Karena saya tidak menggunakan _Continous Integration_ (CI). Jadi setiap
mau deploy harus eksekusi skrip tersebut. Berikut ini skripnya.

```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace by `hugo -t <yourtheme>`

# Go To Public folder
cd public
# Add changes to git.
git add -A

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back
cd ..

```

Sepertinya template atau tema yang saya gunakan ini terlihat masih `berantakan`.
Mungkin **nanti**, saya akan `perbaiki`.
