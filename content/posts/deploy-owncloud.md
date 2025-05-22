---
title: "Mudah Bikin Cloud Storage (Dropbox/GDrive) Sendiri"
slug: deploy-owncloud
date: 2020-12-15T23:33:49+07:00
draft: false
tags:
  - Traefik
  - Docker
  - DevOps

image: ""
description: ""
---

Berawal dari kisah sekelas Google yang tadi malam bisa `down` gara-gara kehabisan `storage`, saya tidak bisa mengakses file di Google Drive dan akhirnya beberapa pekerjaan terhambat. 😔 🤕

![Tampilan Deploy Owncloud](/img/deploy-owncloud/1.jpg)

Belajar dari kejadian tersebut, akhirnya saya berusaha untuk mencari cara agar bisa membuat `cloud storage` sendiri, akhirnya menemukan satu perangkat lunak `CMS(Content Management System)` berbagi berkas gratis dan bebas seperti Google Drive/Dropbox bernama [Owncloud](https://owncloud.com/).

Dengan menggunakan `owncloud`, kita dapat mengatur layanan cloud storage mulai dari user, group user, limited akses, size quota user dan lain sebagainya. Owncloud bisa kita jadikan sebagai salah satu bahan testing untuk cloud computing dikarenakan owncloud termasuk salah satu kategori dari model layanan cloud computing.

**Deploy OwnCloud**

Seperti biasa, agar mudah kita akan menggunakan [docker-compose](https://docs.docker.com/compose/). Pada dasarnya `docker-compose` adalah sebuah tool untuk menjalankan aplikasi docker yang menggunakan banyak container, yang dibagi-bagi menjadi/sebagai sebuah services.

Oh iya, sebelumnya saya akan menjabarkan spec service/docker image apa saja yang akan kita gunakan, berikut daftarnya:

- [Traefik](https://doc.traefik.io/traefik/), jika belum tahu apa itu traefik bisa baca tulisan [Apa Itu Traefik](/posts/apa-itu-traefik/).
- [Owncloud](https://hub.docker.com/_/owncloud)
- [Mariadb](https://hub.docker.com/r/webhippie/mariadb/) untuk database di disk
- [Redis](https://hub.docker.com/r/webhippie/redis) untuk database memory

Petama kita akan buat direktori terlebih dahulu:

    mkdir owncloud-docker
    cd owncloud-docker

Lalu kita bikin file konfigurasi environment dan file docker-compose.yml, sesuaikan dengan preferensi teman-teman ya:

    cat << EOF > .env
    OWNCLOUD_VERSION=10.6
    OWNCLOUD_DOMAIN=localhost:8080
    ADMIN_USERNAME=admin
    ADMIN_PASSWORD=admin
    HTTP_PORT=8080
    EOF

    touch docker-compose.yml

Kemudian docker-compose.yml edit dan sesuaikan. Saya ada sample dibawah dengan integrasi traefik:

    version: '3.6'

    volumes:
      files:
        driver: local
      mysql:
        driver: local
      backup:
        driver: local
      redis:
        driver: local

    services:
      owncloud:
        image: owncloud/server:${OWNCLOUD_VERSION}
        restart: always
        ports:
          - ${HTTP_PORT}:8080
        depends_on:
          - db
          - redis
        environment:
          - OWNCLOUD_DOMAIN=${OWNCLOUD_DOMAIN}
          - OWNCLOUD_DB_TYPE=mysql
          - OWNCLOUD_DB_NAME=owncloud
          - OWNCLOUD_DB_USERNAME=owncloud
          - OWNCLOUD_DB_PASSWORD=owncloud
          - OWNCLOUD_DB_HOST=db
          - OWNCLOUD_ADMIN_USERNAME=${ADMIN_USERNAME}
          - OWNCLOUD_ADMIN_PASSWORD=${ADMIN_PASSWORD}
          - OWNCLOUD_MYSQL_UTF8MB4=true
          - OWNCLOUD_REDIS_ENABLED=true
          - OWNCLOUD_REDIS_HOST=redis
        healthcheck:
          test: ["CMD", "/usr/bin/healthcheck"]
          interval: 30s
          timeout: 10s
          retries: 5
        volumes:
          - files:/mnt/data
        networks:
          - web
          - owncloud
        labels:
          - traefik.enable=true
          - traefik.frontend.rule=Host:own.example.com
          - traefik.port=8080
          - traefik.docker.network=web

      db:
        image: webhippie/mariadb:latest
        restart: always
        environment:
          - MARIADB_ROOT_PASSWORD=owncloud
          - MARIADB_USERNAME=owncloud
          - MARIADB_PASSWORD=owncloud
          - MARIADB_DATABASE=owncloud
          - MARIADB_MAX_ALLOWED_PACKET=128M
          - MARIADB_INNODB_LOG_FILE_SIZE=64M
        healthcheck:
          test: ["CMD", "/usr/bin/healthcheck"]
          interval: 30s
          timeout: 10s
          retries: 5
        volumes:
          - mysql:/var/lib/mysql
          - backup:/var/lib/backup
        networks:
          - owncloud

      redis:
        image: webhippie/redis:latest
        restart: always
        environment:
          - REDIS_DATABASES=1
        healthcheck:
          test: ["CMD", "/usr/bin/healthcheck"]
          interval: 30s
          timeout: 10s
          retries: 5
        volumes:
          - redis:/var/lib/redis
        networks:
          - owncloud

    networks:
      web:
        external: true
      owncloud:

Mari kita `deploy` dengan cara seperti biasa:

    docker-compose up -d

Coba kita akses ke own.example.com atau dengan IP Address server:8080 maka cloud storage kita sudah jadi! ![Tampilan Deploy Owncloud](/img/deploy-owncloud/2.png)

Untuk login pertama, seperti yang didefinisikan di file .env tadi, yaitu admin admin jangan lupa untuk mengubahnya dan tambahkan user lainnya juga.

Oh iya, owncloud juga tersedia versi mobile, jika teman-teman menggunkan smarphone android ada di [Playstore](https://play.google.com/store/apps/details?id=com.owncloud.android&hl=en&gl=US).

![Tampilan Deploy Owncloud](/img/deploy-owncloud/3.jpg)

Lumayankan teman-teman? Saya bisa bebas upload file sesuka saya selama storage server belum penuh. 🥳
