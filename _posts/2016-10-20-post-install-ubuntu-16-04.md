---
layout: post
title: "14 Hal yang Saya Lakukan Setelah Install Ubuntu 16.04 LTS"
permalink: post-install-ubuntu-lts
#categories:
#tags: HTML5
image: /assets/images/ubuntu_wallpaper.png
---

Dulu saya menggunakan Fedora dalam jangka waktu cukup lama, mencoba hal-hal yang berkaitan dengan RPM (*RedHat Package Manager*). Baru baru ini saya mencoba hal baru. Saya mencoba menggunakan Ubuntu versi 16.04 LTS, sesaat setelah dirilis. Dari pengalaman saya menggunakan linux, Ubuntu tidak terlalu asing, walaupun saya sendiri belum pernah memasang Ubuntu pada komputer saya. Ubuntu sendiri merupakan turunan dari keluarga Debian. Ngomong-ngomong soal Debian, sebelum menggunakan Fedora, saya sempat lama menggunakan Debian, jadi saya pikir tidak terlalu sulit untuk mencoba Ubuntu,mengingat Ubuntu masih turunan dari Debian.

Jadi ini adalah 13 hal yang saya lakukan setelah memasang Ubuntu 16.04, di antaranya adalah;

### 1. Update System
Walaupun melakukan fresh install, update system tetap perlu dilakukan, karena bisa jadi ada pembaharuan paket atau bug yang perlu diperbaiki setelah tanggal rilis.

![](/assets/images/soft-updater.png)

Hal ini dapat dilakukan secara GUI (*Graphical User Interface*) dengan:

  1. **Menjalankan perkakas Software Updater dari Unity Dash.**
  2. **Centang tombol check for updates**
  3. **Pasang (Install)**

Atau dengan menggunakan CLI (*Command Line Interface*) dengan mengetikkan perintah;

```bash
$ sudo apt-get update && apt-get upgrade
```

### 2. Install Media Codecs

``` bash
$ sudo apt-get install ubuntu-restricted-extras
```

### 3. Memindahkan Launcher ke bawah
Bagi pengguna Fedora, Launcher biasanya di atas atau di bawah, ubuntu secara default posisi launcher di sebelah kiri. Tapi sekarang Launcher dapat dipindahkan ke bawah dan ke samping kiri. Sebenarnya ini hanya masalah selera saja.

##### Pindahkakan launcher ke bawah

{% highlight bash %}
$ gsettings set com.canonical.Unity.Launcher launcher-position Bottom
{% endhighlight %}
![](/assets/images/launcher_bottom.png)

##### Pindahkan launcher ke samping kiri

{% highlight bash %}
$ gsettings set com.canonical.Unity.Launcher launcher-position Left
{% endhighlight %}
![](/assets/images/launcher_left.png)

### 4. Menghilangkan *Guest Session*

Ubuntu memungkin siapapun dapat login ke system tanpa password. Karena alasan keamanan, kita dapat menghilangkan Guest Session.

{% highlight bash %}
$ sudo sh -c "echo 'allow-guest=false' >> /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf"
{% endhighlight %}

### 5. Install Flash Player

Ubuntu tidak memasang Flash player secara bawaan. Flash player diperlukan untuk menjalankan flash media dalam peramban web. Flash palyer dapat dipasang dengan menggunakan perintah berikut ini di terminal.

{% highlight bash %}
$ sudo apt-get install flashplugin-installer
{% endhighlight %}

### 6. Enable 'Minimise on click'

Nah, biasanya apabila satu aplikasi kita buka dan jalankan, aplikasi tersebut dapat di-minimise, tapi pada Ubuntu, untuk dapat melakukan ini, harus dengan mengatur *launcher minimise* menjadi *true* dengan perintah seperti di bawah ini'

{% highlight bash %}
$ gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshell/ launcher-minimize-window true
{% endhighlight %}

### 7. Install Google chrome

Peramban web kesukaan developer. Ubuntu tidak menyertakan Chrome secara default di dalamnya. Untuk memasang google chrome, pertama yang harus kita lakukan adalah mengunduh paket chrome
{% highlight bash %}
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_i386.deb
{% endhighlight %}

kemudian melakukan instalasi dengan perintah
{% highlight bash %}
$ sudo dpkg -i --force-depends google-chrome-stable_current_i386.deb
{% endhighlight %}

### 8. Install Skype

![](/assets/images/skype.png)
{% highlight bash %}
$ sudo apt-get update && sudo apt-get install skype
{% endhighlight %}

### 9. Install Atom text editor

![](/assets/images/AtomEditor.png)

{% highlight bash %}
$ sudo add-apt-repository ppa:webupd8team/atom
$ sudo apt-get update
$ sudo apt-get install atom
{% endhighlight %}

### 10. Install Sublime Text 3

![](/assets/images/sublimetext3.png)

{% highlight bash %}
$ sudo add-apt-repository ppa:webupd8team/sublime-text-3
$ sudo apt-get update
$ sudo apt-get install sublime-text-installer
{% endhighlight %}

### 11. Install Telegram Messenger

![](/assets/images/telegram.png)

{% highlight bash %}
$ sudo add-apt-repository ppa:atareao/telegram
$ sudo apt-get update
$ sudo apt-get install telegram
{% endhighlight %}

### 12. Install 'Oh My ZSH!'

Oh My Zsh merupakan *framework open source* untuk mmengatur konfigutasi zsh terminal kita. Sejak melihat beberapa tutorial di youtube, saya penasaran bagaimana membuat terminal menjadi begitu menarik dan simple, ternyata yang digunakan adalah Oh My Zsh.

![](/assets/images/OhMyZsh.png)

Sebelumnya kita harus memasang zsh dan git-core terlebih dahulu;

{% highlight bash %}
apt-get install zsh
apt-get install git-core
{% endhighlight %}

Langkah berikutnya adalah;
{% highlight bash %}
$ wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
{% endhighlight %}

dan kemudian menggantikan terminal shell menjadi zsh

$ chsh -s 'which zsh'

lalu *restart*
{% highlight bash %}
$ sudo shutdown -r 0
{% endhighlight %}

Kira-kira penampakan terminal zsh saya kurang lebih seperti ini ![](/assets/images/myterminal.png)

Untuk informasi lebih lanjut tentang 'Oh My Zsh' dan cara installasi di ubuntu dapat merujuk ke [Getting oh-my-zsh to work in Ubuntu](https://gist.github.com/tsabat/1498393) dan Repository RobbyRussell tentang [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

### 13. Install Oracle VirtualBox
VirtualBox saya perlukan untuk mencoba beberapa distro lain untuk perbandingan dan tujuan belajar. Kalau sedang ngoprek Vagrant, virtualbox menjadi syarat yang harus diinstall sebelum menginstall Vagrant.

Pertama yang harus dilakukan adalah menambahkan repository VirtualBox ke dalam repo sistem dengan cara merubah berkas **/etc/apt/sources.list** dengan menambahkan;

```bash
## For Ubuntu 16.04 ("Xenial")
deb http://download.virtualbox.org/virtualbox/debian xenial contrib
```

Langkah berikutnya adalah menambahkan Public Key dari Oracle;

```bash
$ wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
$ wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
```
Jika sudah berhasil, selanjutnya adalah install virtual box dengan menggunakan perintah;

```bash
$ sudo apt-get update
$ sudo apt-get install virtualbox-5.1
```
Perintah tersebut akan menginstall virtualbox versi 5.1, jika sudah berhasil, virtualbox dapat dijalankan dengan perintah'

```bash
$ virtualbox
```
![](/assets/images/VirtualBox.png)

### 14. Install Aplikasi lain yang sering digunakan.
Langkah berikutnya adalah memasang aplikasi-aplikasi yang akan digunakan untuk keperluan kerja dan hiburan sehari-hari seperti aplikasi perkantoran(biasanya sudah ada secara *default*), editing gambar, music dan video player dan lain-lain sesuai kebutuhan.

{% highlight bash %}
$ sudo apt-get install inkscape gimp vlc audacity
{% endhighlight %}

Itulah 14 hal yang saya lakukan setelah install Ubuntu 16.04 LTS, semoga bermanfaat, saran dan masukan akan diterima dengan senang hati.
