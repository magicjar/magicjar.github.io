---
layout: post
title: "Membuat Website Statis Cepat, Mudah, dan Gratis dengan Jekyll"
date: 2020-06-02 05:04:14 +0700
author: dawntale
categories: jekyll blog
tags: jekyll blog website gratis
comments: true
cover: /assets/images/2020/05/logo-jekyll.png
---
Siapa yang tak mengenal website? Tanpa disangka, setiap hari kita mengaksesnya tanpa sadar. Mulai dari website sosial media, blog, sampai website jual-beli atau yang disebut dengan e-commerce.

Pada dasarnya website dibagi menjadi 2, statis dan dinamis. Website dinamis menggunakan bahasa server-side seperti PHP, Ruby on Rails, ASP, dll. Dengan demikian konten akan diambil dari database atau file di server dan ditampilkan kepada pengguna akhir. Sedangkan website statis biasanya dibuat dari HTML dan CSS sehingga isi dari HTML itulah yang akan ditampilkan kepada pengguna.

Pada pembahasan kali ini, kita akan membuat website statis yang berasa dinamis dengan Jekyll sampai online.

* Content
{:toc}

## Apa itu Jekyll?
>Jekyll is a simple, blog-aware, static site generator perfect for personal, project, or organization sites. Think of it like a file-based CMS, without all the complexity.

Jekyll adalah generator web statis yang memungkinkan kamu untuk membuat website statis namun dengan kemudahan-kemudahan yang ditawarkan oleh website dinamis seperti WordPress atau Drupal.

Jekyll dibuat oleh salah satu pendiri / co-founder GitHub, Tom Preston-Werner, mengunakan bahasa pemrograman Ruby. Jekyll selanjutnya diambil alih oleh Parker Moore yang mempunyai tujuan untuk mengeluarkan versi pertama Jekyll.

Jekyll mengolah Markdown dan Liquid untuk diproses menjadi website statis yang siap disajikan oleh semua web server.

## Apa alasan menggunakan web statis?
Pilihan CMS (Content Management System) seperti Wordpress, Drupall, Joomla memang bagus untuk membangun website besar dan rumit. Tapi untuk blog, website pribadi, atau portfolio online, website statis sudah sangat mampu memberikan apa yang kamu inginkan berikut keuntungan dengan keuntungannya.

* **Murah.** Meskipun CMS yang disebutkan tadi dapat digunakan secara gratis, namun untuk hosting mungkin butuh biaya.
* **Mudah.** Kamu tidak perlu mempelajari bahasa pemrograman PHP, ASP, Ruby dan SQL untuk membuat sebuah website statis. Dengan hanya bermodal pengetahuan HTML dan CSS, kamu sudah dapat membuatnya.
* **Cepat.** Karena tidak memakai database dan pemrosesan didalam server. Web statis cenderung lebih cepat dalam hal *page-load* karena server tinggal menampilkan apa yang sudah ada tanpa ada proses lebih lanjut.
* **Aman.** Tidak ada database yang perlu diamankan dari tangan hacker.

## Kebutuhan system
Karena Jekyll merupakan Ruby Gem, untuk dapat memakainya kita harus menginstall terlebih dahulu Ruby versi 2.5.0 keatas. Jika kamu ingin deploy websitenya ke GitHub Pages, maka kamu perlu menginstall `git` atau dapat menggunakan GitHub Client.

## Installasi Jekyll

Jalan paling mudah untuk menjalankan Jekyll di Windows adalah dengan menginstall [RubyInstaller](https://rubyinstaller.org/downloads).

1. Download `Ruby+Devkit` dari website RubyInstaller Downloads. Ingat download **Ruby+Devkit**, jangan yang lain. Install dengan opsi default, tidak perlu diubah-ubah.

2. Buka CMD dan install Jekyll gem dan bundler gem dengan command berikut.

    ``` sh
    gem install jekyll bundler
    ```

3. Cek apakah Jekyll sudah terpasang dengan benar.

    ``` sh
    jekyll -v
    ```

## Membuat blog baru

1. Buka CMD dan pindah ke lokasi yang diinginkan misal D:\website

    ``` text
    cd D:\website
    ```

2. Buat situs Jekyll baru didalam folder website dengan nama blogbaru

    ``` sh
    jekyll new blogbaru
    ```

3. Pindah ke folder situs Jekyll yang baru dibuat.

    ``` sh
    cd blogbaru
    ```

4. Build agar dapat disajikan dan diakses dari lokalhost

    ``` sh
    bundle exec jekyll serve
    ```
    atau 
    ``` sh
    jekyll serve
    ```

5. Buka browser dan pergi ke [localhost:4000](localhost:4000)

### Membuat postingan baru

Untuk membuat postingan baru, tambahkan file baru didalam folder `_posts` dengan format berikut.

``` text
TAHUN-BULAN-TANGGAL-judul.md
```

Contoh:
``` text
2020-12-12-postingan-baru.md
2020-12-13-cara-membuat-website-dengan-jekyll.md
```

Semua postingan blog wajib mengikuti format standar diawali dengan `front matter` yang biasanya digunakan untuk mengatur layout dan hal lain seperti judul, kategori, dan tag.

``` markdown
---
layout: post
title: "Cara Membuat Website Statis"
categories: blog
tags: website jekyll
---
Cara cepat untuk membuat website statis adalah dengan menggunakan Jekyll.
```

Jekyll akan langsung otomatis membuild setiap kali kamu menyimpan file yang kamu ubah, dan akan langsung dapat diakses.

### Menambah gambar dan tautan

Untuk menambah gambar atau media lainnya, kamu harus membuat folder bari di projek root dengan nama `assets`. Tempatkan semua gambar dan media lainnya didalam folder ini agar dapat ditautkan didalam postingan.

Untuk menambah gambar:

``` markdown
![Alt gambar yang ditautkan](/assets/gambar.jpg)
```

Untuk menautkan file:

``` markdown
..kamu dapat mengunduhnya menggunakan [link ini](/assets/download.zip)
```

### Membuat draft

Draft dibuat tanpa menyertakan tanggal didalam nama filenya dan masukkan file draft didalam folder `_drafts`. Folder ini akan memastikan bahwa draft tidak akan ikut dibuild pada saat kamu menyimpan perubahan isi draft.

``` text
├─ _drafts
│  └── draft-postingan.md
```

Untuk preview draft, jalankan perintah `jekyll serve --drafts`. Sistem akan otomatis menambahkan tanggal publikasi sehingga draft akan tampil sebagai postingan terbaru.

## Mengganti tema Jekyll

Jekyll mempunyai sistem tema yang simpel dan *extensible*.
Tema Jekyll dapat dicari di beberapa galeri tema seperti:

* [jekyllthemes.org](http://jekyllthemes.org)
* [jekyllthemes.io](http://jekyllthemes.io)
* [jekyll-themes.com](http://jekyll-themes.com)

Misanya kamu ingin mengubah tema Jekyll dengan tema [Architect](https://github.com/pages-themes/architect)

1. Ubah nama tema didalam `_config.yml` dengan `jekyll-theme-architect`.

    ``` yaml
    ...

    theme: jekyll-theme-architect

    ...
    ```

2. Agar kamu dapat melihat preview tema di komputermu, tambahkan ini di `Gemfile`.

    ``` yaml
    ...

    # This is the default theme for new Jekyll sites. You may change this to anything you like.
    # gem "minima", "~> 2.0"

    gem "github-pages", group: :jekyll_plugins

    ...
    ```

3. Lalu jalankan perintah

    ``` sh
    bundle install
    ```

**Catatan:** GitHub Pages hanya support sebagian tema saja. Kamu dapat melihat tema-tema yang disupport GitHub melalui tautan berikut ini. [GitHub Pages Theme](https://pages.github.com/themes/)

## Deploy ke GitHub Pages

>Jekyll dapat dideploy di `GitHub User Page` dan `GitHub Project Page`. Untuk *GitHub User Page* mengunakan branch / cabang `master` sedangkan *GitHub Project Page* menggunakan branch / cabang `gh-pages`.

**Catatan:** Tutorial ini untuk *deploying* Jekyll ke GitHub User Page. Untuk GitHub Project Page akan saya tambahkan berkala.

### GitHub User Page

Untuk mendeploy website yang baru saja dibuat ke GitHub Pages, kamu membutuhkan akun GitHub. Daftar terlebih dahulu jika belum punya, gratis.

1. Pastikan dahulu bahwa komputer kamu sudah terinstall Git. Kamu dapat mengunduhnya dan install di [Git untuk Windows](https://git-scm.com/download/win) bisa juga menggunakan GitHub Desktop. Sebelum lanjut, cek dahulu dengan membuka terminal (CMD / PowerShell) dan jalankan perintah dibawah ini.

    ``` sh
    git
    ```

2. Buat repository baru di GitHub dan beri nama `*username*.github.io`.
3. Buka terminal lalu pindah ke *directory* situs Jekyll yang kamu buat.

    ``` sh
    cd D:\website\blogbaru
    ```

4. Jalankan perintah `git clone`.

    ``` sh
    git clone https://github.com/username/username.github.io.git
    ```

5. Tambahkan situs Jekyll-mu ke git.

    ``` sh
    git add --all
    ```

6. Commit.

    ``` sh
    git commit -m "Website statis Jekyll"
    ```

7. *Push* / unggah semua file ke repository.

    ``` sh
    git push origin master
    ```

GitHub Pages akan secara otomatis mem-build situsmu. Kunjungi `username.github.io` untuk melihat situsmu yang sudah mengudara.

### GitHub Project Page
Tunggu updatenya.

## Kesimpulan

Jekyll menawarkan kemudahan untuk membuat sebuah website statis. Jekyll mampu mempercepat pembuatan website statis karena ia menggunakan sistem berbasis file markdown dan layout dinamis. Dengan sistem ini kamu tidak perlu menulis semua tag html dari *header* sampai ke *footer* beserta konten web. Dengan support dari GitHub Pages, Jekyll dapat dideploy dengan cepat dan mudah serta gratis.