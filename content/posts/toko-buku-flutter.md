---
title: "Membangun Aplikasi Toko Buku Multiplatform dengan Flutter"
slug: toko-buku-flutter
date: 2019-03-15T21:40:35+07:00
draft: false
tags:
  - Flutter
  - Bahasa Pemrograman

image: ""
description: ""
---

**Siapa bilang membuat aplikasi mobile multiplatform itu sulit?**

Dengan [Flutter](https://flutter.dev/) semua terasa mudah, karena `everything is a widget`, membuat widget yang ringan dan dapat digunakan kembali, ngoding terasa lebih ringkas dan lebih efisien, apalagi sekali ngoding bisa di-build ke `Android` dan `iOS`.

Kali ini kita akan membuat aplikasi sederhana toko buku, sebelum itu bagi anda yang belum pernah ngoding dengan `flutter` sebaiknya anda membaca artikel saya sebelumnya yang berjudul [Membuat Tampilan Login Ciamik dengan Flutter](/flutter-login-ciamik) agar lebih mudah mengikuti tutorial kali ini.

## Persiapan

Download asset gambar untuk aplikasi yang akan kita buat.

- [Buku Webmaster](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/webmaster.jpeg)
- [Buku InDesign](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/indesign.jpg)
- [Buku Sketchup](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/sketchup.jpeg)
- [Buku Photoshop](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/photoshop.jpg)
- [Buku 3ds Max](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/max_3d.jpeg)
- [Buku Adobe Premier](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/premier.jpg)
- [Buku Autodesk Maya](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/maya.jpeg)
- [Buku CorelDraw](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/corel.jpg)
- [Buku Dafter](https://raw.githubusercontent.com/rifkyfu32/Toko-Buku-Flutter/master/assets/drafter.jpg)

## Membuat Projek

Jalankan editor VS Code, selanjutnya buat projek baru dengan menekan kombinasi tombol `CTRL+SHIFT+P` dan tulis nama projeknya misalnya `toko_buku`. Untuk nama aplikasi harus huruf kecil semua dan tidak boleh mengandung spasi.

Selanjutnya buat folder `assets` pada direktori projek dan salin semua file persiapan yang sudah kita download ke dalam folder `assets` tersebut.

Jangan lupa untuk mendeklarasikan file-file tadi pada file `pubspec.yaml` agar dapat digunakan, berikut ini `snippet code`-nya :

```bash
name: toko_buku
description: A new Flutter project.

version: 1.0.0+1

environment:
  sdk: ">=2.1.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^0.1.2

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true
  assets:
    - assets/webmaster.jpeg
    - assets/indesign.jpg
    - assets/sketchup.jpeg
    - assets/photoshop.jpg
    - assets/max_3d.jpeg
    - assets/premier.jpg
    - assets/maya.jpeg
    - assets/corel.jpg
    - assets/drafter.jpg

}
```

## Dummy Data

Buat file baru dengan klik kanan pada folder lib selanjutnya beri nama `data.dart`. Kita akan membuat `sample` data yang nantinya akan ditampilkan di halaman utama, berikut ini `snippet code`-nya :

```bash
class Book {
  String title,
      writer,
      price,
      image,
      description =
          'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum id neque libero. Donec finibus sem viverra, luctus nisi ac, semper enim. Vestibulum in mi feugiat, mattis erat suscipit, fermentum quam. Mauris non urna sed odio congue rhoncus. \nAliquam a dignissim ex. Suspendisse et sem porta, consequat dui et, placerat tortor. Sed elementum nunc a blandit euismod. Cras condimentum faucibus dolor. Etiam interdum egestas sagittis. Aliquam vitae molestie eros. Cras porta felis ac eros pellentesque, sed lobortis mi eleifend. Praesent ut.';
  int pages;
  double rating;

  Book(
      this.title, this.writer, this.price, this.image, this.rating, this.pages);
}

final List<Book> books = [
  Book('CorelDraw untuk Tingkat Pemula Sampai Mahir', 'Jubilee Enterprise',
      'Rp 50.000', 'assets/corel.jpg', 3.5, 123),
  Book('Buku Pintar Drafter Untuk Pemula Hingga Mahir', 'Widada', 'Rp 55.000',
      'assets/drafter.jpg', 4.5, 200),
  Book('Adobe InDesign: Seri Panduan Terlengkap', 'Jubilee Enterprise',
      'Rp 60.000', 'assets/indesign.jpg', 5.0, 324),
  Book('Pemodelan Objek Dengan 3Ds Max 2014', 'Wahana Komputer', 'Rp 58.000',
      'assets/max_3d.jpeg', 3.0, 200),
  Book('Penerapan Visualisasi 3D Dengan Autodesk Maya', 'Dhani Ariatmanto',
      'Rp 90.000', 'assets/maya.jpeg', 4.8, 234),
  Book('Teknik Lancar Menggunakan Adobe Photoshop', 'Jubilee Enterprise',
      'Rp 57.000', 'assets/photoshop.jpg', 4.5, 240),
  Book('Adobe Premiere Terlengkap dan Termudah', 'Jubilee Enterprise',
      'Rp 56.000', 'assets/premier.jpg', 4.8, 432),
  Book('Cad Series : Google Sketchup Untuk Desain 3D', 'Wahana Komputer',
      'Rp 55.000', 'assets/sketchup.jpeg', 4.5, 321),
  Book('Webmaster Series : Trik Cepat Menguasai CSS', 'Wahana Komputer',
      'Rp 54.000', 'assets/webmaster.jpeg', 3.5, 431),
];
```

## Tampilan Rating Bar

Berikutnya buat file baru untuk membuat tampilan `rating bar` dengan nama `rating_bar.dart`, berikut ini `snippet code`-nya :

```bash
import 'package:flutter/material.dart';

class RatingBar extends StatelessWidget {
  final int starCount;
  final double rating;
  final Color color;

  RatingBar(
      {this.starCount = 5, this.rating = 0.0, this.color = Colors.black87});

  ///create star
  Widget buildStar(BuildContext context, int index) {
    IconData icName = Icons.star;
    Color icColor = color;

    if (index >= rating) {
      icName = Icons.star_border;
      icColor = color.withOpacity(0.6);
    } else if (index > rating - 1 && index < rating) {
      icName = Icons.star_half;
    }

    return Icon(icName, size: 16.0, color: icColor);
  }

  @override
  Widget build(BuildContext context) {
    return Row(
      children: List.generate(starCount, (i) => buildStar(context, i)),
    );
  }
}
```

## Halaman Detail

Selanjutnya kita akan membuat halaman detail informasi dari buku yang dipilih, buat file baru dengan nama `detail.dart`, berikut ini `snippet code`-nya :

```bash
import 'data.dart';
import 'rating_bar.dart';
import 'package:flutter/material.dart';

class Detail extends StatelessWidget {
  final Book book;

  Detail(this.book);

  @override
  Widget build(BuildContext context) {
    //app bar
    final appBar = AppBar(
      elevation: .5,
      title: Text('Toko Buku'),
      actions: <Widget>[
        IconButton(
          icon: Icon(Icons.search),
          onPressed: () {},
        )
      ],
    );

    final topLeft = Column(
      children: <Widget>[
        Padding(
          padding: EdgeInsets.all(16.0),
          child: Hero(
            tag: book.title,
            child: Material(
              elevation: 15.0,
              shadowColor: Colors.purple.shade900,
              child: Image(
                image: AssetImage(book.image),
                fit: BoxFit.cover,
              ),
            ),
          ),
        ),
        text('${book.pages} halaman', color: Colors.white30, size: 12)
      ],
    );

    ///detail top right
    final topRight = Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: <Widget>[
        text(book.title,
            size: 16, isBold: true,color: Colors.white70, padding: EdgeInsets.only(top: 16.0)),
        text(
          'oleh ${book.writer}',
          color: Colors.white30,
          size: 12,
          padding: EdgeInsets.only(top: 8.0, bottom: 16.0),
        ),
        Row(
          children: <Widget>[
            text(
              book.price,
              isBold: true,
              color: Colors.white70,
              padding: EdgeInsets.only(right: 8.0),
            ),
            RatingBar(rating: book.rating,color: Colors.white70)
          ],
        ),
        SizedBox(height: 32.0),
        Material(
          borderRadius: BorderRadius.circular(20.0),
          shadowColor: Colors.blue.shade200,
          elevation: 5.0,
          child: MaterialButton(
            onPressed: () {},
            minWidth: 160.0,
            color: Colors.blue,
            child: text('BELI', color: Colors.white, size: 13),
          ),
        )
      ],
    );

    final topContent = Container(
      color: Theme.of(context).primaryColor,
      padding: EdgeInsets.only(bottom: 16.0),
      child: Row(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: <Widget>[
          Flexible(flex: 2, child: topLeft),
          Flexible(flex: 3, child: topRight),
        ],
      ),
    );

    ///scrolling text description
    final bottomContent = Container(
      height: 220.0,
      child: SingleChildScrollView(
        padding: EdgeInsets.all(16.0),
        child: Text(
          book.description,
          style: TextStyle(fontSize: 13.0, height: 1.5),
        ),
      ),
    );

    return Scaffold(
      appBar: appBar,
      body: Column(
        children: <Widget>[topContent, bottomContent],
      ),
    );
  }

  ///create text widget
  text(String data,
          {Color color = Colors.black87,
          num size = 14,
          EdgeInsetsGeometry padding = EdgeInsets.zero,
          bool isBold = false}) =>
      Padding(
        padding: padding,
        child: Text(
          data,
          style: TextStyle(
              color: color,
              fontSize: size.toDouble(),
              fontWeight: isBold ? FontWeight.bold : FontWeight.normal),
        ),
      );
}

```

## Halaman Utama

Berikutnya buat file baru untuk halaman utama dengan nama `home.dart`. Pada halaman ini kita akan menampilkan daftar buku berupa gambar dengan `assets` yang sudah kita siapkan tadi, berikut ini `snippet code`-nya :

```bash
import 'data.dart';
import 'package:flutter/material.dart';

class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //app bar
    final appBar = AppBar(
      elevation: .5,
      leading: IconButton(
        icon: Icon(Icons.menu),
        onPressed: () {},
      ),
      title: Text('Toko Buku'),
      actions: <Widget>[
        IconButton(
          icon: Icon(Icons.search),
          onPressed: () {},
        )
      ],
    );

    ///create book tile hero
    createTile(Book book) => Hero(
          tag: book.title,
          child: Material(
            elevation: 15.0,
            shadowColor: Colors.purple.shade900,
            child: InkWell(
              onTap: () {
                Navigator.pushNamed(context, 'detail/${book.title}');
              },
              child: Image(
                image: AssetImage(book.image),
                fit: BoxFit.cover,
              ),
            ),
          ),
        );

    ///create book grid tiles
    final grid = CustomScrollView(
      primary: false,
      slivers: <Widget>[
        SliverPadding(
          padding: EdgeInsets.all(16.0),
          sliver: SliverGrid.count(
            childAspectRatio: 2 / 3,
            crossAxisCount: 3,
            mainAxisSpacing: 20.0,
            crossAxisSpacing: 20.0,
            children: books.map((book) => createTile(book)).toList(),
          ),
        )
      ],
    );

    return Scaffold(
      backgroundColor: Theme.of(context).primaryColor,
      appBar: appBar,
      body: grid,
    );
  }
}
```

## Sentuhan Terakhir

Selanjutnya kita ubah main.dart, hapus semua kemudian ganti dengan `snippet code` berikut ini :

```bash
import 'package:flutter/material.dart';
import 'data.dart';
import 'detail.dart';
import 'home.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Toko Buku',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.purple,
        platform: TargetPlatform.iOS,
      ),
      home: Home(),
      onGenerateRoute: (settings) => generateRoute(settings),
    );
  }

  generateRoute(RouteSettings settings) {
    final path = settings.name.split('/');
    final title = path[1];

    Book book = books.firstWhere((it) => it.title == title);
    return MaterialPageRoute(
      settings: settings,
      builder: (context) => Detail(book),
    );
  }
}
```

Selesai. sekarang jalankan aplikasi `Toko Buku` dengan menekan tombol F5, namun sebelumnya jangan lupa start Android Emulator atau iOS Simulator.
![Tampilan Aplikasi Toko Buku pertama](/img/toko-buku-flutter/1.png)

Hasilnya akan terlihat seperti berikut ini:

![Tampilan Aplikasi Toko Buku kedua](/img/toko-buku-flutter/2.png)

![Tampilan Aplikasi Toko Buku ketiga](/img/toko-buku-flutter/3.png)
