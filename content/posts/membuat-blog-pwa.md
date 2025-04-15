---
title: "Membuat Blog menjadi PWA"
slug: membuat-blog-pwa
date: 2020-05-30T19:22:51+07:00
draft: false
tags:
  - Info
  - Tips dan Trick

image: ""
description: ""
---

Menambahkan fitur PWA ke situs atau blog pribadi anda sangatlah mudah. Blog saya menggunakan static site generator dari [Hugo](https://gohugo.io), saya pernah menulis cara [Ngeblog dari Teks Editor dan Terminal ala Programmer](/posts/hello-word/) dengan Hugo dan jika anda masih menggunakan blogger ingin bermigrasi dengan Hugo bisa membaca tulisan saya yang ini [Mudahnya Mengisi Artikel Hugo dari Blogger](/posts/hugo-import-blogger/).

**Apa itu PWA dan mengapa saya harus menambahkannya?**

Istilah Progressive Web App diperkenalkan oleh Alex Russel, salah seorang Google Chrome engineer, dan Frances Berriman, desainer yang bekerja untuk Google pada tahun 2015. Google mendefinisikan PWA sebagai berikut:

> Progressive Web Apps use modern web capabilities to deliver an app-like user experience. They evolve from pages in browser tabs to immersive, top-level apps, maintaining the web's low friction at every moment.

Tujuan utama PWA ialah untuk memungkinkan web developer mengubah web yang sudah ada agar bisa berperilaku layaknya aplikasi mobile native tanpa melakukan banyak perubahan atau menambah programmer khusus.
Tujuan ini bisa dicapai berkat kumpulan teknologi web. Ia bisa memanfaatkan kelebihan-kelebihan web dan aplikasi mobile native sekaligus.
Kumpulan teknologi ini memungkinkan aplikasi web tradisional untuk bisa diakses tanpa koneksi internet (offline), bisa dipasang di homescreen seperti aplikasi mobile native, bisa melakukan sinkronisasi data ke server, bisa mengirim push notification, dan-lain lain. Seperti ini karakteristik sebuah PWA :

- Progresif yang berarti bekerja untuk setiap pengguna. Tak peduli apapun browsernya, tidak masalah. Pasalnya, PWAs dibangun dengan peningkatan progresif sebagai konsep intinya.
- Responsif yang berarti cocok dengan setiap faktor bentuk: perangkat desktop, seluler, tablet, atau apa saja yang muncul berikutnya.
- Konektivitas independen yang berarti Disempurnakan dengan service worker agar bisa bekerja offline atau pada jaringan berkualitas-rendah.
- Seperti Aplikasi yang berarti terasa seperti sebuah aplikasi untuk pengguna dengan interaksi dan navigasi bergaya-aplikasi karena mereka dibangun di atas model shell application.
- Fresh yang berarti selalu terkini berkat proses pembaruan service worker.
- Aman yang berarti disediakan melalui HTTPS untuk mencegah snooping dan memastikan materi belum dirusak.
- Dapat ditemukan yang berarti dapat diidentifikasi sebagai "aplikasi" berkat manifes W3C dan cakupan registrasi service worker. Ini memungkinkan mesin telusur untuk menemukannya.
- Re-engageable yang berarti dengan fitur pemberitahuan seperti push notification, dapat mengajak (engaged) kembali pengguna untuk menggunakan aplikasi.
- Dapat dipasang yang berarti memungkinkan pengguna untuk "menyimpan" aplikasi yang mereka anggap paling berguna di layar beranda tanpa kerumitan application store.
- Bisa ditautkan yang berarti dapat dengan mudah dibagikan melalui URL. Pemasangannya pun mudah.

**Bagaimana cara menambahkan PWA ke Hugo?**

Fitur minimal PWA paling tidak membutuhkan Web App Manifest dan Service Worker.
`Web app manifest` adalah file JSON sederhana yang mengontrol bagaimana aplikasi ditampilkan dan dijalankan di sisi pengguna. Umumnya file ini diberi nama manifest.json. Saat aplikasi pertama kali dibuka di browser, browser akan membaca file manifest, mengunduh resource dan menampilkan konten.
`Service Worker` adalah skrip yang dijalankan oleh browser di latar belakang, yang terpisah dengan skrip lain di halaman web browser. Service worker ditulis menggunakan bahasa pemrograman JavaScript, namun dipanggil dengan cara yang berbeda dari kode JavaScript pada umumnya. Dengan menggunakan service worker, kita dapat memanfaatkan resource yang telah disimpan di dalam cache untuk menampilkan bahkan dalam mode jaringan offline.

**Aplikasi ke Home Screen**

Add to Home Screen atau yang sering juga disebut dengan `web app install prompt` dibuat untuk mempermudah pengguna untuk memasang aplikasi PWA kita di perangkat mobile atau desktop. Tidak hanya mempermudah pengguna untuk membuka kembali aplikasi kita, menambahkan ikon aplikasi ke home screen juga punya efek yang lebih besar yakni memperkuat ikatan dengan pengguna.

Agar sebuah PWA bisa dipasang ke home screen, aplikasi kita harus memenuhi beberapa kriteria berikut:

- Belum pernah terpasang pada perangkat
- Memenuhi user engagement heuristic (yakni syarat dimana pengguna harus berinteraksi dengan aplikasi yang bersangkutan sekurang-kurangnya 30 detik).
- Memiliki web app manifest yang memiliki atribut:
  - name atau short_name
  - icons dengan ukuran 192x192 atau 512x512
  - start_url
  - display harus bernilai fullscreen, standalone, atau minimal-ui.
- Harus menggunakan HTTPS (agar service worker bisa bekerja)
- Memiliki sebuah service worker dengan sebuah event handler fetch.

**Buat Ikon Aplikasi**

PWA tersedia offline dan dapat dipasang di homescreen seperti aplikasi mobile native. Ini memerlukan ikon dengan ukuran berbeda untuk situs web Anda. Anda dapat menggunakan layanan seperti [Favicomatic](https://favicomatic.com/) untuk membuat ikon aplikasi dengan proses satu klik.

**Membuat Web App Manifest**

Buat file baru bernama manifest.json di folder /static pada template Hugo yang anda gunakan dan contoh kode di bawah ini sesuaikan dengan keinginan :

```bash
{
  "name": "Rifky Fuady Blog",
  "short_name": "RF Blog",
  "icons": [{
    "src": "/img/icons/favicon-128.png",
    "sizes": "128x128",
    "type": "image/png"
  }, {
    "src": "/img/icons/apple-touch-icon-144x144.png",
    "sizes": "144x144",
    "type": "image/png"
  }, {
    "src": "/img/icons/apple-touch-icon-152x152.png",
    "sizes": "152x152",
    "type": "image/png"
  }, {
    "src": "/img/icons/icon-512.png",
    "sizes": "512x512",
    "type": "image/png"
  }],
  "start_url": "/index.html",
  "display": "standalone",
  "orientation" : "portrait",
  "background_color": "#0069c0",
  "theme_color": "#0069c0"
}
```

**Mendaftarkan Web App Manifest**

Tambahkan tautan ke manifest.json di header template, biasanya di `<root>themes/layouts/partials/head.html` tergantung template yang anda gunakan.

```bash
<link rel="manifest" href="/manifest.json">
```

**Membuat Service Worker**

Buat file javascript baru sw.js di /static seperti tadi. Contoh dari blog saya yang bisa anda sesuaikan dengan kebutuhan anda.

```bash
const CACHE_VERSION = 1;

const BASE_CACHE_FILES = [
    '/manifest.json',
    '/css/bootstrap.min.css',
    '/css/style.css',
    '/js/jquery-3.2.1.slim.min.js',
    '/js/popper.min.js',
    '/js/bootstrap.min.js',
    '/img/logo.png',
    '/img/favicon.png',
];

const OFFLINE_CACHE_FILES = [
    '/css/bootstrap.min.css',
    '/css/style.css',
    '/js/jquery-3.2.1.slim.min.js',
    '/js/popper.min.js',
    '/js/bootstrap.min.js',
    '/img/logo.png',
    '/img/favicon.png',
];

const NOT_FOUND_CACHE_FILES = [

    '/404.html',
];

const OFFLINE_PAGE = '/offline/index.html';
const NOT_FOUND_PAGE = '/404.html';

const CACHE_VERSIONS = {
    assets: 'assets-v' + CACHE_VERSION,
    content: 'content-v' + CACHE_VERSION,
    offline: 'offline-v' + CACHE_VERSION,
    notFound: '404-v' + CACHE_VERSION,
};

const MAX_TTL = {
    '/': 3600,
    html: 3600,
    json: 86400,
    js: 86400,
    css: 86400,
};

const SUPPORTED_METHODS = [
    'GET',
];

function isBlacklisted(url) {
    return (CACHE_BLACKLIST.length > 0) ? !CACHE_BLACKLIST.filter((rule) => {
        if(typeof rule === 'function') {
            return !rule(url);
        } else {
            return false;
        }
    }).length : false
}

function getFileExtension(url) {
    let extension = url.split('.').reverse()[0].split('?')[0];
    return (extension.endsWith('/')) ? '/' : extension;
}

function getTTL(url) {
    if (typeof url === 'string') {
        let extension = getFileExtension(url);
        if (typeof MAX_TTL[extension] === 'number') {
            return MAX_TTL[extension];
        } else {
            return null;
        }
    } else {
        return null;
    }
}

function installServiceWorker() {
    return Promise.all(
        [
            caches.open(CACHE_VERSIONS.assets)
                .then(
                    (cache) => {
                        return cache.addAll(BASE_CACHE_FILES);
                    }
                ),
            caches.open(CACHE_VERSIONS.offline)
                .then(
                    (cache) => {
                        return cache.addAll(OFFLINE_CACHE_FILES);
                    }
                ),
            caches.open(CACHE_VERSIONS.notFound)
                .then(
                    (cache) => {
                        return cache.addAll(NOT_FOUND_CACHE_FILES);
                    }
                )
        ]
    );
}

function cleanupLegacyCache() {

    let currentCaches = Object.keys(CACHE_VERSIONS)
        .map(
            (key) => {
                return CACHE_VERSIONS[key];
            }
        );

    return new Promise(
        (resolve, reject) => {

            caches.keys()
                .then(
                    (keys) => {
                        return legacyKeys = keys.filter(
                            (key) => {
                                return !~currentCaches.indexOf(key);
                            }
                        );
                    }
                )
                .then(
                    (legacy) => {
                        if (legacy.length) {
                            Promise.all(
                                legacy.map(
                                    (legacyKey) => {
                                        return caches.delete(legacyKey)
                                    }
                                )
                            )
                                .then(
                                    () => {
                                        resolve()
                                    }
                                )
                                .catch(
                                    (err) => {
                                        reject(err);
                                    }
                                );
                        } else {
                            resolve();
                        }
                    }
                )
                .catch(
                    () => {
                        reject();
                    }
                );

        }
    );
}


self.addEventListener(
    'install', event => {
        event.waitUntil(installServiceWorker());
    }
);

// The activate handler takes care of cleaning up old caches.
self.addEventListener(
    'activate', event => {
        event.waitUntil(
            Promise.all(
                [
                    cleanupLegacyCache(),
                ]
            )
                .catch(
                    (err) => {
                        event.skipWaiting();
                    }
                )
        );
    }
);

self.addEventListener(
    'fetch', event => {

        event.respondWith(
            caches.open(CACHE_VERSIONS.content)
                .then(
                    (cache) => {

                        return cache.match(event.request)
                            .then(
                                (response) => {

                                    if (response) {

                                        let headers = response.headers.entries();
                                        let date = null;

                                        for (let pair of headers) {
                                            if (pair[0] === 'date') {
                                                date = new Date(pair[1]);
                                            }
                                        }

                                        if (date) {
                                            let age = parseInt((new Date().getTime() - date.getTime()) / 1000);
                                            let ttl = getTTL(event.request.url);

                                            if (ttl && age > ttl) {

                                                return new Promise(
                                                    (resolve) => {

                                                        return fetch(event.request)
                                                            .then(
                                                                (updatedResponse) => {
                                                                    if (updatedResponse) {
                                                                        cache.put(event.request, updatedResponse.clone());
                                                                        resolve(updatedResponse);
                                                                    } else {
                                                                        resolve(response)
                                                                    }
                                                                }
                                                            )
                                                            .catch(
                                                                () => {
                                                                    resolve(response);
                                                                }
                                                            );

                                                    }
                                                )
                                                    .catch(
                                                        (err) => {
                                                            return response;
                                                        }
                                                    );
                                            } else {
                                                return response;
                                            }

                                        } else {
                                            return response;
                                        }

                                    } else {
                                        return null;
                                    }
                                }
                            )
                            .then(
                                (response) => {
                                    if (response) {
                                        return response;
                                    } else {
                                        return fetch(event.request)
                                            .then(
                                                (response) => {

                                                    if(response.status < 400) {
                                                        if (~SUPPORTED_METHODS.indexOf(event.request.method) && !isBlacklisted(event.request.url)) {
                                                            cache.put(event.request, response.clone());
                                                        }
                                                        return response;
                                                    }
                                                    else {
                                                        return caches.open(CACHE_VERSIONS.notFound).then((cache) => {
                                                            return cache.match(NOT_FOUND_PAGE);
                                                        })
                                                    }
                                                }
                                            )
                                            .then((response) => {
                                                if(response) {
                                                    return response;
                                                }
                                            })
                                            .catch(
                                                () => {

                                                    return caches.open(CACHE_VERSIONS.offline)
                                                        .then(
                                                            (offlineCache) => {
                                                                return offlineCache.match(OFFLINE_PAGE)
                                                            }
                                                        )

                                                }
                                            )

                                    }
                                }
                            )
                            .catch(
                                (error) => {
                                    console.error('  Error in fetch handler:', error);
                                    throw error;
                                }
                            );
                    }
                )
        );

    }
);
```

**Tambahkan Service Worker**

Untuk meload service worker, biasanya ditaruh di footer dari template yang anda gunakan. Berikut potongan kodenya :

```bash
<script>
  if('serviceWorker' in navigator) {
      navigator.serviceWorker
          .register('/sw.js', { scope: '/' })
          .then(function(registration) {
              //console.log('Service Worker Registered');
          });

      navigator.serviceWorker
          .ready
          .then(function(registration) {
              //console.log('Service Worker Ready');
          });
  }
</script>
```

**Lihat hasilnya**

Sekarang situs kita secara otomatis menjadi PWA. Sangat mudah bukan?

Untuk mengujinya, bila menggunakan browser Google Chrome, kita dapat memanfaatkan [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/) untuk memantau aktivitas aplikasi webmu. Kamu dapat menampilkan DevTools pada browser Chrome dengan menekan tombol keyboard Ctrl+Shift+i atau mengklik kanan pada layar browser dan memilih opsi Inspect pada menu popup.

![Tampilan Membuat Blog menjadi PWA pertama](/img/membuat-blog-pwa/1.png)

Pada tab Aplikasi, kita bisa melihat detail yang disediakan dalam manifes termasuk ikon yang berbeda. Kita juga akan melihat berbagai file yang kita tentukan di bagian Penyimpanan Cache.

Buka tab Audit dan lakukan audit Lighthouse dan lihat hasilnya.
![Tampilan Membuat Blog menjadi PWA kedua](/img/membuat-blog-pwa/2.png)
