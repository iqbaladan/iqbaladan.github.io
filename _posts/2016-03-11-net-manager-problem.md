---
layout: post
cover: false
title: Network Manager - Deviced not managed
date: 2016-03-11 10:18:00
tags: Linux
subclass: 'post tag-linux'
categories: 'iqbaladan'
navigation: True
logo: 'assets/images/iqbal.png'
#cover: 'assets/images/cover8.png'
disqus: true
---
---

*Network manager* saya tidak berjalan dengan baik, pesan error yang muncul adalah "**Network Manager: Deviced not managed**", dengan sedikit googling, solusi dari masalah saya bisa diselesaikan, kadang hanya butuh sedikit usaha untuk menyelesaikan sedikit masalah, tanpa perlu panik tentunya, boleh jadi orang lain juga pernah mengalami masalah yang sama dan kabar baiknya adalah mereka mendokumentasikan hasil kerja mereka.

Berikut ini adalah solusinya;

{% highlight bash %}
$ nano /etc/NetworkManager/NetworkManager.conf
{% endhighlight %}

{% highlight bash %}
[main]
plugins=ifupdown,keyfile
[ifupdown]
managed=false
{% endhighlight %}

Ganti *false* ke *true*, kemudian *reboot* sistem Linux. Masalah selesai, sekarang *Aplet Network Manager* kita sudah dapat kembali secara normal.
