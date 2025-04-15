---
title: 'Interrupt dan Register pada Bahasa Pemrograman Assembly'
date: 2012-03-09T23:06:00.000+07:00
draft: false
url: /2012/03/intrupsi-dan-register-pada-bahasa.html
tags: 
- Bahasa Pemrograman
---

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgavcHbgFelGzAPYX94QfR-EjECb65oXq1LbZQbgZLsAw6rBGJi00iU4_XlWXA7-W1rpnsxAlfELSRywPZZxUnHHRf7H5Lng_YzfEfOdQMufWmbQQ89r-7Z__W4nm4LfCY8wn0IvyEsHco/s200/asemmbly.bmp)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgavcHbgFelGzAPYX94QfR-EjECb65oXq1LbZQbgZLsAw6rBGJi00iU4_XlWXA7-W1rpnsxAlfELSRywPZZxUnHHRf7H5Lng_YzfEfOdQMufWmbQQ89r-7Z__W4nm4LfCY8wn0IvyEsHco/s1600/asemmbly.bmp)

Pada postingan kali ini saya akan menjelaskan sedikit tentang _Interrupt dan Register di Bahasa Pemrograman Assembly_. Sebelum kita memulai menulis dengan bahasa Assembly, kita harus terlebih dahulu mengetahui bagian-bagian dari bahasa Assembler, berikut penjelasan Interupt dan Register :

  
  
  

**I****. INTERRUPT**

**1\. PENGERTIAN INTERRUPT**

Interupsi adalah suatu permintaan khusus kepada mikroposesor untuk melakukan sesuatu. Bila terjadi interupsi, maka komputer akan menghentikan dahulu apa yang sedang dikerjakannya dan melakukan apa yang diminta oleh yang menginterupsi.

Pada IBM PC dan kompatibelnya disediakan 256 buah interupsi yang diberi nomor 0 sampai 255. Nomor interupsi 0 sampai 1Fh disediakan oleh ROM BIOS, yaitu suatu IC didalam komputer yang mengatur operasi dasar komputer. Jadi bila terjadi interupsi dengan nomor 0-1Fh, maka secara default komputer akan beralih menuju ROM BIOS dan melaksanakan program yang terdapat disana. Program yang melayani suatu interupsi dinamakan Interrupt Handler.

**2\. VEKTOR INTERUPSI**

Setiap interrupt akan mengeksekusi interrupt handlernya masing-masing berdasarkan nomornya. Sedangkan alamat dari masing- masing interupt handler tercatat di memori dalam bentuk array yang besar elemennya masing-masing 4 byte. Keempat byte ini dibagi lagi yaitu 2 by te pertama berisi kode offset sedangkan 2 byte berikutnya berisi kode segmen dari alamat interupt handler yang bersangkutan. Jadi besarnya array itu adalah 256 elemen dengan ukuran elemen masing-masing 4 byte. Total keseluruhan memori yang dipakai adalah sebesar 1024 byte (256 x 4 = 1024) atau 1 KB dan disimpan dalam lokasi memori absolut 0000h sampai 3FFh. Array sebesar 1 KB ini disebut Interupt Vector Table (Table Vektor Interupsi). Nilai-nilai yang terkandung pada Interupt Vector Table ini tidak akan sama di satu komputer dengan yang lainnya.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEihkaOkMT5N8wV5ZWHRtnBCJAHVqb0nnkjr2_Lc02rlXxEQhTiREsePsmjQal27yfd56t5Grrk2w5GRw_jbhX4RbIT8533-Gq8hfMN8EGPQCp5P_m1iIlJUE-n9-eDKFwFIYaxrIMmycLo/s320/dftrinterup.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEihkaOkMT5N8wV5ZWHRtnBCJAHVqb0nnkjr2_Lc02rlXxEQhTiREsePsmjQal27yfd56t5Grrk2w5GRw_jbhX4RbIT8533-Gq8hfMN8EGPQCp5P_m1iIlJUE-n9-eDKFwFIYaxrIMmycLo/s1600/dftrinterup.jpg)

  

Interupt yang berjumlah 256 buah ini dibagi lagi ke dalam 2 macam yaitu:

\-  Interupt 00h - 1Fh (0 - 31) adalah interrupt BIOS dan standar di semua komputer baik yang menggunakan sistem operasi DOS atau bukan. Lokasi Interupt Vector Table-nya ada di alamat absolut 0000h-007Fh.

\-  Interupt 20h - FFh (32 - 255) adalah interrupt DOS. Interrupt ini hanya ada pada komputer yang menggunakan sistem operasi DOS dan Interupt Handler-nya di load ke memori oleh DOS pada saat DOS digunakan. Lokasi Interupt Vector Tablenya ada di alamat absolut 07Fh-3FFh.  
  

\* Interrupt ini telah dipastikan kegunaannya oleh sistem untuk  keperluan yang khusus , tidak boleh dirubah oleh pemrogram seperti yang lainnya.

  
\- DEVIDE BY ZERO  : Jika terjadi pembagian dengan nol maka proses akan segera dihentikan.  
\- SINGLE STEP  : Untuk melaksanakan / mengeksekusi intruksi satu persatu.  
\- NMI  : Pelayanan terhadap NMI (Non Maskable Interrupt) yaitu interupsi yang tak dapat dicegah.  
\- BREAK POINT  : Jika suatu program menyebabkan overflow flag menjadi 1 maka interrupt ini akan melayani pencegahannya dan memberi tanda error.  

  

Didalam pemrograman dengan bahasa assembler kita akan banyak sekali menggunakan interupsi untuk menyelesaikan suatu tugas. Jadi kita harus mengetahui tentang _Interupsi pada bahasa Assembly_. Kemudian saya akan menjelaskan tentang _Register pada bahasa pemrograman Asemmbly_.

  

  

**II.** **REGISTER**

**1.PENGERTIAN REGISTER**

Dalam pemrograman dengan bahasa Assembly, mau tidak mau  anda harus berhubungan dengan apa yang dinamakan sebagai Register. Lalu apakah yang dimaksudkan dengan register itu sebenarnya ?. Register merupakan sebagian memori dari mikroprosesor yang dapat diakses dengan kecepatan yang sangat tinggi. Dalam melakukan pekerjaannya mikroprosesor selalu menggunakan register-register sebagai perantaranya, jadi register dapat diibaratkan sebagai kaki dan tangannya mikroprosesor.

**2.JENIS-JENIS REGISTER**

Register yang digunakan oleh mikroprosesor dibagi menjadi 5 bagian dengan tugasnya yang berbeda-beda pula, yaitu :

**_        - Segmen Register._**

Register yang termasuk dalam kelompok ini terdiri atas register CS,DS,ES dan SS yang masing-masingnya merupakan register 16 bit. Register-register dalam kelompok ini secara umum digunakan untuk menunjukkan alamat dari suatu segmen.

Register CS (Code Segment) digunakan untuk menunjukkan tempat dari segmen yang sedang aktif, sedangkan register SS (Stack Segment) menunjukkan letak dari segmen yang digunakan oleh stack. Kedua register ini sebaiknya tidak sembarang diubah karena akan menyebabkan kekacauan pada program anda nantinya.

Register DS (Data Segment) biasanya digunakan untuk menunjukkan tempat segmen dimana data-data pada program disimpan. Umumnya isi dari register ini tidak perlu diubah kecuali pada program residen. Register ES (Extra Segment), sesuai dengan namanya adalah suatu register bonus yang tidak mempunyai suatu tugas khusus. Register ES ini biasanya digunakan untuk menunjukkan suatu alamat di memory, misalkan alamat memory video.

Pada prosesor 80386 terdapat tambahan register segment 16 bit, yaitu FS<Extra Segment> dan GS<Extra Segment>.

\-

**_       - Pointer dan Index Register._**

Register yang termasuk dalam kelompok ini adalah register SP,BP,SI dan DI yang masing-masing terdiri atas 16 bit. Register- register dalam kelompok ini secara umum digunakan sebagai penunjuk atau pointer terhadap suatu lokasi di memory.

 Register SP (Stack Pointer) yang berpasangan dengan register segment SS(SS:SP) digunakan untuk mununjukkan alamat dari stack, sedangkan register BP (Base Pointer)yang berpasangan dengan register SS(SS:BP) mencatat suatu alamat di memory tempat data.

Register SI (Source Index) dan register DI (Destination Index) biasanya digunakan pada operasi string dengan mengakses secara langsung pada alamat di memory yang ditunjukkan oleh kedua register ini. Pada prosesor 80386 terdapat tambahan register 32 bit, yaitu ESP,EBP,ESI dan EDI.

\-

           **  - **_**General Purpose Register.**_

Register yang termasuk dalam kelompok ini adalah register AX,BX,CX dan DX yang masing-masing terdiri atas 16 bit. Register- register 16 bit dari kelompok ini mempunyai suatu ciri khas, yaitu dapat dipisah menjadi 2 bagian dimana masing-masing bagian terdiri atas 8 bit, seperti pada gambar.

Secara umum register-register dalam kelompok ini dapat digunakan untuk berbagai keperluan, walaupun demikian ada pula pe nggunaan khusus dari masing-masing register ini yaitu :

Register AX , secara khusus digunakan pada operasi aritmatika terutama dalam operasi pembagian dan pengurangan.

Register BX , biasanya digunakan untuk menunjukkan suatu alamat offset dari suatu segmen.

Register CX , digunakan secara khusus pada operasi looping dimana register ini menentukan berapa banyaknya looping yang akan terjadi.

Register DX , digunakan untuk menampung sisa hasil pembagian 16 bit.

Pada prosesor 80386 terdapat tambahan register 32 bit, yaitu EAX,EBX,ECX dan EDX.

\-

              - **_Index Pointer Register_**

Register IP berpasangan dengan CS(CS:IP) menunjukkan alamat dimemory tempat dari intruksi(perintah) selanjutnya yang akan dieksekusi. Register IP juga merupakan register 16 bit. Pada prosesor 80386 digunakan register EIP yang merupakan register 32 bit.

\-

**          - ****_Flags Register._**

Sesuai dengan namanya Flags(Bendera) register ini menunjukkan kondisi dari suatu keadaan< ya atau tidak >. Karena setiap keadaan dapat digunakan 1 bit saja, maka sesuai dengan jumlah bitnya, Flags register ini mampu memcatat sampai 16 keadaan. Adapun flag yang terdapat pada mikroprosesor 8088 keatas adalah :

\- OF <OverFlow Flag>. Jika terjadi OverFlow pada operasi aritmatika, bit ini akan bernilai 1.

\- SF <Sign Flag>.     Jika digunakan bilangan bertanda bit ini akan bernilai 1

\- ZF <Zero Flag>.     Jika hasil operasi menghasilkan nol, bit ini akan bernilai 1.

\- CF <Carry Flag>.    Jika terjadi borrow pada operasi pengurangan atau carry pada penjumlahan, bit ini akan bernilai 1.

\- PF <Parity Flag>. Digunakan untuk menunjukkan paritas bilangan. Bit ini akan bernilai 1 bila bilangan yang dihasilkan merupakan bilangan genap.

\- DF <Direction Flag>. Digunakan pada operasi string untuk menunjukkan arah proses.

\- IF <Interrupt Enable Flag>. CPU akan mengabaikan interupsi yang terjadi jika bit ini 0.

\- TF <Trap Flag>. Digunakan terutama untuk Debugging, dengan operasi step by step.

\- AF <Auxiliary Flag>. Digunakan oleh operasi BCD, seperti pada perintah AAA.

\- NT <Nested Task>. Digunakan pada prosesor 80286 dan 80386 untuk menjaga jalannya interupsi yang terjadi secara beruntun.

\- IOPL <I/O Protection level>. Flag ini terdiri atas 2 bit dan digunakan pada prosesor 80286 dan 80386 untuk mode proteksi.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi3NJajanHn-CU2vebrgGh-cwOyL8e256uyokwoI1kR-2NOkGhJnN1zogC96F5jTHGBhSMB1ZmnNxOca4beZvR0hJ6AILBxO-4cNtj8d2mx86o9mioqM9MpDc691eBfvS9ar2wZZAOwweI/s320/flags.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi3NJajanHn-CU2vebrgGh-cwOyL8e256uyokwoI1kR-2NOkGhJnN1zogC96F5jTHGBhSMB1ZmnNxOca4beZvR0hJ6AILBxO-4cNtj8d2mx86o9mioqM9MpDc691eBfvS9ar2wZZAOwweI/s1600/flags.jpg)

  

Adapun susunan dari masing-masing flag didalam flags register dapat anda lihat pada gambar disamping Pada prosesor 80286 dan 80386 keatas terdapat beberapa tambahan pada flags register, yaitu :

\- PE <Protection Enable>. Digunakan untuk mengaktifkan mode proteksi. flag ini akan bernilai 1 pada mode proteksi dan 0 pada mode real.

\- MP <Monitor Coprosesor>. Digunakan bersama flag TS untuk menangani terjadinya intruksi WAIT.

\- EM <Emulate Coprosesor>. Flag ini digunakan untuk mensimulasikan coprosesor 80287 atau 80387.

\- TS <Task Switched>. Flag ini tersedia pada 80286 keatas.

\- ET <Extension Type>. Flag ini digunakan untuk menentukan jenis coprosesor 80287 atau 80387.

\- RF <Resume Flag>. Register ini hanya terdapat pada prosesor 80386 keatas.

\- VF <Virtual 8086 Mode>. Bila flag ini bernilai 1 pada saat mode proteksi, mikroprosesor akan memungkinkan dijalankannya aplikasi mode real pada mode proteksi. Register ini hanya terdapat pada 80386 keatas. 

Demikian penjelasan yang bisa saya rangkum tentang **_[Interrupt dan Register di Bahasa Pemrograman Assembly](http://rifky-fuady.blogspot.com/2012/03/intrupsi-dan-register-pada-bahasa.html). _**Jika ingin belajar lebih banyak lagi, bisa download tutorialnya [disini.](http://www.ziddu.com/download/18825030/Assembly.byfu.rar.html)  

  

Semoga Bermanfaat Untuk Anda.