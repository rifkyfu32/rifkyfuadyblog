---
title: "Aplikasi Dragon Ball dengan Animasi di Flutter"
slug: flutter-animasi-dragonball
date: 2019-04-01T21:58:46+07:00
draft: false
tags:
  - Flutter
  - Bahasa Pemrograman

image: ""
description: ""
---

**Siapa yang gak tau Dragon Ball hayoo?**

Ketika dahulu saya masih kecil, teringat jelas setiap hari minggu adalah hari paling ditunggu, setiap jam 09.00 WIB di Indosiar setia menonton film animasi `Dragon Ball`, televisi saat itu masih berbentuk tabung dan nonton bareng sama tetangga saya dekat rumah.

Kali ini kita akan belajar bikin aplikasi karakter `Dragon Ball` dengan animasi sederhana di [Flutter](https://flutter.dev/) sambil ber-_nostalgia_ mengingat karakter-karakter yang ada di film animasi `Dragon Ball`.

**# Persiapan**

Seperti biasa, buka visual studio code, bikin projek baru. Kemudian bikin folder assets/images untuk menaruh gambar dari karakter `Dragon Ball`.

Download gambar karakter dibawah dan taruh di folder assets/images.

- [Boo](https://raw.githubusercontent.com/rifkyfu32/Dragon-Ball-Flutter/master/assets/images/boo.png)
- [Broly](https://raw.githubusercontent.com/rifkyfu32/Dragon-Ball-Flutter/master/assets/images/broly.png)
- [Cell](https://raw.githubusercontent.com/rifkyfu32/Dragon-Ball-Flutter/master/assets/images/cell.png)
- [Frieza](https://raw.githubusercontent.com/rifkyfu32/Dragon-Ball-Flutter/master/assets/images/frieza.png)
- [Gohan](https://raw.githubusercontent.com/rifkyfu32/Dragon-Ball-Flutter/master/assets/images/gohan.png)
- [Goku](https://raw.githubusercontent.com/rifkyfu32/Dragon-Ball-Flutter/master/assets/images/goku.png)
- [Vegeta](https://raw.githubusercontent.com/rifkyfu32/Dragon-Ball-Flutter/master/assets/images/vegeta.png)

**# Ubah pubspec.yaml**

Deklarasikan file-file tadi pada file `pubspec.yaml` agar dapat digunakan, berikut ini `snippet code`-nya :

```bash
name: dragonball_flutter
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
    - assets/images/
```

**# Bikin Class Karakter**

Buat file baru dengan klik kanan pada folder lib selanjutnya beri nama `karakter.dart`, berikut ini `snippet code`-nya :

```bash
class Karakter {
  final String avatar;
  final String title;
  final String description;
  final int color;

  Karakter({
    this.avatar,
    this.title,
    this.description,
    this.color,
  });
}

//sumber: https://www.giantbomb.com/dragon-ball-z/3025-159/characters/
final karakters = <Karakter>[
  Karakter(
    title: "Goku",
    description:
        "Goku adalah pemeran utama protagonis dalam franchise Dragon Ball dan salah satu pejuang terkuat di alam semesta. Dia adalah seorang prajurit Saiyan yang nama aslinya adalah Kakarot, putra Bardock. Dia adalah suami dari Chi Chi, dan ayah dari Gohan dan Goten. Dia juga Kakek ke Pan.",
    avatar: "assets/images/goku.png",
    color: 0xFFE83835,
  ),
  Karakter(
    title: "Vegeta",
    description:
        "Pangeran dari semua Saiyan, Vegeta adalah pejuang Saiyan elit yang sangat kuat. Dalam perjuangan konstannya untuk melampaui saingannya yang abadi Goku, ia telah menjadi salah satu pejuang paling kuat di alam semesta.",
    avatar: "assets/images/vegeta.png",
    color: 0xFF238BD0,
  ),
  Karakter(
    title: "Gohan",
    description:
        "Gohan adalah putra Goku dan salah satu pahlawan di alam semesta Dragon Ball Z. Dia juga protagonis dari Cell Saga, di mana dia adalah orang pertama yang mencapai bentuk Super Saiyan 2, melalui kemarahan dan emosi yang luar biasa. Dalam bentuk Ultimate kemudian, ia dianggap sebagai prajurit paling kuat di Dragon Ball Z. Dia adalah kakak Goten dan ayah Pan. Istrinya adalah Videl dan kakeknya adalah Bardock.",
    avatar: "assets/images/gohan.png",
    color: 0xFF354C6C,
  ),
  Karakter(
    title: "Frieza",
    description:
        "Di Dragon Ball Z universe, Frieza adalah salah satu penjahat pertama yang benar-benar menguji Goku.",
    avatar: "assets/images/frieza.png",
    color: 0xFF6F2B62,
  ),
  Karakter(
    title: "Cell",
    description:
        "Cell adalah android yang dibangun dari sel-sel yang diambil dari beberapa pejuang dalam Dragon Ball Z universe. Dia adalah antagonis utama dari Saga Android Dragon Ball.",
    avatar: "assets/images/cell.png",
    color: 0xFF447C12,
  ),
  Karakter(
    title: "Majin Buu",
    description:
        "Salah satu karakter Dragon Ball Z yang paling ganas dan senang transformasi, Majin Buu adalah musuh besar terakhir dalam alur cerita Dragon Ball Z. Dengan kemampuan untuk menyerap musuh, belajar bergerak, dan memberikan pukulan serius, Majin Buu adalah salah satu musuh Goku dan teman yang paling menantang.",
    avatar: "assets/images/boo.png",
    color: 0xFFE7668E,
  ),
  Karakter(
    title: "Broly",
    description:
        "Sang Legendaris Super Saiyan, Broly adalah salah satu penjahat Saiyan Dragon Ball Z yang paling kuat dan destruktif.",
    avatar: "assets/images/broly.png",
    color: 0xFFBD9158,
  ),
];
```

**# Halaman Detail**

Selanjutnya kita akan membuat halaman detail informasi dari setiap karakter yang dipilih, buat file baru dengan nama `detail.dart`, berikut ini `snippet code`-nya :

```bash
import 'package:flutter/material.dart';
import 'karakter.dart';

class Detail extends StatefulWidget {
  final Karakter karakter;

  const Detail({
    Key key,
    @required this.karakter,
  }) : super(key: key);

  @override
  _DetailState createState() => _DetailState();
}

class _DetailState extends State<Detail>
    with SingleTickerProviderStateMixin {
  AnimationController _controller;

  @override
  void initState() {
    _controller =
        AnimationController(vsync: this, duration: Duration(milliseconds: 500));
    _controller.forward();
    super.initState();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        Hero(
          tag: "background_${widget.karakter.title}",
          child: Container(
            color: Color(widget.karakter.color),
          ),
        ),
        Scaffold(
          backgroundColor: Colors.transparent,
          appBar: AppBar(
            backgroundColor: Color(widget.karakter.color),
            elevation: 0,
            title: Text(widget.karakter.title),
            leading: CloseButton(),
          ),
          body: SingleChildScrollView(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              children: [
                Hero(
                  tag: "image_${widget.karakter.title}",
                  child: Image.asset(
                    widget.karakter.avatar,
                    height: MediaQuery.of(context).size.height / 2,
                  ),
                ),
                AnimatedBuilder(
                  animation: _controller,
                  builder: (context, widget) => Transform.translate(
                        transformHitTests: false,
                        offset: Offset.lerp(
                            Offset(0.0, 200.0), Offset.zero, _controller.value),
                        child: widget,
                      ),
                  child: Padding(
                    padding: EdgeInsets.all(10),
                    child: Text(
                      widget.karakter.description,
                      style: TextStyle(
                        fontSize: 18,
                        color: Colors.white,
                        fontWeight: FontWeight.w400,
                      ),
                    ),
                  ),
                ),
              ],
            ),
          ),
        )
      ],
    );
  }
}
```

**# Sentuhan Terakhir**

Selanjutnya kita ubah main.dart, hapus semua kemudian ganti dengan `snippet code` berikut ini :

```bash
import 'package:flutter/material.dart';
import 'detail.dart';
import 'karakter.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Dragon Ball',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ListPage(),
    );
  }
}

class ListPage extends StatefulWidget {
  @override
  _ListPageState createState() => _ListPageState();
}

class _ListPageState extends State<ListPage> {
  PageController _controller;

  _goToDetail(Karakter karakter) {
    final page = Detail(karakter: karakter);
    Navigator.of(context).push(
      PageRouteBuilder<Null>(
          pageBuilder: (BuildContext context, Animation<double> animation,
              Animation<double> secondaryAnimation) {
            return AnimatedBuilder(
                animation: animation,
                builder: (BuildContext context, Widget child) {
                  return Opacity(
                    opacity: animation.value,
                    child: page,
                  );
                });
          },
          transitionDuration: Duration(milliseconds: 400)),
    );
  }

  _pageListener() {
    setState(() {});
  }

  @override
  void initState() {
    _controller = PageController(viewportFraction: 0.6);
    _controller.addListener(_pageListener);
    super.initState();
  }

  @override
  void dispose() {
    _controller.removeListener(_pageListener);
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Dragon Ball"),
        backgroundColor: Colors.black54,
      ),
      body: PageView.builder(
          scrollDirection: Axis.vertical,
          controller: _controller,
          itemCount: karakters.length,
          itemBuilder: (context, index) {
            double currentPage = 0;
            try {
              currentPage = _controller.page;
            } catch (_) {}

            final resizeFactor =
                (1 - (((currentPage - index).abs() * 0.3).clamp(0.0, 1.0)));
            final karakterSekarang = karakters[index];
            return ListItem(
              karakter: karakterSekarang,
              resizeFactor: resizeFactor,
              onTap: () => _goToDetail(karakterSekarang),
            );
          }),
    );
  }
}

class ListItem extends StatelessWidget {
  final Karakter karakter;
  final double resizeFactor;
  final VoidCallback onTap;

  const ListItem({
    Key key,
    @required this.karakter,
    @required this.resizeFactor,
    @required this.onTap,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    double height = MediaQuery.of(context).size.height * 0.4;
    double width = MediaQuery.of(context).size.width * 0.85;
    return InkWell(
      onTap: onTap,
      child: Align(
        alignment: Alignment.topCenter,
        child: Container(
            width: width * resizeFactor,
            height: height * resizeFactor,
            child: Stack(
              children: [
                Positioned(
                  left: 0,
                  right: 0,
                  top: height / 4,
                  bottom: 0,
                  child: Hero(
                    tag: "background_${karakter.title}",
                    child: Card(
                      clipBehavior: Clip.antiAliasWithSaveLayer,
                      elevation: 10,
                      shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(15)),
                      child: DecoratedBox(
                        decoration: BoxDecoration(
                            gradient: LinearGradient(
                                begin: Alignment.topCenter,
                                end: Alignment.bottomCenter,
                                colors: [
                              Color(karakter.color),
                              Colors.white,
                            ],
                                stops: [
                              0.4,
                              1.0,
                            ])),
                        child: Container(
                          alignment: Alignment.bottomLeft,
                          margin: EdgeInsets.only(
                            left: 20,
                            bottom: 10,
                          ),
                          child: Text(
                            karakter.title,
                            style: TextStyle(
                              fontSize: 24 * resizeFactor,
                              fontWeight: FontWeight.w600,
                            ),
                          ),
                        ),
                      ),
                    ),
                  ),
                ),
                Align(
                  alignment: Alignment.topRight,
                  child: Hero(
                    tag: "image_${karakter.title}",
                    child: Image.asset(
                      karakter.avatar,
                      width: width / 2,
                      height: height,
                    ),
                  ),
                ),
              ],
            )),
      ),
    );
  }
}
```

Selesai. sekarang jalankan aplikasi `Dragon Ball` dengan menekan tombol F5, namun sebelumnya jangan lupa start Android Emulator atau iOS Simulator.

Hasilnya akan terlihat seperti berikut ini:

![Tampilan Aplikasi Mobile](/img/flutter-animasi-dragonball/dragon-ball.gif)
