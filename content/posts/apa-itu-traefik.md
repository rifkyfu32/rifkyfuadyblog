---
title: "Apa Itu Traefik"
slug: apa-itu-traefik
date: 2020-06-25T23:33:49+07:00
draft: false
tags:
  - Traefik
  - DevOps
  - Docker

image: ""
description: ""
---

![Tampilan Treafik arsitektur](/img/apa-itu-traefik/1.png)
**Apa sih traefik itu?**

> A reverse proxy / load balancer that’s easy, dynamic, automatic, fast, full-featured, open source, production proven, provides metrics, and integrates with every major cluster technology.

Kutipan diatas diambil dari websitenya traefik. Nah, bagaimana penjelasanya?

**The Edge Router**

Internet adalah tentang bagaimana komputer saling terhubung, tentang bagaimana satu komputer berkomunikasi dengan komputer lainnya. Sama seperti manusia, untuk bisa berkomunikasi dengan lancar, kita memerlukan `cara yang disepakati kedua belah pihak`, yakni bahasa yang sama-sama dimengerti.

Misalnya, orang Jawa akan nyambung bila berbicara bahasa Jawa dengan orang yang mengerti bahasa Jawa juga. Mereka secara tidak langsung sama-sama sepakat untuk berbicara menggunakan bahasa Jawa.

Di Internet, protokol yang biasa digunakan adalah TCP/IP, spesifiknya adalah HTTP untuk komunikasi antara komputer satu (client) dengan komputer lainnya (server). Singkatnya, client (browser) mengetikkan sebuah “identifier” yang biasa disebut domain address di address bar browser, lalu browser mencari alamat IP dari domain tersebut ke DNS, baru request akan diteruskan ke alamat IP yang dituju.

Tugas edge router adalah meneruskan request tersebut. Tentang siapa yang bertanggung jawab untuk request ini? Dan dalam konteks disini, Traefik adalah Edge router kita.

**The (auto) service discovery**

Jika kita berbicara tentang `tradisional` web app (monolith), ketika kita akses path /admin dari suatu domain, pasti si `app` mencoba bertanya ke “application router” tentang siapa yang bertanggung jawab untuk path tersebut?

Berbeda dengan `microservices`. Mungkin bisa saja path tersebut mengarah ke container lain, mesin lain, server lain. Alias, service lain.

Jika kita ambil contoh dengan yang `monolith` tadi, pada dasarnya routing sudah berada di level aplikasi, yang maksudnya, konteksnya berada di sekeliling aplikasi tersebut saja. Berbeda dengan `microservices` yang memang routing-nya bukan berada di level aplikasi, melainkan di `edge router`.

Untuk bisa tahu /admin ini di handle oleh container misal dengan id `0442f45e41d3`, memangnya caranya gimana? Menggunakan cara tradisional `menembak port`? Jika port nya dinamis, apakah yakin menuju container yang kita inginkan? Apalagi yang menggunakan cluster, ke IP address mana kita harus nembaknya?

Disinilah peran `Service Discovery`, via `Service Registry`. Kita tidak akan berbicara panjang lebar tentang Service Discovery, karena Traefik menjanjikan proses discovery ini dilakukan secara `automagically`. Singkatnya, Traefik tahu itu semua berdasarkan `karakteristik` yang diberikan oleh service itu sendiri.

**Load Balancer**

Load balancing adalah tentang bagaimana cara mengatur request yang ada terhadap kumpulan server secara `efisien`. Jika kamu hanya menggunakan 1 server, pastinya load balancer ini tidak akan berguna.

Misal, kamu memiliki situs bernama [rifkyfuady.github.io](https://rifkyfuady.github.io/). Server kamu hanya kuat menghandle 1000 request per-detik atau server akan memberikan response code 503 alias down. Cara untuk menanggulanginya adalah dengan membuat `instance baru`. Artinya, bila kita membuat 3 instance, berarti sekarang [rifkyfuady.github.io](https://rifkyfuady.github.io/) bisa menghandle 3000 request per-detik.

Masalahnya, Bagaimana cara `mem-proxy` request-request tersebut ke `instance` kita yang mana berbeda-beda namun tetap 1 service? dan Bagaimana caranya agar request tersebut dihandle secara efisien dan adil? (misal instance 1 handle 1500 req/s dan instance 2 handle 1500 req/s)

Itulah tugasnya load balancer. Menjawab yang pertama, traefik akan mengaturnya secara `automagically!` Buat instance sebanyak-banyaknya, maka traefik akan `meng-load-balance` nya ke instance yang berbeda-beda. Ada 2 algoritma yang didukung traefik: WRR (Weighted Round Robin) dan DRR (Dynamic Round Robin).

Misal untuk untuk WRR, jika ada 3 instance memiliki kriteria seperti berikut:

- Instance 1, weight 8
- Instance 2, weight 6
- Instance 3, weight 4

Maka setiap 8 request akan dikirim ke instance 1, dan 6 nya akan dikirim ke instance 2, dan 4 nya akan dikirim ke instance 3. `Automagically` by traefik. Sehingga, server akan tetap _balance_ se-_balance_ yang kita maksud.

**Healthcheck**

Singkatnya, healthcheck untuk melakukan pengecekan apakah service yang dimaksud tersebut `healthy` atau `unhealthy` (down). Misal dengan cara melakukan request setiap n waktu ke endpoint yang sudah ditentukan dengan batas ambang n waktu. Misal, bila dalam 10 detik server tidak me-response, berarti kemungkinan service tersebut down.

**Circuit Breaker**

`Error` pasti akan terjadi, dan seringnya tidak `terprediksi`. Daripada pusing gambling menentukan kapan masalah itu akan datang, mendingan menyiapkan jalan keluar disaat masalah itu datang.

Jika `healthcheck` hanya tentang melakukan cek saja, `circuit breaker` adalah tentang jalan keluarnya. Sehingga, load balancer tidak meneruskan request ke container yang bermasalah/unhealthy secara berkelanjutan yang dapat menyebabkan penggunaan CPU yang meningkat dan membuat load balancing `tidak balance`.

Apabila healtcheck mungkin `threshold` nya ada di `timeout`, di circuit breaker salah satunya adalah di rasio total jumlah `error response code`.

**Automatic SSL**

Siapa yang rela membayar jika ada layanan gratis? ya betul, terima kasih [Let’s Encrypt](https://letsencrypt.org/) sekarang semua website bisa dengan mudah membuat & menggunakan sertifikat ssl dengan gratis!

Jika biasanya kita menggunakan [Certbot](https://certbot.eff.org/) untuk provisioning sertifikat ssl kita secara otomatis, dengan traefik kita bisa lebih otomatis lagi. Jadi, ketika kita men-_deploy_ service baru, `endpoint` tersebut akan langsung bisa diakses via protokol `https` tanpa harus melakukan `acme challenge` lagi secara manual.

Inilah salah satu alasan saya menggunakan traefik.

Sebenarnya masih banyak fitur-fitur lain yang ditawarkan oleh traefik (tracing, metrics, dll). Silahkan teman-teman bisa membaca di dokumentasinya langsung disitus resminya [Traefik](https://doc.traefik.io/traefik/).
