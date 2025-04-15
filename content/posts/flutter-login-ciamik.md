---
title: "Membuat Tampilan Login Ciamik dengan Flutter"
slug: flutter-login-ciamik
date: 2019-03-13T22:02:53+07:00
draft: false
tags:
  - Flutter
  - Bahasa Pemrograman

image: ""
description: ""
---

## Apa itu Flutter?

Flutter adalah sebuah framework open-source yang dikembangkan oleh Google untuk membangun antarmuka (user interface/UI) aplikasi Android dan iOS.

Aplikasi yang kita buat dengan Flutter dapat di-build ke Android dan iOS. Ini untungnya belajar Flutter, sekali coding aplikasi, bisa digunakan pada Android dan iOS. Enak bukan?

Membuat user interface mobile yang menarik dengan code terkadang sulit dilakukan, namun tidak demikian jika menggunakan [Flutter](https://flutter.dev/) SDK Framework. Framework ini diklaim bisa membuat aplikasi mobile multi platform dan dapat membuat user interface yang menarik serta menjanjikan performa yang baik.

Sedikit informasi bagi yang masih ragu-ragu untuk mengadopsi Flutter :

1. Framework satu ini menjamin performa yang sangat mulus yaitu 60fps.
2. Satu-satunya multi platform reactive SDK yang tidak menggunakan Javascript.
3. Memiliki fitur Hot Reload yang sangat membantu dalam proses development, ngoding android terasa seperti ngoding web.
4. Kode di-compile ke native binary saat build untuk release.
5. Dan masih banyak lagi fitur menarik lainnya.

Sebenarnya saya ingin membuat tulisan cara instalasi flutter, berhubung sudah terlebih dahulu menginstall flutter sebelum bikin blog, maka saya skip, tetapi jangan khawatir mudah kok, kalo bingung bisa mengikuti panduan pada [halaman ini](https://flutter.dev/docs/get-started/install), kemudian jangan lupa install juga editor [VS Code](https://code.visualstudio.com/Download) dan ekstensi Dart [disini](https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code).

## Persiapan

Pertama-tama siapkan beberapa asset untuk gambar foto profil, logo, dan font.

- Foto profile ([profil.jpg](https://raw.githubusercontent.com/rifkyfu32/flutter-login-cantik/master/assets/profil.jpg))
- Logo aplikasi ([butterfly.png](https://raw.githubusercontent.com/rifkyfu32/flutter-login-cantik/master/assets/butterfly.png))
- Nunito font family ([Nunito.ttf](https://raw.githubusercontent.com/rifkyfu32/flutter-login-cantik/master/assets/Nunito.ttf))

## Membuat Projek

Jalankan editor VS Code, Selanjutnya buat projek baru dengan menekan kombinasi tombol `CTRL+SHIFT+P` dan tulis nama projeknya misalnya `login_cantik`. Untuk nama aplikasi harus huruf kecil semua dan tidak boleh mengandung spasi.

![Tampilan Login Ciamik dengan Flutter pertama](/img/flutter-login-ciamik/1.png)

Selanjutnya buat folder `assets` pada direktori projek dan salin semua file persiapan (profil.jpg, butterfly.png, nunito.ttf) ke dalam folder `assets` tersebut.

![Tampilan Login Ciamik dengan Flutter kedua](/img/flutter-login-ciamik/2.png)
![Tampilan Login Ciamik dengan Flutter ketiga](/img/flutter-login-ciamik/3.png)

File-file ini harus dijelaskan terlebih dahulu pada file `pubspec.yaml` agar dapat digunakan, tambahkan baris berikut ini tepat di bawah konfigurasi `flutter` seperti ini.

![Tampilan Login Ciamik dengan Flutter keempat](/img/flutter-login-ciamik/4.png)

```bash
flutter:
  uses-material-design: true
  assets:
    - assets/butterfly.png
    - assets/profil.jpg
  fonts:
    - family: Nunito
      fonts:
          - asset: assets/Nunito.ttf
```

Kemudian pada file main.dart hapus semua code hingga yang tersisa hanya class MyApp seperti ini:

```bash
import 'package:flutter/material.dart';

void main() => runApp(MyApp());
```

## Halaman Login

Buat file baru dengan klik kanan pada folder lib selanjutnya beri nama `login_page.dart`. Pada halaman login ini kita membutuhkan beberapa widget yaitu widget gambar untuk logo, field untuk email, field untuk password, tombol login, dan terakhir adalah tombol flat untuk lupa password. Selengkapnya code untuk `login_page.dart` seperti ini:

```bash
import 'package:flutter/material.dart';
import 'home_page.dart';

class LoginPage extends StatefulWidget {
  static String tag = 'login-page';
  @override
  _LoginPageState createState() => new _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  @override
  Widget build(BuildContext context) {
    final logo = Hero(
      tag: 'hero',
      child: CircleAvatar(
        backgroundColor: Colors.transparent,
        radius: 48.0,
        child: Image.asset('assets/butterfly.png'),
      ),
    );

    final email = TextFormField(
      keyboardType: TextInputType.emailAddress,
      autofocus: false,
      initialValue: 'profil@gmail.com',
      decoration: InputDecoration(
        hintText: 'Email',
        contentPadding: EdgeInsets.fromLTRB(20.0, 10.0, 20.0, 10.0),
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(32.0)),
      ),
    );

    final password = TextFormField(
      autofocus: false,
      initialValue: 'terserah',
      obscureText: true,
      decoration: InputDecoration(
        hintText: 'Password',
        contentPadding: EdgeInsets.fromLTRB(20.0, 10.0, 20.0, 10.0),
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(32.0)),
      ),
    );

    final loginButton = Padding(
      padding: EdgeInsets.symmetric(vertical: 16.0),
      child: RaisedButton(
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(24),
        ),
        onPressed: () {
          Navigator.of(context).pushNamed(HomePage.tag);
        },
        padding: EdgeInsets.all(12),
        color: Colors.lightBlueAccent,
        child: Text('Log In', style: TextStyle(color: Colors.white)),
      ),
    );

    final forgotLabel = FlatButton(
      child: Text(
        'Lupa password?',
        style: TextStyle(color: Colors.black54),
      ),
      onPressed: () {},
    );

    return Scaffold(
      backgroundColor: Colors.white,
      body: Center(
        child: ListView(
          shrinkWrap: true,
          padding: EdgeInsets.only(left: 24.0, right: 24.0),
          children: <Widget>[
            logo,
            SizedBox(height: 48.0),
            email,
            SizedBox(height: 8.0),
            password,
            SizedBox(height: 24.0),
            loginButton,
            forgotLabel
          ],
        ),
      ),
    );
  }
}
```

## Halaman Utama

Berikutnya buat file baru untuk halaman utama dengan nama `home_page.dart`. Pada halaman ini kita hanya akan menampikan widget foto profil dari aset `profil.jpg` dan sebuah widget text untuk informasi tambahan. Widget foto profil tersebut akan dibungkus oleh widget `Hero`, dengan nama tag yang sama seperti tag hero logo pada `login_page.dart`. Tuliskan kodenya seperti ini:

```bash
import 'package:flutter/material.dart';

class HomePage extends StatelessWidget {
  static String tag = 'home-page';

  @override
  Widget build(BuildContext context) {
    final profil = Hero(
      tag: 'hero',
      child: Padding(
        padding: EdgeInsets.all(16.0),
        child: CircleAvatar(
          radius: 72.0,
          backgroundColor: Colors.transparent,
          backgroundImage: AssetImage('assets/profil.jpg'),
        ),
      ),
    );

    final welcome = Padding(
      padding: EdgeInsets.all(8.0),
      child: Text(
        'Selamat datang',
        style: TextStyle(fontSize: 28.0, color: Colors.white),
      ),
    );

    final paragraf1 = Padding(
      padding: EdgeInsets.all(8.0),
      child: Text(
        'Halo, nama saya Akhmad Fuady Rifkiyanto, Sering dipanggil Rifki (di rumah) dan Fuad (di kampus).',
        style: TextStyle(fontSize: 16.0, color: Colors.white),
      ),
    );

    final paragraf2 = Padding(
      padding: EdgeInsets.all(8.0),
      child: Text(
        'Saat ini, saya adalah freelance di salah satu instansi di Kabupaten Batang.',
        style: TextStyle(fontSize: 16.0, color: Colors.white),
      ),
    );

    final paragraf3 = Padding(
      padding: EdgeInsets.all(8.0),
      child: Text(
        'Pernah menempuh pendidikan di STMIK Widya Pratama Pekalongan mengambil program studi Teknik Informatika.',
        style: TextStyle(fontSize: 16.0, color: Colors.white),
      ),
    );

    final body = Container(
      width: MediaQuery.of(context).size.width,
      padding: EdgeInsets.all(28.0),
      decoration: BoxDecoration(
        gradient: LinearGradient(colors: [
          Colors.blue,
          Colors.lightBlueAccent,
        ]),
      ),
      child: Column(
        children: <Widget>[profil, welcome, paragraf1,paragraf2,paragraf3],
      ),
    );

    return Scaffold(
      body: body,
    );
  }
}
```

## Sentuhan Terakhir

Selanjutnya kembali pada kembali pada main.dart, tambahkan kode untuk navigasi router, atur atribut routes widget MaterialApp dengan objek routes diatas, atur juga untuk property home menjadi objek dari login_page seperti ini LoginPage(). Sehingga kode lengkap untuk main sebagai berikut:

```bash
import 'package:flutter/material.dart';
import 'login_page.dart';
import 'home_page.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  final routes = <String, WidgetBuilder>{
    LoginPage.tag: (context) => LoginPage(),
    HomePage.tag: (context) => HomePage(),
  };

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Kodeversitas',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.lightBlue,
        fontFamily: 'Nunito',
      ),
      home: LoginPage(),
      routes: routes,
    );
  }
}
```

Selesai. sekarang jalankan aplikasi Flutter dengan menekan tombol F5 namun sebelumnya jangan lupa start Android Emulator atau iOS Simulator.

![Tampilan Login Ciamik dengan Flutter kelima](/img/flutter-login-ciamik/5.png)

Hasilnya akan terlihat seperti berikut ini:

![Tampilan Login Ciamik dengan Flutter keenam](/img/flutter-login-ciamik/6.png)
![Tampilan Login Ciamik dengan Flutter ketujuh](/img/flutter-login-ciamik/7.png)
