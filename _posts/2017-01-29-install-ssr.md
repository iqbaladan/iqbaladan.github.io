---
layout: post
cover: true
title: Install Simple Screen Recorder di Ubuntu 16.10
date: 2017-01-29 17:01:00
tags: Linux Ubuntu
subclass: 'post tag-linux'
categories: 'iqbaladan'
navigation: True
#logo: 'assets/images/iqbal.png'
#cover: 'assets/images/cover8.png'
disqus: true
---

sudo add-apt-repository ppa:maarten-baert/simplescreenrecorder

 SimpleScreenRecorder is a feature-rich screen recorder that supports X11 and OpenGL. It has a Qt-based graphical user interface. It can record the entire screen or part of it, or record OpenGL applications directly. The recording can be paused and resumed at any time. Many different file formats and codecs are supported.

More information can be found here:
http://www.maartenbaert.be/simplescreenrecorder/
 More info: https://launchpad.net/~maarten-baert/+archive/ubuntu/simplescreenrecorder
Press [ENTER] to continue or ctrl-c to cancel adding it

gpg: keybox '/tmp/tmpiwm6ns70/pubring.gpg' created
gpg: /tmp/tmpiwm6ns70/trustdb.gpg: trustdb created
gpg: key 409C8B51283EC8CD: public key "Launchpad PPA for Maarten Baert" imported
gpg: Total number processed: 1
gpg:               imported: 1
OK

sudo apt-get update
sudo apt-get install simplescreenrecorder
# if you want to record 32-bit OpenGL applications on a 64-bit system:
sudo apt-get install simplescreenrecorder-lib:i386


Referensi:
1. http://www.maartenbaert.be/simplescreenrecorder/
