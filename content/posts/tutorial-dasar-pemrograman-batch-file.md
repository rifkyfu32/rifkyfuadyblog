---
title: "Tutorial Dasar Pemrograman Batch File"
date: 2013-01-02T21:00:00.000+07:00
draft: false
url: /2013/01/maaf-ini-sebelumnyasahabat-blogger-lama.html
tags:
  - Bahasa Pemrograman
  - Tips dan Trick
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjx7AqdaA86Xm1c3t_ZrHUjKBmCBm0z57xealnOz5tbwwvtPcOv3ELmj487MbIY6NGw9h4jAYZrFAlZWJMcJGev28-ho_1PorCLvB62uvOtxuUce2EWWKsN4LJcNjEAi6Qnn05uC9hi478/s200/G_127.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjx7AqdaA86Xm1c3t_ZrHUjKBmCBm0z57xealnOz5tbwwvtPcOv3ELmj487MbIY6NGw9h4jAYZrFAlZWJMcJGev28-ho_1PorCLvB62uvOtxuUce2EWWKsN4LJcNjEAi6Qnn05uC9hi478/s1600/G_127.png)

Maaf ini sebelumnya sahabat blogger, lama gak pernah posting...

Oke. Sekarang kita langsung saja masuk ke Judul posting di atas, kemaren makul Sistem Operasi Praktek yang di ajarkan Oleh _Bpk. **M. Rifqi Maulana M.Kom**_ adalah Pemrograman Batch File di Windows, setelah mengajarkan cara mengoprek-oprek registry tools di Windows. Dan sekarang saya ingin men-sharing apa yang diajarkan **_Beliau._**

Udah pada tau Perintah-perintah dasar di DOS belum? Kalo belum bisa lihat [disini.](http://rifky-fuady.blogspot.com/2013/01/perintah-dasar-dos.html)

Biar nggak kebingunan, lebih baik baca dasar-dasarnya dulu. Oke...????

Lanjut deh,  yang ingin saya sharing disini adalah source code dan tutorial pemrograman batch file yang masih sederhana, masih dalam tingkatan pemula, jadi kalo ada master-master yang membaca  postingan saya, dan mungkin saya ada kesalahan, bisa membagikan kritik dan saran nya dibawah komentar, supaya kita semua disini bisa sama belajar dan berbagi ilmu. Setuju gak??? Hehehhe...:-)

· **Apa itu Pemrograman Batch File?**

\- Batch file programming adalah pemrograman dasar yang dikenalkan oleh sistem operasi  Microsoft Windows (Premkumar, 2009).

\- Batch file biasanya dibuat untuk memberikan perintah kepada SO Windows secara beruntun. Misalnya:

1. Copykan file bernama myfile.txt dari drive d:\\ ke c:\\

2. Setelah itu rename c:\\myfile.txt menjadi c:\\fileku.txt

3. Kemudian hapus file d:\\myfile.txt

\- Dasar sintak program didalam batch file adalah perintah-perintah DOS.

\- Ketika Batch Program di eksekusi, program didalamnya di interpreter baris demi baris oleh CLI (Commad Line Interpreter) yaitu: command.com atau cmd.exe

\- Interpreter: Proses pembacaan, pengecekan dan pegeksekusian sintak program secara perbaris.

\- Misal, jika ada 5 baris program, dan dibaris ke-3 ada kesalahan penulisan, maka yang akan dieksekusi baris 1 dan 2 saja sedangkan baris 3,4 dan 5 tidak dieksekusi.

· **Bagaimana cara membuat File Batch?**

\- Batch file dapat dibuat dengan editor apapun semacam Notepad, Notepad++, WordPad dan lain sebagainya.

\- Penulisan script / sintak pada batch file tidak case sensitive artinya huruf besar dan huruf kecil dianggap sama

\- Ekstensi batch file adalah .bat

\- Contohnya seperti gambar berikut (buka spoiler):

**Membuat File Batch**:

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgdF5KuZGIkKYtvY8BWsSxreW9gk5nsHVcZPuvRjcVTYvNRPlP-9Im7QLhN-oSo_eysxbu2vq7t8A5QWFFdK1JDu_BhGnm3laPZcw3Dz81QoBd8dubRMU9Xn8omGGF49obsoJMxUCn6aus/s320/gmbr1.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgdF5KuZGIkKYtvY8BWsSxreW9gk5nsHVcZPuvRjcVTYvNRPlP-9Im7QLhN-oSo_eysxbu2vq7t8A5QWFFdK1JDu_BhGnm3laPZcw3Dz81QoBd8dubRMU9Xn8omGGF49obsoJMxUCn6aus/s1600/gmbr1.jpg)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgxtf6EJ7M6xQNMrvXHCltaEdOxDTcPxxqegqEz2l9EwQMzsjhnap5NlDsrZ4MIwR-ogEzcBu5hyAtyUEyo8AMTbVqqR00hD9vctJdUZO8nSorgXvMnwfX5u-GnRWDFHD3tERktApFXxr8/s320/gmbr2.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgxtf6EJ7M6xQNMrvXHCltaEdOxDTcPxxqegqEz2l9EwQMzsjhnap5NlDsrZ4MIwR-ogEzcBu5hyAtyUEyo8AMTbVqqR00hD9vctJdUZO8nSorgXvMnwfX5u-GnRWDFHD3tERktApFXxr8/s1600/gmbr2.jpg)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgW7YcS7f1RT-LVPuHVmJJauUQXhzjAbHT9doWxkXqEg-PdUnn-FlOvk7VNyCFsUBBqKJXOWLDqo_DzVlxdYyEP4Aq3SWttWj1NFLbZFpM7B1Gi4R27J4Y8EqFZyGLYGax7lHtu4LOooBU/s320/gmbr3.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgW7YcS7f1RT-LVPuHVmJJauUQXhzjAbHT9doWxkXqEg-PdUnn-FlOvk7VNyCFsUBBqKJXOWLDqo_DzVlxdYyEP4Aq3SWttWj1NFLbZFpM7B1Gi4R27J4Y8EqFZyGLYGax7lHtu4LOooBU/s1600/gmbr3.jpg)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjDDC261oboudt7zAHODGB63Lug_KFDChzHpoy1xArDIGPGAZ0qO0rkTblmbsGW8lw4b4bVEqbV4CoJDmgP06CVaRIeajW72DzTNw4b4YOSJFPl6M0p0AW3ssu0P3vVi5XS2RIhW2QLs3k/s320/gmbr4.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjDDC261oboudt7zAHODGB63Lug_KFDChzHpoy1xArDIGPGAZ0qO0rkTblmbsGW8lw4b4bVEqbV4CoJDmgP06CVaRIeajW72DzTNw4b4YOSJFPl6M0p0AW3ssu0P3vVi5XS2RIhW2QLs3k/s1600/gmbr4.jpg)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilXe227X8dWEhclPxhIEJa9NiedolzbCTErcrg_DPww8uSJ17Gn-S4x8rlEJgo2xpnpl5NzYxN108vy-ybf76vxRhdlcgxWkRMQnJoVC1OUcm2VpoYPWA1sxvBFpOT8-yRFItw-s6q2kE/s320/gmbr5.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilXe227X8dWEhclPxhIEJa9NiedolzbCTErcrg_DPww8uSJ17Gn-S4x8rlEJgo2xpnpl5NzYxN108vy-ybf76vxRhdlcgxWkRMQnJoVC1OUcm2VpoYPWA1sxvBFpOT8-yRFItw-s6q2kE/s1600/gmbr5.jpg)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEik8cMrtFH8jKlTcDv1RTDI7unTQWJdNpht1UvaAIAoXbi0tVia134KQfa5xJA7_NkL83rPyGHvjUOQ53R5kYuCy_dJkyTlMpqmXQjUm2ahOnLb5KzT4JffJzYd0J1rx1EekK-jq6uQ6Mo/s320/gmbr6.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEik8cMrtFH8jKlTcDv1RTDI7unTQWJdNpht1UvaAIAoXbi0tVia134KQfa5xJA7_NkL83rPyGHvjUOQ53R5kYuCy_dJkyTlMpqmXQjUm2ahOnLb5KzT4JffJzYd0J1rx1EekK-jq6uQ6Mo/s1600/gmbr6.jpg)

· **Bagaimana cara Memberi Title Window?**

\- Kita dapat mengubah window title dengan menambah title nama_window sebelum sintak pause. Disarankan: letakkan sintak title setelah sintak: @echo off.

\- Contoh :

**Memberi Title Window**:

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhwkjOIEU8qXO0HO1rKZ-4YT7wHKPZvq9YQB6UBTax8kBvaTrtXHzlmoE7GlNJIMAVU9zP7SXy3p0Hnqr1qg3RZRLGv3n5jhxNb7oPQX3bZ3M5OnW8l0auWrwd0d6CkZGkhXVOJD4d3sGM/s320/gmbrtw1+fix.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhwkjOIEU8qXO0HO1rKZ-4YT7wHKPZvq9YQB6UBTax8kBvaTrtXHzlmoE7GlNJIMAVU9zP7SXy3p0Hnqr1qg3RZRLGv3n5jhxNb7oPQX3bZ3M5OnW8l0auWrwd0d6CkZGkhXVOJD4d3sGM/s1600/gmbrtw1+fix.jpg)

@echo off  
title Program Pertamaku  
echo NIM : 12.240.0001  
echo Nama : A. Fuady Rifky  
echo HP : 0878 3081 4574  
pause

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZrQvWz1ec2DQxStpbywkGlMfZgojGh-y_XKDZYZvnd_DsANGBkAOm9dsKW4j7GqjZLOT_Od8dsDdPivHkVLpQN-PqXSR9jqAOVJEMSkztrokn8GAvFlX9E9jc8ePf13SvyGH0zYVREhU/s320/gmbrtw3+fix.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZrQvWz1ec2DQxStpbywkGlMfZgojGh-y_XKDZYZvnd_DsANGBkAOm9dsKW4j7GqjZLOT_Od8dsDdPivHkVLpQN-PqXSR9jqAOVJEMSkztrokn8GAvFlX9E9jc8ePf13SvyGH0zYVREhU/s1600/gmbrtw3+fix.jpg)

· **Bagaimana cara Mendefinisikan Variabel?**

\- Seperti bahasa pemrograman, batch file programming juga dapat mendefinisikan variabel.

\- Variabel: adalah salah satu cara yang dilakukan oleh program untuk menyimpan sebuah nilai di dalam memory. Secara default pendefinisian variabel pada batch file bertipe string.

\- Contoh: a=2, b=4, nama=budi, jenjang=S1 dan lain sebagainya.

\- Cara mendefinisikan variabel pada batch programming adalah dengan menggunakan sintak _set_

\- Contoh:

**Mendefinisikan Variabel**:

@echo off  
set a=2  
set b=4  
set nama=budi  
set jenjang=S1  
pause

· **Bagaimana cara Menampilkan Isi Variabel?**

\- Variabel yang telah kita definisikan sebelumnya belum ditampilkan ke layar. Nah, cara menampilkan isi variabel tersebut ke layar secara sederhana adalah dengan: **echo** _%nama_variabel%_

\- Contoh:

**Menampilkan Variabel**:

@echo off  
set a=2  
set b=4  
set nama=fuady  
set jenjang=S1  
echo %a%  
echo %b%  
echo %nama%  
echo %jenjang%  
pause
