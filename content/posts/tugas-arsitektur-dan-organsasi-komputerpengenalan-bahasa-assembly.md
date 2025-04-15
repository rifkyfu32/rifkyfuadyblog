---
title: 'TUGAS ARSITEKTUR dan ORGANSASI KOMPUTERPENGENALAN BAHASA ASSEMBLY'
date: 2012-12-12T00:46:00.002+07:00
draft: false
url: /2012/12/tugas-pengenalan-bahasa-assembly.html
tags: 
- Bahasa Pemrograman
- Tugas
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqyvhJHfhNlDvnWumconCx6yHTkWY3EmpovpvqOw3oO7fXR0fg2FVXoBAgUsnK0oHnK_Q9uWxuyk2nwwWSUtHqghclPde7ICcimRf6Zs0DBTFOePpIbJBcr2A64WpfTsZyDYmx6tU9Tkc/s320/asemmbly.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqyvhJHfhNlDvnWumconCx6yHTkWY3EmpovpvqOw3oO7fXR0fg2FVXoBAgUsnK0oHnK_Q9uWxuyk2nwwWSUtHqghclPde7ICcimRf6Zs0DBTFOePpIbJBcr2A64WpfTsZyDYmx6tU9Tkc/s1600/asemmbly.jpg)

  

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEikDsi_i_iozHsBauNouPVGhtwdn0w99N3DphSNIZlyht84x2-gLRH4eydwE0PiOghmTcja8YfLkZuZ2y-06jylluWIPmcPcjde5mqP0TkAp_ycWZg6XtiHwQrePl3Ho2gN4UNZx7kQ44A/s200/logo_stmik_png.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEikDsi_i_iozHsBauNouPVGhtwdn0w99N3DphSNIZlyht84x2-gLRH4eydwE0PiOghmTcja8YfLkZuZ2y-06jylluWIPmcPcjde5mqP0TkAp_ycWZg6XtiHwQrePl3Ho2gN4UNZx7kQ44A/s1600/logo_stmik_png.png)

  

For  **Bpk. ****Sattriedi W.B,S.Si,M.Kom**

  

  

**PENGENALAN BAHASA ASSEMBLY**
------------------------------

  

  

**BAB I . PENDAHULUAN**

**1.1 LATAR BELAKANG**

Bahasa Assembly  atau  Rakitan  diprakarsai oleh  IBM  pada  tahun  1956  – 1963.  Bahasa  assembly  termasuk  bahasa  tingkat  rendah.  Pada  tahun  1957,  sebuah  tim  yang  dipimpin oleh  John W. Backus berhasil mengembangkan sebuah bahasa baru yang lebih  mengarah pada keperluan untuk menganalisa persoalan numeric. Extensi yang dihasilkan  dari bahasa assembly adalah file dengan extensi Com dan Exe. Secara umum kedua jenis  file  tersebut memiliki  perbedaan  antara  program  yang  berekstensi  Com dan  Exe,  yang  merupakan ukuran luas daerah yang menyebabkan kelainan program dalam assembler.

Untuk  file  yang  diakhiri  dengan  extension  Com,  berarti  file  itu  paling  banyak  hanya  akan  memakan  luas  64  kilobyte  yang  disebut  1  segment,  sedangkan  untuk  file  berekstensi EXE  tidak dibatasi berapa segment  yang dapat dipakai. Dapat 1 segment, 2  segment,  3  segment  atau  lebih  dari  3  segment.  Oleh  karena  COM  hanya  memiliki  1  segment, Maka file Com memiliki kelebihan dan kekurangan sebagai  berikut :

a. Stack yang telah dibuat sendiri oleh program di akhir Segment

b. Hanya terdapat satu segment, sehingga tidak perlu mengatur DS, CS, SS, kecuali

bila diinginkan.

c. Karena hanya satu segment, maka tidak mungkin membuat program lebih dari 64

kb.

d. Butuh ruangan di awal program sebanyak 100 hexa byte untuk keperluan program

segment prefix (PSP).

e. Karena PSP  diketahui  dengan  pasti,  maka perlu dilakukan  operasi  ke  PSP lebih

mudah karena masih berada dalam 1 segment.

f. Dapat menggunakan utility DEBUG untuk membuat program.

Kelebihan dan kekurangan program EXE, sebagai berikut :

a. Hasil Program panjang

b. Tidak perlu menyediakan tempat untuk PSP.

c. Pembagian segmen diatur sendiri

d. Membuat stack sendiri

e. Tidak dapat membuat progr am dengan Debug.

  

**1.2. Rumusan Masalah** Permasalahan yang akan dibahas dalam penulisan makalah ini, adalah definisi dari bahasa assembly dan assembler; penjelasan mengenai system bilangan dan konversi bilangan; elemen dasar bahasa assembly.  
  
**1.3. Tujuan.**  
Tujuan dari penulisan makalah ini ialah untuk menyelesaikan tugas mata kuliah BAHASA ASSEMBLY,dan untuk mendapatkan pengetahuan mengenai bahasa assembly baik bagi penulis maupun pembaca.  
  
**1.4. Manfaat.**  
Manfaat Penulisan Makalah ini adalah sebagai sarana untuk menambah pengetahuan dan sebagai media pembelajaran.

  

**BAB II PEMBAHASAN**

  

**2.1. Elemen Bahasa Asembly**

Dalam  pemrograman  bahasa  assembly  lebih  ditekankan  pada  system  operasi Microsoft Intel yang seiring dengan perkembangan mikroprosesor 8088/8086. Perkembangan bahasa assembly tergantung pada linker yang mengubah file \*.obj menjadi \*.exe atau \*.com. Bahasa assembly dikategorikan sebagai bahasa tingkat rendah. Hal ini untuk menggambarkan spesifikasi sebagai bahasa yang berorientasi

pada machine dependent. Untuk membandingkan bahasa mesin dan bahasa assembly menurut karakteristik dibagi 2 bagian :

· Mnemonic Operation Code

· Simbolic Operand Spesification

  

  

**2.2. Proses Assembly**

Untuk  membangun  skema  proses  translasi  dari  satu  bahasa  ke  bentuk  lain,  maka yang perlu diperhatikan adalah mengidentifikasi tugas dasar yang dikerjakan dalam proses translasi .

  

  

**2.3. Skema Assembly**

Proses penerjemahan secara sederhana dapat dikelompokkan dalam dua fase, yaitu:

  

· **Fase Analisa**

a. Memisahkan label, mnemonic operation code dan operand field yang ada pada

statement.

b. Memasukkan symbol yang ditemukan pada label field dan alamat yang dituju

machine word ke dalam symbol table.

c. Melakukan validasi mnemonic operation code dengan melihat pada mnemonic

table

d. Menentukan  alamat  yang  dibutuhkan  oleh  statement  berdasarkan  pada

mnem

onic operation code dan operand field pada statement.

  

·** Fase analisis dapat dikelompokkan menjadi beberapa tahap, yaitu :**

 a. Lexical Analisys

Lexical  Analisys  adalah  menjalankan  mikro  level  examination  dari  teks

masukan  untuk  mengenal  lexial  unit  yang  ada  didalamnya  dan  menentukan

kategori syntax.

 b. Syntax Analisys

Proses  Syntac  Analisys  dilakukan  terhadap  descriptor  dari  lexical  analisys

untuk  menentukan  struktur  syntax  dari  statement  masukan.  Proses  tersebut

dikenal  dengan  PARSING.  Output  dari  parsing  adalah  representasi  dari

struktur syntac suatu statement.

  c. Semantic Analisys

Proses  semantic  analisys  dapat  diklasifikasikan  kedalam  proses  declarative

statement dan proses eksekusi.

  

· **Fase Syntesis**

a. Menghasilkan machine operation code yang berkorespodensi dengan

mnemonic operation code yang telah dicari pada mnemonic table.

b. Menghasilkan alamat operand dari symbol table

c. Melakukan syntesis instruksi machine.

Pada fase sysntesis dilakukan pemilihan machine operation code yang sesuai

dengan mnemonic Load  dan menempatkan pada  machine  instruction opcode

field.  Evaluasi  korespodensi  pengalamatan  dilakukan  untuk  operand

expression ‘ Result + 4.

  

**2.4. Proses Assembly**

Unit  dalam sources program digunakan untuk  menterjemah semua bagian program.

Ketika  fase  analisys  statement  program  pertama  kali  dilakukan,  maka  proses  LC

akan dikerjakan dan symbol yang didefinisikan dalam program dimasukkan ke dalam

symbol table. Untuk mengurangi pengulangan, maka hasil analisis sources statement

dari  first  pass  direpresentasikan  dalam  internal  form  pada  sources  statement  yang

disebut  intermediate  code. Selain  membentuk  intermediate  code,  suatu  proses

assembler juga membangun struktur database yang digunakan oleh subsequent pass.

  

  

**2.5. Spesifikasi Komputer**

Dalam  pemrograman  bahasa  assembly,  ada  beberapa  aspek  utama  yang  minimal

harus ada persyaratan yang menunjang, meliputi :

Langkah Pasti Menuju Sukses

A. Perangkat Keras (Hardware) yang diperlukan:

1\. Prosesor Intel, minimal Intel Pentium I, Intel Pentium II dan Pentium III

2\. Monitor CGA, EGA atau VGA

3\. Keyboard dan Mouse

4\. USB Port

5\. Harddisk

B. Perangkat Lunak (Software) yang diperlukan :

1\. Microsoft Windows XP

2\. Turbo Assembler

3\. Linker : Tlink ver 3 minimal

4\. Text Editor : Edit atau bahasa pemrograman

  
  
  
  
  
  

**BAB III  PENUTUP**  
  
  
3.1. Kesimpulan.  
Bahasa Assembly adalah bahasa yang memudahkan pemahaman bagian computer yang paling rendah, mendekati mesin. Bahasa assembly sebaiknya dipelajari secara kontektual sehingga interaksi perangkat keras dan perangkat lunak computer mungkin lebih mudah dipahami.  
Bahasa assembly adalah bahasa pemrograman dengan korespondensi satu-satu antara perintah-perintah/pertanyaannya dan bahasa mesin computer.  
Assembler adalah program yang mengonversi kode program sumber ke dalam bahasa mesin  
System bilangan (number system) adalah suatu cara untuk mewakili besaran dari suatu item fisik. System bilangan terdiri dari: bilangan biner, bilangan decimal, bilangan octal dan hexadesimal.  
Kumpulan karakter dalam assembly  
Letter : A-Z, a-z  
Digit : 0-9  
Karakter khusus:  
? , (koma)  
@ “  
\_ &  
$ %  
: !  
. ‘  
\[\] ~  
() |  
{} =  
\+ #  
\- ^  
/ ;  
\* \`