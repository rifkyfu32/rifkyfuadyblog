---
title: 'Perintah Dasar DOS'
date: 2013-01-02T20:27:00.001+07:00
draft: false
url: /2013/01/perintah-dasar-dos.html
tags: 
- Info
- Tips dan Trick
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhGgxUMQnSatHraKB9ofcYGkv8SXgdUgMLC_4QeQ3vXFMN1Tt1niGlOAcU3aoXz0vIydtDIez1Qfba3GHiEcQwTMa-BDwWlReJDT6HYfTlHuXisnIUG8TG2ZhY7OvedZ1Eqk0vsSQruKHo/s200/LogoNewY.GIF)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhGgxUMQnSatHraKB9ofcYGkv8SXgdUgMLC_4QeQ3vXFMN1Tt1niGlOAcU3aoXz0vIydtDIez1Qfba3GHiEcQwTMa-BDwWlReJDT6HYfTlHuXisnIUG8TG2ZhY7OvedZ1Eqk0vsSQruKHo/s1600/LogoNewY.GIF)

  

  

DOS (Disk Operating System) adalah sistem operasi berbasis teks yang dikeluarkan microsoft sebelum windows. Sama seperti Terminal di Linux, DOS memiliki daftar perintah berbasis teks yang harus diketik di Console DOS atau lazim disebut Command Prompt. Mengetahui penggunaan perintah DOS adalah pengetahuan tersendiri yang perlu dipahami oleh administrator jaringan berbasis windows. Anda akan lebih mudah menguasai NetBios Hacking atau remote komputer berbasis console di windows dengan mengetahui perintah- perintah DOS.

Tidak semua orang yang bisa menggunakan komputer atau operator komputer bisa mengerti perintah dos. Sebenarnya DOS adalah sistem operasi, akan tetapi setelah dos mulai banyak di tinggalkan maka sekarang dos tetap di integrasikan oleh windows yang lebih kita kenal dengan nama MS-DOS atau Command Prompt Window dengan kata lain DOS adalah Sistem Operasi Berbasis Baris Perintah.

MS-DOS merupakan shell yang memiliki banyak fungsi seperti halnya shell yang ada di linux ( wah kejahuan ya kok sampai ke linux sih ).

Perintah yang ada di dalam DOS juga dapat digunakan untuk mengelola jaringan maupun hardware komputer. Akan tetapi sebelum kamu mengetahui perintah lanjut dari dos  ada baiknya kamu mengenal perintah dasar yang ada di DOS

  

**1\. Komunikasi dengan Sistem**

COMMAND : memuatkan kopian baru command interpreter.

DATE : mengeset atau menampilkan tanggal system.

EXIT : mengakhiri kopian command interpreter (kembali ke kopian Induk).

PROMPT : mendefinisikan prompt system.

SET : mendefinisikan variable lingkungan.

SHARE : memuatkan dukungan file sharing (untuk Microsoft Network).

TIME : mengeset atau menampilkan waktu system saat itu.

VER : menampilkan nomor versi dari command interpreter MS- DOS.

  

**2\. Bekerja dengan Disk**

ASSIGN : merute permintaan operasi disk dari satu drive ke drive lain.

CHKDSK : memeriksa alokasi ruang penyimpanan, kesalahan isian. direktori, table alokasi file atau kerusakan fisik disk

DISKCOMP : membandingkan dua floppy disk track demi track dan melaporkan perbedaannya.

DISKCOPY : mengkopi floppy disk secara track demi track (tidak mengonsolidasikan file terfragmentasi).

FDISK : mengonfigurasi fixed disk (harddisk) untuk digunakan MS- DOS.

FORMAT : memformat disk untuk digunakan MS-DOS dengan menginisialisasi direktori dan file allocation table (FAT).

JOIN : membuat disk sebagai subdirektori dari disk lain.

LABEL : memodifikasi, menciptakan dan menghapus label volume.

SUBST : mensubsitusi huruf drive untuk nama jalur direktori, membuat subdirektori menjadi satu drive maya.

SYS : mentransfer file-file system MS-DOS (IO.sys dan MSDOS. .sys) ke disk.

VERIFY : memverifikasi data begitu dituliskan ke disk.

VOL : menampilkan label volume dari disk.

  

**3.Bekerja dengan Direktori**

Direktori puncak disebut root directory. Root directory menyimpan isian-isian(entry) yang menunjukkan file dan subdirectori, menyimpan nomor isian FAT yang menyimpan awal cluster dari file. Subdirektori adalah file yang menyimpan isian-isian direktori.

Perintah-perintah yang berhubungan dengan direktori,antara lain:

CHDIR atau CD : mengubah direktori kerja.

DIR : menampilkan informasi mengenai isian-isian direktori(nama file, ekstensi, ukuran dalam byte, tanggal

dan jam diciptakanatau terakhir diubah.

MKDIR atau MD : menciptakan subdirektori baru.

PATH : mendefinisikan nama jalur yang digunakan MS-DOS dalam mencari file yang dieksekusi (untuk ekstensi COM, EXE, dan BAT).

RMDIR atau RD : menghapus direktori kosong.

TREE : menampilkan struktur direktori secara hirarki.

  

**4\. Pengelolaan file**

ATRIB : menampilkan dan mendefinisikan atribut file.

BACKUP : membuat kopian backup dari file atau struktur direktori.

COPY : mengkopi file.

EDLIN : menciptakan atau memidifikasi file teks ASCII.

ERASE : menghapus file.

EXE2BIN : mengonversi file dieksekusi dalam format.EXE menjadi file memori (.COM, .BIN atau .SYS).

FC : membandingkan dua file dan menampilkan perbedaannya.

RECOVER : merekonstruksi file dari disk yang mempunyai sector-sektor Rusak.

RENAME atau REN : mengubah nama satu file atau lebih.

RESTORE : mengembalikan file-file yang diciptakan dengan perintah BACKUP ke disk dengan struktur direktori yang sama seperti aslinya.

  

**5\. Pengelolaan Masukan dan Keluaran**

CLS : membersihkan layar tampilan.

CTTY : mengubah prangkat untuk masukan dan keluaran standar.

FIND : mencari suatu sring.

GRAFTABL : mendefinisikan IBM extended character set.

MODE : mengendalikan mode perangkat keluaran. MODE menge-set

karakteristik tampilan , menge-set panjang baris dan spasi untuk port printer, mengoneksi printer serial dengan men-redirect keluaran printer parallel ke port komunikasi serial, menge-set parameter komunikasi untuk port komunikasi asincron.

MORE : perintah untuk filter yang menampilkan isian file per layar.

PRINT : mencetak file di background (sehingga pemakaian dapat mengerjakan tugas lain).

SORT : filter yang menampilkan secara terurut.

TYPE : mengirim file ke keluaran standar.

  

**6\. Setting (penyesuaian) lingkungan kerja**

Pemakai dapat menyesuaikan lingkungan keranya lewat file CONFIG.SYS yang mendefinisikan karakteristik operasi system MS-DOS. Ketika MS-DOS dimulai, MS-DOS mengeksekusi perintah di CONFIG.SYS secara otomatis jika tersedia. Yang digunakan untuk Penyesuaian Lingkungan Kerja

ANSY.SYS : device driver ini mengimplementasikan kode escape standar dari ANSI untuk kendali layar dan keyboard.

BREAK : mengendalikan interupsi control-C.

BUFFERS : menspesifikasikan jumlah buffer disk di memori yang dialokasikan MS-DOS saat pertama kali dimulai.

COUNTRY : menspesifikasikan country untuk penulisan tanggal yang cocok, tanda decimal, dan symbol mata uang yang di gunakan.

DEVICE : menginstal device driver baru.

DRIVPARM : mendefinisi ulang karakteristik default yang didefinisikan device driver untuk perangkat blok.

FCBS : menspesifikasikan jumlah maksimum file-file yang dikendalikan FCB yang dapat dibuka, file sharing sebagai efeknya.

FILES : menspesifikasikan jumlah maksimum file yang dapat dibuka.

LASTDRIVE : menentukan jumlah maksimum drive yang dikenali oleh MS-DOS.

SHELL : menspesifikasikan command interpreter pengganti COMMAND .COM.

VIDISK.SYS : menciptakan disk virtual yang berada di memori.

  

**7\. Penggunaan Batch**

Batch adalah file yang dapat dieksekusi. File berisi kumpulan /sekuen perintah yang dieksekusi secara berurutan. Pemakaian mengetikkan nama file dan MC-DOS mengeksekusi perintah-perintah di file itu. Batch berekstensi .BAT. Pembuatan batch sebagaimana program karena disediakan beragam bentukan kendali dalam hal ini pemakaian dapat memberikan beragam alternayif eksekusi perintah-perintah. File AUTOEXEC.BAT pada root directori akan dieksekusi saat MC-DOS boot. Perintah yang berhubungan dengan pengendalian jalannya eksekusi perintah-perintah file batch adalah:

CALL : memanggil batch lain.

ECHO : menampilkan nama perintah atau pesan yang dieksekusi dari batch.

FOR : mengeksekusi perintah secara iterasi untuk tiap file di sekumpulan file.

GOTO : mengeksekusi perintah dari batch, lompat ke perintah di sembarang lokasi.

IF : memeriksa kondisi dan mengeksekusi perintah di batch ,bergantung hasil.

PAUSE : menghentikan eksekusi batch untuk sementara.

REM : penanda komentar.

SHIFT : memperluas jumlah parameter di baris perintah.