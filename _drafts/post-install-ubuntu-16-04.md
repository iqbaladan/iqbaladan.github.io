---
layout: post
title: "Things to do after installing ubuntu 16.04"
permalink: post-install-ubuntu
#categories:
#tags: HTML5
#image: /assets/images/05.09.2016-1.png
---

Dulu saya menggunakan Fedora dalam jangka waktu cukup lama, mencoba hal-hal yang berkaitan dengan RPM (RedHat Package Manager). Baru baru ini saya mencoba hal baru. Saya mencoba menggunakan Ubuntu versi 16.04 LTS, sesaat setelah dirilis. Dari pengalaman saya menggunakan linux, Ubuntu tidak terlalu asing, walaupun saya sendiri belum pernah memasang Ubuntu pada komputer saya. Ubuntu sendiri merupakan turunan dari keluarga Debian. Ngomong-ngomong soal Debian, sebelum menggunakan Fedora, saya sempat lama menggunakan Debian, jadi saya pikir tidak terlalu sulit untuk mencoba Ubuntu,mengingat Ubuntu masih turunan dari Debian.

Jadi ini adalah beberapa hal yang saya lakukan setelah memasang Ubuntu 16.04 di antaranya adalah;

### 1. Update System
Walaupun melakukan fresh install, update system tetap perlu dilakukan, karena bisa jadi ada pembaharuan paket atau bug yang perlu diperbaiki setelah tanggal rilis.

Hal ini bisa dilakukan dengan:
1. Menjalankan perkakas Software Updater dari Unity Dash.
2. Centang tombol check for updates
3. Pasang (Install)

### 2. Install Media Codecs
$ sudo apt-get install ubuntu-restricted-extras

### 3. Memindahkan Launcher ke bawah
Bagi pengguna Fedora, Launcher biasanya di atas atau di bawah, ubuntu secara default posisi launcher di sebelah kiri. Tapi sekarang Launcher dapat dipindahkan ke bawah dan ke samping kiri.

#### Pindahkakan launcher ke bawah
$ gsettings set com.canonical.Unity.Launcher launcher-position Bottom

#### Pindahkan launcher ke samping kiri
$ gsettings set com.canonical.Unity.Launcher launcher-position Left

### 4. Menghilangkan Guest Session
Ubuntu memungkin siapapun dapat login ke system tanpa password. Karena alasan kemanan, kita dapat menghilangkan Gues Session.
$ sudo sh -c "echo 'allow-guest=false' >> /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf"

### 5. Memasang Flash Player
Ubuntu tidak memasang Flash player secara bawaan. Flash player diperlukan untuk menjalankan flash media dalam peramban web. Flash palyer dapat dipasang dengan menggunakan perintah berikut ini di terminal.
$ sudo apt-get install flashplugin-installer
