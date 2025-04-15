---
title: "Membuat aplikasi konverter youtube ke Mp3 mutiplatform"
slug: konverter-youtube-mp3
date: 2019-04-08T20:29:06+07:00
draft: false
tags:
  - Flutter
  - Bahasa Pemrograman

image: ""
description: ""
---

Sering sekali saya menemukan lagu yang menurut pendapat saya bagus di [Youtube](https://youtube.com), akan tetapi saya hanya ingin mendengarkan lagunya saja tidak dengan videonya.

Alih-alih ingin menghemat kuota internet dirumah (Indihome berkuota :joy:), saya sering melakukan konvert youtube ke mp3 dengan aplikasi web ini [Online Video Converter](https://www.onlinevideoconverter.com/mp3-converter) kalo saya sedang memakai komputer...

**Bagaimana kalo di smartphone?**

Beberapa kali saya mencoba donwload aplikasi dari Apps Store ada dua jenis aplikasi, yaitu aplikasi gratis tetapi banyak iklan atau yang tidak ada iklan tetapi berbayar, hehe... :sweat_smile:

**Gimana kalo coba bikin aplikasi konverter youtube ke Mp3 sendiri?**

Yaps, bisa donk. Semenjak bercinta dengan [Flutter](https://flutter.dev/) bikin aplikasi mobile multiplatform (Android/IOS) jadi mudah, karena `everything is a widget` !!!

Kita akan menggunakan tools [Youtube Donwloader](https://y2mate.com/) untuk mengambil data dan konversi ke format MP3.

**# Persiapan**

Seperti biasa, jalankan editor Visual Studio Code, Selanjutnya buat projek baru dengan menekan kombinasi tombol `CTRL+SHIFT+P` dan tulis nama projeknya misalnya `konverter-youtube-mp3`. Untuk nama aplikasi harus huruf kecil semua dan tidak boleh mengandung spasi.

**# Tambahkan library**

Untuk menambahkan libarary yang akan kita gunakan, buka dan edit file `pubspec.yaml` seperti dibawah ini :

```bash
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^0.1.2
  http: ^0.12.0+2
  toast: ^0.1.4
  font_awesome_flutter: ^8.4.0
  dio: ^2.1.0
  path_provider: ^0.5.0+1
  simple_permissions: ^0.1.9
```

**# Bikin class model**

Untuk membuat object dari data [Youtube Donwloader](https://y2mate.com/), bikin file baru beri nama `youtube_model.dart`, berikut ini `snippet code`-nya :

```bash
class Result {
  String id;
  String vid;
  String ajax;
  String ftype;
  String fquality;
  String audioName;
  String thumbnail;
  String duration;

  Result(
      {this.id,
      this.vid,
      this.ajax,
      this.ftype,
      this.fquality,
      this.audioName,
      this.thumbnail,
      this.duration});

  Result.convertResult(String inpute) {
    id = RegExp(r"\\n_id: '(.*?)',").firstMatch(inpute).group(1);
    vid = RegExp(r"v_id: '(.*?)',").firstMatch(inpute).group(1);
    audioName = RegExp(r"data_vtitle = \\" "(.*?)\\" ";").firstMatch(inpute).group(1).replaceAll(RegExp('"\\"|"'), "").replaceAll("\\", "");
    thumbnail = RegExp(r'<img src=\\"(.*?)\\"').firstMatch(inpute).group(1).replaceAll("\\", "");
    duration = RegExp(r'>Duration:.(.*?)<').firstMatch(inpute).group(1);
    fquality = "128";
    ajax = "1";
    ftype = ".mp3";
  }
}
```

**# Halaman Utama**

Selanjutnya untuk membuat halaman utama, buat file baru dengan nama `youtube_konversi.dart`, berikut ini `snippet code`-nya :

```bash
import 'dart:io';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'youtube_model.dart';
import 'package:font_awesome_flutter/font_awesome_flutter.dart';
import 'package:simple_permissions/simple_permissions.dart';
import 'package:toast/toast.dart';
import 'package:path_provider/path_provider.dart';
import 'package:dio/dio.dart';

class YoutubeKonversi extends StatefulWidget {
  @override
  _YoutubeKonversiState createState() => _YoutubeKonversiState();
}

class _YoutubeKonversiState extends State<YoutubeKonversi> {
  bool _allowWriteFile = false;
  TextEditingController videoURL = TextEditingController();
  Result video;
  bool isFetching = false;
  bool fetchSuccess = false;
  bool isDownloading = false;
  bool downloadsuccess = false;
  String status = "Unduh ";
  String progress = "";
  String lokasi = "";

  Map<String, String> headers = {
    "X-Requested-With": "XMLHttpRequest",
  };

  Map<String, String> body;

  void insertBody(String videoURL) {
    body = {"url": videoURL, "ajax": "1"};
  }

  Future<void> getInfo() async {
    insertBody(videoURL.text);
    setState(() {
      progress = "";
      lokasi = "";
      status = "Unduh";
      downloadsuccess = false;
      isDownloading = false;
      isFetching = true;
      fetchSuccess = false;
    });
    try {
      var response = await http.post("https://y2mate.com/id/analyze/ajax",
          body: body, headers: headers);

      video = Result.convertResult(response.body);
      setState(() {
        isFetching = false;
        fetchSuccess = true;
      });
    } catch (e) {
      print(e.toString());
      setState(() {
        isFetching = true;
        fetchSuccess = false;
      });
    }
    print("${video.thumbnail}\n${video.audioName}\n${video.vid}\n${video.id}");
  }

  Future<void> directURI(
      String _id, String vid, String ajax, String ftype, String quality) async {
    setState(() {
      isDownloading = true;
      status = "Mengunduh...";
    });
    try {
      var bodies = {
        "type": "youtube",
        "_id": _id,
        "v_id": vid,
        "ajax": ajax,
        "ftype": ftype.replaceAll(".", ""),
        "fquality": quality,
      };
      var response =
          await http.post("https://y2mate.com/id/convert", body: bodies);
      print(response.body);
      if (response.body.contains("Error:")) {
        Toast.show(
          "Tidak dapat mengunduh \n Silakan coba lagi nanti ...",
          context,
          duration: 4,
          textColor: Colors.white,
          gravity: Toast.BOTTOM,
        );
        setState(() {
          isDownloading = false;
        });
        return;
      }
      var directURL = RegExp(r'<a href=\\"(.*?)\\"')
          .firstMatch(response.body)
          .group(1)
          .replaceAll("\\", "");
      print("FIle Link :" + directURL);
      downloadVideo(directURL, video.audioName, video.ftype);
    } catch (e) {
      setState(() {
        isDownloading = false;
      });
      Toast.show(
        e.toString(),
        context,
        duration: 2,
        backgroundColor: Colors.red[300],
        textColor: Colors.black,
        gravity: Toast.BOTTOM,
      );
    }
  }

  Future<void> downloadVideo(
      String trackURL, String trackName, String format) async {
    if (!_allowWriteFile) {
      return null;
    }
    try {
      Dio dio = Dio();

      Response response = await dio.get(
        trackURL,
        onReceiveProgress: (rec, total) {
          setState(() {
            progress = ((rec / total) * 100).toStringAsFixed(0) + "%";
          });
        },
        options: Options(
          responseType: ResponseType.bytes,
          followRedirects: false,
        ),
      );
      print(response.headers);
      //getExternalStorageDirectory getApplicationDocumentsDirectory
      var directory = await getExternalStorageDirectory();
      var testdir = await Directory(
              '${directory.path}/io.github.rifkyfu32.konversi_youtube_mp3')
          .create(recursive: true);
      File file = File("${testdir.path}/" + trackName + format);
      var raf = file.openSync(mode: FileMode.write);
      raf.writeFromSync(response.data);
      await raf.close();
      setState(() {
        isDownloading = false;
        status = "Selesai ^_^";
        downloadsuccess = true;
        lokasi = "${testdir.path}/" + trackName + format;
      });
      print("${testdir.path}/" + trackName + format);
    } catch (e) {
      setState(() {
        isDownloading = false;
      });
      Toast.show(
        e.toString(),
        context,
        duration: 2,
        backgroundColor: Colors.red[300],
        textColor: Colors.black,
        gravity: Toast.BOTTOM,
      );
    }
  }

  @override
  void initState() {
    super.initState();
    _requestWritePermission();
  }

  _requestWritePermission() async {
    PermissionStatus permissionStatus =
        await SimplePermissions.requestPermission(
            Permission.WriteExternalStorage);

    if (permissionStatus == PermissionStatus.authorized) {
      setState(() {
        _allowWriteFile = true;
      });
    }
  }

  void nothingHere() {
    print("Tidak masalah");
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: searchBar(),
        backgroundColor: Color.fromARGB(255, 30, 30, 30),
        centerTitle: true,
      ),
      body: bodyPart(),
    );
  }

  Widget bodyPart() {
    return Container(
      color: Color.fromARGB(255, 30, 30, 30),
      child: Center(
        child: isFetching
            ? progressScreen()
            : fetchSuccess
                ? downloadScreen()
                : Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                      Text(
                        "Konversi Youtube ke MP3",
                        style: TextStyle(color: Colors.white, fontSize: 18.0),
                      ),
                      SizedBox(
                        height: 5.0,
                      ),
                      Text(
                        "Api dari y2mate.com",
                        style: TextStyle(color: Colors.white, fontSize: 16.0),
                      ),
                      SizedBox(
                        height: 5.0,
                      ),
                      Icon(
                        FontAwesomeIcons.youtube,
                        color: Colors.redAccent,
                        size: 45.0,
                      ),
                    ],
                  ),
      ),
    );
  }

  Widget progressScreen() {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        CircularProgressIndicator(),
        Padding(
          padding: const EdgeInsets.all(9.0),
          child: Text(
            'Mengambil Data ...',
            style: TextStyle(color: Colors.white, fontSize: 18.0),
          ),
        )
      ],
    );
  }

  Widget downloadScreen() {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Container(
          margin: EdgeInsets.symmetric(horizontal: 20.0),
          height: 300.0,
          decoration: BoxDecoration(
            borderRadius: BorderRadius.all(
              Radius.circular(19.0),
            ),
          ),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.start,
            children: <Widget>[
              Expanded(
                child: Image(
                  image: NetworkImage(video.thumbnail),
                ),
              ),
              SizedBox(
                height: 10.0,
              ),
              labelTitle("Judul : ", video.audioName),
              SizedBox(
                height: 8.0,
              ),
              labelTitle("Durasi : ", video.duration),
              SizedBox(
                height: 8.0,
              ),
              FlatButton(
                onPressed: () {
                  !downloadsuccess
                      ? directURI(video.id, video.vid, video.ajax, video.ftype,
                          video.fquality)
                      : nothingHere();
                },
                child: Container(
                  height: 40.0,
                  width: 200.0,
                  decoration: BoxDecoration(
                    color: downloadsuccess == true
                        ? Colors.greenAccent
                        : Colors.redAccent,
                    borderRadius: BorderRadius.all(
                      Radius.circular(
                        50.0,
                      ),
                    ),
                  ),
                  child: Padding(
                    padding: const EdgeInsets.symmetric(
                        vertical: 4.0, horizontal: 10.0),
                    child: Row(
                      mainAxisAlignment: MainAxisAlignment.center,
                      children: <Widget>[
                        Text(
                          status,
                          style: TextStyle(
                              color: downloadsuccess == true
                                  ? Colors.black87
                                  : Colors.white70,
                              fontSize: 16.0),
                        ),
                        SizedBox(
                          width: 12.0,
                        ),
                        Icon(
                          isDownloading
                              ? FontAwesomeIcons.spinner
                              : downloadsuccess
                                  ? FontAwesomeIcons.check
                                  : FontAwesomeIcons.download,
                          color: downloadsuccess == true
                              ? Colors.black87
                              : Colors.white70,
                          size: 20.0,
                        )
                      ],
                    ),
                  ),
                ),
              ),
              Padding(
                padding: const EdgeInsets.only(top: 8.0, bottom: 10.0),
                child: Text(
                  progress,
                  style: TextStyle(color: Colors.white),
                ),
              ),
              downloadsuccess
                  ? Card(
                      elevation: 3.0,
                      child: Padding(
                        padding: const EdgeInsets.all(8.0),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.center,
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: <Widget>[
                            Text('Lokasi berkas : ',
                                style: TextStyle(color: Colors.red)),
                            Padding(padding: EdgeInsets.only(bottom: 5.0)),
                            Text(lokasi,
                                style: TextStyle(color: Colors.black87))
                          ],
                        ),
                      ),
                    )
                  : SizedBox(
                      height: 8.0,
                    )
            ],
          ),
        ),
      ],
    );
  }

  Widget labelTitle(String title, String inpute) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Flexible(
          child: Text(
            title,
            style: TextStyle(
                color: Colors.redAccent,
                fontSize: 17.0,
                fontWeight: FontWeight.bold),
          ),
        ),
        Flexible(
          child: Text(
            inpute,
            style: TextStyle(
                color: Colors.white,
                fontSize: 16.0,
                fontWeight: FontWeight.normal),
          ),
        ),
      ],
    );
  }

  Widget searchBar() {
    return Container(
      padding: EdgeInsets.symmetric(horizontal: 4.0),
      margin: EdgeInsets.symmetric(
        horizontal: 20.0,
        vertical: 8.0,
      ),
      decoration: BoxDecoration(
        color: Color.fromARGB(100, 255, 255, 255),
        borderRadius: BorderRadius.all(
          Radius.circular(10.0),
        ),
      ),
      child: Row(
        children: <Widget>[
          Flexible(
            flex: 1,
            child: TextFormField(
              controller: videoURL,
              style: TextStyle(color: Colors.white),
              decoration: InputDecoration(
                hintText: "Video URL ...",
                border: InputBorder.none,
                hintStyle: TextStyle(color: Colors.white70),
                icon: IconButton(
                  onPressed: () {
                    getInfo();
                  },
                  icon: Icon(
                    Icons.search,
                    color: Colors.white,
                  ),
                ),
              ),
              keyboardType: TextInputType.url,
              autofocus: true,
              onFieldSubmitted: (String value) {
                getInfo();
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

**# Sentuhan Terakhir**

Selanjutnya kita ubah main.dart, hapus semua kemudian ganti dengan `snippet code` berikut ini :

```bash
import 'package:flutter/material.dart';
import 'youtube_konversi.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Konversi Youtube ke MP3',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        accentColor: Colors.red[400]
      ),
      debugShowCheckedModeBanner: false,
      home: YoutubeKonversi(),
    );
  }
}
```

Selesai. sekarang jalankan aplikasi `Konverter Youtube to MP3` dengan menekan tombol F5, namun sebelumnya jangan lupa start Android Emulator atau iOS Simulator.

Hasilnya akan terlihat seperti berikut ini:

![Tampilan aplikasi konverter youtube ke Mp3 mutiplatform pertama](/img/konverter-youtube-mp3/1.png)
![Tampilan aplikasi konverter youtube ke Mp3 mutiplatform kedua](/img/konverter-youtube-mp3/2.png)
![Tampilan aplikasi konverter youtube ke Mp3 mutiplatform ketiga](/img/konverter-youtube-mp3/3.png)

Hasil aplikasi bisa didownload <a href="https://drive.google.com/file/d/1I8xSeqOuoFdzYrQHYyFdgIWZt2im_DhQ/view" target="_blank">disini</a>
