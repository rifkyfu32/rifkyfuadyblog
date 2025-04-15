---
title: 'Mengenal Memori  di Bahasa Pemrograman Assembly'
date: 2012-03-09T21:14:00.000+07:00
draft: false
url: /2012/03/mengenal-memori-di-bahasa-pemrograman.html
tags: 
- Bahasa Pemrograman
---

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjItSf-xkMS3UYlBGryEUh5nWL5a3SPMxFBcoJazc-rshOPL5_vmxA8B5SzdatAKDWlzuJ10yfYrhIkH_Kh-lJWYK9gn143clnGGMlNklTeNiOkvTChFLJ4-EfWzfe-av_pHkS2i4XYjYU/s200/asemmbly.bmp)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjItSf-xkMS3UYlBGryEUh5nWL5a3SPMxFBcoJazc-rshOPL5_vmxA8B5SzdatAKDWlzuJ10yfYrhIkH_Kh-lJWYK9gn143clnGGMlNklTeNiOkvTChFLJ4-EfWzfe-av_pHkS2i4XYjYU/s1600/asemmbly.bmp)Memori dengan komputer memiliki hubungan yang tak dapat dipisahkan,karena setiap komputer memerlukan memori sebagai tempat kerjanya. Memori ini dapat berfungsi untuk memuat program dan juga sebagai tempat untuk menampunghasil proses.  
  

Yang perlu kita perhatikan bahwa memori untuk menyimpan program maupun hasil dari pekerjaan bersifat volatile yang berarti bahwa data yang disimpan cuma sebatas adanya aliran listrik. Jadi bila listrik mati maka hilang pulalah semua data yang ada di dalamnya. Hal ini mengakibatkan diperlukannya media penyimpan kedua yang biasanya berupa disket maupun hard disk.  
  
**1\. Microprocessor**

Pada IBM-PC terdapat suatu bagian penting yang disebut microprocessor atau yang sering disebut processor saja. Processor ini berfungsi untuk menangani keseluruhan dari kerja komputer kita. Pada processor inilah segala hal yang berhubungan dengan kerja komputer diatur dan dibagi prioritasnya dengan baik agar tidak terjadi kesalahan yang kemudian akan menyebabkan kacaunya informasi yang diperoleh.  
  

Lama kelamaan tugas komputer tentu saja makin bertambah baik dari segi kuantitas maupun kerumitannya. Sejalan dengan itu processor juga makin dikembangkan. Processor yang baru sebenarnya hanyalah perbaikan danpengembangan dari yang versi lama sehingga semua instruksi yang berlaku di processor lama dapat pula dikerjakan oleh yang baru dengan tentu saja beberapa keunggulan.

Adapun processor yang kini banyak beredar di pasaran :  
  

_\- 8088 & 8086 :_

Ini merupakan processor IBM-PC yang pertama sekali atau yang sering disebut XT. Processor 8088 menggunakan jalur bus data 8 bit sedangkan 8086 menggunakan 16 bit. Pe rbedaan jalur bus ini menyebabkan perbedaan jumlah data yang dikirim pada satu saat dan secara langsung mengakibatkan speed 8086 berada di atas 8088. Baik 8088 maupun 8086 mampu mengalamatkan memori hingga 1 MB.  
  

_\- 80286 :_

Versi pengembangan dari 8086. Pada 80286 ini beberapa instruksi baru ditambahkan. Selain itu dengan jalur bus yang sama dengan 8086, 80286 dirancang mempunyai speed di atas 8086. Selain itu 80286 dapat bekerja pada 2  mode yaitu mode real dan protected.

Mode real pada 80286 dapat beroperasi sama seperti 8088 dan 8086 hanya terdapat perbedaan dalam hal speed. Mode real ini dimaksudkan agar semua software yang dapat dioperasikan pada 8088/8086 dapat pula dioperasikan dengan baik di 80286. Pada mode protected 80286 mampu mengalamatkan sampai 16 MB memori.  
  

_\- 80386 :_

Processor 80386 merupakan sesuatu yang sangat baru dibanding 80286 sebab bus data yang digunakan di sini sudah 32 bit sehingga speednya juga jauh di atas 80286. Selain itu pada 80386 ditambahkan pula sebuah mode pemrograman baru yaitu mode virtual. Pada mode virtual ini 80386 mampu mengalamatkan sampai 4 GB memori. Sama seperti 80286, mode real dimaksudkan untuk kompatibilitas dengan 8088/8086 dan mode protected untuk menjaga kompatibilitas dengan 80286.  
  

**2\. Organisasi Memori Pada PC**

Memori yang ada pada komputer perlu diatur sedemikian rupa sehingga mudah dalam pengaksesannya. Oleh sebab itu di kembangkanlah suatu metode yang efektif dalam pengorganisasiannya. Pada bagian ini akan dibahas mengenai pengorganisasian memori ini.  
  

**3\. Pembagian Memori**

Memori komputer terbagi atas 16 blok dengan fungsi-fungsi khusus yang sebagian besar adalah sebagai RAM (Random Access Memory) yang berfungsi sebagai penyimpan bagi hasil pengolahan       pada komputer itu sendiri. Untuk lebih jelasnya diberikan pembagian fungsi pada blok memori ini secara kasar pada gambar berikut :  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjSGcgLg_YbPBKfFukG0VL5NACDC3MaMmdppPcFG9ZEQ_0qjIocMOId0iK7zf6sIKJyU1XRkn6MBqgS3qSwhrxXb-v8KptWKDD2VZvzIxgUi8nvzoQIEOexUlaj3kA9XUWAVSRROdNyuX0/s320/blok+memory.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjSGcgLg_YbPBKfFukG0VL5NACDC3MaMmdppPcFG9ZEQ_0qjIocMOId0iK7zf6sIKJyU1XRkn6MBqgS3qSwhrxXb-v8KptWKDD2VZvzIxgUi8nvzoQIEOexUlaj3kA9XUWAVSRROdNyuX0/s1600/blok+memory.jpg)

  

**4\. Pengalamatan Memori Dengan Segment Offset**

Sudah kita bahas bersama bahwa baik 8086 maupun mode real 80286 dapat mengalamatkan sampai 1 MB memori. Tetapi sebenarnya baik 8086 maupun 80286 adalah procesor 16 bit. Banyaknya memori yang dapat dicatat atau dialamatkan oleh procesor 16 bit adalah maksimal 216 byte (=64 KB). Jadi bagaimana 8086 dan mode real 80286 mampu mengalamatkan sampai 1 MB memori ?  
  

Hal ini dapat dimungkinkan dengan adanya pengalamatan yang menggunakan sistem 20 bit walaupun sebenarnya procesor itu hanya 16 bit. Dengan cara ini dapat dialamatkan 220 byte (=1 MB) memori. Tetapi masih tetap ada satu kendala dalam pengalamatan 20 bit ini. Yaitu bahwa sesuai dengan tipenya procesor ini hanya mampu mengakses 16 bit data pada satu kali akses time. Sebagai pemecahannya dikembangkanlah suatu metode pengalamatan 20 bit yang dimasukkan ke dalam format 16 bit. Pada metode pengalamatan ini baik 8086 maupun mode real 80286 membagi ruang memori ke dalam segmen-segmen di mana besar 1 segmen adalah 64 KB (=216 byte). Jadi pada segmen 0000h(Tanda "h" menunjukkan hexadesimal) terdapat 64 KB data, demikian pula dengan segmen 0001h dan seterusnya.  
  

Sekarang bagaimana caranya agar setiap data yang tersimpan dalam satu segmen yang besarnya 64 KB itu dapat diakses secara individual. Cara yang dikembangkan adalah dengan membagi-bagi setiap segmen menjadi bagian-bagian yang disebut offset. Dalam satu segmen terdapat 216 offset yang diberi nomor dari  0000h  sampai FFFFh. Nomor offset selalu diukur relatif dari awal suatu segmen.  
  

Sekarang kita lihat bagaimana sebenarnya letak suatu segmen dalam memori komputer kita. Segmen 0000h berawal dari lokasi memori 0 hingga 65535 ( 64 KB ). Segmen 0001h berawal dari lokasi memori 16 (0010h) hingga 65551 (65535 + 16). Segmen 0002h berawal dari lokasi 32 hingga 65567. Demikian seterusnya. Kita lihat bahwa sistem penempatan segmen semacam ini akan menyebabkan  terjadinya overlapping (tumpang-tindih) di mana lokasi offset 0010h bagi segmen 0000h akan merupakan offset 0000h bagi segmen 0001h. Demikian pula offset 0011h bagi segmen 0000h akan merupakan offset 0001h bagi segmen 0001h. Dalam pembahasan selanjutnya akan kita lihat bahwa a da banyak nilai segmen:offset yang dapat digunakan untuk menyatakan suatu alamat memori tertentu disebabkan adanya overlapping ini. Untuk lebih jelasnya dapat kita lihat pada gambar berikut dibawah.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh0ZsN_o9zvvTsphoQdNlkdAoSSKLFlRGFj1V0lhN4EAY2PmJz3DX11ueU8MOiq-S1Tq1l1t6psk0SnCCfGE1mEaM_LO_fafqRONi3yFHLv8036WLX8i7PtQIOOH4OsRT4oR82ZkYNdCSI/s320/overlapping.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh0ZsN_o9zvvTsphoQdNlkdAoSSKLFlRGFj1V0lhN4EAY2PmJz3DX11ueU8MOiq-S1Tq1l1t6psk0SnCCfGE1mEaM_LO_fafqRONi3yFHLv8036WLX8i7PtQIOOH4OsRT4oR82ZkYNdCSI/s1600/overlapping.jpg)

  

**5\. Konversi Alamat**

Alamat yang menggunakan sistem segmen:offset ini disebut sebagai alamat relatif karena sifat offset yang relatif terhadap segmen. Sedangkan alamat memori yang sebenarnya disebut alamat absolut. Berikut kita lihat cara pengkonversian alamat relatif ke absolut. Pengkonversian dapat dilakukan dengan menggeser nilai segmen 4 bit ke kiri dan kemudian dijumlahkan dengan nilai offset. Atau yang lebih sederhana adalah dengan mengalikan nilai segmen dengan 24 (=10h) dan kemudian dijumlahkan dengan nilai offset. Cara ini dike mbangkan dari besarnya selisih segmen yang satu dengan yang berikutnya yang sebesar 16 bit (=10h).

  

Alamat relatif :   1357h:2468h           1356h:2478h

13570                 13560

2468                  2478

\-------               -------

Alamat absolut :    159D8h                159D8h  
  

Pada kedua contoh di atas terlihat jelas alamat relatif 1357h:2468h sebenarnya menunjukkan lokasi yang sama dalam memori dengan alamat relative 1356h:2478h yang disebut overlapping. Alamat yang overlapping ini menyebabkan sebuah alamat absolute dapat dinyatakan dengan alamat segmen:offset yang bervariasi sebanyak 2 pangkat 12 atau sebanyak 4096 variasi.  
  

Variasi untuk alamat absolute :

0  - 15      dapat dinyatakan dengan 1 variasi

16 - 31      dapat dinyatakan dengan 2 variasi

32 - 48      dapat dinyatakan dengan 3 variasi

:

:

65520 keatas  dapat dinyatakan dengan 4096 variasi.

  

Demikian informasi yang bisa saya bagikan tentang _Memori  di Bahasa Pemrograman Assembly._