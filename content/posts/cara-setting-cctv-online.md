---
title: 'Cara Setting CCTV Online'
date: 2012-03-12T23:49:00.000+07:00
draft: false
url: /2012/03/cara-setting-cctv-online.html
tags: 
- Tips dan Trick
---

  

Di postingan ini saya akan berbagi ilmu cara setting **CCTV online**. Disini saya menggunakan Kamera dan DVR merk **Avtech**, serta modem Adsl Speedy (**TP-Link**). berikut ini cara setting agar CCTV bisa Online :

  

1\. Kita buka [www.dyndns.com](http://www.dyndns.com/)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilrc4OwmGskCpRffI17IIKsuHaUo71aHc1wak-YsJOP2DLjWf04wmxMpO_qqIrwC01s2Bl4x-KkqXDsc5M-qp7VSsZCEUZ4iASSZaVsozAfMQiv9l-ROP0YKavieBPtKW0eWj-eTofgCI/s320/logindyn.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilrc4OwmGskCpRffI17IIKsuHaUo71aHc1wak-YsJOP2DLjWf04wmxMpO_qqIrwC01s2Bl4x-KkqXDsc5M-qp7VSsZCEUZ4iASSZaVsozAfMQiv9l-ROP0YKavieBPtKW0eWj-eTofgCI/s1600/logindyn.jpg)

  

   Login, bila belum punya akun, buat akun anda dulu. disini kita akan mendaftarkan DNS yg akan dipakai buat CCTV.

  

2\. Klik ke **My servise - Host Servise - Add Hostname**.

   Buat Hostname anda, lihat gambar :

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjjajYX_VvgloI6qO7P2CEWsyfP13UpJXiZKF-50jOwwRDhfK7n5_KdhNMEL6HuAjfj2twM7sPLPiwkgagidW3450cDgtVf4f7WglV2PjtA84t30bWFxUrOk4ihumdl1U8fMuoPXDzLo7Q/s320/DNSadd.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjjajYX_VvgloI6qO7P2CEWsyfP13UpJXiZKF-50jOwwRDhfK7n5_KdhNMEL6HuAjfj2twM7sPLPiwkgagidW3450cDgtVf4f7WglV2PjtA84t30bWFxUrOk4ihumdl1U8fMuoPXDzLo7Q/s1600/DNSadd.jpg)

  

3\. Untuk mengeceknya sudah aktif apa belum, kita lakukan ping test ke hostname tersebut.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiV4hTZUOcB5s9PdcJRKrOVDwn3mj9Ui7a9E8SxvB3ONCDBrtlEHI0rVv5cc84rK6PafbMCqFE0Uh20U-laiTW61iycFa4uhHzVdY5uOn8VqcqqTZwstik2fwi5Rva-i4wJcesCy1qICTY/s320/ping.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiV4hTZUOcB5s9PdcJRKrOVDwn3mj9Ui7a9E8SxvB3ONCDBrtlEHI0rVv5cc84rK6PafbMCqFE0Uh20U-laiTW61iycFa4uhHzVdY5uOn8VqcqqTZwstik2fwi5Rva-i4wJcesCy1qICTY/s1600/ping.jpg)

  

   **Start - RUN.**

   ping home-rifky.dvrdns.org -t

   jika "**reply** from 144.79.61.122", berarti berhasil.

  

4\. Kalau sudah, kemudian kita Setting modem **Tp-Link** nya,

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgAGJWFFjAULaP_tI8ijLqHQjiHss7uGqF9BD8n3S9HYd_LLcImAjJFyJjxiFJEA7Ice1y7brQRdzxiOF2uN2aoW9IxaWcrx-C2Hf1F7ftE4nxO6CJe3xijSuAlSlk6oLeonocS9OwcRs8/s320/loginmodem.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgAGJWFFjAULaP_tI8ijLqHQjiHss7uGqF9BD8n3S9HYd_LLcImAjJFyJjxiFJEA7Ice1y7brQRdzxiOF2uN2aoW9IxaWcrx-C2Hf1F7ftE4nxO6CJe3xijSuAlSlk6oLeonocS9OwcRs8/s1600/loginmodem.jpg)

  

   Masuk ke settingan modem lewat browser dulu (defaultnya tulis di browser **192.168.1.1**, user sama passwordnya : admin).

  

5\. Masuk ke tab menu **Advanced Setup - NAT**

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhtrpXIslsfHoqf5ttKdi3TuMBjMCCloPxqQc-3jF4u6imOomiyII-FivpGzup9SBYTff7-b3lB_ngRT-J6_e1nwXuigTo833oOf8QhmwPfa98D4-3988to6dHL9umrwypNXH-EuPaICTw/s320/Nat.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhtrpXIslsfHoqf5ttKdi3TuMBjMCCloPxqQc-3jF4u6imOomiyII-FivpGzup9SBYTff7-b3lB_ngRT-J6_e1nwXuigTo833oOf8QhmwPfa98D4-3988to6dHL9umrwypNXH-EuPaICTw/s1600/Nat.jpg)

  

                Virtual Ciecuit : **PVC1**

  

6\. Setelah itu klik **DMZ**,

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEicn59ZjgAmfWkJoZIUJ0ELrza23zFYQ4qc6yLE75PhjuekU82BaosTwLyQghFjzChKm-BPeAhULvMmoJ8T7Ax7A_MaJR_sTYY2Yu9DRPUDZujArm-7N6Ap-Cv2RLh_aU6dHwTyqZx64Nw/s320/DMZ.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEicn59ZjgAmfWkJoZIUJ0ELrza23zFYQ4qc6yLE75PhjuekU82BaosTwLyQghFjzChKm-BPeAhULvMmoJ8T7Ax7A_MaJR_sTYY2Yu9DRPUDZujArm-7N6Ap-Cv2RLh_aU6dHwTyqZx64Nw/s1600/DMZ.jpg)

  

                DMZ : **Enable**

                DMZ Host IP Address : **192.168.1.10** (karena ini adalah IP default dari DVR Avtech)

  

7\. Kemudian masuk ke tab menu **Access Management - DDNS**,

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj-71F22PTmZEWvAhtCFbWqHTRCOJ7tgKnKykcPN5KMnYf9_YoLxCEvfAWYpf7s6aVjglj3LgVFPKlycAQvszKYlD3nfmLpGPduLlMhyphenhyphenE9mcjBL-yoo72YsoFOBtkLvRcLJjIvP4WDijic/s320/DDNS.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj-71F22PTmZEWvAhtCFbWqHTRCOJ7tgKnKykcPN5KMnYf9_YoLxCEvfAWYpf7s6aVjglj3LgVFPKlycAQvszKYlD3nfmLpGPduLlMhyphenhyphenE9mcjBL-yoo72YsoFOBtkLvRcLJjIvP4WDijic/s1600/DDNS.jpg)

  

                Dynamic DNS : **Actived**

                My Host name : home-rifky.dvrdns.org (nama DNS yang tadi didaftarkan di Dyndns)

                Wildcard support : **No**

  

8\. Jika sudah, kita hubungkan DVR ke Modem dengan **kabel LAN** (UTP).

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhFu6-c1FymxOQRoRu9YVnVRQ7x_CIUlcmWWwY0buCeY4lW8AH8T6eiF9BsQoaaSjlloviM3g5sIsclRzRYPry9-jJsZrfINFenh22bpnyYLfZkSbFoLQKEaxVuRVMc0tOgvyoQ1zNEJnQ/s320/cat512.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhFu6-c1FymxOQRoRu9YVnVRQ7x_CIUlcmWWwY0buCeY4lW8AH8T6eiF9BsQoaaSjlloviM3g5sIsclRzRYPry9-jJsZrfINFenh22bpnyYLfZkSbFoLQKEaxVuRVMc0tOgvyoQ1zNEJnQ/s1600/cat512.jpg)

  

  

9\. Untuk setting di DVRnya, Install Video Viewer.exe, biasanya ada di CD DVR nya. kalau belum punya, bisa donwload [disini](http://www.ziddu.com/download/18851966/Avtech.rar.html).

  

10\. Jalankan Video Viewer.exe, **Add **(tanda +). Settingan lihat digambar :

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhh6k9E43X5p69E5TBT-fOJkMuqacTiNti18WNhsPftp4aFkThnfui2flkO-BwoYwTAz4RR3vkyBenrGHkVL-CgwhIg0dNNEl8KieOg2kFkiJLWwmUAi-5bn40Ru3og54NaoREgOsHcddo/s320/runAvexe.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhh6k9E43X5p69E5TBT-fOJkMuqacTiNti18WNhsPftp4aFkThnfui2flkO-BwoYwTAz4RR3vkyBenrGHkVL-CgwhIg0dNNEl8KieOg2kFkiJLWwmUAi-5bn40Ru3og54NaoREgOsHcddo/s1600/runAvexe.jpg)

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj2PmZ48Ci64UcuJzEdeeddXDkL6gL7NnXLqhDEbkB52vM_yMTpWOoB5njyTf3mygpeUE48ZRZKhFRDtG3reJNOK5Z2JPEv5tN6E7AVTzh-nZse8Hv5Dg_l8fWXE5XXqoWGB6lQPbopaNI/s320/addIPlocal.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj2PmZ48Ci64UcuJzEdeeddXDkL6gL7NnXLqhDEbkB52vM_yMTpWOoB5njyTf3mygpeUE48ZRZKhFRDtG3reJNOK5Z2JPEv5tN6E7AVTzh-nZse8Hv5Dg_l8fWXE5XXqoWGB6lQPbopaNI/s1600/addIPlocal.jpg)

  

  

11\. Double klik IP settingan tadi untuk login.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUb3ioFujyXRQvy0MepsbVw-dip0xOdsKZ-1C-qSwfQVTR3xxNJU0Y-pVyuTkQTq7Se2V7pHXAfHwrrhTwaULVEUuCPiBK8gUPxiQRsrx7PKldSsL7zMVNS08kJtzdaAWoF4YuXFkg3XU/s320/loginAvtect.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUb3ioFujyXRQvy0MepsbVw-dip0xOdsKZ-1C-qSwfQVTR3xxNJU0Y-pVyuTkQTq7Se2V7pHXAfHwrrhTwaULVEUuCPiBK8gUPxiQRsrx7PKldSsL7zMVNS08kJtzdaAWoF4YuXFkg3XU/s1600/loginAvtect.jpg)

  

  

12\. Kemudian masuk ke menu **Miscellaneous Control - Server seetting**.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXSN0dKbKLx75elq_13iVru5T8jhyphenhyphenoPn8PPcD1CIzvi5jWGwcxVAqV9i3oUb9gxkaufuiwa79H7Mw_j-6TsnLuPPo-cWshf_X-xpntPWiLTQDnXEy7LZnHckYeb52lRrX6WwZXpZUUG-8/s320/milleciound.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXSN0dKbKLx75elq_13iVru5T8jhyphenhyphenoPn8PPcD1CIzvi5jWGwcxVAqV9i3oUb9gxkaufuiwa79H7Mw_j-6TsnLuPPo-cWshf_X-xpntPWiLTQDnXEy7LZnHckYeb52lRrX6WwZXpZUUG-8/s1600/milleciound.jpg)

  

  

13\. Klik **Network**. Setting sperti gambar dibawah.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiBP24yQ_UU4OuCoixHIDzZlBrHaPQFz1kompV67B9F-MufGThcrPlBBggCaDRJ3eE7YEXk0B7_wMxSPao8SwW0wSANVOvBU-rRMZP_wY11SKDCt9FCIeB5z1Ojk1ZB31x2kFl_AMuhAlY/s320/network.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiBP24yQ_UU4OuCoixHIDzZlBrHaPQFz1kompV67B9F-MufGThcrPlBBggCaDRJ3eE7YEXk0B7_wMxSPao8SwW0wSANVOvBU-rRMZP_wY11SKDCt9FCIeB5z1Ojk1ZB31x2kFl_AMuhAlY/s1600/network.jpg)

  

                Web Port : 81, karena biar bisa diakses lewat Handphone.

  

14\. Masuk ke **DDNS**. Setting seperti gambar dibawah.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiFa-DWR1ilr-xU9qXzlgnGr5-D3eUkDmoB2MJ7-Ld9SSwcOA_ksXJPQP7_vUnqfJvkszOmrYLTOQumbDiisX-QnFqzefpaGqOgkHIrKA6GnEJn_ZAsSBpYdNCUQJyhvzQEoarOtKlxZhM/s320/ddnsvv.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiFa-DWR1ilr-xU9qXzlgnGr5-D3eUkDmoB2MJ7-Ld9SSwcOA_ksXJPQP7_vUnqfJvkszOmrYLTOQumbDiisX-QnFqzefpaGqOgkHIrKA6GnEJn_ZAsSBpYdNCUQJyhvzQEoarOtKlxZhM/s1600/ddnsvv.jpg)

  

                DNS 1 dan DNS 2 adalah IP dari www.dyndns.com (lakukan ping test kalau tidak percaya)

  

15\. Klik **Apply - OK**.

  

16\. seperti langkah no. 10, coba IP Addres di ganti : “home-rifky.dvrdns.org” dan Login. berhasil berarti selesai.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgpUvo99aF9obTqnU84_2vnXMdAcwiqO0b5w0_jaTvY0RHKlAsl2eM1m21VAT3nkKuL6GZvQtTNgE8FEZLCFKsyrL0A4fo4pSS33F9yV7rS9QhN1o3BBk3wcsBbsXboyvtitWtemrkp-iE/s320/videoviewer_0130_full_screen_dashboard.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgpUvo99aF9obTqnU84_2vnXMdAcwiqO0b5w0_jaTvY0RHKlAsl2eM1m21VAT3nkKuL6GZvQtTNgE8FEZLCFKsyrL0A4fo4pSS33F9yV7rS9QhN1o3BBk3wcsBbsXboyvtitWtemrkp-iE/s1600/videoviewer_0130_full_screen_dashboard.jpg)

  

  

  

Sekian dulu tutorial dari saya, semoga bermanfaat untuk anda.

  

Catatan : sekarang akun Dyndns sudah tidak free lagi, kalau ingin yang free bisa memakai akun [no-ip](http://www.no-ip.com/), tapi harus memakai modem yang support [no-ip](http://www.no-ip.com/), contoh : Modem **D-Link.**