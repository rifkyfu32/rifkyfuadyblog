---
title: "Tutorial Membuat Aplikasi Pemutar Musik Android dan IOS dengan Flutter"
slug: pemutar-musik-flutter
date: 2019-03-16T01:48:31+07:00
draft: false
tags:
  - Flutter
  - Bahasa Pemrograman

image: ""
description: ""
---

Nada-nada yang diatur indah dalam sebuah musik memiliki efek yang besar bagi kita. Harmoni suara ini bisa menjadi media penyembuhan, mengusir kecemasan, menenangkan, hingga mendongkrak semangat.

> ## **Ngoding** tanpa dengerin **musik**, seperti makan sayur kurang _`micin`_ _(hambar)_... :sweat_smile:

Bagi saya medengarkan musik tak hanya bisa menghibur, saat malam hari sunyi sepi **ngoding** `sendiri` _(jodoh undefined )_ :joy: kode program bermasalah gak ketemu-ketemu solusinya, dengan mendengarkan musik yang saya sukai terkadang bisa mendatangkan inspirasi ide solusi dari masalah tersebut. _(Hilihhh... malah curcol)_.

**Gimana kalo kita bikin aplikasi pemutar musik sederhana?**

_Programmer suka dengerin musik, masa iya gak bisa bikin aplikasi pemutar musik sederhana... Hehe_

Okay, langsung saja ya kita bikin, seperti biasa agar bisa berjalan di `Android` maupun `IOS` kita pake `Flutter` ya.

Bikin aplikasi zaman sekarang mudah, tinggal gabung-gabungin aja library/plugin yang sudah dibuat oleh programmer lain, kali ini kita akan menggunakan bantuan dari plugin [fluttery](https://pub.dartlang.org/packages/fluttery) agar mempermudah membuat tampilan dan plugin [fluttery_audio](https://pub.dartlang.org/packages/fluttery_audio) untuk memutar suara.

## Membuat Projek

Langkah pertama, jalankan editor VS Code, selanjutnya buat projek baru dengan menekan kombinasi tombol `CTRL+SHIFT+P` dan tulis nama projeknya misalnya `pemutar_musik`. Untuk nama aplikasi harus huruf kecil semua dan tidak boleh mengandung spasi.

![Tampilan Aplikasi Pemutar Musik pertama](/img/pemutar-musik-flutter/1.png)

Kemudian edit file `pubspec.yaml`, tambahkan plugin yang kita butuhkan tadi. Berikut ini `snippet code`-nya :

```bash
name: pemutar_musik
description: A new Flutter project.

version: 1.0.0+1

environment:
  sdk: ">=2.1.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^0.1.2

  fluttery: 0.0.8
  fluttery_audio: 0.0.4

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true
```

## Konfigurasi Tema

Buat file baru dengan klik kanan pada folder lib selanjutnya beri nama `theme.dart`. Disini kita hanya akan mendeklarasikan warna yang akan kita gunakan. Berikut ini `snippet code`-nya :

```bash
import 'package:flutter/material.dart';

const Color accentColor = const Color(0xFF00897b);
const Color lightAccentColor = const Color(0xFF4ebaaa);
const Color darkAccentColor = const Color(0xFF005b4f);
```

## Dummy Data

Selanjutnya buat file baru dengan nama `song.dart`, kita akan mengambil contoh data suara dari [SoundCloud](https://soundcloud.com) berikut ini `snippet code`-nya :

```bash
import 'package:meta/meta.dart';

final demoPlaylist = new DemoPlaylist(
  songs: [
    new DemoSong(
      audioUrl: 'https://api.soundcloud.com/tracks/151906119/stream?secret_token=s-tj3IS&client_id=LBCcHmRB8XSStWL6wKH2HPACspQlXg2P',
      albumArtUrl: 'https://rifkyfu32.github.io/img/profil-300.jpg',
      songTitle: 'Nocturne Op.9 - No.2',
      artist: 'Chopin',
    ),
    new DemoSong(
      audioUrl: 'https://api.soundcloud.com/tracks/52910579/stream?secret_token=s-tj3IS&client_id=LBCcHmRB8XSStWL6wKH2HPACspQlXg2P',
      albumArtUrl: 'https://i1.sndcdn.com/avatars-000018621313-4f0n4a-t200x200.jpg',
      songTitle: 'Romantic Saxophone',
      artist: 'Kenny G',
    ),
    new DemoSong(
      audioUrl: 'https://api.soundcloud.com/tracks/142334780/stream?secret_token=s-tj3IS&client_id=LBCcHmRB8XSStWL6wKH2HPACspQlXg2P',
      albumArtUrl: 'https://i1.sndcdn.com/artworks-000075361684-gzr4u4-t200x200.jpg',
      songTitle: 'Hey Jude',
      artist: 'The Beatles',
    ),
    new DemoSong(
      audioUrl: 'https://api.soundcloud.com/tracks/92389400/stream?secret_token=s-tj3IS&client_id=LBCcHmRB8XSStWL6wKH2HPACspQlXg2P',
      albumArtUrl: 'https://i1.sndcdn.com/artworks-000145200947-x75uby-t200x200.jpg',
      songTitle: 'The Sound of Silence',
      artist: 'Kenny G',
    ),
    new DemoSong(
      audioUrl: 'https://api.soundcloud.com/tracks/81788555/stream?secret_token=s-tj3IS&client_id=LBCcHmRB8XSStWL6wKH2HPACspQlXg2P',
      albumArtUrl: 'https://i1.sndcdn.com/artworks-000075361684-gzr4u4-t200x200.jpg',
      songTitle: 'You Are Not Alone',
      artist: 'Michael Jackson',
    ),

  ],
);

class DemoPlaylist {

  final List<DemoSong> songs;

  DemoPlaylist({
    @required this.songs,
  });

}

class DemoSong {

  final String audioUrl;
  final String albumArtUrl;
  final String songTitle;
  final String artist;

  DemoSong({
    @required this.audioUrl,
    @required this.albumArtUrl,
    @required this.songTitle,
    @required this.artist,
  });

}
```

## Tampilan Kontrol Musik

Kemudian buat file baru lagi untuk membuat tampilan kontrol musik, beri nama `bottom_controls.dart`, berikut ini `snippet code`-nya :

```bash
import 'dart:math';

import 'package:flutter/material.dart';
import 'package:fluttery_audio/fluttery_audio.dart';
import 'songs.dart';
import 'theme.dart';

class BottomControls extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      width: double.infinity,
      child: Material(
        shadowColor: const Color(0x44000000),
        color: accentColor,
        child: Padding(
          padding: const EdgeInsets.only(top: 40.0, bottom: 50.0),
          child: Column(
            children: <Widget>[
             AudioPlaylistComponent(
                playlistBuilder: (BuildContext context, Playlist playlist, Widget child) {
                  final songTitle = demoPlaylist.songs[playlist.activeIndex].songTitle;
                  final artistName = demoPlaylist.songs[playlist.activeIndex].artist;

                  return RichText(
                      text: TextSpan(
                          text: '',
                          children: [
                           TextSpan(
                              text: '${songTitle.toUpperCase()}\n',
                              style: TextStyle(
                                color: Colors.white,
                                fontSize: 14.0,
                                fontWeight: FontWeight.bold,
                                letterSpacing: 4.0,
                                height: 1.5,
                              ),
                            ),
                           TextSpan(
                              text: '${artistName.toUpperCase()}',
                              style: TextStyle(
                                color: Colors.white.withOpacity(0.75),
                                fontSize: 12.0,
                                letterSpacing: 3.0,
                                height: 1.5,
                              ),
                            ),
                          ]
                      ),
                    textAlign: TextAlign.center,
                  );
                },
              ),
             Padding(
                padding: const EdgeInsets.only(top: 40.0),
                child: Row(
                  children: <Widget>[
                   Expanded(child: Container()),

                   PreviousButton(),

                   Expanded(child: Container()),

                   PlayPauseButton(),

                   Expanded(child: Container()),

                   NextButton(),

                   Expanded(child: Container()),
                  ],
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}

class PlayPauseButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return AudioComponent(
      updateMe: [
        WatchableAudioProperties.audioPlayerState,
      ],
      playerBuilder: (BuildContext context, AudioPlayer player, Widget child) {
        IconData icon = Icons.music_note;
        Color buttonColor = lightAccentColor;
        Function onPressed;

        if (player.state == AudioPlayerState.playing) {
          icon = Icons.pause;
          onPressed = player.pause;
          buttonColor = Colors.white;
        } else if (player.state == AudioPlayerState.paused
          || player.state == AudioPlayerState.completed) {
          icon = Icons.play_arrow;
          onPressed = player.play;
          buttonColor = Colors.white;
        }

        return RawMaterialButton(
          shape: CircleBorder(),
          fillColor: buttonColor,
          splashColor: lightAccentColor,
          highlightColor: lightAccentColor.withOpacity(0.5),
          elevation: 10.0,
          highlightElevation: 5.0,
          onPressed: onPressed,
          child: Padding(
            padding: const EdgeInsets.all(8.0),
            child: Icon(
              icon,
              color: darkAccentColor,
              size: 35.0,
            ),
          ),
        );
      },
    );
  }
}

class PreviousButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return AudioPlaylistComponent(
      playlistBuilder: (BuildContext context, Playlist playlist, Widget child) {
        return IconButton(
          splashColor: lightAccentColor,
          highlightColor: Colors.transparent,
          icon: Icon(
            Icons.skip_previous,
            color: Colors.white,
            size: 35.0,
          ),
          onPressed: playlist.previous,
        );
      },
    );
  }
}

class NextButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return AudioPlaylistComponent(
      playlistBuilder: (BuildContext context, Playlist playlist, Widget child) {
        return IconButton(
          splashColor: lightAccentColor,
          highlightColor: Colors.transparent,
          icon: Icon(
            Icons.skip_next,
            color: Colors.white,
            size: 35.0,
          ),
          onPressed: playlist.next,
        );
      },
    );
  }
}

class CircleClipper extends CustomClipper<Rect> {
  @override
  Rect getClip(Size size) {
    return Rect.fromCircle(
      center: Offset(size.width / 2, size.height / 2),
      radius: min(size.width, size.height) / 2,
    );
  }

  @override
  bool shouldReclip(CustomClipper<Rect> oldClipper) {
    return true;
  }

}
```

## Modifikasi main.dart

Berikutnya kita ubah main.dart, hapus semua kemudian ganti dengan `snippet code` berikut ini :

```bash
import 'dart:math';
import 'package:flutter/material.dart';
import 'package:meta/meta.dart';
import 'bottom_controls.dart';
import 'songs.dart';
import 'theme.dart';
import 'package:fluttery/gestures.dart';
import 'package:fluttery_audio/fluttery_audio.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Pemutar Musik',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

  @override
  Widget build(BuildContext context) {
    return AudioPlaylist(
      playlist: demoPlaylist.songs.map((DemoSong song) {
        return song.audioUrl;
      }).toList(growable: false),
      playbackState: PlaybackState.paused,
      child: Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.transparent,
          elevation: 0.0,
          leading: IconButton(
            icon: Icon(
              Icons.arrow_back_ios,
            ),
            color: const Color(0xFFDDDDDD),
            onPressed: () {},
          ),
          title: Text(''),
          actions: <Widget>[
            IconButton(
              icon: Icon(
                Icons.menu,
              ),
              color: const Color(0xFFDDDDDD),
              onPressed: () {},
            ),
          ],
        ),
        body: Column(
          children: <Widget>[
            Expanded(
              child: AudioPlaylistComponent(
                playlistBuilder: (BuildContext context, Playlist playlist, Widget child) {
                  String albumArtUrl = demoPlaylist.songs[playlist.activeIndex].albumArtUrl;

                  return AudioRadialSeekBar(
                    albumArtUrl: albumArtUrl,
                  );
                },
              ),
            ),

            Container(
              width: double.infinity,
              height: 125.0,
              child: Visualizer(
                builder: (BuildContext context, List<int> fft) {
                  return CustomPaint(
                    painter: VisualizerPainter(
                      fft: fft,
                      height: 125.0,
                      color: accentColor,
                    ),
                    child: Container(),
                  );
                },
              ),
            ),

            BottomControls()
          ],
        ),
      ),
    );
  }
}

class VisualizerPainter extends CustomPainter {

  final List<int> fft;
  final double height;
  final Color color;
  final Paint wavePaint;

  VisualizerPainter({
    this.fft,
    this.height,
    this.color,
  }) : wavePaint = Paint()
        ..color = color.withOpacity(0.75)
        ..style = PaintingStyle.fill;

  @override
  void paint(Canvas canvas, Size size) {
    _renderWaves(canvas, size);
  }

  void _renderWaves(Canvas canvas, Size size) {
    final histogramLow = _createHistogram(fft, 15, 2, ((fft.length) / 4).floor());
    final histogramHigh = _createHistogram(fft, 15, (fft.length / 4).ceil(), (fft.length / 2).floor());

    _renderHistogram(canvas, size, histogramLow);
    _renderHistogram(canvas, size, histogramHigh);
  }

  void _renderHistogram(Canvas canvas, Size size, List<int> histogram) {
    if (histogram.length == 0) {
      return;
    }

    final pointsToGraph = histogram.length;
    final widthPerSample = (size.width / (pointsToGraph - 2)).floor();

    final points = List<double>.filled(pointsToGraph * 4, 0.0);

    for (int i = 0; i < histogram.length - 1; ++i) {
      points[i * 4] = (i * widthPerSample).toDouble();
      points[i * 4 + 1] = size.height - histogram[i].toDouble();

      points[i * 4 + 2] = ((i + 1) * widthPerSample).toDouble();
      points[i * 4 + 3] = size.height - (histogram[i + 1].toDouble());
    }

    Path path = Path();
    path.moveTo(0.0, size.height);
    path.lineTo(points[0], points[1]);
    for (int i = 2; i < points.length - 4; i += 2) {
      path.cubicTo(
        points[i - 2] + 10.0, points[i - 1],
        points[i] - 10.0, points [i + 1],
        points[i], points[i + 1]
      );
    }
    path.lineTo(size.width, size.height);
    path.close();

    canvas.drawPath(path, wavePaint);
  }

  List<int> _createHistogram(List<int> samples, int bucketCount, [int start, int end]) {
    if (start == end) {
      return const [];
    }

    start = start ?? 0;
    end = end ?? samples.length - 1;
    final sampleCount = end - start + 1;

    final samplesPerBucket = (sampleCount / bucketCount).floor();
    if (samplesPerBucket == 0) {
      return const [];
    }

    final actualSampleCount = sampleCount - (sampleCount % samplesPerBucket);
    List<int> histogram = List<int>.filled(bucketCount, 0);

    for (int i = start; i <= start + actualSampleCount; ++i) {
      if ((i - start) % 2 == 1) {
        continue;
      }

      int bucketIndex = ((i - start) / samplesPerBucket).floor();
      histogram[bucketIndex] += samples[i];
    }

    for (var i = 0; i < histogram.length; ++i) {
      histogram[i] = (histogram[i] / samplesPerBucket).abs().round();
    }

    return histogram;
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }

}

class AudioRadialSeekBar extends StatefulWidget {

  final String albumArtUrl;

  AudioRadialSeekBar({
    this.albumArtUrl,
  });

  @override
  AudioRadialSeekBarState createState() {
    return AudioRadialSeekBarState();
  }
}

class AudioRadialSeekBarState extends State<AudioRadialSeekBar> {

  double _seekPercent;

  @override
  Widget build(BuildContext context) {
    return AudioComponent(
      updateMe: [
        WatchableAudioProperties.audioPlayhead,
        WatchableAudioProperties.audioSeeking,
      ],
      playerBuilder: (BuildContext context, AudioPlayer player, Widget child) {
        double playbackProgress = 0.0;
        if (player.audioLength != null && player.position != null) {
          playbackProgress = player.position.inMilliseconds / player.audioLength.inMilliseconds;
        }

        _seekPercent = player.isSeeking ? _seekPercent : null;

        return RadialSeekBar(
          progress: playbackProgress,
          seekPercent: _seekPercent,
          onSeekRequested: (double seekPercent) {
            setState(() => _seekPercent = seekPercent);

            final seekMillis = (player.audioLength.inMilliseconds * seekPercent).round();
            player.seek(Duration(milliseconds: seekMillis));
          },
          child: Container(
            color: accentColor,
            child: Image.network(
              widget.albumArtUrl,
              fit: BoxFit.cover,
            ),
          ),
        );
      },
    );
  }
}

class RadialSeekBar extends StatefulWidget {

  final double progress;
  final double seekPercent;
  final Function(double) onSeekRequested;
  final Widget child;

  RadialSeekBar({
    this.progress = 0.0,
    this.seekPercent = 0.0,
    this.onSeekRequested,
    this.child,
  });

  @override
  RadialSeekBarState createState() {
    return RadialSeekBarState();
  }
}

class RadialSeekBarState extends State<RadialSeekBar> {

  double _progress = 0.0;
  PolarCoord _startDragCoord;
  double _startDragPercent;
  double _currentDragPercent;


  @override
  void initState() {
    super.initState();
    _progress = widget.progress;
  }

  @override
  void didUpdateWidget(RadialSeekBar oldWidget) {
    super.didUpdateWidget(oldWidget);
    _progress = widget.progress;
  }

  void _onDragStart(PolarCoord coord) {
    _startDragCoord = coord;
    _startDragPercent = _progress;
  }

  void _onDragUpdate(PolarCoord coord) {
    final dragAngle = coord.angle - _startDragCoord.angle;
    final dragPercent = dragAngle / (2 * pi);

    setState(() => _currentDragPercent = (_startDragPercent + dragPercent) % 1.0);
  }

  void _onDragEnd() {
    if (widget.onSeekRequested != null) {
      widget.onSeekRequested(_currentDragPercent);
    }

    setState(() {
      _currentDragPercent = null;
      _startDragCoord = null;
      _startDragPercent = 0.0;
    });
  }

  @override
  Widget build(BuildContext context) {
    double thumbPosition = _progress;
    if (_currentDragPercent != null) {
      thumbPosition = _currentDragPercent;
    } else if (widget.seekPercent != null) {
      thumbPosition = widget.seekPercent;
    }

    return RadialDragGestureDetector(
      onRadialDragStart: _onDragStart,
      onRadialDragUpdate: _onDragUpdate,
      onRadialDragEnd: _onDragEnd,
      child: Container(
        width: double.infinity,
        height: double.infinity,
        color: Colors.transparent,
        child: Center(
          child: Container(
            width: 140.0,
            height: 140.0,
            child: RadialProgressBar(
              trackColor: const Color(0xFFDDDDDD),
              progressPercent: _progress,
              progressColor: accentColor,
              thumbPosition: thumbPosition,
              thumbColor: lightAccentColor,
              innerPadding: const EdgeInsets.all(10.0),
              child: ClipOval(
                clipper: CircleClipper(),
                child: widget.child,
              ),
            ),
          )
        ),
      ),
    );
  }
}

class RadialProgressBar extends StatefulWidget {

  final double trackWidth;
  final Color trackColor;
  final double progressWidth;
  final Color progressColor;
  final double progressPercent;
  final double thumbSize;
  final Color thumbColor;
  final double thumbPosition;
  final EdgeInsets outerPadding;
  final EdgeInsets innerPadding;
  final Widget child;

  RadialProgressBar({
    this.trackWidth = 3.0,
    this.trackColor = Colors.grey,
    this.progressWidth = 5.0,
    this.progressColor = Colors.black,
    this.progressPercent = 0.0,
    this.thumbSize = 10.0,
    this.thumbColor = Colors.black,
    this.thumbPosition = 0.0,
    this.outerPadding = const EdgeInsets.all(0.0),
    this.innerPadding = const EdgeInsets.all(0.0),
    this.child,
  });

  @override
  _RadialProgressBarState createState() => _RadialProgressBarState();
}

class _RadialProgressBarState extends State<RadialProgressBar> {

  EdgeInsets _insetsForPainter() {
    final outerThickness = max(
      widget.trackWidth,
      max(
        widget.progressWidth,
        widget.thumbSize,
      ),
    ) / 2.0;
    return EdgeInsets.all(outerThickness);
  }

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: widget.outerPadding,
      child: CustomPaint(
        foregroundPainter: RadialSeekBarPainter(
          trackWidth: widget.trackWidth,
          trackColor: widget.trackColor,
          progressWidth: widget.progressWidth,
          progressColor: widget.progressColor,
          progressPercent: widget.progressPercent,
          thumbSize: widget.thumbSize,
          thumbColor: widget.thumbColor,
          thumbPosition: widget.thumbPosition,
        ),
        child: Padding(
          padding: _insetsForPainter() + widget.innerPadding,
          child: widget.child,
        ),
      ),
    );
  }
}

class RadialSeekBarPainter extends CustomPainter {

  final double trackWidth;
  final Paint trackPaint;
  final double progressWidth;
  final Paint progressPaint;
  final double progressPercent;
  final double thumbSize;
  final Paint thumbPaint;
  final double thumbPosition;

  RadialSeekBarPainter({
    @required this.trackWidth,
    @required trackColor,
    @required this.progressWidth,
    @required progressColor,
    @required this.progressPercent,
    @required this.thumbSize,
    @required thumbColor,
    @required this.thumbPosition,
  }) : trackPaint = Paint()
        ..color = trackColor
        ..style = PaintingStyle.stroke
        ..strokeWidth = trackWidth,
       progressPaint = Paint()
        ..color = progressColor
        ..style = PaintingStyle.stroke
        ..strokeWidth = progressWidth
        ..strokeCap = StrokeCap.round,
       thumbPaint = Paint()
        ..color = thumbColor
        ..style = PaintingStyle.fill;

  @override
  void paint(Canvas canvas, Size size) {
    final outerThickness = max(trackWidth, max(progressWidth, thumbSize));
    Size constrainedSize = Size(
      size.width - outerThickness,
      size.height - outerThickness,
    );

    final center = Offset(size.width / 2, size.height / 2);
    final radius = min(constrainedSize.width, constrainedSize.height) / 2;

    canvas.drawCircle(
      center,
      radius,
      trackPaint,
    );

    final progressAngle = 2 * pi * progressPercent;
    canvas.drawArc(
      Rect.fromCircle(
        center: center,
        radius: radius,
      ),
      -pi / 2,
      progressAngle,
      false,
      progressPaint,
    );

    final thumbAngle = 2 * pi * thumbPosition - (pi / 2);
    final thumbX = cos(thumbAngle) * radius;
    final thumbY = sin(thumbAngle) * radius;
    final thumbCenter = Offset(thumbX, thumbY) + center;
    final thumbRadius = thumbSize / 2.0;
    canvas.drawCircle(
      thumbCenter,
      thumbRadius,
      thumbPaint,
    );
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }

}
```

## Setting Permission

Langkah terakhir kita menambahkan permission, edit file `android/app/src/main/AndroidManifiest.xml`, tambahkan dengan `snippet code` berikut ini :

```bash
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS"/>
```

![Tampilan Aplikasi Pemutar Musik kedua](/img/pemutar-musik-flutter/2.png)

Agar lebih jelas bisa melihat gambar diatas.

## Jalankan Aplikasi

Setelah selesai semua, sekarang saatnya menjalankan aplikasi `Pemutar Musik` dengan menekan tombol F5, namun sebelumnya jangan lupa start Android Emulator atau iOS Simulator.

![Tampilan Aplikasi Pemutar Musik ketiga](/img/pemutar-musik-flutter/3.png)

Hasilnya akan terlihat seperti berikut ini:

![Tampilan Aplikasi Pemutar Musik keempat](/img/pemutar-musik-flutter/4.png)
