## Konsep:

Semenjak rencana kita bakal pakai Dart untuk implementasi, berikut adalah cara untuk mempublish package Dart yang udah kita buat sehingga bisa dikonsumsi module/sistem lain yang terlibat dalam sistem aplikasi kita.
untuk mempublish package dalam Dart menggunankan Pub. Pub ini adalah platform yang digunakan di lingkungan Dart, berfungsi untuk berbagi atau menggunakan package dari sebuah sistem ke sistem yang lain.

Pub ini fungsinya sama seperti Maven bagi programmer java yang sudah sering menggunakan. Bagi yang belum pernah, perhatikan analogi berikut ini:
Dalam sebuah kelompok survey yang terdiri dari 3 orang (A,B,C), meneliti tentang pekerjaan impian di kota Buah. Kota Buah terdiri atas 2 distrik yaitu Pisang dan Jeruk.
A bertugas mencari survey di distrik Pisang, B bertugas mencari survey di distrik Jeruk, sedangkan C bertugas buat ngeprint hasil survey hehe, canda. C bertugas untuk menyimpulkan hasil survey kedua distrik di kota Buah.
untuk dapat menyimpulkan hasil survey C perlu mengetahui hasil dari A dan B oleh karena itu A dan B membagi hasil survey mereka melalui google drive. Setelah mengetahui hasil dari A dan B maka C bisa menyimpulkan hasil survey mereka.

Berdasarkan ilustrasi diatas, bayangkan A,B,C sebagai sistem yang berdiri sendiri dari satu dengan yang lainnya. A dan B ingin berbagi fungsi mereka dengan C karena C untuk melakukan fungsi sistemnya membutuhkan apa yang dimiliki A dan B.
Olehkarena itu A dan B mempublish fungsi mereka dalam bentuk package kedalam sebuah platform (google drive). platform berbagi fungsi inilah adalah Pub atau Maven dalam dunia Java.

## Apa itu Pub:

Secara singkat, Pub adalah tools untuk mengelolah Dart package. Dart package merupakan sebuah direktori yang berisi file pubspec. Pubspec berisi beberapa metadata tentang package tersebut. 
Selain itu, package dapat berisi dependensi (terdaftar di pubspec), Dart library, command-line apps, aplikasi web, resource, tes, gambar, atau lainnya. Jika sebuah aplikasi menggunakan satu package atau lebih, maka aplikasi itu sendiri harus berupa package.

https://user-images.githubusercontent.com/28759060/56457233-b3dcfe80-63a1-11e9-81e9-63e0cc231b01.png
sebuah package paling miniman terdapat lib direktori dan pubspec directori.

### File pubspec:
File pubspec.yaml adalah file yang berisikan informasi tentang library atau aplikasi yang dipublish. Contoh format pubspec:
```
name: my_app
dependencies:
  js: ^0.3.0
  intl: ^0.12.4
```
contoh lengkap:
```
name: newtify
version: 1.2.3
description: >-
  Have you been turned into a newt?  Would you like to be?
  This package can help. It has all of the
  newt-transmogrification functionality you have been looking
  for.
author: Natalie Weizenbaum <nweiz@google.com>
homepage: https://example-pet-store.com/newtify
documentation: https://example-pet-store.com/newtify/docs
environment:
  sdk: '>=2.0.0 <3.0.0'
dependencies:
  efts: ^2.0.4
  transmogrify: ^0.4.0
dev_dependencies:
  test: '>=0.6.0 <0.12.0'
```

mengenai penjelas lengkap field pada pubspec disarankan menuju link resmi pubspec berikut:
[pubspec field](https://www.dartlang.org/tools/pub/pubspec)

### Direktori lib
Kode dari fungsi/librari bertempat di bawah direktori lib dan bersifat publik untuk package atau sistem lain.
Kita dapat membuat hierarki apa pun di bawah direktori lib, sesuai kebutuhan. Sesuai ketentuan, implementasi kode ditempatkan di bawah lib / src. 
Kode di bawah lib / src bersifat private; package/sistem lain seharusnya tidak perlu mengimport src / .... Untuk membuat API di bawah lib / src publik, kita dapat mengekspor file lib / src dari file yang langsung di bawah lib.
untuk penjelasan resmin yang lebih detail disarankan untuk mengunjungi link berikut:
[package direktori](https://www.dartlang.org/guides/libraries/create-library-packages)


## Mempublish package Pub
Sebelum mempublish sebuah package pastikan format pubspec yang digunakan sudah benar sesuai ketentuan. Beberapa ketentuan perlu diikuti agar package kita bisa digunakan dan mudah dimengerti oleh pengguna package yang kita publish.
Ada kebutuhan tambahan ketika akan mempublish package kita. diantaranya:
* Menyertakan file lisensi (lisensi, hak cipta) yang mengandung open-source licence. Dart menyarankan menggunakan [BSD-License](http://opensource.org/licenses/BSD-2-Clause).
* Besar ukuran package harus kurang dari 10MB setelah kompresi. Jika ukuran lebih besar disarankan untuk dipecah menjadi beberpa package.
* Package seharusnya hanya memiliki dependency yang dihost saja. Dependency git diperbolehkan tetapi sangat tidak dianjurkan; 
tidak semua orang yang menggunakan Dart telah menginstal Git, dan dependensi Git tidak mendukung version resolution.
* Alangkah baiknya kita juga menyertakan file-file penting seperti, CHANGELOG dan README

Jika semuanya sudah tepenuhi mulailah untuk mempublih package yang sudah kita buat. Gunakan command berikut ini untuk mempublish package:
```
$ pub publish
```
Tetapi jika ingin mengecek file yang dipublish sebelum benar-benar mempublish ke pub, gunakan command berikut:
```
$ pub publish --dry-run
```
pub akan memeriksa apakah file package yang dipublish sudah benar.
```
Publishing transmogrify 1.0.0
    .gitignore
    CHANGELOG.md
    README.md
    lib
        transmogrify.dart
        src
            transmogrifier.dart
            transmogrification.dart
    pubspec.yaml
    test
        transmogrify_test.dart

Package has 0 warnings.
```
Setelah package berhasil dipublish pub user lainnya sudah dapat menggunakan package kita. Untuk menggunakan package yang sudah kita publish cukup mudah. Yaitu dengan menambahkan dependency ke dalam file pubspec pengguna package.
```
dependencies:
  example: ^1.0.0
```

## Menggunakan Pub dependency
Dependency adalah salah satu konsep inti pada pub. Dependency adalah package/sistem lain yang dibutuhkan package/sistem kita agar dapat berfungsi. Dependency ditentukan didalam file pubspec kita. Contoh:
```
dependencies:
  freshgradquery: ^1.0.0
```
Jika kita menginginkan sumber yang lebih spesifik maka syntax pada pubspec sebagai berikut:
```
dependencies:
  freshgradquery:
    hosted:
      name: freshgradquery
      url: http://some-package-server.com
    version: ^1.0.0
```

### Tipe dependency
Ada beberapa tipe source yang didukung oleh pub diantara lain:
### 1. SDK
Untuk saat ini source SDK yang didukung adalah dalam bentuk flutter. contoh:
```
dependencies:
  flutter_driver:
    sdk: flutter
    version: ^0.0.1
```
### 2. Hosted packages
Kita dapat mendownload dari pub
```
dependencies:
  freshgradquery: ^1.0.0
```
Atau dapat menggunakan server buatan sendiri
```
dependencies:
  freshgradquery:
    hosted:
      name: freshgradquery
      url: http://some-package-server.com
    version: ^1.0.0
```
### 3. Git packages
Dapat digunakan ketika kita belum ingin membulish package keseluruh pengguna pub.
```
dependencies:
  kittens:
    git: git://github.com/owner/target_repo.git
```
Atau dapat kita spesifikasikan berdasarkan sebuah branch.
```
dependencies:
  kittens:
    git:
      url: git://github.com/owner/target_repo.git
      ref: target-branch
```
Jika url yang digunakan adalah git private.
```
dependencies:
  kittens:
    git: git@github.com:owner/target_repo.git
```
### 4. Local source
```
dependencies:
  transmogrify:
    path: /Users/user/freshgradapp
```
Setelah dependency telah ditambahkan kedalam pubspec, selanjutnya kita perlu menginstall package tersebut a dengan menjalankan command berikut:
```
cd <path-to-root-of-my_app>
pub get
```
Perintah pub get menentukan kebergantungan aplikasi kita pada package mana saja dan menempatkannya dalam cache sistem pusat.
Untuk dependency git, pub mengkloning repositori git. Untuk dependency yang dihosting, pub mengunduh paket dari situs Pub

### Importing package
Gunakan prefix **import 'package:** untuk mengimport library yang ditemukan. Berikut ilustrasi menggunkan package yang diimport:
```
import 'package:js/js.dart' as js;
import 'package:intl/intl.dart';
```
Jika dependency terdapat perubahan gunakan command berikut:
```
$ pub upgrade
```
atau
```
$ pub upgrade <specific-dependency-name>
```

## Untuk informasi resmi
* [Pub Getting Started](https://www.dartlang.org/tools/pub/get-started)
* [Pub Publishing](https://www.dartlang.org/tools/pub/publishing)
* [Pub Dependencies](https://www.dartlang.org/tools/pub/dependencies)
* [Pub Commands](https://www.dartlang.org/tools/pub/cmd)

NOTE: Keep in mind that publishing is forever. As soon as you publish your package, users will be able to depend on it. Once they start doing that, removing the package would break theirs. To avoid that, pub strongly discourages deleting packages.

