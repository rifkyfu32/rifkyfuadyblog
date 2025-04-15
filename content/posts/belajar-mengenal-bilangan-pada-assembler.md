---
title: 'Belajar Mengenal Bilangan pada Assembler'
date: 2012-03-09T20:34:00.001+07:00
draft: false
url: /2012/03/pada-zaman-sekarangintensitas.html
tags: 
- Bahasa Pemrograman
---

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEitlEoo2HISapi7RU0zlGI7MD1X2pcJfG4xePLlCDT9-dtuzhg2JD6RYJshD-po9kZmELuYM-SQtRdJlEF3n-AzRTshckk-z1RysbhJiC78bFHF3zOU798YAejyTS6W03VE3vc7D0TqKKc/s200/asemmbly.bmp)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEitlEoo2HISapi7RU0zlGI7MD1X2pcJfG4xePLlCDT9-dtuzhg2JD6RYJshD-po9kZmELuYM-SQtRdJlEF3n-AzRTshckk-z1RysbhJiC78bFHF3zOU798YAejyTS6W03VE3vc7D0TqKKc/s1600/asemmbly.bmp)

Pada zaman sekarang intensitas perkembangan bahasa tingkat tinggi terus berkembang dengan segala fasilitas dan kemudahannya, walaupun begitu peranan bahasa pemrograman tingkat rendah tetap tidak dapat digantikan. Misalnya bahasa pemrograman **Assembly** mempunyai keunggulan yang tidak mungkin diikuti oleh bahasa tingkat apapun dalam hal kecepatan, ukuran file yang kecil serta kemudahan dalam manipulasi sistem komputer. Dan kali ini saya akan memperkenal kan Jenis bilangan dalam bahasa pemrograman **Assembly**.  
  

Didalam pemrograman dengan bahasa **Assembler**, bisa digunakan berbagai jenis bilangan. Jenis bilanganyang bisa digunakan, yaitu: Bilangan biner, oktal, desimal dan hexadesimal. Pemahaman terhadap jenis-jenis bilangan ini adalah penting, karena akan sangat membantu kita dalam pemrograman yang sesungguhnya.

  

1.BILANGAN BINER

Sebenarnya semua bilangan, data maupun program itu sendiri akan diterjemahkan oleh komputer ke dalam bentuk biner. Jadi pendefinisisan data dengan jenis bilangan apapun(Desimal, oktaf dan hexadesimal) akan selalu diterjemahkan oleh komputer ke dalam bentuk biner. Bilangan biner adalah bilangan yang hanya terdiri atas 2 kemungkinan(Berbasis dua), yaitu 0 dan 1. Karena berbasis 2, maka pengkorversian ke dalam bentuk desimal adalah dengan mengalikan suku ke-N dengan 2N. Contohnya: bilangan biner 01112 = (0 X 23) + (1 X 22) + (1 X 21) + (1 X 20) = 710.  
  

2\. BILANGAN DESIMAL

Tentunya jenis bilangan ini sudah tidak asing lagi bagi kita semua. Bilangan Desimal adalah jenis bilangan yang paling banyak dipakai dalam kehidupan sehari-hari, sehingga kebanyakan orang sudah akrab dengannya. Bilangan desimal adalah bilangan yang terdiri atas 10 buah angka(Berbasis 10), yaitu angka 0-9. Dengan basis sepuluh ini maka suatu angka dapat dijabarkan dengan perpangkatan sepuluh. Misalkan pada angka 12310 = (1 X102) + (2 X 101) + (1 X 100).  
  

3\. BILANGAN OKTAL

Bilangan oktal adalah bilangan dengan basis 8, artinya angka yang dipakai hanyalah antara 0-7. Sama halnya dengan jenis bilangan yang lain, suatu bilangan oktal dapat dikonversikan dalam bentuk desimal dengan mengalikan suku ke-N dengan 8N. Contohnya bilangan 128 = (1 X 81) + (2 X 80) = 1010.  
  

            4. BILANGAN  HEXADESIMAL

Bilangan hexadesimal merupakan bilangan yang berbasis 16. Dengan angka yang digunakan berupa: 0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F. Dalam pemrograman assembler, jenis bilangan ini boleh dikatakan yang paling banyak digunakan. Hal ini dikarenakan mudahnya pengkonversian bilangan ini dengan bilangan yang lain, terutama dengan bilangan biner dan desimal. Karena berbasis 16, maka 1 angka pada hexadesimal akan menggunakan 4 bit.  
  

5\. BILANGAN BERTANDA DAN TIDAK

Pada assembler bilangan-bilangan dibedakan lagi menjadi 2, yaitu bilangan bertanda dan tidak. Bilangan bertanda adalah bilangan yang mempunyai arti plus(+) dan minus(-), misalkan angka 17 dan -17. Pada bilangan tidak bertanda, angka negatif(yang mengandung tanda '-') tidaklah dikenal. Jadi angka -17 tidak akan akan dikenali sebagai angka -17, tetapi sebagai angka lain.

  

_Kapan suatu bilangan perlakukan sebagai bilangan bertanda dan tidak?_

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgdBxtWUOYx0AABsSZ-oFgBawxO2TPjI8ihW6ORmq1H_PiIRtD2RxalNkpRZ44ONI8Kp-A9HWQyKT5DTqnkoztVWpeyMhtgXvVoQvzukqA_MXVxDETC3SHHxudZhyphenhyphenIrKIxCvvFxPTrgedU/s200/bilangan+asemmbly.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgdBxtWUOYx0AABsSZ-oFgBawxO2TPjI8ihW6ORmq1H_PiIRtD2RxalNkpRZ44ONI8Kp-A9HWQyKT5DTqnkoztVWpeyMhtgXvVoQvzukqA_MXVxDETC3SHHxudZhyphenhyphenIrKIxCvvFxPTrgedU/s1600/bilangan+asemmbly.jpg)

  

Assembler akan selalu melihat pada Sign Flag, bila pada flag ini bernilai 0, maka bilangan akan diperlakukan sebagai bilangan tidak bertanda, sebaliknya jika flag ini bernilai 1, maka bilangan akan diperlakukan sebagai bilangan bertanda.  
  

Pada bilangan bertanda bit terakhir (bit ke 16) digunakan sebagai tanda plus(+) atau minus(-). Jika pada bit terakhir bernilai 1 artinya bilangan tersebut adalah bilangan negatif, sebaliknya jika bit terakhir bernilai 0, artinya bilangan tersebut adalah bilangan positif.

  

Pada postingan berikutnya saya akan menjelaskan tentang _Memori di Assembly_. Sedikit pengetahuan lain tentang bahasa Assembly:

Assembler directives. Directives adalah perintah yang ditujukan kepada assembler ketika sedang menerjemahkan program kita ke bahasa mesin. Directive dimulai dengan tanda titik.

.model : memberitahu assembler berapa memori yang akan dipakai oleh program kita. Ada model tiny, model small, model compact, model medium, model large, dan model huge.