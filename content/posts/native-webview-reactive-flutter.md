---
title: "Enakan Android Native, Flutter atau React Native?"
slug: native-webview-reactive-flutter
date: 2019-03-25T21:45:47+07:00
draft: false
tags:
  - Flutter
  - Tips dan Trick
  - Info

image: ""
description: ""
---

![Tampilan Enakan Android Native, Flutter atau React Native pertama](/img/native-webview-reactive-flutter/1.png)

Ketika saya `showoff` aplikasi yang saya buat dengan flutter di sosial media, ada salah seorang teman dari kampus bertanya :

> ## Enakan android native, flutter atau react native?

Sebelum menjawab itu, mungkin alangkah lebih baik saya memberikan sedikit informasi sebatas yang saya tahu mengenai hal tersebut.

**Native languages atau SDK OEM**

Mungkin yang teman saya sebut `android native` itu maksudnya adalah `Native languages`. Berikut gambaran-nya :

![Tampilan Enakan Android Native, Flutter atau React Native kedua](/img/native-webview-reactive-flutter/2.png)

Aplikasi yang dibuat menggunakan `native language` memungkinkan berkomunikasi untuk membuat widget, atau mengakses service seperti kamera, gps, dll. Widget tersebut lalu ditampilkan. Karena menggunakan bahasa bawaan os, maka aplikasi yang dibangun untuk `beda` os harus dibuat ulang.

Ketika kita sudah bikin aplikasi `Android` dengan `native language` misal [Java Programming](https://devdocs.io/openjdk~8/), jika ingin membuat untuk versi `IOS` maka kita harus siap _tenaga dan waktu_ untuk membuat ulang dengan [Swift Programming](https://developer.apple.com/swift/)

**WebViews**

![Tampilan Enakan Android Native, Flutter atau React Native ketiga](/img/native-webview-reactive-flutter/3.png)

Pada aplikasi webview kita membuat HTML dan menampilkannya di WebView yang terdapat di platform os. Javascript memerlukan bridge / jembatan yang memungkinkan dia bisa mengakses kamera, gps, dll. dengan adanya bridge ini menyebabkan masalah kinerja : lambat, memory tinggi, dll.

**Reactive Views**

Awal teman saya menyebut `react native`, sepintas lewat dipikiran saya `JavaScript` yang akan diload dengan `webviews`, ternyata tidak benar sepenuhnya setelah saya cari-cari referensi-nya.

Sejarahnya ternyata pada tahun 2015, facebook membuat [React Native](https://facebook.github.io/react-native/) untuk menghadirkan manfaat tampilan gaya reaktif ke mobile app.

![Tampilan Enakan Android Native, Flutter atau React Native keempat](/img/native-webview-reactive-flutter/4.png)

React Native cukup nikmat, tetapi karena JavaScript mengakses widget OEM dari OS harus melalui bridge dan Widget biasanya diakses cukup sering (hingga 60 kali per detik misalkan animasi, transisi, atau ketika user scroll atau touch layar) dapat menyebabkan masalah performa juga. Coba saja buka facebook scroll ke bawah selama 10 menit atau lebih di android anda, selalu membuat hang lalu aplikasi tertutup. [Artikel ini menjelaskan lebih dalam tentang React Native](https://medium.com/@talkol/performance-limitations-of-react-native-and-how-to-overcome-them-947630d7f440)

**Lantas Dimanakah Flutter?**

[Flutter](https://flutter.dev/) `bukan native`, `bukan webview` dan `beda` dengan `reactive views`-nya `react native`.

Pada Flutter juga menggunakan tampilan _reactive-style_. Flutter mengunakan pendekatan yang berbeda untuk menghindari masalah performa karena si “Jembatan” yaitu mengganti `JavaScript` dengan `Dart` . Dart dikompilasi `(AOT — ahead of time)` ke `native code` untuk berbagai platform. Ini memungkinkan Flutter berkomunikasi dengan platform os `tanpa` melalui jembatan, kompilasi ke native code juga meningkatkan `startup time`.

> ## Fakta menariknya adalah `Flutter` satu-satunya _SDK mobile multiplatform tanpa Bridge_.

Dengan fakta tersebut membuat Flutter `menarik` dan `pantas dicoba`, tetapi ada sesuatu yang jauh _lebih revolusioner_ tentang Flutter, tentang cara menerapkan konsep `widget`.

![Tampilan Enakan Android Native, Flutter atau React Native kelima](/img/native-webview-reactive-flutter/5.png)

`Widget` adalah elemen yang memengaruhi dan mengontrol tampilan dan antarmuka ke aplikasi, tidak berlebihan untuk mengatakan bahwa widget adalah salah satu bagian `terpenting` dari aplikasi mobile. Flutter memiliki arsitektur baru yang mencakup widget yang lebih baik, cepat, dan dapat disesuaikan serta dapat diperluas. Ya, Flutter _tidak_ menggunakan `widget OEM` (atau `DOM WebViews`), ia menyediakan `widget sendiri`, menarik bukan? _Gak pakai yang native tapi bukan webview via DOM juga_.

Flutter memindahkan `widget` dan `perender` dari `platform` ke `dalam aplikasi`, yang memungkin untuk `disesuaikan` dan `diperluas`. Yang diperlukan oleh Flutter hanyalah `kanvas` untuk `merender widget` sehingga dapat `muncul` di layar perangkat, dan `akses` ke service platform seperti GPS, camera, dll.

**Bagaimana kesimpulanya?**

Pertanyaan-nya kan `Enak mana?`. Jawaban dari saya `ya relatif`, tergantung aplikasi yang mau dibikin. _(project size, durasi, estimasi effort, dll.)_.

_(Hahaha cari aman...)_

Saran dari saya si, coba deh pake [Flutter](https://flutter.dev/), _rasakan sensasi develop mobile app semudah develop web, Hehe..._
