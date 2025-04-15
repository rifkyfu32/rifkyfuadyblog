---
title: "Optimasi SSD & Konfigurasi Web Server di Ubuntu 18.04"
slug: optimasi-ssd-ubuntu-lts
date: 2019-08-04T23:46:41+07:00
draft: false
tags:
  - Tips dan Trick
  - Info

image: ""
description: ""
---

**Catatan `pribadi` :**

- `SSD` untuk `Ubuntu 18.04.2 LTS`, full hanya satu partisi `root` /
- `HDD` untuk `menyimpan` data

# fstab

- buka `fstab`

```bash
sudo gedit /etc/fstab
```

- matikan update tanggal file `noatime,nodiratime` :

```bash
UUID=d8c6a126-8cbe-4f72-8ab2-2e9b09b28a25 / ext4 noatime,nodiratime,errors=remount-ro 0 1
```

- pindah file `log` ke `RAM` :

```bash
tmpfs /tmp tmpfs defaults,noatime,mode=1777 0 0
tmpfs /var/spool tmpfs defaults,noatime,mode=1777 0 0
tmpfs /var/log tmpfs defaults,noatime,mode=0755 0 0
```

# Scheduler I/O :

Untuk SSD direkomendasikan oleh [Wiki Ubuntu](https://wiki.ubuntu.com/Kernel/Reference/IOSchedulers) memakai I/O `deadline`.

- bikin file `60-ssd-scheduler.rules`

```bash
sudo touch /etc/udev/rules.d/60-ssd-scheduler.rules
```

- buka file `60-ssd-scheduler.rules`

```bash
sudo gedit /etc/udev/rules.d/60-ssd-scheduler.rules
```

- tambahkan

```bash
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="deadline"
```

- cek konfigurasi

```bash
for f in /sys/block/sd?/queue/scheduler; do printf "$f is "; cat $f; done
```

# Web Server dan Database

Tujuan penggunaan untuk develop aplikasi, untuk aplikasi web dalam membangun `Web Server` menggunakan `Apache`.

Karena tidak akan menyimpan aplikasi di /var/www/html tetapi di HDD menggunakan `Symbolic link`.

Log yang sudah dipindah di RAM (`fstab`) akan hilang ketika di restart akan terjadi error tidak bisa menjalankan `Apache` maupun `MySql`.

Maka dari itu memerlukan konfigurasi **ekstra**.

# Apache2

- membuat `log apache`

```bash
sudo mkdir /var/apache2/
sudo touch /var/apache2/error.log
sudo touch /var/apache2/access.log
sudo touch /var/apache2/other_vhosts_access.log
sudo chown root:adm /var/apache2
sudo chown root:adm /var/apache2/error.log
sudo chown root:adm /var/apache2/access.log
sudo chown root:adm /var/apache2/other_vhosts_access.log
sudo chmod 0750 /var/apache2
sudo chmod 0640 /var/apache2/error.log
sudo chmod 0640 /var/apache2/access.log
sudo chmod 0640 /var/apache2/other_vhosts_access.log
```

- edit envvars `APACHE_LOG_DIR`

```bash
sudo gedit /etc/apache2/envvars
```

```bash
export APACHE_LOG_DIR=/var/apache2$SUFFIX
```

- melakukan `Symbolic link`

```bash
sudo ln -s /mnt/32a34605-e617-4bf9-87bf-9d7c2a44a10f/project/web/ /var/www/
```

- konfigurasi apache2.conf edit `LogLevel` dan `AllowOverride`

```bash
sudo gedit /etc/apache2/apache2.conf
```

```bash
LogLevel error
AllowOverride All
```

- aktifkan `a2enmod`

```bash
sudo a2enmod rewrite
```

- arahkan `localhost` ke `Symbolic link` dan konfigurasi

```bash
sudo gedit /etc/apache2/sites-available/000-default.conf
```

```bash
DocumentRoot /var/www/web
LogLevel error
ErrorLog /var/www/web/error.log
CustomLog /var/www/web/access.log combined
```

- `restart` apache

```bash
sudo service apache2 restart
```

# Mrcrypt

[sumber gist](https://gist.github.com/rifkyfu32/65c45e00999548a7c37f61395c7bcbe6)

- `install ekstensi` mcrypt

```bash
sudo apt-get install php7.2-dev
sudo apt-get -y install libmcrypt-dev
sudo pecl install mcrypt-1.0.1
```

- tekan Enter untuk `autodetect`.
- tambahkan ke `cli` dan `apache2` php.ini

```bash
sudo bash -c "echo extension=/usr/lib/php/20170718/mcrypt.so > /etc/php/7.2/cli/conf.d/mcrypt.ini"
sudo bash -c "echo extension=/usr/lib/php/20170718/mcrypt.so > /etc/php/7.2/apache2/conf.d/mcrypt.ini"
```

- `cek` ekstensi terinstall

```bash
php -i | grep mcrypt
```

- restart apache

```bash
sudo service apache2 restart
```

# Mysql

- membuat `log mysql`

```bash
sudo mkdir /var/mysql/
sudo touch /var/mysql/error.log
sudo chown mysql:adm /var/mysql
sudo chown mysql:adm /var/mysql/error.log
sudo chmod 0750 /var/mysql
sudo chmod 0640 /var/mysql/error.log
```

- mengubah log file `apparmor` mysql

```bash
sudo gedit /etc/apparmor.d/usr.sbin.mysqld
```

```bash
# Allow log file access :
  /var/mysql.err rw,
  /var/mysql.log rw,
  /var/mysql/ r,
  /var/mysql/** rw,
```

- reload `apparmor`

```bash
sudo systemctl reload apparmor
```

- `mengarahkan` log dan `izin` remote koneksi

```bash
sudo gedit /etc/mysql/mysql.conf.d/mysqld.cnf
```

```bash
log_error = /var/mysql/error.log
bind-address = 0.0.0.0
```

- `restart` MySql

```bash
sudo service mysql restart
```

# Allow remote dbquery

- `membuat` user untuk `remote` db

```bash
CREATE USER 'docker'@'localhost' IDENTIFIED BY 'docker';
GRANT ALL PRIVILEGES ON *.* TO 'docker'@'localhost' WITH GRANT OPTION;
CREATE USER 'docker'@'%' IDENTIFIED BY 'docker';
GRANT ALL PRIVILEGES ON *.* TO 'docker'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
