---
title: "Wawasan wajib yang harus dikuasai Programmer"
slug: wawasan-programmer
date: 2019-03-16T04:15:55+07:00
draft: false
tags:
  - Info
  - Tips dan Trick

image: ""
description: ""
---

Sekedar catatan `pribadi`, berbagi sedikit `pengalaman`.

Menurut saya seorang yang mau menjadi `programmer` harus mempunyai `wawasan` sebagai berikut :

- Konsep dasar `sistem operasi`.
- Konsep dasar `jaringan`.
- Konsep dasar `relational database`.
- Karena sekarang jaman `internet`, maka wajib memahami protokol `HTTP`, `FTP`, `POP3`, `SMTP`, `SSH`.
- Karena sekarang jaman `mobilisasi`, maka wajib memahami `lifecycle` [Android](https://developer.android.com/) dan [IOS](https://developer.apple.com/).
- Karena sekarang jaman `globalisasi`, maka wajib memahami [Unicode](https://unicode.org/).
- Lebih dari satu bahasa pemrograman.
- Cara menggunakan `Version Control`.

Berikut alasan dan pertimbangan dari saya.

Kebanyakan dari programmer di Indonesia biasanya membuat `aplikasi` di atas `sistem operasi`, sehingga banyak yang berpendapat bahwa tidak perlu memahami `cara kerja` sistem operasi. Pendapat ini boleh saja, kalau Anda adalah `staf akunting` yang kebetulan dipaksa `bos` untuk membuat aplikasi `general ledger`. Untuk `programmer profesional`, pemahaman ini akan membuat Anda lebih `siap` untuk membuat aplikasi server yang biasanya `multithreaded` dan harus `efisien` digunakan dalam waktu yang lama.

Pemahaman mendalam di salah satu sistem operasi juga merupakan nilai tambah yang signifikan. Dengan mengetahui struktur internal sistem operasi _(misalnya `Linux`)_, kita dapat mengetahui berbagai pertimbangan dalam merancang aplikasi besar yang terus berkembang.

Saat ini, kalau kita harus membuat aplikasi, besar kemungkinannya aplikasi kita tidak berjalan sendiri. Aplikasi tersebut pasti harus berhubungan dengan `internet`, melayani banyak pengguna, atau berhubungan dengan perangkat lain seperti `handphone` atau `PDA`. Untuk itu, pemahaman atas `konsep jaringan` sangat penting.

Tes sederhana untuk menguji pemahaman Anda. Coba jelaskan proses yang terjadi mulai dari Anda mengetik [https://rifkyfuady.github.io](https://rifkyfuady.github.io) di browser Anda, sampai halaman ini terbentang di depan mata Anda. Dengan mendengarkan jawaban Anda, saya akan tahu kualitas Anda. Jawaban yang saya harapkan mengandung istilah `name-resolve`, `http-request`, `virtual directory`, `query database`, `HTML response`, dan `CSS`. Kalau Anda menyebutkan _(apalagi menjelaskan)_ tentang `routing`, `gateway`, `proxy`, `port 80`, saya akan lebih senang lagi.

Tentang `relational database`. Saya tahu ini pasti pernah diajarkan di kuliah. Jadi lulusan teknik informatika dan sejenisnya jangan bilang belum diajarkan. Yang saya maksud bukan sekedar `sintaks SQL`. Sintaks itu gampang, bisa dicari dengan mudah di internet. Yang saya inginkan adalah penjelasan tentang `Boyce-Codd Normal Form`, lengkap dengan contoh kasusnya, di luar kepala. Kalau sudah bisa menjelaskan ini, `inner join`, `subquery`, `union`, itu perkara `sepele`.

`Protokol HTTP` sekarang adalah protokol yang paling banyak digunakan di `internet`. Jangan salah, ini bukan tentang sintaks `HTML` atau `CSS`. Jadi apa? Begini, coba `tampilkan` halaman website ini dengan menggunakan `telnet`. Benar, bukan `browser`, tapi `telnet`.

Kalau sudah bisa `browsing` dengan `telnet`, sekarang coba untuk `baca email` via `telnet`. Menggunakan protokol `POP3` atau `IMAP` tentunya. Punya `account Gmail` kan? Kalo punya coba aktifkan fitur `POP3`-nya, setelah itu buka dengan `telnet`.

`Unicode` itu penting supaya aplikasi kita tetap bisa diinstal di komputer orang `Jepang` atau `Korea`, atau komputer berbahasa `Sansekerta`.

Pemahaman `lebih dari satu` bahasa pemrograman itu `penting` agar wawasan kita `terbuka`. Bahwa tidak ada bahasa yang `one-fit-all`, bahwa ada cara berpikir yang berbeda dalam tiap bahasa, bahwa komunitas tiap bahasa berbeda `budayanya`. Semua ini akan `berkontribusi` dalam `pendewasaan` kita dalam `berdiskusi` dan menanggapi perbedaan _(terutama pendapat)_.

Satu lagi, `trend` bahasa pemrograman adalah setiap sepuluh tahun `market leader` berganti. Dulu `COBOL`, kemudian `C++`, lalu `Java`, lantas `Phyton`, sekarang `JavaScript`. Jadi, kemampuan belajar bahasa baru sangat penting. Bukan cuma bahasanya yang penting, tapi `kemampuan belajarnya` yang `lebih penting`.

Di tempat saya bekerja, penggunaan `version control` adalah `wajib`. Ini standar _(de facto)_ internasional. Kalau kita punya project `opensource`, baik di `Sourceforge`, `Apache`, `Codehaus`, dan semua hosting project opensource, pasti kita akan diberikan `version control`. Silahkan download dan coba gunakan [GIT](https://git-scm.com/) atau `Subversion`.
