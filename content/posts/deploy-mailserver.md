---
title: "Deploy Mail Server"
slug: deploy-mailserver
date: 2021-01-05T23:33:49+07:00
draft: false
tags:
  - Traefik
  - Docker
  - Mail Server

image: ""
description: ""
---

Menjelang akhir tahun saya mendapat project yang sedikit berhubungan dengan `Mail Server`, yah walupun saya tidak mendapat task membangun `Mail Server` karena bukan team email, saya jadi agak penasaran bagaimana kalau membangun `Mail Server` sendiri.

Pertama kita harus beli domain tentunya, beli saja domain my.id yang tergolong sangat murah. Saya beli di [Cloud Kilat](cloudkilat.com)

Oh iya, sebelumnya saya akan menjabarkan spec service/docker image apa saja yang akan kita gunakan, berikut daftarnya:

- [Traefik](https://doc.traefik.io/traefik/), jika belum tahu apa itu traefik bisa baca tulisan [Apa Itu Traefik](/posts/apa-itu-traefik/).
- [docker-mailserver](https://github.com/tomav/docker-mailserver), simple mail server
- [cert-renewer-traefik](https://github.com/youtous/docker-mailserver-traefik), karena saya masih menggunakan traefik v1
- [roundcubemail](https://hub.docker.com/r/roundcube/roundcubemail/) untuk email client webmailnya
- [Mail Jet](https://mailjet.com) untuk SMTP Relay

Kita akan buat direktori terlebih dahulu:

    mkdir mailserver
    cd mailserver

Lalu download tools yang dibutuhkan dan membuat file docker-compose.yml

    wget https://raw.githubusercontent.com/tomav/docker-mailserver/master/setup.sh
    wget https://raw.githubusercontent.com/tomav/docker-mailserver/master/mailserver.env
    wget -O .env https://raw.githubusercontent.com/tomav/docker-mailserver/master/compose.env

    chmod a+x ./setup.sh
    touch docker-compose.yml

Jangan lupa untuk membuat akun [Mail Jet](mailjet.com), di halaman [Setup SMTP](https://app.mailjet.com/account/setup) copy dan simpan Credentials (API and SMTP) host, username dan password, nanti akan kita gunakan pada mailserver sebagai relay SMTP.

edit file `.env`, sesuaikan dengan preferensi teman-teman:

    HOSTNAME=mail
    DOMAINNAME=belidomaintadi.my.id #domain yang tadi dibeli
    CONTAINER_NAME=mailserver

edit file `mailserver.env`, sesuaikan dengan preferensi teman-teman:

    ENABLE_SPAMASSASSIN=1
    SPAMASSASSIN_SPAM_TO_INBOX=1
    ENABLE_CLAMAV=1
    ENABLE_FAIL2BAN=1
    ENABLE_POSTGREY=1
    ENABLE_SASLAUTHD=0
    ONE_DIR=1
    DMS_DEBUG=1
    ENABLE_POP3=1
    SSL_TYPE=manual
    SSL_CERT_PATH=/var/mail-state/manual-ssl/cert
    SSL_KEY_PATH=/var/mail-state/manual-ssl/key
    RELAY_HOST=in-v3.mailjet.com # isi host dari Mail Jet
    RELAY_PORT=587 # isi port dari Mail Jet
    RELAY_USER=a65752c21111f5f7b154c44867b228f5 # isi user dari Mail Jet
    RELAY_PASSWORD=e458c30dc3ecb70d1e1c5c1bdde331cc # isi password dari Mail Jet

edit file `docker-compose.yml`, sesuaikan dengan preferensi teman-teman:

    version: '3.8'

    services:

      cert-renewer-traefik:
        container_name: cert-renewer-traefik
        image: youtous/mailserver-traefik:latest
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
          - ../traefik/acme.json:/tmp/traefik/acme.json:ro
        environment:
          - TRAEFIK_VERSION=1
          - CERTS_SOURCE=file
          - DOMAINS=mail.example.com

      mail:
        image: tvial/docker-mailserver:latest
        hostname: ${HOSTNAME}
        domainname: ${DOMAINNAME}
        container_name: ${CONTAINER_NAME}
        labels:
          - "mailserver-traefik.renew.domain=mail.example.com"
          - "traefik.frontend.rule=Host:mail.example.com"
          - "traefik.frontend.redirect.replacement=https://webmail.example.com/"
          - "traefik.frontend.redirect.regex=.*"
          - "traefik.enable=true"
          - "traefik.docker.network=web"
        ports:
          - "25:25"
          - "143:143"
          - "587:587"
          - "993:993"
        volumes:
          - maildata:/var/mail
          - mailstate:/var/mail-state
          - maillogs:/var/log/mail
          - ./config/:/tmp/docker-mailserver/${SELINUX_LABEL}
        env_file:
          - mailserver.env
        cap_add:
          - NET_ADMIN
          - SYS_PTRACE
        restart: always
        networks:
          - web

      roundcubemail:
        image: roundcube/roundcubemail:latest
        container_name: roundcubemail
        restart: unless-stopped
        volumes:
          - ./www:/var/www/html
          - ./db/sqlite:/var/roundcube/db
        labels:
          - "traefik.frontend.rule=Host:webmail.example.com"
          - "traefik.enable=true"
          - "traefik.port=80"
          - "traefik.docker.network=web"
        environment:
          - ROUNDCUBEMAIL_DB_TYPE=sqlite
          - ROUNDCUBEMAIL_SKIN=elastic
          - ROUNDCUBEMAIL_DEFAULT_HOST=tls://mail.example.com
          - ROUNDCUBEMAIL_SMTP_SERVER=tls://mail.example.com
        networks:
          - web

    volumes:
      maildata:
        driver: local
      mailstate:
        driver: local
      maillogs:
        driver: local

    networks:
      web:
        external: true

Mari kita `deploy` dan config `Mail Server`\-nya:

    docker-compose up -d
    ./setup.sh email add rifky@example.com rahasia123
    ./setup.sh alias add postmaster@example.com rifky@example.com
    ./setup.sh email add user1@example.com user123
    ./setup.sh config dkim

Sekarang setelah kunci DNS - DKIM dibuat, kita dapat mengkonfigurasi server DNS kita hanya dengan meng-`copy` isi config/opendkim/keys/example.com/mail.txt ke zona DNS example.com kita. Sekalian kita bikin subdomain untuk service mail dan webmail kita.

    cat config/opendkim/keys/example.com/mail.txt

![Tampilan Deploy Mail Server](/img/deploy-mailserver/1.png)

Kemudian jangan lupa untuk menambahkan `MX record`, `Spf MX Mail Server` kita dan juga `SPF DKIM` untuk `Mail Jet`.

![Tampilan Deploy Mail Server](/img/deploy-mailserver/2.png)

Untuk melakukan tes pengiriman email bisa menggunakan aplikasi CLI `swaks` yang ringan jika anda menggunakan sistem operasi `Linux`.

    swaks --from user1@example.com --to rifky@example.com --server mail.example.com:587 -tlso -au user1@example.com -ap user123 --header "Subject: admin from user1" --body "testing user1 sending email"

Atau kita bisa melakukan tes pengiriman GUI yang enak dipandang dengan [Roundcube](https://roundcube.net/) dengan mengakses `subdomain` [webmail.example.com](https://webmail.example.com) kita tadi.

![Tampilan Deploy Mail Server](/img/deploy-mailserver/3.png)
