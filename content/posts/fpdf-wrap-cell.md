---
title: "Laporan PDF cantik, Auto Wrap Content Table dengan FPDF"
slug: fpdf-wrap-cell
date: 2019-03-14T22:47:33+07:00
draft: false
tags:
  - Info
  - Tips dan Trick
image: ""
description: ""
---

**Pernah gak sih, pas lagi bikin laporan dengan `FPDF`, ternyata hasilnya tidak sesuai harapan?**

Saat isi data pada suatu kolom `melebihi` lebar dari kolom tersebut, maka tulisannya akan `kepotong` alias `gak keliatan`. Hehe...

Kebetulan tadi sore saya sendiri mengalaminya, biar gak lupa mending catet aja di blog.

Perkenalan sedikit, [FPDF](http://fpdf.org/) adalah `library PHP` yang bisa kita manfaatkan untuk membuat file `PDF` _(bikin laporan)_.

Bagi anda yang belum pernah menggunakan library [FPDF](http://fpdf.org/), silahkan bermain-main dengan tutorial dasarnya terlebih dahulu.

Disini saya hanya akan memberikan `snippet code`, berbagi cara agar output tabel file PDF menjadi rapi nan cantik.

Berikut ini adalah contoh output masalah yang saya hadapi tadi sore :

![Tampilan PDF cantik, Auto Wrap Content Table dengan FPDF pertama](/img/fpdf-wrap-cell/1.png)

Terlihat jelas, kolom pesan terlalu panjang isinya sehingga terpotong, ini terjadi karena saya hanya menggunakan fungsi `$pdf->Cell`. Berikut saya lampirkan `snippet code`-nya :

```bash
while($hasil=mysqli_fetch_array($data)){
    $pdf->SetFillColor(255,255,255);
    $pdf->Cell(1,0.8,$no++,1,0,'C',true);
    $pdf->Cell(4,0.8,$hasil['tanggal'],1,0,'L',true);
    $pdf->Cell(20,0.8,$hasil['pesan'],1,0,'L',true);
    $pdf->Cell(3,0.8,$hasil['pengirim'],1,0,'L',true);
    $pdf->Ln();
}
```

Kemudian seperti biasa, saya bertanya kepada mbah dukun terhebat saya, **`Stackoverflow`**, ketemulah diskusi [disini](https://stackoverflow.com/questions/3477372/make-text-wrap-in-a-cell-with-fpdf), solusinya menyarankan untuk menggunakan fungsi `$pdf->MultiCell`.

Gak pake lama, langsung saya coba dan hasilnya :

![Tampilan PDF cantik, Auto Wrap Content Table dengan FPDF kedua](/img/fpdf-wrap-cell/2.png)

Haduuuhhh kok malah jadi berantakan, berikut `snippet code`-nya :

```bash
while($hasil=mysqli_fetch_array($data)){
    $pdf->SetFillColor(255,255,255);
    $pdf->Cell(1,0.8,$no++,1,0,'C',true);
    $pdf->Cell(4,0.8,$hasil['tanggal'],1,0,'L',true);
    $pdf->MultiCell(20,0.8,$hasil['pesan'],1,'L');
    $pdf->Cell(3,0.8,$hasil['pengirim'],1,0,'L',true);
    $pdf->Ln();
}
```

Tapi kalo dilihat-lihat dan agak sedikit dipikir, hhmmm... sepertinya gak bisa main `copy-paste` nih macam tugas kampus, rasanya tidak menghargai Tuhan kalo saya tidak memanfaatkan otak untuk berfikir, padahal sudah dikasih `gratis` sejak lahir, hehehe...

Merenung sejenak, `try-error-learn` berulang-ulang muter otak sampe semedi nongkrong di kamar mandi, dan akhirnya... taraaaa...

![Tampilan PDF cantik, Auto Wrap Content Table dengan FPDF ketiga](/img/fpdf-wrap-cell/3.png)

Maka, benar sabda `Kakek Bijak` :

> #### `Usaha` Tidak Akan Pernah `Mengkhianati Hasil`, Maka `Jangan Pernah Menyerah` !

berikut `snippet code` beserta penjelasan tiap barisnya :

```bash
while($hasil=mysqli_fetch_array($data)){
    $cellWidth=20; //lebar sel
	$cellHeight=1; //tinggi sel satu baris normal

	//periksa apakah teksnya melibihi kolom?
	if($pdf->GetStringWidth($hasil['pesan']) < $cellWidth){
		//jika tidak, maka tidak melakukan apa-apa
		$line=1;
	}else{
		//jika ya, maka hitung ketinggian yang dibutuhkan untuk sel akan dirapikan
		//dengan memisahkan teks agar sesuai dengan lebar sel
		//lalu hitung berapa banyak baris yang dibutuhkan agar teks pas dengan sel

		$textLength=strlen($hasil['pesan']);	//total panjang teks
		$errMargin=5;		//margin kesalahan lebar sel, untuk jaga-jaga
		$startChar=0;		//posisi awal karakter untuk setiap baris
		$maxChar=0;			//karakter maksimum dalam satu baris, yang akan ditambahkan nanti
		$textArray=array();	//untuk menampung data untuk setiap baris
		$tmpString="";		//untuk menampung teks untuk setiap baris (sementara)

		while($startChar < $textLength){ //perulangan sampai akhir teks
			//perulangan sampai karakter maksimum tercapai
			while(
			$pdf->GetStringWidth( $tmpString ) < ($cellWidth-$errMargin) &&
			($startChar+$maxChar) < $textLength ) {
				$maxChar++;
				$tmpString=substr($hasil['pesan'],$startChar,$maxChar);
			}
			//pindahkan ke baris berikutnya
			$startChar=$startChar+$maxChar;
			//kemudian tambahkan ke dalam array sehingga kita tahu berapa banyak baris yang dibutuhkan
			array_push($textArray,$tmpString);
			//reset variabel penampung
			$maxChar=0;
			$tmpString='';

		}
		//dapatkan jumlah baris
		$line=count($textArray);
	}

    //tulis selnya
    $pdf->SetFillColor(255,255,255);
	$pdf->Cell(1,($line * $cellHeight),$no++,1,0,'C',true); //sesuaikan ketinggian dengan jumlah garis
	$pdf->Cell(4,($line * $cellHeight),$hasil['tanggal'],1,0); //sesuaikan ketinggian dengan jumlah garis

	//memanfaatkan MultiCell sebagai ganti Cell
	//atur posisi xy untuk sel berikutnya menjadi di sebelahnya.
	//ingat posisi x dan y sebelum menulis MultiCell
	$xPos=$pdf->GetX();
	$yPos=$pdf->GetY();
	$pdf->MultiCell($cellWidth,$cellHeight,$hasil['pesan'],1);

	//kembalikan posisi untuk sel berikutnya di samping MultiCell
    //dan offset x dengan lebar MultiCell
	$pdf->SetXY($xPos + $cellWidth , $yPos);

    $pdf->Cell(3,($line * $cellHeight),$hasil['pengirim'],1,1); //sesuaikan ketinggian dengan jumlah garis
}
```
