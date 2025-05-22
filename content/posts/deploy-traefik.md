---
title: "Deploy Traefik"
slug: deploy-traefik
date: 2020-07-27T23:33:49+07:00
draft: false
tags:
  - Traefik
  - Docker
  - DevOps

image: ""
description: ""
---

Jika teman-teman belum mengerti apa itu traefik, sebelumnya saya pernah menulis [Apa Itu Traefik](/posts/apa-itu-traefik/) silahkan dibaca terlebih dahulu.

Kita disini akan menggunakan [docker-compose](https://docs.docker.com/compose/) karena menjalankan `docker run` terlalu ribet dan membuat file .sh lebih ribet lagi. Pada dasarnya `docker-compose` adalah sebuah tool untuk menjalankan aplikasi docker yang menggunakan banyak container, yang dibagi-bagi menjadi/sebagai sebuah services.

Traefik adalah service pertama kita, minimal konfigurasi untuk membuat service adalah:

    nama_service:
      image: <docker_image>

Mari kita buat service traefik kita (di file docker-compose.yml):

    version: '3.6' # memberitahu docker menggunakan compose versi 3.6

    services:
      proxy: # service name traefik
        image: traefik:v1.7.16 # stable version
        command: --configFile=/traefik.toml # memberitahu untuk menggunkan config file dengan nama traefik.toml
        restart: unless-stopped
        container_name: traefik  # nama container
        # network yg kita buat:
        networks:
          - web
        # traefik entryPoints
        ports:
          - 80:80
          - 443:443
        labels:
          - traefik.enable=true
          - traefik.frontend.rule=Host:traefik.example.com #hostname untuk dashboard traefik
          - traefik.port=8080
          - traefik.docker.network=web
          - "traefik.frontend.auth.basic=fuad:$$apr1$$hLskx/4L$$rG4XxGxcSdb6CiTL/jsqAP0" #auth untuk keamanan
        # membuat volumes docker
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
          - ./traefik.toml:/traefik.toml
          - ./acme.json:/acme.json # lokasi acme
    #jangan lupa untuk membuat network external
    networks:
      web:
        external: true

Lalu kita buat file traefik.toml yang berisikan:

    defaultEntryPoints = ["https","http"]

    [entryPoints]
      [entryPoints.http]
      address = ":80"
        [entryPoints.http.redirect]
        entryPoint = "https"
      [entryPoints.https]
      address = ":443"
      [entryPoints.https.tls]

    [docker]
    endpoint = "unix:///var/run/docker.sock"
    domain = "example.com"
    watch = true
    exposedbydefault = false

    [acme]
    email = "mi.rifky.fuady@gmail.com"
    storage = "/acme.json"
    entryPoint = "https"
    OnHostRule = true
    [acme.httpChallenge]
    entryPoint = "http"

    [web]
    address = ":8080"

Kemudian kita `deploy` service tersebut dengan perintah berikut:

    docker-compose up -d

Jika `port 80 dan 443` kita sudah digunakan (biasanya oleh web server/ apache bawaan linux), kita bisa mematikan terlebih dahulu service tersebut sehingga traefik bisa berjalan di port 80 dan 443.

apabila sukses dan kita akses `traefik.example.com` maka seharusnya muncul dashboard traefik kita: ![Tampilan Deploy Traefik](/img/deploy-traefik/1.png)

**Deploy service lain**

Kita akan menggunakan example image nya dari traefik, yakni [containous/whoami](https://github.com/traefik/whoami), sebuah `web app` untuk menampilkan beberapa informasi seperti Request Header, IP dari container tsb, dll.

    whoami:
      image: containous/whoami

Kemudian kita `deploy` dengan cara seperti biasa:

    docker-compose up -d

Akan tetapi masih ada yang kurang, kita belum memberi tahu `provider` alias docker ini tentang `karakteristik` atau `rules`. Untuk memberi tahu traefik service whoami ini karakteristiknya apa, mari kita tambahkan `labels` di file docker-compose.yml kita:

    labels:
      - "traefik.frontend.rule=Host: whoami.example.com"

Label diatas intinya adalah Jika ada request ke Host: whoami.example.com, maka container `whoami` harusnya yang menghandle. Jika kita ingin mencoba `Load Balancer`nya, kita bisa membuat 3 instance untuk service ini dengan cara:

    docker-compose up -d --scale whoami=3

untuk docker-compose lengkapnya bisa seperti ini:

    version: '3.6' # memberitahu docker menggunakan compose versi 3.6

    services:
      proxy: # service name traefik
        image: traefik:v1.7.16 # stable version
        command: --configFile=/traefik.toml # memberitahu untuk menggunkan config file dengan nama traefik.toml
        restart: unless-stopped
        container_name: traefik  # nama container
        # network yg kita buat:
        networks:
          - web
        # traefik entryPoints
        ports:
          - 80:80
          - 443:443
        labels:
          - traefik.enable=true
          - traefik.frontend.rule=Host:traefik.example.com #hostname untuk dashboard traefik
          - traefik.port=8080
          - traefik.docker.network=web
          - "traefik.frontend.auth.basic=fuad:$$apr1$$hLskx/4L$$rG4XxGxcSdb6CiTL/jsqAP0" #auth untuk keamanan
        # membuat volumes docker
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
          - ./traefik.toml:/traefik.toml
          - ./acme.json:/acme.json # lokasi acme

      whoami:
        image: containous/whoami:v1.3.0
        container_name: whoami
        labels:
          - "traefik.frontend.rule=Host:whoami.dinkes.my.id"
          - "traefik.enable=true"
          - "traefik.port=80"
          - "traefik.docker.network=web"
        networks:
          - web

    #jangan lupa untuk membuat network external
    networks:
      web:
        external: true

Nantinya di dashboar traefik akan terlihat seperti ini: ![Tampilan Deploy Traefik](/img/deploy-traefik/2.png)
